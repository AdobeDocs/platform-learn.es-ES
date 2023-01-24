---
title: Bootcamp - Fusión física y digital - Utiliza la aplicación móvil y déclencheur una entrada de señalización - Brasil
description: Bootcamp - Fusión física y digital - Utiliza la aplicación móvil y déclencheur una entrada de señalización - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# 3.1 Uso de la aplicación móvil y déclencheur de una entrada de señalización

## Instalación de la aplicación móvil

Antes de instalar la aplicación, debe activar **Seguimiento** en su dispositivo iOS. Para ello, vaya a **Configuración** > **Privacidad y seguridad** > **Seguimiento** y asegúrese de que la opción **Permitir que las aplicaciones soliciten rastrear**.

![DSN](./../uc3/images/app4.png)

Vaya a Apple App Store y busque `aepmobile-bootcamp`. Haga clic en **Instalar** o **Descargar**.

![DSN](./../uc3/images/app1.png)

Una vez instalada la aplicación, haga clic en **Apertura**.

![DSN](./../uc3/images/app2.png)

Haga clic en **Aceptar**.

![DSN](./../uc3/images/app9.png)

Haga clic en **Permitir**.

![DSN](./../uc3/images/app3.png)

Haga clic en **Estoy de acuerdo**.

![DSN](./../uc3/images/app7.png)

Haga clic en **Permitir al usar la aplicación**.

![DSN](./../uc3/images/app8.png)

Haga clic en **Permitir**.

![DSN](./../uc3/images/app5.png)

Ahora está en la aplicación, en la página principal, listo para pasar por el recorrido del cliente.

![DSN](./../uc3/images/app12.png)

## Flujo de recorrido del cliente

En primer lugar, debe iniciar sesión. Haga clic en **Login**.

![DSN](./images/app13.png)

Después de crear su cuenta en ejercicios anteriores, lo vio en el sitio web. Ahora necesita reutilizar la dirección de correo electrónico de la cuenta creada en la aplicación para iniciar sesión.

![Demostración](./images/pv1.png)

Escriba la dirección de correo electrónico que utilizó en el sitio web aquí y haga clic en **Inicio de sesión**.

![DSN](./images/app14.png)

Recibirá una confirmación de que ha iniciado sesión y recibirá una notificación push.

![DSN](./images/app15.png)

Vuelva a la página principal de la aplicación y verá que aparecen funciones adicionales.

![DSN](./images/app17.png)

En primer lugar, vaya a **Productos**. Haga clic en cualquier producto, en este ejemplo **Café para ir**.

![DSN](./images/app19.png)

Verá el **Café para ir** página del producto en la aplicación.

![DSN](./images/app20.png)

Ahora simulará un evento de entrada de señalización en una ubicación de tienda sin conexión. El objetivo de simular esto es personalizar la experiencia del cliente en las pantallas de las tiendas. Para visualizar la experiencia en la tienda, se ha creado una página que mostrará dinámicamente la información relevante para el cliente que acaba de entrar en la tienda.

Antes de continuar, abra esta página web en su equipo: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Verá esto:

![DSN](./images/screen1.png)

A continuación, vuelva a la página principal. Haga clic en el **señalización** icono.

![DSN](./images/app23.png)

Entonces verás esto. Primero, seleccione **Señalización de pantalla de Bootcamp** y, a continuación, haga clic en la **entrada** botón. Esto le permite simular una entrada de señalización.

![DSN](./images/app21.png)

Ahora, echen un vistazo a la pantalla de la tienda. Verá que el último producto que vio aparece allí en 5 segundos.

![DSN](./images/screen2.png)

A continuación, vuelva a **Productos**. Haga clic en cualquier producto, en este ejemplo **Manta de playa Tan**.

![DSN](./images/app22.png)

A continuación, vuelva a la página principal. Haga clic en el **señalización** icono.

![DSN](./images/app23.png)

Entonces verás esto. Primero, seleccione **Señalización de pantalla de Bootcamp** y, a continuación, haga clic en la **entrada** de nuevo. Esto le permite simular una entrada de señalización.

![DSN](./images/app21.png)

Ahora, eche un vistazo a la pantalla de la tienda de nuevo. Verá que el último producto que vio aparece allí en 5 segundos.

![DSN](./images/screen3.png)

Ahora, echemos un vistazo a su Visor de Perfil en el sitio web. Verá muchos eventos que se agregaron allí, solo para mostrar que cualquier interacción con un cliente se recopila y almacena en Adobe Experience Platform.

![DSN](./images/screen4.png)

En los próximos ejercicios, configurará y probará su propio recorrido de entrada de señalización.

Paso siguiente: [3.2 Crear un evento](./ex2.md)

[Volver al flujo de usuario 3](./uc3.md)

[Volver a todos los módulos](../../overview.md)
