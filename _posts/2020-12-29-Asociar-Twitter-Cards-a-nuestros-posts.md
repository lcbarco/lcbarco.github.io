---
layout: post
title: Asociar Twitter Cards a nuestros posts
summary: Crea una Card de Twitter para que puedas compartirla
author: lcbarco
image: /images/twitter-cards.png
---

El otro día, cuando fui a compartir un post de mi blog en **Twitter**, me di cuenta que sólo salía la url del mismo. Investigando un poco, me di cuenta que necesitaba añadir más información a nuestro post para que **Twitter** pudiera generar lo que se llama una [Card](https://developer.twitter.com/en/docs/twitter-for-websites/cards/overview/abouts-cards).



![Ayuda de Twitter sobre Cards](/images/twitter-cards.png)

<!--more-->

## Todos son metas
Para que **Twitter** pueda generar una **Card** con la información necesaria para representarla en un **Tweet**, es necesario añadir una serie de **metas** al post:

```html
  <!-- Twitter cards -->
    <meta name="twitter:site"    content="@lcbarco">
    <meta name="twitter:creator" content="@lcbarco">
    <meta name="twitter:title"   content="¿Cómo asocio mi propio dominio a mi blog?">
    <meta name="twitter:description" content="Usa tu propio dominio en tu blog">
    <meta name="twitter:card"  content="summary_large_image">
    <meta name="twitter:image" content="https://lcbarco.com/images/lcbarco_com.png">
  <!-- end of Twitter cards -->
```

Para ello vamos a modificar el fichero *_includes/meta.html* para añadir los metas necesarios:

```
  <!-- Twitter cards -->
    <meta name="twitter:site"    content="@{ { site.twitter_username }}">
    <meta name="twitter:creator" content="@{ { page.author }}">
    <meta name="twitter:title"   content="{ { page.title }}">

    { % if page.summary %}
    <meta name="twitter:description" content="{ { page.summary }}">
    { % else %}
    <meta name="twitter:description" content="{ { site.description }}">
    { % endif %}

    { % if page.image %}
    <meta name="twitter:card"  content="summary_large_image">
    <meta name="twitter:image" content="{ { site.url }}{ { page.image }}">
    { % else %}
    <meta name="twitter:card"  content="summary">
    <meta name="twitter:image" content="{ { site.title_image }}">
    { % endif %}
  <!-- end of Twitter cards -->
```


## Añadir la información para generar el Card

Una vez que hemos modificado el fichero de metas, vamos a añadir la información que va a aparecer.

Primero añadiremos la información general a *_config.yml*. En mi caso sólo necesitaba añadir el campo de mi cuenta de Twitter:

```yaml
# Global info for Twitter Cards
twitter_username: lcbarco
```

A continuación debemos añadir en la cabecera de cada post la información concreta del post para generar el Twitter Card:
```yaml
summary: Usa tu propio dominio en tu blog
author: lcbarco
image: /images/lcbarco_com.png
```

Ahora ya si que podemos compartir nuestro post en Twitter y se generará la Card molona del mismo.
![Card de Twitter al compartir](/images/card-post.png)

## Conclusiones
Ahora gracias a nuestra Card, nuestro post quedará más lucido en Twitter. Prueba a crear el tuyo y contáctame si tienes algún problema enviándome un email a [lcbarco@gmail.com](mailto:lcbarco@gmail.com) o a través de mi cuenta de Twitter [https://twitter.com/lcbarco](https://twitter.com/lcbarco).






