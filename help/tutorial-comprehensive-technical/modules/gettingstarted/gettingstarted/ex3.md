---
title: 'Introducción: Creación de una secuencia de datos'
description: 'Introducción: Creación de una secuencia de datos'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 1%

---

# 0.3 Crear su secuencia de datos

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Después del ejercicio anterior, ahora tiene dos propiedades de recopilación de datos: una para la web y otra para el móvil.

![DSN](./images/launchprop.png)

Estas propiedades están casi listas para utilizarse, pero antes de empezar a recopilar datos con estas propiedades, debe configurar una secuencia de datos. Obtendrá más información sobre el concepto de conjunto de datos y su significado en el Ejercicio 1.2.

Por ahora, siga estos pasos.

## 0.3.1 Creación de un flujo de datos para la web

Haga clic en **[!UICONTROL Datastreams]** o **[!UICONTROL Datastreams (Beta)]**.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1a.png)

En la esquina superior derecha de la pantalla, seleccione el nombre de la zona protegida, que debe ser `--aepSandboxName--`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

Haga clic en **[!UICONTROL Nueva secuencia de datos]**.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1.png)

Para **[!UICONTROL Nombre descriptivo]** y para la descripción opcional, escriba `--aepUserLdap-- - Demo System Datastream`. Para Esquema de eventos, seleccione **Sistema de demostración - Esquema de eventos para el sitio web (Global v1.1)**. Haga clic en **Guardar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig2.png)

Entonces verá esto... Haga clic en **Agregar servicio**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig3.png)

Seleccione el servicio **[!UICONTROL Adobe Experience Platform]**, que mostrará campos adicionales. Entonces verá esto...

Para Conjunto de datos de evento, seleccione **Sistema de demostración - Conjunto de datos de evento para el sitio web (Global v1.1)** y para Conjunto de datos de perfil, seleccione **Sistema de demostración - Conjunto de datos de perfil para el sitio web (Global v1.1)**. Haga clic en **Guardar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig4.png)

Ahora va a ver esto.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig5.png)

Eso es todo por ahora. En [Módulo 1.1](./../../../modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md) aprenderá más sobre el SDK web y cómo configurar todas sus funcionalidades.

En el menú de la izquierda, haga clic en **[!UICONTROL Etiquetas]**.

Filtre los resultados de búsqueda para ver las dos propiedades de recopilación de datos. Abra la propiedad de **Web** al hacer clic en ella.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig10a.png)

Entonces verá esto... Haga clic en **Extensiones**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig11.png)

En la extensión SDK para web de Adobe Experience Platform, haga clic en **Configurar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig12.png)

Entonces verá esto... Para **Datastreams**, actualmente verá un valor ficticio establecido en 1. Ahora necesita hacer clic en el botón de opción **Elegir de la lista**. En la lista desplegable, seleccione la secuencia de datos que creó anteriormente.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig13.png)

Asegúrese de haber seleccionado **Flujo de datos**. SUGERENCIA: Puede filtrar los resultados de la lista desplegable fácilmente escribiendo su `--aepUserLdap--`.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig14.png)

Desplácese hacia abajo hasta que vea **Recopilación de datos**. Asegúrese de que la casilla de verificación para **Habilitar la recopilación de datos de clics** no esté habilitada. Haga clic en **Guardar** para guardar los cambios.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig14a.png)

Vaya a **Flujo de publicación**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig15.png)

Haga clic en **...** para **Principal** y luego haga clic en **Editar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig16.png)

Haga clic en **Agregar todos los recursos modificados** y, a continuación, haga clic en **Guardar y generar para desarrollo**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig17.png)

Los cambios se están publicando y estarán listos en un par de minutos.

## 0.3.2 Crear un flujo de datos para dispositivos móviles

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Haga clic en **[!UICONTROL Datastreams]** o **[!UICONTROL Datastreams (Beta)]**.

![Haga clic en el icono Flujo de datos en el panel de navegación izquierdo](./images/edgeconfig1a.png)

En la esquina superior derecha de la pantalla, seleccione el nombre de la zona protegida, que debe ser `--aepSandboxName--`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

Haga clic en **[!UICONTROL Nueva secuencia de datos]**.

![Haga clic en el icono Flujo de datos en el panel de navegación izquierdo](./images/edgeconfig1.png)

Para **[!UICONTROL Nombre descriptivo]** y para la descripción opcional, escriba `--aepUserLdap-- - Demo System Datastream (Mobile)`. Para Esquema de eventos, seleccione **Sistema de demostración - Esquema de eventos para aplicación móvil (Global v1.1)**. Haga clic en **Guardar**.

Haga clic en **[!UICONTROL Guardar]**.

![Asigne un nombre al conjunto de datos y guarde](./images/edgeconfig2m.png)

Entonces verá esto... Haga clic en **Agregar servicio**.

![Asigne un nombre al conjunto de datos y guarde](./images/edgeconfig3m.png)

Seleccione el servicio **[!UICONTROL Adobe Experience Platform]**, que mostrará campos adicionales. Entonces verá esto...

Para Conjunto de datos de evento, seleccione **Sistema de demostración - Conjunto de datos de evento para aplicación móvil (Global v1.1)** y para Conjunto de datos de perfil, seleccione **Sistema de demostración - Conjunto de datos de perfil para aplicación móvil (Global v1.1)**. Haga clic en **Guardar**.

![Asigne un nombre a la configuración de secuencia de datos y guarde](./images/edgeconfig4m.png)

Entonces verá esto...

![Asigne un nombre a la configuración de secuencia de datos y guarde](./images/edgeconfig5m.png)

La secuencia de datos ya está lista para utilizarse en la propiedad de cliente de recopilación de datos de Adobe Experience Platform para dispositivos móviles.

Vaya a **Etiquetas** y filtre los resultados de búsqueda para ver sus dos propiedades de recopilación de datos. Abra la propiedad de **Mobile** al hacer clic en ella.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig10am.png)

Entonces verá esto... Haga clic en **Extensiones**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig11m.png)

En la extensión **Adobe Experience Platform Edge Network**, haga clic en **Configurar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig12m.png)

Entonces verá esto... Ahora debe seleccionar la zona protegida y la secuencia de datos correctos que acaba de configurar. La zona protegida que se va a usar es `--aepSandboxName--` y el conjunto de datos se llama `--aepUserLdap-- - Demo System Datastream (Mobile)`.

Para el **dominio de Edge Network**, use el dominio predeterminado que es **edge.adobedc.net**.

Haga clic en **Guardar** para guardar los cambios.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig13m.png)

Vaya a **Flujo de publicación**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig15m.png)

Haga clic en **...** junto a **Principal** y, a continuación, haga clic en **Editar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig16m.png)

Haga clic en **Agregar todos los recursos modificados** y luego haga clic en **Guardar y generar para desarrollo**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig17m.png)

Los cambios se están publicando y estarán listos en un par de minutos.

Paso siguiente: [0.4 Usar el sitio web](./ex4.md)

[Volver al módulo 0](./getting-started.md)

[Volver a todos los módulos](./../../../overview.md)