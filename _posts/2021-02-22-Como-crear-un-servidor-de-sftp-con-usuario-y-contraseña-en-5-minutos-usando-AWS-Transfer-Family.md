---
layout: post
title: ¿Cómo crear un servidor de SFTP con usuario y contraseña en 5 minutos usando AWS Transfer Family?
summary: Cómo crear un servidor de SFTP con usuario y contraseña en 5 minutos usando AWS Transfer Family
author: lcbarco
image: /images/aws-transfer-family.png
tags: aws transfer family, aws, sftp
---

¿Quién no ha necesitado en algún momento montar un servidor de **SFTP**? Crear el servidor, preparar el espacio de disco duro, pegarse con los usuarios, pruebas y realizar un respaldo de la información almacenada...

En un proyecto en el que estoy trabajando nos ha surgido la necesidad de crear un servidor **SFTP** efímero que sólo va a ser usado una vez. Se podrían haber planteado el hacer uso de algún sistema de transferencia de ficheros que no fuera **SFTP**, pero por la facilidad de integración como por la estandarización del protocolo **SFTP**, descartamos el resto de opciones.

Debíamos plantearnos realizar el periplo de realizar la creación del servidor de forma tradicional o buscar una opción más álgil, sobretodo teniendo en cuenta el tiempo que iba a estar activo. 

Como gran parte de nuestros servicios se encuentran bajo el paráguas de **Amazon AWS**, nos decidimos por usar **AWS Transfer Family**.

![AWS Transfer Family](/images/aws-transfer-family.png)
<!--more-->

## ¿Cómo funciona AWS Transfer Family
AWS Transfer Family es un servicio de AWS que permite levantar un servidor de **SFTP** y conectarlo con un bucket de S3 en un par de minutos.

El cobro del servicio se realiza tanto por el tiempo que esté levantado el servicio como los datos transferidos, unos 30 centimos de dolar por hora levantado y 4 centimos de dolar por Giga transferido.

Teniendo en cuenta el coste del servicio, el tiempo que iba a estar activo y que directamente vuelca la información a S3 estaba clara la elección.

**AWS Transfer Family** te permite hacer la típica configuración de siguiente, siguiente, siguiente y finalizar.

Aquí es donde venía nuestro problema, este tipo de configuración sólo te termite crear usuarios con autentificación con clave pública/privada.

## Cómo realizar la autentificación a través de usuario/contraseña
**AWS Transfer Family** te permite tener tu propio servicio de autentificación para el servidor de **SFTP**. 

Tranquilo, AWS proporciona una plantilla de Cloud Formation que se encarga de casi todo. Crear el Stack con Lambda, AWS API Gateway y el servidor de SFTP. Se puede descargar de [aquí](https://s3.amazonaws.com/aws-transfer-resources/custom-idp-templates/aws-transfer-custom-idp-secrets-manager-apig.template.yml).

En está página te explican en el [Step1 cómo crear el stack](https://cloudsbaba.com/enabling-password-authentication-for-aws-sftp-transfer-family-service-using-aws-secrets-manager/). El Step2 se hace automáticamente.

Para el Step3 recomiendo que sigas los pasos que indico a continuación.

## Configuración de roles
Una vez que tenemos creado el servicio de **SFTP**, vamos a configurar los usuarios que va a acceder a nuestro servidor.

Lo primero que haremos, una vez tenemos el bucket corresponiente, será crear las *Policy* y los *Roles* correspondientes en **AWS IAM**.

Vamos a crear la siguiente *Policy* para dar acceso a nuestro bucket:
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:GetBucketLocation"
            ],
            "Resource": "arn:aws:s3:::nombre_del_bucket"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObjectAcl",
                "s3:GetObject",
                "s3:DeleteObjectVersion",
                "s3:DeleteObject",
                "s3:PutObjectAcl",
                "s3:GetObjectVersion"
            ],
            "Resource": "arn:aws:s3:::nombre_del_bucket/*"
        }
    ]
}
```

Una vez creada la *Policy* se la asignamos a un nuevo *Rol* que llamaremos **Role-for-accesing-S3**.

La parte más importante, y que no se explica correctamente, es que en la pestaña **Trust relationship** del Rol debemos modificar la **Trusted Entity** del *Rol* y dar permisos a "transfer.amazonaws.com". Este cambio es el que hacía que el resto dejara de funcionar.

## Creación de usuarios
Como último paso, vamos a crear en el servicio **Secret Manager** los diferentes usuarios que van a acceder a nuestro servidor.

Haremos click *Store a new secret*. Acontinuación elegiremos la opción "**Other type of secret**" y añadiremos la información del usuario como plaintext:

![Other type of secret](/images/aws-secret-manager-1.png)

En el siguiente paso en el campo **Secret name** podremos el nombre de usuario bajo el formato **SFTP/nombre_de_usuario**:

![Secret name](/images/aws-secret-manager-2.png)


Seguimos los siguientes pasos y almacenamos la clave.

## URL de conexión
Ya tenemos el servicio, los permisos, los usuarios y sus contraseñas. Sólo nos falta saber dónde conectarnos. 

Para ello volvemos acceder al servicio **AWS Transfer Family** y una vez elegido nuestro servidor, buscamos el campo Endpoint. 

![Endpoint](/images/aws-transfer-family-end-point.png)

Ese campo contendrá la URL a la que nos tenemos que conectar usando nuestro cliente de **SFTP** favorito.

## Conclusiones
Hay veces que queremos crear nuestros propios servicios desde cero. Siempre recomiendo el hacer uso de servicios existentes ya que muchas veces no valoramos el coste económico de la persona que tiene que implementar dicho servicio y sólo nos fijamos en el coste del servicio en si. Prueba a configurar tu servidor de **SFTP** y contáctame si tienes algún problema enviándome un email a [lcbarco@gmail.com](mailto:lcbarco@gmail.com) o a través de mi cuenta de Twitter [https://twitter.com/lcbarco](https://twitter.com/lcbarco).






