---
title: "Diccionarios, recursión, y Fibonacci"
categories:
  - programación
  - algoritmo
tags:
  - recursión
  - memoización
  - recursion
---

Un arreglo asociativo -o más comúnmente llamado mapa o diccionario-, es un tipo de dato abstracto.

Está compuesto por una colección de pares (clave, valor).

La clave de cada par debe ser única en todo el diccionario, pero el valor puede estar repetido.

La mayoría de lenguajes cuenta con diccionarios de manera primitiva, o con la inclusión de librerías. Puedes consultar una <a href="https://www.wikiwand.com/en/Comparison_of_programming_languages_(associative_array)">lista comparativa</a> en Wikipedia.

Los diccionarios tienen varias aplicaciones importantes, incluyendo los patrones de diseño de decorador y <em>memoización</em>.
<h2>Memoización</h2>
La <em>memoización</em> es un patrón de diseño de software que puede acelerar la ejecución de programas.

Consiste en «recordar» los resultados computados anteriormente. Así, cuando esos resultados quieran usarse de nuevo, no será necesario calcularlos otra vez, sólo se recupera la versión almacenada.

<hr />

Para poder ejemplificar el uso de los diccionarios y el patrón de <em>memoización</em>, los utilizaré para mejorar esta función fib.

<script src="https://gist.github.com/DavidOmarF/3aa7a33ef9ec1df9b8bcc4bd36b459ba.js"></script>

Este algoritmo es ineficiente, pues el número de recursiones que tiene que hacer aumenta increíblemente rápido.

Por ejemplo, si queremos calcular <strong>fib(6)</strong>, las llamadas recursivas se verán algo así:

<a href="http://davidomar.me/es/blog/diccionarios-y-memoizacion/recursive_fibonacci/" rel="attachment wp-att-338"><img class="aligncenter size-full wp-image-338" src="http://davidomar.me/wp-content/uploads/2017/10/Recursive_fibonacci.png" alt="" width="1294" height="453" /></a>

Tanto <strong>fib(5)</strong> como <strong>fib(6)</strong> son llamados sólo una vez, pero <strong>fib(4)</strong> dos veces, y <strong>fib (3)</strong> tres.
<h3>Diccionarios</h3>
Para optimizar este algoritmo vamos a utilizar un diccionario. Éste contendrá todos los números de Fibonacci de 1 a n.

Sabemos que <strong>fib(1) = 1</strong>, y <strong>fib(2) = 1</strong>. Por lo tanto, nuestro diccionario inicial lucirá algo así:
<pre><code>computed_fib = {1:1, 2:1}
</code></pre>
Para que podamos consultar el diccionario dentro de la función fib(), necesitamos recibir el diccionario. Así que tenemos que cambiar nuestra definición:
<pre><code>def fib(n, computed_fib):
</code></pre>
también hay que escribir una manera de

a) revisar si el número que buscamos ya existe en el diccionario
<pre><code>if n in computed_fib:
return computed_fib[n]
</code></pre>
b) calcularlo y añadirlo al diccionario (si no existe)
<pre><code>nth_fib = fib(n - 1, computed_fib) + fib(n - 2, computed_fib)
computed_fib[number] = nth_fib
return nth_fib
</code></pre>
<h4>Mutabilidad</h4>
Al final, <em>fib</em> queda definida de esta manera:

<script src="https://gist.github.com/DavidOmarF/10a1b901f026bfbab938add098064023.js"></script>

¡Mucho mejor! Pero habría un problema con esta definición: tenemos que cambiar la manera en la que invocamos la función, ya que recibe dos argumentos.

Específicamente, tendríamos que llamarla enviando un diccionario conteniendo al menos los casos base.
<pre><code>fib(6, {1:1, 2:2})
</code></pre>
Y eso puede traer problemas, como enviar un diccionario inválido. Además <strong>se ve feo</strong>.

Para arreglarlo, vamos a hacer que <em>computed_fib</em> sea recibido con un valor por defecto.

Esto es: que si no se envía un argumento manualmente, tomará un valor pre-definido.

Podemos definirlo de esta manera:
<pre><code>def fib(n, computed_fib = {1:1, 2:1}):
</code></pre>
pero es considerado una <strong>pésima práctica</strong> por <a href="https://docs.quantifiedcode.com/python-anti-patterns/correctness/mutable_default_value_as_argument.html">algunas cosas oscuras y truculentas de los objetos mutables</a>.

así que mejor lo predeterminamos en <em>None</em>, y lo creamos después:
<pre><code>def fib(n, computed_fib = None):
if computed_fib is None:
computed_fib = {1:1, 2:1}
</code></pre>
Así podremos llamar fib(n) y fib(n, dict) sin problema alguno.
<h2>Estadísticas</h2>

<hr />

<strong>tl;dr: Al calcular el 40-ésimo término, la recursión pura hace más de 200 millones de llamadas en 51s. Con memoización, 77 llamadas en 0.00s</strong>

<hr />

Veamos algunas estadísticas sobre el número de llamadas recursivas, y el tiempo de ejecución de cada algoritmo:

Nota: Originalmente planeé calcular todos los números de <strong>fib(1)</strong> a <strong>fib(100)</strong>. Con esto no hablo de calcular <strong>fib(100)</strong>, sino de calcular <strong>fib(1)</strong>, y luego <strong>fib(2)</strong>, y luego <strong>fib(3)</strong>, etc...
<pre><code>for i in range(1, 101):
    stats(fib(i))
</code></pre>
Sin embargo, pasadas poco más de dos horas, decidí interrumpir el programa. Y para enterarme que sólo había calculado hasta fib(48). ¡Y había tardado 49 minutos <strong>sólo en ese último</strong>!

Pero perdí los dos archivos .csv que había generado al re-ejecutar el programa con un número más pequeño sin respaldar los dos archivos creados al principio.

De cualquier forma, re-ejecuté hasta fib(40), y aún ahí se puede ver la <strong>enorme</strong> diferencia entre ambos algoritmos.

El número de llamadas recursivas por algoritmo es:
<table>
<thead>
<tr>
<th align="right">n</th>
<th align="right">No-memoización</th>
<th align="right">Memoización</th>
</tr>
</thead>
<tbody>
<tr>
<td align="right">1</td>
<td align="right">1</td>
<td align="right">1</td>
</tr>
<tr>
<td align="right">2</td>
<td align="right">1</td>
<td align="right">1</td>
</tr>
<tr>
<td align="right">3</td>
<td align="right">3</td>
<td align="right">3</td>
</tr>
<tr>
<td align="right">.</td>
<td align="right">.</td>
<td align="right">.</td>
</tr>
<tr>
<td align="right">38</td>
<td align="right">78,176,337</td>
<td align="right">73</td>
</tr>
<tr>
<td align="right">39</td>
<td align="right">126,491,971</td>
<td align="right">75</td>
</tr>
<tr>
<td align="right">40</td>
<td align="right">204,668,309</td>
<td align="right">77</td>
</tr>
</tbody>
</table>
Y el tiempo de ejecución (en segundos) de cada uno:
<table>
<thead>
<tr>
<th align="right">n</th>
<th align="right">No-memoización</th>
<th align="right">Memoización</th>
</tr>
</thead>
<tbody>
<tr>
<td align="right">1</td>
<td align="right">0.0000 s</td>
<td align="right">0.0000 s</td>
</tr>
<tr>
<td align="right">2</td>
<td align="right">0.0000 s</td>
<td align="right">0.0000 s</td>
</tr>
<tr>
<td align="right">3</td>
<td align="right">0.0000 s</td>
<td align="right">0.0000 s</td>
</tr>
<tr>
<td align="right">.</td>
<td align="right">.</td>
<td align="right">.</td>
</tr>
<tr>
<td align="right">38</td>
<td align="right">20.2371 s</td>
<td align="right">0.0000 s</td>
</tr>
<tr>
<td align="right">39</td>
<td align="right">32.7778 s</td>
<td align="right">0.0000 s</td>
</tr>
<tr>
<td align="right">40</td>
<td align="right">53.0221 s</td>
<td align="right">0.0000 s</td>
</tr>
</tbody>
</table>
Con esto queda claro que la memoización es un patrón de diseño excelente en casos como este.
<h4><strong>OK, AQUÍ LAS COSAS SE EMPIEZAN A TORNAR UN POCO OSCURAS, TODO ESTO ERA INNECESARIO, PERO AÚN ASÍ LO ESCRIBÍ. y peor aún: aún así lo publiqué.</strong></h4>
Pero no importa si no pude recuperar el 49no número en la secuencia de Fibonacci, por que podemos hacer una estimación con los datos que tenemos.

Tanto el número de llamadas recursivas como el tiempo de ejecución de la implementación recursiva, se comportan como la secuencia de Fibonacci.

Las llamadas pueden calcularse de manera exacta. El tiempo no.

En concreto:
<pre><code>n_llamadas(n) = n_llamadas(n-1) + n_llamadas(n-2) + 1
tiempo(n) =~ tiempo(n-1) + tiempo(n-2)
</code></pre>
El problema serían los casos base, pero creo que con utilizar los últimos dos datos registrados bastará.

Para eso sólo llamaremos a la función enviando nuestros propios diccionarios.

Así que veamos qué tantas llamadas y tiempo haría para calcular 1000 números fibonacci:

fib(1000) haría...

86, 933, 115, 373, 874, 912, 871, 377, 055, 350, 081, 251, 605, 129, 321, 034, 743, 560, 804, 963, 458, 179, 073, 110, 835, 898, 103, 780, 807, 759, 680, 158, 510, 338, 591, 845, 186, 160, 645, 269, 550, 419, 379, 246, 479, 746, 644, 942, 323, 285, 992, 881, 813, 066, 375, 876, 597, 939, 299, 857, 032, 007, 408, 952, 275, 590, 333, 698, 457, 749

llamadas en, aproximadamente,

22, 368, 247, 025, 775, 198, 923, 204, 500, 838, 004, 838, 905, 889, 316, 192, 143, 756, 994, 318, 944, 191, 936, 469, 718, 811, 583, 554, 057, 695, 250, 902, 151, 169, 111, 265, 234, 166, 779, 627, 076, 117, 356, 815, 012, 808, 335, 317, 548, 081, 991, 314, 018, 847, 704, 591, 467, 486, 307, 969, 223, 542, 098, 027, 384, 185, 813, 172

segundos.

O 86.933 x10^205 llamadas en 22.368 x10^199

O 86 <em>69-illones</em> de llamadas en 22 <em>67-illones</em> de segundos.

¿cuánto son 22 <em>67-illones</em> de segundos? Bueno, más o menos 709 64-illones de años.

Considerando que la estimación de la edad de la tierra es de 4,540,000,000 años, son como 156 62-illones de vidas-tierra.