---
title: 'Recopilación de datos de Adobe Experience Platform y reenvío del servidor en tiempo real: cree y configure un vínculo web personalizado'
description: Creación y configuración de un enlace web personalizado
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: db15c445-b45a-44cb-bc24-598676f02a5d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 1%

---

# 14.3 Crear y configurar un vínculo web personalizado

## 14.3.1 Cree su vínculo web personalizado

Vaya a [https://webhook.site/](https://webhook.site/). Verá algo así:

![demostración](./images/webhook1.png)

Verá su URL única, que tiene este aspecto: `https://webhook.site/585126a1-41fc-4721-864b-d4aa8c268a1d`.

Este sitio web ya ha creado este enlace web para usted, y usted podrá configurar este enlace web en su **[!DNL Event Forwarding property]** para comenzar a probar el reenvío de eventos.

## 14.3.2 Actualice la propiedad Event Forwarding: Crear un elemento de datos

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) y vaya a **Reenvío de eventos**. Busque la propiedad Event Forwarding y haga clic en ella para abrirla.

![SSF de recopilación de datos de Adobe Experience Platform](./images/prop1.png)

En el menú de la izquierda, vaya a **Elementos de datos**. Haga clic en **Crear nuevo elemento de datos**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/de1.png)

A continuación, verá un nuevo elemento de datos para configurar.

![SSF de recopilación de datos de Adobe Experience Platform](./images/de2.png)

Realice la siguiente selección:

- Como **Nombre**, introduzca **Evento XDM**.
- Como **Extensión**, seleccione **Principal**.
- Como **Tipo de elemento de datos**, seleccione **Ruta**.
- Como **Ruta**, introduzca **arc.event.xdm**. Al entrar en esta ruta, filtrará el **XDM** de la carga útil de evento que envía el sitio web o la aplicación móvil a Adobe Edge.

Ahora tendrás esto. Haga clic en **Guardar**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/de3.png)

>[!NOTE]
>
>En la ruta anterior, se hace referencia a **arc**. **arc** representa Contexto de Recursos de Adobe y **arc** representa siempre el objeto más alto disponible que está disponible en el contexto del servidor. Los enriquecimientos y transformaciones pueden añadirse a los **arc** mediante las funciones del servidor de recopilación de datos de Adobe Experience Platform.
>
>En la ruta anterior, se hace referencia a **evento**. **evento** significa un evento único y Adobe Experience Platform Data Collection Server siempre evaluará cada evento individualmente. A veces, es posible que vea una referencia a **events** en la carga útil que envía el cliente del SDK web, pero en el servidor de recopilación de datos de Adobe Experience Platform, cada evento se evalúa individualmente.

## 14.3.3 Actualice la propiedad Servidor de recopilación de datos de Adobe Experience Platform: Crear una regla

En el menú de la izquierda, vaya a **Reglas**. Haga clic en **Crear nueva regla**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl1.png)

A continuación, verá una nueva regla para configurar. Introduzca la variable **Nombre**: **Todas las páginas**. Para este ejercicio, no es necesario configurar una condición. En su lugar, configurará una acción. Haga clic en el **+ Agregar** botón debajo de **Acciones**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl2.png)

Entonces verás esto. Realice la siguiente selección:

- Seleccione el **Extensión**: **Conector de Adobe Cloud**.
- Seleccione el **Tipo de acción**: **Llamada de recuperación**.

Eso debería darte esto **Nombre**: **Conector de Adobe Cloud: Realizar llamada de recuperación**. Ahora debería ver esto:

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl4.png)

A continuación, configure lo siguiente:

- Cambiar el método de solicitud de GET a **POST**
- Introduzca la dirección URL del vínculo web personalizado que ha creado en uno de los pasos anteriores del [https://webhook.site/](https://webhook.site/) sitio web con este aspecto: `https://webhook.site/585126a1-41fc-4721-864b-d4aa8c268a1d`

Ahora deberías tener esto. A continuación, vaya a **Cuerpo**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl6.png)

Entonces verás esto. Haga clic en el icono del elemento de datos como se indica a continuación.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl7.png)

En la ventana emergente, seleccione el elemento de datos . **Evento XDM** que creó en el paso anterior. Haga clic en **Seleccionar**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl8.png)

Entonces verás esto. Haga clic en **Mantener cambios**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl9.png)

Entonces verás esto. Haga clic en **Guardar**.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl10.png)

Ahora ha configurado la primera regla en una propiedad Event Forwarding . Vaya a **Flujo de publicación** para publicar los cambios.
Abra la biblioteca de desarrollo. **Principal** haciendo clic en **Editar** como se indica.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl11.png)

Haga clic en el **Agregar todos los recursos modificados** , después de lo cual verá su Regla y el Elemento de datos en esta biblioteca. A continuación, haga clic en **Guardar y generar para desarrollo**. Los cambios se están implementando.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl13.png)

Después de un par de minutos, verá que la implementación ha finalizado y está lista para probarse.

![SSF de recopilación de datos de Adobe Experience Platform](./images/rl14.png)

## 14.3.4 Probar la configuración

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión en Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](../module0/images/web8.png)

Ahora puede seguir el flujo siguiente para acceder al sitio web. Haga clic en **Integraciones**.

![DSN](../module0/images/web1.png)

En el **Integraciones** , debe seleccionar la propiedad Recopilación de datos que se creó en el ejercicio 0.1.

![DSN](../module0/images/web2.png)

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

Cuando abra la vista del desarrollador del explorador, podrá inspeccionar las solicitudes de red como se indica a continuación. Al utilizar el filtro **interactuar**, verá las solicitudes de red que envía el cliente de recopilación de datos de Adobe Experience Platform a Adobe Edge.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/hook1.png)

Si selecciona la carga útil sin procesar, vaya a [https://jsonformatter.org/json-pretty-print](https://jsonformatter.org/json-pretty-print) y pegue la carga útil. Haga clic en **Convertir en bonita**. A continuación, verá la carga útil JSON, la variable **events** y **xdm** objeto. En uno de los pasos anteriores, cuando definió el elemento de datos, utilizó la referencia **arc.event.xdm**, lo que le resultará en el análisis de la variable **xdm** de esta carga útil.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/hook2.png)

Cambie la vista al sitio web [https://webhook.site/](https://webhook.site/) que utilizó en uno de los pasos anteriores. Ahora debería tener una vista similar a esta, con solicitudes de red mostradas en el menú de la izquierda. Está viendo el **xdm** carga útil que se filtró fuera de la solicitud de red que se mostró arriba.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/hook3.png)

Desplácese hacia abajo un poco en la carga útil para encontrar el nombre de la página, que en este caso es **vangeluw-OCUC** (que es el nombre del proyecto de su sitio web de demostración).

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/hook4.png)

Si ahora navega por el sitio web, verá solicitudes de red adicionales que estarán disponibles en este enlace web personalizado en tiempo real.

![Configuración de la recopilación de datos de Adobe Experience Platform](./images/hook5.png)

Ya ha configurado el reenvío del lado del servidor de las cargas útiles de SDK web/XDM en un enlace web personalizado externo. En los próximos ejercicios, configurará un enfoque similar y enviará esos mismos datos a los entornos de Google y AWS.

Paso siguiente: [14.4 Crear y configurar una función de nube de Google](./ex4.md)

[Volver al módulo 14](./aep-data-collection-ssf.md)

[Volver a todos los módulos](./../../overview.md)
