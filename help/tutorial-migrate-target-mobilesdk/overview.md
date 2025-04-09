---
title: Migrate your mobile app from the Adobe Target to the Adobe Journey Optimizer - Decisioning extension
description: Learn how to migrate your mobile app implementation from the Adobe Target to the Adobe Journey Optimizer - Decisioning extension
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: 2ebad2014d4c29a50af82328735258958893b42c
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 1%

---

# Migrar la aplicación móvil de la Adobe Target a la Adobe Systems Journey Optimizer: extensión de toma de decisiones

Este guía es para que los implementadores de Adobe Target experimentados aprendan a migrar las implementaciones existentes de Adobe Systems Experience desde Mobile SDK desde la extensión Adobe Target a la extensión Adobe Systems Journey Optimizer - Decisioning.

Adobe Experience Platform SDK móvil potencia las participación integrales en sus aplicaciones móviles. La extensión Target se basa en el SDK de Mobile para ayudarle a personalizar las experiencias de aplicación con Adobe Target. La extensión Decisioning es un enfoque más nuevo para implementar Adobe Target en aplicaciones móviles que usa capacidades de red de Adobe Experience Platform Edge que ayudan a integrar Target con aplicaciones basadas en Platform, como Real-Time CDP y Journey Optimizer.

![Diagrama que muestra el SDK móvil conectándose a Target a través de la red perimetral con la extensión Decisioning](assets/datacollection.png)

## Ventajas principales

Some of the benefits of the Adobe Journey Optimizer Decisioning extension compared to the Target extension include:

* Faster sharing of audiences from [Real-Time Customer Data Platform](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization)
* Integrating Target with Journey Optimizer to support [Offer Decisioning delivery](https://experienceleague.adobe.com/en/docs/target/using/integrate/ajo/offer-decision)
* A tighter integration with Adobe Analytics which does not rely on stitching information from separate network calls
* Additional implementation flexibility for developers

Podría decirse que el mayor beneficio para Target clientes de la migración es la integración con el Platform de datos del cliente en tiempo real. CDP en tiempo real ofrece enormes capacidades de creación de audiencia basadas en toda la gama de datos ingeridos en Experience Platform y su capacidad de perfil de cliente en tiempo real. Un marco de trabajo de gobierno de datos integrado automatiza el uso responsable de esos datos. La IA del cliente le permite utilizar fácilmente modelos de aprendizaje automático para construir modelos de propensión y pérdida de resultados cuya salida se puede compartir con Adobe Target. Y, por último, los clientes de los complementos opcionales de Healthcare y Privacy &amp; Security Shield pueden usar la función de aplicación de consentimiento para hacer cumplir las preferencias de consentimiento de los clientes individuales. Platform SDK móvil y la extensión Decisioning son un requisito para utilizar estas funciones de CDP en tiempo real en su canal móvil.

## Pasos de migración

El nivel de esfuerzo para migrar de la extensión Target a la extensión Decisioning depende de la complejidad de las implementación actuales y de Target funciones utilizadas.

No importa cuán simple o compleja sea su implementación, es importante comprender completamente su estado actual antes de migrar. This guide helps you to break down the components of your current implementation and develop a manageable plan to migrate each piece.

The migration process involves the following key steps:

1. Assess your current implementation, including:
   1. All Target SDK APIs used
   1. Modifications to Target&#39;s global settings
   1. Integración con Adobe Analytics
   1. Uso de parámetros de entidad, perfil y mbox
   1. Uso de scripts y audiencias perfil
   1. Código personalizado único del implementación
1. Configure los componentes iniciales para conectarse a la red de Adobe Experience Platform Edge
1. Actualice el implementación fundamental para sustituir la extensión Target por la extensión Decisioning
1. Enhance the Optimize SDK implementation for your specific use cases. Esto puede implicar pasar parámetros adicionales, usar tokens de respuesta, etc.
1. Update objects in the Target interface, such as profile scripts, activities, and audience definitions
1. Validate the final implementation before making the switch in your production app


>[!INFO]
>
>Within the Adobe Experience Platform Mobile SDK ecosystem, extensions are implemented by SDKs imported into your applications which may have different names:
>
> * **Target SDK** implementa la extensión Adobe Target ****
> * **Optimize SDK** implementa la extensión de **Adobe Systems Journey Optimizer: Decisioning**

Siguiente, revise la comparación detallada [de la extensión de Target y la extensión](comparison.md) de toma de decisiones para comprender mejor las diferencias técnicas e identificar áreas que requieren enfocar adicionales.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con la migración de su Target móvil de la extensión Target a la extensión Decisioning. Si se encuentra con obstáculos con su migración o siente gustar falta esencial información en este guía, háganoslo saber publicando en [esta discusión](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625) de la Comunidad.
