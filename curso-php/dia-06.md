# Día 6

Hoy trabajamos con bases de datos, DBAL y diferentes implementaciones de un
repositorio.

## Notas tomadas

DBAL = database abstract layer

Es como una capa de abstracción por encima de MySQL, Postgres, MSSQL, SQLite,...

Sirve para escribir código SQL que no esté ligado a ninguna base de datos

Luego, por debajo, o una vez ya has elegido el cliente SQL (MySQL,...) entraría
el ORM

El DBAL que mete DritfPHP, depende del DBAL de Doctrine, que viene de Symfony

Como es un bundle, hay que activarlo en el `bundles.php` y `composer.json`

```
// composer.json
"require": {
    "drift/dbal-bundle": "*",
    "clue/reactphp-sqlite": "*",
}
```

```
// bundles.php
  Drift\DBAL\DBALBundle::class => [ 'all' => true ],
```

También hay que configurar la conexión en `services.yml`

```
dbal:
    connections:
        main:
            driver: mysql
            host: 127.0.0.1
            port: 3306
            user: root
            password: root
            dbname: users
```

Pero antes de empezar a usar esta conexión... vamos a por los tests

¿Dónde creamos la implementación de DBAL? No es todo de Dominio. Es una parte
del Dominio, que va a hablar con Infraestructura. Entonces, lo ponemos en
algo intermedio, pero fuera del Dominio: `src/DBAL/Model/User`

Ahí crearemos un repositorio `DBALUserRepository`, y habrá que inyectar una 
conexión, una conexión DBAL (que saldrá de la configuración de antes),
la conexión será del tipo `Drift\DBAL\Connection`.

¿Cómo testeamos? Ya tenemos los tests de la interfaz `UserRepository`, así que
los tests los tenemos hechos ya. Solo faltaría extender del test correcto,
crear el repositorio correcto, y comenzar con la implementación de 
`DBALUserRepository`

De hecho, como ya están todos los tests, esto sería TDD puro y duro

Para hacer tests que ataquen a una base de datos, hay que crear una conexión
real a una base de datos real, crear las tablas, crear datos de prueba,
testear, y limpiar todo

Al utilizar un repo DBAL, como utilizamos una conexión DBAL, para los tests,
podemos utilizar una conexión DBAL a SQLite. No es exactamente la base de datos
a la que vamos a atacar en producción, pero como tenemos DBAL por medio,
podemos cambiar la base de datos real. Lo que nos interesa testear en este punto
es la conexión DBAL

Hay que crear la conexión, y crear las tablas:
[`DBALUserRepositoryTest`](https://github.com/rchavarria/driftphp-skeleton/blob/master/test/DBAL/Model/User/DBALUserRepositoryTest.php)

En `DBALUserRepositoryTest`, tenemos un `User`, con lo que habría que transformar de
`User` a otra estructura que no dependiera del Dominio. Por ahora, lo haremos
en el repositorio, porque solo tenemos una trasformación. Si tuviéramos varios
repositorios, varias transformaciones, lo extraeríamos a un Transformer,
como hicimos con el Controller

El método `save` de nuestro repositorio, no es un *insert* exactamente, y tampoco
es un *update*, entonces es un... *upsert*. ¡¡¡Juas!!! internamente es: busco
por id, si encuentro, hago update, si no encuentro hago insert => `upsert`.
Curioso el concepto

Las conexiones DBAL de DriftPHP ya devuelven promesas, así que el repositorio
tiene que devolver lo que devuelva `upsert`

Para implementar el `find` en el `DBALUserRepositoryTest` usamos el query builder:

```
$queryBuilder = $this
  ->connection
  ->createQueryBuilder();

$queryBuilder->select('*')
  ->from('users', 'u')
  ->where('u.uid = ?')
  ->setParameters([ $uid ])
  ->setMaxResults(1);

return $this
  ->connection
  ->query($queryBuilder)
  ->then(function (Result $result) {
    $userAsArray = $result->fetchFirstRow();
    if (is_null($userAsArray)) {
      throw new UserNotFoundException('User not found');
    }

    // transformar un array en un objeto User
    return new User(
      $userAsArray['uid'],
      $userAsArray['name']
    );
  });
```

Las trasformaciones de `array` a `User` y al revés, son las mismas que teníamos
en el Controller, pero de hacerlo con Transformers, lo haríamos en Transformers
distintos, para no mezclar conceptos. El código será el mismo, pero el concepto
no. Cuidadín con esto.

Ya tenemos muchas piezas:

- Interfaz del repositorio
- Varias implementaciones del mismo
- Command y Query handlers que usan el repositorio inyectado
- Autowiring en `services.yml`

Así, ya podemos unirlas todas para poder testear el API entero, la aplicación
entera:

- Como implementación del repo, usamos el `DBALUserRepository`
- La conexión que inyectará, está definida en las conexiones DBAL de `services.yml`.

**aqui falta enlace a la documentacion de driftphp/dbal para ver cómo se inyecta, cuando
hay una conexion o cuando hay varias, que se hace mucha magia con el autowiring**

Un poco de código SQL para crear la base de datos y la tabla que usamos:

```
create database usersdb;

use usersdb;

create table users
(
    uid  varchar(64) default '' not null primary key,
    name varchar(255)           not null
);
```

## Deberes

## Referencias

- [DBAL for ReactPHP](https://github.com/driftphp/reactphp-dbal)
- [DriftPHP DBAL adapter](https://github.com/driftphp/dbal-bundle)
- Clase donde se crea una conexión a SQLite y se crea una tabla para los test
de un repositorio DBAL:
[`DBALUserRepositoryTest`](https://github.com/rchavarria/driftphp-skeleton/blob/master/test/DBAL/Model/User/DBALUserRepositoryTest.php)
