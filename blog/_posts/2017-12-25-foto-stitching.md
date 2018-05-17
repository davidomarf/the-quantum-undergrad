---
title: "Construyendo mi propio sastre fotográfico"
categories:
  - vision artificial
tags:
  - cosido de imagen
---

Era 24 de diciembre, el cielo comenzaba a aclararse, y hacía un frío entumecedor. Me vestí, até mis agujetas, y salí a correr.

Después de un rato, me topé con un paisaje que, si bien no es hermoso, me gustó bastante. Decidí tomar tres fotos, y seguí corriendo.

Después de un rato de haber regresado a mi casa, recibo una notificación de Google Photos diciéndome que mi "foto panorámica" estaba lista. Abro la notificación, y encuentro esto:

![Paisaje](/images/posts/foto-stitching/san-rafael-tlalmanalco.jpg)

Para empezar, no sabía que Google hacía eso de manera automática. Pasada la sorpresa inicial, se me ocurrió que sería buena idea construir mi propio «panoramizador» de imágenes.

No tenía ni la más miníscula idea de cómo podía construirlo, pero estaba emocionado.

---------

Al día siguiente, y después de un par de búsquedas, encontré el concepto que buscaba: *«image stitching»*, o cosido de imagen.

En este artículo estará escrito todo el proceso desde el estado del arte, hasta el algoritmo para coser imágenes que yo implementaré. Será bastante extenso, pero estará bastante bien auto-contenido. Lo suficiente para que, si lo decides, puedas escribir tu propio algoritmo en el lenguaje que quieras.

## Contenido
{:.no_toc}

* TOC
{:toc}

## ¿Qué es el *photo-stitching*?

Es un proceso en el que se combinan diferentes imágenes con áreas traslapadas, para generar una imagen de mayor dimensión.

![Ejemplo de photo-stitching](/images/posts/foto-stitching/foto-stitching.jpg)

Sus usos pueden ser la fotografía médica, la cartografía, o la estabilización de vídeo.

## El proceso

### Registro de imagen

Consiste en encontrar la función que alínea el contenido de una imagen con el contenido de otra.

Desde un punto de vista más técnico, el registro de imagen es una función que recibe como entrada dos imágenes diferentes, y produce como salida, una transformación geométrica.

Al coser imágenes, se genera un «área de traslape». Idealmente, las secciones de las múltiples fotos en una misma área de traslape, es la misma.

Pero en condiciones no ideales, existen «discrepancias»: diferencias causadas por movimiento, profundidad de campo, o iluminación.

La transformación geométrica producidadebe ser tal, que la suma total de diferencias en el área de traslape, sea la mínima.

### Calibración

Es tal vez el paso más *truculento* de todos en cuestión de intuición.

La calibración **extrae** los parámetros de la cámara con la que las fotografías fueron capturadas, como la distancia focal o la relación de aspecto.

Una vez conocidos los parámetros, se pueden detectar discrepancias como distorsiones, diferencias de exposición, o aberraciones cromáticas.

[^fn1]
[^fn2]
[^fn3]
[^fn4]
[^fn5]
[^fn6]
[^fn7]
[^fn8]

### Mezclado

El paso final, y tal vez el único en el que pensé al momento de idear el proyecto.

Aquí es donde se asegura que las imágenes se hayan «cosido» de una manera dulce y suave como la mantequilla, para evitar que se vean las «costuras».

Esto implica corregir colores, compensar movimiento, y eliminar fantasmas.

---------

Tal vez parezca que todos los pasos hacen lo mismo. Pero, en cuanto comience con la explicación matemática, y después, con la implementación programática, se notarán las diferencias entre cada uno.

Y lo más increíble es que todo este artículo no hubiera existido de no ser por esa carrera matutina.

## Referencias

[^fn1]: [<i class="fa fa-link" aria-hidden="true"></i>](http://matthewalunbrown.com/papers/ijcv2007.pdf){: target="_blank"} Brown, M., & Lowe, D. G. (2007). Automatic panoramic image stitching using invariant features. International journal of computer vision, 74(1), 59-73.

[^fn2]: [<i class="fa fa-link" aria-hidden="true"></i>](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.96.6746&rep=rep1&type=pdf){: target="_blank"} Rankov, V., Locke, R. J., Edens, R. J., Barber, P. R., & Vojnovic, B. (2005, March). An algorithm for image stitching and blending. In Proceedings of SPIE (Vol. 5701, pp. 190-199).

[^fn3]: [<i class="fa fa-link" aria-hidden="true"></i>](https://pdfs.semanticscholar.org/2b0c/9c57572b156680e10f711b13ae205849493d.pdf){: target="_blank"} Szeliski, R. (2006). Image alignment and stitching: A tutorial. Foundations and Trends® in Computer Graphics and Vision, 2(1), 1-104.

[^fn4]: [<i class="fa fa-link" aria-hidden="true"></i>](http://www.cs.cmu.edu/~yx/papers/pstitcher.pdf){: target="_blank"} Xiong, Y., & Turkowski, K. (1998, October). Registration, calibration and blending in creating high quality panoramas. In Applications of Computer Vision, 1998. WACV'98. Proceedings., Fourth IEEE Workshop on (pp. 69-74). IEEE.

[^fn5]: [<i class="fa fa-link" aria-hidden="true"></i>](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.464.5408&rep=rep1&type=pdf){: target="_blank"} Fitzpatrick, J. M., Hill, D. L., & Maurer Jr, C. R. (2000). Image registration. Handbook of medical imaging, 2, 447-513.

[^fn6]: [<i class="fa fa-link" aria-hidden="true"></i>](https://en.wikipedia.org/w/index.php?title=Image_stitching&oldid=809039739){: target="_blank"} Image stitching. (2017, November 6). In Wikipedia, The Free Encyclopedia. Retrieved 20:00, December 26, 2017, from https://en.wikipedia.org/w/index.php?title=Image_stitching&oldid=809039739

[^fn7]: [<i class="fa fa-link" aria-hidden="true"></i>](http://ksimek.github.io/2012/08/14/decompose/){: target="_blank"} Simek, K. (2013, June 02). Dissecting the Camera Matrix. Retrieved December 26, 2017, from http://ksimek.github.io/2013/08/13/intrinsic/

[^fn8]: [<i class="fa fa-link" aria-hidden="true"></i>](https://hypjudy.github.io/2017/05/10/panorama-image-stitching/){: target="_blank"}HYPJUDY. (2017, May 10). [CVPR] Panorama Image Stitching. Retrieved December 26, 2017, from https://hypjudy.github.io/2017/05/10/panorama-image-stitching/