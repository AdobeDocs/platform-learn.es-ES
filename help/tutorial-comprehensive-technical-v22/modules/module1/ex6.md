---
title: 'Fundamento: Configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: Implementación de Adobe Target'
description: 'Fundamento: Configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: Implementación de Adobe Target'
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 4aee8ae2-38ca-49a3-8f1b-57713d16f5b5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 1.6 Implementar Adobe Target

## 1.6. Actualice el almacén de datos para utilizar Adobe Target

Si desea enviar datos recopilados por el SDK web a Adobe Target y obtener una respuesta de Adobe Target con una experiencia personalizada para cada cliente, siga estos pasos.

Vaya a [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) y vaya a **Datastreams**.

En la esquina superior derecha de la pantalla, seleccione el nombre del simulador de pruebas, que debería ser `--aepSandboxId--`. Abra el conjunto de datos específico, que lleva el nombre `--demoProfileLdap-- - Demo System Datastream`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

Entonces verás esto. Para habilitar Adobe Target, haga clic en **+Añadir servicio**.

![AEP Debugger](./images/aa2.png)

Entonces verás esto. Seleccione el servicio **Adobe Target**, después de lo cual puede proporcionar información adicional de forma opcional. En este momento, no es necesario guardar esto, así que haga clic en **Cancelar**.

![AEP Debugger](./images/at1.png)

Paso siguiente: [Requisitos del esquema XDM 1.7 en Adobe Experience Platform](./ex7.md)

[Volver al módulo 1](./data-ingestion-launch-web-sdk.md)

[Volver a todos los módulos](./../../overview.md)
