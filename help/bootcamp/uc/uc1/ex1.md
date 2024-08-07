---
title: Bootcamp - Perfil del cliente en tiempo real - De desconocido a conocido en el sitio web
description: Bootcamp - Perfil del cliente en tiempo real - De desconocido a conocido en el sitio web
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 32a084a3-4c04-4367-947e-f7151fdad73b
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# 1.1 De desconocido a conocido en el sitio web

## Contexto

El recorrido de lo desconocido a lo conocido es uno de los temas más importantes entre las marcas en estos días, como lo es el recorrido del cliente desde la adquisición hasta la retención.

Adobe Experience Platform juega un papel muy importante en este recorrido. Platform es el cerebro para la comunicación, el **sistema de registro de experiencia**.

Platform es un entorno en el que la palabra cliente es más amplia que solo los clientes conocidos. Un visitante desconocido del sitio web también es un cliente desde la perspectiva de Platform y, como tal, todo el comportamiento como visitante desconocido también se envía a Platform. Gracias a ese enfoque, cuando este visitante finalmente se convierte en un cliente conocido, una marca también puede visualizar lo que sucedió antes de ese momento. Esto ayuda desde la perspectiva de la atribución y la optimización de la experiencia.

## Flujo de recorrido del cliente

Vaya a [https://bootcamp.aepdemo.net](https://publish9122.adobedemo.com/content/aep-bootcamp-experience/language-masters/en.html). Haga clic en **Permitir todo**.

![DSN](./images/web8.png)

Haga clic en el Adobe del logotipo situado en la esquina superior izquierda de la pantalla para abrir el Visor de perfiles.

![Demostración](./images/pv1.png)

Eche un vistazo al panel Visor de perfiles y al Perfil del cliente en tiempo real con el **ID de Experience Cloud** como identificador principal de este cliente actualmente desconocido.

![Demostración](./images/pv2.png)

También puede ver todos los eventos de experiencia recopilados según el comportamiento del cliente. La lista está actualmente vacía, pero cambiará pronto.

![Demostración](./images/pv3.png)

Vaya a la opción de menú **Servicios de aplicaciones** y haga clic en el producto **Real-Time CDP**.

![Demostración](./images/pv4.png)

A continuación, verá la página de detalles del producto. Ahora se ha enviado a Adobe Experience Platform un evento de experiencia de tipo **Vista de producto** mediante la implementación del SDK web que revisó en el módulo 1. Abra el panel Visor de perfiles y eche un vistazo a los **Eventos de experiencia**.

![Demostración](./images/pv5.png)

Vaya a la opción de menú **Servicios de aplicaciones** y haga clic en el producto **Adobe Journey Optimizer**. Se ha enviado otro evento de experiencia a Adobe Experience Platform.

![Demostración](./images/pv7.png)

Abra el panel Visor de perfiles. Ahora verá 2 eventos de experiencia del tipo **Vista de producto**. Aunque el comportamiento es anónimo, se realiza un seguimiento de cada clic y se almacena en Adobe Experience Platform. Una vez que se conozca al cliente anónimo, podremos fusionar automáticamente todos los comportamientos anónimos con el perfil conocido.

![Demostración](./images/pv8.png)

Analicemos ahora su perfil de cliente y luego utilicemos su comportamiento para personalizar su experiencia de cliente en el sitio web.

Paso siguiente: [1.2 Visualice su propio perfil de cliente en tiempo real: IU](./ex2.md)

[Volver al flujo de usuario 1](./uc1.md)

[Volver a todos los módulos](../../overview.md)
