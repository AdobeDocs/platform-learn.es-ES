---
title: Bootcamp - Real-time CDP - Cree una audiencia y tome medidas - Envíe su audiencia a DV360
description: Bootcamp - Real-time CDP - Cree una audiencia y tome acción - Envíe su audiencia a DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5 Tomar medidas: enviar la audiencia a Facebook

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``Bootcamp``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar la [!UICONTROL zona protegida] adecuada, verá el cambio en la pantalla y ahora se encuentra en la [!UICONTROL zona protegida] dedicada.

![Ingesta de datos](./images/sb1.png)

En el menú de la izquierda, ve a **Destinos** y luego ve a **Catálogo**. Verá el **Catálogo de destinos**. En **Destinos**, haga clic en **Activar audiencias** en la tarjeta **Audiencia personalizada de Facebook**.

![RTCDP](./images/rtcdpgoogleseg.png)

Seleccione el destino **bootcamp-facebook** y haga clic en **Siguiente**.

![RTCDP](./images/rtcdpcreatedest2.png)

En la lista de audiencias disponibles, seleccione la audiencia que creó en el ejercicio anterior. Haga clic en **Next**.

![RTCDP](./images/rtcdpcreatedest3.png)

En la página **Asignación**, asegúrese de que la casilla de verificación **Aplicar transformación** esté habilitada. Haga clic en **Next**.

![RTCDP](./images/rtcdpcreatedest4a.png)

En la página **Programación de audiencias**, seleccione **Origen de su audiencia** y configúrelo en **Directamente de los clientes**. Haga clic en **Next**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por último, en la página **Revisar**, haga clic en **Finalizar**.

![RTCDP](./images/rtcdpcreatedest5.png)

La audiencia ahora está vinculada a Audiencias personalizadas de Facebook. Cada vez que un cliente se califica para esta audiencia, se enviará una señal al lado del servidor de Facebook para incluir a ese cliente en la audiencia personalizada en el lado del Facebook.

En Facebook, encontrará la audiencia de Adobe Experience Platform en Audiencias personalizadas :

![RTCDP](./images/rtcdpcreatedest5b.png)

Ahora puede ver su audiencia personalizada en Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Volver al flujo de usuario 1](./uc1.md)

[Volver a todos los módulos](../../overview.md)
