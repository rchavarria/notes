---
title: "Coding dojo: Test Driven Development"
categories:
- Cursos
---

Notas sobre el curso [Coding dojo: Test Driven Development](https://app.pluralsight.com/library/courses/the-coding-dojo/) de [Emily Bache]() publicado en Pluralsight.

El curso trata sobre los *Coding Dojos*. Los Coding Dojos son una gran herramienta para aprender y enseñar a programar, así como para aprender y enseñar TDD.

Así que, ¿qué tal si te animas a ser el anfitrión de un Global Day of Code Retreat?

<!-- more -->

## Review

It starts with basic concepts (this is starting to be the norm) about TDD, tests, different development games,...

Emily explains aobut different games to practice while coding, to learn programming and to learn how to solve problems.

The most interesting part is when she shows how to host a set of 5 or more codign dojos, with their objectives, tools, katas, games,...

## Learned topics

Emily adds a new phase to TDD, additionally to the typical three: red, green, refactor. It's called *overview*. In this phase you think about a list of tests (to do incremental development), decides what test to write next,...

Randori in pairs: that's the way almost all code retreats and coding dojos are hosted.

# Notes (English)

# Sample series of Coding Dojos

Component skills for TDD:

1. Designing test cases
2. Designing clean code
3. Driving development with tests
4. Refactoring safely

All of them are interrelated to each other. Coding dojos are designed to practice one of them, to focus on one of them. Is better to focus on just one of them than to practice all of them at the same time.

## TDD phases

Emiliy adds a new phase to TDD, the *overview* phase:

1. Overview
    - Analyse problem
    - Test list
    - Guiding test
2. Red
    - Declare & name
    - Arrange-Act-Assert
    - Satisfy compiler
3. Green
    - Implement solution
    - Fake it
    - Start over
4. Refactor
    - Remove fake
    - Remove code smell
    - (no new functionality)
    - Note new test cases

## First coding dojo

Meeting outline:

- Introduction
    - What's a coding dojo?
    - Deliberate practice
- Agree activities
    - Explain TDD states and moves
    - Randori rules
    - Keyboard switch - 5 mins each
- Code!
    - String calculator of FizzBuzz

You'll practice *Driving development with tests* skill

## Refactoring dojo

- Concept of *code smell* and *refactoring*
- Small refactorings steps add up to significant improvements
- Having comprehensive automated tests changes the way you work

Outline:

- Introduction
    - Reminder of Dojo purpose
- Agree activities
    - Connect to previous meeting
    - What's refactoring?
    - Together recreate steps of *Extract method* (and compare agains Martin Fowler's book)
- Code!
    - Randori in pairs
    - Tennis or Yahtzee
- Retrospective
    - How did it feel to have comprehensive tests?
    - Could we work like this in our production code?

## Writing good tests

- Discuss what a good test look like
- Practice writing tests with Arrange - Act - Assert that are readable
- Talk about legacy code

Outline:

- Introduction
    - Dojo purpose
    - TDD component skils
- Agree activities
    - Arrange-Act-Assert
    - Properties of good tests: readibility
- Code!
    - Randori in pairs
    - Gilded Rose Kata
- Retrospective
    - How readable are these tests?
    - Would these tests support us when refactoring?
    - Could we write tests like this for our production code?

## Clean and SOLID code

Outline:

- Introduction
    - Dojo purpose
    - TDD component skils
- Agree activities
    - SOLID principles
- Code!
    - Randori in pairs
    - Racing Car Katas
- Retrospective
    - Is SOLID code the same as Testable code?
    - Does our production code follow SOLID principles?

## Incremental development

- Writing a test list
- Taking Baby Steps
- Before start writing tests, it's a good idea to think of a list of possible tests

Outline:

- Introduction
    - Dojo purpose
    - Using code katas for practice
- Agree activities
    - Test list
    - Baby steps
- Code!
    - Randori in pairs
    - Gilded Rose, Tenis or Yathzee, but from scratch
- Retrospective
    - Did you feel your tests were driving development?
    - Could we work like this in our production code?

# Finally, the transcript

Pluralsigt [transcript](transcript.markdown) of the course.

