---
title: Información general
description: Punto de partida para ingenieros de datos, analistas de datos, arquitectos de datos, científicos de datos, ingenieros de orquestación y especialistas en marketing para obtener una comprensión completa del valor comercial de Adobe Experience Platform y todos sus servicios de aplicación.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 1%

---

# Tutorial técnico completo de Adobe Experience Platform

## Información general

Este tutorial es el punto de partida perfecto para Ingenieros de datos, Analistas de datos, Arquitectos de datos, Científicos de datos, Ingenieros de orquestación y Especialistas en marketing para comprender plenamente el valor comercial de Adobe Experience Platform y todos sus servicios de aplicaciones. Cada lección se centra en un desafío real que las empresas enfrentan en el complejo ecosistema de personalización de hoy en día y desglosa cómo el Experience Platform resuelve ese desafío en varios ejercicios prácticos. Consulte este vídeo para comprender los problemas que Adobe Experience Platform le ayudará a solucionar.

>[!VIDEO](https://video.tv.adobe.com/v/344237?quality=12&enable=on)

Este tutorial es muy diverso y ofrece perspectivas claras en las siguientes aplicaciones:

- Adobe Experience Platform
- Recopilación de datos de Adobe Experience Platform
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics
- Offer Decisioning

Este tutorial no solo se centra en las aplicaciones de Adobe, sino que tiene en cuenta el ecosistema más amplio en el que operan las marcas. Para ello, en algunas lecciones se ha centrado la atención en cómo _no Adobe_ las aplicaciones se integran con Adobe Experience Platform. Como tal, obtendrá una comprensión profunda de cómo funcionarán las siguientes aplicaciones junto con Adobe Experience Platform:

- Amazon: AWS Lambda, AWS S3, AWS Kinesis
- Google: Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft: Power BI, Azure EventHub, Azure Blob Storage
- Salesforce: Tableau
- Apache Kafka
- Postman
- ...

Después de completar este tutorial, podrá:

- Configurar esquemas, mezclas, conjuntos de datos e identidades
- Configurar una propiedad de recopilación de datos de Adobe Experience Platform y configurar la nueva extensión del SDK web en la recopilación de datos de Adobe Experience Platform
- Transmitir datos a Adobe Experience Platform en tiempo real mediante la recopilación de datos de Adobe Experience Platform, el administrador de etiquetas de Google o Amazon Alexa
- Ingesta por lotes de datos en Adobe Experience Platform mediante un flujo de trabajo o utilizando una aplicación de extracción, transformación, carga (ETL)
- Visualizar y utilizar el perfil del cliente en tiempo real en Adobe Experience Platform
- Creación de segmentos
- Consumir varias API de Adobe Experience Platform
- Utilice SQL para consultar los datos en Adobe Experience Platform
- Configuración, formación y puntuación de modelos de aprendizaje automático en Adobe Experience Platform
- Utilice el Journey Orchestration para configurar recorridos en tiempo real basados en déclencheur
- Utilice CDP en tiempo real para realizar acciones activando un segmento en varios destinos
- Utilice el Customer Journey Analytics para informar sobre los datos de clientes omnicanal de varias fuentes, incluida Google BigQuery

## Requisitos previos

- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acceso a la recopilación de datos de Adobe Experience Platform: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Acceso al sistema de demostración: [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

>[!IMPORTANT]
>
>Este tutorial se creó para facilitar un formato de taller concreto. Utiliza sistemas y cuentas específicos a los que es posible que no tenga acceso. Incluso sin acceso, creemos que aún puede aprender mucho leyendo este contenido muy detallado. Si participa en uno de los talleres y necesita sus credenciales de acceso, póngase en contacto con el representante del Adobe, que le proporcionará la información necesaria.

## Acerca de este tutorial

En estas lecciones, implementará Adobe Experience Platform y Servicios de aplicaciones mediante un sitio web de demostración que admita varias industrias. El sitio web de demostración y la aplicación móvil tienen una capa de datos y una funcionalidad enriquecidas que le permiten crear una implementación realista. Proporciona acceso a marcas de demostración como **Luma**, **Señal Citi**, **Noticias de EXP**, **MUTUO365**, **Carvelo** y muchos otros. Puede crear su propia propiedad de cliente de recopilación de datos de Adobe Experience Platform, en su propia organización de Experience Cloud, y asignarla a su sitio web de demostración. A continuación, esto genera datos que se envían a su propia instancia de Adobe Experience Platform.

## Arquitectura

Antes de comenzar con los ejercicios prácticos, eche un vistazo a la arquitectura subyacente a este tutorial. Como puede ver en la Información general anterior, este tutorial profundizará en una serie de funciones y características de Adobe Experience Platform, pero también discutirá integraciones múltiples en una variedad de Fuentes y Destinos. Para que pueda comprender correctamente la arquitectura subyacente a este tutorial y la posición general de Adobe Experience Platform en el ecosistema de Enterprise, comience por revisar el diagrama y el vídeo de arquitectura.

Vaya a [Arquitectura](./architecture.md).


## Vídeos

Vídeos de ![](./assets/images/yt.jpeg)

Puedes encontrar muchos videos interesantes de nuestros eventos de la Academia Tecnológica, de Bootcamp y más sobre nuestros [Canal de YouTube de la comunidad de Experience Makers](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

Se han creado varios vídeos que muestran elementos de la habilitación y potentes integraciones entre aplicaciones de Adobe Experience Platform y aplicaciones que no son de Adobe. Haga clic en el vínculo siguiente para encontrar una descripción general de esos vídeos.

Vaya a [Vídeos](./videos.md).



## ¿Cómo se mide la finalización del tutorial técnico completo para Adobe Experience Platform?

Si participa en este tutorial como socio de Adobe o empleado de Adobe, debe enviar el progreso después de completar cada módulo de habilitación.

Aquí puede encontrar los requisitos y el proceso para enviar la finalización: [Medición finalizada](./completion.md)

## Contenido

[0. Introducción](./modules/module0/getting-started.md)

- **Audiencia:** Todos los participantes del tutorial técnico completo para Adobe Experience Platform
- **Requisitos previos:** Acceso a Demo System Next, Adobe Experience Platform y recopilación de datos de Adobe Experience Platform. Acceda al ID de configuración predeterminado de su entorno de Adobe Experience Platform.
- **Descripción:** En este módulo fundacional, configurará todo para que pueda acceder y utilizar el entorno de demostración.
- **Inversión en tiempo:** 30 minutos

[1. Fundamento: configuración de la recopilación de datos de Adobe Experience Platform y el SDK web](./modules/module1/data-ingestion-launch-web-sdk.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos
- **Requisitos previos:** Acceso a la recopilación de datos de Adobe Experience Platform y Adobe Experience Platform.
- **Descripción:** En este módulo fundacional, aprenderá sobre la recopilación de datos de Adobe Experience Platform y la nueva extensión del SDK web.
- **Inversión en tiempo:** 30 minutos

[2. Base: ingesta de datos](./modules/module2/data-ingestion.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos
- **Requisitos previos:** Acceso a la recopilación de datos de Adobe Experience Platform y Adobe Experience Platform.
- **Descripción:** En este módulo fundacional, ingerirá datos del sitio web en Platform
- **Inversión en tiempo:** 120 minutos

[3. Fundamento: Perfil del cliente en tiempo real](./modules/module3/real-time-customer-profile.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, especialista en marketing
- **Requisitos previos:** Acceso a Adobe Experience Platform y Postman
- **Descripción:** En este módulo fundacional, explorará el Perfil del cliente en tiempo real en Adobe Experience Platform mediante la interfaz de usuario y la API.
- **Inversión en tiempo:** 90 minutos
- **Descargar estos recursos**:
   - [Colecciones de Postman](./assets/postman/postman_profile.zip)

[4. Servicio de consultas](./modules/module4/query-service.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, analista de datos, experto de BI
- **Requisitos previos:** Acceso a Adobe Experience Platform, servicio de consultas, Power BI o Tableau
- **Descripción:** En este módulo, aprenderá a utilizar el servicio de consulta de Adobe Experience Platform.
- **Inversión en tiempo:** 90 minutos
- **Descargar estos recursos**:
   - [JSON: Datos de muestra: Sistema de demostración: conjunto de datos de evento para el sitio web](./assets/json/ee.json)
   - [JSON: Datos de muestra: Sistema de demostración: conjunto de datos de evento para el centro de llamadas](./assets/json/callcenter.json)
   - [JSON: Datos de muestra: Sistema de demostración: conjunto de datos de perfil para la fidelidad](./assets/json/loyalty.json)

[5. Servicios inteligentes](./modules/module5/intelligent-services.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, científico de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform, servicios inteligentes
- **Descripción:** En este módulo, aprenderá a configurar, configurar y utilizar los servicios inteligentes de Adobe Experience Platform.
- **Inversión en tiempo:** 60 minutos

[6. Real-Time CDP: cree un segmento y tome medidas](./modules/module6/real-time-cdp-build-a-segment-take-action.md)

- **Audiencia:** Arquitecto de datos, ingeniero de orquestación, especialista en marketing
- **Requisitos previos:** Acceso a Adobe Experience Platform, CDP en tiempo real, Adobe Audience Manager, Adobe Target, AWS S3
- **Descripción:** En este módulo, debe configurar un segmento, habilitarlo para la segmentación por transmisión y activarlo en varios destinos, incluidos Google DV360, Google AdWords, Adobe Audience Manager, Adobe Target y destinos S3 como el Marketing Cloud de Salesforce.
- **Inversión en tiempo:** 90 minutos

[7. Adobe Journey Optimizer: Organización](./modules/module7/journey-orchestration-create-account.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, ingeniero de orquestación
- **Requisitos previos:** Acceso a Adobe Experience Platform y Adobe Journey Optimizer
- **Descripción:** En este módulo, utilizará Adobe Journey Optimizer para crear un recorrido basado en déclencheur.
- **Inversión en tiempo:** 60 minutos

[8. Adobe Journey Optimizer: Fuentes de datos externas y acciones personalizadas](./modules/module8/journey-orchestration-external-weather-api-sms.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, ingeniero de orquestación, especialista en marketing
- **Requisitos previos:** Acceso a Adobe Experience Platform, Adobe Journey Optimizer, API de tiempo abierto, Twilio
- **Descripción:** En este módulo, utilizará Adobe Journey Optimizer para escuchar el comportamiento de los clientes, tanto en línea como sin conexión, y responder a él de forma inteligente, contextual y en tiempo real a través de varios canales.
- **Inversión en tiempo:** 90 minutos

[9. Adobe Journey Optimizer: offer decisioning](./modules/module9/offer-decisioning.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, ingeniero de orquestación, especialista en marketing
- **Requisitos previos:** Acceso a Adobe Experience Platform y Offer decisioning
- **Descripción:** En este módulo, utilizará el servicio de aplicación Adobe Experience Platform - Ofertas/Decisiones de forma práctica para configurar Ofertas personalizadas y su propia actividad de oferta.
- **Inversión en tiempo:** 120 minutos

[10. Adobe Journey Optimizer: Recorridos basados en eventos](./modules/module10/journeyoptimizer.md)

- **Audiencia:** Especialista en marketing de correo electrónico, especialista en orquestación, ingeniero de datos, arquitecto de datos, analista de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform y Journey Optimizer
- **Descripción:** En este módulo, aprenderá todo lo que hay que saber sobre Journey Optimizer, que ayuda a las empresas a diseñar y ofrecer experiencias conectadas, contextuales y personalizadas a sus clientes.
- **Inversión en tiempo:** 120 minutos

[11. Customer Journey Analytics: Creación de un tablero con Analysis Workspace en la parte superior de Adobe Experience Platform](./modules/module11/customer-journey-analytics-build-a-dashboard.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, analista de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform y Customer Journey Analytics
- **Descripción:** En este módulo, obtendrá perspectivas sin conexión en línea configurando un panel que contenga datos omnicanal como Interacciones de sitios web, Interacciones de aplicaciones móviles, Interacciones de centros de llamadas, Interacciones en el almacén y mucho más.
- **Inversión en tiempo:** 120 minutos

[12. Customer Journey Analytics: Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector de origen BigQuery](./modules/module12/customer-journey-analytics-bigquery-gcp.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, analista de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery
- **Descripción:** En este módulo, debe configurar su propia instancia de Google Cloud Platform, cargar datos de demostración en Google Cloud Platform y, a continuación, utilizar el conector de origen BigQuery para introducir esos datos de Google Cloud Platform en Adobe Experience Platform. Por último, utilizará Customer Journey Analytics para visualizar esos datos.
- **Inversión en tiempo:** 120 minutos
- **Descargar estos recursos**:
   - [JSON: Datos de muestra: Demostración: Datos de fidelidad](./assets/json/bqLoyalty.json)

[13. Real-Time CDP: Activación de segmentos en el centro de eventos de Microsoft Azure](./modules/module13/segment-activation-microsoft-azure-eventhub.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, analista de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform, CDP en tiempo real y Microsoft Azure
- **Descripción:** En este módulo, configurará un destino de Microsoft Azure EventHub como destino en tiempo real para CDP en tiempo real de Adobe Experience Platform. También configurará e implementará una función de Azure que se activará en tiempo real cada vez que Adobe Experience Platform envíe una carga útil de segmento a su destino de Azure EventHub. La función de Azure que va a almacenar en déclencheur mostrará el mecanismo de las funciones de activación de CDP en tiempo real de Adobe Experience Platform.
Como parte de este módulo, también obtendrá una comprensión de los déclencheur de CDP en tiempo real para proporcionar una carga útil a un destino especificado. También analizaremos el estado de una calificación de segmento y cómo se relaciona con la activación.
- **Inversión en tiempo:** 90 minutos

[14. Conexiones de Real-Time CDP: Reenvío de eventos](./modules/module14/aep-data-collection-ssf.md)

- **Audiencia:** Ingeniero de datos, arquitecto de datos, analista de datos
- **Requisitos previos:** Acceso a las propiedades de conexiones, etiquetas y reenvío de eventos de Real-Time CDP
- **Descripción:** En este módulo, utilizará los conjuntos de datos, esquemas y la propiedad de recopilación de datos de Adobe Experience Platform configurados anteriormente para recopilar datos y, a continuación, reenviar esos datos del lado del servidor a un punto final de su elección.
- **Inversión en tiempo:** 90 minutos

[15. Transmitir datos de Apache Kafka a Real-Time CDP](./modules/module15/aep-apache-kafka.md)

- **Audiencia:** Analista de datos, ingeniero de datos, arquitecto de datos
- **Requisitos previos:** Acceso a Adobe Experience Platform
- **Descripción:** En este módulo, aprenderá a configurar su propio clúster de Apache Kafka, definir temas, productores y consumidores y transmitir datos a Adobe Experience Platform mediante el conector Adobe Experience Platform Sink para Kafka Connect.
- **Inversión en tiempo:** 90 minutos

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.
