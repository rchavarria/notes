# Día 8

Ponemos en marcha RabbitMQ como event bus, y a escuchar Eventos de Dominio
en varios servers

Creamos una optimización para tablas con pocas escrituras (save o delete) y muchas
lecturas, de forma que con cada Evento de Dominio, se actualice el contenido de
la tabla en memoria

## Notas tomadas

Para que un event bus sea asíncrono, algunas arquitecturas como Symfony, lo que
hacen es poner un middleware en el bus, que coge los eventos y los mete en una
cola de RabbitMQ. Luego, hay un consumer que saca de la cola y la vuelve a meter
al bus. Pero el middleware tiene que meter algo para que los eventos no estén 
dando vueltas como tontos

Lo que hace Drift, es tener dos buses, el event bus, cuyos eventos se meten
en RabbitMQ, y el *inline event bus*, donde el consumer de la cola mete los 
eventos al otro bus

    event -> middleware -> rabbit -> consumer -> inline event bus

Añadimos la dependencia en `composer.json`: `drift/amqp-bundle`

En `bundles.php` no hace falta hacer nada, es el event bus el que lo monta

En `services.yml`

```
event_bus:
    exchanges:
        <nombre-de-mi-exchange>: <nombre-del-exchange-en-rabbit>
    router:
        _all: <nombre-de-mi-exchange>
    async_pass_through: true
    async_adapter:
        amqp:
            host: 172.168.1.143
```

`async_pass_through` significa que si queremos que el evento que se meta en el
event bus, además de meterse en la cola RabbitMQ, siga hacia adelante, pase
hacia adelante, para consumirse en ese momento en el servidor internamente
(pass through)

Si no queremos que se consuma internamente, pondremos `false`

Ahora, hay que configurar los exchanges en RabbitMQ

Vamos a `http://localhost:15672`, la consola de RabbitMQ, entramos con `guest`/`guest`

Vamos a Exchanges, y creamos uno, que se llame `events_amqp` (como le hayamos
puesto en `services.yml`). Tiene que ser de tipo `fanout`, para que los eventos
se envíen a todos los que estén conectados al exchange

Al arrancar el server, podemos indicar por parámetros al arrancarlo, que escuche
de un exchange, de una cola

```
php vendor/bin/server watch 0.0.0.0:8000 --exchange=my-exchange
```

`my-exchange` es el nombre que le hemos dado en `services.yml`, no el nombre
del exchange en RabbitMQ

Con `--help` tenemos todos los parámetros que podemos pasar al server

Así, podemos arrancar varios server escuchando de ese exchange. De esta forma,
la petición la recibe un server, que emite el evento, pero el evento lo reciben
y consumen todos los servers

### Mantener sincronizada la tabla en memoria

Lo que  vamos a hacer ahora es tener una copia de nuestra tabla en memoria

Así, si recibimos un evento de que los usuarios han cambiado, lo que tenemos
que hacer es recargar toda la lista

Esto es un nuevo repositorio prácticamente. Ese repositorio, usará DBAL para
los métodos que modifican usuarios (put y delete) y usará `InMemoryUserRepository`
para los get

Nuestro composed repository (que usa dos), habrá que ponerlo en `services.yml` para
que lo inyecte en el command handler

El composed repository usa los dos por separado, pero... ¿cómo se sincronizan?,
¿cómo actualiza los datos el in-memory cuando es cambiado en el persistente
(el repositorio con la conexión DBAL)?

`ComposedUserRepository` es un `EventSubscriber`, y tiene que implementar el método
estático `getSubscribedEvents`, que tiene que devolver una estructura de datos así:

    return [
      UserWasCreated::class => [
        [ 'loadAllUsersToMemory', 0 ]
      ]
    ];

Por cada evento que tenemos que escuchar nos dice qué métodos públicos hay que
llamar y con qué prioridad (por ahora la prioridad es siempre `0`)

Ese `loadAllUsersToMemory` coge datos del repositorio persistente (DBAL) y los
mete en el in-memory. Necesitamos implementar métodos nuevos. Se parece a esto:

```
return $this
    ->persistent
    ->findAll()
    ->then(function (array $users) {
        $this
            ->memory
            ->loadFroArray($users);
        });
```

¿Qué pasa si arrancamos el server y ya había datos en la base de datos? Pues que
tenemos que escuchar el evento `preload` del server de DriftPHP para precargar
esos datos:

```
AsyncKernelEvents::PRELOAD => [
    [ 'loadAllUsersToMemory', 0 ]
]
```

### Dependencias en el Dominio

`ComposedUserRepository` usa dos repositorios, `InMemoryUserRepository` y
`DBALUserRepository`. Pero el DBAL es de infraestructura, no es de Dominio, por
lo que `ComposedUserRepository` no puede depender de él. 

Debemos añadir una interfaz en el Dominio, `PersistentUserRepository`, para que
Dominio no dependa de Infraestructura. `DBALUserRepository` implementará esa
interfaz. La interfaz simplemente heredará de `UserRepository`.

## Deberes

## Referencias
