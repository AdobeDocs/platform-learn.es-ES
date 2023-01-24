---
title: Bootcamp - Perfil del cliente en tiempo real - Visualice su propio Perfil del cliente en tiempo real - IU - Brasil
description: Bootcamp - Perfil del cliente en tiempo real - Visualice su propio Perfil del cliente en tiempo real - IU - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# 1.2 Visualizar su propio perfil del cliente en tiempo real: IU

En este ejercicio, iniciará sesión en Adobe Experience Platform y verá su propio perfil de cliente en tiempo real en la interfaz de usuario.

## Historia

En el Perfil del cliente en tiempo real, todos los datos de perfil se muestran junto con los datos de evento, así como las suscripciones a segmentos existentes. Los datos mostrados pueden provenir de cualquier lugar, desde aplicaciones de Adobe y soluciones externas. Esta es la vista más poderosa de Adobe Experience Platform, el verdadero sistema de registro de experiencias.

## 1.2.1 Uso de la vista de perfil del cliente en Adobe Experience Platform

Vaya a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``Bootcamp``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar los elementos adecuados [!UICONTROL entorno limitado], verá el cambio de pantalla y ahora estará en su [!UICONTROL entorno limitado].

![Ingesta de datos](./images/sb1.png)

En el menú de la izquierda, vaya a **Perfiles** y **Examinar**.

![Perfil del cliente](./images/homemenu.png)

En el panel Visor de perfiles de su sitio web, puede encontrar la descripción general de la identidad. Cada identidad está vinculada a un área de nombres.

![Perfil del cliente](./images/identities.png)

En el panel Visor de perfiles, actualmente puede ver esta identidad:

| Área de nombres | Identidad |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

Con Adobe Experience Platform, todos los ID son igualmente importantes. Anteriormente, el ECID era el ID más importante en el contexto de Adobe y todos los demás ID estaban vinculados al ECID en una relación jerárquica. Con Adobe Experience Platform, este ya no es el caso y cada ID se puede considerar un identificador principal.

Normalmente, el identificador principal depende del contexto. Si consulta con su centro de llamadas, **¿Cuál es el ID más importante?** probablemente responderán, **el número de teléfono!** Pero si le pregunta a su equipo de CRM, responderán, **¡La dirección de correo electrónico!**  Adobe Experience Platform comprende esta complejidad y la gestiona por usted. Cada aplicación, ya sea de Adobe o de Adobe, hablará con Adobe Experience Platform haciendo referencia al ID que consideran principal. Y simplemente funciona.

Para el campo **Área de nombres de identidad**, seleccione **ECID** y para el campo **Valor de identidad** introduzca el ECID que puede encontrar en el panel Visor de perfiles del sitio web de bootcamp. Haga clic en **Ver**. A continuación, verá su perfil en la lista. Haga clic en el **ID de perfil** para abrir el perfil.

![Perfil del cliente](./images/popupecid.png)

Ahora verá una descripción general de un par de importantes **Atributos de perfil** de su perfil de cliente.

![Perfil del cliente](./images/profile.png)

Vaya a **Eventos**, donde puede ver entradas para cada evento de experiencia vinculado a su perfil.

![Perfil del cliente](./images/profileee.png)

Finalmente, vaya a la opción de menú **Pertenencia a segmentos**. Ahora verá todos los segmentos que cumplen los requisitos para este perfil.

![Perfil del cliente](./images/profileseg.png)

Ahora vamos a crear un nuevo segmento que le permitirá personalizar la experiencia del cliente para un cliente anónimo o conocido.

Paso siguiente: [1.3 Crear un segmento: IU](./ex3.md)

[Volver al flujo de usuario 1](./uc1.md)

[Volver a todos los módulos](../../overview.md)
