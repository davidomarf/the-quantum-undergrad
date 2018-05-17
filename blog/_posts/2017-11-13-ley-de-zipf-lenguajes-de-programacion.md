---
title: "Visualizando la ley de Zipf en diferentes lenguajes de programación"
categories:
  - visualización
tags:
  - distribución
  - lenguaje
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

Hace un par de años me topé con un vídeo de VSauce en el que trata el tema de [«El misterio de Zipf»](https://www.youtube.com/watch?v=fCn8zs912OE){:target='_blank'}. Durante todo ese tiempo, hasta esta madrugada de noviembre en la que mezclaba mi quinta taza de café, había permanecido en mi cabeza como algo recurrente pero irrelevante.

Y es porque tuve la idea de querer de visualizar la ley de Zipf en códigos fuente. Incluso, más allá de eso, tratar de visualizar la propensión de algunos lenguajes a *cumplir* con la ley de Zipf.

O si el número de colaboradores, número de estrellas, *forkeos*, y más, tiene relación con ello.

Este pequeño proyecto estará compuesto de tres fases *básicas*:

* el minado de los archivos,
* el procesamiento de los archivos,
* la visualización de los datos.

## Contenido
{:.no_toc}

* TOC
{:toc}

## Introducción

La Ley de Zipf fue popularizada por George Zipf, lingüista en la Universidad de Harvard. Ésta refleja la manera en que se distribuye la frecuencia de distintos «eventos» en la naturaleza.

Para familiarizarnos un poco, digamos que existe un conjunto de $$n$$ eventos. Cada evento se repite cierta frecuencia $$P$$, y posee un rango $$k$$ que va en función de $$P$$: El de mayor frecuencia tiene rango 1, y el de menor frecuencia tiene rango n.

Y lo interesante de la Ley de Zipf, es que propone que la frecuencia de cualquier evento, es inversamente proporcional a su rango. Específicamente:

$$
\begin{align*}
  P_k \approx P_1 / k
\end{align*}
$$

donde $$P_k$$ es la frecuencia del evento en el rango $$k$$, y $$P_1$$ la frecuencia del evento en el rango 1.

![Distribución de Zipf](/images/posts/zipf/distribucion.svg)

Lo más sorprendente de la distribución de Zipf, es que no representa el comportamiento de uno o dos fenómenos, sino de **cientos**.

Por ejemplo, en la frecuencia de uso de las palabras de **cualquier lenguaje**. Incluso de aquellos que aún no logran descifrarse.

O la población de las ciudades, el tráfico de los sitios web, las magnitudes de los sismos, los ingredientes usados en libros de cocina, el diámetro de los cráteres de la luna, o —entre incontables más— el número de citas que reciben los artículos académicos.

Visualizar la distribución de Zipf se vuelve un poco difícil cuando el número de eventos es grande. Para mejorar su visualización, suele graficarse en una escala logarítmica.

![Distribución de Zipf](/images/posts/zipf/escalas.svg)

Entonces, ¿pueden los lenguajes de programación, al igual que los lenguajes naturales, comportarse de una manera que *cumpla* con la Ley de Zipf?

Esperadamente, ya se han realizado trabajos que abordan esa pregunta. 

[Abhinav Tushar](https://github.com/lepisma){:target='_blank'} en su artículo [Computer Programs and Zipf's law](https://lepisma.github.io/2015/01/14/computer-programs-and-zipf-law/){:target='_blank'} realiza una exploración al código fuente de Linux, FreeBSD, Bootstrap, y otros proyectos, tratando de visualizar su distribución de palabras reservadas.

[Sam Radhakrishnan](https://github.com/sam09){:target='_blank'} y otros colaboradores [analizaron Flask para tratar de verificar la Ley de Zipf en Python](https://github.com/sam09/zipf){:target='_blank'}.

En este proyecto, se analizarán son los 5 repositorios con mayor número de estrellas, desarrollados en cada uno de los 10 lenguajes más populares en GitHub, según el reporte [The State of the Octoverse 2017](https://octoverse.github.com){:target='_blank'}.

Tales lenguajes son **JavaScript, Python, Java, Ruby, PHP, C++, CSS, C#, Go, y C.**

Pero CSS, por no ser lenguaje de programación —y por que lidiar con las palabras reservadas sería un tormento—, lo voy a descartar, dando lugar a **TypeScript**.

## Minado de datos

Lo primero es construir una araña web. Yo decidí construirla en Python, por ser un lenguaje con el que tengo una mediana familiaridad en el que nunca he programado algo así.

Después, se debe crear un conjunto de datos. Éste contendrá:

- el lenguaje de programación, 
- el repositorio al que pertenece,
- el número de colaboradores,
- la fecha de creación,
- la fecha de la última actualización, 
- número de estrellas,
- *forkeos* del repositorio, y, 
- **lo más importante**: las ocurrencias de cada palabra clave.

Por ahora, la propiedad del número de ocurrencias quedará pendiente, ya que ésta la generaré en pasos siguientes.

Para lo que pretendo usar, seguramente no utilizaré ni siquiera la mitad de *propiedades* que voy a minar. Pero es que durante el desarrollo, se me ocurrió compartir el conjunto de datos. Así podré ver qué análisis pueden darle otras personas.

### Esquematización del proceso

1. **Escoger repositorios aleatoriamente**: Crear un archivo .csv, que contenga **n** direcciones web, apuntando a repositorios aleatorios. **Nota**: será importante ignorar los repositorios «recién nacidos»
1. **Minar todos los repositorios de la lista**: Obtener todos los archivos dentro de un repositorio, y procesar cada uno.

### Obtener direcciones de repositorios

Estaba comenzando a morir pensando cómo podía obtener una lista de repositorios *aleatoria*. Lista en la que no hubiera ninguna tendencia hacia ningún extremo en número de estrellas, forks, o fecha de actualización.

Los resultados de una búsqueda varían cada vez que sea hace una consulta, así que definitivamente no era una opción.

Después, encontré la API de GitHub. Específicamente [List all public repositories](https://developer.github.com/v3/repos/#list-all-public-repositories){:target='_blank'}.

Así que, escribo un programa para consultar la API recurrentemente, y me dedico a otras cosas mientras lo dejo ejecutando.

```python
import csv
import requests
import json

api = "https://api.github.com/repositories?since="
since = 0

url_csv = open("urls.csv", 'w+')

url = api + str(since)
response = requests.get(url, auth=('davidomarf','mi llave que no puedo compartirte :('))

while response.ok:
    url = api + str(since)
    response = requests.get(url, auth=('davidomarf','mi llave que no puedo compartirte :('))

    reposList = json.loads(response.content)
    for repo in reposList:
        url_csv.write(repo['html_url'] + '\n')

    since = since + len(reposList)

url_csv.close()
```

## Procesamiento del archivo crudo

Una vez habiendo obtenido el archivo crudo, tenemos que procesarlo, de forma que podamos contabilizar **sólo** las palabras clave.

Es importante ignorar los comentarios, ya que si uno de ellos contiene una palabra clave, se contará, a pesar de que no es parte del código.

Se me ocurren varias maneras de procesar cada cadena para encontrar las ocurrencias de cada palabra clave, pero la única que me parece sensata, para mantener la eficiencia, es el uso de un *trie* -- no me siento realmente cómodo pronunciando ese término.

Cada lenguaje contendrá su propio *trie* de palabras clave. Puedo hacerlo manualmente, o puedo hacerlo programáticamente. Primero, crearé un arreglo con todas las palabras clave para cada lenguaje.

Algo así:

```python
kws.py = ['def', 'for', 'if', ...]
kws.js = ['function', 'for', 'break', ...]
kws.go = ['packge', 'string', 'append', ...]
```

Eso también podría hacerlo manualmente o programáticamente. Pero hacerlo de la segunda manera vencería el propósito: ahorrar tiempo, así que no.

Después, definiría una función que me permita crear un *trie* dado un arreglo de palabras:

```python
_end = '_end_'
 
def make_trie(words):
    root = dict()

    for word in words:
        current_dict = root
        for letter in word:
            current_dict = current_dict.setdefault(letter, {})
        current_dict[_end] = _end

    return root
```
**Función robada de [senderle ](https://stackoverflow.com/a/11016430){:target='_blank'}

Y después, sólo actualizaría los valores de mi objeto `kws` usando esa función:

```python
kws.py = make_trie(kws.py)
```

```json
{
  "a": {
    "n": {
      "d": {
        "_end_": "_end_"
      }
    },
    "s": {
      "_end_": "_end_",
      "s": {
        "e": {
          "r": {
            "t": {
              "_end_": "_end_"
}}}}}}}
```


