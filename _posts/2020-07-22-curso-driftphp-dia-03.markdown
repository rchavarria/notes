---
title: "Curso DriftPHP: día 3"
categories:
- Cursos
- PHP
---

Revisamos el caso de uso para buscar un usuario.

Continuamos por nuestra cuenta con el segundo caso de uso: crear un usuario

Gestión de errores con promesas, `otherwise`

Diferencias entre POST, PUT y PATCH, verbos HTTP

Comunicación desde el Framework o la Infraestructura con nuestro Dominio. El
Dominio no depende de nada.

<!-- more ->

## Notas tomadas

Al modificar `services.yml` (lo que hicimos para registrar los handlers para
que se manejen las queries) lo que estamos haciendo es decir a DriftPHP que 
registre unos servicios, a partir del namespace y de la ruta de directorios.
Este `services.yml` viene de Symfony. DriftPHP usa varios componentes de Symfony
(y ReactPHP). La configuración (rutas, servicios,...) viene de Symfony.

Al poner el tag: `query_handler` estamos diciendo que los servicios de ese 
namespace son query handlers

Como la relación es 1 a 1, con el casting del método `handle` del query handler,
DriftPHP sabe encontrar qué query handler maneja qué query

Es el bundle (command-bus-bundle) la librería que hace esta relación

Los handlers se registran como servicios (con un determinado tag) porque pueden
tener otros servicios inyectados

Documentación sobre [servicios en Symfony](https://symfony.com/doc/current/service_container.html)

El query handler también devuelve una promesa, porque si en algún momento
accede a base de datos, disco,... no podrá hacerlo síncronamente, si no que lo hará
a través de ReactPHP y de forma asíncrona

Las promesas pueden ser

- *fulfilled*: una fulfilled promise tiene un valor
- *rejected*: tiene una excepción, un error, en lugar de lanzar excepcioens,
lo que hacemos es devolver promesas rejected con `reject`, una función de
ReactPHP

Marc es muy de la forma de trabajar así: digamos que vamos a tener un modelo de
usuario, y una excepción. En lugar de poner todas las excepciones juntas, usa
una aproximación más de DDD. en `/Domain/Model` crea una carpeta `User` (el
*bounded context* `User`) y ahí mete todo: modelo, excepciones, repositorios,...

Con un código como éste, estamos capturando promesas rejected, estamos
gestionando los errores. Incluso se pueden capturar varios tipos de excepciones:

```
  ->then()
  ->otherwise(function (UserNotFoundException $exception) {})
  ->otherwise(function (CoreException $exception) {})
  ->otherwise(function (Exception $exception) {})
```

Dentro del `otherwise`, podemos lanzar una excepción o si estamos en el Controller
podremos devolver una respuesta con un error

```
->otherwise(function (UserNotFoundException $exception) {
  throw $exception;
});

->otherwise(function (UserNotFoundException $exception) {
  return new Response('Not found', 404);
});
```

Symfony nos permite inyectar la `Request` en el Controlador, o incluso los
parámetros de la ruta:

```
public function __invoke(Request $request) {}

public function __invoke(string $uid) {}
```

**Importante**

La capa de Dominio es la capa central. El Dominio no depende de ninguna otra
capa, el resto de capas son las que dependen del Domino. Mi capa del framework
puede acceder a mi capa de Domino, pero mi capa de Dominio no debe acceder a mi
capa del framework, ni a la de Infraestructura

Como el framework puede depender del Dominio, el Controlador puede recibir un
objecto `User`, que es parte del Dominio

Podemos tener *transformers*, que conviertan de un array de la `Request` a un
`User` del modelo, y al revés, de un `User` del modelo a un array para generar la
`Response`. Pero estos *transformers* solo se pueden usar en el Controlador

Toca hacer una petición PUT, para crear un usuario, put-user, ese sería el
nuevo caso de uso

Las peticiones PUT y POST son distintas, y no tienen nada que ver con crear
o actualizar. Son distintas por el concepto de idempotencia. POST no se
puede utilizar para modificar.
 
idempotencia: una acción que se puede realizar varias veces, y el resultado final
es siempre el mismo. PUT es idempotente, POST no lo es

Nosotros vamos a utilizar peticiones PUT para crear usuarios, pero es el cliente
quien debe generar el `uid` del `User`. Si `uid` lo genera nuestro
Controlador debemos usar POST. Es cuestión de quién genera el id. Nosotros hemos
decidido que el `uid` se genere fuera, lo genera el cliente

El verbo http para modificar un usuario, para cambiar datos, es PATCH, no es PUT,
ni POST

## Deberes

- Añadir una ruta para añadir usuarios, me van a decir el uid y el nombre del
usuario desde fuera
- Cómo tiene que ser la petición `curl` para mandar datos como el nombre
mediante un PUT

### Peticiones PUT con `curl`

Con `-X <method>` podemos hacer distintas peticiones HTTP

El uid se lo paso en la URL, `curl -s -X PUT localhost:8000/users/<uid>`

¿Y el nombre?

## Referencias

- [Servicios en Symfony](https://symfony.com/doc/current/service_container.html)
