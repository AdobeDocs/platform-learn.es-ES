---
title: 'CDP en tiempo real: genere un segmento y realice una acción: configure un destino publicitario como Google DV360'
description: 'CDP en tiempo real: genere un segmento y realice una acción: configure un destino publicitario como Google DV360'
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 40441815-428a-48dc-a12e-91220d4ba307
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 1%

---

# 6.2 Configurar un destino publicitario como Google DV360

>[!IMPORTANT]
>
>El siguiente contenido está diseñado como para su información personal: **NOT** tienen que configurar un nuevo destino para DV360. El destino ya se ha creado y puede utilizarlo en el siguiente ejercicio.

Vaya a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](../module2/images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``--aepSandboxId--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar los elementos adecuados [!UICONTROL entorno limitado], verá el cambio de pantalla y ahora estará en su [!UICONTROL entorno limitado].

![Ingesta de datos](../module2/images/sb1.png)

En el menú de la izquierda, vaya a **Destinos** y vaya a **Catálogo**. Verá el **Catálogo de destinos**.

![RTCDP](./images/rtcdp.png)

En **Destinos**, haga clic en **Pantalla y vídeo de Google 360** y haga clic en **+ Configurar**.

![RTCDP](./images/rtcdpgoogle.png)

Entonces verás esto. Haga clic en **Conectarse al destino**.

![RTCDP](./images/rtcdpgooglecreate1.png)

En la siguiente pantalla, puede configurar el destino a Google DV360.

![RTCDP](./images/rtcdpgooglecreatedest.png)

Introduzca un valor en los campos **Nombre** y **Descripción**.

El campo **ID de cuenta** es la variable **ID del anunciante** de la cuenta DV360. Puede encontrar esto aquí:

![RTCDP](./images/rtcdpgoogledv360advid.png)

La variable **Tipo de cuenta** debe configurarse como **Invitar anunciante**.

Ahora tienes esto. Haga clic en **Siguiente**.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google necesita incluir el Adobe en la lista de permitidos para que Adobe Experience Platform envíe datos a Google DV360. Póngase en contacto con el administrador de cuentas de Google para habilitar este flujo de datos.

Después de crear el destino, lo verá. Si lo desea, puede seleccionar una directiva de control de datos. A continuación, haga clic en **Guardar y salir**.

![RTCDP](./images/rtcdpcreatedest1.png)

A continuación, verá una lista de destinos disponibles.
En el siguiente ejercicio, conectará el segmento que haya creado en el ejercicio anterior al destino DV360 de Google.

Paso siguiente: [6.3 Acción: enviar el segmento a DV360](./ex3.md)

[Volver al módulo 6](./real-time-cdp-build-a-segment-take-action.md)

[Volver a todos los módulos](../../overview.md)
