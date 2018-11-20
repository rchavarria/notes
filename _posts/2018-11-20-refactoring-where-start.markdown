---
title: "Refactorizar, ¿por dónde empiezo?"
categories:
- Artículos
- Refactoring
---

Notas sobre el artículo de [J.B. Rainsberger] titulado
[Refactoring: where do I start?]. Rainsberger es una persona a la que
admiro como profesional, suele expresarse con bastante claridad y 
suele hablar/escribir/comunicar sobre temas que me interesan bastante.

<!-- more -->

*Refactoring* es una habilidad clave a desarrollar, ya que reescribir
las aplicaciones cuesta mucho y se es tolerado bastante menos.

## ¿Qué es el refactoring?

Es mejorar el diseño del código existente.

Se usa la metáfora de *olores de código* para describir problemas en 
la estructura del código, de tal forma que refactorizar consiste en 
identificar olores en el código, decidir cómo eliminar dichos olores 
y luego transformar sistemáticamente el código, en pasos pequeños y 
reversibles, hasta que el olor desaparezca.

## ¿Cómo me convierto en alguien bueno refactorizando?

Debo aprender 3 cosas:

1. Cómo identificar olores en el código
2. Cómo aplicar refactorizaciones
3. Qué refactorizaciones eliminan qué olores

## ¿Por qué necesito refactorizar?

El código se pudre poco a poco. Las refactorizaciones refrescan el
producto. Cuanto más esperes a refactorizar tu código, más esfuerzo
vas a necesitar para mantenerlo en el tiempo.

## ¿Cómo refactorizo código que no conozco?

Los primeros contactos con código que no conozco son aquellos donde
voy aplicando la refactorización más sencilla y menos arriesgada:
renombrado.

Cuando no conozco el impacto de un cambio en el resto del sistema, busco
maneras de crear cambios poco arriesgados que creen un lugar seguro
donde ir trabajando.  Normalmente introduzco interfaces en los límites
del código que quiero cambiar. La extracción de interfaces es uno de
los cambios estructurales más seguros que uno puede hacer en un
repositorio de código.

## Otras referencias

- [Oxidación del software], de Alejandro Pérez, Autentia

[J.B. Rainsberger]: https://www.jbrains.ca/
[Refactoring: where do I start?]: https://blog.jbrains.ca/permalink/refactoring-where-do-i-start
[Oxidación del software]: https://www.autentia.com/2015/07/22/design-smells-los-malos-olores-motivados-por-la-oxidacion-del-codigo/
