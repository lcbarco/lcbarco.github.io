---
layout: post
title: ¿Cómo asocio mi propio dominio a mi blog?
summary: Usa tu propio dominio en tu blog
author: lcbarco
image: https://lcbarco.com/images/lcbarco_com.png
---

En el blog anterior explicaba [¿cómo crear un blog con Jekyll y Github pages en 15 minutos?](/2020/11/22/Como-crear-un-blog-con-Jekyll-y-Github-pages.html). Esto nos permite tener un blog creado de forma sencilla, extendible y rápido.

Ahora lo que necesitamos es poder asociarle nuestro propio dominio y que no tengamos que usar la url suministrada por Github https://\<username\>.github.io.

![lcbarco.com](/images/lcbarco_com.png)

<!--more-->

## Configurar el dns para usar nuestro blog
Lo primero que debemos hacer es acceder al lugar donde tengamos comprado nuestro dominio y configurar los registros DNS necesarios para que funcione nuestro blog. Empezaremos añadiendo los registros **A** asociados a las diferentes **IPs** usadas por **Github**. También añadiremos un registro de tipo CNAME apuntando a la url suministrada hasta ahora por Github de nuestro blog.

![Configuración de registros A y CNAME](/images/dns-setting.png)

## Configurar el dominio en Github

Una vez que hemos creado los registros A y CNAME en nuestro servidor de DNS, indicamos a Github cuál es el dominio a usar.

Accedemos a la página de Settings del proyecto y en la parte inferior de la página, encontramos la sección **GitHub Pages**. En el apartado **Custom domain** indicamos el dominio que queremos usar. 

Debemos asegurarnos de marcar la opción **Enforce HTTPS** para que se encargue de generar un certificado asociado.

![Configuración del dominio](/images/git-hub-pages-domain.png)

Pasados unos segundos podremos acceder a nuestro blog usando nuestro propio dominio.


## Conclusiones
Como veis es muy sencillo tener tu propio dominio asociado a un blog. Prueba a crear el tuyo y contáctame si tienes algún problema enviándome un email a [lcbarco@gmail.com](mailto:lcbarco@gmail.com) o a través de mi cuenta de Twitter [https://twitter.com/lcbarco](https://twitter.com/lcbarco).






