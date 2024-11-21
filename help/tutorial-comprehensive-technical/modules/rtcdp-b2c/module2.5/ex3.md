---
title: 'Recopilación de datos de Adobe Experience Platform y reenvío del lado del servidor en tiempo real: creación y configuración de un webhook personalizado'
description: Crear y configurar un webhook personalizado
kt: 5342
doc-type: tutorial
exl-id: bb712980-5910-4f01-976b-b7fcf03f5407
source-git-commit: 7779e249b4ca03c243cf522811cd81370002d51a
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 1%

---

# 2.5.3 Crear y configurar un webhook personalizado

## Cree su webhook personalizado

Vaya a [https://pipedream.com/requestbin](https://pipedream.com/requestbin). Ya usó esta aplicación en [SDK de destinos de Ejercicio 2.3.7](./../../../modules/rtcdp-b2c/module2.3/ex7.md)

Si aún no ha utilizado ese servicio, cree una cuenta de y, a continuación, un espacio de trabajo. Una vez creado el espacio de trabajo, verá algo similar a esto.

Haga clic en **copiar** para copiar la dirección URL. Deberá especificar esta dirección URL en el siguiente ejercicio. La dirección URL de este ejemplo es `https://eodts05snjmjz67.m.pipedream.net`.

![demostración](./images/webhook1.png)

Este sitio web ha creado este webhook para usted, y usted podrá configurarlo en su **[!DNL Event Forwarding property]** para comenzar a probar el reenvío de eventos.

## Actualizar la propiedad de reenvío de eventos: Crear un elemento de datos

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) y luego a **Reenvío de eventos**. Busque la propiedad Reenvío de eventos y haga clic en ella para abrirla.

![Recopilación de datos Adobe Experience Platform SSF](./images/prop1.png)

En el menú de la izquierda, vaya a **Elementos de datos**. Haga clic en **Crear nuevo elemento de datos**.

![Recopilación de datos Adobe Experience Platform SSF](./images/de1.png)

A continuación, verá un nuevo elemento de datos para configurar.

![Recopilación de datos Adobe Experience Platform SSF](./images/de2.png)

Realice la siguiente selección:

- Como **Nombre**, introduzca **Evento XDM**.
- Como la **extensión**, seleccione **Principal**.
- Como **Tipo de elemento de datos**, seleccione **Ruta**.
- Como **Ruta**, seleccione **Leer datos de XDM (arc.event.xdm)**. Al seleccionar esta ruta, filtrará la sección **XDM** de la carga útil de evento que el sitio web o la aplicación móvil envían a Adobe Edge.

![Recopilación de datos Adobe Experience Platform SSF](./images/de3.png)

Ahora vas a tener esto. Haga clic en **Guardar**.

![Recopilación de datos Adobe Experience Platform SSF](./images/de3a.png)

>[!NOTE]
>
>En la ruta anterior, se hace referencia a **arc**. **arc** significa Contexto de recursos de Adobe y **arc** siempre representa el objeto más alto disponible en el contexto del lado del servidor. Se pueden agregar enriquecimientos y transformaciones a ese objeto **arc** mediante las funciones del servidor de recopilación de datos de Adobe Experience Platform.
>
>En la ruta anterior, se hace referencia a **event**. **event** significa un evento único y el servidor de recopilación de datos de Adobe Experience Platform siempre evaluará cada evento de forma individual. A veces, es posible que vea una referencia a **events** en la carga útil enviada por el lado del cliente del SDK web, pero en el servidor de recopilación de datos de Adobe Experience Platform, cada evento se evalúa individualmente.

## Actualizar la propiedad del servidor de recopilación de datos de Adobe Experience Platform: Crear una regla

En el menú de la izquierda, ve a **Reglas**. Haga clic en **Crear nueva regla**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl1.png)

A continuación, verá una nueva regla para configurar. Escriba **Nombre**: **Todas las páginas**. Para este ejercicio, no es necesario configurar una condición. En su lugar, configurará una acción. Haga clic en el botón **+ Agregar** en **Acciones**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl2.png)

Entonces verá esto... Realice la siguiente selección:

- Seleccione la **extensión**: **Conector de nube de Adobe**.
- Seleccione el **Tipo de acción**: **Realizar llamada de recuperación**.

Esto debería proporcionarle este **Nombre**: **Conector de nube de Adobe - Realizar llamada de búsqueda**. Ahora debería ver esto:

![Recopilación de datos Adobe Experience Platform SSF](./images/rl4.png)

A continuación, configure lo siguiente:

- Cambiar el método de solicitud de GET a **POST**
- Escriba la dirección URL del webhook personalizado que creó en uno de los pasos anteriores, que tiene este aspecto: `https://eodts05snjmjz67.m.pipedream.net`

Ahora debería tener esto. A continuación, vaya a **Cuerpo**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl6.png)

Entonces verá esto... Haga clic en el icono de elemento de datos como se indica a continuación.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl7.png)

En la ventana emergente, seleccione el elemento de datos **Evento XDM** que creó en el paso anterior. Haga clic en **Seleccionar**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl8.png)

Entonces verá esto... Haga clic en **Conservar cambios**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl9.png)

Entonces verá esto... Haga clic en **Guardar**.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl10.png)

Ahora ha configurado la primera regla en una propiedad de reenvío de eventos. Vaya a **Flujo de publicación** para publicar los cambios.
Abra la biblioteca de desarrollo **Main** haciendo clic en **Editar** como se indica.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl11.png)

Haga clic en el botón **Agregar todos los recursos modificados**, tras lo cual verá que la regla y el elemento de datos aparecen en esta biblioteca. A continuación, haga clic en **Guardar y generar para desarrollo**. Los cambios se están implementando.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl13.png)

Después de un par de minutos, verá que la implementación está completa y lista para probarse.

![Recopilación de datos Adobe Experience Platform SSF](./images/rl14.png)

## Pruebe la configuración

Vaya a [https://dsn.adobe.com](https://dsn.adobe.com). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en los 3 puntos **...** del proyecto del sitio web y, a continuación, haga clic en **Ejecutar** para abrirlo.

![DSN](./../../datacollection/module1.1/images/web8.png)

A continuación, verá cómo se abre el sitio web de demostración. Seleccione la URL y cópiela en el portapapeles.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Abra una nueva ventana del explorador de incógnito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Pegue la dirección URL del sitio web de demostración, que copió en el paso anterior. Luego se le pedirá que inicie sesión con su Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleccione el tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Luego verá el sitio web cargado en una ventana de incógnito del explorador. Para cada ejercicio, deberá utilizar una ventana nueva del explorador de incógnito para cargar la URL del sitio web de demostración.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Cuando abra la Vista de desarrollador del explorador, puede inspeccionar las Solicitudes de red como se indica a continuación. Cuando use el filtro **interaction**, verá las solicitudes de red que envía el cliente de recopilación de datos de Adobe Experience Platform a Adobe Edge.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hook1.png)

Si selecciona la carga útil sin procesar, vaya a [https://jsonformatter.org/json-pretty-print](https://jsonformatter.org/json-pretty-print) y pegue la carga útil. Haga clic en **Minificar / Beautify**. Verá la carga útil JSON, el objeto **events** y el objeto **xdm**. En uno de los pasos anteriores, al definir el elemento de datos, utilizó la referencia **arc.event.xdm**, que le permitirá analizar el objeto **xdm** de esta carga.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hook2.png)

Cambie la vista al webhook personalizado [https://pipedream.com/requestbin](https://pipedream.com/requestbin) que utilizó en uno de los pasos anteriores. Ahora debería tener una vista similar a esta, con las solicitudes de red mostradas en el menú de la izquierda. Está viendo la carga útil **xdm** que se filtró fuera de la solicitud de red que se mostró arriba.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hook3.png)

Desplácese un poco hacia abajo en la carga para encontrar el nombre de página, que en este caso es **home**.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hook4.png)

Si ahora navega por el sitio web, verá solicitudes de red adicionales disponibles en este webhook personalizado en tiempo real.

![Configuración de recopilación de datos de Adobe Experience Platform](./images/hook5.png)

Ahora ha configurado el reenvío de eventos del lado del servidor de las cargas útiles del SDK web/XDM en un webhook personalizado externo. En los próximos ejercicios, configurará un enfoque similar y enviará esos mismos datos hacia Google Cloud Platform y AWS.

Siguiente paso: [2.5.4 Reenviar eventos a GCP Pub/Sub](./ex4.md)

[Volver al módulo 2.5](./aep-data-collection-ssf.md)

[Volver a todos los módulos](./../../../overview.md)
