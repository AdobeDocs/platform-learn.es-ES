---
title: Foundation - Perfil del cliente en tiempo real - De desconocido a conocido en el sitio web
description: Foundation - Perfil del cliente en tiempo real - De desconocido a conocido en el sitio web
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 065d79c5-8979-4992-afb1-4da47bbff74b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 2%

---

# 3.1 De desconocido a conocido en el sitio web

## Contexto

El recorrido de desconocido a conocido es uno de los temas más importantes entre las marcas en estos días, al igual que el recorrido del cliente desde la adquisición hasta la retención.

Adobe Experience Platform juega un papel enorme en este recorrido. Platform es el cerebro de la comunicación, el &quot;sistema de experiencia del registro&quot;.

Platform es un entorno en el que la palabra cliente es más amplia que solo los clientes conocidos. Un visitante desconocido en el sitio web también es cliente desde la perspectiva de Platform y, como tal, todo el comportamiento como visitante desconocido también se envía a Platform. Gracias a este enfoque, cuando este visitante finalmente se convierte en un cliente conocido, una marca también puede visualizar lo que sucedió antes de ese momento. Esto ayuda desde la perspectiva de la atribución y la optimización de la experiencia.

## Flujo de recorrido del cliente

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión en Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](../module0/images/web8.png)

En el **Pantallas** página, haga clic en **Ejecutar**.

![DSN](../module1/images/web2.png)

Verá que su sitio web de demostración se abre. Seleccione la dirección URL y cópiela en el portapapeles.

![DSN](../module0/images/web3.png)

Abra una nueva ventana del explorador incógnito.

![DSN](../module0/images/web4.png)

Pegue la dirección URL del sitio web de la demostración, que copió en el paso anterior. A continuación, se le pedirá que inicie sesión con su Adobe ID.

![DSN](../module0/images/web5.png)

Seleccione su tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../module0/images/web6.png)

Verá su sitio web cargado en una ventana del navegador incógnito. Para cada demostración, tendrá que usar una ventana nueva del explorador incógnito para cargar la URL de su sitio web de demostración.

![DSN](../module0/images/web7.png)

Haga clic en el icono del logotipo de Adobe en la esquina superior izquierda de la pantalla para abrir el Visor de perfiles.

![Demostración](../module2/images/pv1.png)

Consulte el panel Visualizador de perfiles y el perfil del cliente en tiempo real con el **ID de Experience Cloud** como identificador principal para este cliente actualmente desconocido.

![Demostración](../module2/images/pv2.png)

También puede ver todos los eventos de experiencias que se recopilaron en función del comportamiento del cliente. La lista está vacía actualmente, pero eso cambiará pronto.

![Demostración](../module2/images/pv3.png)

Vaya a la **Hombres** categoría del producto. A continuación, haga clic en el producto **Montana Wind Jacket**.

![Demostración](../module2/images/pv4.png)

A continuación, verá la página de detalles del producto. Un evento de experiencia de tipo **Vista del producto** se ha enviado a Adobe Experience Platform mediante la implementación del SDK web que revisó en el módulo 1.

![Demostración](../module2/images/pv5.png)

Abra el panel Visualizador de proveedores y eche un vistazo a su **Eventos de experiencias**.

![Demostración](../module2/images/pv6.png)

Vuelva a la **Mujeres** y haga clic en otro producto. Se ha enviado otro evento de experiencia a Adobe Experience Platform.

![Demostración](../module2/images/pv7.png)

Abra el panel Visor de perfiles . Ahora verá dos eventos de experiencia de tipo **Vista del producto**. Aunque el comportamiento es anónimo, podemos rastrear cada clic y almacenarlo en Adobe Experience Platform. Una vez que el cliente anónimo sea conocido, podremos fusionar todo el comportamiento anónimo automáticamente con el perfil conocido.

![Demostración](../module2/images/pv8.png)

Vaya a la página Registro/Inicio de sesión . Haga clic en **CREAR UNA CUENTA**.

![Demostración](../module2/images/pv9.png)

Complete los detalles y haga clic en **Registro** después de lo cual, se le redirigirá a la página anterior.

![Demostración](../module2/images/pv10.png)

Abra el panel Visor de perfiles y vaya a Perfil del cliente en tiempo real. En el panel Visor de perfiles, debería ver todos los datos personales mostrados, como los identificadores de correo electrónico y teléfono recién agregados.

![Demostración](../module2/images/pv11.png)

En el panel Visor de perfiles, vaya a Eventos de experiencias. Verá los dos productos que ya había visto en el panel Visor de perfiles . Ambos eventos ahora están conectados a su perfil &quot;conocido&quot;.

![Demostración](../module2/images/pv12.png)

Ahora ha introducido datos en Adobe Experience Platform y los ha vinculado a identificadores como ECID y direcciones de correo electrónico. El objetivo de esto es comprender el contexto comercial de lo que estás a punto de hacer. En el siguiente ejercicio, empezará a configurar todo lo que necesite para que sea posible introducir todos los datos.

### Navegar por la aplicación móvil

Después de convertirse en un cliente conocido, es hora de empezar a usar la aplicación móvil. Abra la aplicación móvil en iPhone y, a continuación, inicie sesión en la aplicación.

Si ya no tiene la aplicación instalada, o si no puede recordar cómo instalarla, consulte este documento: [0.5 Usar la aplicación móvil](../module0/ex5.md)

Después de instalar la aplicación como se indica, verá la página de aterrizaje de la aplicación con la marca Luma cargada. Haga clic en el icono de cuenta en la parte superior izquierda de la pantalla.

![Demostración](./images/app_hp.png)

En la pantalla Inicio de sesión, inicie sesión con la dirección de correo electrónico que utilizó en el sitio web del escritorio. Haga clic en **Login**.

![Demostración](./images/app_acc.png)

Vaya a la pantalla de inicio de la aplicación y haga clic en para abrir cualquier producto.

![Demostración](./images/app_hp.png)

A continuación, verá la página de detalles del producto.

![Demostración](./images/app_carst.png)

Vaya a la pantalla principal de la aplicación y deslice a la izquierda en la pantalla para ver el panel Visor de perfiles . A continuación, verá el producto que acaba de ver en la **Eventos de experiencias** junto con todas las vistas de productos de la sesión anterior del sitio web.

![Demostración](./images/app_after_carst.png)

Ahora vuelva al equipo de escritorio y actualice la página principal, después de lo cual verá que el producto también aparece allí.

![Demostración](./images/lb_x_aftermobile.png)

Ahora ha introducido datos en Adobe Experience Platform y los ha vinculado a identificadores como ECID y direcciones de correo electrónico. El objetivo de este ejercicio era comprender el contexto comercial de lo que estás a punto de hacer. Ahora ha creado un perfil de cliente en tiempo real entre dispositivos. En el siguiente ejercicio, seguirá adelante y visualizará su perfil en Adobe Experience Platform.

Paso siguiente: [3.2 Visualizar su propio perfil de cliente en tiempo real: IU](./ex2.md)

[Volver al módulo 3](./real-time-customer-profile.md)

[Volver a todos los módulos](../../overview.md)
