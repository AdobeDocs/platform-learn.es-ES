---
title: Información general
description: Punto de partida para ingenieros de datos, analistas de datos, arquitectos de datos, científicos de datos, ingenieros de orquestaciones y especialistas en marketing para comprender plenamente el valor comercial de Adobe Experience Platform y todos sus servicios de aplicaciones.
doc-type: multipage-overview
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 2%

---

# Tutorial técnico completo de Adobe Experience Platform

![Perspectivas técnicas](./assets/images/techinsiders.png){width="50px" align="left"}

## Información general

Este tutorial es el punto de partida perfecto para que los ingenieros de datos, analistas de datos, arquitectos de datos, científicos de datos, ingenieros de orquestaciones y especialistas en marketing comprendan plenamente el valor comercial de Adobe Experience Platform y todos sus servicios de aplicaciones. Cada lección se centra en un desafío real que las empresas afrontan en el complejo ecosistema de personalización de hoy en día y desglosa cómo resuelve Experience Platform ese desafío en varios ejercicios prácticos.

Este tutorial es muy diverso y ofrece perspectivas claras en las siguientes aplicaciones:

- Adobe Experience Platform
- Recopilación de datos de Adobe Experience Platform
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics

Este tutorial no solo se centra en las aplicaciones de Adobe, sino que tiene en cuenta el ecosistema más amplio en el que operan las marcas. Para hacerlo, en algunas lecciones hay un enfoque en cómo se integran las aplicaciones de _que no son de Adobe_ con Adobe Experience Platform. De este modo, obtendrá información detallada sobre cómo las siguientes aplicaciones funcionan junto con Adobe Experience Platform:

- Amazon: AWS Lambda, AWS S3, AWS Kinesis
- Google: Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft: Power BI, Azure EventHub, Azure Blob Storage
- Salesforce: Tableau
- Apache Kafka
- Postman
- ...

Después de completar los ejercicios de este tutorial, podrá hacer lo siguiente:

- Configuración de esquemas, grupos de campos, conjuntos de datos e identidades
- Configure una propiedad de recopilación de datos de Adobe Experience Platform y la nueva extensión de SDK web en Recopilación de datos de Adobe Experience Platform
- Transmitir datos a Adobe Experience Platform en tiempo real mediante la recopilación de datos de Adobe Experience Platform
- Ingesta por lotes de datos en Adobe Experience Platform mediante un flujo de trabajo o mediante una aplicación de extracción, transformación y carga (ETL)
- Visualice y utilice el perfil del cliente en tiempo real en Adobe Experience Platform
- Creación de públicos
- Consumir varias API de Adobe Experience Platform
- Utilice SQL para consultar los datos en Adobe Experience Platform
- Configuración y ejecución de recorridos en tiempo real basados en déclencheur
- Utilice CDP en tiempo real para tomar medidas al activar una audiencia en varios destinos
- Utilice Customer Journey Analytics para informar sobre datos de clientes omnicanal de varias fuentes, como Google BigQuery

## Requisitos previos

Si desea realizar este tutorial con su propia instancia de Adobe Experience Platform, siga las instrucciones [aquí](./setup.md) para preparar su organización para el tutorial.

- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acceso a la recopilación de datos de Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acceso al sistema de demostración: [https://dsn.adobe.com/](https://dsn.adobe.com/)

## Vídeos

Puedes encontrar muchos videos interesantes de nuestros seminarios web de Tech Academy, de bootcamp y más en nuestro [canal de YouTube de la Comunidad de Experience Makers](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

## Finalización y certificación

Este tutorial forma parte de un curso de certificación de Adobe. Puede inscribirse en el curso junto con este tutorial yendo a [https://certification.adobe.com](https://certification.adobe.com).

Para cada módulo que complete usando el tutorial siguiente, debe enviar una prueba de finalización como se indica [aquí](./completion.md).

## Contenido

Para comprobar el estado del contenido siguiente, vaya a la [página de estado](./status.md).

[0. Introducción](./modules/gettingstarted/gettingstarted/getting-started.md)

En este módulo básico, configurará todo para que pueda acceder y utilizar el entorno de demostración.

**Inversión de tiempo:** 30 minutos

### 1. Recopilación de datos

[1.1 Foundation: configuración de la recopilación de datos de Adobe Experience Platform y Web SDK](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

En este módulo básico, aprenderá sobre la recopilación de datos de Adobe Experience Platform y la nueva extensión de Web SDK.

**Inversión de tiempo:** 30 minutos

[Base 1.2: ingesta de datos](./modules/datacollection/module1.2/data-ingestion.md)

En este módulo básico, ingerirá datos de varias fuentes en Adobe Experience Platform

**Inversión de tiempo:** 120 minutos

[1.3 Composición de audiencia federada](./modules/datacollection/module1.3/fac.md)

En este módulo, aprenderá a configurar un modelo de audiencias federadas y a generar audiencias mediante datos federados.

**Inversión de tiempo:** 90 minutos

### 2. Real-Time CDP B2C

[Base 2.1: perfil del cliente en tiempo real](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

En este módulo básico, explorará el perfil del cliente en tiempo real en Adobe Experience Platform mediante la interfaz de usuario y la API.

**Inversión de tiempo:** 90 minutos

[2.2 Servicios inteligentes](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

En este módulo, aprenderá a configurar y utilizar Adobe Experience Platform Intelligent Services.

**Inversión de tiempo:** 60 minutos

[2.3 Real-Time CDP: crear una audiencia y actuar en consecuencia](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

En este módulo, configurará una audiencia y la activará en varios destinos, incluidos Google DV360, Adobe Target y AWS S3.

**Inversión de tiempo:** 90 minutos

[2.4 Real-Time CDP: Audience Activation de Microsoft Azure Event Hub](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

En este módulo, configurará un destino de Microsoft Azure EventHub como un destino en tiempo real para Adobe Experience Platform Real-time CDP. También configurará e implementará una función de Azure que se activará en tiempo real cada vez que Adobe Experience Platform envíe una carga útil de audiencia a su destino de Azure EventHub. La función de Azure que almacenará en déclencheur mostrará el mecanismo de las capacidades de activación de Adobe Experience Platform Real-time CDP.
Como parte de este módulo, también comprenderá qué déclencheur necesita CDP en tiempo real para entregar una carga útil a un destino especificado. También analizaremos el estado de una calificación de audiencia y cómo se relaciona con la activación.

**Inversión de tiempo:** 90 minutos

[Conexiones Real-Time CDP 2.5: Reenvío de eventos](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

En este módulo, se utilizarán los conjuntos de datos, esquemas y la propiedad de recopilación de datos de Adobe Experience Platform configurados anteriormente para recopilar datos y, a continuación, reenviar esos datos del lado del servidor a varios extremos, como Google Cloud Platform Pub/Sub y AWS Kinesis.

**Inversión de tiempo:** 90 minutos

[2.6 Transmitir datos de Apache Kafka a Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

En este módulo, aprenderá a configurar su propio clúster de Apache Kafka, definir temas, productores y consumidores y transmitir datos a Adobe Experience Platform mediante el Conector del receptor de Adobe Experience Platform para Kafka Connect.

**Inversión de tiempo:** 90 minutos

### 3. Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer: Orchestration](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

En este módulo utilizará Adobe Journey Optimizer para crear un recorrido basado en déclencheur.

**Inversión de tiempo:** 60 minutos

[3.2 Adobe Journey Optimizer: Fuentes de datos externas y acciones personalizadas](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

En este módulo, utilizará Adobe Journey Optimizer para escuchar el comportamiento de los clientes, tanto en línea como sin conexión, y responder a él de forma inteligente, contextual y en tiempo real a través de varios canales.

**Inversión de tiempo:** 90 minutos

[3.3 Adobe Journey Optimizer: Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

En este módulo, utilizará el servicio de aplicaciones Adobe Experience Platform - Ofertas/Decisiones de forma práctica para configurar Ofertas personalizadas y su propia actividad de oferta.

**Inversión de tiempo:** 120 minutos

[3.4 Adobe Journey Optimizer: Recorridos basados en eventos](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

En este módulo, aprenderá todo lo que debe saber sobre Journey Optimizer, que ayuda a las empresas a diseñar y ofrecer experiencias conectadas, contextuales y personalizadas a sus clientes.

**Inversión de tiempo:** 120 minutos

### 4. Adobe Customer Journey Analytics

[Customer Journey Analytics 4.1: cree un tablero con Analysis Workspace sobre Adobe Experience Platform](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

En este módulo, obtendrá perspectivas en línea y sin conexión configurando un panel que contiene datos omnicanal como interacciones de sitios web, interacciones de aplicaciones móviles, interacciones de centros de llamadas, interacciones en tienda y mucho más.

**Inversión de tiempo:** 120 minutos

[Customer Journey Analytics de 4.2: Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector de Source de BigQuery](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

En este módulo, configurará su propia instancia de Google Cloud Platform, cargará datos de demostración en Google Cloud Platform y, a continuación, utilizará el conector de Source de BigQuery para introducir esos datos de Google Cloud Platform en Adobe Experience Platform. Por último, utilizará Customer Journey Analytics para visualizar esos datos.

**Inversión de tiempo:** 120 minutos

### 5. Data Distiller

[5.1 Servicio de consultas](./modules/datadistiller/module5.1/query-service.md)

En este módulo, aprenderá a utilizar el servicio de consultas de Adobe Experience Platform.

**Inversión de tiempo:** 90 minutos

![Perspectivas técnicas](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, póngase en contacto directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.
