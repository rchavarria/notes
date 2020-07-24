# [Dependencias de I/O](https://php.coach/course.es.html#io-dependencies)

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
