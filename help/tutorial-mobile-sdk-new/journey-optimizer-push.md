---
title: mensajería push de Adobe Journey Optimizer
description: Obtenga información sobre cómo crear mensajes push en una aplicación móvil con el SDK móvil de Platform y Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
hide: true
source-git-commit: e119e2bdce524c834cdaf43ed9eb9d26948b0ac6
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 3%

---

# mensajería push de Adobe Journey Optimizer

Obtenga información sobre cómo crear mensajes push para aplicaciones móviles con el SDK móvil de Platform y Adobe Journey Optimizer.

Journey Optimizer le permite crear sus recorridos y enviar mensajes a audiencias de destino. Antes de enviar notificaciones push con Journey Optimizer, debe asegurarse de que las configuraciones e integraciones adecuadas estén implementadas. Para comprender el flujo de datos de notificaciones push en Adobe Journey Optimizer, consulte [la documentación](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>Esta lección es opcional y solo se aplica a los usuarios de Adobe Journey Optimizer que buscan enviar mensajes push.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.
* Acceso a Adobe Journey Optimizer y permisos suficientes, tal como se describe [aquí](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Además, necesita permisos suficientes para las siguientes funciones de Adobe Journey Optimizer.
   * Cree una superficie de aplicación.
   * Creación de un recorrido
   * Cree un mensaje.
   * Creación de ajustes preestablecidos de mensaje.
* Cuenta de desarrollador de Apple de pago con acceso suficiente para crear certificados, identificadores y claves.
* Dispositivo o simulador físico de iOS para realizar pruebas.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Registre el ID de la aplicación con el servicio de notificaciones push de Apple (APN).
* Crear un **[!UICONTROL Superficie de aplicación]** en AJO.
* Actualice su **[!UICONTROL esquema]** para incluir campos de mensajería push.
* Instalación y configuración de **[!UICONTROL Adobe Journey Optimizer]** extensión de etiqueta.
* Actualice la aplicación para incluir la extensión de etiqueta AJO.
* Valide la configuración en Assurance.
* Enviar un mensaje de prueba.
* Defina su propio evento, recorrido y experiencia de notificaciones push en Journey Optimizer.
* Envíe su propia notificación push desde la aplicación.


## Registro del ID de la aplicación con APN

Los siguientes pasos no son específicos de Adobe Experience Cloud y están diseñados para guiarle a través de la configuración de APN.

### Crear una clave privada

1. En el portal para desarrolladores de Apple, vaya a **[!UICONTROL Claves]**.
1. Para crear una clave, seleccione **[!UICONTROL +]**.
   ![crear clave nueva](assets/mobile-push-apple-dev-new-key.png)

1. Proporcione un **[!UICONTROL Nombre de clave]**.
1. Seleccione el **[!UICONTROL APN]** casilla de verificación
1. Seleccionar **[!UICONTROL Continuar]**.
   ![configurar nueva clave](assets/mobile-push-apple-dev-config-key.png)
1. Revise la configuración y seleccione **[!UICONTROL Registrar]**.
1. Descargue la `.p8` clave privada. Se utiliza en la configuración de la superficie de la aplicación.
1. Tome nota de la [!UICONTROL ID de clave]. Se utiliza en la configuración de la superficie de la aplicación.
1. Tome nota de la [!UICONTROL Identificador de equipo]. Se utiliza en la configuración de la superficie de la aplicación.
   ![Detalles clave](assets/push-apple-dev-key-details.png)

Puede obtenerse documentación adicional [encontrado aquí](https://help.apple.com/developer-account/#/devcdfbb56a3).

## Añadir las credenciales push de la aplicación en la recopilación de datos

1. Desde el [Interfaz de recopilación de datos](https://experience.adobe.com/data-collection/), seleccione **[!UICONTROL Superficies de aplicación]** en el panel izquierdo.
1. Para crear una configuración, seleccione **[!UICONTROL Crear superficies de aplicación]**.
   ![inicio de superficie de aplicación](assets/push-app-surface.png)
1. Introduzca una **[!UICONTROL Nombre]** para la configuración, por ejemplo `Luma App Tutorial`  .
1. En Configuración de aplicaciones móviles, seleccione **[!UICONTROL Apple iOS]**.
1. Introduzca el ID del paquete de la aplicación móvil en el campo ID de aplicación (ID de paquete de iOS). Si está siguiendo junto con la aplicación de Luma, ese valor es `com.adobe.luma.tutorial.swiftui`.
1. Encienda el **[!UICONTROL Credenciales push]** para añadir sus credenciales.
1. Arrastre y suelte su `.p8` **Clave de autenticación de notificación push de Apple** archivo.
1. Proporcione el **[!UICONTROL ID de clave]**, una cadena de 10 caracteres asignada durante la creación de `p8` clave de autenticación. Se encuentra en **[!UICONTROL Claves]** pestaña en **Certificados, identificadores y perfiles** de las páginas del portal para desarrolladores de Apple.
1. Proporcione el **[!UICONTROL Identificador de equipo]**. El identificador de equipo es un valor que se encuentra en **Suscripción** o en la parte superior de las páginas del portal para desarrolladores de Apple.
1. Seleccione **[!UICONTROL Guardar]**.

   ![configuración de superficie de aplicación](assets/push-app-surface-config.png)

## Instalación de la extensión Adobe Journey Optimizer tags

1. Vaya a **[!UICONTROL Etiquetas]** > **[!UICONTROL Extensiones]** > **[!UICONTROL Catálogo]**,
1. Abra la propiedad, por ejemplo **[!UICONTROL Tutorial de aplicación móvil de Luma]**.
1. Seleccionar **[!UICONTROL Catálogo]**.
1. Busque la variable **[!UICONTROL Adobe Journey Optimizer]** extensión.
1. Instale la extensión de.
1. En el **[!UICONTROL Instalar extensión]** diálogo
   1. Seleccione un entorno, por ejemplo **[!UICONTROL Desarrollo]**.
   1. Seleccione el **[!UICONTROL Conjunto de datos de evento de experiencia de seguimiento push AJO]** conjunto de datos del **[!UICONTROL Conjunto de datos de evento]** lista desplegable.
      ![Configuración de extensión de AJO](assets/push-tags-ajo.png)
   1. Seleccionar **[!UICONTROL Guardar en biblioteca y crear]**.

>[!NOTE]
>
>Si no lo ve... `AJO Push Tracking Experience Event Dataset` como opción, póngase en contacto con el servicio de atención al cliente.
>

## Implementar Adobe Journey Optimizer en la aplicación

Como se ha explicado en lecciones anteriores, la instalación de una extensión de etiqueta móvil solo proporciona la configuración. A continuación, debe instalar y registrar el SDK de mensajería. Si estos pasos no están claros, revise la [Instalación de SDK](install-sdks.md) sección.

>[!NOTE]
>
>Si ha completado la [Instalación de SDK](install-sdks.md) , el SDK ya está instalado y puede pasar al paso #7.
>

1. En Xcode, asegúrese de que [Mensajería AEP](https://github.com/adobe/aepsdk-messaging-ios.git) se añade a la lista de paquetes en Dependencias del paquete. Consulte [Administrador De Paquetes Swift](install-sdks.md#swift-package-manager).
1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]**.
1. Asegurar `AEPMessaging` forma parte de su lista de importaciones.

   `import AEPMessaging`

1. Asegurar `Messaging.self` forma parte de la matriz de extensiones que está registrando.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

1. Añada el `MobileCore.setPushIdentifier` a la `func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data)` función.

   ```swift
   // Send push token to Experience Platform
   MobileCore.setPushIdentifier(deviceToken)
   ```

   Esta función recupera el token del dispositivo exclusivo del dispositivo en el que está instalada la aplicación. A continuación, establece el token para la entrega de notificaciones push mediante la configuración que ha configurado y que depende del servicio de notificaciones push de Apple (APNS).

## Validar con Assurance

1. Revise la [instrucciones de configuración](assurance.md) sección.
1. Instale la aplicación en su dispositivo físico o en el simulador.
1. Inicie la aplicación mediante la URL generada por Assurance.
1. En la IU de Assurance, seleccione **[!UICONTROL Configurar]**.
   ![configurar clic](assets/push-validate-config.png)
1. Seleccione el ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) botón situado junto a **[!UICONTROL Depuración push]**.
1. Seleccione **[!UICONTROL Guardar]**.
   ![guardar](assets/push-validate-save.png)
1. Seleccionar **[!UICONTROL Depuración push]** en el panel de navegación izquierdo.
1. Seleccione el **[!UICONTROL Validar configuración]** pestaña.
1. Seleccione el dispositivo en la **[!UICONTROL Cliente]** lista.
1. Confirme que no está recibiendo ningún error.
   ![validate](assets/push-validate-confirm.png)
1. Seleccione el **[!UICONTROL Enviar inserción de prueba]** pestaña.
1. (opcional) Cambie los detalles predeterminados de **[!UICONTROL Título]** y **[!UICONTROL Cuerpo]**
1. Seleccionar ![Error](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL Enviar notificación push de prueba]**.
1. Compruebe la **[!UICONTROL Resultados de prueba]**.
1. Debería ver la notificación push en la aplicación.

   <img src="assets/luma-app-push.png" width="300" />


## Cree su propia notificación push

Para crear su propia notificación push, debe definir un evento en Journey Optimizer que almacene en déclencheur un recorrido que se encargue de enviar una notificación push.

### Definición de un evento

1. En la IU de Journey Optimizer, seleccione **[!UICONTROL Configuraciones]** desde el carril izquierdo.

1. En el **[!UICONTROL Tablero]** , seleccione la **[!UICONTROL Administrar]** botón en el **[!UICONTROL Eventos]** mosaico.

1. En el **[!UICONTROL Eventos]** pantalla, seleccione **[!UICONTROL Crear evento]**.

1. En el **[!UICONTROL Editar evento1]** panel:

   1. Entrar `LumaTestEvent` como el **[!UICONTROL Nombre]** del evento.
   1. Proporcione un **[!UICONTROL Descripción]**, por ejemplo `Test event to trigger push notifications in Luma app`.

   1. Seleccione el esquema del evento de experiencia de la aplicación móvil creado anteriormente en [Creación de un esquema XDM](create-schema.md) desde el **[!UICONTROL Esquema]** , por ejemplo **[!UICONTROL Esquema de evento de aplicación móvil de Luma v.1]**.
   1. Seleccionar ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) situado junto a la lista Campos.

      ![Editar paso de evento 1](assets/ajo-edit-event1.png)

      En el **[!UICONTROL Campos]** , asegúrese de que los siguientes campos están seleccionados (sobre los campos predeterminados que siempre están seleccionados (_id, id y marca de tiempo)). Mediante la lista desplegable, puede alternar entre **[!UICONTROL Seleccionado]**, **[!UICONTROL Todo]** y **[!UICONTROL Principal]** o use el ![Buscar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) field.

      * **[!UICONTROL Aplicación identificada (id)]**,
      * **[!UICONTROL Tipo de evento (eventType)]**,
      * **[!UICONTROL Principal (principal)]**.

      ![Editar campos de evento](assets/ajo-event-fields.png)

      A continuación seleccione **[!UICONTROL Ok]**.

   1. Seleccionar ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) junto al **[!UICONTROL Condición de ID de evento]** field.

      1. En el **[!UICONTROL Añadir una condición de ID de evento]** diálogo, arrastrar y soltar **[!UICONTROL Identificador de aplicación (id)]** debajo **[!UICONTROL Aplicación (aplicación)]** en a **[!UICONTROL Arrastre y suelte un elemento aquí]**.
      1. En la ventana emergente, introduzca el identificador de paquete desde Xcode, por ejemplo `com.adobe.luma.tutorial.swiftui` en el campo situado junto a **[!UICONTROL igual a]**.
      1. Haga clic en **[!UICONTROL Ok]**.
      1. Haga clic en **[!UICONTROL Ok]**.
         ![Editar condición de evento](assets/ajo-edit-condition.png)

   1. Seleccionar **[!UICONTROL ECID (ECID)]** desde el **[!UICONTROL Área de nombres]** lista. Automáticamente el **[!UICONTROL Identificador de perfil]** el campo se rellena con **[!UICONTROL El ID del primer elemento del ECID de clave para el identityMap de mapa]**.
   1. Seleccione **[!UICONTROL Guardar]**.
      ![Editar paso de evento 2](assets/ajo-edit-event2.png)

Acaba de crear una configuración de evento basada en el esquema de eventos de experiencia de la aplicación móvil creado anteriormente como parte de este tutorial. Esta configuración de evento filtrará los eventos de experiencia entrantes mediante el identificador de su aplicación móvil, por lo que se asegura de que solo los eventos iniciados desde su aplicación móvil almacenarán en déclencheur el recorrido que creará en el siguiente paso.

### Creación del recorrido

El siguiente paso es crear el recorrido que almacene en déclencheur el envío de la notificación push al recibir el evento correspondiente.

1. En la IU de Journey Optimizer, seleccione **[!UICONTROL Recorridos]** desde el carril izquierdo.
1. Seleccionar **[!UICONTROL Crear Recorrido]**.
1. En el **[!UICONTROL Propiedades de recorrido]** panel:

   1. Introduzca una **[!UICONTROL Nombre]** para el recorrido, por ejemplo `Luma - Test Push Notification Journey`.
   1. Introduzca una **[!UICONTROL Descripción]** para el recorrido, por ejemplo `Journey for test push notifications in Luma mobile app`.
   1. Asegurar **[!UICONTROL Permitir la reentrada]** está seleccionado y configurado **[!UICONTROL Período de espera de reentrada]** hasta **[!UICONTROL 30]** **[!UICONTROL Seconds]**.
   1. Seleccionar **[!UICONTROL Ok]**.
      ![Propiedades del recorrido](assets/ajo-journey-properties.png)

1. De vuelta en el lienzo de recorrido, de la **[!UICONTROL EVENTOS]**, arrastre y suelte su ![Evento](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg) **[!UICONTROL LumaTestEvent]** en el lienzo donde se lee **[!UICONTROL Seleccione un evento de entrada o una actividad de audiencia de lectura]**.

   * En los eventos: **[!UICONTROL LumaTestEvent]** , introduzca un **[!UICONTROL Etiqueta]**, por ejemplo `Luma Test Event`.

1. Desde el **[!UICONTROL ACCIONES]** desplegable, arrastrar y soltar ![Push](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PushNotification_18_N.svg) **[!UICONTROL Push]** en el ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) que aparecen directamente en su **[!UICONTROL LumaTestEvent]** actividad. En el **[!UICONTROL Acciones: push]** panel:

   1. Proporcione un **[!UICONTROL Etiqueta]**, por ejemplo `Luma Test Push Notification`, proporcione un **[!UICONTROL Descripción]**, por ejemplo `Test push notification for Luma mobile app`, seleccione **[!UICONTROL Transaccional]** desde el **[!UICONTROL Categoría]** lista y seleccione **[!UICONTROL Luma]** desde el **[!UICONTROL Superficie de inserción]**.
   1. Seleccionar ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar contenido]** para empezar a editar la notificación push real.
      ![Propiedades push](assets/ajo-push-properties.png)

      En el **[!UICONTROL Notificación push]** editor:

      1. Introduzca una **[!UICONTROL Título]**, por ejemplo `Luma Test Push Notification` e introduzca un **[!UICONTROL Cuerpo]**, por ejemplo `Test push notification for Luma mobile app`.
      1. Para guardar y salir del editor, seleccione ![Corchete izquierdo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronLeft_18_N.svg).
         ![Editor push](assets/ajo-push-editor.png)

   1. Para guardar y finalizar la definición de la notificación push, seleccione **[!UICONTROL Ok]**.

1. El recorrido debe ser similar al siguiente. Seleccionar **[!UICONTROL Publish]** para publicar y activar el recorrido.
   ![Recorrido finalizado](assets/ajo-journey-finished.png)


## Activación de la notificación push

Tiene todos los ingredientes para enviar una notificación push. Lo que queda es cómo almacenar en déclencheur esta notificación push. En esencia, es lo mismo que ha visto antes: simplemente envíe un evento de experiencia con la carga útil adecuada.

Esta vez, el evento de experiencia que está a punto de enviar no se construye construyendo un diccionario XDM simple. Va a utilizar una estructura que represente una carga útil de notificación push. La definición de un tipo de datos dedicado es una forma alternativa de implementar la construcción de cargas útiles de evento de experiencia en la aplicación.

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Modelo]** > **[!UICONTROL XDM]** > **[!UICONTROL TestPushPayload]** e inspeccione el código.

   ```swift
   import Foundation
   
   // MARK: - TestPush
   struct TestPushPayload: Codable {
      let application: Application
      let eventType: String
   }
   
   // MARK: - Application
   struct Application: Codable {
      let id: String
   }
   ```

   El código es una representación de la siguiente carga útil simple que va a enviar al déclencheur de su recorrido de notificaciones push de prueba

   ```json
   {
      "eventType": string,
      "application" : [
          "id": string
      ]
   }
   ```

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode y añada el siguiente código a `func sendTestPushEvent(applicationId: String, eventType: String)`:

   ```swift
   Task {
       let testPushPayload = TestPushPayload(
           application: Application(
               id: applicationId
           ),
           eventType: eventType
       )
       // send the final experience event
       await sendExperienceEvent(
           xdm: testPushPayload.asDictionary() ?? [:]
       )
   }
   ```

   Este código crea un `testPushPayload` usando los parámetros proporcionados a la función (`applicationId` y `eventType`) y luego llama a `sendExperienceEvent` al convertir la carga útil en un diccionario. Este código, esta vez, también tiene en cuenta los aspectos asíncronos de llamar al SDK de Adobe Experience Platform mediante el modelo de concurrencia de Swift basado en `await` y `async`.

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vistas]** > **[!UICONTROL General]** > **[!UICONTROL ConfigView]** en el navegador del proyecto Xcode. En la definición del botón de notificación push, añada el siguiente código para enviar la carga útil del evento de experiencia de notificación push de prueba al déclencheur del recorrido cada vez que se pulse ese botón.

   ```swift
   // Setting parameters and calling function to send push notification
   let eventType = "mobileapp.testpush"
   let applicationId = Bundle.main.bundleIdentifier ?? "No bundle id found"
   await MobileSDK.shared.sendTestPushEvent(applicationId: applicationId, eventType: eventType)   
   ```


## Validar con la aplicación

1. Abra la aplicación en un dispositivo o en el simulador.

1. Vaya a la **[!UICONTROL Configuración]** pestaña.

1. Tocar **[!UICONTROL Notificación push]**. Verá aparecer la notificación push en la aplicación.
   <img src="assets/ajo-test-push.png" width="300" />


## Implemente en la aplicación

Ahora debe tener todas las herramientas para empezar a añadir notificaciones push, cuando corresponda y corresponda, a la aplicación de Luma. Por ejemplo, dar la bienvenida al usuario cuando inicia sesión en la aplicación o cuando se aproxima a una geolocalización específica.

>[!SUCCESS]
>
>Ahora ha habilitado la aplicación para notificaciones push mediante Adobe Journey Optimizer y la extensión de Adobe Journey Optimizer para el SDK de Adobe Experience Platform Mobile.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Mensajería en la aplicación con Journey Optimizer](journey-optimizer-inapp.md)**

