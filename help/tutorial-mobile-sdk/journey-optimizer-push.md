---
title: Creación y envío de notificaciones push con el SDK de Platform Mobile
description: Obtenga información sobre cómo crear notificaciones push en una aplicación móvil con el SDK móvil de Platform y Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
jira: KT-14638
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: e316f881372a387b82f8af27f7f0ea032a99be99
workflow-type: tm+mt
source-wordcount: '2582'
ht-degree: 0%

---

# Creación y envío de notificaciones push

Obtenga información sobre cómo crear notificaciones push para aplicaciones móviles con el SDK móvil de Experience Platform y Journey Optimizer.

Journey Optimizer le permite crear recorridos y enviar mensajes a audiencias de destino. Antes de enviar notificaciones push con Journey Optimizer, debe asegurarse de que las configuraciones e integraciones adecuadas estén implementadas. Para comprender el flujo de datos de notificaciones push en Journey Optimizer, consulte la [documentación](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-gs.html).

![Arquitectura](assets/architecture-ajo.png)

>[!NOTE]
>
>Esta lección es opcional y solo se aplica a los usuarios de Journey Optimizer que buscan enviar notificaciones push.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.
* Configure la aplicación para Adobe Experience Platform.
* Acceso a Journey Optimizer y permisos suficientes como se describe [aquí](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html?lang=en). Además, necesita permisos suficientes para las siguientes funciones de Journey Optimizer.
   * Cree una superficie de aplicación.
   * Cree un recorrido.
   * Cree un mensaje.
   * Cree ajustes preestablecidos de mensaje.
* **Cuenta de desarrollador de Apple de pago** con acceso suficiente para crear certificados, identificadores y claves.
* Dispositivo o simulador físico de iOS para realizar pruebas.

## Objetivos de aprendizaje

En esta lección, debe

* Registre el ID de la aplicación con el servicio de notificaciones push de Apple (APNS).
* Crear una superficie de aplicación en Journey Optimizer.
* Actualice el esquema para incluir los campos de mensajería push.
* Instale y configure la extensión de etiquetas de Journey Optimizer.
* Actualice la aplicación para registrar la extensión de etiqueta de Journey Optimizer.
* Valide la configuración en Assurance.
* Enviar un mensaje de prueba desde Assurance
* Defina su propio evento, recorrido y experiencia de notificaciones push en Journey Optimizer.
* Envíe su propia notificación push desde la aplicación.


## Configuración

>[!TIP]
>
>Si ya configuró su entorno como parte de la lección [Mensajería en la aplicación de Journey Optimizer](journey-optimizer-inapp.md), es posible que ya haya realizado algunos de los pasos de esta sección de configuración.

### Registro del ID de la aplicación con APNS

Los siguientes pasos no son específicos de Adobe Experience Cloud y están diseñados para guiarle a través de la configuración de APNS.

#### Crear una clave privada

1. En Apple Developer Portal, vaya a **[!UICONTROL Keys]**.
1. Para crear una clave, seleccione **[!UICONTROL +]**.
   ![crear nueva clave](assets/mobile-push-apple-dev-new-key.png)

1. Proporcione un **[!UICONTROL Nombre de clave]**.
1. Seleccione la casilla de verificación **[!UICONTROL Servicio de notificaciones push de Apple] (APN)**.
1. Seleccione **[!UICONTROL Continuar]**.
   ![configurar nueva clave](assets/mobile-push-apple-dev-config-key.png)
1. Revise la configuración y seleccione **[!UICONTROL Registrar]**.
1. Descargar la clave privada `.p8`. Se utiliza en la configuración de la superficie de la aplicación más adelante en esta lección.
1. Tome nota de la **[!UICONTROL ID de clave]**. Se utiliza en la configuración de la superficie de la aplicación.
1. Tome nota de **[!UICONTROL Id. de equipo]**. Se utiliza en la configuración de la superficie de la aplicación.
   ![Detalles de clave](assets/push-apple-dev-key-details.png)

Encontrará documentación adicional [aquí](https://help.apple.com/developer-account/#/devcdfbb56a3).

#### Añadir una superficie de aplicación en la recopilación de datos

1. En la [interfaz de recopilación de datos](https://experience.adobe.com/data-collection/), seleccione **[!UICONTROL Superficies de la aplicación]** en el panel izquierdo.
1. Para crear una configuración, seleccione **[!UICONTROL Crear superficie de aplicación]**.
   ![inicio de superficie de aplicación](assets/push-app-surface.png)
1. Escriba un **[!UICONTROL Nombre]** para la configuración, por ejemplo `Luma App Tutorial` .
1. En **[!UICONTROL Configuración de aplicaciones móviles]**, seleccione **[!UICONTROL Apple iOS]**.
1. Introduzca el ID del paquete de la aplicación móvil en el campo **[!UICONTROL ID de la aplicación (ID del paquete de iOS)]**. Por ejemplo, `com.adobe.luma.tutorial.swiftui`.
1. Active la opción **[!UICONTROL Credenciales push]** para agregar sus credenciales.
1. Arrastre y suelte su archivo `.p8` **Clave de autenticación de notificaciones push de Apple**.
1. Proporcione la **[!UICONTROL ID de clave]**, una cadena de 10 caracteres asignada durante la creación de la clave de autenticación `p8`. Se encuentra en la ficha **[!UICONTROL Keys]** de la página **Certificados, identificadores y perfiles** de las páginas del portal de Apple Developer. Consulte también [Crear una clave privada](#create-a-private-key).
1. Proporcione el **[!UICONTROL ID de equipo]**. El identificador de equipo es un valor que se encuentra en la ficha **Pertenencia** o en la parte superior de la página del portal para desarrolladores de Apple. Consulte también [Crear una clave privada](#create-a-private-key).
1. Seleccione **[!UICONTROL Guardar]**.

   ![configuración de superficie de aplicación](assets/push-app-surface-config.png)

### Actualizar configuración de secuencia de datos

Para garantizar que los datos enviados desde su aplicación móvil al Edge Network se reenvíen a Journey Optimizer, actualice la configuración de Experience Edge

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y su secuencia de datos, por ejemplo **[!DNL Luma Mobile App]**.
1. Seleccione ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) para **[!UICONTROL Experience Platform]** y seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar]** del menú contextual.
1. En la pantalla **[!UICONTROL Datastreams]** > ![Folder](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]**:

   1. Si aún no está seleccionado, seleccione **[!UICONTROL Conjunto de datos del perfil push de AJO]** de **[!UICONTROL Conjunto de datos de perfil]**. Este conjunto de datos de perfil es necesario al usar la llamada API `MobileCore.setPushIdentifier` (consulte [Registrar el token de dispositivo para notificaciones push](#register-device-token-for-push-notifications)), que garantiza que el identificador único para notificaciones push (también conocido como identificador push) se almacene como parte del perfil del usuario.

   1. **[!UICONTROL Adobe Journey Optimizer]** está seleccionado. Consulte [Configuración de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) para obtener más información.

   1. Para guardar la configuración de su secuencia de datos, seleccione **[!UICONTROL Guardar]**.

   ![Configuración de secuencia de datos AEP](assets/datastream-aep-configuration.png)



### Instalación de la extensión Journey Optimizer tags

Para que la aplicación funcione con Journey Optimizer, debe actualizar la propiedad de etiquetas.

1. Vaya a **[!UICONTROL Etiquetas]** > **[!UICONTROL Extensiones]** > **[!UICONTROL Catálogo]**,
1. Abra su propiedad, por ejemplo **[!DNL Luma Mobile App Tutorial]**.
1. Seleccione **[!UICONTROL Catálogo]**.
1. Busque la extensión **[!UICONTROL Adobe Journey Optimizer]**.
1. Instale la extensión de.
1. En el diálogo **[!UICONTROL Instalar extensión]**
   1. Seleccione un entorno, por ejemplo **[!UICONTROL Desarrollo]**.
   1. Seleccione el conjunto de datos **[!UICONTROL AJO Push Tracking Experience Event Dataset]** de la lista **[!UICONTROL Event Dataset]**.
   1. Seleccione **[!UICONTROL Guardar en biblioteca y compilar]**.
      ![Configuración de la extensión de AJO](assets/push-tags-ajo.png)

>[!NOTE]
>
>Si no ve **[!UICONTROL Conjunto de datos de evento de experiencia de seguimiento push de AJO]** como opción, póngase en contacto con el servicio de atención al cliente.
>

## Validar la configuración con Assurance

1. Revise la sección [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar su simulador o dispositivo a Assurance.
1. En la IU de Assurance, seleccione **[!UICONTROL Configurar]**.
   ![configurar clic](assets/push-validate-config.png)
1. Seleccione ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a **[!UICONTROL Push Debug]**.
1. Seleccione **[!UICONTROL Guardar]**.
   ![guardar](assets/push-validate-save.png)
1. Seleccione **[!UICONTROL Push Debug]** en el panel de navegación izquierdo.
1. Seleccione la ficha **[!UICONTROL Validar configuración]**.
1. Seleccione su dispositivo de la lista **[!UICONTROL Cliente]**.
1. Confirme que no está recibiendo ningún error.
   ![validar](assets/push-validate-confirm.png)
1. Seleccione la ficha **[!UICONTROL Enviar inserción de prueba]**.
1. (opcional) Cambie los detalles predeterminados de **[!UICONTROL Title]** y **[!UICONTROL Body]**
1. Seleccione ![Error](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL Enviar notificación push de prueba]**.
1. Compruebe **[!UICONTROL resultados de la prueba]**.
1. Debería ver la notificación push de prueba en la aplicación.

   <img src="assets/luma-app-push.png" width="300" />


## Firma

La firma de la aplicación Luma es necesaria para enviar notificaciones push y **requiere una cuenta de desarrollador de Apple de pago**.

Para actualizar la firma de la aplicación:

1. Vaya a la aplicación en Xcode.
1. Seleccione **[!DNL Luma]** en el navegador de proyectos.
1. Seleccione el destino **[!DNL Luma]**.
1. Seleccione la pestaña **Firma y capacidades**.
1. Configure **[!UICONTROL Firma automática de administración]**, **[!UICONTROL Equipo]** y **[!UICONTROL Identificador de paquete]**, o use sus detalles específicos de aprovisionamiento de desarrollo de Apple.

   >[!IMPORTANT]
   >
   >Asegúrese de utilizar un identificador de paquete _unique_ y reemplace el identificador de paquete `com.adobe.luma.tutorial.swiftui`, ya que cada identificador de paquete debe ser único. Normalmente, utiliza un formato DNS inverso para cadenas de ID de paquete, como `com.organization.brand.uniqueidentifier`. La versión final de este tutorial, por ejemplo, utiliza `com.adobe.luma.tutorial.swiftui`.


   ![Funciones de firma de Xcode](assets/xcode-signing-capabilities.png){zoomable="yes"}


## Añadir funciones de notificaciones push a la aplicación

>[!IMPORTANT]
>
>Para implementar y probar las notificaciones push en una aplicación de iOS, debes tener una cuenta de desarrollador de Apple **de pago**. Si no tiene una cuenta de desarrollador de Apple de pago, puede omitir el resto de esta lección.

1. En Xcode, seleccione **[!DNL Luma]** de la lista **[!UICONTROL TARGETS]**, seleccione la pestaña **[!UICONTROL Firma y capacidades]**, seleccione el botón **[!UICONTROL + capacidad]** y, a continuación, seleccione **[!UICONTROL Notificaciones push]**. Esto permite que la aplicación reciba notificaciones push.

1. A continuación, debe añadir una extensión de notificación a la aplicación. Vuelva a la ficha **[!DNL General]** y seleccione el icono **[!UICONTROL +]** en la parte inferior de la sección **[!UICONTROL TARGETS]**.

1. Se le pedirá que seleccione la plantilla para el nuevo destino. Seleccione **[!UICONTROL Extensión del servicio de notificaciones]** y, a continuación, seleccione **[!UICONTROL Siguiente]**.

1. En la siguiente ventana, use `NotificationExtension` como nombre de la extensión y haga clic en el botón **[!UICONTROL Finalizar]**.

Ahora debería tener una extensión de notificación push agregada a la aplicación, similar a la pantalla siguiente.

![Extensión de notificaciones push](assets/xcode-signing-capabilities-pushnotifications.png)


## Implementar Journey Optimizer en la aplicación

Como se ha explicado en lecciones anteriores, la instalación de una extensión de etiqueta móvil solo proporciona la configuración. A continuación, debe instalar y registrar el SDK de mensajería. Si estos pasos no están claros, revise la sección [Instalar SDK](install-sdks.md).

>[!NOTE]
>
>Si ha completado la sección [Instalar SDK](install-sdks.md), el SDK ya está instalado y puede omitir este paso.
>

1. En Xcode, asegúrese de que [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios) se añada a la lista de paquetes en Dependencias del paquete. Consulte [Administrador De Paquetes Swift](install-sdks.md#swift-package-manager).
1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** en el navegador del proyecto Xcode.
1. Asegúrese de que `AEPMessaging` forme parte de su lista de importaciones.

   `import AEPMessaging`

1. Asegúrese de que `Messaging.self` forme parte de la matriz de extensiones que está registrando.

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

## Registrar token de dispositivo para notificaciones push

1. Agregar la API [`MobileCore.setPushIdentifier`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setpushidentifier) a la función `func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data)`.

   ```swift
   // Send push token to Mobile SDK
   MobileCore.setPushIdentifier(deviceToken)
   ```

   Esta función recupera el token del dispositivo exclusivo del dispositivo en el que está instalada la aplicación. A continuación, establece el token para la entrega de notificaciones push mediante la configuración que ha configurado y que depende del servicio de notificaciones push de Apple (APN).

>[!IMPORTANT]
>
>`MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])` determina si las notificaciones push utilizan una zona protegida de APNS o un servidor de producción para enviar notificaciones push. Al probar la aplicación en el simulador o en un dispositivo, asegúrese de que `messaging.useSandbox` está establecido en `true` para que reciba notificaciones push. Al implementar su aplicación para producción con el programa Testflight de Apple, asegúrese de establecer `messaging.useSandbox` en `false`; de lo contrario, la aplicación de producción no podrá recibir notificaciones push.


## Cree su propia notificación push

Para crear su propia notificación push, debe definir un evento en Journey Optimizer que almacene en déclencheur un recorrido que se encargue de enviar una notificación push.

### Actualizar el esquema

Va a definir un nuevo tipo de evento, que aún no está disponible, como parte de la lista de eventos definidos en el esquema. Este tipo de evento se utiliza más adelante al activar las notificaciones push.

1. En la interfaz de usuario de Journey Optimizer, seleccione **[!UICONTROL Esquemas]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Examinar]** en la barra de fichas.
1. Seleccione el esquema, por ejemplo **[!DNL Luma Mobile App Event Schema]** para abrirlo.
1. En el Editor de esquemas:
   1. Seleccione el campo **[!UICONTROL eventType]**.
   1. En el panel **[!UICONTROL Propiedades del campo]**, desplácese hacia abajo para ver la lista de valores posibles para el tipo de evento. Seleccione **[!UICONTROL Agregar fila]** y agregue `application.test` como **[!UICONTROL VALUE]** y `[!UICONTROL Test event for push notification]` como `DISPLAY NAME`.
   1. Seleccione **[!UICONTROL Aplicar]**.
   1. Seleccione **[!UICONTROL Guardar]**.
      ![Agregar valor a tipos de eventos](assets/ajo-update-schema-eventtype-enum.png)

### Definición de un evento

Los eventos de Journey Optimizer le permiten almacenar en déclencheur sus recorridos de forma unitaria para enviar mensajes como, por ejemplo, notificaciones push. Consulte [Acerca de los eventos](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/events-journeys/about-events.html?lang=en) para obtener más información.

1. En la interfaz de usuario de Journey Optimizer, seleccione **[!UICONTROL Configuraciones]** en el carril izquierdo.

1. En la pantalla **[!UICONTROL Tablero]**, seleccione el botón **[!UICONTROL Administrar]** en el mosaico **[!UICONTROL Eventos]**.

1. En la pantalla **[!UICONTROL Eventos]**, seleccione **[!UICONTROL Crear evento]**.

1. En el panel **[!UICONTROL Editar evento de evento1]**:

   1. Escriba `LumaTestEvent` como **[!UICONTROL Nombre]** del evento.
   1. Proporcione una **[!UICONTROL descripción]**, por ejemplo `Test event to trigger push notifications in Luma app`.

   1. Seleccione el esquema del evento de experiencia de la aplicación móvil que creó anteriormente en [Crear un esquema XDM](create-schema.md) desde la lista **[!UICONTROL Esquema]**, por ejemplo **[!DNL Luma Mobile App Event Schema v.1]**.
   1. Seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) junto a la lista **[!UICONTROL Campos]**.

      ![Editar paso de evento 1](assets/ajo-edit-event1.png)

      En el cuadro de diálogo **[!UICONTROL Campos]**, asegúrese de que los siguientes campos estén seleccionados (sobre los campos predeterminados que siempre están seleccionados (**[!UICONTROL _id]**, **[!UICONTROL id]** y **[!UICONTROL timestamp]**)). Con la lista desplegable, puede alternar entre **[!UICONTROL Seleccionado]**, **[!UICONTROL Todo]** y **[!UICONTROL Principal]**, o usar el campo ![Buscar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg).

      * **[!UICONTROL Aplicación identificada (id.)]**,
      * **[!UICONTROL Tipo de evento (eventType)]**,
      * **[!UICONTROL Principal (principal)]**.

      ![Editar campos de evento](assets/ajo-event-fields.png)

      A continuación, seleccione **[!UICONTROL Aceptar]**.

   1. Seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) junto al campo **[!UICONTROL Condición de ID de evento]**.

      1. En el cuadro de diálogo **[!UICONTROL Agregar una condición de id. de evento]**, arrastre y suelte **[!UICONTROL Tipo de evento (eventType)]** en **[!UICONTROL Arrastrar y soltar un elemento aquí]**.
      1. En la ventana emergente, desplácese hasta la parte inferior y seleccione **[!UICONTROL application.test]** (que es el tipo de evento que agregó anteriormente a la lista de tipos de eventos como parte de [Actualizar el esquema](#update-your-schema)). A continuación, desplácese hacia arriba y seleccione **[!UICONTROL Aceptar]**.
      1. Seleccione **[!UICONTROL Aceptar]** para guardar la condición.
         ![Editar condición de evento](assets/ajo-edit-condition.png)

   1. Seleccione **[!UICONTROL ECID (ECID)]** de la lista **[!UICONTROL Espacio de nombres]**. Automáticamente, el campo **[!UICONTROL Identificador de perfil]** se rellena con **[!UICONTROL El identificador del primer elemento del ECID de clave para el identityMap]** del mapa.
   1. Seleccione **[!UICONTROL Guardar]**.
      ![Editar paso de evento 2](assets/ajo-edit-event2.png)

Acaba de crear una configuración de evento basada en el esquema de eventos de experiencia de la aplicación móvil creado anteriormente como parte de este tutorial. Esta configuración de evento filtrará los eventos de experiencia entrantes usando su tipo de evento específico (`application.test`), de modo que solo los eventos con ese tipo específico, iniciados desde su aplicación móvil, almacenarán en déclencheur el recorrido que genere en el siguiente paso. En una situación real, es posible que desee enviar notificaciones push desde un servicio externo; sin embargo, se aplican los mismos conceptos: desde la aplicación externa, envíe un evento de experiencia al Experience Platform que tenga campos específicos que pueda utilizar para aplicar condiciones antes de que estos eventos entren en déclencheur con un recorrido.

### Creación del recorrido

El siguiente paso es crear el recorrido que almacene en déclencheur el envío de la notificación push al recibir el evento correspondiente.

1. En la interfaz de usuario de Journey Optimizer, seleccione **[!UICONTROL Recorridos]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Crear Recorrido]**.
1. En el panel **[!UICONTROL Propiedades del Recorrido]**:

   1. Escriba un **[!UICONTROL Nombre]** para el recorrido, por ejemplo `Luma - Test Push Notification Journey`.
   1. Escriba una **[!UICONTROL descripción]** para el recorrido, por ejemplo `Journey for test push notifications in Luma mobile app`.
   1. Asegúrese de seleccionar **[!UICONTROL Permitir la reentrada]** y establezca **[!UICONTROL Período de espera de reentrada]** en **[!UICONTROL 30]** **[!UICONTROL Segundos]**.
   1. Seleccione **[!UICONTROL Aceptar]**.
      ![Propiedades del recorrido](assets/ajo-journey-properties.png)

1. En el lienzo del recorrido, en **[!UICONTROL EVENTS]**, arrastra y suelta tu ![evento](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg) **[!DNL LumaTestEvent]** en el lienzo donde se muestra **[!UICONTROL Selecciona un evento de entrada o una actividad de lectura de audiencia]**.

   * En el panel **[!UICONTROL Eventos: LumaTestEvent]**, escriba una **[!UICONTROL Etiqueta]**, por ejemplo `Luma Test Event`.

1. En el menú desplegable **[!UICONTROL ACCIONES]**, arrastra y suelta ![Insertar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PushNotification_18_N.svg) **[!UICONTROL Insertar]** en el ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) que aparece a la derecha de tu actividad **[!DNL LumaTestEvent]**. En el panel **[!UICONTROL Acciones: Push]**:

   1. Proporcione una **[!UICONTROL Etiqueta]**, por ejemplo `Luma Test Push Notification`, proporcione una **[!UICONTROL Descripción]**, por ejemplo `Test push notification for Luma mobile app`, seleccione **[!UICONTROL Transaccional]** de la lista **[!UICONTROL Categoría]** y seleccione **[!DNL Luma]** de la **[!UICONTROL Superficie de inserción]**.
   1. Seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar contenido]** para comenzar a editar la notificación push real.
      ![Propiedades push](assets/ajo-push-properties.png)

      En el editor de **[!UICONTROL notificaciones push]**:

      1. Escriba un **[!UICONTROL Título]**, por ejemplo `Luma Test Push Notification` y un **[!UICONTROL Cuerpo]**, por ejemplo `Test push notification for Luma mobile app`.
      1. Opcionalmente, puede escribir un vínculo a una imagen (.png o .jpg) en **[!UICONTROL Agregar medios]**. Si lo hace, la imagen formará parte de la notificación push.
      1. Para guardar y salir del editor, selecciona ![Chevron left](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronLeft_18_N.svg).
         ![Editor push](assets/ajo-push-editor.png)

   1. Para guardar y finalizar la definición de la notificación push, seleccione **[!UICONTROL Aceptar]**.

1. El recorrido debe ser similar al siguiente. Seleccione **[!UICONTROL Publish]** para publicar y activar su recorrido.
   ![recorrido finalizado](assets/ajo-journey-finished.png)


## Déclencheur de la notificación push

Tiene todos los ingredientes para enviar una notificación push. Lo que queda es cómo almacenar en déclencheur esta notificación push. En esencia, es lo mismo que ha visto antes: simplemente envíe un evento de experiencia con la carga útil adecuada (como en [Eventos](events.md)).

Esta vez, el evento de experiencia que está a punto de enviar no se construye construyendo un diccionario XDM simple. Va a usar un(a) `struct` que representa una carga de notificación push. La definición de un tipo de datos dedicado es una forma alternativa de implementar la construcción de cargas útiles de evento de experiencia en la aplicación.

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL Modelo]** > **[!UICONTROL XDM]** > **[!UICONTROL TestPushPayload]** en el navegador del proyecto Xcode e inspeccione el código.

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

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode y agregue el siguiente código a `func sendTestPushEvent(applicationId: String, eventType: String)`:

   ```swift
   // Create payload and send experience event
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

   Este código crea una instancia de `testPushPayload` utilizando los parámetros proporcionados a la función (`applicationId` y `eventType`) y, a continuación, llama a `sendExperienceEvent` mientras convierte la carga útil en un diccionario. Este código, esta vez, también tiene en cuenta los aspectos asíncronos de llamar al SDK de Adobe Experience Platform mediante el modelo de concurrencia de Swift basado en `await` y `async`.

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]** en el navegador del proyecto Xcode. En la definición del botón de notificación push, añada el siguiente código para enviar la carga útil del evento de experiencia de notificación push de prueba al déclencheur del recorrido cada vez que se pulse ese botón.

   ```swift
   // Setting parameters and calling function to send push notification
   Task {
       let eventType = testPushEventType
       let applicationId = Bundle.main.bundleIdentifier ?? "No bundle id found"
       await MobileSDK.shared.sendTestPushEvent(applicationId: applicationId, eventType: eventType)
   }
   ```


## Validar con la aplicación

1. Vuelva a compilar y ejecute la aplicación en el simulador o en un dispositivo físico desde Xcode con ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Vaya a la ficha **[!UICONTROL Configuración]**.

1. Pulse **[!UICONTROL Notificación push]**. Verá aparecer la notificación push en la aplicación.

   <img src="assets/ajo-test-push.png" width="300" />


## Pasos siguientes

Ahora debe tener todas las herramientas para gestionar las notificaciones push en la aplicación. Por ejemplo, puede crear un recorrido en Journey Optimizer que envíe una notificación push de bienvenida cuando un usuario de la aplicación inicie sesión. O una notificación push de confirmación cuando un usuario compra un producto en la aplicación. O bien, introduce la geovalla de una ubicación (como verá en la lección [Places](places.md)).

>[!SUCCESS]
>
>Ahora ha habilitado la aplicación para notificaciones push mediante Journey Optimizer y la extensión de Journey Optimizer para el SDK de Experience Platform Mobile.
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Crear y enviar mensajes en la aplicación](journey-optimizer-inapp.md)**
