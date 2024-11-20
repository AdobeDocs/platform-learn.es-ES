---
title: Información general
description: Punto de partida para ingenieros de datos, analistas de datos, arquitectos de datos, científicos de datos, ingenieros de orquestaciones y especialistas en marketing para comprender plenamente el valor comercial de Adobe Experience Platform y todos sus servicios de aplicaciones.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: b46c753a8d854b5a448d10d30c7a5701900a35b8
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 2%

---

# Tutorial técnico completo de Adobe Experience Platform

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
- Configure una propiedad de recopilación de datos de Adobe Experience Platform y la nueva extensión del SDK web en la recopilación de datos de Adobe Experience Platform
- Transmitir datos a Adobe Experience Platform en tiempo real mediante la recopilación de datos de Adobe Experience Platform
- Ingesta por lotes de datos en Adobe Experience Platform mediante un flujo de trabajo o mediante una aplicación de extracción, transformación y carga (ETL)
- Visualice y utilice el perfil del cliente en tiempo real en Adobe Experience Platform
- Creación de segmentos
- Consumir varias API de Adobe Experience Platform
- Utilice SQL para consultar los datos en Adobe Experience Platform
- Configuración y ejecución de recorridos en tiempo real basados en déclencheur
- Utilice CDP en tiempo real para tomar medidas al activar un segmento en varios destinos
- Utilice Customer Journey Analytics para informar sobre datos de clientes omnicanal de varias fuentes, como Google BigQuery

## Requisitos previos

- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acceso a la recopilación de datos de Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acceso al sistema de demostración: [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

## Vídeos

Puedes encontrar muchos videos interesantes de nuestros eventos de Tech Academy, de Bootcamp y más en nuestro [canal de YouTube de la Comunidad de Experience Makers](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

## Contenido

[0. Introducción](./modules/gettingstarted/gettingstarted/getting-started.md)

- **Audiencia:** Todos los participantes en el Tutorial técnico completo de Adobe Experience Platform
- **Requisitos previos:** Acceso a Demo System Next, Recopilación de datos de Adobe Experience Platform y Adobe Experience Platform.
- **Descripción:** En este módulo fundacional, configurará todo para que pueda acceder y utilizar el entorno de demostración.
- **Inversión de tiempo:** 30 minutos

### 1. Recopilación de datos

[1.1 Foundation: configuración de la recopilación de datos de Adobe Experience Platform y SDK web](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos
- **Requisitos previos:** Acceso a la recopilación de datos de Adobe Experience Platform y Adobe Experience Platform.
- **Descripción:** En este módulo básico, aprenderá acerca de la recopilación de datos de Adobe Experience Platform y la nueva extensión del SDK web.
- **Inversión de tiempo:** 30 minutos

[Base 1.2: ingesta de datos](./modules/datacollection/module1.2/data-ingestion.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos
- **Requisitos previos:** Acceso a la recopilación de datos de Adobe Experience Platform y Adobe Experience Platform.
- **Descripción:** En este módulo básico, ingerirá datos del sitio web en Platform
- **Inversión de tiempo:** 120 minutos

[1.3 Composición de audiencia federada](./modules/datacollection/module1.3/fac.md)

- **Audiencia:** Analista de datos, Ingeniero de datos, Arquitecto de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform
- **Descripción:** En este módulo, aprenderá a configurar su propio clúster de Apache Kafka, definir temas, productores y consumidores y transmitir datos a Adobe Experience Platform mediante el Conector del receptor de Adobe Experience Platform para Kafka Connect.
- **Inversión de tiempo:** 90 minutos

### 2. Real-Time CDP B2C

[Base 2.1: perfil del cliente en tiempo real](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, experto en marketing
- **Requisitos previos:** Acceso a Adobe Experience Platform y Postman
- **Descripción:** En este módulo básico, explorará el perfil del cliente en tiempo real en Adobe Experience Platform mediante la interfaz de usuario y la API.
- **Inversión de tiempo:** 90 minutos
- **Descargar estos recursos**:
   - [Colecciones de Postman](./assets/postman/postman_profile.zip)

[2.2 Servicios inteligentes](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, científico de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform, Servicios inteligentes
- **Descripción:** En este módulo, aprenderá a configurar y utilizar Adobe Experience Platform Intelligent Services.
- **Inversión de tiempo:** 60 minutos

[2.3 Real-Time CDP: Crear un segmento y actuar en consecuencia](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

- **Audiencia:** arquitecto de datos, ingeniero de orquestaciones, experto en marketing
- **Requisitos previos:** Acceso a Adobe Experience Platform, Real-time CDP, Adobe Audience Manager, Adobe Target, AWS S3
- **Descripción:** En este módulo, configurará un segmento, lo habilitará para la segmentación de streaming y activará el segmento en varios destinos, entre ellos Google DV360, Google AdWords, Adobe Audience Manager, Adobe Target y destinos S3 como Salesforce Marketing Cloud.
- **Inversión de tiempo:** 90 minutos

[2.4 Real-Time CDP: Activación de segmentos en Microsoft Azure Event Hub](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, analista de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform, Real-time CDP y Microsoft Azure
- **Descripción:** En este módulo, configurará un destino de Microsoft Azure EventHub como destino en tiempo real de CDP en tiempo real de Adobe Experience Platform. También configurará e implementará una función de Azure que se activará en tiempo real cada vez que Adobe Experience Platform envíe una carga útil de segmento a su destino de Azure EventHub. La función de Azure que almacenará en déclencheur mostrará el mecanismo de las capacidades de activación de Adobe Experience Platform Real-time CDP.
Como parte de este módulo, también comprenderá qué déclencheur necesita CDP en tiempo real para entregar una carga útil a un destino especificado. También analizaremos el estado de la calificación de un segmento y cómo se relaciona con la activación.
- **Inversión de tiempo:** 90 minutos

[Conexiones Real-Time CDP 2.5: Reenvío de eventos](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, analista de datos
- **Requisitos previos:** Acceso a las propiedades de conexiones de Real-Time CDP, Etiquetas y Reenvío de eventos
- **Descripción:** En este módulo, usará los conjuntos de datos, esquemas y la propiedad de recopilación de datos de Adobe Experience Platform que configuró anteriormente para recopilar datos y, a continuación, reenviar esos datos del lado del servidor a un extremo de su elección.
- **Inversión de tiempo:** 90 minutos

[2.6 Transmitir datos de Apache Kafka a Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

- **Audiencia:** Analista de datos, Ingeniero de datos, Arquitecto de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform
- **Descripción:** En este módulo, aprenderá a configurar su propio clúster de Apache Kafka, definir temas, productores y consumidores y transmitir datos a Adobe Experience Platform mediante el Conector del receptor de Adobe Experience Platform para Kafka Connect.
- **Inversión de tiempo:** 90 minutos

### 3. Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer: Orchestration](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, ingeniero de orquestaciones
- **Requisitos previos:** Acceso a Adobe Experience Platform y Adobe Journey Optimizer
- **Descripción:** En este módulo, usará Adobe Journey Optimizer para crear un recorrido basado en déclencheur.
- **Inversión de tiempo:** 60 minutos

[3.2 Adobe Journey Optimizer: Fuentes de datos externas y acciones personalizadas](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, ingeniero de orquestaciones, experto en marketing
- **Requisitos previos:** Acceso a Adobe Experience Platform, Adobe Journey Optimizer, API de clima abierto, Twilio
- **Descripción:** En este módulo, usará Adobe Journey Optimizer para escuchar el comportamiento de los clientes, tanto en línea como sin conexión, y responderá a él de forma inteligente, contextual y en tiempo real a través de varios canales.
- **Inversión de tiempo:** 90 minutos

[3.3 Adobe Journey Optimizer: Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, ingeniero de orquestaciones, experto en marketing
- **Requisitos previos:** Acceso a Adobe Experience Platform y Offer decisioning
- **Descripción:** En este módulo, usará el servicio de aplicaciones Adobe Experience Platform - Ofertas/Decisiones de forma práctica para configurar Ofertas personalizadas y su propia Actividad de ofertas.
- **Inversión de tiempo:** 120 minutos

[3.4 Adobe Journey Optimizer: Recorridos basados en eventos](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

- **Audiencia:** Especialista en marketing por correo electrónico, Especialista en orquestaciones, Ingeniero de datos, Arquitecto de datos, Analista de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform y Journey Optimizer
- **Descripción:** En este módulo, aprenderá todo lo que tiene que saber sobre Journey Optimizer, que ayuda a las compañías a diseñar y ofrecer experiencias conectadas, contextuales y personalizadas a sus clientes.
- **Inversión de tiempo:** 120 minutos

### 4. Adobe Customer Journey Analytics

[Customer Journey Analytics 4.1: cree un tablero con Analysis Workspace sobre Adobe Experience Platform](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, analista de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform y Customer Journey Analytics
- **Descripción:** En este módulo, obtendrá información en línea y sin conexión mediante la configuración de un tablero que contiene datos omnicanal, como interacciones de sitios web, interacciones de aplicaciones móviles, interacciones de centros de llamadas, interacciones en tiendas y mucho más.
- **Inversión de tiempo:** 120 minutos

[Customer Journey Analytics de 4.2: Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector de Source de BigQuery](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, analista de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery
- **Descripción:** En este módulo, configurará su propia instancia de Google Cloud Platform, cargará datos de demostración en Google Cloud Platform y, a continuación, utilizará el conector de Source de BigQuery para ingerir esos datos de Google Cloud Platform en Adobe Experience Platform. Por último, utilizará Customer Journey Analytics para visualizar esos datos.
- **Inversión de tiempo:** 120 minutos
- **Descargar estos recursos**:
   - [JSON: datos de muestra: demostración: datos de fidelización](./assets/json/bqLoyalty.json)

### 5. Data Distiller

[5.1 Servicio de consultas](./modules/datadistiller/module5.1/query-service.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, analista de datos, experto en BI
- **Requisitos previos:** Acceso a Adobe Experience Platform, Query Service, Power BI o Tableau
- **Descripción:** En este módulo, aprenderá a utilizar el servicio de consultas de Adobe Experience Platform.
- **Inversión de tiempo:** 90 minutos
- **Descargar estos recursos**:
   - [JSON: datos de muestra: sistema de demostración: conjunto de datos de evento para el sitio web](./assets/json/ee.json)
   - [JSON: datos de muestra: sistema de demostración: conjunto de datos de evento para el centro de llamadas](./assets/json/callcenter.json)
   - [JSON: datos de muestra: sistema de demostración: conjunto de datos de perfil para fidelización](./assets/json/loyalty.json)





