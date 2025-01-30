---
title: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión de Web SDK: implementación de Adobe Target'
description: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión de Web SDK: implementación de Adobe Target'
kt: 5342
doc-type: tutorial
exl-id: 475e9a34-c80e-41e4-9660-61c79f26922d
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

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

Paso siguiente: [1.1.7 Requisitos de esquema XDM en Adobe Experience Platform](./ex7.md)

[Volver al módulo 1.1](./data-ingestion-launch-web-sdk.md)

[Volver a todos los módulos](./../../../overview.md)
