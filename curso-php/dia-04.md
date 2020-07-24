# Día 4

Terminamos el siguiente caso de uso, put-user, que crea un nuevo usuario en
nuestro sistema

Aprendemos sobre los middlewares de query/command bus. Crearlos, configurarlos
y cómo funcionan. Son como los middlewars de Slim, pero con promesas, claro.

Comenzamos con el concepto de Repositorio. La interfaz es parte del Modelo, parte
del Dominio, y estará junto al modelo de User: entidad, excepciones,...

Las implementaciones de los repositorios... para el siguiente día

## Notas tomadas

CQRS sirve más para APIs, para aplicaciones web quizá no cuadre muy bien, porque
en una aplicación web las peticiones hacen algo y devuelven algo, todo en la
misma petición, para ser más eficientes

Petición PUT con `curl`:

```
curl -s \
    -XPUT \
    -H "Content-Type: application/json" \
    localhost:8000/users/10 
    -d'{"name":"Engonga"}'
```

- `-XPUT`: es una petición HTTP PUT
- `-H "Content-Type: application/json"`: envía esta cabecera, le estamos diciendo
el content type de la petición
- `-d'{"name":"Engonga"}'`: el body de la petición, el contenido, en formato
JSON, como hemos indicado con la cabecera

Normalmente, la instancia de la entidad `User` se creará en el Controlador,
con el `UserTransformer`. Esto es conveniente, porque si añadimos/quitamos 
propiedades al `User`, solo deberemos cambiar el transformer

En cambio, si le pasamos todos las propiedades al comando, al añadir/quitar cosas
del usuario, tendremos que cambiar el comando, el handler,...

El command bus no devuelve nada, el query bus devuelve un resultado:

```
$queryBus
    ->ask($query)
    ->then(function ($result) {
        return Response($result);
    });

$commandBus
    ->execute($command)
    ->then(function () {
        return Response();
    });
```

Como código de respuesta a una petición PUT, no deberíamos devolver un 
`HTTP 201` (Created), porque no estamos seguros si se ha creado o no, es asíncrono
y la petición se puede terminar antes de que realmente insertemos. Una opción
válida es `HTTP 202` (Accepted) para decir:
 
> ok, acepto lo que me has mandado, en un futuro te lo insertaré

Los command handler no devuelven nada, pero su método `handle()` sí pueden devolver
una promesa (aunque vacía), porque tarde o temprano trabajaremos con servicios
como la base de datos de forma asíncrona, y deberemos devolver la promesa, para que
pueda ser encadenada.

**Middlewares**

Los middleware, en el Dominio, son parte del Dominio, de lógica que debemos
hacer nosotros y sólo nosotros, no son parte del framework

Un middleware va a nivel de bus, de todo el query o command bus, por lo que
todos los commandos que pasen por el bus, serán procesados por el middleware

Algunos middleware son solo para ciertos tipos de comandos, para ello se usan los
`Drift\CommandBus\Middleware\DiscriminableMiddleware`

Para ello hay que implementar el método `onlyHandle()`

```
public function onlyHandle(): array {
  return [
    PutUser::class
  ];
}
```

Los middleware funcionan como los de Slim, nos pasan un `callable $next`, y
podemos hacer cosas antes y después del siguiente middleware. Un middleware
puede hacer acciones en los dos sentidos del bus, del pipe: 

1. Controller -> Handler
2. Handler -> Controller

Y la función devuelve una promesa

```
public function execute($command, callable $next) {
  // hago cosas antes
  return $next($command)
    ->then(function ($result) {
      // hago cosas después
    });
}
```

Para cortar la ejecución en la cadena de middlewares, se puede devolver una promesa
rejected o lanzar una excepción

Hay que configurar los middlewares como servicios, sin tag ninguna, porque son
servicios normales y corrientes

Y tambien hay que configurar los middleware para el query/command bus,
modificando `services.yml`:

```
command_bus:
    query_bus:
    command_bus:
        middlewares:
            - Domain\Middleware\CheckUserNameLength
```

**Repositorios**

Muy bien, ahora y solo ahora que tenemos ya los casos de uso de get-user y 
put-user, es cuando podemos empezar a trabajar con la capa de persistencia

El Repositorio forma parte de nuestro modelo, todavía no sería Infraestrutura

Como es del modelo, y del usuario, lo ponemos en `Domain/Model/User`, y será una
interfaz

**desarrollar con mis palabras** diferencias entre `persist` y `flush` en un ORM,
unit of work, entidades que el ORM conoce al hacer un `find`...

Discutiendo sobre qué métodos debería tener nuestro Repositorio, hablamos sobre
las diferencias entre `persist` y `flush` en los ORM. Pero antes, un poco de
cómo trabaja un ORM.

Cuando en un ORM, hacemos un `find` para buscar una entidad, el ORM se apunta en
su *unit of work* (UOW) qué entidades ha usado. En el UOW, el ORM se guarda las
entidades que conoce. 

Al hacer `flush`, el ORM actualiza la base de datos de las entidades que conoce,
ninguna más. Así, si hemos modificado/creado alguna entidad que no tiene apuntada
en su UOW, ésta no será actualizada.

Con `persist`, le decimos al ORM que añada una entidad a su UOW, para así, cuando
hagamos `flush`, la tenga en cuenta.

`persist` no tiene que ver con guardar, o crear una nueva entidad. Tiene que ver
sobre cómo trabaja un ORM.

En nuestro Repositorio no vamos a utilizar conceptos de ORM, eso será la
implementación. Usaremos métodos que debe conocer nuestro Domino: `save`, `find`
y `delete`, por ahora.

Todo lo que definamos en la interfaz `UserRepository` debe ser de Dominio, las
implementaciones del repositorio usarán transformers para convertir los datos
de la infraestructura a los datos del Dominio, por ejemplo, una excepción del ORM
a una excepción del Dominio

Cuando ya tenemos la interfaz, ya podemos modificar los query/command handler
para que la usen, aunque todavía no funcionará porque no tenemos implementación

## Deberes

- Hacer el caso de uso de borrar usuario, utilizando el Repositorio. No funcionará
todavía, pero en conceptualmente sabes hacerlo
