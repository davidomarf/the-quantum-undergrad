---
title: "Algoritmos genéticos: de cero a héroe"
categories:
  - algoritmo
  - plan de aprendizaje
tags:
  - algoritmo genético
hidden: true  
---

// Escribir introducción toa chula toa rechulona

## Prefacio

Muchos de los considerados pioneros de la computación —Turing, Von Neuman, Wiener, y otros—, quisieron utilizar los sistemas naturales como metáfora [pa qué no sé jaja].

No es sorpresa, entonces, que las primeras computadoras fueran usadas —además del uso militar— para **modelar el cerebro, imitar el aprendizaje humano, y simular la evolución biológica.**

Durante mucho tiempo, esas actividades motivadas por la biología sufrieron de altibajos, pero desde los ochenta, recibieron una increíble atención por parte de la comunidad de investigación en computación.

Lo primero, evolucionó al campo de las redes neuronales; lo segundo, al aprendizaje automático; y lo tercero, en lo que hoy se conoce como «computación evolutiva», de la cual, los algoritmos genéticos son el ejemplo más prominente.

[Continuar con la historia jaja]

## Contenido
{:.no_toc}

* TOC
{:toc}

## Terminología

Creo que antes de comenzar con la representación en la computadora de estos algoritmos, es importante familiarizarnos con el origen de estas abstracciones. Así será más fácil ir adquiriendo la intuición del problema.

Al principio parecerá no tener ni una pizca de sentido, especialmente si tienes un contexto más relacionado con la ingeniería —cosa que imagino—, pero te prometo que al terminar de leer, podrás entender fácilmente la paridad entre la evolución biológica, y su abstracción para la computación.

---

Todo ser vivo consiste de un conjunto de células. Cada célula consiste de un conjunto de cromosomas. Cada cromosoma consiste en un conjunto de genes. Y cada gen puede tomar varias *formas*, llamadas alelos.

