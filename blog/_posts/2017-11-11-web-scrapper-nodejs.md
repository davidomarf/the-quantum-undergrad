---
title: "Construyendo un extractor web con NodeJS, Cheerio, y Request"
categories:
  - minado de datos
tags:
  - datos
  - extracción web
---

Desde hace ya un año, había tenido planeado desarrollar un bot para Messenger. Éste recibiría un mensaje
con el nombre de un artista y una canción, y devolvería la letra.

Pero desde el momento en que lo consideré desarrollar, hasta hace una semana, se había quedado en la fase de "ojalá".

Durante los últimos días había comenzado a desarrollar aplicaciones web, gracias a [FreeCodeCamp](https://www.freecodecamp.org).

Así que aproveché y decidí, finalmente, construirlo.

_________________

Lo primero que tuve que desarrollar, fue [mi propia API](https://gimme-the-lyrics.glitch.me).

La API es la que hace el trabajo del bot. Éste último sólo lo presenta de una manera más amigable.

Para que mi API funcionara, tenía que **extraer datos de la web**. Y eso es lo que motivó la escritura de este artículo.

## Contenido
{:.no_toc}

* TOC
{:toc}

## Introducción

Planeba explicar qué era la extracción de datos web. Afortunadamente, el término es bastante autodescriptivo.

Podemos extraer datos **estáticos** y datos **dinámicos**.

Los datos **estáticos** de una web, son aquellos que son parte del archivo fuente de la página; los **dinámicos** aquellos que son generados.

En palabras más chabacanas, y tal vez un poco inexactas:

Los estáticos son parte del archivo html **antes de ser cargado por el navegador**. Por ejemplo, este artículo.

Los dinámicos se generan **durante la ejecución del sitio**, por ejemplo, los resultados de una búsqueda en Google.

_________________

En este artículo describiré cómo es que hice para extraer contenido HTML de la página estática de cada canción en [Genius](http://genius.com){:target="_blank"}

## Preparaciones

Lo primero que tenemos que hacer es iniciar el proyecto con `npm init`. Podemos configurar cada uno de los campos, pero por ahora, y para mí, basta con spamear el Enter.

Lo segundo, es instalar las dependencias de nuestro proyecto.

```
npm install --save cheerio
npm install --save request
```

Esto nos dejará con un par de líneas en nuestro archivo `package.json` que se miran algo así:

```json
"dependencies": {
    "cheerio": "^1.0.0-rc.2",
    "request": "^2.83.0"
  }
```

## Escribiendo el extractor

Ahora vamos a crear nuestro *script* principal, al que yo llamaré `index.js`.

### Incluir nuestros paquetes

```javascript
const cheerio = require('cheerio');
const request = require('request');
```

### Definir la URL que usaremos

En una aplicación más «real», la URL la generaríamos programáticamente. Por ahora, sólo asumiré que ya está generada y que es la siguiente:

```javascript
const url = "https://genius.com/Billy-joel-uptown-girl-lyrics"
```

### Crear una copia del código fuente

Aquí comenzamos a echar mano de los paquetes que incluimos.

`request(url, callback)` tomará dos argumentos. El primero, es la dirección web de la página que queremos extraer, y el callback... bueno. Si sabes qué es un callback, no es necesario que lo explique; y si no, no podría hacerlo sin extenderme demasiado.

Pero no te preocupes, no es indispensable que sepas cómo funciona, sólo debes saber que envía una función como argumento.

La llamada a request lucirá así:

```javascript
request(url, function (err, res, body) {
    if (err) throw err;
});
```

Y ahora, la variable `body` contendrá todo el contenido HTML de la página.

### Habilitar el uso de selectores

Con `cheerio` podremos utilizar selectores de la misma manera en que lo haríamos en jQuery.

```javascript
request(url, function (err, res, body) {
    if (err) throw err;

    let $ = cheerio.load(body);
})
```

Ahora, utilizando selectores podemos extraer el contenido que queramos. Pero para eso tenemos que saber cómo está compuesta la página.

## Explorando la página

Para saber qué es lo que debe extraer nuestro script, tenemos que conocer la estructura de la página.

Básicamente, este paso consiste en encontrar qué valores de `clase` o `id` tiene el elemento que nos interesa.

Podemos hacerlo explorando **tooodo** el código fuente, o podemos utilizar otras herramientas, como la consola de desarrolladores.

Yo utilizo Chrome, y la consola se abre con F12. O podemos abrir un menú contextual con click derecho en el elemento que queremos, y seleccionar `Inspeccionar`.

![Inspeccionar elemento](/assets/images/inspeccionar-elemento.png){:class ="img-responsive"}

Esto abrirá una nueva sección en nuestra pestaña actual en la que se resaltará el elemento que estamos inspeccionando.

Lo que yo hago, y que después de practicar, me resulta algo «inmediato», es leer las etiquetas *padre* hasta encontrar un `div`.

![Uptown Girl, Lyrics](/assets/images/codigo-fuente-uptown-girl.png){:class="img-responsive"}

En este caso, el primer `div` *padre* del elemento que quiero, es:

```html
<div class = "lyrics">
```

Y la verdad, suena bastante lógico, así que esa será la **clase** que voy a extraer en mi código.

## Extrayendo los datos

De vuelta al código.

El selector para una clase es `$(".mi-clase")` -para un id es `$('#mi-id')`. Pero esto devolverá un objeto.

Para acceder al contenido html de la etiqueta, podemos llamar el prototipo `.html()`.

Para acceder al texto de la etiqueta, `.text()`

```javascript
let lyrics = $(".lyrics").text();
```

Pero el valor que regresa puede tener muchos espacios al principio y al final, para limpiarlo, simplemente agregamos `.trim()`.

```javascript
let lyrics = $(".lyrics").text().trim();
```

Y listo. Para verlo en acción, puedes copiar este código y ejecutarlo con `node <nombre-archivo>.js`.

```javascript
const cheerio = require('cheerio');
const request = require('request');

const url = "https://genius.com/Billy-joel-uptown-girl-lyrics"

request(url, function (err, res, body) {
    if (err) throw err;

    let $ = cheerio.load(body);
    let lyrics = $(".lyrics").text().trim();
    console.log(lyrics)
})
```

![Letra de la canción impresa en la consola](/assets/images/letras-impresas-consola.png){:class="img-responsive"}

## Conclusión

Esta implementación funciona perfectamente bien, siempre y cuando estemos seguros que la página que estamos visitando tiene su propio código fuente, y no es generado cada vez que se consulta.

Actualmente estoy trabajando en un extractor de datos dinámicos para mejorar la API.

¿Por qué?

Porque funciona bien, siempre y cuando proporcionemos el nombre de artista y canción correctos.
Pero si tenemos un error en la escritura de cualquiera de los dos, visita un sitio que no existe.

Y si visita un sitio que no existe, no habrán datos que extraer.

Por ejemplo:

[Phil Collins, Another Day in Paradise](https://gimme-the-lyrics.glitch.me/phil%20collins&another%20day%20in%20paradise){:target="_blank"} funciona bien;

[Phill Collins, Another Day in Paradise](https://gimme-the-lyrics.glitch.me/phill%20collins&another%20day%20in%20paradise){:target="_blank"}, no.

La solución que planeo implementar es obtener la mejor coincidencia en una búsqueda, que es más flexible en cuanto errores de escritura o información incompleta.

Escribiré sobre ello en cuanto esté listo.