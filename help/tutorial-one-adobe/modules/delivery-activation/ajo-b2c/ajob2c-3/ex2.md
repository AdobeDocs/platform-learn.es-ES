---
title: Configuración de un recorrido con mensajes push
description: Configuración de un recorrido con mensajes push
kt: 5342
doc-type: tutorial
source-git-commit: 203590e3289d2e5342085bf8b6b4e3cd11859539
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 2%

---

# 3.3.2 Configuración de un recorrido con mensajes push


## 3.4.4.6 Crear un nuevo evento

Ir a **Journey Optimizer**. En el menú de la izquierda, ve a **Configuraciones** y haz clic en **Administrar** en **Eventos**.

![ACOP](./images/acopmenu.png)

En la pantalla **Eventos**, verá una vista similar a esta. Haga clic en **Crear evento**.

![ACOP](./images/add.png)

A continuación, verá una configuración de evento vacía.
En primer lugar, asigne al evento un Nombre como este: `--aepUserLdap--StoreEntryEvent` y establezca la descripción en `Store Entry Event`.
A continuación se muestra la selección **Tipo de evento**. Seleccione **Unitario**.
A continuación se muestra la selección **Tipo de ID de evento**. Seleccione **Sistema generado**.

![ACOP](./images/eventname.png)

A continuación se muestra la selección Esquema. Se ha preparado un esquema para este ejercicio. Use el esquema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

Después de seleccionar el esquema, verá una serie de campos seleccionados en la sección **Carga útil**. El evento está ahora completamente configurado.

Haga clic en **Guardar**.

![ACOP](./images/eventschema.png)

El evento se ha configurado y guardado. Vuelve a hacer clic en el evento para abrir de nuevo la pantalla **Editar evento**.

![ACOP](./images/eventdone.png)

Pase el ratón sobre el campo **Carga útil** y haga clic en el icono **Ver carga útil**.

![ACOP](./images/hover.png)

Ahora verá un ejemplo de la carga útil esperada.

Su evento tiene un identificador de evento de orquestación único, que puede encontrar desplazándose hacia abajo en esa carga hasta que vea `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

El ID de evento es lo que debe enviarse a Adobe Experience Platform para almacenar en déclencheur el Recorrido que va a generar en el siguiente paso. Escriba este eventID, tal como lo necesitará en el paso siguiente.
`"eventID": "89acd341ec2b7d1130c9a73535029debf2ac35f486bc99236b1a5091d6f4bc68"`

Haga clic en **Aceptar**, seguido de **Cancelar**.

## 3.4.4.7 Crear un recorrido

En el menú, ve a **Recorridos** y haz clic en **Crear Recorrido**.

![DSN](./images/sjourney1.png)

Entonces verá esto... Dé un nombre a su recorrido. Usar `--aepUserLdap-- - Store Entry journey`. Haga clic en **Guardar**.

![DSN](./images/sjourney3.png)

En primer lugar, debe agregar el evento como punto de partida del recorrido. Busque el evento `--aepUserLdap--StoreEntryEvent`, arrástrelo y suéltelo en el lienzo. Haga clic en **Guardar**.

![DSN](./images/sjourney4.png)

A continuación, en **Acciones**, busque la acción **Push**. Arrastre y suelte la acción **Push** en el lienzo.

Establezca **Category** en **Marketing** y seleccione una superficie push que le permita enviar notificaciones push. En este caso, la superficie de correo electrónico que se va a seleccionar es **Push-iOS-Android**.

>[!NOTE]
>
>Debe existir un canal en Journey Optimizer que esté usando la **superficie de aplicación** tal como se revisó anteriormente.

![ACOP](./images/journeyactions1push.png)

El siguiente paso es crear el mensaje. Para ello, haga clic en **Editar contenido**.

![ACOP](./images/journeyactions2push.png)

Entonces verá esto... Haga clic en el icono **personalización** para el campo **Título**.

![Push](./images/bp5.png)

Entonces verá esto... Ahora puede seleccionar cualquier atributo de perfil directamente desde el Perfil del cliente en tiempo real.

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

Haga clic en **Guardar** para cerrar la acción de inserción.

![DSN](./images/sjourney8.png)

Haga clic en **Publicar**.

![DSN](./images/sjourney10.png)

Vuelva a hacer clic en **Publicar**.

![DSN](./images/sjourney10a.png)

El recorrido se ha publicado.

![DSN](./images/sjourney11.png)

## 3.4.4.8: probar el recorrido y el mensaje push

En la aplicación móvil DX Demo 2.0, ve a la pantalla **Configuración**. Haga clic en el botón **Entrada de tienda**.

>[!NOTE]
>
>El botón **Entrada de tienda** se está implementando en este momento. Aún no lo encontrará en la aplicación.

![DSN](./images/demo1b.png)

Asegúrese de cerrar la aplicación inmediatamente después de hacer clic en el icono **Entrada de la tienda**; de lo contrario, no se mostrará el mensaje push.

Después de un par de segundos, verá el mensaje.

![DSN](./images/demo2.png)

Ha terminado este ejercicio.

## Pasos siguientes

Ir a [3.3.3 Configurar una campaña con mensajes en la aplicación](./ex3.md){target="_blank"}

Volver a [Adobe Journey Optimizer: mensajes push y en la aplicación](ajopushinapp.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
