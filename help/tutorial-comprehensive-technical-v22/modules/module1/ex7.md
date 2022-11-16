---
title: 'Base: Configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: requisitos del esquema XDM en Adobe Experience Platform'
description: 'Base: Configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: requisitos del esquema XDM en Adobe Experience Platform'
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 8e17129c-633d-45bd-aa70-78cc3d3a2108
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Requisitos del esquema XDM 1.7 en Adobe Experience Platform

Para garantizar que el SDK web y alloy.js puedan introducir datos en Adobe Experience Platform, es necesario que una mezcla XDM específica forme parte del esquema XDM en Adobe Experience Platform.

Vaya a [https://experience.adobe.com/platform](https://experience.adobe.com/platform) e inicie sesión.

![AEP Debugger](./images/exp1.png)

Después de iniciar sesión, seleccione el simulador para pruebas correspondiente haciendo clic en el texto **Producción** en la línea azul de la parte superior de la pantalla. Seleccione el entorno limitado `--aepSandboxId--`.

Después de seleccionar el simulador para pruebas, verá el cambio de pantalla y ahora estará en el simulador para pruebas.

![AEP Debugger](./images/exp2.png)

En el menú de la izquierda, vaya a **Esquemas** y abra el **Sistema de demostración: Esquema de eventos para sitio web (Global v1.1)** Esquema.

![AEP Debugger](./images/exp3.png)

En ese esquema, verá que el grupo de campos **Mezcla de ExperienceEvent del SDK web de AEP** se ha añadido. Este grupo de campos agrega todos los campos mínimos requeridos al esquema. Todos los esquemas de eventos de experiencia de Adobe Experience Platform que utilice el SDK web siempre requerirán que ese grupo de campos forme parte del esquema.

![AEP Debugger](./images/exp4.png)

En [Módulo 2](./../module2/data-ingestion.md) aprenderá a añadir grupos de campos a esquemas.

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 1](./data-ingestion-launch-web-sdk.md)

[Volver a todos los módulos](./../../overview.md)
