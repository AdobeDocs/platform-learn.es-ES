---
title: Mensajería en la aplicación de Adobe Journey Optimizer
description: Obtenga información sobre cómo crear mensajes en la aplicación para una aplicación móvil con el SDK móvil de Platform y Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
hide: true
source-git-commit: 7de7c7e13ea6d02f1193620e0cc35299e07d59e5
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 3%

---

# Mensajería en la aplicación de Adobe Journey Optimizer

Obtenga información sobre cómo crear mensajes en la aplicación para aplicaciones móviles con el SDK móvil de Platform y Adobe Journey Optimizer.

Journey Optimizer le permite crear sus recorridos y enviar mensajes en la aplicación a audiencias de destino. Antes de enviar mensajes en la aplicación con Journey Optimizer, debe asegurarse de que las configuraciones y integraciones adecuadas estén implementadas. Para comprender el flujo de datos de mensajería en la aplicación en Adobe Journey Optimizer, consulte [la documentación](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>Esta lección es opcional y solo se aplica a los usuarios de Adobe Journey Optimizer que buscan enviar mensajes en la aplicación.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.
* Acceso a Adobe Journey Optimizer y permisos suficientes, tal como se describe [aquí](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Además, necesita permisos suficientes para las siguientes funciones de Adobe Journey Optimizer.
   * Creación de una campaña.
* Cuenta de desarrollador de Apple de pago con acceso suficiente para crear certificados, identificadores y claves.
* Dispositivo o simulador físico de iOS para realizar pruebas.
* [ID de aplicación registrada con APN](journey-optimizer-push.md#register-app-id-with-apn)
* [Se han añadido las credenciales push de la aplicación en la recopilación de datos](journey-optimizer-push.md#add-your-app-push-credentials-in-data-collection)
* [Extensión de etiquetas de Adobe Journey Optimizer instalada](journey-optimizer-push.md#install-adobe-journey-optimizer-tags-extension)
* [Se ha implementado Adobe Journey Optimizer en la aplicación](journey-optimizer-push.md#implement-adobe-journey-optimizer-in-the-app)


## Validar con Assurance

1. Revise la [instrucciones de configuración](assurance.md) sección.
1. Instale la aplicación en su dispositivo físico o en el simulador.
1. Inicie la aplicación mediante la URL generada por Assurance.
1. En la IU de Assurance, seleccione **[!UICONTROL Configurar]**.
   ![configurar clic](assets/push-validate-config.png)
1. Seleccione el ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) botón situado junto a **[!UICONTROL Mensajería en la aplicación]**.
1. Seleccione **[!UICONTROL Guardar]**.
   ![guardar](assets/assurance-in-app-config.png)
1. Seleccionar **[!UICONTROL Mensajería en la aplicación]** en el panel de navegación izquierdo.
1. Seleccione el **[!UICONTROL Validación]** pestaña.
1. Confirme que no está recibiendo ningún error.
   ![Validación en la aplicación](assets/assurance-in-app-validate.png)


## Cree su propio mensaje en la aplicación

Para crear su propio mensaje en la aplicación, debe definir una campaña en Journey Optimizer que almacene en déclencheur un mensaje en la aplicación en función de los eventos que se produzcan. Estos eventos pueden ser:

* datos enviados a Adobe Experience Platform,
* eventos de seguimiento principales, como la acción o el estado o la recopilación de datos PII, a través de las API genéricas principales de Mobile,
* eventos del ciclo vital de la aplicación, como inicio, instalación, actualización, cierre o bloqueo,
* eventos de geolocalización, como entrar o salir de un punto de interés.

En este tutorial, va a utilizar las API principales genéricas e independientes de la extensión de Mobile para facilitar el seguimiento de eventos de pantallas de usuario, acciones y datos PII. Los eventos generados por estas API se publican en el centro de eventos del SDK y las extensiones los pueden utilizar. Por ejemplo, cuando se instala la extensión de Analytics, todas las acciones del usuario y los datos de evento de las pantallas de la aplicación se envían a los extremos de los informes de Analytics correspondientes.

1. En la IU de Journey Optimizer, seleccione **[!UICONTROL Campañas]** desde el carril izquierdo.
1. Seleccionar **[!UICONTROL Crear campaña]**.
1. En el **[!UICONTROL Crear campaña]** pantalla:
   1. Seleccionar **[!UICONTROL Mensaje en la aplicación]** y seleccione **[!UICONTROL Aplicación móvil de Luma]** desde el **[!UICONTROL Superficie de aplicación]** lista.
   1. Seleccione **[!UICONTROL Crear]**
      ![Propiedades de campaña](assets/ajo-campaign-properties.png)
1. En la pantalla Campaign definition, en **[!UICONTROL Propiedades]**, introduzca un **[!UICONTROL Nombre]** para la campaña, por ejemplo `Luma - In-App Messaging Campaign`, y a **[!UICONTROL Descripción]**, por ejemplo `In-app messaging campaign for Luma app`.
   ![Nombre de la campaña](assets/ajo-campaign-properties-name.png)
1. Desplácese hacia abajo hasta **[!UICONTROL Acción]** y seleccione **[!UICONTROL Editar contenido]**.
1. En el **[!UICONTROL Mensaje en la aplicación]** pantalla:
   1. Seleccionar **[!UICONTROL Modal]** como el **[!UICONTROL Diseño del mensaje]**.
   2. Entrar `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` para **[!UICONTROL URL de medios]**.
   3. Introduzca una **[!UICONTROL Header]**, por ejemplo `Welcome to this Luma In-App Message` e introduzca un **[!UICONTROL Cuerpo]**, por ejemplo `Triggered by pushing that button in the app...`.
   4. Entrar **[!UICONTROL Descartar]** como el **[!UICONTROL Texto de #1 de botón (principal)]**.
   5. Observe cómo se actualiza la vista previa.
   6. Seleccionar **[!UICONTROL Revisar para activar]**.
      ![Editor en la aplicación](assets/ajo-in-app-editor.png)
1. En el **[!UICONTROL Revise para activar (Luma, campaña de mensajería en la aplicación)]** pantalla, seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) en el **[!UICONTROL Programación]** mosaico.
   ![Revisar programación seleccionar Programación](assets/ajo-review-select-schedule.png)
1. De nuevo en **[!UICONTROL Luma: Campaña de mensajería en la aplicación]** pantalla, seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar déclencheur]**.
1. En el **[!UICONTROL Déclencheur de mensajes en la aplicación]** , configure los detalles de la acción de seguimiento que almacena en déclencheur el mensaje en la aplicación:
   1. Para eliminar **[!UICONTROL Evento de inicio de aplicación]**, seleccione ![Cerrar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) .
   1. Uso ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir condición]** repetidamente para generar la siguiente lógica para **[!UICONTROL Mostrar mensaje si]**.
   1. Haga clic en **[!UICONTROL Finalizado]**.
      ![lógica de déclencheur](assets/ajo-trigger-logic.png)

   Ha definido una acción de seguimiento, donde la variable **[!UICONTROL Acción]** igual a `in-app` y el **[!UICONTROL Datos de contexto]** con la acción es un par de valor clave de `"showMessage" : "true"`.

1. De nuevo en **[!UICONTROL Luma: Campaña de mensajería en la aplicación]** pantalla, seleccione **[!UICONTROL Revisar para activar]**.
1. En el **[!UICONTROL Revise para activar (Luma, campaña de mensajería en la aplicación)]** pantalla, seleccione **[!UICONTROL Activar]**.
1. Ya ve su **[!UICONTROL Luma: Campaña de mensajería en la aplicación]** con estado **[!UICONTROL Activo]** en el **[!UICONTROL Campañas]** lista.
   ![Lista de campañas](assets/ajo-campaign-list.png)


## Activación del mensaje en la aplicación

Dispone de todos los ingredientes para enviar un mensaje en la aplicación. Lo que queda es cómo almacenar en déclencheur este mensaje en la aplicación en el código.

1. Vaya a Luma > Luma > Utils > MobileSDK en el navegador del proyecto Xcode y busque `func sendTrackAction(action: String, data: [String: Any]?)` y agregue el siguiente código, que llama a la función `MobileCore.track` función, según los parámetros `action` y `data`.


   ```swift
   // send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Ir a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vistas]** > **[!UICONTROL General]** > **[!UICONTROL ConfigView]** en el Navegador de proyectos de Xcode. Busque el código del botón Mensaje en la aplicación y añada el siguiente código:

   ```swift
   Task {
       AEPService.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

## Validar con la aplicación

1. Abra la aplicación en un dispositivo o en el simulador.

1. Vaya a la **[!UICONTROL Configuración]** pestaña.

1. Tocar **[!UICONTROL Mensaje en la aplicación]**. Verá que el mensaje en la aplicación aparece en la aplicación.

   <img src="assets/ajo-in-app-message.png" width="300" />


## Validar en Assurance

Puede validar los mensajes en la aplicación en la interfaz de usuario de Assurance.

1. Seleccionar **[!UICONTROL Mensajería en la aplicación]**.
1. Seleccionar **[!UICONTROL Lista de eventos]**.
1. Seleccione una **[!UICONTROL Mostrar mensaje]** entrada.
1. Inspect el evento sin procesar, especialmente el `html`, que contiene el diseño completo y el contenido del mensaje en la aplicación.
   ![Mensaje en la aplicación de Assurance](assets/assurance-in-app-display-message.png)


## Implemente en la aplicación

Ahora debe tener todas las herramientas para empezar a añadir notificaciones push, cuando corresponda y corresponda, a la aplicación de Luma. Por ejemplo, dar la bienvenida al usuario cuando inicia sesión en la aplicación o cuando se aproxima a una geolocalización específica.

>[!SUCCESS]
>
>Ahora ha habilitado la aplicación para mensajería en la aplicación y ha agregado una campaña de mensajería en la aplicación mediante Adobe Journey Optimizer y la extensión Adobe Journey Optimizer para el SDK de Adobe Experience Platform Mobile.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Conclusión y pasos siguientes](conclusion.md)**
