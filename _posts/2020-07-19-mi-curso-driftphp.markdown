---
title: "Curso Event-Driven PHP"
categories:
- Cursos
- PHP
---

[Curso](https://php.coach) impartido por [Mar Morera](https://mmoreram.com)
sobre ReactPHP, CQRS y Even-Driven/Eventos de Dominio.

Esta es la [agenda](2020-07-19-agenda-curso-driftphp.markdown) del curso de 16h.

<!-- more ->

## [Día 1](2020-07-20-curso-driftphp-dia-01.markdown)

Problemas de PHP tradicional, bloquear el hilo, beneficios de la programación
asíncrona, ReactPHP, DriftPHP.

Limitaciones de los frameworks actuales: Symfony, Laravel,...

## [Día 2](2020-07-21-curso-driftphp-dia-02.markdown)

CQRS y nuestro primer caso de uso: get-user, buscar un usuario por su UID

## [Día 3](2020-07-22-curso-driftphp-dia-03.markdown)

Revisamos el caso de uso para buscar un usuario.

Continuamos por nuestra cuenta con el segunod caso de uso: crear un usuario

Gestión de errores con promesas, `otherwise`

Diferencias entre POST, PUT y PATCH, verbos HTTP

Comunicación desde el Framework o la Infraestructura con nuestro Dominio. El
Dominio no depende de nada.

## [Día 4](2020-07-23-curso-driftphp-dia-04.markdown)

Terminamos el siguiente caso de uso, put-user, que crea un nuevo usuario en
nuestro sistema

Aprendemos sobre los middlewares de query/command bus. Crearlos, configurarlos
y cómo funcionan. Son como los middlewars de Slim, pero con promesas, claro.

Comenzamos con el concepto de Repositorio. La interfaz es parte del Modelo, parte
del Dominio, y estará junto al modelo de User: entidad, excepciones,...

Las implementaciones de los repositorios... para el siguiente día

## [Día 5](2020-07-27-curso-driftphp-dia-05.markdown)

Testear interfaces

Implementamos y testeamos un User Repository, in memory user repository

## [Día 6](2020-07-28-curso-driftphp-dia-06.markdown)

Hoy trabajamos con bases de datos, DBAL y diferentes implementaciones de un
repositorio.

## [Día 7](2020-07-29-curso-driftphp-dia-07.markdown)

Vemos el uso de la herramienta `ab`, Apache Benchmark, para ver el rendimiento
de lo que estamos creando.

Vemos cómo lanzar Eventos de Dominio, primero en un bus interno, pero al menos
es algo asíncrono

También discutimos qué beneficios nos traen los Eventos de Dominio

## [Día 8](2020-07-30-curso-driftphp-dia-08.markdown)

Ponemos en marcha RabbitMQ como event bus, y a escuchar Eventos de Dominio
en varios servers

Creamos una optimización para tablas con pocas escrituras (save o delete) y muchas
lecturas, de forma que con cada Evento de Dominio, se actualice el contenido de
la tabla en memoria

Por cierto, hoy hemos ido a toda pastilla

## [Día 9](2020-08-03-curso-driftphp-dia-09.markdown)

Websockets
