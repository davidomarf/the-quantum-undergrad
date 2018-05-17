---
title: "Guía: Basemap para graficar mapas con Python"
categories:
  - visualización de datos
tags:
  - visualización
  - datos
  - python
  - datos geográficos
hidden: true
---

Recientemente empecé a trabajar en un proyecto de visualización de datos, usando el conjunto [World Language Family Map](https://www.kaggle.com/rtatman/world-language-family-map) en Kaggle. El conjunto contiene , entre muchas otras características, la latitud y longitud donde se habla cada uno de más de 18 000 lenguajes.

Decidí comenzar graficando la latitud y longitud como mapa de calor. Quería distinguir las zonas geográficas donde existen más lenguajes.

Mi primera solución, fue utilizar `pd.plot.hexbin()`. Pero en la gráfica no quería ejes, barra de color, cuadrícula, ni chilito del que no pica. Sólo quería la gráfica. Y la solución era enviar demasiados argumentos clave. Tampoco quería eso.

Después de buscar un poco, encontré [Basemap Toolkit](https://matplotlib.org/basemap/). Es una librería de Python que permite graficar información en mapas 2D. Al principio, comencé a usarla ciegamente, llegando a resultados feos como ...

Después de ciertos ajustes —que me tomaron más de un par de horas, y después, días—, llegué a graficar algo así:

[Incrustar imágenes de las gráficas ya terminadas]

Y en este artículo compartiré todas las cosas que podrían ayudar a alguien más a iniciar más rápido a utilizar Basemap. Así, podrán pasar más tiempo usando la herramienta, que aprendiendo a utilizarla.

## Contenido
{:.no_toc}

* TOC
{:toc}

## Dibujar mapas
