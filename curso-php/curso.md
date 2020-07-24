# Curso Event-Driven PHP

[Curso](https://php.coach) impartido por [Mar Morera](https://mmoreram.com)
sobre ReactPHP, CQRS y Even-Driven/Eventos de Dominio.

Esta es la [agenda](agenda.md) del curso de 16h.

# Nuestro curso

## [Día 1](dia-01.md)

Problemas de PHP tradicional, bloquear el hilo, beneficios de la programación
asíncrona, ReactPHP, DriftPHP.

Limitaciones de los frameworks actuales: Symfony, Laravel,...

## [Día 2](dia-02.md)

CQRS y nuestro primer caso de uso: get-user, buscar un usuario por su UID

## [Día 3](dia-03.md)

Revisamos el caso de uso para buscar un usuario.

Continuamos por nuestra cuenta con el segunod caso de uso: crear un usuario

Gestión de errores con promesas, `otherwise`

Diferencias entre POST, PUT y PATCH, verbos HTTP

Comunicación desde el Framework o la Infraestructura con nuestro Dominio. El
Dominio no depende de nada.

## [Día 4](dia-04.md)

Terminamos el siguiente caso de uso, put-user, que crea un nuevo usuario en
nuestro sistema

Aprendemos sobre los middlewares de query/command bus. Crearlos, configurarlos
y cómo funcionan. Son como los middlewars de Slim, pero con promesas, claro.

Comenzamos con el concepto de Repositorio. La interfaz es parte del Modelo, parte
del Dominio, y estará junto al modelo de User: entidad, excepciones,...

Las implementaciones de los repositorios... para el siguiente día

## [Día 5](dia-05.md)

## [Día 6](dia-06.md)

## [Día 7](dia-07.md)

## [Día 8](dia-08.md)
