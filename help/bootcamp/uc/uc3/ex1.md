---
title: Bootcamp - Fusión física y digital - Utilice la aplicación móvil y déclencheur una entrada de señalización
description: Bootcamp - Fusión física y digital - Utilice la aplicación móvil y déclencheur una entrada de señalización
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Mobile SDK
exl-id: c33c973b-db8a-49ce-bd6c-a6c4fbe579a0
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# 3.1 Uso de la aplicación móvil y déclencheur de una entrada de señalización

## Instalación de la aplicación móvil

Antes de instalar la aplicación, debes habilitar **Seguimiento** en tu dispositivo iOS. Para ello, ve a **Configuración** > **Privacidad y seguridad** > **Seguimiento** y asegúrate de que la opción **Permitir que las aplicaciones soliciten seguimiento**.

![DSN](./../uc3/images/app4.png)

Vaya al App Store de Apple y busque `aepmobile-bootcamp`. Haz clic en **Instalar** o **Descargar**.

![DSN](./../uc3/images/app1.png)

Una vez que la aplicación esté instalada, haga clic en **Abrir**.

![DSN](./../uc3/images/app2.png)

Haga clic en **Aceptar**.

![DSN](./../uc3/images/app9.png)

Haga clic en **Permitir**.

![DSN](./../uc3/images/app3.png)

Haz clic en **Acepto**.

![DSN](./../uc3/images/app7.png)

Haga Clic En **Permitir Mientras Usa La Aplicación**.

![DSN](./../uc3/images/app8.png)

Haga clic en **Permitir**.

![DSN](./../uc3/images/app5.png)

Ahora está en la aplicación, en la página principal, listo para pasar por el recorrido del cliente.

![DSN](./../uc3/images/app12.png)

## Flujo de recorrido del cliente

En primer lugar, debe iniciar sesión. Haga clic en **Iniciar sesión**.

![DSN](./images/app13.png)

Después de crear la cuenta en los ejercicios anteriores, lo vio en el sitio web. Ahora debe reutilizar la dirección de correo electrónico de la cuenta que creó en la aplicación para iniciar sesión.

![Demostración](./images/pv1.png)

Escriba aquí la dirección de correo electrónico que utilizó en el sitio web y haga clic en **Iniciar sesión**.

![DSN](./images/app14.png)

A continuación, recibirá una confirmación de que ha iniciado sesión y una notificación push.

![DSN](./images/app15.png)

Vuelva a la página principal de la aplicación y verá que aparecen funciones adicionales.

![DSN](./images/app17.png)

Primero, vaya a **Productos**. Haz clic en cualquier producto, en este ejemplo **Café para llevar**.

![DSN](./images/app19.png)

Verá la página de producto **Café para llevar** en la aplicación.

![DSN](./images/app20.png)

Ahora simulará un evento de entrada de señalización en una ubicación de tienda sin conexión. El objetivo de simular esto es personalizar la experiencia del cliente en las pantallas de las tiendas. Para visualizar la experiencia en tienda, se ha creado una página que muestra dinámicamente la información relevante para el cliente que acaba de entrar en la tienda.

Antes de continuar, abra esta página web en el equipo: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

A continuación, verá esto:

![DSN](./images/screen1.png)

A continuación, vuelva a la página principal. Haga clic en el icono **baliza**.

![DSN](./images/app23.png)

Entonces verá esto... Primero, seleccione **Señalización de pantalla Bootcamp** y luego haga clic en el botón **entry**. Esto le permite simular una entrada de señalización.

![DSN](./images/app21.png)

Eche un vistazo a la pantalla de la tienda. Verá el último producto que vio aparecer allí en 5 segundos.

![DSN](./images/screen2.png)

A continuación, vuelva a **Productos**. Haz clic en cualquier producto, en este ejemplo **Manta de playa Tan**.

![DSN](./images/app22.png)

A continuación, vuelva a la página principal. Haga clic en el icono **baliza**.

![DSN](./images/app23.png)

Entonces verá esto... Primero, selecciona **Señalización de pantalla Bootcamp** y luego haz clic en el botón **entry** de nuevo. Esto le permite simular una entrada de señalización.

![DSN](./images/app21.png)

Ahora, vuelva a ver la pantalla de la tienda. Verá el último producto que vio aparecer allí en 5 segundos.

![DSN](./images/screen3.png)

Ahora también echemos un vistazo al Visor de perfiles en el sitio web. Verá muchos eventos que se agregaron allí, solo para mostrar que cualquier interacción con un cliente se recopila y almacena en Adobe Experience Platform.

![DSN](./images/screen4.png)

En los próximos ejercicios, configurará y probará su propio recorrido de entrada de señalización.

Siguiente paso: [3.2 Crea tu evento](./ex2.md)

[Volver al flujo de usuario 3](./uc3.md)

[Volver a todos los módulos](../../overview.md)
