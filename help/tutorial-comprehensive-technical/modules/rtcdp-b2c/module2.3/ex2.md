---
title: 'Real-time CDP: cree una audiencia y tome medidas . Configure un destino de Advertising como Google DV360'
description: 'Real-time CDP: cree una audiencia y tome medidas . Configure un destino de Advertising como Google DV360'
kt: 5342
doc-type: tutorial
exl-id: fdc590d5-b986-422c-97ef-b5a439644439
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 1%

---

# 2.3.2 Configuración de un destino de Advertising como Google DV360

>[!IMPORTANT]
>
>El siguiente contenido está parcialmente diseñado para su información - Si ese destino ya existe en su instancia, entonces **NO** tiene que configurar un nuevo destino para DV360. El destino ya se ha creado en ese caso y puede utilizarlo en el siguiente ejercicio.

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la [!UICONTROL zona protegida] adecuada, verá el cambio en la pantalla y ahora se encuentra en la [!UICONTROL zona protegida] dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

En el menú de la izquierda, ve a **Destinos** y luego ve a **Catálogo**. Verá el **Catálogo de destinos**.

![RTCDP](./images/rtcdp.png)

En **Destinos**, haz clic en **Google Display &amp; Video 360** y luego haz clic en **+ Configurar**.

![RTCDP](./images/rtcdpgoogle.png)

Entonces verá esto... Haga clic en **Conectar con destino**.

![RTCDP](./images/rtcdpgooglecreate1.png)

En la siguiente pantalla, puede configurar el destino en Google DV360.

![RTCDP](./images/rtcdpgooglecreatedest.png)

Escriba un valor en los campos **Nombre** y **Descripción**.

El campo **ID de cuenta** es el **ID de anunciante** de la cuenta DV360. Puede encontrar lo siguiente:

![RTCDP](./images/rtcdpgoogledv360advid.png)

El **tipo de cuenta** debe establecerse en **Anunciante invitado**.

Ahora tienes esto. Haga clic en **Next**.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google necesita un Adobe de lista de permitidos para que Adobe Experience Platform envíe datos a Google DV360. Póngase en contacto con el administrador de cuentas de Google para habilitar este flujo de datos.

Después de crear el destino, verá esto. Si lo desea, puede seleccionar una política de control de datos. A continuación, haga clic en **Guardar y salir**.

![RTCDP](./images/rtcdpcreatedest1.png)

A continuación, verá una lista de destinos disponibles.
En el siguiente ejercicio, conectará la audiencia que creó en el ejercicio anterior al destino de Google DV360.

Siguiente paso: [2.3.3 Realizar acción: enviar la audiencia a DV360](./ex3.md)

[Volver al módulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Volver a todos los módulos](../../../overview.md)
