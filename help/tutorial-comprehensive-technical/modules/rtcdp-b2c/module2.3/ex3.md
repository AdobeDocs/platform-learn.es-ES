---
title: 'Real-time CDP: cree un segmento y tome medidas . Envíe su segmento a DV360'
description: 'Real-time CDP: cree un segmento y tome medidas . Envíe su segmento a DV360'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 2%

---

# 2.3.3 Tomar acción: enviar el segmento a DV360

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar la [!UICONTROL zona protegida] adecuada, verá el cambio en la pantalla y ahora se encuentra en la [!UICONTROL zona protegida] dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

En el menú de la izquierda, ve a **Destinos** y luego ve a **Catálogo**. Verá el **Catálogo de destinos**.

![RTCDP](./images/rtcdpmenudest.png)

En **Destinos**, haga clic en **Activar segmentos** en la tarjeta **Google Display &amp; Video 360**.

![RTCDP](./images/rtcdpgoogleseg.png)

Seleccione su destino y haga clic en **Siguiente**.

![RTCDP](./images/rtcdpcreatedest2.png)

En la lista de segmentos disponibles, seleccione el segmento que creó en el ejercicio anterior. Haga clic en **Next**.

![RTCDP](./images/rtcdpcreatedest3.png)

En la página **Programación de segmentos**, haga clic en **Siguiente**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por último, en la página **Revisar**, haga clic en **Finalizar**.

![RTCDP](./images/rtcdpcreatedest5.png)

El segmento ahora está vinculado a Google DV360. Cada vez que un cliente se incluye en este segmento, se envía una señal a Google DV360 para incluir al cliente en la audiencia de Google DV360.

Paso siguiente: [2.3.4 Tomar medidas: enviar el segmento a un destino S3](./ex4.md)

[Volver al módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Volver a todos los módulos](../../../overview.md)
