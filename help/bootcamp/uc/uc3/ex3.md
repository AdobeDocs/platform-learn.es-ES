---
title: Bootcamp - Fusión física y digital - Journey Optimizer Cree su recorrido y notificaciones push
description: Bootcamp - Fusión física y digital - Journey Optimizer Cree su recorrido y notificaciones push
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: be8c23ec-c5f8-4abc-849f-994446072a84
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 3%

---

# 3.3 Crear el recorrido y las notificaciones push

En este ejercicio, debe configurar el recorrido y el mensaje que deben activarse cuando alguien introduce una señalización mediante la aplicación móvil.

Inicie sesión en Adobe Journey Optimizer desde [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./images/acophome.png)

Se le redirigirá al **Página principal**  en Journey Optimizer. En primer lugar, asegúrese de que está utilizando el simulador para pruebas correcto. El entorno limitado que se va a usar se denomina `Bootcamp`. Para cambiar de un simulador de pruebas a otro, haga clic en **Prod** y seleccione el simulador de pruebas de la lista. En este ejemplo, el simulador de pruebas recibe el nombre **Bootcamp**. Entonces estará en el **Página principal** vista del entorno limitado `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Crear su recorrido

En el menú de la izquierda, haga clic en **Recorridos**. A continuación, haga clic en **Crear Recorrido** para crear un nuevo recorrido.

![ACOP](./images/createjourney.png)

A continuación, verá una pantalla de recorrido vacía.

![ACOP](./images/journeyempty.png)

En el ejercicio anterior, creó una **Evento**. Lo llamaste así `yourLastNameBeaconEntryEvent` y sustituido `yourLastName` con su apellido. Este fue el resultado de la creación del evento:

![ACOP](./images/eventdone.png)

Ahora debe tomar este evento como el inicio de este Recorrido. Para ello, vaya a la izquierda de la pantalla y busque el evento en la lista de eventos.

![ACOP](./images/eventlist.png)

Seleccione el evento, arrástrelo y suéltelo en el lienzo del recorrido. Tu recorrido ahora se ve así. Haga clic en **Ok** para guardar los cambios.

![ACOP](./images/journeyevent.png)

Como segundo paso en el recorrido, debe agregar una **Push** acción. Vaya al lado izquierdo de la pantalla para **Acciones**, seleccione **Push** a continuación, arrástrela y colóquela en el segundo nodo del recorrido.

![ACOP](./images/journeyactions.png)

A la derecha de la pantalla, debe crear la notificación push.

Configure las variables **Categoría** a **Marketing** y seleccione una superficie push que le permita enviar notificaciones push. En este caso, la superficie push que se va a seleccionar es **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Crear su mensaje

Haga clic en **Editar contenido**.

![ACOP](./images/emptymsg.png)

Verá esto:

![ACOP](./images/emailmsglist.png)

Definamos el contenido de la notificación push.

Haga clic en el **Título** campo de texto.

![Journey Optimizer](./images/msg5.png)

En el área de texto empiece a escribir **Hi**. Haga clic en el icono de personalización.

![Journey Optimizer](./images/msg6.png)

Ahora necesita introducir el token de personalización para el campo **Nombre** que se almacenan en `profile.person.name.firstName`. En el menú de la izquierda, seleccione **Atributos de perfil**, desplácese hacia abajo o navegue hasta encontrar la variable **Persona** y haga clic en la flecha para ir un nivel más profundo hasta que alcance el campo `profile.person.name.firstName`. Haga clic en el **+** para añadir el campo al lienzo. Haga clic en **Guardar**.

![Journey Optimizer](./images/msg7.png)

Volverás aquí. Haga clic en el icono de personalización situado junto al campo . **Cuerpo**.

![Journey Optimizer](./images/msg11.png)

En el área de texto, escriba `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

A continuación, haga clic en **Atributos contextuales** y luego **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Haga clic en **Eventos**.

![ACOP](./images/jomsg4.png)

Haga clic en el nombre del evento, que debería tener este aspecto: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Haga clic en **Contexto del lugar**.

![ACOP](./images/jomsg6.png)

Haga clic en **Interacción de puntos de interés**.

![ACOP](./images/jomsg7.png)

Haga clic en **Detalle del punto de interés**.

![ACOP](./images/jomsg8.png)

Haga clic en el **+** icono **Nombre de punto de interés**.
Entonces verás esto. Haga clic en **Guardar**.

![ACOP](./images/jomsg9.png)

El mensaje ya está listo. Haga clic en la flecha situada en la esquina superior izquierda para volver al recorrido.

![ACOP](./images/jomsg11.png)

Haga clic en **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Enviar un mensaje a una pantalla

Como tercer paso en el recorrido, debe agregar una **sendMessageToScreen** acción. Vaya al lado izquierdo de la pantalla para **Acciones**, seleccione **sendMessageToScreen** a continuación, arrástrela y suéltela en el tercer nodo del recorrido. Entonces verás esto.

![ACOP](./images/jomsg15.png)

La variable **sendMessageToScreen** es una acción personalizada que publica un mensaje en el extremo que usa la visualización en la tienda. La variable **sendMessageToScreen** action espera que se definan varias variables. Para ver estas variables, desplácese hacia abajo hasta que vea **Parámetros de acción**.

![ACOP](./images/jomsg16.png)

Ahora debe establecer los valores para cada parámetro de acción. Siga esta tabla para comprender qué valores se requieren.

| Parámetro | valor |
|:-------------:| :---------------:|
| ENTREGA | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| NOMBRE | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| SANDBOX | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style=&quot;table-layout:auto&quot;}

Para establecer estos valores, haga clic en el botón **Editar** icono.

![ACOP](./images/jomsg17.png)

A continuación, seleccione **Modo avanzado**.

![ACOP](./images/jomsg18.png)

A continuación, pegue el valor en función de la tabla anterior. Haga clic en **Ok**.

![ACOP](./images/jomsg19.png)

Repita este proceso para añadir valores para cada campo.

>[!IMPORTANT]
>
>Para el campo ECID, hay una referencia al evento `yourLastNameBeaconEntryEvent`. Asegúrese de reemplazar `yourLastName` por su apellido.

El resultado final debería tener este aspecto:

![ACOP](./images/jomsg20.png)

Desplácese hacia arriba y haga clic en **Ok**.

![ACOP](./images/jomsg21.png)

Aún necesita darle un Nombre a su recorrido. Para ello, haga clic en el botón **Propiedades** en la parte superior derecha de la pantalla.

![ACOP](./images/journeyname.png)

A continuación, puede introducir el nombre del recorrido aquí. Utilice `yourLastName - Beacon Entry Journey`. Haga clic en **OK** para guardar los cambios.

![ACOP](./images/journeyname1.png)

Ahora puede publicar el recorrido haciendo clic en **Publicación**.

![ACOP](./images/publishjourney.png)

Haga clic en **Publicación** de nuevo.

![ACOP](./images/publish1.png)

A continuación, verá una barra de confirmación verde que indica que su recorrido se ha publicado.

![ACOP](./images/published.png)

El recorrido ya está activo y se puede activar.

Ya has terminado este ejercicio.

Paso siguiente: [3.4 Probar el recorrido](./ex4.md)

[Volver al flujo de usuario 3](./uc3.md)

[Volver a todos los módulos](../../overview.md)
