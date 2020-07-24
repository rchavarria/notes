# Agenda

## [Estructura del proyecto](01-estructura-proyecto.md)

Principios básicos de DriftPHP, el framework PHP para trabajar con los
componentes de ReactPHP y de Symfony.

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

## [Básicos de Docker](02-basicos-docker.md)

Aprenderemos todo lo que necesitamos saber de docker para deployar nuestras
aplicationes. Este curso asume que ya sabes lo que es docker y para qué sirve.

Hoy en día, una de las mejores formas de hacer que cualquier aplicación pueda 
funciona en cualquier entorno moderno es añadiendo soporte para Docker. Docker 
es una tecnología bastante asequible si entiendes su función, y este será nuestro 
objetivo. Una vez tengamos nuestra propia estructura para nuestra aplicación de 
hello world, vamos a configurar docker y docker-composer para poder hacer 
deployments, testing y desarrollo en local.

El objetivo de este bloque es añadir soporte de docker en nuestra aplicación. 
Añadiremos también integración con CircleCI para añadir un hook en nuestras 
pull requests

- Duración del bloque - 2h
- Elementos necesarios de Docker
- Docker composer para testing
- Crear un Dockerfile base

## [Fundamentos de ReactPHP](03-fundamentos-reactphp.md)

Para entender correctamente cómo funciona la programación asíncrona en PHP,
antes necesitamos aprender cómo funciona ReactPHP internamente.

Trabajar con ReactPHP es una experiencia completamente nueva si nunca has 
trabajado con un Event-Loop o una Promesa. Las cosas suceden eventualmente, y 
precisamente esto te fuerza a cambiar tu mentalidad sobre como programar tus 
servicios.

DriftPHP, por primera vez en un framework PHP, te permite trabajar con Responses 
de ReactPHP. Esto te permitirá aplicar todos los conceptos de asincronía en tu
dominio de una forma que nunca antes habrías visto.

Tras este bloque, entenderás todos los fundamentos de ReactPHP, una parte 
esencial del curso.

- Duración del bloque - 3h
- ¿Qué es un event-loop?
- ¿Qué es una promesa?
- ¿Qué es un stream?

## [Definición del dominio](04-definicion-dominio.md)

Con un proyecto simple, pero completo, delante nuestro, empezaremos a pensar
en nuestro modelo. En esta parte no vamos a cargar ninguna dependencia externa
como Mysql o Redis. Solo nuestras clases. Después de este módulo, tu proyecto
funcionará síncronamente sin ninguna capa de persistencia

Ahora ya tenemos un servicio que sirve peticiones tan rápido como realmente 
puede hacerlo, pero solo podemos servir un solo endpoint. Y será complicado 
ganar un poco de dinero tan solo con esta funcionalidad, por lo que vamos a 
empezar a diseñar nuestro dominio.

Y nuestro proyecto será simple. Crearemos un pequeño servicio para gestionar 
usuarios. No será un sistema de login ni un sistema de gestión demasiado complejo, 
solo una pequeña API donde podremos:

- Añadir un usuario
- Eliminar un usuario existente
- Editar un usuario existente
- Listar todos nuestros usuarios

Estos puntos serán suficientes como para entender ciertos puntos sobre la 
arquitectura, como dónde añadir nuestras clases de dominio, qué deberían 
contener estas clases y qué deberían evitar, y cómo de grande puede ser dicho 
dominio antes de poder aplicar una separación lógica.

Después de este capítulo, todo debería estar funcionando perfectamente de una 
forma completamente síncrona, y guardando absolutamente todo en memoria. Aún no 
siendo útil de ninguna de las formas, oye, es un primer paso.

- Duración del bloque - 3h
- Análisis de requerimientos
- Implementación de las clases del modelo
- Interfaces de repositorios e implementación en memoria
- Tests completos de nuestras necesidades, tanto unitarios como funcionales

## [Dependencias I/O](05-dependencias-io.md)

Una vez nuestro proyecto ya está funcionando correctamente, vamos a trabajar la
capa de persistencia, como Redis o Mysql. Veremos que testear esta capa es
trivial y extremadamente rápido. Veremos cuan rápido es cambiar entre adaptadores.

Vamos a hacer que todo funcione correctamente añadiendo una capa extra en 
nuestro proyecto, relativa a nuestras implementaciones de I/O. En nuestro 
lenguaje, añadir adaptadores para nuestros repositorios, como el Repositorio 
de User.

Todos estos adaptadores tienen que estar cubiertos por tests unitarios al 100%.
Veremos cómo, a pesar de todo, si seguimos la arquitectura que vamos a seguir, 
este ejercicio será trivial y rápido.

Después de este bloque, nuestra aplicación pasará a ser usable.

- Duración del bloque - 2h
- Adaptador Mysql para la capa de persistencia
- Tests unitarios para los nuevos adaptadores

## [Eventos de dominio](06-eventos-dominio.md)

¿Y si transformamos nuestra aplicación entera para que trabaje con eventos de
dominio? ¿Cuánto creéis que podrá mejorar? Este capítulo, literalmente,
te fascinará.

Tras estos últimos 5 capítulos, tendremos un servicio funcionando perfectamente 
en ReactPHP, con algunas implementaciones de repositorio testeadas y con algunos 
benchmarks ejecutados que nos demostrarán que, sin lugar a duda, hemos 
experimentado una mejora de performance sustancial con respecto a servicios a 
los que estamos acostumbrados.

Aún así, lo podemos hacer mejor. Mucho mejor. Increiblemente mejor.

Este capítulo final hará que te estalle la cabeza, pues empezaremos a trabajar 
con eventos de dominio, y precisamente gracias a las features que ReactPHP nos 
brinda en términos de asincronía y non-blocking, podremos convertir nuestro 
servicio en algo mucho más escalable, desacoplándolo muchísimo más de la 
infrastructura y decrementando nuestros tiempos de respuesta y uso de recursos 
por enésima vez.

- Duración del bloque - 3h
- Definición de eventos de dominio
- Introduciendo repositorios en memoria long-term
- Introducción a AMQP (RabbitMQ)
- Deployando la combinación server + consumer
- Introducción a los websockets
