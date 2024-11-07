---
title: Foundation - Perfil del cliente en tiempo real - Visualice su propio perfil del cliente en tiempo real - IU
description: Foundation - Perfil del cliente en tiempo real - Visualice su propio perfil del cliente en tiempo real - IU
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 1%

---

# 2.1.2 Visualizar su propio perfil del cliente en tiempo real: interfaz de usuario

En este ejercicio, iniciará sesión en Adobe Experience Platform y verá su propio perfil de cliente en tiempo real en la interfaz de usuario.

## Historia

En el Perfil del cliente en tiempo real, todos los datos de perfil se muestran junto con los datos de evento, así como las suscripciones a segmentos existentes. Los datos mostrados pueden proceder de cualquier lugar, de aplicaciones de Adobe y soluciones externas. Esta es la vista más potente de Adobe Experience Platform, el verdadero sistema de registro de experiencias.

## 2.1.2.1 Uso de la vista de perfil del cliente en Adobe Experience Platform

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](../../datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar la [!UICONTROL zona protegida] adecuada, verá el cambio en la pantalla y ahora se encuentra en la [!UICONTROL zona protegida] dedicada.

![Ingesta de datos](../../datacollection/module1.2/images/sb1.png)

En el menú de la izquierda, ve a **Perfiles** y a **Examinar**.

![Perfil del cliente](./images/homemenu.png)

En el panel Visor de perfiles del sitio web, puede encontrar varias identidades. Cada identidad está vinculada a un área de nombres.

![Perfil del cliente](./images/identities.png)

En el panel Visor de perfiles, puede ver estas combinaciones de ID y áreas de nombres:

| Identidad | Área de nombres |
|:-------------:| :---------------:|
| ID DEL Experience Cloud (ECID) | 12507560687324495704459439363261812234 |
| ID de correo electrónico | woutervangeluwe+06022022-01@gmail.com |
| Identificador de número de móvil | +32473622044+06022022-01 |

Con Adobe Experience Platform, todos los ID son igualmente importantes. Anteriormente, el ECID era el ID más importante en el contexto de Adobe y todos los demás ID estaban vinculados al ECID en una relación jerárquica. Con Adobe Experience Platform, este ya no es el caso, y cada ID puede considerarse un identificador principal.

Normalmente, el identificador principal depende del contexto. Si le pregunta a su centro de llamadas, **¿Cuál es el ID más importante?** es probable que respondan, **el número de teléfono!** Pero si le pregunta a su equipo de CRM, responderán: **La dirección de correo electrónico!** Adobe Experience Platform comprende esta complejidad y la administra por usted. Cada aplicación, ya sea de Adobe o de no Adobe, hablará con Adobe Experience Platform haciendo referencia al ID que consideran principal. Y simplemente funciona.

Para el campo **Área de nombres de identidad**, seleccione **Correo electrónico** y para el campo **Valor de identidad**, escriba la dirección de correo electrónico que utilizó para registrarse en el ejercicio anterior. Haga clic en **Ver**. A continuación, verá su perfil en la lista. Haga clic en **ID de perfil** para abrir el perfil.

![Perfil del cliente](./images/popupecid.png)

Ahora verá una descripción general de un par de **Atributos de perfil** importantes de su perfil de cliente.

![Perfil del cliente](./images/profile.png)

Si desea ver todos los atributos de perfil disponibles para su perfil, vaya a **Atributos**.

![Perfil del cliente](./images/profilattr.png)

Vaya a **Eventos**, donde podrá ver las entradas de todos los eventos de experiencia vinculados a su perfil.

![Perfil del cliente](./images/profileee.png)

Finalmente, vaya a la opción de menú **Abono a segmentos**. Ahora verá todos los segmentos que cumplen los requisitos para este perfil.

![Perfil del cliente](./images/profileseg.png)

Ahora que ha aprendido a ver el perfil en tiempo real de cualquier cliente utilizando la interfaz de usuario de Adobe Experience Platform, hagamos lo mismo a través de las API utilizando Postman y el Adobe I/O para consultar las API de Adobe Experience Platform.

Siguiente paso: [2.1.3 Visualice su propio perfil de cliente en tiempo real: API](./ex3.md)

[Volver al módulo 2.1](./real-time-customer-profile.md)

[Volver a todos los módulos](../../../overview.md)
