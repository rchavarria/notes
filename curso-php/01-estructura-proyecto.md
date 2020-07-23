# [Estructura del proyecto](https://php.coach/course.es.html#skeleton)

Parece simple y trivial, pero la mayoría de las veces, es uno de los puntos más 
complejos a la hora de empezar un proyecto. En este primer bloque del curso, 
empezaremos por construir lo que será el esqueleto de nuestra aplicación. ¿Qué 
necesitamos para empezar desde cero un proyecto donde, nuestra lógica de negocio, 
será implementada alrededor de una arquitectura CQRS y Event-Driven? ¿Cuales son 
las librerías que realmente vamos a necesitar para empezar con un repositorio lo 
más ligero posible?

En este capítulo exploraremos los principios de DriftPHP, un nuevo framework 
construido con los componentes de Symfony y ReactPHP. Conoceremos los componentes 
del framework así como sus posibles usos.

- Duración del bloque - 3h
- Definición de capas
- Instalamos DriftPHP. Arquitectura y fundamentos.
- Command Bus como el elemento core del proyecto
- Commands, command handlers y middlewares
- Nuestro primer Hello world utilizando CQRS
- Soporte en servidor por parte de DriftPHP. Server + Watcher
- Un poco de benchmarking con AB

## Notas tomadas

[Día 1](dia-01.md)

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

## Recursos

- [API Search](https://apisearch.io)
- [DriftPHP](https://driftphp.io)
