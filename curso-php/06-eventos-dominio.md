# [Eventos de Dominio](https://php.coach/course.es.html#turning-event-driven)

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
