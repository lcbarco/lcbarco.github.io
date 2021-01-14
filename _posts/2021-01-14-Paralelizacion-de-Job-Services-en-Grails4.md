---
layout: post
title: Paralelizacion de Job Services en Grails   4
summary: Cómo poder ejecutar varios Job Services en Grails4 de forma concurrente
author: lcbarco
image: /images/twitter-cards.png
tags: jekyll
---

Hace tiempo comencé un proyecto en [Grails 4](https://grails.org/). En un momento del proyecto se hizo necesario ejecutar Jobs programados a ciertas horas. Para ello **Grails 4** tienen implementados los Job Services. Usando la guía [Grails + @Scheduled](https://guides.grails.org/grails-scheduled/guide/index.html) realizamos la primera versión.

![Log de Grails](https://grails.org/images/grails_logo.svg)

No tardé en darme cuenta que si varios Jobs se tenían que ejecutar a la vez, no se ejecutaban de forma concurrente sino secuencial.


<!--more-->

## Todos es culpa de los Threads
El motivo de este comportamientos es que los Job Services usan un **ThreadPoolTaskScheduler** que por defecto se instancia con un solo **Thread**.

Si se revisa la [documentación](https://guides.grails.org/grails-scheduled/guide/index.html) podemos leer el siguiente párrafo en el que se indica esta circunstancia:

```
By default ThreadPoolTaskScheduler only has a single thread available for execution, which means tasks will not execute concurrently
```

## Configurar nuestro propio ThreadPoolTaskScheduler
La solución es configurar nuestro propio **ThreadPoolTaskScheduler** con más Threads.

Para ello creamos el archivo *src/main/groovy/jobs/SchedulingConfiguration.groovy* con el siguiente código:
```groovy
package com.mycompany.jobs

import groovy.transform.CompileStatic
import org.springframework.context.annotation.Bean
import org.springframework.context.annotation.Configuration
import org.springframework.scheduling.concurrent.ThreadPoolTaskScheduler

@CompileStatic
@Configuration
class SchedulingConfiguration {

    @Bean
    ThreadPoolTaskScheduler threadPoolTaskScheduler() {
        ThreadPoolTaskScheduler threadPoolTaskScheduler = new ThreadPoolTaskScheduler()
        threadPoolTaskScheduler.setThreadNamePrefix("ThreadPoolTaskScheduler")
        threadPoolTaskScheduler.setPoolSize(5)
        threadPoolTaskScheduler.initialize()
        threadPoolTaskScheduler
    }
}

```

Donde *setPoolSize(5)* es el número de Threads que queremos usar.

## Conclusiones
Una vez más se cumple la expresión RTFM (Read The Fucking Manual). Prueba a configurar tu ThreadPoolTaskScheduler y contáctame si tienes algún problema enviándome un email a [lcbarco@gmail.com](mailto:lcbarco@gmail.com) o a través de mi cuenta de Twitter [https://twitter.com/lcbarco](https://twitter.com/lcbarco).






