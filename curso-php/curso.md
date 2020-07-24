# Curso Event-Driven PHP

[Curso](https://php.coach) impartido por [Mar Morera](https://mmoreram.com)
sobre ReactPHP, CQRS y Even-Driven/Eventos de Dominio.

La agenda del curso de 16h es:

## [Estructura del proyecto](01-estructura-proyecto.md)

Principios básicos de DriftPHP, el framework PHP para trabajar con los
componentes de ReactPHP y de Symfony.

## [Básicos de Docker](02-basicos-docker.md)

Aprenderemos todo lo que necesitamos saber de docker para deployar nuestras
aplicationes. Este curso asume que ya sabes lo que es docker y para qué sirve.

## [Fundamentos de ReactPHP](03-fundamentos-reactphp.md)

Para entender correctamente cómo funciona la programación asíncrona en PHP,
antes necesitamos aprender cómo funciona ReactPHP internamente.

## [Definición del dominio](04-definicione-dominio.md)

Con un proyecto simple, pero completo, delante nuestro, empezaremos a pensar
en nuestro modelo. En esta parte no vamos a cargar ninguna dependencia externa
como Mysql o Redis. Solo nuestras clases. Después de este módulo, tu proyecto
funcionará síncronamente sin ninguna capa de persistencia

## [Dependencias I/O](05-dependencias-io.md)

Una vez nuestro proyecto ya está funcionando correctamente, vamos a trabajar la
capa de persistencia, como Redis o Mysql. Veremos que testear esta capa es
trivial y extremadamente rápido. Veremos cuan rápido es cambiar entre adaptadores.

## [Eventos de dominio](06-eventos-dominio.md)

¿Y si transformamos nuestra aplicación entera para que trabaje con eventos de
dominio? ¿Cuánto creéis que podrá mejorar? Este capítulo, literalmente,
te fascinará.

# La agenda que hemos llevado

## Día 1

Problemas de PHP tradicional, bloquear el hilo, beneficios de la programación
asíncrona, ReactPHP, DriftPHP.

Limitaciones de los frameworks actuales: Symfony, Laravel,...

## Día 2

CQRS y nuestro primer caso de uso: get-user, buscar un usuario por su UID

## Día 3

Revisamos el caso de uso para buscar un usuario.

Continuamos por nuestra cuenta con el segunod caso de uso: crear un usuario

Gestión de errores con promesas, `otherwise`

Diferencias entre POST, PUT y PATCH, verbos HTTP

Comunicación desde el Framework o la Infraestructura con nuestro Dominio. El
Dominio no depende de nada.

## Día 4

Terminamos el siguiente caso de uso, put-user, que crea un nuevo usuario en
nuestro sistema

Aprendemos sobre los middlewares de query/command bus. Crearlos, configurarlos
y cómo funcionan. Son como los middlewars de Slim, pero con promesas, claro.

Comenzamos con el concepto de Repositorio. La interfaz es parte del Modelo, parte
del Dominio, y estará junto al modelo de User: entidad, excepciones,...

Las implementaciones de los repositorios... para el siguiente día

