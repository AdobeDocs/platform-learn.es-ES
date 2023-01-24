---
title: Bootcamp - Personalización en el centro de llamadas - Brasil
description: Bootcamp - Personalización en el centro de llamadas - Brasil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# 2.6 Personalización en el centro de llamadas

Como ya se ha comentado varias veces durante el bootcamp, la personalización de la experiencia del cliente es algo que debería suceder de forma omnicanal. Un centro de llamadas suele estar bastante desconectado del resto del recorrido del cliente y a menudo provoca experiencias frustrantes para el cliente, pero no es necesario. Veamos un ejemplo de cómo el centro de llamadas puede conectarse fácilmente a Adobe Experience Platform en tiempo real.

## Flujo de Recorrido del cliente

En el ejercicio anterior, con la aplicación móvil, compró un producto haciendo clic en el botón **Buy** botón.

![DSN](./images/app20.png)

Supongamos que tiene una pregunta sobre el estado de su orden, ¿qué haría? Normalmente, llamaría al centro de llamadas.

Antes de llamar al centro de llamadas, debe conocer su **ID de fidelidad**. Puede encontrar su ID de fidelidad en el visor de perfiles del sitio web.

![DSN](./images/cc1.png)

En este caso, la variable **ID de fidelidad** es **5863105**. Como parte de nuestra implementación personalizada de la función del centro de llamadas en el entorno de demostración, debe añadir un prefijo a su **ID de fidelidad**. El prefijo es **11373**, por lo que el ID de fidelidad que se debe utilizar en este ejemplo es **11373 5863105**.

Hagámoslo ahora. Usa tu teléfono y llama al número **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Se le pedirá que introduzca su ID de fidelidad, seguido de **#**. Introduzca su ID de fidelidad.

![DSN](./images/cc3.png)

Entonces oirás **Hola, nombre**. Ese nombre se toma del Perfil del cliente en tiempo real en Adobe Experience Platform. A continuación, tiene tres opciones. Número de prensa **1**, **Estado del pedido**.

![DSN](./images/cc4.png)

Después de escuchar su estado de pedido, se le dará la opción de presionar **1** para volver al menú principal o, de lo contrario, pulse 2. Press **2**.

![DSN](./images/cc5.png)

A continuación, se le pedirá que clasifique la experiencia del centro de llamadas seleccionando un número entre 1 y 5, siendo 1 baja y 5 alta. Haz tu elección.

![DSN](./images/cc6.png)

La llamada al centro de llamadas finalizará ahora.

Vaya a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``Bootcamp``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar los elementos adecuados [!UICONTROL entorno limitado], verá el cambio de pantalla y ahora estará en su [!UICONTROL entorno limitado].

![Ingesta de datos](./images/sb1.png)

En el menú de la izquierda, vaya a **Perfiles** y **Examinar**.

![Perfil del cliente](./images/homemenu.png)

Seleccione el **Área de nombres de identidad** **Correo electrónico** e introduzca la dirección de correo electrónico de su perfil de cliente. Haga clic en **Ver**. Haga clic en para abrir el perfil.

![DSN](./images/cc7.png)

Volverá a ver el perfil del cliente. Vaya a **Eventos**.

![DSN](./images/cc8.png)

En events (eventos), verá 2 eventos con un eventType de **callCenter**. El primer evento es el resultado de la respuesta a la pregunta **Valore la satisfacción de las llamadas**.

![DSN](./images/cc9.png)

Desplácese hacia abajo un poco y verá el evento que se registró cuando seleccionó la opción para comprobar **Estado del pedido**.

![DSN](./images/cc10.png)

Vaya a **Pertenencia a segmentos**. Ahora verá que 2 segmentos cumplen los requisitos en su perfil, en tiempo real, en función de las interacciones que tuvo a través del centro de llamadas. Estas suscripciones a segmentos pueden y deben utilizarse para afectar a la comunicación y personalización que se produce en cualquier otro canal.

![DSN](./images/cc11.png)

Ya has terminado este ejercicio.

[Volver al flujo de usuario 2](./uc2.md)

[Volver a todos los módulos](../../overview.md)
