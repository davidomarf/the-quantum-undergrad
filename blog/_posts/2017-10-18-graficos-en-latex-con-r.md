---
title: "Añadir gráficos a LaTeX creados con R automáticamente"
categories:
  - computacion
tags:
  - latex
---

Durante el último par de días comencé a aventurarme en la gran curva de aprendizaje de [LaTeX](https://www.latex-project.org). Después de pasar poco más de una hora instalando [MikTex](https://miktex.org) y **varios** paquetes que después no volví a ocupar, logré *entrar en la zona*.

Después de un rato sintiéndome ya un poco cómodo, quise incrustar gráficas hechas en R, pero la manera en la que lo estaba haciendo era lenta. Consistía básicamente en:

- Exportar la gráfica como "plot.png"
- Mover plot.png al directorio de mi proyecto TeX
- Incrustar la imagen

Si quería hacer múltiples gráficos, tenía que repetir todo eso por cada nuevo gráfico. Y peor aún si quería hacer ajustes estéticos.

Al final terminé pseudo-automatizando la incrustación y renderización de gráficos.

Consiste en:

- Crear todos los gráficos que vayas a necesitar usando R
- Imprimir un gráfico por página en un archivo PDF
- Incrustar una página del pdf como imagen en LaTeX

Aunque en esencia pueda parecer un proceso más largo, lo único que tenemos que hacer cada que queramos actualizar los gráficos es **ejecutar el programa** y **recompilar el archivo TeX**

## Contenido
{:.no_toc}

* TOC
{:toc}

## Estructura del directorio

En la carpeta donde está localizado el archivo .tex, crearás una carpeta llamada img -o como quieras llamarla, pero ahí guardarás las imágenes para tu documento.

Dentro de img, escribirás el script en R que creará tus gráficos.

Algo así:
```
-/
├── img/
│ ├── plot.r
├── miDocumento.tex
```
## Script en R

Los siguientes gráficos son algo básicos y sólo sirven para ejemplificar el proceso que utilizo.

Primero, crearé dos gráficos con el conjunto *iris*, y los almacenaré en el archivo "irisPlot.pdf":

```r
# Incluír librería
library(ggplot2)

# Escribir pdf, y definir el tamaño de la hoja
pdf("irisPlot.pdf", width=4, height=2)

# Crear primer gráfico
irisSepal = ggplot(iris, aes(x=Sepal.Length, y=Sepal.Width)) +
            geom_point(colour = "#0277BD")

# Imprimir primer gráfico
plot(irisSepal)

# Crear segundo gráfico
irisPetal = ggplot(iris, aes(x = Petal.Length, y = Petal.Width)) + 
            geom_point(colour = "#FF8F00")

# Imprimir segundo gráfico
plot(irisPetal)
```


y luego dos gráficos con el conjunto *diamonds*, y los almacenaré en el archivo "diamondsPlot.pdf":

```r
# Incluír librería
library(ggplot2)

# Escribir pdf, y definir el tamaño de la hoja
pdf("diamondsPlot.pdf")

# Crear primer gráfico
caratPrice = ggplot(diamonds, aes(carat, price)) +
            geom_hex()

# Imprimir primer gráfico
plot(caratPrice)

# Crear segundo gráfico
cutPrice = ggplot(data=diamonds, aes(x=price)) +
            geom_histogram(binwidth=500)

# Imprimir segundo gráfico
plot(cutPrice)
```

Los dos archivos resultantes son [irisPlot.pdf](https://drive.google.com/file/d/0BzX5n5sP6iUGMEp4S2xtYWZmODQ/view?usp=sharing) y [diamondsPlot.pdf](https://drive.google.com/file/d/0BzX5n5sP6iUGYnZVbHB2RG9fN3c/view?usp=sharing)

---------------------

De los dos gists anteriores, las líneas que merecen la atención son:

```r
pdf("miArchivo.pdf")
%...
%...
plot(figura)
```

El primero, escribe el archivo PDF, y el segundo, imprime «figura» en una página del PDF.

## Incrustarlos en documento TeX

Ahora tenemos que insertar los gráficos creados en nuestro documento .tex

```TeX
\documentclass{article}

  \usepackage{graphicx} % Paquete para incluir recursos gráficos
  \graphicspath{./img/} % Especificar ruta de imágenes

  \begin{document}

    \begin{center} % Centrar contenido
      % Incluir primera página del archivo irisPlot
      \includegraphics[width=.8\textwidth, page = 1]{irisPlot}
      % Incluir segunda página del archivo irisPlot
      \includegraphics[width=.8\textwidth, page = 2]{irisPlot}
      %
      %Incluir primera página del archivo diamondsPlot
      \includegraphics[width=.4\textwidth, page = 1]{diamondsPlot}
      %Incluir segunda página del archivo diamondsPLot
      \includegraphics[width=.4\textwidth, page = 2]{diamondsPlot}  
    \end{center}
\end{document}
```

Y el resultado [se ve así](https://drive.google.com/open?id=0BzX5n5sP6iUGcW54U2lkRGtGU2M).


De nuevo, las líneas que merecen la atención son:

```TeX
\usepackage{graphicx}
\graphicspath{./img/}
%...
%...
\includegraphics[page = 1]{irisPlot}
```

Los primeros dos incluyen el paquete graphicx y especifican la ruta para los recursos gráficos.

La última línea es la manera en la que se incluye un gráfico desde un PDF especificando la página

## Actualizar gráficos

Si queremos cambiar detalles de los gráficos como la fuente de los datos, los colores, etiquetas, o proporciones, basta con ejecutar el script de R, y re-compilar el archivo en LaTeX.

## Conclusión

Tal vez no sea la manera más eficiente de elaborar y renderizar gráficos en nuestros documentos LaTeX. Tal vez haya mejores formas, más automatizadas. Sin embargo, este *método* funcionó para mí, y me consiguió ahorrar tiempo. Especialmente cuando se trataba de actualizar varios gráficos