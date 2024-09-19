---
title: Migración de Target de at.js 2.x a SDK web
description: Obtenga información sobre cómo migrar una implementación de Adobe Target de at.js 2.x al SDK web de Adobe Experience Platform. Los temas incluyen la carga de la biblioteca de JavaScript, el envío de parámetros, las actividades de renderización y otras llamadas importantes.
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: eebe598e55228d038dfc2adb97df0f8ff03748ac
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 4%

---

# Migración de Target de at.js 2.x al SDK web de Platform

Esta guía es para que los implementadores experimentados de Adobe Target aprendan a migrar una implementación de at.js al SDK web de Adobe Experience Platform.

El SDK web de Adobe Experience Platform es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los servicios de Experience Cloud a través del Edge Network de Adobe Experience Platform. Esta nueva biblioteca combina las capacidades de las bibliotecas de aplicaciones de Adobe independientes en un único paquete ligero que puede aprovechar al máximo las nuevas funciones de Adobe Experience Platform.

## Ventajas principales

Algunas de las ventajas del SDK web de Platform en comparación con la biblioteca at.js independiente son:

* Se comparten audiencias más rápido desde [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=es)
* Integrando Target con Journey Optimizer para admitir [entrega de Offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Capacidad para usar [id de origen](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html?lang=es) para generar el ECID para la identificación de visitantes de mayor duración.
* Consolidación de llamadas de red entre aplicaciones de Adobe
* Un espacio menor para métricas de velocidad de página mejorada
* Una integración más estrecha con Adobe Analytics que no depende de la vinculación de información de llamadas de red independientes
* Flexibilidad de implementación adicional para desarrolladores

Podría decirse que la mayor ventaja de migrar para los clientes de Target es la integración con Real-time Customer Data Platform. Real-Time CDP ofrece enormes capacidades de creación de audiencias en función de la gama completa de datos introducidos en Experience Platform y su capacidad de Perfil del cliente en tiempo real. Un marco de trabajo de control de datos integrado que automatiza el uso responsable de esos datos. La inteligencia artificial aplicada al cliente permite utilizar fácilmente modelos de aprendizaje automático para construir modelos de tendencia y pérdida cuya salida se pueda compartir de nuevo con Adobe Target. Por último, los clientes de los complementos opcionales de Healthcare y Privacy &amp; Security Shield pueden utilizar la función de aplicación del consentimiento para aplicar fácilmente las preferencias de consentimiento de los clientes individuales. El SDK web de Platform es un requisito para utilizar estas funciones de RTCDP en su canal web.

## Objetivos de aprendizaje

Al final de este tutorial, debería saber cómo:

* Comprender las diferencias de implementación de Target entre at.js y el SDK web de Platform
* Configuración inicial para la funcionalidad de Target
* Actualización de la biblioteca at.js al SDK web de Platform
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
* Asegúrese de que tiene una [función Editor o Publicador](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) para su instancia de Target para poder intentar ejemplos por su cuenta
* Obtenga información sobre cómo configurar actividades en Adobe Target. Si necesita un actualizador, los siguientes tutoriales y guías le resultarán útiles para esta lección:
   * [Usar el Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Usar el Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Crear actividades de segmentación de experiencias](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

Una vez que esté listo, el primer paso para realizar una migración correcta es [obtener información acerca del proceso de migración](migration-overview.md) y las diferencias entre at.js y el SDK web de Platform.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target de at.js al SDK web. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
