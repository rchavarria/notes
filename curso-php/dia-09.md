# Día 9

Websockets

## Notas tomadas

Hoy el profe está un poco petado, tiene un pco de fiebre, y vamos a tirar mucho
de documentación

Para Websockets, hay un bundle específico

Hasta ahora, pensábamos que en el mismo server se podría estar escuchando un
puerto HTTP y un puerto de Websockets, pero no es así

El servidor de Websockets no va a ser el mismo server, vamos a tener un server de
HTTP y otro de WBS, se comunicarán entre ellos a través de Eventos de Dominio
enviados a través del event bus (que irá a través de RabbitMQ)

Añadir la dependencia al bundle en `composer.json`: `drift/websocket-bundle`

Activarlo en `bundles.php`

Los datos que vengan por Websockets van a ser Eventos de Dominio

También va a haber rutas, porque es muy parecido a un server HTTP. El protocolo
Websockets va sobre HTTP

Cada ruta es una conexión, y nosotros podemos inyectar esa conexión

```
# services.yml, antes de services:
websocket:
  routes:
    events:
      path: /events
    resources:
      path: /rs
    teams:
      path: /tms
```

¿Qué eventos tenemos en Websockets?

- Conexión abierta
- Conexión con error
- Conexión cerrada
- Ha llegado un mensaje
- Broadcast de mensajes

Vamos a lanzar un evento por el Websocket cada vez que se guarda un usuario

Los eventos que no heredan de Event, se meten en DomainEventEnvelope

Se inyectan como un array de conexiones, del tipo
`Drift\Websocket\Connection\Connections`

Y el nombre del parámetro en el constructor se tiene que llamar como el nombre
que pusimos en `services.yml` terminado en *Connections*: `eventsConnections`,
`resourcesConections` o `teamsConnections`

Queremos hacer broadcast cada vez que alguien se conecta, mira la clase
`BroadcastNewConnections`. Hay que implementar `EventSubscriberInterface`,
y definir qué eventos vamos a escuchar

Los broadcasters, o event subscribers, `BroadcastNewConnections` y `BroadcastDomainEvents`,
los declaramos como servicios en `services.yml` para que el kernel los cree y
puedan ser inyectados en caso de ser necesario

Comprobar que todo funciona, que al hacer PUT de un usuario, los broadcasters
pillan el evento `UserWasCreated`

Ahora, hay que levantar un nuevo server, que escuche puerto de Websockets. Esto se
hace con la consola de Symfony

```
php bin/console websocket:run 0.0.0.0:1234 --route=events --exchange=my_events
```

Si todo funciona bien, al hacer un PUT, el servidor de Websockets lo consumirá,
porque consume eventos del event bus (parámetro `--exchange` al arrancarlo)

Nos podemos conectar con el cliente Websockets del browser

Abrimos un `index.html`, solamente para estar conectado al server y el browser
no se queje

```
const conn = new WebSocket('ws://localhost:1234/events');
```

Y hasta aquí llegué. Yo no fui capaz de conectar un cliente al servidor de Websockets

## Deberes

Debemos hacer un server con todo lo visto hasta ahora, y además, una página web
sencilla, que se conecte al servidor de Websockets y tenga dos columnas: 

- Izquierda: vista en tiempo real del estado de la base de datos. Al recibir un evento de
usuario guardado, añade una fila a la tabla. Si el usuario se borra, se borra
el elemento. Y así. Evento a evento. No vale leer todos los datos de la tabla
y crearla desde cero
- Derecha: algo parecido a un event source, log de todos los eventos

Por mi parte, dar feedback del curso a Marc. Para poner en la web, exponer
nuestro caso de uso de por qué creemos que nos ha venido bien el curso,...

## Referencias

- [Página con un cliente muy sencillo de Websockets](http://www.websocket.org/echo.html),
suficiente para testear que podemos conectarnos a nuestro servidor de Websockets
