# [Básicos de Docker](https://php.coach/course.es.html#docker-basics)

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

## Notas tomadas

[Día 2](dia-02.md)

## Preguntas

- `tactician` ¿para qué se usa? tactician-bundle,... parece que permite crear
buses, command-bus, query-bus,...

## Recursos

- Teoría similar a la de hoy: https://www.youtube.com/watch?v=3o9bOuJt56k
- Lista de vídeos sobre ReactPHP: https://www.youtube.com/playlist?list=PLKIEFFgNQYpVmUAKUjT_BRYYOdMHwGt0v
- [Fowler y CQRS](https://martinfowler.com/bliki/CQRS.html)
- [Mis problemas ejecutando DriftPHP en Windows](https://github.com/rchavarria/driftphp-skeleton/blob/master/docs/running-project-on-windows.md)
- [Cómo usar QueryBus en DriftPHP](https://driftphp.io/#/?id=query-bus)
- [Código de mi práctica](https://github.com/rchavarria/driftphp-skeleton/tree/get-user)
- [Proyecto skeleton de DriftPHP](https://github.com/driftphp/skeleton)
