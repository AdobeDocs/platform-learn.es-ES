---
title: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión de Web SDK: requisitos de esquema XDM en Adobe Experience Platform'
description: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión de Web SDK: requisitos de esquema XDM en Adobe Experience Platform'
kt: 5342
doc-type: tutorial
exl-id: 3fc4a1d6-4130-464e-98c0-5b9cac8051a0
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 1.1.7 Requisitos de esquema XDM en Adobe Experience Platform

Para garantizar que Web SDK pueda introducir datos en Adobe Experience Platform, se necesita que una mezcla XDM específica forme parte del esquema XDM en Adobe Experience Platform.

Vaya a [https://experience.adobe.com/platform](https://experience.adobe.com/platform) e inicie sesión.

![Depurador de AEP](./images/exp1.png)

Después de iniciar sesión, selecciona la zona protegida adecuada haciendo clic en el texto **Producción** en la línea azul de la parte superior de la pantalla. Seleccione la zona protegida `--aepSandboxName--`.

Después de seleccionar la zona protegida, verá que la pantalla cambia y ahora está en ella.

![Depurador de AEP](./images/exp2.png)

En el menú de la izquierda, vaya a **Esquemas** y abra el esquema **Sistema de demostración: esquema de eventos para el sitio web (Global v1.1)**.

![Depurador de AEP](./images/exp3.png)

En ese esquema, verá que se ha agregado el grupo de campos **AEP Web SDK ExperienceEvent**. Este grupo de campos añade todos los campos mínimos requeridos al esquema. Cada esquema de evento de experiencia de Adobe Experience Platform que Web SDK utilizará siempre requerirá que ese grupo de campos forme parte del esquema.

![Depurador de AEP](./images/exp4.png)

En [Módulo 1.2](./../module1.2/data-ingestion.md) aprenderá a agregar grupos de campos a los esquemas.

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 1.1](./data-ingestion-launch-web-sdk.md)

[Volver a todos los módulos](./../../../overview.md)
