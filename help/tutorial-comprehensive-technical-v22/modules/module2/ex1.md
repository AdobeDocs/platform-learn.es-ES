---
title: 'Foundation - Ingesta de datos: de desconocido a conocido en el sitio web'
description: 'Foundation - Ingesta de datos: de desconocido a conocido en el sitio web'
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 683c7dd9-af69-456e-ab75-2a694588e3b3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---

# 2.1 - De desconocido a conocido en el sitio web

## Contexto

El recorrido de desconocido a conocido es uno de los temas más importantes entre las marcas en estos días, al igual que el recorrido del cliente desde la adquisición hasta la retención.

Adobe Experience Platform juega un papel enorme en este recorrido. Platform es el cerebro de la comunicación, el sistema de experiencia del registro.

Platform es un entorno en el que la palabra **cliente** es más amplio que el **known**-clientes. Esto es muy importante cuando se habla con marcas: un visitante desconocido del sitio web también es cliente desde la perspectiva de Platform y, como tal, todo el comportamiento como visitante desconocido también se envía a Platform. Gracias a este enfoque, cuando este cliente se convierte en un cliente conocido, una marca también puede visualizar lo que sucedió antes de ese momento. Esto ayuda desde la perspectiva de la atribución y la optimización de la experiencia.

## ¿Qué vas a hacer?

Ahora incorporará datos en Adobe Experience Platform y esos datos se vincularán a identificadores como ECID y direcciones de correo electrónico. El objetivo de esto es comprender el contexto empresarial de lo que está a punto de hacer desde una perspectiva de configuración. En el siguiente ejercicio, empezará a configurar todo lo que necesite para que todo ese ingreso de datos sea posible en su propio entorno de espacio aislado.

### Flujo de Recorrido del cliente

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

![Demostración](./images/pv1.png)

Consulte el panel Visualizador de perfiles y el perfil del cliente en tiempo real con el **ID de Experience Cloud** como identificador principal para este cliente actualmente desconocido.

![Demostración](./images/pv2.png)

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

Paso siguiente: [2.2 Configurar esquemas y definir identificadores](./ex2.md)

[Volver al módulo 2](./data-ingestion.md)

[Volver a todos los módulos](../../overview.md)
