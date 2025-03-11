---
title: Migre la implementación de Adobe Target en su aplicación móvil a la extensión Adobe Journey Optimizer - Decisioning
description: Obtenga información sobre cómo migrar la implementación de su aplicación móvil de Adobe Target a la extensión Adobe Journey Optimizer - Decisioning
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Migre la implementación de Adobe Target en su aplicación móvil a la extensión Adobe Journey Optimizer - Decisioning

Esta guía es para que los implementadores con experiencia en Adobe Target aprendan a migrar las implementaciones existentes de Adobe Experience Platform Mobile SDK de la extensión de Adobe Target a la extensión Adobe Journey Optimizer - Decisioning.

Adobe Experience Platform Mobile SDK potencia la participación integral en sus aplicaciones móviles. La extensión de Target se basa en Mobile SDK para ayudarle a personalizar las experiencias de la aplicación con Adobe Target. La extensión de Decisioning es un enfoque más reciente para implementar Adobe Target en aplicaciones móviles que utiliza las funcionalidades de Adobe Experience Platform Edge Network que ayudan a integrar Target con aplicaciones basadas en Platform, como Real-Time CDP y Journey Optimizer.

![Diagrama que muestra el SDK móvil conectándose a Target a través de Edge Network con la extensión Decisioning](assets/datacollection.png)

>[!INFO]
>
>Dentro del ecosistema de Adobe Experience Platform Mobile SDK, las extensiones se implementan mediante SDK importados en las aplicaciones que pueden tener nombres diferentes:
>
> * **Target SDK** implementa la **extensión de Adobe Target**
> * **Optimizar SDK** implementa la extensión **Adobe Journey Optimizer - Decisioning**


## Ventajas principales

Algunas de las ventajas de la extensión de Adobe Journey Optimizer Decisioning en comparación con la extensión de Target son:

* Se comparten audiencias más rápido desde [Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=es)
* Integrando Target con Journey Optimizer para admitir [Offer Decisioning delivery](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Una integración más estrecha con Adobe Analytics que no depende de la vinculación de información de llamadas de red independientes
* Flexibilidad de implementación adicional para desarrolladores

Podría decirse que la mayor ventaja de migrar para los clientes de Target es la integración con Real-Time Customer Data Platform. Real-Time CDP ofrece enormes capacidades de creación de audiencias en función de la gama completa de datos ingeridos en Experience Platform y su capacidad de Perfil del cliente en tiempo real. Un marco de trabajo de control de datos integrado automatiza el uso responsable de esos datos. La inteligencia artificial aplicada al cliente permite utilizar fácilmente modelos de aprendizaje automático para construir modelos de tendencia y pérdida cuya salida se pueda compartir de nuevo con Adobe Target. Y, por último, los clientes de los complementos opcionales de Healthcare y Privacy &amp; Security Shield pueden utilizar la función de aplicación del consentimiento para aplicar las preferencias de consentimiento de los clientes individuales. Platform Mobile SDK y la extensión Decisioning son requisitos para utilizar estas funciones de Real-Time CDP en el canal móvil.

## Pasos de migración

El nivel de esfuerzo para migrar de la extensión de Target a la extensión de Decisioning depende de la complejidad de la implementación actual y de las funciones de Target utilizadas.

Independientemente de lo simple o compleja que sea su implementación, es importante comprender completamente su estado actual antes de migrar. Esta guía le ayuda a desglosar los componentes de la implementación actual y a desarrollar un plan manejable para migrar cada parte.

El proceso de migración incluye los siguientes pasos clave:

1. Evaluar la implementación actual
1. Configuración de los componentes iniciales para conectarse a Adobe Experience Platform Edge Network
1. Actualice la implementación base para reemplazar la extensión de Target con la extensión Decisioning.
1. Mejore la implementación de Optimize SDK para sus casos de uso específicos. Esto puede implicar pasar parámetros adicionales, utilizar tokens de respuesta, etc.
1. Actualizar objetos en la interfaz de Target, como scripts de perfil, actividades y definiciones de audiencia
1. Valide la implementación final antes de realizar el cambio en la aplicación de producción.

>[!INFO]
>
>Dentro del ecosistema de Adobe Experience Platform Mobile SDK, las extensiones se implementan mediante SDK importados en las aplicaciones que pueden tener nombres diferentes:
>
> * **Target SDK** implementa la **extensión de Adobe Target**
> * **Optimizar SDK** implementa la extensión **Adobe Journey Optimizer - Decisioning**

A continuación, revise la [comparación detallada de la extensión de Target y la extensión de Decisioning](comparison.md) para comprender mejor las diferencias técnicas e identificar las áreas que requieren un enfoque adicional.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
