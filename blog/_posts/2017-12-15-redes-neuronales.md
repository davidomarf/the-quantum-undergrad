---
title: "Sobre Better Call Saul, perros con sombrero, y redes neuronales"
blog: blog
categories:
  - inteligencia artificial
tags:
  - red neuronal
---

Este es un artículo re-escrito después de haberlo perdido en un arranque fúrico e inconsciente. ¿Saben sobre ese sentimiento cuando haces algo por segunda vez y tienes la sensación de que la primer versión fue mucho mejor? Bueno, es eso que siento justo ahora.

Como sea, haré mi mejor esfuerzo: comencemos contando una pequeña historia.

## Contenido
{:.no_toc}

* TOC
{:toc}

## La fotogenia de Mike Ehrmantraut

Era 10 de Abril de 2017 y se estrenaba la tercera temporada de una serie que me ha encantado desde el principio y recomiendo febrilmente: Better Call Saul.

Había reservado mi propio horario para ver el estreno. Terminé mis labores —y las que no, las dejé inconclusas; iba a devorarme ese episodio sí o sí—, preparé la cena, y me senté a verlo.

Cerca del final del episodio, vi una de las escenas que ahora es una de mis favoritas en todo el cine y televisión. No entraré en detalles para evitar que alguien que está viendo la serie se trague algún *spoiler* por culpa mía.

Como sea, desde esa misma noche me dediqué a buscar esa escena en YouTube. No la hallé —cosa que después, me enteré que fue por mi incompetencia para buscar, pues sí existía—, así que decidí subirla yo mismo.

Cuando había terminado de cargarse el vídeo, me di cuenta de algo en lo que no se me había ocurrido pensar: la miniatura era tan perfecta que me voló la peluca.

![Mike Ehrmantraut](https://i.ytimg.com/vi/Lr04qGKgrf4/maxresdefault.jpg)

No soy ningún entendido de la fotografía, pero diría que es excelente.

Y, naturalmente, me pregunté cómo es que había resultado esa miniatura. En el pasado había subido vídeos a YouTube, y recuerdo que tenías dos opciones:

1. Subir tu propia miniatura (cosa que claro, está descartada)
1. Seleccionar una auto-generada por YouTube

YouTube generaba las miniaturas usando lapsos de tiempo. Y creí recordar que eran, al menos, al 25%, 50% y 75%.

Si el cuadro en cualquiera de esos instantes del vídeo correspondía a la miniatura, habría terminado ahí mi búsqueda. Afortunadamente no fue así.

Comencé una breve búsqueda, y después de encontrar nada más que tutoriales para "Crear MUY buenas miniaturas para YouTube sin programas" -sí, eso lo extraje de uno de esos vídeos, que curiosamente tiene una pésima miniatura-, encontré el blog de investigación de Google: un tesoro cuya existencia ignoraba.

A partir de aquí es donde la cosa se pone técnica.

## Inteligencia artificial y computadoras torpes

En 1943 se creó el primer modelo de neuronas artificiales. A pesar de que el término *inteligencia artificial* aún no se había acuñado, se considera el primer trabajo en el campo después de la computación moderna.

Uno de los objetivos de la inteligencia artificial consiste en dotar al computador de las habilidades que, nosotros como humanos, damos por sentado —una vez aprendidas.

Algunos frutos de esta rama ya están algo maduros, como —ya explicaré más adelante— la visión artificial.

Otros, como conseguir que un robot estibe cajas, están algo... verdes.

<center><blockquote class="imgur-embed-pub" lang="en" data-id="led15Z7"><a href="//imgur.com/led15Z7">Shitty helperbot</a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script></center>

------------

La inteligencia artificial tiene usos que probablemente imaginabas, como el «Descubrimiento Semanal» de Spotify, que filtra de vez en cuando aquellos gustos rasposos que tienes. O la posibilidad de lucir la cara de un perro con los filtros de Snapchat.

Y algunos de los cuales no tenías ni idea, como Google, [encontrando la receta para la galleta de chocolate perfecta](https://www.cnbc.com/2017/12/05/eric-schmidt-google-used-ai-to-create-the-perfect-cookie-recipe.html). O Mathieu Cliche, [creando un detector de sarcasmo basado en tuits](http://www.thesarcasmdetector.com/about/).

Son usos peculiares, pero sin duda, uno que me sorprendió conocer fue el de la generación de miniaturas para YouTube. Sólo que antes de llegar a ello, hablaremos sobre la estrella de la noche: la visión por computadora.

## Visión por computadora

También llamada visión artificial. Es la disciplina que pretende darle a la computadora la capacidad de generar información útil a partir de una imagen. [^fn3]

Entre sus aplicaciones están el reconocimiento de rostros, reconocimiento de texto, y la tecnología de conducción autónoma.

Dos de las tareas más importantes que realiza son la clasificación y la detección. Explicar cómo funcionan y en qué consiste cada una lo haré en otro momento, pues no es necesario para llegar al punto principal de este artículo: las redes neuronales. Además es bastante largo. [^fn1]

### El desafío ImageNet [^fn2]

Existe un proyecto llamado ImageNet, un esfuerzo de investigación que pretende acelerar el desarrollo de la visión por computadora.

ImageNet organiza un desafío anual: *"ImageNet large-scale visual recognition challenge"*, o ILSVRC, el desafío más grande y difícil en el área, en donde se exponen los últimos avances de investigación.

En el [ILSVRC 2014](http://www.image-net.org/challenges/LSVRC/2014/), GoogLeNet ganó el primer lugar en las categorías de clasificación y detección en imágenes.

Estos son algunos ejemplos de las imágenes que GoogLeNet pudo procesar:

![Perrito con sombrero](https://2.bp.blogspot.com/-TDP7iU5MRSo/VAjer5jrPzI/AAAAAAAAAV0/xk3lWXsO2xQ/s1600/ILSVRC2012_val_00021791.PNG){: .align-center }

![GoogLeNet](https://2.bp.blogspot.com/-R7rgVNYKYM8/VAjmduy-VqI/AAAAAAAAAWU/TzKcFhfAfXc/s1600/ojbE4A2LeM.png)

En abril de 2015, el equipo de Google, intentó aprovechar el increíble avance en la clasificación y detección de objetos en imágenes, y quiso llevarlo un paso más lejos: clasificación de vídeo.

### Análisis de vídeo

Repasemos un poco: Ya sabemos que se pueden analizar imágenes; y un vídeo es una colección de imágenes. Entonces, ¿analizar un vídeo consiste en analizar todas las imágenes (cuadros) que lo componen? Sí. Pero no.

Básicamente, esa solución es válida. Pero la cantidad de cuadros por segundo de un vídeo «normal» son 24. Un vídeo de apenas un minuto tendría que analizar 1440 imágenes. Y más del doble si se trata de un vídeo a 60 fps.

En pocas palabras: analizar todos los cuadros sería mortal. Una pésima idea.

Para reducir todo esa carga de trabajo computacional, se tienen que elegir los cuadros a analizar. Hay que escogerlos lo suficientemente espaciados para evitar comparar cuadros casi repetitivos, pero no tanto para perder demasiados cuadros importantes.

## Referencias

[^fn1]: [<i class="fa fa-link" aria-hidden="true"></i>](https://research.googleblog.com/2015/10/improving-youtube-video-thumbnails-with.html){: target="_blank"} Yang, W., Tsai, M., Video Content Analysis team, & YouTube Creator team. (2015, October 08). *Improving YouTube video thumbnails with deep neural nets.* Retrieved December 26, 2017, from https://research.googleblog.com/2015/10/improving-youtube-video-thumbnails-with.html

[^fn2]: [<i class="fa fa-link" aria-hidden="true"></i>](https://research.googleblog.com/2014/09/building-deeper-understanding-of-images.html){: target="_blank"} Szegedy, C. (2014, September 05). *Building a deeper understanding of images.* Retrieved December 26, 2017, from https://research.googleblog.com/2014/09/building-deeper-understanding-of-images.html

[^fn3]: [<i class="fa fa-link" aria-hidden="true"></i>](https://research.googleblog.com/2015/04/beyond-short-snippets-deep-networks-for.html){: target="_blank"} Toderici , G., & Vijayanarasimhan, S. (2015, April 08). *Beyond Short Snippets: Deep Networks for Video Classification.* Retrieved December 26, 2017, from https://research.googleblog.com/2015/04/beyond-short-snippets-deep-networks-for.html

