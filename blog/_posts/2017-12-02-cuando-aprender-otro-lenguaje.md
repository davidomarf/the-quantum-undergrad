---
title: "Aprender un nuevo lenguaje de programación: ¿cómo, cuándo y por qué?"
categories:
  - programación
tags:
  - lenguaje
hidden: true
---

La semana pasada salí de una «crisis mental» en la que perdí casi toda motivación, interés, y entusiasmo por cualquier cosa.

Después de casi un mes de no crear, escribir, leer, o aprender nada, decidí que quería extender, tanto en amplitud como en profundidad, mi conocimiento en programación.

Quería aprender nuevos conceptos y paradigmas. Podía hacerlo de varias formas, pero me terminé convenciendo de que tal vez lo más sencillo para mí, sería «adquirirlo» programando en diferentes lenguajes que explotaran esos conceptos más allá de lo cotidiano.

¿A qué me refiero? Imaginemos que quiero aprender sobre programación funcional. Podría tratar de aprender usando lenguajes multi-paradigma que incluya el paradigma funcional de manera «impura»: JavaScript, Python, Ruby, etc. O podría utilizar un lenguaje de programación funcional **pura** como Haskell o Elm.

Entonces, seleccioné un par de conceptos de los que quería aprender, y comencé mi pequeña búsqueda para saber qué lenguaje era el indicado para ir adquiriendo tal concepto.

Después de una media hora, encontré un libro por Bruce A. Tate: [Seven Languages in Seven Weeks](https://pragprog.com/book/btlang/seven-languages-in-seven-weeks)

## Prefacio

La semana pasada me dio por aprender nuevos lenguajes. El plan original era encontrar y seleccionar ~5 lenguajes, para implementar los mismos algoritmos en cada uno de ellos.

Los algoritmos que usaría estaban por decidirse, pero imaginaba cosas «estándar»: ordenación, búsqueda, regresión, algo de programación dinámica, algo con grafos, etc.

Después de unas horas de búsqueda, había creado mi lista: Ensamblador, C, C++, C#, Haskell, Java, Python, Scheme, Smalltalk.

Era fluido en C y Python; estaba familiarizado con C# y Haskell; respetaba Ensamblador; ignoraba Scheme y Smalltalk; odiaba -dos veces en el pasado- a Java.

Si ahora mismo alguien me preguntara cuál había sido el criterio de selección, no sabría responder.

Como sea, justo antes de comenzar bastante desorientado, pero decidido, decidí hacer una última sesión de búsqueda, y me encontré con [Seven Languages in Seven Weeks](https://pragprog.com/book/btlang/seven-languages-in-seven-weeks){:target="_blank"}.

**Sin querer, encontré algo que sin saber buscaba.**

## Introducción

Las razones por las que alguien aprende un segundo lenguaje *–por ahora hablo fuera del contexto de la programación–* pueden ser varias: avanzar su carrera, adaptarse al cambio, o siemplemente, y mi favorita: **por que sí**.

Sea cual sea la razón, al aprender nuevos lenguajes, te *ilustras*. Además, puede influenciar la manera en que piensas.

Pasa lo mismo con los lenguajes de programación. Cada uno *tiene lo suyo*. Y cada uno va a aportarte diferentes conceptos, que eventualmente, te convertirán en un mejor desarrollador.

Cuando estás aprendiendo tu primer lenguaje —incluso el segundo—, un curso introductorio completo puede ser útil. Pero cuantos más vamos aprendiendo, más inútil se vuelve un curso.

En un principio, tal vez era indispensable saber cómo declarar una variable. Cómo asignar y leer un valor, cómo operar, cómo hacer ciclos, o cómo probar valores lógicos.

Ahora, mirar el "Hola, Mundo!" y tal vez "Fibonacci", es más que suficiente para que empecemos a experimentar por cuenta propia. Y si algo sale mal, una búsqueda rápida soluciona nuestro problema.

Ya no necesitamos *tantear las aguas*. Necesitamos un clavado. Algo que sea rápido, explosivo, y nos lleve a las profundidades del lenguaje.

Necesitamos volver a sentirnos en aprietos, como cuando entramos al agua por primera vez, y sentimos ahogarnos cuandeo sólo nuestros pies estaban dentro.

Durante el resto del artículo, te explicaré cómo es que "ataco" un nuevo lenguaje, y cómo puedes saltarte las guías que te explican lo mismo que ya has aprendido antes.

## Conociendo la alberca

Bueno, he de confesar que antes te mentí un poquito. Pero sólo poquito: no vamos a darnos un clavado en una alberca de la que no sabemos nada.

Para saber con qué lenguaje nos estamos metiendo, es conveniente hacernos varias preguntas.

### ¿Cómo es el tipado?

Todo lenguaje ---o al menos eso espero--- tiene tipos de dato primitivos. Y cuando creamos variables, éstas adquieren un tipo. 

Cuando hablamos del *tipo de tipado*, nos referimos a la manera en la que le hacemos saber al programa de qué tipo es esa variable.

El tipado tiene dos criterios: estático/dinámico, y débil/fuerte.

C tiene un tipado estático:

```c
char* cadena = "Pichurri";
int entero = 3;
float decimal = 4.85;
```

JavaScript, dinámico:

```javascript
let cadena = "Despeñaperros";
let entero = 12;
let decimal = 1.125;
```

En cuanto a la *dureza* del tipado... las cosas son más ambiguas. Y averiguar si es fuerte o débil, se hace mientras se programa.

Algunos lenguajes permiten utilizar un tipo de dato, como si fuera **otro** tipo de dato.

```c
char letra = 'a';
printf("Char: %c, Val: %d", letra, letra);
// >> Char: a, Val: 127

int numero = 68;
printf("Char: %c, Val: %d", numero, numero);
// >> Char: D, Val: 68
```

C permite operar con un caracter como si fuera entero, y un entero como si fuera caracter. C es de tipado débil.

Java, por otro lado, no te concede esa libertad: Java es de tipado fuerte.

Existen más criterios para categorizar un lenguaje entre tipado fuerte o débil. Además, las cosas no son tan binarias. Existen lenguajes de tipado más débil que otros que también son débiles. Pero entrar en esos asuntos es meterse con seguridad de tipo, seguridad de memoria, chequeo dinámico, y chequeo estático. Esto lo dejaremos aquí.

----------------

No considero que exista un tipado mejor que otro: cada uno tiene sus ventajas y desventajas.

### ¿Cuál es el paradigma?

Afortunadamente, tanto para ti como para mí, no voy a ponerme a elaborar las diferencias, características, historia, ni nada sobre ningún paradigma.

Sólo voy a mencionar que es importante conocer el paradigma. ¿Es estructurado, orientado a objetos, funcional, multi-paradigma?

Consideraría ésta pregunta la más importante de todas. Conocer paradigmas es, en realidad, la motivación mayor detrás de conocer lenguajes.

Muy probablemente sea mejor conocer dos lenguajes de distintos paradigmas, que 10 del mismo, así que atrévete a variar tu aprendizaje explorando otros paradigmas.

### ¿Cómo se controla el flujo del programa?

Esto es: ¿qué estructuras de control tiene? Regularmente son sentencias **if** para tomar decisiones, y ciclos **for/while** para repetir código. Pero algunos lenguajes guardan sorpresas.

Recuerdo que me había acostumbrado tanto a los ciclos. Simplemente asumía que todos los lenguajes debían tenerlos. Pero cuando me enteré de que en Haskell no existían se me voló la peluca. Ahí dependes enteramente de la recursividad.

Como alternativa al uso de sentencias *if*, te encontrarás "patrones" en Haskell, Erlang, SML, y otros. O con "unificación" en Prolog.

### ¿Qué estructuras primitivas tiene?

Las colecciones son tan importantes como los tipos. Es la manera en la que almacenas, bajo un mismo nombre, más de un valor.

En lenguajes como Python o Ruby, puedes usar directamente los diccionarios (o tablas, mapas, hash).

En otros, como en C, sólo cuentas con arreglos, y tienes que arreglártelas para implementar toda otra estructura que necesites.

En algunos lenguajes, los arreglos pueden contener datos de diferente tipo. En otros, no.

### ¿Por qué es especial?

Como comenté antes, muchos lenguajes tienen ciertas peculiaridades. Algunos son tremendamente increíbles para computación matemática. Algunos aprovechan mejor que otros la concurrencia.

La respuesta a esta pregunta, debería ser la misma a la siguiente:

## Por qué aprender "ese" lenguaje

**tl;dr: te provee de nuevos conceptos, haciéndote mejor programador.**

Considero -al igual que miles de desarrolladores- que es necesario aprender bastantes lenguajes a lo largo de tu carrera para considerarte un buen desarrollador.

Pero más allá de aprender a programar un lenguaje, al menos para mí, es **aprender de él**.

Me refiero a que muchísimos lenguajes cuentan con alguna «peculiaridad». Tal vez algunos exploten una característica más que otros, o algunos sean mejor para familiarizarse con algún paradigma o concepto.

Y, para mí, ahí es donde está la importancia: saber *absorber* las características de un lenguaje, y aplicarlas a tu propio estilo de programación, mejorando con cada lenguaje que aprendemos.

Además, cuantos más lenguajes aprendes, más fácil es aprender el que sigue. Y el que sigue y el que sigue...

Algo que me ocurrió hace meses al intentar aprender Haskell -por tercera vez-, fue el absorber la idea de la inmutabilidad.

Desde entonces, procuro que todo el código que escribo, independientemente del lenguaje, esté libre de mutación.

## ¿Cómo aprender un nuevo lenguaje?

Esto varía. Y mucho.

Aprender un primer lenguaje será siempre lo más difícil. Seguido, al menos para mí, por aprender un lenguaje completamente opuesto a lo que estás acostumbrado: distinto paradigma, tipado, lógica, estructuras de datos, etc.

Si eres alguien que, como yo, *viene* de C, te será fácil comenzar a programar en JavaScript o Python. Pero Haskell o SML será tanto o más doloroso como haber aprendido C en primer lugar.

Como sea, aquí sólo me enfocaré para un cierto grupo de usuarios: aquellos a quienes les basta con leer algún "Hola, mundo!", "Fibonacci", o "Factorial", para empezar a experimentar por su propia cuenta. Aquellos que se saltan la parte de la creación de variables, asignación, creación de funciones, etc.