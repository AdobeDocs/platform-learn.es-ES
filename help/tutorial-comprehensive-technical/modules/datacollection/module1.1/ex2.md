---
title: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: Edge Network, flujos de datos y recopilación de datos del servidor'
description: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: Edge Network, flujos de datos y recopilación de datos del servidor'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Edge Network 1.1.2, flujos de datos y recopilación de datos del lado del servidor

## Contexto

En este ejercicio creará una **secuencia de datos**. Un **flujo de datos** indica a los servidores de Adobe Edge a dónde enviar los datos una vez que el SDK web los ha recopilado. Por ejemplo, ¿desea enviar los datos a Adobe Experience Platform? ¿Adobe Analytics? ¿Adobe Audience Manager? ¿Adobe Target?

Las secuencias de datos siempre se administran en la interfaz de usuario de recopilación de datos de Adobe Experience Platform y son esenciales para la recopilación de datos de Adobe Experience Platform con el SDK web. Incluso cuando implemente un SDK web con una solución de administración de etiquetas que no sea de Adobe, deberá crear su secuencia de datos en la interfaz de usuario de recopilación de datos de Adobe Experience Platform.

En el próximo ejercicio se implementará el SDK web en el explorador. A continuación, tendrá más claro el aspecto de los datos que se están recopilando. Por ahora, solo estamos diciendo a la secuencia de datos dónde reenviar los datos.

## Crear una secuencia de datos

En el [Ejercicio 0.2](./../../../modules/gettingstarted/gettingstarted/ex2.md) ya creó una secuencia de datos, pero no se analizó el fondo y el motivo de pertenecer a dicha secuencia.

Un conjunto de datos indica a los servidores de Adobe Edge dónde enviar los datos una vez que el SDK web los ha recopilado. Por ejemplo, ¿desea enviar los datos a Adobe Experience Platform? ¿Adobe Analytics? ¿Adobe Audience Manager? ¿Adobe Target? Las secuencias de datos se administran en la interfaz de usuario de recopilación de datos de Adobe Experience Platform y son esenciales para la recopilación de datos de Platform con el SDK web, independientemente de si va a implementar o no el SDK web mediante la recopilación de datos de Adobe Experience Platform.

Revisemos tu **[!UICONTROL secuencia de datos]**:

Vaya a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/).

Haga clic en **[!UICONTROL Datastreams]** o **[!UICONTROL Datastreams (Beta)]** en el menú de la izquierda.

![Haga clic en el icono Flujo de datos en el panel de navegación izquierdo](./images/edgeconfig1.png)

Busque su secuencia de datos, que se llama `--aepUserLdap-- - Demo System Datastream`.

![Asigne un nombre al conjunto de datos y guarde](./images/edgeconfig2.png)

A continuación, verá los detalles de su secuencia de datos.

![Asigne un nombre al conjunto de datos y guarde](./images/edgecfg1.png)

Haz clic en **...** junto a **Adobe Experience Platform** y haz clic en **Editar**.

![Asigne un nombre al conjunto de datos y guarde](./images/edgecfg1a.png)

Entonces verá esto... En este momento, solo ha habilitado Adobe Experience Platform. Su configuración será similar a la siguiente. (Según el entorno y la instancia de Adobe Experience Platform, el nombre de la zona protegida puede ser diferente)

![Asigne un nombre al conjunto de datos y guarde](./images/edgecfg2.png)

Debe interpretar los campos siguientes de esta manera:

Para esta secuencia de datos...

- Todos los datos recopilados se almacenarán en la zona protegida `--aepSandboxName--` de Adobe Experience Platform
- Todos los datos de Experience Event se recopilan de forma predeterminada en el conjunto de datos **Sistema de demostración: conjunto de datos de evento para el sitio web (Global v1.1)**
- Todos los datos de perfil se recopilarán de forma predeterminada en el conjunto de datos **Sistema de demostración - Conjunto de datos de perfil para el sitio web (Global v1.1)** (el SDK web aún no admite la ingesta nativa de datos de perfil con el SDK web, y estarán disponibles en una fase posterior)
- Si desea utilizar el servicio de aplicación **Offer decisioning** para esta secuencia de datos, debe marcar la casilla de Offer decisioning. (Esto formará parte de [Módulo 3.3](./../../../modules/ajo-b2c/module3.3/offer-decisioning.md))
- Si desea usar la **Segmentación de Edge**, marque la casilla de la Segmentación de Edge.
- Si desea usar **Destinos de Personalization**, marque la casilla Destinos de Personalization.

Por ahora, no se necesita ninguna otra configuración para el conjunto de datos.

Paso siguiente: [1.1.3 Introducción a la recopilación de datos de Adobe Experience Platform](./ex3.md)

[Volver al módulo 1.1](./data-ingestion-launch-web-sdk.md)

[Volver a todos los módulos](./../../../overview.md)
