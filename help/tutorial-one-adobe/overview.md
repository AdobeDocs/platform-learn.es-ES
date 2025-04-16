---
title: 'Información general: tutorial técnico completo: One Adobe'
description: 'Tutorial técnico completo: One Adobe'
doc-type: multipage-overview
exl-id: 5bc0d621-0662-4d94-80a0-b6c173c0ac9e
source-git-commit: 603e48e0453911177823fe7ceb340f8ca801c5e1
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 3%

---

# Tutorial técnico completo: One Adobe

![Perspectivas técnicas](./assets/images/techinsiders.png){width="50px" align="left"}

## Información general

Este tutorial es muy diverso y ofrece perspectivas claras en las siguientes aplicaciones:

- Adobe Firefly Services, Adobe Photoshop, Adobe Frame I/O, Adobe Substance 3D Staging
- Adobe Workfront y Adobe Workfront Fusion
- Adobe Experience Manager Cloud Service, Sites, Assets y servicios de entrega perimetral
- Adobe Experience Platform
- Adobe Systems CDP en tiempo real
- Adobe Journey Optimizer

Este tutorial no solo enfocar en Adobe Systems aplicaciones, sino que toma en cuenta la ecosistema más amplia en la que operan las marcas. Para ello, en algunas lecciones se hace hincapié en cómo las aplicaciones que no son de Adobe se integran con las aplicaciones de Adobe. De este modo, obtendrá información detallada sobre cómo las siguientes aplicaciones funcionan junto con Adobe Experience Platform:

- Amazon AWS
- Google Cloud Platform
- Microsoft Azure
- Cartero
- Snowflake
- ...

## Requisitos previos

Si desea realizar este tutorial utilizando su propia instancia de Adobe Experience Cloud, debe aprovisionar las siguientes aplicaciones en su instancia y debe poder acceder a ellas:

- Adobe Firefly
- Adobe Photoshop, Adobe Frame I/O, Adobe Substance 3D Staging
- Adobe Workfront
- Adobe Workfront Fusion
- Adobe Experience Platform, recopilación de datos de Adobe Experience Platform
- Acceso al sistema de demostración Siguiente: [https://dsn.adobe.com/](https://dsn.adobe.com/){target="_blank"}

## Finalización y certificación

Este tutorial forma parte del curso Adobe Certification. Puede inscribirse en el curso junto con este tutorial yendo a [https://certification.adobe.com](https://certification.adobe.com).

Para cada módulo que complete utilizando el siguiente tutorial, debe enviar un prueba de finalización como se indica [aquí](./completion.md).

## Estado de contenido

Para comprobar el estado de los siguientes contenido, vaya al [estado Página](./status.md){target="_blank"}.

### Primeros pasos

[Introducción](./modules/getting-started/gettingstarted/getting-started.md){target="_blank"}

En este módulo básico, preparará todo para que pueda acceder y utilizar el entorno de demostración.

### 1. Flujo de trabajo y planificación

### 2. Creación y producción

[1.1 Servicios Adobe Systems Firefly](./modules/creation-production/module1.1/firefly-services.md){target="_blank"}

En este módulo, usará Adobe Systems API de Firefly Services, API de Photoshop y Servicios de almacenamiento de Microsoft Azure para generar imágenes y tienda ellas mediante programación.

[1.2 Automatización del flujo de trabajo Creative con Workfront Fusion](./modules/creation-production/module1.2/automation.md){target="_blank"}

En este módulo básico, utilizará Adobe Workfront Fusion para automatizar y escalar los flujos de trabajo de creación de contenido.

[1.3 Adobe Express y Adobe Experience Cloud](./modules/creation-production/module1.3/express.md){target="_blank"}

En este módulo básico, utilizará Adobe Express para crear imágenes y vídeos, y compartirá esos recursos con el ecosistema de Adobe Experience Cloud en general.

### 3. Administración de recursos

[1.1 Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}

En este módulo básico, configurará el programa Cloud Service de Adobe Experience Manager, el sitio y el repositorio de Assets.

[1.2 Administración del flujo de trabajo con Adobe Systems Workfront](./modules/asset-mgmt/module2.2/workfront.md){target="_blank"}

En este módulo fundamental, configurará y utilizará Adobe Systems Workfront para administrar flujos de aprobación y utilizará integraciones con Adobe Experience Manager Assets, Universal Editor, Photoshop y más.

### 4. Entrega y Activation

#### Recopilación de datos

[1.1 Fundamento: configuración de Adobe Experience Platform recopilación de datos y SDK web](./modules/delivery-activation/datacollection/dc1.1/data-ingestion-launch-web-sdk.md)

En este módulo básico, aprenderá sobre la recopilación de datos de Adobe Experience Platform y la nueva extensión de Web SDK.

[Base 1.2: ingesta de datos](./modules/delivery-activation/datacollection/dc1.2/data-ingestion.md)

En este módulo básico, ingerirá datos de varias fuentes en Adobe Experience Platform

[1.3 Composición de audiencias federadas](./modules/delivery-activation/datacollection/dc1.3/fac.md)

En este módulo, aprenderá a configurar un modelo de Audiences Federated y a generar audiencias mediante datos federados.

#### Real-Time CDP B2C

[Base 2.1: perfil del cliente en tiempo real](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-1/real-time-customer-profile.md)

En este módulo básico, explorará el perfil del cliente en tiempo real en Adobe Experience Platform mediante la interfaz de usuario y la API.

[2.2 Servicios inteligentes](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-2/intelligent-services.md)

En este módulo, aprenderá a configurar y utilizar Adobe Experience Platform Intelligent Services.

[2.3 Real-Time CDP: crear una audiencia y actuar en consecuencia](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/real-time-cdp-build-a-segment-take-action.md)

En este módulo, configurará una audiencia y la activará en varios destinos, incluidos Google DV360, Adobe Target y AWS S3.

[2.4 Real-Time CDP: Audience Activation a Microsoft Azure Event Hub](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-4/segment-activation-microsoft-azure-eventhub.md)

En este módulo, configurará un destino de Microsoft Azure EventHub como un destino en tiempo real para Adobe Experience Platform Real-time CDP.

[Conexiones Real-Time CDP 2.5: Reenvío de eventos](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-5/aep-data-collection-ssf.md)

En este módulo, reenviará datos del lado del servidor a varios extremos, como Google Cloud Platform Pub/Sub y AWS Kinesis.

[2.6 Transmitir datos desde Apache Kafka a CDP en tiempo real](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-6/aep-apache-kafka.md)

En este módulo, aprenderá a configurar su propio clúster de Apache Kafka y transmitir datos a Adobe Experience Platform.

#### Adobe Journey Optimizer B2C

[3.1 Adobe Systems Journey Optimizer: orquestación](./modules/delivery-activation/ajo-b2c/ajob2c-1/journey-orchestration-create-account.md)

En este módulo utilizará Adobe Journey Optimizer para crear un recorrido basado en déclencheur.

[3.2 Adobe Journey Optimizer: Fuentes de datos externas y acciones personalizadas](./modules/delivery-activation/ajo-b2c/ajob2c-2/journey-orchestration-external-weather-api-sms.md)

En este módulo, utilizará Adobe Journey Optimizer para escuchar el comportamiento de los clientes, tanto en línea como sin conexión, y responder a él de forma inteligente, contextual y en tiempo real a través de varios canales.

[3.3 Adobe Journey Optimizer: Offer Decisioning](./modules/delivery-activation/ajo-b2c/ajob2c-3/offer-decisioning.md)

En este módulo, utilizará Adobe Journey Optimizer para configurar Ofertas personalizadas y su propia decisión de oferta.

[3.4 Adobe Systems Journey Optimizer: recorridos basados en eventos](./modules/delivery-activation/ajo-b2c/ajob2c-4/journeyoptimizer.md)

En este módulo, aprenderá todo lo que hay que saber sobre Journey Optimizer, que ayuda a las empresas a diseñar y ofrecer experiencias conectadas, contextuales y personalizadas a sus clientes.

[3.5 Adobe Journey Optimizer: Servicios de traducción](./modules/delivery-activation/ajo-b2c/ajob2c-5/ajotranslationsvcs.md)

En este módulo, aprenderá a configurar y utilizar los servicios de traducción dentro de Adobe Journey Optimizer para localizar los mensajes a sus clientes.

### 5. Informes e información

#### Adobe Customer Journey Analytics

[1.1 Customer Journey Analytics: crear un tablero con Analysis Workspace sobre Adobe Experience Platform](./modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)

En este módulo, obtendrá información en línea y sin conexión configurando un tablero que contenga datos omnicanal.

[1.2 Customer Journey Analytics: Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector Source de BigQuery](./modules/reporting-insights/cja-b2c/cjab2c-2/customer-journey-analytics-bigquery-gcp.md)

En este módulo, configurará su propia instancia de Google Cloud Platform, cargará datos de demostración en Google Cloud Platform y, a continuación, utilizará el conector de Source de BigQuery para introducir esos datos de Google Cloud Platform en Adobe Experience Platform.

#### Data Distiller

[2.1 Servicio de consultas](./modules/reporting-insights/datadistiller/dd-1/query-service.md)

En este módulo, aprenderá a utilizar el servicio de consultas de Adobe Experience Platform.

![Expertos en tecnología](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre futuros contenido, comuníquese directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.
