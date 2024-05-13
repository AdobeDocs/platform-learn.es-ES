---
title: Bootcamp - Perfil del cliente en tiempo real - Visualice su propio perfil del cliente en tiempo real - IU
description: Bootcamp - Perfil del cliente en tiempo real - Visualice su propio perfil del cliente en tiempo real - IU
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 1.2 Visualice su propio perfil de cliente en tiempo real: interfaz de usuario

En este ejercicio, iniciará sesión en Adobe Experience Platform y verá su propio perfil de cliente en tiempo real en la interfaz de usuario.

## Historia

En el Perfil del cliente en tiempo real, todos los datos de perfil se muestran junto con los datos de evento, así como las suscripciones a audiencias existentes. Los datos mostrados pueden proceder de cualquier lugar, de aplicaciones de Adobe y soluciones externas. Esta es la vista más potente de Adobe Experience Platform, el verdadero sistema de registro de experiencias.

## 1.2.1 Uso de la vista de perfil del cliente en Adobe Experience Platform

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar un **espacio aislado**. La zona protegida que se va a seleccionar se denomina ``Bootcamp``. Para ello, haga clic en el texto **[!UICONTROL Producción de producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar las [!UICONTROL espacio aislado], verá el cambio de pantalla y ahora estará en su dedicado [!UICONTROL espacio aislado].



En el menú de la izquierda, vaya a **Perfiles** y a **Examinar**.

![Perfil del cliente](./images/homemenu.png)

En el panel Visualizador de perfiles del sitio web, puede encontrar la descripción general de la identidad. Cada identidad está vinculada a un área de nombres.

![Perfil del cliente](./images/identities.png)




Con Adobe Experience Platform, todos los ID son igualmente importantes. Anteriormente, el ECID era el ID más importante en el contexto de Adobe y todos los demás ID estaban vinculados al ECID en una relación jerárquica. Con Adobe Experience Platform, este ya no es el caso, y cada ID puede considerarse un identificador principal.

Normalmente, el identificador principal depende del contexto. Si le pregunta a su centro de llamadas, **¿Cuál es el ID más importante?** probablemente responderán, **¡el número de teléfono!** Pero si le preguntas a tu equipo de CRM, ellos responderán, **La dirección de correo electrónico**  Adobe Experience Platform comprende esta complejidad y la administra por usted. Cada aplicación, ya sea de Adobe o de no Adobe, hablará con Adobe Experience Platform haciendo referencia al ID que consideran principal. Y simplemente funciona.

Para el campo **Área de nombres de identidad**, seleccione **ECID** y para el campo **Valor de identidad** introduzca el ECID que se puede encontrar en el panel Visor de perfiles del sitio web de bootcamp. Clic **Ver**. A continuación, verá su perfil en la lista. Haga clic en **ID de perfil** para abrir el perfil.

![Perfil del cliente](./images/popupecid.png)

Ahora verá una descripción general de un par de **Atributos de perfil** del perfil de cliente.

![Perfil del cliente](./images/profile.png)

Ir a **Eventos**, donde puede ver las entradas de cada evento de experiencia vinculado a su perfil.

![Perfil del cliente](./images/profileee.png)

Finalmente, vaya a la opción de menú **Abono a audiencia**. Ahora verá todas las audiencias que cumplen los requisitos para este perfil.

![Perfil del cliente](./images/profileseg.png)

Ahora vamos a crear una nueva audiencia que le permitirá personalizar la experiencia del cliente para un cliente anónimo o conocido.

Paso siguiente: [1.3 Crear una audiencia: IU](./ex3.md)

[Volver al flujo de usuario 1](./uc1.md)

[Volver a todos los módulos](../../overview.md)
