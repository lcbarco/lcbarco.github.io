---
layout: post
title: ¿Cómo conseguir el código java de una app Android?
summary: Extraer el código de una aplicación Java es muy sencillo
author: lcbarco
image: https://lcbarco.com/images/dex2jar-1.png
---

Siempre me ha preocupado qué hacían las apks que instalo con mi información.

La mejor forma de saberlo es saber qué hace la app y a dónde se conecta.

El método “sencillo” sería conectar el móvil a un Hotspot WIFI en el que tuviéramos corriendo un sniffer tipo tcpdump.

Pero como no quiero montar la de Dios, prefiero decompilar la app para intentar averiguar lo que hace.

Lo primero que necesitaremos será el apk. Para ello nos podemos conectar a https://apkpure.com/es/ buscar la app que tenemos instalada y descargarla.

![Página home apkpure.com](/images/dex2jar-1.png)
<!--more-->

Para conseguir los ficheros java de la app, descargamos dex2jar de la página https://sourceforge.net/projects/dex2jar/ , descomprimimos el zip y copiamos dentro el apk de la aplicación. A continuación ejecutamos el comando d2j-dex2jar.sh

```
cp aplicacion_de_la_que_no_me_fio.apk dex2jar-2.0
cd dex2jar-2.0
sh d2j-dex2jar.sh aplicacion_de_la_que_no_me_fio.apk
```

Generará un fichero aplicacion_de_la_que_no_me_fio-dex2jar.jar.

Ahora necesitaremos el JD-GUI para poder sacar las clases java del jar. Para ello descargamos el programa de http://jd.benow.ca/

Una vez abierto y elegido el fichero jar, podemos navegar por el código java de la app. 

![Captura JD-GUI](/images/dex2jar-2.png)

 
Si también queremos sacar todos los recursos de la app, lo siguiente que tenemos que hacer es descargarnos el software Apk Tool https://ibotpeaches.github.io/Apktool/install/ para decompilar el fichero apk original. Para ello seguimos las instrucciones para instalarlo según nuestro sistema operativo.

~~~

apktool d aplicacion_de_la_que_no_me_fio.apk

~~~

![Resultado del terminal](/images/dex2jar-3.png)

Con ello conseguiremos tener decompilados todos los recursos de al app.

