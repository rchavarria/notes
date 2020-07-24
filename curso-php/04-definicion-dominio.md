# [Definición del dominio](https://php.coach/course.es.html#domain-definition)

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

## Notas tomadas

[Día 4](dia-04.md)

## Deberes

- Hacer el caso de uso de borrar usuario, utilizando el Repositorio. No funcionará
todavía, pero en conceptualmente sabes hacerlo

## Preguntas

## Recursos

- [DriftPHP middlewares](https://driftphp.io/#/?id=middleware)
