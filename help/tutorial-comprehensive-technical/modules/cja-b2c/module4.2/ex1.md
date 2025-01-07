---
title: 'Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector Source de BigQuery: cree su cuenta de Google Cloud Platform'
description: 'Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector Source de BigQuery: cree su cuenta de Google Cloud Platform'
kt: 5342
doc-type: tutorial
exl-id: 6dbfb5a3-adc2-4818-8f79-bbb00e56fbdf
source-git-commit: d6f6423adbc8f0ce8e20e686ea9ffd9e80ebb147
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# 4.2.1 Empezar a utilizar Google Cloud Platform

>[!NOTE]
>
>Para este ejercicio, necesita acceder a un entorno de Google Cloud Platform. Si todavía no tiene acceso a GCP, cree una nueva cuenta con su dirección de correo electrónico personal.

## 4.2.1.1 Por qué conectar Google BigQuery a Adobe Experience Platform para obtener datos de Google Analytics

Google Cloud Platform (GCP) es un conjunto de servicios públicos de computación en la nube que ofrece Google. Google Cloud Platform incluye una serie de servicios alojados para el desarrollo de aplicaciones, almacenamiento y computación que se ejecutan en hardware de Google.

BigQuery es uno de estos servicios y siempre se incluye con Google Analytics 360. Los datos de los Google Analytics se muestrean con frecuencia cuando intentamos obtener datos directamente de ellos (API, por ejemplo). Es por eso que Google incluye BigQuery para obtener datos no muestreados, de modo que las marcas puedan hacer análisis avanzados usando SQL y beneficiarse de la potencia de GCP.

Los datos de Google Analytics se cargan a diario en BigQuery mediante un mecanismo por lotes. Como tal, no tiene ningún sentido utilizar esta integración de GCP/BigQuery para casos de uso de personalización y activación en tiempo real.

Si una marca desea ofrecer casos de uso de personalización en tiempo real basados en datos de Google Analytics, puede recopilar esos datos en el sitio web con Google Tag Manager y luego transmitirlos a Adobe Experience Platform en tiempo real.

El conector Source GCP/BigQuery debe usarse para...

- realice un seguimiento del comportamiento de todos los clientes en el sitio web y cargue esos datos en Adobe Experience Platform para análisis, ciencia de datos y casos de uso de personalización que no requieran activación en tiempo real.
- cargar datos históricos de los Google Analytics en Adobe Experience Platform, para casos de uso de análisis y ciencia de datos.

## 4.2.1.2 Su cuenta de Google

>[!NOTE]
>
>Para este ejercicio, necesita acceder a un entorno de Google Cloud Platform. Si todavía no tiene acceso a GCP, cree una nueva cuenta con su dirección de correo electrónico personal.

## 4.2.1.3 Seleccionar o crear un proyecto

Vaya a [https://console.cloud.google.com/](https://console.cloud.google.com/).

A continuación, haz clic en **Seleccionar un proyecto** o haz clic en un proyecto existente.

![demostración](./images/ex12.png)

Si todavía no tiene un proyecto, haga clic en **NUEVO PROYECTO**. Si ya tiene un proyecto, puede elegir seleccionarlo y continuar con el paso siguiente.

![demostración](./images/ex1createproject.png)

Asigne un nombre al proyecto según esta convención de nombres. Haga clic en **CREAR**.

| Convención |
| ----------------- |
| `--aepUserLdap---googlecloud` |

![demostración](./images/ex13.png)

Espere hasta que la notificación en la parte superior derecha de la pantalla le indique que la creación ha finalizado. A continuación, haga clic en **SELECCIONAR PROYECTO**.

![demostración](./images/ex14.png)

A continuación, vaya a la barra de búsqueda en la parte superior de la pantalla y escriba **BigQuery**. Seleccione el primer resultado.

![demostración](./images/ex17.png)

El objetivo de este módulo es obtener los datos de los Google Analytics en Adobe Experience Platform. Para ello, necesita datos ficticios en un conjunto de datos de Google Analytics para empezar.

Haga clic en **+ Agregar** y, a continuación, haga clic en **Conjuntos de datos públicos** en el menú derecho.

![demostración](./images/ex118.png)

A continuación, verá esta ventana:

![demostración](./images/ex119.png)

Escriba el término de búsqueda **Ejemplo de Google Analytics** en la barra de búsqueda y haga clic en el primer resultado de la búsqueda.

![demostración](./images/ex120.png)

Verá la siguiente pantalla con una descripción del conjunto de datos. Haga clic en **VER CONJUNTO DE DATOS**.

![demostración](./images/ex121.png)

Luego se le redirigirá a BigQuery, donde verá este conjunto de datos de **bigquery-public-data** en **Explorer**.

![demostración](./images/ex122a.png)

En **Explorer**, debería ver varias tablas. No dude en explorarlos. Vaya a `google_analytics_sample`.

![demostración](./images/ex122.png)

Haga clic para abrir la tabla `ga_sessions`.

![demostración](./images/ex123.png)

Antes de continuar con el siguiente ejercicio, anote los siguientes elementos en un archivo de texto independiente en el equipo:

| Credencial | Nombre | Ejemplo |
| ----------------- |-------------| -------------|
| Nombre de proyecto | `--aepUserLdap---googlecloud` | vangeluw-googlecloud |
| Identificador de proyecto | random | possible-bee-447102-h3 |

Encontrará su nombre de proyecto e ID de proyecto haciendo clic en su **Nombre de proyecto** en la barra de menús superior:

![demostración](./images/ex1projectMenu.png)

A continuación, verá su ID de proyecto a la derecha:

![demostración](./images/ex1projetcselection.png)

Ahora puede pasar al siguiente ejercicio donde se ensuciará las manos consultando los datos de los Google Analytics.

Paso siguiente: [4.2.2 Cree su primera consulta en BigQuery](./ex2.md)

[Volver al módulo 4.2](./customer-journey-analytics-bigquery-gcp.md)

[Volver a todos los módulos](./../../../overview.md)
