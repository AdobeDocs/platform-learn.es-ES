---
title: Bootcamp - Fusión física y digital - Journey Optimizer Cree su recorrido y notificación push
description: Bootcamp - Fusión física y digital - Journey Optimizer Cree su recorrido y notificación push
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: be8c23ec-c5f8-4abc-849f-994446072a84
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 2%

---

# 3.3 Crear el recorrido y las notificaciones push

En este ejercicio, configurará el recorrido y el mensaje que deben activarse cuando alguien entre en una señalización mediante la aplicación móvil.

Inicie sesión en Adobe Journey Optimizer accediendo a [Adobe Experience Cloud](https://experience.adobe.com). Clic **Journey Optimizer**.

![ACOP](./images/acophome.png)

Se le redirigirá a la variable **Inicio**  ver en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. Se llama a la zona protegida que se va a utilizar `Bootcamp`. Para cambiar de una zona protegida a otra, haga clic en **Prod** y seleccione la zona protegida de la lista. En este ejemplo, la zona protegida se denomina **Bootcamp**. Entonces estarás en el... **Inicio** vista de la zona protegida `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Creación de un recorrido

En el menú izquierdo, haga clic en **Recorridos**. A continuación, haga clic en **Crear Recorrido** para crear un nuevo recorrido.

![ACOP](./images/createjourney.png)

A continuación, verá una pantalla de recorrido vacía.

![ACOP](./images/journeyempty.png)

En el ejercicio anterior creó un nuevo **Evento**. Lo llamaste así `yourLastNameBeaconEntryEvent` y reemplazado `yourLastName` con tu apellido. Este fue el resultado de la creación del Evento:

![ACOP](./images/eventdone.png)

Ahora debe tomar este evento como inicio de este Recorrido. Para ello, vaya al lado izquierdo de la pantalla y busque el evento en la lista de eventos.

![ACOP](./images/eventlist.png)

Seleccione el evento, arrástrelo y suéltelo en el lienzo de recorrido. Su recorrido ahora tiene este aspecto. Clic **Ok** para guardar los cambios.

![ACOP](./images/journeyevent.png)

Como segundo paso en el recorrido, debe agregar un **Push** acción. Vaya al lado izquierdo de la pantalla para **Acciones**, seleccione la **Push** acción y, a continuación, arrástrela y suéltela en el segundo nodo del recorrido.

![ACOP](./images/journeyactions.png)

A la derecha de la pantalla, debe crear la notificación push.

Configure las variables **Categoría** hasta **Marketing** y seleccione una superficie push que le permita enviar notificaciones push. En este caso, la superficie de inserción que se va a seleccionar es **mmeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Crear el mensaje

Clic **Editar contenido**.

![ACOP](./images/emptymsg.png)

A continuación, verá esto:

![ACOP](./images/emailmsglist.png)

Definamos el contenido de la notificación push.

Haga clic en **Título** campo de texto.

![Journey Optimizer](./images/msg5.png)

En el área de texto, empiece a escribir **Hola**. Haga clic en el icono de personalización.

![Journey Optimizer](./images/msg6.png)

Ahora debe introducir el token de personalización para el campo **Nombre** que se almacena en `profile.person.name.firstName`. En el menú izquierdo, seleccione **Atributos de perfil**, desplácese hacia abajo/navegue hasta encontrar la **Persona** y haga clic en la flecha para profundizar hasta llegar al campo `profile.person.name.firstName`. Haga clic en **+** para añadir el campo al lienzo. Haga clic en **Guardar**.

![Journey Optimizer](./images/msg7.png)

Entonces volverás a estar aquí. Haga clic en el icono de personalización junto al campo **Cuerpo**.

![Journey Optimizer](./images/msg11.png)

En el área de texto, escriba `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

A continuación, haga clic en **Atributos contextuales** y luego **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clic **Eventos**.

![ACOP](./images/jomsg4.png)

Haga clic en el nombre del evento, que debería tener este aspecto: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clic **Contexto del lugar**.

![ACOP](./images/jomsg6.png)

Clic **Interacción del PDI**.

![ACOP](./images/jomsg7.png)

Clic **Detalles del PDI**.

![ACOP](./images/jomsg8.png)

Haga clic en **+** icono en **Nombre del PDI**.
Entonces verá esto... Haga clic en **Guardar**.

![ACOP](./images/jomsg9.png)

El mensaje ya está listo. Haga clic en la flecha de la esquina superior izquierda para volver al recorrido.

![ACOP](./images/jomsg11.png)

Haga clic en **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Enviar un mensaje a una pantalla

Como tercer paso del recorrido, debe agregar una **sendMessageToScreen** acción. Vaya al lado izquierdo de la pantalla para **Acciones**, seleccione la **sendMessageToScreen** acción y, a continuación, arrástrela y suéltela en el tercer nodo del recorrido. Entonces verá esto...

![ACOP](./images/jomsg15.png)

El **sendMessageToScreen** acción es una acción personalizada que publicará un mensaje en el extremo que utiliza la visualización en tienda. El **sendMessageToScreen** action espera que se definan varias variables. Puede ver esas variables desplazándose hacia abajo hasta que vea **Parámetros de acción**.

![ACOP](./images/jomsg16.png)

Ahora debe establecer los valores de cada parámetro de acción. Siga esta tabla para comprender qué valores se requieren dónde.

| Parámetro | valor |
|:-------------:| :---------------:|
| ENVÍO | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| NOMBRE | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| ZONA PROTEGIDA | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style="table-layout:auto"}

Para definir estos valores, haga clic en **Editar** icono.

![ACOP](./images/jomsg17.png)

A continuación, seleccione **Modo avanzado**.

![ACOP](./images/jomsg18.png)

A continuación, pegue el valor en función de la tabla anterior. Haga clic en **Ok**.

![ACOP](./images/jomsg19.png)

Repita este proceso para agregar valores a cada campo.

>[!IMPORTANT]
>
>Para el ECID de campo, hay una referencia al evento `yourLastNameBeaconEntryEvent`. Asegúrese de reemplazar `yourLastName` por tu apellido.

El resultado final debería ser similar al siguiente:

![ACOP](./images/jomsg20.png)

Desplazarse arriba y hacer clic **Ok**.

![ACOP](./images/jomsg21.png)

Aún necesita darle un Nombre a su recorrido. Para ello, haga clic en el icono **Propiedades** en la parte superior derecha de la pantalla.

![ACOP](./images/journeyname.png)

A continuación, puede introducir el nombre del recorrido aquí. Utilice `yourLastName - Beacon Entry Journey`. Clic **OK** para guardar los cambios.

![ACOP](./images/journeyname1.png)

Ahora puede publicar el recorrido haciendo clic en **Publish**.

![ACOP](./images/publishjourney.png)

Clic **Publish** otra vez.

![ACOP](./images/publish1.png)

A continuación, verá una barra de confirmación verde que indica que el recorrido se ha publicado.

![ACOP](./images/published.png)

El recorrido ya está activo y se puede activar.

Ya ha terminado este ejercicio.

Paso siguiente: [3.4 Probar el recorrido](./ex4.md)

[Volver al flujo de usuario 3](./uc3.md)

[Volver a todos los módulos](../../overview.md)
