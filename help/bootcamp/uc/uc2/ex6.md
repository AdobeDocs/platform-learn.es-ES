---
title: 'Bootcamp: personalización en el centro de llamadas'
description: 'Bootcamp: personalización en el centro de llamadas'
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: f7697673-38f9-41f6-ac4d-2561db2ece67
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 2.6 Personalización en el centro de llamadas

Como se ha mencionado varias veces durante el bootcamp, personalizar la experiencia del cliente es algo que debería suceder de una manera omnicanal. Un centro de llamadas a menudo está bastante desconectado del resto del recorrido del cliente y eso a menudo conduce a experiencias frustrantes del cliente, pero no es necesario. Veamos un ejemplo de cómo el centro de llamadas se puede conectar fácilmente a Adobe Experience Platform, en tiempo real.

## Flujo de Recorrido del cliente

En el ejercicio anterior, utilizando la aplicación móvil, compró un producto haciendo clic en **Buy** botón.

![DSN](./images/app20.png)

Supongamos que tiene una pregunta sobre el estado de su pedido, ¿qué haría? Normalmente, llamaría al centro de llamadas.

Antes de llamar al centro de llamadas, debe saber su **ID de fidelización**. Puede encontrar su ID de fidelización en el Visor de perfiles del sitio web.

![DSN](./images/cc1.png)

En este caso, la variable **ID de fidelización** es **5863105**. Como parte de la implementación personalizada de la función de centro de llamadas en el entorno de demostración, debe agregar un prefijo a la **ID de fidelización**. El prefijo es **11373**, por lo que el ID de fidelización que se utilizará en este ejemplo es **11373 5863105**.

Vamos a hacer eso ahora. Usa tu teléfono y llama al número **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Se le pedirá que introduzca su ID de fidelización, seguido de **#**. Introduzca su ID de fidelización.

![DSN](./images/cc3.png)

Entonces vas a escuchar **Hola, nombre**. Ese nombre se toma del Perfil del cliente en tiempo real en Adobe Experience Platform. A continuación, tiene 3 opciones. Número de prensa **1**, **Estado del pedido**.

![DSN](./images/cc4.png)

Después de escuchar el estado de su pedido, se le dará la opción de presionar **1** para volver al menú principal o, de lo contrario, pulse 2. Prensa **2**.

![DSN](./images/cc5.png)

Luego se le pedirá que clasifique su experiencia con el centro de llamadas, seleccionando un número entre 1 y 5, siendo 1 bajo y 5 alto. Haga su elección.

![DSN](./images/cc6.png)

La llamada al centro de llamadas finalizará ahora.

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar un **espacio aislado**. La zona protegida que se va a seleccionar se denomina ``Bootcamp``. Para ello, haga clic en el texto **[!UICONTROL Producción de producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar las [!UICONTROL espacio aislado], verá el cambio de pantalla y ahora estará en su dedicado [!UICONTROL espacio aislado].

![Ingesta de datos](./images/sb1.png)

En el menú de la izquierda, vaya a **Perfiles** y a **Examinar**.

![Perfil del cliente](./images/homemenu.png)

Seleccione el **Área de nombres de identidad** **Correo electrónico** e introduzca la dirección de correo electrónico del perfil de cliente. Clic **Ver**. Haga clic en para abrir el perfil.

![DSN](./images/cc7.png)

Volverá a ver el perfil de cliente. Ir a **Eventos**.

![DSN](./images/cc8.png)

En eventos, verá 2 eventos con un eventType de **callCenter**. El primer evento es el resultado de su respuesta a la pregunta **Valore la satisfacción de la llamada**.

![DSN](./images/cc9.png)

Desplácese un poco hacia abajo y verá el evento que se grabó al seleccionar la opción para comprobar su **Estado del pedido**.

![DSN](./images/cc10.png)

Ir a **Abono de segmentos**. Ahora verá que dos segmentos cumplen los requisitos en su perfil, en tiempo real, según las interacciones que tuvo a través del centro de llamadas. Estas suscripciones a segmentos pueden y deben utilizarse para influir en la comunicación y personalización que se produce en cualquier otro canal.

![DSN](./images/cc11.png)

Ya ha terminado este ejercicio.

[Volver al flujo de usuario 2](./uc2.md)

[Volver a todos los módulos](../../overview.md)
