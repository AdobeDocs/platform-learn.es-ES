---
title: 'Adobe Journey Optimizer: Configuración y uso de notificaciones push para iOS'
description: Configuración y uso de notificaciones push para iOS
kt: 5342
doc-type: tutorial
exl-id: a49fa91c-5235-4814-94c1-8dcdec6358c5
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 1%

---

# 3.4.4 Configuración y uso de notificaciones push para iOS

Para utilizar las notificaciones push con Adobe Journey Optimizer, hay que comprobar y conocer varias opciones de configuración.

Estos son todos los ajustes que se deben verificar:

- Conjuntos de datos y esquemas en Adobe Experience Platform
- Flujo de datos para dispositivos móviles
- Propiedad de recopilación de datos para dispositivos móviles
- Superficie de aplicación para certificados push
- Prueba de la configuración push con AEP Assurance

Revisemos estos uno por uno.

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

## 3.4.4.1 Conjuntos de datos push

Adobe Journey Optimizer utiliza conjuntos de datos para almacenar elementos como los tokens push de dispositivos móviles o las interacciones con mensajes push (como: mensaje enviado, mensaje abierto, etc.) en un conjunto de datos en Adobe Journey Optimizer.

Puede encontrar estos conjuntos de datos en **[!UICONTROL Conjuntos de datos]** en el menú de la izquierda de la pantalla. Para mostrar conjuntos de datos del sistema, haga clic en el icono de filtro.

![Ingesta de datos](./images/menudsjo.png)

Habilite la opción **Mostrar conjuntos de datos del sistema** y busque **AJO**. A continuación, verá los conjuntos de datos utilizados para las notificaciones push.

![Ingesta de datos](./images/menudsjo1.png)

## 3.4.4.2 Flujo de datos para dispositivos móviles

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

En el menú de la izquierda, vaya a **[!UICONTROL Flujo de datos]** y busque el flujo de datos que creó en el [Ejercicio 0.2](./../../../modules/gettingstarted/gettingstarted/ex2.md), que se llama `--aepUserLdap-- - Demo System Datastream (Mobile)`. Haga clic en para abrirlo.

![Haga clic en el icono Flujo de datos en el panel de navegación izquierdo](./images/edgeconfig1a.png)

Haga clic en **Editar** en el servicio **Adobe Experience Platform**.

![Haga clic en el icono Flujo de datos en el panel de navegación izquierdo](./images/edgeconfig1.png)

A continuación, verá la configuración del flujo de datos que se definió y en qué conjuntos de datos se almacenarán los eventos y atributos de perfil.

![Asigne un nombre al conjunto de datos y guarde](./images/edgeconfig2.png)

No es necesario realizar cambios, el conjunto de datos ya está listo para utilizarse en la propiedad Cliente de recopilación de datos para dispositivos móviles.

## 3.4.4.3 Revisar la propiedad de recopilación de datos para móviles

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Como parte de [Ejercicio 0.1](./../../../modules/gettingstarted/gettingstarted/ex1.md), se crearon 2 propiedades de recopilación de datos.
Ya ha estado utilizando estas propiedades del cliente de recopilación de datos como parte de módulos anteriores.

Haga clic para abrir la propiedad Recopilación de datos para dispositivos móviles.

![DSN](./images/launchprop.png)

En su propiedad de recopilación de datos, vaya a **Extensiones**. A continuación, verá las distintas extensiones necesarias para la aplicación móvil. Haga clic para abrir la extensión **Adobe Experience Platform Edge Network**.

![Recopilación de datos de Adobe Experience Platform](./images/launchprop1.png)

A continuación, verá que el flujo de datos para móviles está vinculado aquí. A continuación, haga clic en **Cancelar** para volver a la descripción general de las extensiones.

![Recopilación de datos de Adobe Experience Platform](./images/launchprop2.png)

Entonces volverás a estar aquí de nuevo. Verá la extensión de **AEP Assurance**. AEP Assurance le ayuda a inspeccionar, probar, simular y validar la forma en que recopila datos o sirve experiencias en su aplicación móvil. Puede leer más sobre AEP Assurance y Project Griffon aquí [https://aep-sdks.gitbook.io/docs/beta/project-griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon).

![Recopilación de datos de Adobe Experience Platform](./images/launchprop8.png)

A continuación, haga clic en **Configurar** para abrir la extensión **Adobe Journey Optimizer**.

![Recopilación de datos de Adobe Experience Platform](./images/launchprop9.png)

Luego verá que aquí es donde se vincula el conjunto de datos para el seguimiento de eventos push.

![Recopilación de datos de Adobe Experience Platform](./images/launchprop10.png)

No es necesario realizar ningún cambio en la propiedad de recopilación de datos.

## 3.4.4.4 Revisar la configuración de la superficie de la aplicación

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). En el menú de la izquierda, ve a **Superficies de aplicación** y abre la Superficie de aplicación para **APNS de aplicación de demostración DX**.

![Recopilación de datos de Adobe Experience Platform](./images/appsf.png)

A continuación, verá la superficie de aplicación configurada para iOS y Android.

![Recopilación de datos de Adobe Experience Platform](./images/appsf1.png)

## 3.4.4.5 Probar la configuración de notificaciones push mediante AEP Assurance.

Una vez que la aplicación esté instalada, la encontrarás en la pantalla de inicio del dispositivo. Haga clic en el icono para abrir la aplicación.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn1.png)

Cuando uses la aplicación por primera vez, se te pedirá que inicies sesión con tu Adobe ID. Complete el proceso de inicio de sesión.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn2.png)

Después de iniciar sesión, verá una notificación que solicita su permiso para enviar notificaciones. Enviaremos notificaciones como parte del tutorial, así que haz clic en **Permitir**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn3.png)

A continuación, verá la página principal de la aplicación. Vaya a **Configuración**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn4.png)

En la configuración, verá que actualmente hay un **Proyecto público** cargado en la aplicación. Haga clic en **Proyecto personalizado**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn5.png)

Ahora puede cargar un proyecto personalizado. Haga clic en el código QR para cargar fácilmente el proyecto.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn6.png)

Después del ejercicio 0.1, tuvo este resultado. Haga clic para abrir el **proyecto de venta minorista móvil** que se creó para usted.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/dsn5b.png)

En caso de que hayas cerrado accidentalmente la ventana de tu navegador, o para futuras sesiones de demostración o habilitación, también puedes acceder a tu proyecto de sitio web yendo a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en el proyecto de la aplicación móvil para abrirlo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8a.png)

Entonces verá esto... Haga clic en **Integraciones**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8aa.png)

Debe seleccionar la propiedad Recopilación de datos para móvil creada en el ejercicio 0.1. A continuación, haga clic en **Ejecutar**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8b.png)

A continuación, verá esta ventana emergente, que contiene un código QR. Escanee este código QR desde la aplicación móvil.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8c.png)

Luego verás el identificador de tu proyecto en la aplicación, después de lo cual podrás hacer clic en **Guardar**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn7.png)

Ahora, vuelve a **Inicio** en la aplicación. La aplicación ya está lista para utilizarse.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn8.png)

Ahora debe escanear un código QR para conectar su dispositivo móvil a la sesión de AEP Assurance.

Para iniciar una sesión de AEP Assurance, vaya a [https://experience.adobe.com/#/@experienceplatform/griffon](https://experience.adobe.com/#/@experienceplatform/griffon). Haga clic en **Crear sesión**.

![Recopilación de datos de Adobe Experience Platform](./images/griffon3.png)

Haga clic en **Start**.

![Recopilación de datos de Adobe Experience Platform](./images/griffon5.png)

Rellene los valores:

- Nombre de sesión: use `--aepUserLdap-- - push debugging` y reemplace ldap por su ldap
- URL básica: usar **dxdemo://default**

Haga clic en **Next**.

![Recopilación de datos de Adobe Experience Platform](./images/griffon4.png)

Luego verá un código QR en la pantalla, que debe escanear con su dispositivo iOS.

![Recopilación de datos de Adobe Experience Platform](./images/griffon6.png)

En su dispositivo móvil, abra la aplicación de la cámara y escanee el código QR que muestra AEP Assurance.

![Recopilación de datos de Adobe Experience Platform](./images/ipadPushTest8a.png)

A continuación, verá una pantalla emergente en la que se le pedirá que introduzca el código PIN. Copie el código PIN de su pantalla de Assurance de AEP y haga clic en **Conectar**.

![Recopilación de datos de Adobe Experience Platform](./images/ipadPushTest9.png)

Entonces verá esto...

![Recopilación de datos de Adobe Experience Platform](./images/ipadPushTest11.png)

En AEP Assurance, ahora verá que un dispositivo está conectado a la sesión de AEP Assurance.

![Recopilación de datos de Adobe Experience Platform](./images/griffon7.png)

Vaya a **Depuración push**. Vas a ver algo como esto.

![Recopilación de datos de Adobe Experience Platform](./images/griffon10.png)

Alguna explicación:

- La primera columna, **Cliente**, muestra los identificadores disponibles en su dispositivo iOS. Verá un ECID y un token push.
- La segunda columna muestra información de **Perfil**, con información adicional sobre la plataforma en la que se encuentra el token push (APNS o APNSandbox). Si hace clic en el botón **Perfil de Inspect**, se le redirigirá a Adobe Experience Platform y verá el perfil de cliente en tiempo real completo.
- La tercera columna muestra la **Configuración de aplicación**, que se configuró como parte del ejercicio **3.4.5.4 Crear configuración de aplicación en Launch**

Para probar la configuración push, haga clic en el botón **Enviar notificación push**.

![Recopilación de datos de Adobe Experience Platform](./images/griffon11.png)

Debe asegurarse de que la aplicación **DX Demo** no esté abierta cuando haga clic en el botón **Enviar notificación push**. Si la aplicación está abierta, es posible que la notificación push se reciba en segundo plano y no esté visible.

Verá una notificación push como esta en su dispositivo móvil.

![Recopilación de datos de Adobe Experience Platform](./images/ipadPush2.png)

Si ha recibido la notificación push, significa que la configuración es correcta y funciona correctamente.

## 3.4.4.6 Crear un nuevo evento

En el menú, ve a **Administración de Recorrido** y haz clic en **Administrar** en **Eventos**.

![ACOP](./images/acopmenu.png)

En la pantalla **Eventos**, verá una vista similar a esta. Haga clic en **Crear evento**.

![ACOP](./images/add.png)

A continuación, verá una configuración de evento vacía.

![ACOP](./images/emptyevent.png)

En primer lugar, asigne al evento un Nombre como este: `--aepUserLdap--StoreEntryEvent` y establezca la descripción en `Store Entry Event`.

![ACOP](./images/eventname.png)

A continuación se muestra la selección **Tipo de evento**. Seleccione **Unitario**.

![ACOP](./images/eventidtype1.png)

A continuación se muestra la selección **Tipo de ID de evento**. Seleccionar **sistema generado**

![ACOP](./images/eventidtype.png)

A continuación se muestra la selección Esquema. Se ha preparado un esquema para este ejercicio. Use el esquema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Después de seleccionar el esquema, verá una serie de campos seleccionados en la sección **Carga útil**. El evento está ahora completamente configurado.

![ACOP](./images/eventpayload.png)

Entonces debería ver esto. Haga clic en **Guardar**.

![ACOP](./images/eventsave.png)

El evento se ha configurado y guardado. Vuelve a hacer clic en el evento para abrir de nuevo la pantalla **Editar evento**.

![ACOP](./images/eventdone.png)

Pase el ratón sobre el campo **Carga útil** y haga clic en el icono **Ver carga útil**.

![ACOP](./images/hover.png)

Ahora verá un ejemplo de la carga útil esperada.

![ACOP](./images/fullpayload.png)

Su evento tiene un identificador de evento de orquestación único, que puede encontrar desplazándose hacia abajo en esa carga hasta que vea `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

El ID de evento es lo que debe enviarse a Adobe Experience Platform para almacenar en déclencheur el Recorrido que va a generar en el siguiente paso. Escriba este eventID, tal como lo necesitará en el paso siguiente.
`"eventID": "e3a8f0bdc0b609667cd96a72a6b1e5aafa0ddaf6ccf121c574e6a2030860a633"`

Haga clic en **Aceptar**, seguido de **Cancelar**.

## 3.4.4.7 Creación de un recorrido

En el menú, ve a **Recorridos** y haz clic en **Crear Recorrido**.

![DSN](./images/sjourney1.png)

Entonces verá esto... Dé un nombre a su recorrido. Usar `--aepUserLdap-- - Store Entry journey`. Haga clic en **Aceptar**.

![DSN](./images/sjourney3.png)

En primer lugar, debe agregar el evento como punto de partida del recorrido. Busque el evento `--aepUserLdap--StoreEntryEvent`, arrástrelo y suéltelo en el lienzo. Haga clic en **Aceptar**.

![DSN](./images/sjourney4.png)

A continuación, en **Acciones**, busque la acción **Push**.
Arrastre y suelte la acción **Push** en el lienzo.

![DSN](./images/sjourney5.png)

Establezca **Category** en **Marketing** y seleccione una superficie push que le permita enviar notificaciones push. En este caso, la superficie de correo electrónico que se va a seleccionar es **Push-iOS-Android**.

![ACOP](./images/journeyactions1push.png)

El siguiente paso es crear el mensaje. Para ello, haga clic en **Editar contenido**.

![ACOP](./images/journeyactions2push.png)

Entonces verá esto... Haga clic en el icono **personalización** para el campo **Título**.

![Push](./images/bp5.png)

Entonces verá esto... Ahora puede seleccionar cualquier atributo de perfil directamente desde el Perfil del cliente en tiempo real.

![Push](./images/bp6.png)

Busque el campo **Nombre** y, a continuación, haga clic en el icono **+** situado junto al campo **Nombre**. Verá el token de personalización del nombre que se está agregando: **{{profile.person.name.firstName}}**.

![Push](./images/bp9.png)

A continuación, agregue el texto **, ¡bienvenido a nuestra tienda!** detrás de **{{profile.person.name.firstName}}**.

Haga clic en **Guardar**.

![Push](./images/bp10.png)

Ahora tiene esto. Haga clic en el icono **personalización** para el campo **Cuerpo**.

![Push](./images/bp11.png)

Escriba este texto **Haga clic aquí para obtener un descuento del 10% al comprar hoy.** y haga clic en **Guardar**.

![Push](./images/bp12.png)

Entonces, tendrás esto. Haga clic en la flecha de la esquina superior izquierda para volver al recorrido.

![Journey Optimizer](./images/bp12a.png)

Haga clic en **Aceptar** para cerrar la acción de inserción.

![DSN](./images/sjourney8.png)

Haga clic en **Publish**.

![DSN](./images/sjourney10.png)

Vuelva a hacer clic en **Publish**.

![DSN](./images/sjourney10a.png)

El recorrido se ha publicado.

![DSN](./images/sjourney11.png)

## 3.4.4.8 Probar el recorrido y el mensaje push

En la aplicación móvil DX Demo 2.0, ve a la pantalla **Configuración**. Haga clic en el botón **Entrada de tienda**.

>[!NOTE]
>
>El botón **Entrada de tienda** se está implementando en este momento. Aún no lo encontrará en la aplicación.

![DSN](./images/demo1b.png)

Asegúrese de cerrar la aplicación inmediatamente después de hacer clic en el icono **Entrada de la tienda**; de lo contrario, no se mostrará el mensaje push.

![DSN](./images/demo2.png)

Después de un par de segundos, verá el mensaje.

![DSN](./images/demo3.png)

Ha terminado este ejercicio.

Siguiente paso: [3.4.5 Crear un recorrido de evento empresarial](./ex5.md)

[Volver al módulo 3.4](./journeyoptimizer.md)

[Volver a todos los módulos](../../../overview.md)
