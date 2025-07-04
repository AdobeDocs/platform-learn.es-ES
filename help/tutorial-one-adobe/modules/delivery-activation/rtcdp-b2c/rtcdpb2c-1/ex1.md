---
title: 'Foundation - Perfil del cliente en tiempo real: de desconocido a conocido en el sitio web'
description: 'Foundation - Perfil del cliente en tiempo real: de desconocido a conocido en el sitio web'
kt: 5342
doc-type: tutorial
exl-id: f33a7448-e1b9-47e7-97c7-509ad36cf991
source-git-commit: 2264f26a0778c2570c36abe1bae4d6a1dc3a465c
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# 2.1.1 De desconocido a conocido en el sitio web

## Contexto

El recorrido de lo desconocido a lo conocido es uno de los temas más importantes entre las marcas en estos días, como lo es el recorrido del cliente desde la adquisición hasta la retención.

Adobe Experience Platform juega un papel muy importante en este recorrido. Platform es el cerebro para la comunicación, el &quot;sistema de experiencia de registro&quot;.

Platform es un entorno en el que la palabra cliente es más amplia que solo los clientes conocidos. Un visitante desconocido del sitio web también es un cliente desde la perspectiva de Platform y, como tal, todo el comportamiento como visitante desconocido también se envía a Platform. Gracias a ese enfoque, cuando este visitante finalmente se convierte en un cliente conocido, una marca también puede visualizar lo que sucedió antes de ese momento. Esto ayuda desde la perspectiva de la atribución y la optimización de la experiencia.

## Flujo de recorrido del cliente

Vaya a [https://dsn.adobe.com](https://dsn.adobe.com). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en los 3 puntos **...** del proyecto del sitio web y, a continuación, haga clic en **Ejecutar** para abrirlo.

![DSN](./../../datacollection/dc1.1/images/web8.png)

A continuación, verá cómo se abre el sitio web de demostración. Seleccione la URL y cópiela en el portapapeles.

![DSN](../../../getting-started/gettingstarted/images/web3.png)

Abra una nueva ventana del explorador de incógnito.

![DSN](../../../getting-started/gettingstarted/images/web4.png)

Pegue la dirección URL del sitio web de demostración, que copió en el paso anterior. Luego se le pedirá que inicie sesión con su Adobe ID.

![DSN](../../../getting-started/gettingstarted/images/web5.png)

Seleccione el tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../../../getting-started/gettingstarted/images/web6.png)

Luego verá el sitio web cargado en una ventana de incógnito del explorador. Para cada ejercicio, deberá utilizar una ventana nueva del explorador de incógnito para cargar la URL del sitio web de demostración.

![DSN](../../../getting-started/gettingstarted/images/web7.png)

Haga clic en el icono del logotipo de Adobe, en la esquina superior izquierda de la pantalla, para abrir el Visor de perfiles.

![Demostración](../../datacollection/dc1.2/images/pv1.png)

Eche un vistazo al panel del visor de perfiles y al perfil del cliente en tiempo real con el **Experience Cloud ID** como identificador principal de este cliente actualmente desconocido.

![Demostración](../../datacollection/dc1.2/images/pv2.png)

También puede ver todos los eventos de experiencia recopilados según el comportamiento del cliente. La lista está actualmente vacía, pero cambiará pronto.

![Demostración](../../datacollection/dc1.2/images/pv3.png)

Vaya a la categoría de productos **Teléfonos y dispositivos**. A continuación, haz clic en el producto **iPhone 16 Pro**.

![Demostración](../../datacollection/dc1.2/images/pv4.png)

A continuación, verá la página de detalles del producto. Ahora se ha enviado un evento de tipo **Vista de producto** a Adobe Experience Platform mediante la implementación de Web SDK que revisó en el módulo 1.

![Demostración](../../datacollection/dc1.2/images/pv5.png)

Abra el panel Visor de Provile y eche un vistazo a los **Eventos**.

![Demostración](../../datacollection/dc1.2/images/pv6.png)

Vuelva a la página de categoría **Teléfonos y dispositivos** y haga clic en otro producto. Se ha enviado otro evento de experiencia a Adobe Experience Platform. Abra el panel Visor de perfiles. Ahora verá 2 eventos de tipo **Vista de producto**. Aunque el comportamiento es anónimo, con el consentimiento adecuado, puede rastrear cada clic y almacenarlo en Adobe Experience Platform. Una vez que se conozca al cliente anónimo, podremos fusionar automáticamente todos los comportamientos anónimos con el perfil conocido.

Haga clic en **Iniciar sesión**.

![Demostración](../../datacollection/dc1.2/images/pv7.png)

Haga clic en **Crear una cuenta**.

![Demostración](../../datacollection/dc1.2/images/pv8.png)

Complete sus detalles y haga clic en **Registrarse** después de lo cual se le redirigirá a la página anterior.

![Demostración](../../datacollection/dc1.2/images/pv9.png)

Abra el panel Visualizador de perfiles y vaya a Perfil del cliente en tiempo real. En el panel Visor de perfiles, debería ver todos los datos personales que se muestran, como los identificadores de correo electrónico y teléfono que acaba de agregar.

![Demostración](../../datacollection/dc1.2/images/pv10.png)

En el panel Visor de perfiles, vaya a Eventos de experiencia. Verá los 2 productos que vio antes en el panel Visor de perfiles. Ambos eventos ahora también están conectados al perfil &quot;conocido&quot;.

![Demostración](../../datacollection/dc1.2/images/pv11.png)

Ahora ha introducido datos en Adobe Experience Platform y los ha vinculado a identificadores como ECID y direcciones de correo electrónico. El objetivo de esto es comprender el contexto empresarial de lo que está a punto de hacer. En el siguiente ejercicio, empezará a configurar todo lo que necesita para que sea posible toda esa ingesta de datos.

### Navegar por la aplicación móvil

Después de convertirse en un cliente conocido, es hora de empezar a usar la aplicación móvil. Abra la aplicación móvil en el iPhone y, a continuación, inicie sesión en la aplicación.

Si ya no tienes la aplicación instalada, o si no recuerdas cómo instalarla, mira aquí: [Usa la aplicación móvil](../../../getting-started/gettingstarted/ex5.md)

Después de instalar la aplicación según las instrucciones, verá la página de aterrizaje de la aplicación con la marca Citi Signal cargada. Haga clic en el icono de cuenta en la parte superior izquierda de la pantalla.

![Demostración](./images/app_hpz.png)

En la pantalla Inicio de sesión, inicie sesión con la dirección de correo electrónico que utilizó en el sitio web de escritorio. Haga clic en **Iniciar sesión**.

![Demostración](./images/app_acc.png)

A continuación, recibirá una confirmación de que ha iniciado sesión.

![Demostración](./images/app_acc1.png)

Vaya a la pantalla de inicio de la aplicación y a la página **Teléfonos y dispositivos**.

![Demostración](./images/app_hp1.png)

Haga clic en cualquier producto de la página.

![Demostración](./images/app_hp2.png)

A continuación, verá la página de detalles del producto.

![Demostración](./images/app_galaxy.png)

Vaya a la pantalla de inicio de la aplicación y haga clic en el icono de Adobe para ver el panel Visor de perfiles. Verá la vista **Atributos de perfil**, que ahora muestra una vista combinada de su actividad de aplicaciones web y móviles. Ir a **Eventos**

![Demostración](./images/app_hp3.png)

Verá el producto que acaba de ver en la sección **Eventos de experiencia**, junto con todas las vistas de productos de la sesión del sitio web anterior.

>[!NOTE]
>
>Pueden pasar un par de minutos antes de que vea la vista consolidada en la aplicación y en el sitio web.

![Demostración](./images/app_after_galaxy.png)

Ahora vuelva al equipo de escritorio y actualice la página principal, después de lo cual verá que el producto también aparece allí.

>[!NOTE]
>
>Pueden pasar un par de minutos antes de que vea la vista consolidada en la aplicación y en el sitio web.

![Demostración](./images/web_x_aftermobile.png)

Ahora ha introducido datos en Adobe Experience Platform y los ha vinculado a identificadores como ECID y direcciones de correo electrónico. El objetivo de este ejercicio era comprender el contexto empresarial de lo que está a punto de hacer. Ahora ha creado de forma eficaz un perfil de cliente en tiempo real y entre dispositivos. En el próximo ejercicio, verá el perfil en Adobe Experience Platform.

## Pasos siguientes

Vaya a [2.1.2 y visualice su propio perfil de cliente en tiempo real: IU](./ex2.md){target="_blank"}

Volver a [Perfil del cliente en tiempo real](./real-time-customer-profile.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
