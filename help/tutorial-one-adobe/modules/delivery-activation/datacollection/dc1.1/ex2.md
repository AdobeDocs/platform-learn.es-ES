---
title: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión de Web SDK: Edge Network, Datastreams y recopilación de datos del lado del servidor'
description: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión de Web SDK: Edge Network, Datastreams y recopilación de datos del lado del servidor'
kt: 5342
doc-type: tutorial
exl-id: f805b2a6-c813-4734-8a78-f8588ecd0683
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# 1.1.2 Recopilación de datos de Edge Network, flujos de datos y servidores

## Contexto

En este ejercicio creará un **conjunto de datos**. Una **secuencia de datos** indica a los servidores de Adobe Edge Network a dónde enviar los datos una vez que Web SDK los ha recopilado. Por ejemplo, ¿desea enviar los datos a Adobe Experience Platform? ¿Adobe Analytics? ¿Adobe Audience Manager? ¿Adobe Target?

Las secuencias de datos siempre se administran en la interfaz de usuario de recopilación de datos de Experience Platform y son esenciales para la recopilación de datos de Experience Platform con [Web SDK](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/home). Incluso cuando implementa Web SDK con una solución de administración de etiquetas que no sea de Adobe, debe crear una secuencia de datos.

En el próximo ejercicio se implementará Web SDK en el explorador. A continuación, tendrá más claro el aspecto de los datos que se están recopilando. Por ahora, solo estamos diciendo a la secuencia de datos dónde reenviar los datos.

## Crear un flujo de datos

En [Introducción](./../../../../modules/getting-started/gettingstarted/ex2.md) ya creó un conjunto de datos, pero no se habló del contexto y el motivo por el que lo creó.

Un [conjunto de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/overview) indica a los servidores de Edge Network a dónde enviar los datos una vez que Web SDK los ha recopilado. Consulte la documentación de [agregar servicios a un conjunto de datos](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure#add-services) para obtener información detallada sobre dónde puede enviar los datos a través del conjunto de datos.

Las secuencias de datos se administran en la interfaz de usuario de recopilación de datos de Experience Platform y son esenciales para la recopilación de datos con Web SDK, independientemente de si va a implementar o no Web SDK mediante la recopilación de datos de Adobe Experience Platform.

Revisemos su **[!UICONTROL secuencia de datos]**:

Vaya a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/).

Haga clic en **[!UICONTROL Flujos de datos]** en el menú de la izquierda.

![Haga clic en el icono Flujo de datos en el panel de navegación izquierdo](./images/edgeconfig1.png)

Abra la secuencia de datos, que se llama `--aepUserLdap-- - Demo System Datastream`.

![Asigne un nombre al conjunto de datos y guarde](./images/edgeconfig2.png)

A continuación, verá los detalles del conjunto de datos.

![Asigne un nombre al conjunto de datos y guarde](./images/edgecfg1.png)

Haz clic en **...** junto a **Adobe Experience Platform** y haz clic en **Editar**.

![Asigne un nombre al conjunto de datos y guarde](./images/edgecfg1a.png)

Entonces verá esto... En este momento, solo ha habilitado Adobe Experience Platform. Su configuración será similar a la siguiente. (Según el entorno y la instancia de Adobe Experience Platform, el nombre de la zona protegida puede ser diferente)

![Asigne un nombre al conjunto de datos y guarde](./images/edgecfg2.png)

Debe interpretar los campos siguientes de esta manera:

Para esta secuencia de datos...

- Todos los datos recopilados se almacenarán en la zona protegida `--aepSandboxName--` de Adobe Experience Platform
- Todos los datos de Experience Event se recopilan de forma predeterminada en el conjunto de datos **Sistema de demostración: conjunto de datos de evento para el sitio web (Global v1.1)**
- Todos los datos de perfil se recopilarán de forma predeterminada en el conjunto de datos **Sistema de demostración - Conjunto de datos de perfil para el sitio web (Global v1.1)** (Web SDK aún no admite la ingesta nativa de datos de perfil con Web SDK)
- Si desea utilizar el servicio de aplicaciones **Offer Decisioning** para este conjunto de datos, debe marcar la casilla de Offer Decisioning. (Esto formará parte de [Módulo 3.3](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-3/offer-decisioning.md))
- **La segmentación de Edge** está habilitada de manera predeterminada, lo que significa que las audiencias que cumplan los requisitos se evaluarán en el perímetro, tras la ingesta de tráfico entrante
- Si desea usar [destinos de personalización](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/personalization/overview), marque la casilla de **Destinos de Personalization**.
- Si desea usar las capacidades de **Adobe Journey Optimizer** en esta secuencia de datos, debe marcar la casilla de **Adobe Journey Optimizer**.

Por ahora, no se necesita ninguna otra configuración para el conjunto de datos.

## Pasos siguientes

Ir a [1.1.3 Introducción a la recopilación de datos de Adobe Experience Platform](./ex3.md){target="_blank"}

Volver a la [configuración de la recopilación de datos de Adobe Experience Platform y la extensión de etiquetas de Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
