---
title: 'Recopilación de datos de Adobe Experience Platform y reenvío del lado del servidor en tiempo real: actualice su secuencia de datos para que los datos estén disponibles para la propiedad del servidor de recopilación de datos de Adobe Experience Platform'
description: Actualice la secuencia de datos para que los datos estén disponibles para la propiedad del servidor de recopilación de datos de Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 7b5b598e-e54c-4f0f-b260-d643600ee6ca
source-git-commit: 6485bfa1c75c43bb569f77c478a273ace24a61d4
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# 2.5.2 Actualizar el flujo de datos para que los datos estén disponibles para la propiedad del servidor de recopilación de datos de Adobe Experience Platform

## Actualizar la secuencia de datos

En [Introducción](./../../gettingstarted/gettingstarted/ex2.md), creó su propia **[!UICONTROL secuencia de datos]**. Luego usó el nombre `--aepUserLdap-- - Demo System Datastream`.

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

Paso siguiente: [2.5.3 Crear y configurar un webhook personalizado](./ex3.md)

[Volver al módulo 2.5](./aep-data-collection-ssf.md)

[Volver a todos los módulos](./../../../overview.md)
