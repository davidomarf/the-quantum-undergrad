---
title: "Sobre mí"
excerpt: "Esto es quien soy, lo que hago, y lo que creo."
permalink: /about

layout: single
align: center
header:
  overlay_filter: 0.5
  overlay_image: images/header.jpg
---

<script>
var description = [
  "escuchar música de abuelitos",
  "seguir subreddits de animalitos",
  "<a href = 'https://youtu.be/paqr3kdmcZg?list=PLwic3h1bAlblkSJ-U9YxEpTclFoUS_Otq' target=_blank>Woodkid</a>",
  "referenciar momentos de Los Simpson",
  "el arte generativo",
  "bailar (apesar de hacerlo ridiculamente mal)",
  "la carpintería"
];
var randomNumber = Math.floor(Math.random() * description.length);
</script>
<script>
window.onload = function() {
  var a = document.getElementById("random-description-switcher");
  a.onclick = function() {
    if (randomNumber < description.length - 1) {
      randomNumber++;
      document.getElementById("random-description").innerHTML =
        description[randomNumber];
    } else {
      randomNumber = 0;
      document.getElementById("random-description").innerHTML =
        description[randomNumber];
    }
    return false;
  };
};
</script>

Hola, me llamo David. Soy un estudiante en ciencias de la computación. Tengo un especial interés por la complejidad, el aprendizaje automático, la computación cuántica, y <script>document.write('—<a id="random-description-switcher" href="#">entre otras cosas</a>—, <span id="random-description"> ' + description[randomNumber] + '</span>');</script>.

Este sitio es, en parte, un intento por aprender y escribir sobre todo eso y otros temas que me causan interés.

## ¿Quieres trabajar conmigo? ¡Conectemos!

Puedes enlazar conmigo vía [LinkedIn](https://www.linkedin.com/in/davidomarfch/), o escribirme a [davidomarfch@gmail.com](mailto:davidomarfch@gmail.com). Ambos los reviso constantemente.

---

## Sobre el sitio

El sitio está construido usando [Jekyll](https://jekyllrb.com). El tema que uso es una versión un poco modificada de [Minimal Mistakes](https://mademistakes.com/work/minimal-mistakes-jekyll-theme/).

El dominio `.me` fue un obsequio por parte de [Namecheap](https://www.namecheap.com) incluido en [GitHub Student Pack](https://education.github.com/pack), y el alojamiento lo provee [GitHub Pages](https://pages.github.com).

Para manejar otras cosas como el certificado de seguridad y el caché del sitio, utilizo [CloudFlare](https://www.cloudflare.com).

