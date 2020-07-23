# Día 1

Marc creador de [API Search](https://apisearch.io), como idea para separar las
queries lentas de las rápidas, para que no te bloqueen las lentas

Como viene de Symfony... [DriftPHP](https://driftphp.io) es un intento de migrar
Symfony a ReactPHP

No le interesa tanto lo interno de ReactPHP: event loop, ticks,...

Lo que le interesa es cómo puedes meter ReactPHP en features que le sirvan a tu
empresa

La idea es tener una idea, implementarla, testearla, que sea deployable y 
finalmente, desplegarla. El objetivo es desplegar algo en producción para la
empresa

Está muy enfocado a la empresa, que está bien, lo tiene que vender a empresas,
no a individuos

Va a ser super pesado con la performance, le parece muy mal que Symfony no sea
capaz de bajar de los 4ms por petición. 4ms? Ni Easyvista devolviendo un simple
echo. Un echo ya nos tarda más de 4ms.

Cuellos de botella de PHP y de Symfony:

1. ORMs, conexiones a la base de datos
2. Inicializar el framework (éste es el que le interesa a Marc)
3. 1 thread de PHP solo puedes tener 1 usuario. Si quieres más usuarios, tienes
que inicializar (y finalizar) el framework para cada uno de ellos

ReactPHP evita que haya que levantar PHP entero en cada una (**cada una**) de las
peticiones

En este curso veremos por qué Symfony no nos vale, y por qué DriftPHP (ReactPHP)
sí que nos sirve

Limitaciones de Symfony

- websockets: no puede mantener conexiones permanentes con los clientes web, el
mismo problema que nos encontramos nosotros
- Eventos de dominio: no puedes modelar tu dominio con eventos
- Compartir memoria entre servidores, entre instancias del web server (porque
necesitas escalar)
- No puedes escuchar en varios puertos a la vez: o tienes un websocket, o tienes
un puerto http, o escuchas a RabbitMQ,... Pero no a la vez. Y si tienes varios
servers, no puedes compartir memoria entre ellos

La única forma que tienes de hacer que algo bloqueante (PHP común) sea más rápido
es meter más y más máquina

Lo que quiere romper Marc es la historia esta de petición -> respuesta. Si estás
esperando (bloqueado) a que te llegue una petición HTTP, no puedes estar esperando
otras peticiones. Si estás inicializando el kernel, no puedes estar atendiendo
peticiones. Si estás accediendo a la base de datos, no estás atendiendo peticiones
ni procesando respuestas. 

Por eso, solo puedes escalar. O también, puedes hacerlo asíncrono

Y hasta aquí, la justificación de la necesidad de ReactPHP o DriftPHP

## Componentes de DriftPHP

Para cada petición, DriftPHP no te devuelve una respuesta, si no una promesa, que
al final será una respuesta. Devuelve promesas, como en JS

Hasta ahora, puedo asumir que las promesas en JS y en ReactPHP son lo mismo. El
concepto es el mismo, el API similar. Faltaría ver la gestión de los errores y ver
si existe alguna otra diferencia. Pero por ahora...

Así es como funciona ReactPHP:

Las promesas, tienen un método, `then()`, que devuelven otra promesa, por lo que
puedes ir encadenando promesas y llamadas a `then()`

**CLAVE**: todo lo que es entrada/salida I/O, todo lo que accede fuera del hilo
de PHP, **debe** devolver promesas, debe ser código **no** bloqueante

Si cada llamada a un servicio devuelve una promesa, puedo ir encadenando llamadas
a servicios: redis, base de datos, disco duro,...

fulfilled promise => promesa cumplida

En DriftPHP, y en ReactPHP, un controlador (el punto de entrada a mi dominio, a mi
aplicación) no devuelve una `Response`, devuelve una promesa, que eventualmente,
devolverá la `Response` 

Esto es crucial, al devolver la promesa, no bloquea, retorna muy rápido. La
respuesta llegará más adelante, quizá en el mismo tiempo, pero no bloqueo, y
puedo seguir aceptando peticiones

A DriftPHP, el kernel de Symfony ya no le vale, porque lo que espera el kernel son
respuestas, pero no puedo devolver respuestas, devuelvo promesas. Así que, lo
primero que hay que cambiar el kernel

El *event loop* es un array de promesas, en cada tick, va preguntando a cada una
si ya está lista. La primera promesa que esté cumplida, llama a sus callbacks, 
a sus `then()`, pasándoles el valor con el que se ha cumplido la promesa

Las promesas más rápidas, saldrán antes del event loop. De esta forma, de forma
asíncrona, las peticiones se procesan de poco en poco, `then()` a `then()`,
promesa a promesa

DriftPHP = promesas + event loop + streams

## Deberes para mañana

¿Tiene alguna ventaja usar asincronía con CQRS?

Se supone que CQRS sirve para separar los comandos (hacer cosas) de las requests
(preguntar por datos). Se supone que los comandos son muy costosos en tiempo y
recursos. Pero con el event loop, con asincronía, al estar todo dividido en
promesas, esto ya lo tenemos, ya tenemos esta separación, ya tenemos la parte
**no** bloqueante

Entonces, ¿para qué puede ser útil CQRS asíncrono en ReactPHP?

## Preguntas

- ¿En qué se parecen y en qué se diferencian las promesas de ReactPHP y las de
JavaScript?
- En Symfony, el kernel tendría que esperar a que se cumplan las promesas. Marc
habla de un `await`, similar al de JavaScript. ¿Esta espera es bloqueante?
Entiendo que en DriftPHP no, porque si no, no habría mejora con respecto a
Symfony
- En un tick del event loop, ¿sólo se procesa una promesa? ¿Es un round robin?
- ¿Qué es eso del DBal?
