---
layout: post
title: ¿Cómo crear un blog con Jekyll y Github pages?
---

¿Por qué no uso **Wordpress** en vez de tener que usar **Jekyll** y **Github pages**? Dos motivos: sencillez y personalización.

**Wordpress** es un magnífico CMS (Content Management System) que nos permite tener fácilmente nuestro propio blog. 

Entonces, ¿por qué no lo uso?. **Worpress** te permite elegir entre realizar la instalación **On Premise** en tu propio servidor o hacer uso de su servicio de hosting. Yo no quería "perder tiempo" en realizar la instalación **On Premise** y en primera instancia opté por el servicio de hosting de Wordpress. El problema es que en su primer nivel de usuario de pago de Wordpress no se puede hacer uso de plugins con lo que al final es muy limitado.

Entonces me fijé en la integración **Jekyll** dentro de **Github pages**.

![Página home apkpure.com](/images/github-pages.png)
<!--more-->

## ¿Cómo empezar?
El método más sencillo para realizar la instalación sería buscar el **Theme** que más te gusta y partir de su fork en **Github**.

En mi caso el **Theme** que más me gustaba era [Jekyll Now](https://github.com/barryclark/jekyll-now).

Para ello accedemos a la página de Github de [Jekyll Now](https://github.com/barryclark/jekyll-now) y pulsamos sobre el icono Fork que aparece arriba a la derecha.

![Página del Theme al que hacer Fork](/images/fork-github.png)

Una vez realizado el Fork, nos aparecerá el repositorio con el mismo nombre que el repositorio del Theme. Ahora debemos cambiar el nombre del repositorio por el nuestro en Settings. El nuevo nombre debe llevar la sintaxis de \<username\>.github.io.

![Página de Settings de nuestro proyecto](/images/github-settings.png)

Para ver que todo funciona, sólo hace falta acceder a https://\<username\>.github.io para ver que se está publicando. Puede que tarde algunos segundos en actualizar la información.

## Entorno de edición en local
Se podría realizar la creación y edición de Posts desde la propia página de Github, pero sería un trabajo tedioso. Para ello vamos a realizar la edición en local. 

Lo primero de tenemos que tener instalado en local es la última versión de Jekyll. Enlazo la página web del Quickstart de Jekyll en el que se muestra [cómo realizar la instalación de Jekyll](https://jekyllrb.com/docs/). 

Un vez realizada la instalación hacemos un **clone** de nuestro proyecto en local y lanzamos el servidor interno de Jekyll con la opción de autoreload. Para ello ejecutamos:

```
git clone https://github.com/<username>/<username>.github.io.git
cd <username>.github.io
jekyll serve --livereload
```

Lo siguiente que debemos hacer es editar el archivo *_config.yml* y rellenar la información propia de nuestro blog: *título, descripción, redes sociales, etc...*

Desde este momento podremos ir viendo los cambios que vamos realizando en [http://127.0.0.1:4000/](http://127.0.0.1:4000/)

## Creación del primer Post
Lo primero que vamos a realizar es la creación de un nuevo **Post**. Los **Posts** se almacenan como ficheros independientes dentro de la carpeta **_posts**. Estos ficheros utilizan una sintaxis de tipo **Markdown** que posteriormente serán traducidas a html por **Jekyll**. Se puede usar como referencia la página web de [Markdown Guide](https://www.markdownguide.org/cheat-sheet/) para conseguir más información sobre cómo usar **Markdown**.

Haciendo uso de nuestro editor de texto favorito (Vim, Visual Studio Code, etc...), creamos un fichero que debe empezar por la fecha del post y la url que va a usar en formato **año-mes-día-\<url del post>.md**. Es recomendable hacer uso de los guiones normales para separar las palabras del nombre del fichero en vez de los guiones bajos ya que es mejor para el **SEO**.

El fichero empieza por la sección en la que indicamos los Metadatos del post. En nuestro caso indicamos el layout del Post y el título que se va a mostrar.

```
---
layout: post
title: ¿Cómo crear un blog con Jekyll y Github pages en 15 minutos?
---
```

A continuación iremos creando el post con la sintaxis de **Markdown**.

Siempre podremos modificar los diferentes layouts de la página web del Blog desde la carpeta *_layouts*, modificar la página principal *index.html*, modificar los estilos en *styles.scss*, etc...

## Publicación

Una vez realizados todos los cambios necesarios haremos **commit** de todos los cambios y **push** a la rama **master** de nuestro repositorio en Github para ver los cambios.

```
git add --all
git commit -m "first post"
git push origin master
```

## Conclusiones
Como veis es muy sencillo tener tu propio blog en cuestión de minutos. Prueba a crear el tuyo y contáctame si tienes algún problema enviándome un email a [lcbarco@gmail.com](mailto:lcbarco@gmail.com) o a través de mi cuenta de Twitter [https://twitter.com/lcbarco](https://twitter.com/lcbarco).






