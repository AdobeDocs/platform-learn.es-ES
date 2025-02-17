---
title: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión de Web SDK: implementación de Adobe Target'
description: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión de Web SDK: implementación de Adobe Target'
kt: 5342
doc-type: tutorial
exl-id: 31cdde2f-011d-442d-8e47-15a318a6c89d
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 2%

---

# 1.1.6 Implementación de Adobe Target

## Actualice el flujo de datos para utilizar Adobe Target

Si desea enviar datos recopilados por Web SDK a Adobe Target y obtener una respuesta de Adobe Target con una experiencia personalizada para cada cliente, siga estos pasos.

Vaya a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) y luego a **Datastreams**.

En la esquina superior derecha de la pantalla, seleccione el nombre de la zona protegida, que debe ser `--aepSandboxName--`. Abra la secuencia de datos específica, que se llama `--aepUserLdap-- - Demo System Datastream`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

Entonces verá esto... Para habilitar Adobe Target, haga clic en **Agregar servicio**.

![Depurador de AEP](./images/aa2.png)

Entonces verá esto... Seleccione el servicio **Adobe Target**, después del cual puede proporcionar información adicional de forma opcional. Haga clic en **Guardar**.

![Depurador de AEP](./images/at1.png)

## Pasos siguientes

Ir a [1.1.7 Requisitos de esquema XDM en Adobe Experience Platform](./ex7.md){target="_blank"}

Volver a la [configuración de la recopilación de datos de Adobe Experience Platform y la extensión de etiquetas de Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
