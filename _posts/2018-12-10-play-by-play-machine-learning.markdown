---
title: "Play by play: Machine learning exposed"
categories:
- Cursos
- Pluralsight
- Machine Learning
---

Notas tomadas de un curso de Pluralsight titulado [Play by play: machine learning exposed].
Los *play by play* son cursos donde un par de personas trabajan juntas en un proyecto o
problema. Normalmente una de ellas es una experta en el tema, y la otra hace de estudiante,
aportando una visión novedosa e ingenua del tema.

En este caso, [Katharine Beaumont] es la experta en machine learning y [James Weaver] es
el novato en el campo, aunque aporta su visión experta en el mundo del desarrollo de
software.

<!-- more -->

Índice del curso:

- Machine Learning Introduction
    - Introduction
    - Supervised Learning Overview
- Supervised Learning
    - Types of Supervised Learning Problems: Regression and Classification
    - Anatomy and Visualizing Artificial Neural Networks
    - Forward Propagation
    - Back Propagation
    - Speed Dating Example
    - Evaluating and Optimizing a Neural Network
    - Regression Sum and Tic-tac-toe Examples
    - Introduction Intuition, K-means Algorithm
    - Using Unsupervised Learning to Map Art and Words
- Reinforcement Learning
    - Using BURLAP, Navigating a Grid World with Q-learning
    - Bellman Equation and Reward Tables
    - Tic-tac-toe with Reinforcement Learning
- Course Conclusion
    - Other Neural Networks Architectures and Conclusion

## Glosario

- Regresión lineal
- Gradiente: la velocidad de un cambio, cómo de rápido varía un cambio
- Peso (weight): en este curso se representa con la letra griega theta ( θ )
- Coste: media de la suma de los errores al cuadrado
- Diferenciación: variación de una hipótesis a la siguiente
- Ratio de aprendizaje `α`: ratio de variación de los pesos `θ`
entre iteraciones

## Machine learning introduction

Regresión lineal: lo que queremos saber es la relación que hay entre el tamaño de
la vivienda en `m^2` y el precio: `y = mx + c` (`y = θ1x + θ2`)

Con unos pesos *inventados*, hacemos una estimación. Ahora necesitamo una forma
de saber cómo de buena o mala es dicha estimación.

Cuando hablamos de **error**, en verdad estamos hablando de diferencia.

Restamos el valor estimado del valor real, elevamos al cuadrado, sumamos y calculamos
la media. Este concepto es el **coste**. El coste nos indica cómo de cerca está
nuestra hipótesis (estimación) de los datos. Por lo que si hacemos otra estimación
o hipótesis, podremos compararlas. `h(x)` representa una hipótesis.

Diferenciación es la variación de una hipótesis a la siguiente.

De esta forma, hay un valor para los pesos `θ` donde el valor del coste es
mínimo (que no cero).

Una forma de optimizar los valores de `m`, `c` o `θ`s para minimizarel coste es mirar
el gradiente de la función coste `J`:

- Si la función coste `J` aumenta cuando `θ` aumenta, en el siguiente paso debemos reducir `θ`
- Si la función coste `J` disminuye cuando `θ` aumenta, en el siguiente paso debemos aumentar `θ`

Cuando lleguemos a un mínimo, el gradiente será cero, y el coste dejará de variar.

**Nota**: *¿Recuerdas aquellos problemas de matemáticas donde se buscaba el mínimo de una
función haciendo que su primera derivada valiera cero? Pues esto me recuerda a
eso*

Podemos ir ajustando los valores de `θ` segun el ratio de aprendizaje, `α`. `α`
indica cuánto vamos a variar los valores de `θ` en cada iteración. Este valor de `α`
es un valor que tenemos que decidir/ajustar manualmente.

Por ponerlo en una fórmula:

![Variación de `θ` con la variación de `J`](/assets/images/2018/ml-theta-n-plus-1.png)

Derivamos la función de coste `J` por la variación de `θ`, y dependiendo de ello, así
aplicamos el valor de `α`.

[Play by play: machine learning exposed]: https://app.pluralsight.com/library/courses/play-by-play-machine-learning-exposed/table-of-contents
[Katharine Beaumont]: https://app.pluralsight.com/profile/author/katharine-beaumont
[James Weaver]: https://app.pluralsight.com/profile/author/james-weaver
