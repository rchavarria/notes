---
title: "La pirámide de tests en la práctica"
categories:
- Artículos
- Testing
---

Unas pocas notas sobre un artículo de [Ham Vocke] publicada en la
web de Martin Fowler titulada [The practical test pyramid].

No son notas sobre todo el artículo, porque la mayoría son
conceptos que conozco y estoy de acuerdo, pero alguna idea
nueva sí que he descubierto.

<!-- more -->

El artículo comienza hablando sobre la importancia de los tests y
de su automatización (si lo puede ejecutar la máquina, seguro que
lo hace mejor y más rápido que nosotros).

Continúa hablando de la [pirámide de tests]:

![pirámide de tests]

Más adelante habla de los tests unitarios:

- Solitarios: donde todos los colaboradores son sustituidos por
[dobles de test]
- Sociales: no todos los colaboradores son sustituidos y algunos
colaboradores son los reales, los de producción

Y cómo no, de los tests de integración. Básicamente habla de tests
que necesitan una base de datos, un sistema de ficheros o un
API REST.

A la hora de probar nuestra aplicación con servicios externos
(servicios que no controlamos nosotros), Ham nos cuenta que podemos
utilizar alguna herramienta, como Wiremock (Java), para simular
un servicio externo. Podemos simular llamadas HTTP,... Son
servicios reales, pero controlados por nosotros, por lo que al
menos controlamos la infraestructura.

El problema de estas herramientas es que, según va pasando el
tiempo, no podemos estar seguros de que nuestro *mock* del servicio
responde de la misma forma que el servicio real.

Para solucionar esto, nos presenta los tests de contrato:

## Tests de contrato

blah blah

[Ham Vocke]: http://www.hamvocke.com/
[The practical test pyramid]: https://martinfowler.com/articles/practical-test-pyramid.html
[pirámide de tests]: http://blog.koalite.com/2014/05/deconstruyendo-la-piramide-de-los-tests/
[dobles de test]: http://xurxodev.com/dobles-de-test/
