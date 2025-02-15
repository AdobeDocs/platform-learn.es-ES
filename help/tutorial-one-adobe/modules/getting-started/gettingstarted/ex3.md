---
title: 'Introducción: Creación de una secuencia de datos'
description: 'Introducción: Creación de una secuencia de datos'
kt: 5342
doc-type: tutorial
exl-id: d36057b4-64c6-4389-9612-d3c9cf013117
source-git-commit: ef26abbeb0c1076adbada57f0f18f11c7634d022
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 1%

---

# Crear su secuencia de datos

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

![DSN](./images/launchprop.png)

En el menú de la izquierda, haga clic en **[!UICONTROL Etiquetas]**. Después del ejercicio anterior, ahora tiene 3 propiedades de recopilación de datos: una para la web, otra para el móvil y otra para la aplicación CX.

![DSN](./images/launchprop1.png)

Estas propiedades están casi listas para utilizarse, pero antes de empezar a recopilar datos con estas propiedades, debe configurar una secuencia de datos. Obtendrá más información sobre el concepto de secuencia de datos y lo que significa en un ejercicio posterior del módulo Recopilación de datos.

Por ahora, siga estos pasos.

## Creación de un flujo de datos para la web

Haga clic en **[!UICONTROL Datastreams]**.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1a.png)

En la esquina superior derecha de la pantalla, seleccione el nombre de la zona protegida, que debe ser `--aepSandboxName--`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

Haga clic en **[!UICONTROL Nueva secuencia de datos]**.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1.png)

Para **[!UICONTROL Name]** y para la descripción opcional, escriba `--aepUserLdap-- - One Adobe Datastream`. Para **Esquema de asignación**, seleccione **Sistema de demostración - Esquema de evento para el sitio web (Global v1.1)**. Haga clic en **Guardar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig2.png)

Entonces verá esto... Haga clic en **Agregar servicio**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig3.png)

Seleccione el servicio **[!UICONTROL Adobe Experience Platform]**, que mostrará campos adicionales. Entonces verá esto...

Para Conjunto de datos de evento, seleccione **Sistema de demostración - Conjunto de datos de evento para el sitio web (Global v1.1)** y para Conjunto de datos de perfil, seleccione **Sistema de demostración - Conjunto de datos de perfil para el sitio web (Global v1.1)**. Haga clic en **Guardar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig4.png)

Ahora va a ver esto.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig5.png)

En el menú de la izquierda, haga clic en **[!UICONTROL Etiquetas]**.

Filtre los resultados de búsqueda para ver las propiedades de recopilación de datos. Abra la propiedad de **Web** al hacer clic en ella.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig10a.png)

Entonces verá esto... Haga clic en **Extensiones**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig11.png)

Primero, haga clic en la extensión Adobe Experience Platform Web SDK y, a continuación, haga clic en **Configurar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig12.png)

Entonces verá esto... Eche un vistazo al menú **Datastreams** y compruebe que está seleccionada la zona protegida correcta, que en su caso debería ser `--aepSandboxName--`.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig12a.png)

Abra el menú desplegable **Secuencias de datos** y seleccione la secuencia de datos que creó anteriormente.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig13.png)

Asegúrese de haber seleccionado **Flujo de datos** en los tres entornos diferentes. A continuación, haga clic en **Guardar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig14.png)

Vaya a **Flujo de publicación**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig15.png)

Haga clic en **...** para **Principal** y luego haga clic en **Editar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig16.png)

Haga clic en **Agregar todos los recursos modificados** y, a continuación, haga clic en **Guardar y generar para desarrollo**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig17.png)

Los cambios se están publicando y estarán listos en un par de minutos. Después, verá el punto verde junto a **Principal**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig17a.png)

## Crear un flujo de datos para dispositivos móviles

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Haga clic en **[!UICONTROL Datastreams]**.

![Haga clic en el icono Flujo de datos en el panel de navegación izquierdo](./images/edgeconfig1a.png)

En la esquina superior derecha de la pantalla, seleccione el nombre de la zona protegida, que debe ser `--aepSandboxName--`.

![Haga clic en el icono Configuración de Edge en el panel de navegación izquierdo](./images/edgeconfig1b.png)

Haga clic en **[!UICONTROL Nueva secuencia de datos]**.

![Haga clic en el icono Flujo de datos en el panel de navegación izquierdo](./images/edgeconfig1.png)

Para **[!UICONTROL Nombre descriptivo]** y para la descripción opcional, escriba `--aepUserLdap-- - One Adobe Datastream (Mobile)`. Para **Esquema de asignación**, seleccione **Sistema de demostración - Esquema de evento para aplicación móvil (Global v1.1)**. Haga clic en **Guardar**.

Haga clic en **[!UICONTROL Guardar]**.

![Asigne un nombre al conjunto de datos y guarde](./images/edgeconfig2m.png)

Entonces verá esto... Haga clic en **Agregar servicio**.

![Asigne un nombre al conjunto de datos y guarde](./images/edgeconfig3m.png)

Seleccione el servicio **[!UICONTROL Adobe Experience Platform]**, que mostrará campos adicionales. Entonces verá esto...

Para Conjunto de datos de evento, seleccione **Sistema de demostración - Conjunto de datos de evento para aplicación móvil (Global v1.1)** y para Conjunto de datos de perfil, seleccione **Sistema de demostración - Conjunto de datos de perfil para aplicación móvil (Global v1.1)**. Haga clic en **Guardar**.

![Asigne un nombre a la configuración de secuencia de datos y guarde](./images/edgeconfig4m.png)

Entonces verá esto...

![Asigne un nombre a la configuración de secuencia de datos y guarde](./images/edgeconfig5m.png)

El conjunto de datos está listo para utilizarse en la propiedad de cliente de recopilación de datos de Adobe Experience Platform para dispositivos móviles.

Vaya a **Etiquetas** y filtre los resultados de búsqueda para ver sus dos propiedades de recopilación de datos. Abra la propiedad de **Mobile** al hacer clic en ella.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig10am.png)

Entonces verá esto... Haga clic en **Extensiones**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig11m.png)

Haga clic en la extensión **Adobe Experience Platform Edge Network** y, a continuación, haga clic en **Configurar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig12m.png)

Entonces verá esto... Ahora debe seleccionar la zona protegida y la secuencia de datos correctos que acaba de configurar. La zona protegida que se va a usar es `--aepSandboxName--` y el conjunto de datos se llama `--aepUserLdap-- - Demo System Datastream (Mobile)`.

Para el **dominio de Edge Network**, utilice el dominio predeterminado.

Haga clic en **Guardar** para guardar los cambios.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig13m.png)

Vaya a **Flujo de publicación**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig15m.png)

Haga clic en **...** junto a **Principal** y, a continuación, haga clic en **Editar**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig16m.png)

Haga clic en **Agregar todos los recursos modificados** y luego haga clic en **Guardar y generar para desarrollo**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig17m.png)

Los cambios se están publicando y estarán listos en un par de minutos. Después, verá el punto verde junto a **Principal**.

![Asigne un nombre a la configuración de Edge y guarde](./images/edgeconfig17ma.png)

## Pasos siguientes

Ir a [Usar el sitio web](./ex4.md)

Volver a [Introducción](./getting-started.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}