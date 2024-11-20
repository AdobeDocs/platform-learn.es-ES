---
title: 'Real-time CDP: cree una audiencia y tome medidas . Envíe su audiencia a DV360'
description: 'Real-time CDP: cree una audiencia y tome medidas . Envíe su audiencia a DV360'
kt: 5342
doc-type: tutorial
exl-id: bb76524e-52c1-4c2c-8bcd-33cd39d12741
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# 2.3.3 Tomar acción: enviar a su audiencia a DV360

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la [!UICONTROL zona protegida] adecuada, verá el cambio en la pantalla y ahora se encuentra en la [!UICONTROL zona protegida] dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

En el menú de la izquierda, ve a **Destinos** y luego a **Examinar**. Verá el destino **DV360**. Haga clic en los 3 puntos **...** y luego haga clic en **Activar audiencias**.

![RTCDP](./images/rtcdpmenudest.png)

En la lista de audiencias disponibles, seleccione la audiencia que creó en el ejercicio anterior. Haga clic en **Next**.

![RTCDP](./images/rtcdpcreatedest3.png)

En la página **Programación de audiencias**, haga clic en **Siguiente**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por último, en la página **Revisar**, haga clic en **Finalizar**.

![RTCDP](./images/rtcdpcreatedest5.png)

La audiencia ahora está vinculada a Google DV360. Cada vez que un cliente se incluye en esta audiencia, se envía una señal a Google DV360 para incluir al cliente en la audiencia de Google DV360.

Paso siguiente: [2.3.4 Realizar acción: enviar la audiencia a un S3-destination](./ex4.md)

[Volver al módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Volver a todos los módulos](../../../overview.md)
