---
title: Bootcamp - Journey Optimizer Cree su recorrido y mensaje de correo electrónico
description: Bootcamp - Journey Optimizer Cree su recorrido y mensaje de correo electrónico
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: 138a70fa-fe50-4585-b47f-150db4770c3d
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 2.3 Crear el recorrido y el mensaje de correo electrónico

En este ejercicio, configurará el recorrido que debe activarse cuando alguien cree una cuenta en el sitio web de demostración.

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `Bootcamp`. Para cambiar de una zona protegida a otra, haga clic en **Prod** y seleccione la zona protegida en la lista. En este ejemplo, la zona protegida se llama **Bootcamp**. Estará en la vista **Inicio** de su zona protegida `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Creación de un recorrido

En el menú de la izquierda, haga clic en **Recorridos**. A continuación, haga clic en **Crear Recorrido** para crear un nuevo recorrido.

![ACOP](./images/createjourney.png)

A continuación, verá una pantalla de recorrido vacía.

![ACOP](./images/journeyempty.png)

En el ejercicio anterior creó un nuevo **evento**. Lo nombró de esta manera `yourLastNameAccountCreationEvent` y reemplazó a `yourLastName` con su apellido. Este fue el resultado de la creación del Evento:

![ACOP](./images/eventdone.png)

Ahora debe tomar este evento como inicio de este Recorrido. Para ello, vaya al lado izquierdo de la pantalla y busque el evento en la lista de eventos.

![ACOP](./images/eventlist.png)

Seleccione el evento, arrástrelo y suéltelo en el lienzo de Recorrido. El Recorrido ahora tiene este aspecto:

![ACOP](./images/journeyevent.png)

Como segundo paso en el recorrido, debe agregar un breve paso **Wait**. Vaya al lado izquierdo de la pantalla a la sección **Orchestration** para encontrarlo. Utilizará atributos de perfil y debe asegurarse de que se rellenan en el Perfil del cliente en tiempo real.

![ACOP](./images/journeywait.png)

Su recorrido ahora tiene este aspecto. En el lado derecho de la pantalla debe configurar el tiempo de espera. Configúrelo en 1 minuto. Esto le dará tiempo suficiente para que los atributos de perfil estén disponibles después de que se active el evento.

![ACOP](./images/journeywait1.png)

Haga clic en **Aceptar** para guardar los cambios.

Como tercer paso del recorrido, debes agregar una acción **Correo electrónico**. Vaya al lado izquierdo de la pantalla a **Actions**, seleccione la acción **Email** y arrástrela y suéltela en el segundo nodo del recorrido. Ahora puede ver esto.

![ACOP](./images/journeyactions.png)

Defina **Category** en **Marketing** y seleccione una superficie de correo electrónico que le permita enviar correo electrónico. En este caso, la superficie de correo electrónico que se va a seleccionar es **Correo electrónico**. Asegúrese de que las casillas de verificación de **Clics en el correo electrónico** y **aperturas del correo electrónico** estén habilitadas.

![ACOP](./images/journeyactions1.png)

El siguiente paso es crear el mensaje. Para ello, haga clic en **Editar contenido**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Crear el mensaje

Para crear tu mensaje, haz clic en **Editar contenido**.

![ACOP](./images/journeyactions2.png)

Ahora puede ver esto.

![ACOP](./images/journeyactions3.png)

Haga clic en el campo de texto **Línea de asunto**.

![Journey Optimizer](./images/msg5.png)

Empiece a escribir **Hola** en el área de texto

![Journey Optimizer](./images/msg6.png)

La línea de asunto aún no ha finalizado. A continuación, debe traer el token de personalización para el campo **Nombre** que se almacena en `profile.person.name.firstName`. En el menú de la izquierda, desplácese hacia abajo para encontrar el elemento **Person** y haga clic en la flecha para ir un nivel más profundo.

![Journey Optimizer](./images/msg7.png)

Ahora encuentra el elemento **Nombre completo** y haz clic en la flecha para ir un nivel más profundo.

![Journey Optimizer](./images/msg8.png)

Finalmente, busque el campo **Nombre** y haga clic en el signo **+** que está al lado. A continuación, verá aparecer el token de personalización en el campo de texto.

![Journey Optimizer](./images/msg9.png)

A continuación, agregue el texto **, ¡gracias por registrarse!**. Haga clic en **Guardar**.

![Journey Optimizer](./images/msg10.png)

Entonces volverás a estar aquí. Haga clic en **Enviar correo electrónico a Designer** para crear el contenido del correo electrónico.

![Journey Optimizer](./images/msg11.png)

En la siguiente pantalla, se le solicitarán tres métodos diferentes para proporcionar el contenido del correo electrónico:

- **Diseñe desde cero**: Comience con un lienzo en blanco y utilice el editor WYSIWYG para arrastrar y soltar componentes de estructura y contenido para crear visualmente el contenido del correo electrónico.
- **Codifique su propia**: cree su propia plantilla de correo electrónico codificándola con el HTML
- **HTML de importación**: importe una plantilla de HTML existente que podrá editar.

Haga clic en **Importar HTML**. También puede hacer clic en **Plantillas guardadas** y seleccionar la plantilla **Bootcamp - Plantilla de correo electrónico**.

![Journey Optimizer](./images/msg12.png)

Si seleccionó **HTML de importación**, ahora puede arrastrar y soltar el archivo **mailtemplatebootcamp.html**, que puede descargar [aquí](../../assets/html/mailtemplatebootcamp.html.zip). Haga clic en Importar.

![Journey Optimizer](./images/msg13.png)

A continuación, verá esta plantilla de correo electrónico predeterminada:

![Journey Optimizer](./images/msg14.png)

Vamos a personalizar el correo electrónico. Haz clic junto al texto **Hola** y luego haz clic en el icono **Agregar Personalization**.

![Journey Optimizer](./images/msg35.png)

A continuación, debe traer el token de personalización **First name** que se almacena en `profile.person.name.firstName`. En el menú, busque el elemento **Person**, explore en profundidad el elemento **Nombre completo** y, a continuación, haga clic en el icono **+** para agregar el campo Nombre al editor de expresiones.

Haga clic en **Guardar**.

![Journey Optimizer](./images/msg36.png)

Ahora notará cómo se ha agregado el campo de personalización al texto.

![Journey Optimizer](./images/msg37.png)

Haz clic en **Guardar** para guardar el mensaje.

![Journey Optimizer](./images/msg55.png)

Vuelva al panel de mensajes haciendo clic en la **flecha** junto al texto de la línea de asunto en la esquina superior izquierda.

![Journey Optimizer](./images/msg56.png)

Ha completado la creación del correo electrónico de registro. Haga clic en la flecha de la esquina superior izquierda para volver al recorrido.

![Journey Optimizer](./images/msg57.png)

Haga clic en **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publish su recorrido

Aún necesita darle un Nombre a su recorrido. Para ello, haz clic en el icono **Lápiz** en la parte superior izquierda de la pantalla.

![ACOP](./images/journeyname.png)

A continuación, puede introducir el nombre del recorrido aquí. Use `yourLastName - Account Creation Journey`. Haga clic en **Aceptar** para guardar los cambios.

![ACOP](./images/journeyname1.png)

Ahora puede publicar su recorrido haciendo clic en **Publish**.

![ACOP](./images/publishjourney.png)

Vuelva a hacer clic en **Publish**.

![ACOP](./images/publish1.png)

A continuación, verá una barra de confirmación verde que indica que el recorrido se ha publicado.

![ACOP](./images/published.png)

Ya ha terminado este ejercicio.

Siguiente paso: [2.4 Prueba tu recorrido](./ex4.md)

[Volver al flujo de usuario 2](./uc2.md)

[Volver a todos los módulos](../../overview.md)