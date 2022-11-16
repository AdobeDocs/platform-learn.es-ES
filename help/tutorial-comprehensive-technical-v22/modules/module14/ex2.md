---
title: 'Recopilación de datos de Adobe Experience Platform y reenvío del servidor en tiempo real: actualice el almacén de datos para que los datos estén disponibles en la propiedad del servidor de recopilación de datos de Adobe Experience Platform'
description: Actualice el almacén de datos para que los datos estén disponibles en la propiedad del servidor de recopilación de datos de Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 0c42350c-c38a-410e-bdab-41aff6024f81
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 14.2 Actualizar el almacén de datos para que los datos estén disponibles en la propiedad del servidor de recopilación de datos de Adobe Experience Platform

## 14.2.1 Actualizar el almacén de datos

En [Ejercicio 0.2](./../../modules/module0/ex2.md), ha creado su **[!UICONTROL Datastream]**. A continuación, utilizó el nombre `--demoProfileLdap-- - Demo System Datastream`.

En este ejercicio, debe configurar que **[!UICONTROL Datastream]** para trabajar con su **[!DNL Data Collection Server property]**.

Para ello, vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Entonces verás esto. En el menú de la izquierda, haga clic en **[!UICONTROL Datastreams]**.

En la esquina superior derecha de la pantalla, seleccione el nombre del simulador de pruebas, que debería ser `--aepSandboxId--`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

Busque su **[!UICONTROL Datastream]**, cuyo nombre es `--demoProfileLdap-- - Demo System Datastream`. Haga clic en **[!UICONTROL Datastream]** para abrirlo.

![WebSDK](./images/websdk0.png)

Entonces verás esto. Haga clic en **[!UICONTROL + Añadir servicio]**.

![WebSDK](./images/websdk3.png)

Seleccione el servicio **Reenvío de eventos**. Esto le mostrará dos configuraciones adicionales. Seleccione la propiedad Event Forwarding, que creó en el ejercicio anterior y cuyo nombre es `--demoProfileLdap-- - Demo System (DD/MM/YYYY) (Edge)`. A continuación, seleccione **Desarrollo** under **Entorno**. Haga clic en **Guardar**.

![WebSDK](./images/websdk4.png)

El conjunto de datos se ha actualizado y está listo para su uso.

![WebSDK](./images/websdk8a.png)

El conjunto de datos ya está listo para trabajar con su **[!DNL Event Forwarding property]**.

Paso siguiente: [14.3 Crear y configurar un vínculo web personalizado](./ex3.md)

[Volver al módulo 14](./aep-data-collection-ssf.md)

[Volver a todos los módulos](./../../overview.md)
