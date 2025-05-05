---
title: Migración de Target de at.js 2.x a Web SDK
description: Obtenga información sobre cómo migrar una implementación de Adobe Target de at.js 2.x a Adobe Experience Platform Web SDK. Los temas incluyen la carga de la biblioteca de JavaScript, el envío de parámetros, las actividades de renderización y otras llamadas importantes.
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 5%

---

# Migración de Target de at.js 2.x a Platform Web SDK

Esta guía es para que los implementadores experimentados de Adobe Target aprendan a migrar una implementación de at.js a Adobe Experience Platform Web SDK.

Adobe Experience Platform Web SDK es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los servicios de Experience Cloud a través de Adobe Experience Platform Edge Network. Esta nueva biblioteca combina las capacidades de las bibliotecas de aplicaciones de Adobe independientes en un único paquete ligero que puede aprovechar al máximo las nuevas funciones de Adobe Experience Platform.


>[!NOTE]
>
>Hay tutoriales de migración similares disponibles para:
>
> * [Adobe Analytics](../tutorial-migrate-analytics-websdk/migration-to-websdk-overview.md)
> * [Adobe Audience Manager](https://experienceleague.adobe.com/es/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk)

>[!CAUTION]
>
> Dado que Platform Web SDK admite varias aplicaciones de Adobe, todas las bibliotecas de Adobe de una página determinada deben migrarse al mismo tiempo. Por ejemplo, no se admite una implementación mixta de Web SDK para Target y AppMeasurement para Analytics en una sola página _1._ Sin embargo, se admite una implementación mixta en diferentes páginas, por ejemplo, Web SDK en la página A y at.js con AppMeasurement en la página B.



## Ventajas principales

Algunas de las ventajas de Platform Web SDK en comparación con la biblioteca independiente at.js son las siguientes:

* Se comparten audiencias más rápido desde [Real-Time Customer Data Platform](https://experienceleague.adobe.com/es/docs/platform-learn/tutorials/destinations/target/next-hit-personalization)
* Integrando Target con Journey Optimizer para admitir [Offer Decisioning delivery](https://experienceleague.adobe.com/es/docs/target/using/integrate/ajo/offer-decision)
* Capacidad para usar [id de origen](https://experienceleague.adobe.com/es/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids) para generar el ECID para la identificación de visitantes de mayor duración.
* Un espacio menor para métricas de velocidad de página mejorada
* Flexibilidad de implementación adicional para desarrolladores

Podría decirse que la mayor ventaja de migrar para los clientes de Target es la integración con Real-Time Customer Data Platform. Real-Time CDP ofrece enormes capacidades de creación de audiencias en función de la gama completa de datos ingeridos en Experience Platform y su capacidad de Perfil del cliente en tiempo real. Un marco de trabajo de control de datos integrado que automatiza el uso responsable de esos datos. La inteligencia artificial aplicada al cliente permite utilizar fácilmente modelos de aprendizaje automático para construir modelos de tendencia y pérdida cuya salida se pueda compartir de nuevo con Adobe Target. Por último, los clientes de los complementos opcionales de Healthcare y Privacy &amp; Security Shield pueden utilizar la función de aplicación del consentimiento para aplicar fácilmente las preferencias de consentimiento de los clientes individuales. Platform Web SDK es un requisito para utilizar estas funciones de Real-Time CDP en el canal web.

## Objetivos de aprendizaje

Al final de este tutorial, debería saber cómo:

* Comprender las diferencias de implementación de Target entre at.js y Platform Web SDK
* Configuración inicial para la funcionalidad de Target
* Actualizar la biblioteca at.js a Platform Web SDK.
* Procesar actividades del Compositor de experiencias visuales y basadas en formularios
* Pasar parámetros a Target
* Seguimiento de eventos de conversión
* Habilitar compatibilidad entre dominios
* Actualización de audiencias y scripts de perfil
* Validar la implementación
* Entrega de experiencias de Debug Target


## Requisitos previos

Para completar este tutorial, primero debe:

* Obtenga información técnica sobre su implementación actual de at.js de Target
* Asegúrese de que tiene una [función Editor o Publicador](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=es#section_8C425E43E5DD4111BBFC734A2B7ABC80) para su instancia de Target para poder intentar ejemplos por su cuenta
* Obtenga información sobre cómo configurar actividades en Adobe Target. Si necesita un actualizador, los siguientes tutoriales y guías le resultarán útiles para esta lección:
   * [Usar el Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html?lang=es)
   * [Usar el Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html?lang=es)
   * [Creación de actividades de segmentación de experiencias](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html?lang=es)

Una vez que esté listo, el primer paso para realizar una migración correcta es [obtener información acerca del proceso de migración](migration-overview.md) y las diferencias entre at.js y Platform Web SDK.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con la migración de Target de at.js a Web SDK. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=es#M463).
