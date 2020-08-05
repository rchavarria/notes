---
title: "Curso DriftPHP: día 5"
categories:
- Cursos
- PHP
---

Testear interfaces

Implementamos y testeamos un User Repository, in memory user repository

<!-- more ->

## Notas tomadas

Hoy me toca compartir pantalla. Hay pocas notas, pero habrá mucho código

Vamos a testear una implementación del User Repositorio

Tenemos una interfaz, ¿para qué sirven las interfaces? Para poder intercambiar
implementaciones

¿Cada implementación de la interfaz, tiene sus tests? Si lo haces así,
realmente, no estás testeando "nada". Testeas todo, pero realmente no sabes si
son exactamente implementaciones de la misma interfaz

A nivel conceptual, hay que testear el repositorio a nivel funcional, para poder
asegurar a un tercero que todas mis implementaciones son intercambiables

Esto es un buen punto a favor para una librería, asegurar que todas las
implementaciones son intercambiables. No me vale un test para cada implementación,
porque quizá no sean los mismos tests. Tiene que haber un test que ataquen
las mismas implementaciones

Así, no es suficiente hacer un test con mock, porque el mock no es ninguna
implementación

Marc nos va a enseñar la única forma de hacerlo bien :D :D

Le gusta más el test de usuario, funcional (de aceptación) que el unitario.
Esos tests le permiten refactorizar a lo bestia (claro). Para él, la unidad es
la API entera. A Marc no le gusta mucho hablar de unitarios/integración/...

Para comenzar a escribir tests de PHPUnit, hay que cargar el bridge de PHPUnit
que proporciona DriftPHP

Mi clase de test es abstracta, porque testeamos la interfaz, así que no puedo
ejecutar los tests, todavía

Un método abstracto del test abstracto me devolverá la implementación del
repositorio. El test de la interfaz tiene esta pinta:

```
abstract class UserRepositoryTest extends TestCase {

  /** @var LoopInterface */
  private $loop;

  abstract protected function createEmptyRepository(LoopInterface $loop): UserRepository;

  public function testUserNotFound() {
    $repository = $this->createEmptyRepository($this->loop);
    $promise = $repository->find('1234');

    $this->expectException(UserNotFoundException::class);
    await($promise, $this->loop);
  }

//...
}  
```

Los tests para cada una de las implementaciones serán simplemente heredar del
test abstracto y crear una instancia de la implementación del repositorio. Esos
tests no tendrán métodos de tests, simplemente tendrán que crear la implementación
de la interfaz. El test de la interfaz es quien tiene los tests para todas
las implementaciones

El test de la implementación sería así:

```
<?php

class InMemoryUserRepositoryTest extends UserRepositoryTest {
  protected function createEmptyRepository(LoopInterface $loop): UserRepository {
    return new InMemoryUserRepository();
  }
}
```

**Implementación in-memory del repositorio**

Una limitación de un in-memory repository es que solo se puede ver en el propio
server, si escalo horizontalmente, un repositorio no verá el del otro server

## Deberes

1. implementar delete
2. completar los tests

## Referencias

- [Implementación de InMemoryUserRepository](https://github.com/rchavarria/driftphp-skeleton/blob/master/src/Domain/Model/User/InMemoryUserRepository.php)
- [Tests de la interfaz UserRepository](https://github.com/rchavarria/driftphp-skeleton/blob/master/test/Domain/Model/User/UserRepositoryTest.php),
independiente de la implementación
- [Test de la implementación](https://github.com/rchavarria/driftphp-skeleton/blob/master/test/Domain/Model/User/InMemoryUserRepositoryTest.php)
