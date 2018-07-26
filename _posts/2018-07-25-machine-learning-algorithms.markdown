---
title: "Curso: How to Think About Machine Learning Algorithms"
categories:
- Cursos
- Aprendizaje
- Machine Learning
---

No hay muchos cursos sobre Machine Learning en Pluralsight. Buscando entre los
que parecen más generales, más teóricos que prácticos, este tiene buena pinta.

Busco cursos más generalistas para ir aprendiendo los conceptos. Los más
específicos, los que hablan más sobre herramientas que sobre conceptos, no me
interesan todavía. Todo llegará.

<!-- more -->

Contenidos del curso [How to Think About Machine Learning Algorithms]
de [Swetha Kolalapudi]:

- Course Overview
    - Course Overview

- Introducing Machine Learning
    - Recognizing Machine Learning Applications
    - Knowing When to Use Machine Learning
    - Understanding the Machine Learning Process
    - Identifying the Type of a Machine Learning Problem

- Classifying Data into Predefined Categories
    - Understanding the Setup of a Classification Problem
    - Detecting the Gender of a User
    - Classifying Text on the Basis of Sentiment
    - Deciding a Trading Strategy
    - Detecting Ads
    - Understanding Customer Behavior

- Solving Classification Problems
    - Using the Naive Bayes Algorithm for Sentiment Analysis
    - Understanding When to use Naive Bayes
    - Implementing Naive Bayes
    - Detecting Ads Using Support Vector Machines
    - Implementing Support Vector Machines

- Predicting Relationships between Variables with Regression
    - Understanding the Regression Setup
    - Forecasting Demand
    - Predicting Stock Returns
    - Detecting Facial Features
    - Contrasting Classification and Regression

- Solving Regression Problems
    - Introducing Linear Regression
    - Applying Linear Regression to Quant Trading
    - Minimizing Error Using Stochastic Gradient Descent
    - Finding the Beta for Google
    - Implementing Linear Regression in Python

- Recommending Relevant Products to a User
    - Appreciating the Role of Recommendations
    - Predicting Ratings Using Collaborative Filtering
    - Finding Hidden Factors that Influence Ratings
    - Understanding the Alternative Least Squares Algorithm
    - Implementing ALS to Find Movie Recommendations

- Clustering Large Data Sets into Meaningful Groups
    - Understanding the Clustering Setup
    - Contrasting Clustering and Classification
    - Document Clustering with K-Means
    - Implementing K-Means Clustering

- Wrapping up and Next Steps
    - Surveying Machine Learning Techniques
    - Looking Ahead
    
## Notas tomadas

### Capítulo 1: Introducing Machine Learning

Resolver problemas con Machine Learning es como resolverlos de una manera
parecida a cómo aprendemos los humanos. Los humanos aprendemos de la
experiencia (exposición a un fenómeno durante un largo período de
tiempo). En tecnología, esa *experiencia* la conocemos como *datos*, así,
los programas aprenden de los datos como los humanos aprendemos de la
experiencia.

Hay 4 grandes categorías de problemas a resolver con ML:

- Clasificación
- Regresión
- Recomendaciones
- Clustering

Los algoritmos usados en ML *ya están inventados*. Donde hay que emplear
casi todos los esfuerzos no es en desarrollar el algoritmo, si no en 
ser capaz de representar los datos de forma numérica para poder aplicarlos.
Lo complicado de ML no son los algoritmos, si no representar los datos
de la mejor forma posible. Identificar las *features* correctas,
cuantificarlas,...

### Capítulo 2: Classifying Data into Predefined Categories

**Problem instance**: definición del problema que queremos resolver

**Classifier**: algoritmo de clasificación

**Label**: categoría, clasificación,... identificada

El algoritmo necesita que los datos usados en el aprendizaje estén
correctamente etiquetados/clasificados.

Los patrones identificados por el algoritmo crean lo que se conoce como
**Modelo**

Algoritmos para resolver problemas de clasificación:

- Naive Bayes
- Support vector machines
- Decision trees
- K-Nearest neighbors (K-Means?)
- Random forests
- Logistic regression

**Term frequency representation**: representación para cuantificar textos.
Se crea una colección de todas las palabras que nos vamos a poder encontrar.
Para un texto dado, anotamos las apariciones de cada una de esas palabras.
Así tenemos una representación numérica del texto, con el que lo podemos
comparar con otros textos.

### Capítulo 3: Solving Classification Problems

#### Naive Bayes

Se puede utilizar para analizar textos, por ejemplo, para clasificarlos
como positivos o negativos. Asumimos que los textos
los tenemos cuantificados con *Term freq. representation*.

Para cada palabra/término tenemos que calcular la probabilidad de que aparezca
en comentarios positivos `Po` (la negativa sería `No = 1 - Po`).

```
     (cuantas veces aparece el término en comentarios positivos)
Po = ------------------------------------------------------------
     (cuantas veces aparece el término en todos los comentarios)
```

Para un nuevo texto dado, se multiplican los `Po` de cada palabra y obtenemos
el `Po` del comentario. Lo mismo con `No`.

Se llama *naive* porque asume que todas las palabras son independientes, cosa
que sabemos que es mentira. Ciertas palabras son más probables que aparezcan
junto a otras. Pero el algoritmo así es más sencillo.

#### Support Vector Machines

- Representa los datos como puntos en un hipercubo de `N` dimensiones (si
`N=3` tenemos un cubo de toda la vida, un espacio tridimensional)
- El algoritmo encuentra un hiperplano (en 3 dimensiones sería un plano) que
divide los puntos en dos grupos. El hiperplano no es más que la *línea* de
separación
- El hiperplano actúa como barrera, frontera entre las dos categorías

Pero... ¿cómo funciona este algoritmo? Ya tengo algo para profundizar por
mi cuenta

### Capítulo 4: Predicting Relationships Between Variables with Regression

Tipos de regresión, o algoritmos para resolver problemas de regresión:

- Lineal
- Polinomial
- No lineal

Algoritmos para resolver problemas de recomendaciones:

- Collaborative filtering: alternating least squares, nearest neighbor model
- Association rules
- Content based filtering

Algoritmos de clustering

- K-Means
- Hierarchical
- Density based
- Distribution based

Representación de los datos:

- Data munging
- Feature extraction
- Dimensionality reduction
- Feature engineering

Selección del modelo:

- Hyper parameter tuning
- Cross validation
- Ensembling

![Machine Learning in a nutshell](/notes/assets/images/2018/machine-learning-in-a-nutshell.png)

## Conclusión

Ha habido momentos durante el curso que pensé que era flojillo, pero
al poco tiempo me di cuenta de que es un curso bastante bueno. Expone
distintos problemas para ser resueltos mediante Machine Learning.

No todos los problemas se pueden resolver de la misma manera y Swetha
explica distintos tipos de problemas y sus distintas formas de resolverlos.

Totalmente recomendado para saber por dónde van los tiros a la hora
de enfrentarse a problemas. Abre muchos caminos por los que seguir
aprendiendo. Y esa era mi idea, así que estoy bastante contento
con el curso.

## Y después... ¿qué? ¿con qué sigo?

- ¿Cómo funciona el algoritmo Support Vector Machines?

## Referencias

- [How to Think About Machine Learning Algorithms]
- La autora del curso: [Swetha Kolalapudi]

[How to Think About Machine Learning Algorithms]: https://app.pluralsight.com/library/courses/machine-learning-algorithms
[Swetha Kolalapudi]: https://app.pluralsight.com/profile/author/swetha-kolalapudi
