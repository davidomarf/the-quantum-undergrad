---
title: "Crear una aplicación web con Node.js en un repositorio de GitHub"
categories:
  - computación
tags:
  - aplicación web
  - web
---

En esta -muy- pequeña guía aprenderás a crear y montar un servidor para un aplicación web usando Node.js.

La aplicación creada la alojaremos en GitHub para poder integrar *Apps* del *Marketplace* y facilitar el proceso de desarrollo.

Para esto, asumo que tienes [git](https://git-scm.com) y [Node.js](https://nodejs.org) instalados.

## Contenido
{:.no_toc}

* TOC
{:toc}

## Parte 1: El repositorio

Puedes crear un repositorio nuevo para tu proyecto, o utilizar uno ya creado. Sea lo que sea, asegúrate de [crear un .gitignore](https://www.gitignore.io) en tu directorio raíz. De no hacerlo, terminarás subiendo varios MBs de código en módulos de Node.js.a

El repositorio «muestra» que usaré es [DavidOmarF/node-app](https://github.com/DavidOmarF/node-app)

### Clonar el repositorio

Puedes utilizar alguna interfaz gráfica de git, o hacerlo mediante línea de comandos, lo importante es que tengas una copia local.


```
git clone https://github.com/DavidOmarF/node-app
```

Recomiendo cambiar el directorio de la consola al recién creado:

```
cd ./node-app
```

## Parte 2: El servidor

### Crear package.json

Este archivo contiene información relevante sobre el proyecto, como el nombre, autor, versión, módulos, etc...
Puedes leer más sobre este archivo y cada una de sus propiedades en [el sitio de npm](https://docs.npmjs.com/files/package.json).

Para crear el archivo automáticamente, sólo ejecuta este comando y después *spamea* la tecla Enter

```
npm init
```

### Instalar el generador de Express

[Express](http://expressjs.com/es/) es un *framework* para desarrollo web. El [generador de Express](http://expressjs.com/es/starter/generator.html) crea rápidamente un esqueleto. Para instalarlo, ejecuta el comando

```
npm install -g express-generator
```

### Crear proyecto con Express
Si llamamos al comando `express` desde la consola, podremos crear un esqueleto nuevo. El comando

```
express node-app
```
creará una nueva carpeta con el nombre `node-app`, que contiene los archivos necesarios para poder iniciar el servidor.

**Te recomiendo que el nombre que elijas sea el nombre del repositorio.**

## Mover los archivos de Express, a la carpeta raíz
No es **indispensable**, ya que podemos desplegar la aplicación desde un subdirectorio, pero es terriblemente complicado -¡especialmente si es nuestra primera aplicación!

Así que para evitar esos problemas, será mejor que muevas la aplicación a la carpeta raíz.

Simplemente arrastra el contenido de la carpeta creada por Express a la carpeta de tu repositorio.

Después, elimina la carpeta vacía.

## Instalar módulos necesarios de npm

En la carpeta raíz de tu repositorio, ejecuta el comando

```
npm install
```
éste instalará los módulos necesarios para que el servidor funcione. Estos están especificados en package.json

Y básicamente, tu aplicación web ya está lista para ser montada localmente usando

```
npm start
```

y visitando el servidor local en el puerto 3000 ([http://localhost:3000](http://localhost:3000)).

El servidor continuará ejecutándose hasta que no lo detengas. Para hacerlo, ve a la consola en donde lo iniciaste y presiona `Ctrl` + `C`

## Mandar cambios al repositorio
Bastante «estándar»:

```shell
git add -A
git commit -m "Installed Node.js server"
git push origin
```

Ahora el repositorio en GitHub debe de haber recibido los cambios: [DavidOmarF/node-app](https://github.com/DavidOmarF/node-app/tree/00-create-node-app) ¡El servidor ya está ahí!

Ahora, es turno de modificar la aplicación -¡Haz de este esqueleto, **tu aplicación**!