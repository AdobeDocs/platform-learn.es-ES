---
title: 'Recopilación de datos de Adobe Experience Platform y reenvío del lado del servidor en tiempo real: actualice su secuencia de datos para que los datos estén disponibles para la propiedad del servidor de recopilación de datos de Adobe Experience Platform'
description: Actualice la secuencia de datos para que los datos estén disponibles para la propiedad del servidor de recopilación de datos de Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: f4bb0673-d553-4027-8bfd-53d2608efaf5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---

# 2.5.2 Actualizar el flujo de datos para que los datos estén disponibles para la propiedad del servidor de recopilación de datos de Adobe Experience Platform

## Actualizar la secuencia de datos

En [Introducción](./../../../getting-started/gettingstarted/ex2.md), creó su propia **[!UICONTROL secuencia de datos]**. Luego usó el nombre `--aepUserLdap-- - Demo System Datastream`.

En este ejercicio, debe configurar ese **[!UICONTROL conjunto de datos]** para que funcione con su **propiedad del servidor de recopilación de datos**.

Para ello, vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Entonces verá esto... En el menú de la izquierda, haga clic en **[!UICONTROL Datastreams]**.

En la esquina superior derecha de la pantalla, seleccione el nombre de la zona protegida, que debe ser `--aepSandboxName--`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

Busque su **[!UICONTROL secuencia de datos]**, que se llama `--aepUserLdap-- - Demo System Datastream`. Haga clic en **[!UICONTROL Flujo de datos]** para abrirlo.

![SDK web](./images/websdk0.png)

Entonces verá esto... Haga clic en **[!UICONTROL + Agregar servicio]**.

![SDK web](./images/websdk3.png)

Seleccione el servicio **Reenvío de eventos**. Esto le mostrará dos configuraciones adicionales. Seleccione la propiedad Reenvío de eventos, que creó en el ejercicio anterior y que se llama `--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Luego selecciona **Desarrollo** en **Entorno**. Haga clic en **Guardar**.

![SDK web](./images/websdk4.png)

El conjunto de datos se ha actualizado y está listo para su uso.

![SDK web](./images/websdk8a.png)

Su secuencia de datos está lista para funcionar con su **[!DNL Event Forwarding property]**.

## Pasos siguientes

Ir a [2.5.3 Crear y configurar un webhook personalizado](./ex3.md){target="_blank"}

Volver a [Conexiones de Real-Time CDP: reenvío de eventos](./aep-data-collection-ssf.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
