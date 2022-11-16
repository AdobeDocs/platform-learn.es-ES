---
title: Foundation - Perfil del cliente en tiempo real - Visualice su propio perfil del cliente en tiempo real - IU
description: Foundation - Perfil del cliente en tiempo real - Visualice su propio perfil del cliente en tiempo real - IU
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: ed13e37f-48eb-4668-b828-6c58340a7cc1
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 2%

---

# 3.2 Visualizar su propio perfil del cliente en tiempo real: IU

En este ejercicio, iniciará sesión en Adobe Experience Platform y verá su propio perfil de cliente en tiempo real en la interfaz de usuario.

## Historia

En el Perfil del cliente en tiempo real, todos los datos de perfil se muestran junto con los datos de evento, así como las suscripciones a segmentos existentes. Los datos mostrados pueden provenir de cualquier lugar, desde aplicaciones de Adobe y soluciones externas. Esta es la vista más poderosa de Adobe Experience Platform, el verdadero sistema de registro de experiencias.

## 3.2.1 Uso de la vista de perfil del cliente en Adobe Experience Platform

Vaya a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](../module2/images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``--aepSandboxId--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar los elementos adecuados [!UICONTROL entorno limitado], verá el cambio de pantalla y ahora estará en su [!UICONTROL entorno limitado].

![Ingesta de datos](../module2/images/sb1.png)

En el menú de la izquierda, vaya a **Perfiles** y **Examinar**.

![Perfil del cliente](./images/homemenu.png)

En el panel Visor de perfiles de su sitio web, puede encontrar varias identidades. Cada identidad está vinculada a un área de nombres.

![Perfil del cliente](./images/identities.png)

En el panel Visor de perfiles, puede ver estas combinaciones de ID y espacios de nombres:

| Identidad | Área de nombres |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 12507560687324495704459439363261812234 |
| ID de correo electrónico | woutervangeluwe+06022022-01@gmail.com |
| ID de número de móvil | +32473622044+06022022-01 |

Con Adobe Experience Platform, todos los ID son igualmente importantes. Anteriormente, el ECID era el ID más importante en el contexto de Adobe y todos los demás ID estaban vinculados al ECID en una relación jerárquica. Con Adobe Experience Platform, este ya no es el caso y cada ID se puede considerar un identificador principal.

Normalmente, el identificador principal depende del contexto. Si consulta con su centro de llamadas, **¿Cuál es el ID más importante?** probablemente responderán, **el número de teléfono!** Pero si le pregunta a su equipo de CRM, responderán, **¡La dirección de correo electrónico!**  Adobe Experience Platform comprende esta complejidad y la gestiona por usted. Cada aplicación, ya sea de Adobe o de Adobe, hablará con Adobe Experience Platform haciendo referencia al ID que consideran principal. Y simplemente funciona.

Para el campo **Área de nombres de identidad**, seleccione **Correo electrónico** y para el campo **Valor de identidad** introduzca la dirección de correo electrónico que utilizó para registrarse en el ejercicio anterior. Haga clic en **Ver**. A continuación, verá su perfil en la lista. Haga clic en el **ID de perfil** para abrir el perfil.

![Perfil del cliente](./images/popupecid.png)

Ahora verá una descripción general de un par de importantes **Atributos de perfil** de su perfil de cliente.

![Perfil del cliente](./images/profile.png)

Si desea ver todos los atributos de perfil disponibles para su perfil, vaya a **Atributos**.

![Perfil del cliente](./images/profilattr.png)

Vaya a **Eventos**, donde puede ver entradas para cada evento de experiencia vinculado a su perfil.

![Perfil del cliente](./images/profileee.png)

Finalmente, vaya a la opción de menú **Pertenencia a segmentos**. Ahora verá todos los segmentos que cumplen los requisitos para este perfil.

![Perfil del cliente](./images/profileseg.png)

Ahora que ha aprendido a ver el perfil en tiempo real de cualquier cliente utilizando la interfaz de usuario de Adobe Experience Platform, hagamos lo mismo a través de las API mediante Postman y Adobe I/O para realizar consultas con las API de Adobe Experience Platform.

Paso siguiente: [3.3 Visualizar su propio perfil de cliente en tiempo real: API](./ex3.md)

[Volver al módulo 3](./real-time-customer-profile.md)

[Volver a todos los módulos](../../overview.md)
