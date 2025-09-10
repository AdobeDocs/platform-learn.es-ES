---
title: Creación y envío de mensajes en la aplicación con Platform Mobile SDK
description: Obtenga información sobre cómo crear y enviar mensajes en la aplicación a una aplicación móvil con Platform Mobile SDK y Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
jira: KT-14639
exl-id: 6cb4d031-6172-4a84-b717-e3a1f5dc7d5d
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 1%

---

# Creación y envío de mensajes en la aplicación

Obtenga información sobre cómo crear mensajes en la aplicación para aplicaciones móviles con Experience Platform Mobile SDK y Journey Optimizer.

Journey Optimizer le permite crear campañas para enviar mensajes en la aplicación a audiencias de destino. Las campañas en Journey Optimizer se utilizan para entregar contenido único a una audiencia específica mediante varios canales. Con las campañas, las acciones se realizan simultáneamente, ya sea de forma inmediata o en función de una programación especificada. Cuando se utilizan recorridos (consulte la lección [Notificaciones push de Journey Optimizer](journey-optimizer-push.md)), las acciones se ejecutan de forma secuencial.

![Arquitectura](assets/architecture-ajo.png){zoomable="yes"}

Antes de enviar mensajes en la aplicación con Journey Optimizer, debe asegurarse de que las configuraciones y integraciones adecuadas estén implementadas. Para comprender el flujo de datos de mensajería en la aplicación en Journey Optimizer, consulte [la documentación](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/in-app/inapp-configuration).

>[!NOTE]
>
>Esta lección es opcional y solo se aplica a los usuarios de Journey Optimizer que buscan enviar mensajes en la aplicación.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.
* Configure la aplicación para Adobe Experience Platform.
* Acceso a Journey Optimizer y [permisos suficientes para notificaciones push](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/push/push-config/push-configuration). Además, necesita permisos suficientes para las siguientes funciones de Journey Optimizer.
   * Administrar campañas.
* Dispositivo o simulador físico de iOS para realizar pruebas.


## Objetivos de aprendizaje

En esta lección, debe

* Cree una configuración de canal en Journey Optimizer.
* Instale y configure la extensión de etiquetas de Journey Optimizer.
* Actualice la aplicación para registrar la extensión de etiqueta de Journey Optimizer.
* Valide la configuración en Assurance.
* Defina su propia experiencia de campaña y mensaje en la aplicación en Journey Optimizer.
* Envíe su propio mensaje en la aplicación desde la aplicación.

## Configuración

>[!TIP]
>
>Si ya configuró su entorno como parte de la lección [Mensajería push de Journey Optimizer](journey-optimizer-push.md), es posible que ya haya realizado algunos de los pasos de esta sección de configuración.


### Creación de una configuración de canal

Para empezar, debe crear una configuración de canal para poder enviar notificaciones de mensajes en la aplicación desde Journey Optimizer.

1. En la interfaz de Journey Optimizer, abra el menú **[!UICONTROL Canales]** > **[!UICONTROL Configuración general]** > **[!UICONTROL Configuraciones de canal]** y luego seleccione **[!UICONTROL Crear configuración de canal]**.

1. Introduzca un nombre y una descripción (opcional) para la configuración. Por ejemplo, `LumaInAppMessaging` y `Channel for in-app messaging`.

   >[!NOTE]
   >
   > Los nombres deben comenzar por una letra (A-Z). Solo puede contener caracteres alfanuméricos. También puede utilizar caracteres de guion bajo `_`, punto `.` y guion `-`.

1. Para asignar etiquetas de uso de datos principales o personalizadas a la configuración, puedes seleccionar **[!UICONTROL Administrar acceso]**. [Obtenga más información acerca del Control de acceso de nivel de objeto (OLAC)](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/access-control/object-based-access).

1. Seleccione el canal **mensajería en la aplicación**.

1. Seleccione **[!UICONTROL Acciones de marketing]** para asociar directivas de consentimiento con los mensajes que usan esta configuración. Todas las políticas de consentimiento asociadas con la acción de marketing se aprovechan para respetar las preferencias de los clientes. [Más información sobre las acciones de marketing](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/privacy/consent/consent#surface-marketing-actions). Por ejemplo: Segmentación push.

1. Seleccione la plataforma para la que desea definir la configuración. Esta configuración le permite especificar la aplicación de destino para cada plataforma y garantiza una entrega de contenido coherente en varias plataformas.

   >[!NOTE]
   >
   >En las plataformas iOS y Android, la entrega se basa únicamente en el ID de aplicación. Si ambas aplicaciones comparten el mismo ID de aplicación, el contenido se envía a ambas, independientemente de la plataforma seleccionada en la **[!UICONTROL configuración del canal]**.

1. Introduzca los ID de la aplicación para la plataforma que desea admitir.

   ![Crear una configuración de canal](assets/in-app-messaging-config.png){zoomable="yes"}

1. Seleccione **[!UICONTROL Enviar]** para guardar los cambios.

### Actualizar configuración de secuencia de datos

Para garantizar que los datos enviados desde su aplicación móvil a Edge Network se reenvíen a Journey Optimizer, actualice la configuración de Experience Edge.



1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y su secuencia de datos, por ejemplo **[!DNL Luma Mobile App]**.
1. Seleccione ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) para **[!UICONTROL Experience Platform]** y seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar]** en el menú contextual.
1. En la pantalla **[!UICONTROL Datastreams]** > ![Folder](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]**, compruebe que **[!UICONTROL Adobe Journey Optimizer]** esté seleccionado. Consulte [Configuración de Adobe Experience Platform](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure) para obtener más información.
1. Para guardar la configuración de su secuencia de datos, seleccione **[!UICONTROL Guardar]**.


   ![Configuración de secuencia de datos de AEP](assets/datastream-ajo-inapp-configuration.png){zoomable="yes"}


### Instalación de la extensión Journey Optimizer tags

Para que la aplicación funcione con Journey Optimizer, debe actualizar la propiedad de etiquetas.

1. Vaya a **[!UICONTROL Etiquetas]** > **[!UICONTROL Extensiones]** > **[!UICONTROL Catálogo]**.
1. Abra su propiedad, por ejemplo **[!DNL Luma Mobile App Tutorial]**.
1. Seleccione **[!UICONTROL Catálogo]**.
1. Busque la extensión **[!UICONTROL Adobe Journey Optimizer]**.
1. Instale la extensión de.

Cuando *solo* usa mensajes en la aplicación, en **[!UICONTROL Instalar extensión]** o **[!UICONTROL Configurar extensión]**, no necesita configurar nada. Si ya ha seguido la lección [Notificaciones push](journey-optimizer-push.md) del tutorial, verá que para el entorno **[!UICONTROL Desarrollo]**, el conjunto de datos **[!UICONTROL AJO Push Tracking Experience Event Dataset]** está seleccionado de la lista **[!UICONTROL Conjunto de datos de evento]**.


### Implementar Journey Optimizer en la aplicación

Como se ha explicado en lecciones anteriores, la instalación de una extensión de etiqueta móvil solo proporciona la configuración. A continuación, debe instalar y registrar Messaging SDK. Si estos pasos no están claros, revise la sección [Instalar SDK](install-sdks.md).

>[!NOTE]
>
>Si ha completado la sección [Instalar SDK](install-sdks.md), SDK ya está instalado y puede omitir este paso.
>

>[!BEGINTABS]

>[!TAB iOS]

1. En Xcode, asegúrese de que [Mensajería de AEP](https://github.com/adobe/aepsdk-messaging-ios) se agrega a la lista de paquetes en Dependencias del paquete. Consulte [Administrador De Paquetes Swift](install-sdks.md#swift-package-manager).
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

>[!TAB Android]

1. En Android Studio, asegúrese de que [aepsdk-messaging-android](https://github.com/adobe/aepsdk-messaging-android) forme parte de las dependencias de **[!UICONTROL build.gradle.kts]** en **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!UICONTROL Gradle Scripts]**. Ver [Gradle](install-sdks.md#gradle).
1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** en el navegador de proyectos de Android Studio.
1. Asegúrese de que `com.adobe.marketing.mobile.Messaging` forme parte de su lista de importaciones.

   `import import com.adobe.marketing.mobile.Messaging`

1. Asegúrese de que `Messaging.EXTENSION` forme parte de la matriz de extensiones que está registrando.

   ```kotlin
   val extensions = listOf(
       Identity.EXTENSION,
       Lifecycle.EXTENSION,
       Signal.EXTENSION,
       Edge.EXTENSION,
       Consent.EXTENSION,
       UserProfile.EXTENSION,
       Places.EXTENSION,
       Messaging.EXTENSION,
       Optimize.EXTENSION,
       Assurance.EXTENSION
   )
   ```

>[!ENDTABS]

## Validar la configuración con Assurance

1. Revise la sección [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo a Assurance.
1. En la IU de Assurance, seleccione **[!UICONTROL Configurar]**.
   ![configurar clic](assets/push-validate-config.png){zoomable="yes"}
1. Seleccione el botón ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a **[!UICONTROL Mensajería en la aplicación]**.
1. Seleccione **[!UICONTROL Guardar]**.
   ![guardar](assets/assurance-in-app-config.png){zoomable="yes"}
1. Seleccione **[!UICONTROL Mensajería en la aplicación]** en el panel de navegación izquierdo.
1. Seleccione la ficha **[!UICONTROL Validación]**. Confirme que no está recibiendo ningún error.

   ![Validación en la aplicación](assets/assurance-in-app-validate.png){zoomable="yes"}


## Cree su propio mensaje en la aplicación

Para crear su propio mensaje en la aplicación, debe definir una campaña en Journey Optimizer que almacene en déclencheur un mensaje en la aplicación en función de los eventos que se produzcan. Estos eventos pueden ser:

* datos enviados a Adobe Experience Platform,
* eventos de seguimiento principales, como la acción o el estado o la recopilación de datos PII, a través de las API genéricas principales de Mobile,
* eventos del ciclo vital de la aplicación, como inicio, instalación, actualización, cierre o bloqueo,
* eventos de geolocalización, como entrar o salir de un punto de interés.

En este tutorial, usará las API principales genéricas e independientes de la extensión de Mobile (consulte [API principales genéricas de Mobile](https://developer.adobe.com/client-sdks/documentation/mobile-core/#mobile-core-generic-apis)) para facilitar el seguimiento de eventos de pantallas de usuario, acciones y datos PII. Los eventos generados por estas API se publican en el centro de eventos de SDK y las extensiones los pueden utilizar. El centro de eventos de SDK proporciona la estructura de datos principal vinculada a todas las extensiones de SDK de Mobile Platform. Event Hub mantiene una lista de extensiones registradas y módulos internos, una lista de detectores de eventos registrados y una base de datos de estado compartida.

El centro de eventos de SDK publica y recibe datos de eventos de extensiones registradas para simplificar las integraciones con Adobe y soluciones de terceros. Por ejemplo, cuando se instala la extensión Optimize, el centro de eventos gestiona todas las solicitudes e interacciones con el motor de ofertas de Journey Optimizer - Gestión de decisiones.

1. En la interfaz de usuario de Journey Optimizer, seleccione **[!UICONTROL Campañas]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Crear campaña]**.
1. En el cuadro de diálogo **[!UICONTROL Crear su campaña]**, seleccione ![Reloj](/help/assets/icons/Clock.svg) **[!UICONTROL Programado - Marketing]** y seleccione **[!UICONTROL Confirmar]**.
1. En la pantalla **[!UICONTROL Campaign - *AAAA-MM-DD HH:MM:SS UTC+XX:XX*]**:

   1. En la ficha **[!UICONTROL Propiedades]**:

      1. Escriba un nombre para la campaña. Por ejemplo, `Luma Mobile In-App Campaign`.
      1. Si lo desea, añada una descripción.


   1. Seleccione la ficha **[!UICONTROL Acción]**.

      1. Debajo de **[!UICONTROL Mostrar mensaje si]**, seleccione ![Agregar](/help/assets/icons/Add.svg) **[!UICONTROL Agregar acción]**. En el menú desplegable, seleccione **[!UICONTROL Mensaje en la aplicación]**.
      1. En el menú desplegable **[!UICONTROL Configuración de mensajes en la aplicación]**, seleccione su configuración. Por ejemplo, **[!UICONTROL LumaInAppMessaging]**.
      1. Seleccione ![Editar](/help/assets/icons/Edit.svg) **[!UICONTROL Editar déclencheur]**.
      1. En el diálogo **[!UICONTROL déclencheur de mensajes en la aplicación]**:

         1. Seleccione **[!UICONTROL Inicio de la aplicación]** y seleccione **[!UICONTROL Seguimiento de la acción]** en el menú desplegable.
         1. Seleccione ![AddCircle](/help/assets/icons/AddCircle.svg) **[!UICONTROL Agregar condición]**.
         1. Seleccione **[!UICONTROL Acción]** y **[!UICONTROL es igual que]** en los menús desplegables.
         1. Escriba `in-app`.
         1. Seleccione ![AddCircle](/help/assets/icons/AddCircle.svg) **[!UICONTROL Agregar condición]**.
         1. Seleccione **[!UICONTROL Datos de contexto]** del menú desplegable e indique `showMessage`.
         1. Seleccione **[!UICONTROL es igual que]** en el menú desplegable y escriba `true`.

            ![Editar déclencheur](assets/edit-triggers.png){zoomable="yes"}
         1. Seleccione **[!UICONTROL Listo]**.

   1. En la pantalla de definición de campaña principal, seleccione la pestaña **[!UICONTROL Content]**.

      1. Habilitar **[!UICONTROL formato avanzado]**.
      1. Seleccione **[!UICONTROL Modal]** como **[!UICONTROL diseño de mensajería]**. En el diálogo **[!UICONTROL Cambiar diseño]**, seleccione **[!UICONTROL Cambiar diseño]**.
      1. En la ficha **[!UICONTROL Contenido]**.
         1. Escriba `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` para la **[!UICONTROL URL multimedia]**.
         1. Escriba un **[!UICONTROL encabezado]**, por ejemplo `Welcome to this Luma In-App Message` y un **[!UICONTROL cuerpo]**, por ejemplo `Triggered by pushing that button in the app...`.

         ![Contenido de mensaje en la aplicación](assets/in-app-message-content.png){zoomable="yes"}

      1. Seleccione la ficha **[!UICONTROL Configuración]**.
         1. Seleccionar **[!UICONTROL Personalizar tamaño]** en **[!UICONTROL Mensaje]**.
         1. Deshabilitar **[!UICONTROL Ajustar al contenido]**.
         1. Establezca **[!UICONTROL Altura]** en **[!UICONTROL 75%]**.

         ![Configuración de mensajes en la aplicación](assets/in-app-message-settings.png){zoomable="yes"}

1. Seleccione **[!UICONTROL Revisar para activar]**. Para editar de manera opcional cualquiera de las configuraciones de **[!UICONTROL Contenido]**, **[!UICONTROL Propiedades]**, **[!UICONTROL Acciones]** o más, seleccione ![Editar](/help/assets/icons/Edit.svg).
1. En la pantalla **[!UICONTROL Revisar para activar (*nombre de campaña*)]**, seleccione **[!UICONTROL Activar]**.
1. Después de un tiempo, verás tu **_nombre de campaña_** con el estado **[!UICONTROL Activo]** en la lista **[!UICONTROL Campañas]**.
   ![Lista de campañas](assets/ajo-campaign-list.png){zoomable="yes"}


## Déclencheur del mensaje en la aplicación

Dispone de todos los ingredientes para enviar un mensaje en la aplicación. Lo que queda es cómo almacenar en déclencheur este mensaje en la aplicación.

>[!BEGINTABS]

>[!TAB iOS]

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode. Busque la función `func sendTrackAction(action: String, data: [String: Any]?)` y agregue el código siguiente, que llama a la función [`MobileCore.track`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction), en función de los parámetros `action` y `data`.


   ```swift
   // Send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]** en el navegador del proyecto Xcode. Busque el código del botón Mensaje en la aplicación y añada el siguiente código:

   ```swift
   // Setting parameters and calling function to send in-app message
   Task {
       MobileSDK.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

>[!TAB Android]

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!DNL models]** > **[!UICONTROL MobileSDK]** en el navegador de Android Studio. Busque la función `fun sendTrackAction(action: String, data: Map<String, String>?)` y agregue el código siguiente, que llama a la función [`MobileCore.track`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction), en función de los parámetros `action` y `data`.


   ```kotlin
   // Send trackAction event
   MobileCore.track(action, data)
   ```

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.androi]** > **[!DNL views]** > **[!UICONTROL ConfigView.kt]** en el navegador de Android Studio. Busque el código del botón del controlador `onInAppMessageClick` y agregue el siguiente código:

   ```kotlin
   // Setting parameters and calling function to send in-app message
   MobileSDK.shared.sendTrackAction(
       "in-app",
       mapOf("showMessage" to "true")
   )
   ```

>[!ENDTABS]

## Validar con la aplicación

Puede validar los mensajes en la aplicación desde la propia aplicación.

>[!BEGINTABS]

>[!TAB iOS]

1. Vuelva a compilar y ejecute la aplicación en el simulador o en un dispositivo físico desde Xcode con ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Vaya a la ficha **[!UICONTROL Configuración]**.

1. Pulse **[!UICONTROL Mensaje en la aplicación]**. Verá que el mensaje en la aplicación aparece en la aplicación.

   <img src="assets/ajo-in-app-message.png" width="300" />


>[!TAB Android]

1. Vuelva a compilar y ejecute la aplicación en el simulador o en un dispositivo físico desde Android Studio con ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Vaya a la ficha **[!UICONTROL Configuración]**.

1. Pulse **[!UICONTROL Mensaje en la aplicación]**. Verá que el mensaje en la aplicación aparece en la aplicación.

   <img src="assets/ajo-in-app-message-android.png" width="300" />


>[!ENDTABS]


## Validación de la implementación en Assurance

Puede validar los mensajes en la aplicación en la interfaz de usuario de Assurance.

1. Revise la sección [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo a Assurance.
1. Seleccione **[!UICONTROL Mensajería en la aplicación]**.
1. Seleccione **[!UICONTROL Lista de eventos]**.
1. Seleccione una entrada de **[!UICONTROL Mostrar mensaje]**.
1. Inspeccione el evento sin procesar, especialmente `html`, que contiene el diseño y el contenido completos del mensaje en la aplicación.
   ![Mensaje en la aplicación de Assurance](assets/assurance-in-app-display-message.png){zoomable="yes"}


## Próximos pasos

Ahora debe tener todas las herramientas para empezar a añadir mensajes en la aplicación, cuando corresponda. Por ejemplo, promocionar productos en función de interacciones específicas que esté rastreando en la aplicación.

>[!SUCCESS]
>
>Ha habilitado la aplicación para mensajería en la aplicación y ha agregado una campaña de mensajería en la aplicación mediante Journey Optimizer y la extensión Journey Optimizer para Experience Platform Mobile SDK.
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Mobile SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=es).

Siguiente: **[Crear y mostrar ofertas](journey-optimizer-offers.md)**
