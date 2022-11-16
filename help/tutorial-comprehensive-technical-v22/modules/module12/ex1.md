---
title: 'Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector de origen BigQuery: Cree su cuenta de Google Cloud Platform'
description: 'Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector de origen BigQuery: Cree su cuenta de Google Cloud Platform'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 632ff2fe-ae56-4481-b281-c11224b18639
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 2%

---

# 12.1 Cree su cuenta de Google Cloud Platform

## Objetivos

- Cree su cuenta de Google Cloud Platform
- Familiarícese con Google Cloud Platform Console
- Cree y prepare su proyecto BigQuery

## 12.1.1 ¿Por qué conectar Google BigQuery a Adobe Experience Platform para obtener los datos de los Google Analytics?

Google Cloud Platform (GCP) es un conjunto de servicios públicos de computación en la nube que ofrece Google. Google Cloud Platform incluye una serie de servicios alojados para el desarrollo de aplicaciones, almacenamiento y computación que se ejecutan en el hardware de Google.

BigQuery es uno de estos servicios y siempre se incluye con Google Analytics 360. Los datos de Google Analytics se muestrean con frecuencia cuando intentamos obtener datos directamente desde él (API, por ejemplo). Por eso Google incluye BigQuery para obtener datos sin muestrear, de modo que las marcas puedan realizar análisis avanzados utilizando SQL y beneficiarse del poder de GCP.

Los datos de Google Analytics se cargan diariamente en BigQuery mediante un mecanismo por lotes. Como tal, no tiene sentido utilizar esta integración GCP/BigQuery para casos de uso de activación y personalización en tiempo real.

Si una marca desea ofrecer casos de uso de personalización en tiempo real basados en datos de Google Analytics, puede recopilar esos datos en el sitio web con Google Tag Manager y luego transmitirlos a Adobe Experience Platform en tiempo real.

El conector de origen GCP/BigQuery debe usarse para...

- realice un seguimiento de todo el comportamiento de los clientes en el sitio web y cargue esos datos en Adobe Experience Platform para su análisis, ciencia de datos y casos de uso de personalización que no requieran activación en tiempo real.
- cargar datos históricos de Google Analytics en Adobe Experience Platform, de nuevo para casos de uso de análisis y ciencia de datos

## 12.1.2 Crear su cuenta de Google

Para obtener una cuenta de Google Cloud Platform, necesita una cuenta de Google.

## 12.1.3 Activar su cuenta de Google Cloud Platform

Ahora que tiene su cuenta de Google, puede crear un entorno de Google Cloud Platform. Para ello, vaya a [https://console.cloud.google.com/](https://console.cloud.google.com/).

En la página siguiente, acepte los Términos y condiciones.

![demostración](./images/ex1/1.png)

A continuación, haga clic en **Seleccionar un proyecto**.

![demostración](./images/ex1/2.png)

Haga clic en **NUEVO PROYECTO**.

![demostración](./images/ex1/createproject.png)

Asigne un nombre al proyecto siguiendo esta convención de nomenclatura:

| Convención | Ejemplo |
| ----------------- |-------------| 
| `--demoProfileLdap---googlecloud` | delaigle-googlecloud |

![demostración](./images/ex1/3.png)

Haga clic en **Crear**.

![demostración](./images/ex1/3-1.png)

Espere hasta que la notificación en la parte superior derecha de la pantalla le indique que la creación ha finalizado. A continuación, haga clic en **Ver proyecto**.

![demostración](./images/ex1/4.png)

A continuación, vaya a la barra de búsqueda en la parte superior de la pantalla y escriba **BigQuery**. Seleccione el primer resultado.

![demostración](./images/ex1/7.png)

A continuación, se le redirigirá a la consola BigQuery y verá un mensaje emergente.

**Haga clic en Finalizado**.

![demostración](./images/ex1/5.png)

El objetivo de este módulo es obtener los datos de los Google Analytics en Adobe Experience Platform. Para ello, necesitamos datos ficticios en un conjunto de datos de Google Analytics para empezar.

Haga clic en **Agregar datos** en el menú de la izquierda, seguido de hacer clic en **Explorar conjuntos de datos públicos**.

![demostración](./images/ex1/18.png)

A continuación, verá esta ventana:

![demostración](./images/ex1/19.png)

Escriba el término de búsqueda **Ejemplo de Google Analytics** en la barra de búsqueda y seleccione el primer resultado.

![demostración](./images/ex1/20.png)

Verá la siguiente pantalla con una descripción del conjunto de datos. Haga clic en **VER CONJUNTO DE DATOS**.

![demostración](./images/ex1/21.png)

A continuación, se le redirigirá a BigQuery, donde verá esto **bigquery-public-data** conjunto de datos en **Explorer**.

![demostración](./images/ex1/22a.png)

En **Explorer**, debería ver una serie de tablas. Siéntase libre de explorarlas. Vaya a `google_analytics_sample`.

![demostración](./images/ex1/22.png)

Haga clic en para abrir la tabla `ga_sessions`.

![demostración](./images/ex1/23.png)

Antes de continuar con el siguiente ejercicio, anote las siguientes cosas en un archivo de texto independiente en su equipo:

| Credencial | Nombre | Ejemplo |
| ----------------- |-------------| -------------|
| Proyecto Nombre | `--demoProfileLdap---googlecloud` | vangeluw-googlecloud |
| ID del proyecto | random | compuesta-task-306413 |

Puede encontrar el nombre del proyecto y el ID del proyecto haciendo clic en su **Nombre del proyecto** en la barra de menús superior:

![demostración](./images/ex1/projectMenu.png)

A continuación, verá su ID de proyecto en el lado derecho:

![demostración](./images/ex1/projetcselection.png)

Ahora puede pasar al Ejercicio 12.2, donde se ensuciarán las manos consultando los datos de los Google Analytics.

Paso siguiente: [12.2 Crear la primera consulta en BigQuery](./ex2.md)

[Volver al módulo 12](./customer-journey-analytics-bigquery-gcp.md)

[Volver a todos los módulos](./../../overview.md)
