---
title: Creación y envío de notificaciones push con Platform Mobile SDK
description: Obtenga información sobre cómo crear notificaciones push en una aplicación móvil con Platform Mobile SDK y Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
jira: KT-14638
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 1%

---

# Creación y envío de notificaciones push

Obtenga información sobre cómo crear notificaciones push para aplicaciones móviles con Experience Platform Mobile SDK y Journey Optimizer.

Journey Optimizer le permite crear recorridos y enviar mensajes a audiencias de destino. Antes de enviar notificaciones push con Journey Optimizer, debe asegurarse de que las configuraciones e integraciones adecuadas estén implementadas. Para comprender el flujo de datos de notificaciones push en Journey Optimizer, consulte la [documentación](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/push/push-config/push-gs).

![Arquitectura](assets/architecture-ajo.png){zoomable="yes"}

>[!NOTE]
>
>Esta lección es opcional y solo se aplica a los usuarios de Journey Optimizer que buscan enviar notificaciones push.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.
* Configure la aplicación para Adobe Experience Platform.
* Acceso a Journey Optimizer y [permisos suficientes](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/channels/push/push-config/push-configuration). Además, necesita permisos suficientes para las siguientes funciones de Journey Optimizer.
   * Cree una credencial push.
   * Cree una configuración de canal push.
   * Cree un recorrido.
   * Cree un mensaje.
   * Cree ajustes preestablecidos de mensaje.
* Para iOS, una **cuenta de desarrollador de Apple de pago** con acceso suficiente para crear certificados, identificadores y claves.
* Para Android, una cuenta de desarrollador de Google con acceso suficiente para crear certificados y claves.
* Simulador o dispositivo físico de iOS o Android para realizar pruebas.

## Objetivos de aprendizaje

En esta lección, debe

* Registre el ID de la aplicación con el servicio de notificaciones push de Apple (APNS).
* Cree una configuración de canal en Journey Optimizer.
* Actualice el esquema para incluir los campos de mensajería push.
* Instale y configure la extensión de etiquetas de Journey Optimizer.
* Actualice la aplicación para registrar la extensión de etiqueta de Journey Optimizer.
* Valide la configuración en Assurance.
* Envío de un mensaje de prueba desde Assurance
* Defina su propio evento, recorrido y experiencia de notificaciones push en Journey Optimizer.
* Envíe su propia notificación push desde la aplicación.


## Configuración

>[!TIP]
>
>Si ya configuró su entorno como parte de la lección [Mensajería en la aplicación de Journey Optimizer](journey-optimizer-inapp.md), es posible que ya haya realizado algunos de los pasos de esta sección de configuración.

### Crear credenciales push

Para las notificaciones push, primero debe registrar la aplicación para las notificaciones push.

>[!BEGINTABS]

>[!TAB iOS]

Los siguientes pasos no son específicos de Adobe Experience Cloud y están diseñados para guiarle a través de la configuración de APNS.

1. En Apple Developer Portal, vaya a **[!UICONTROL Keys]**.
1. Para crear una clave, seleccione **[!UICONTROL +]**.

   ![crear nueva clave](assets/mobile-push-apple-dev-new-key.png){zoomable="yes"}

1. Proporcione un **[!UICONTROL Nombre de clave]**.
1. Seleccione **[!UICONTROL Servicio de notificaciones push de Apple] (APN)** y seleccione **[!UICONTROL Configurar]**.
   1. En la pantalla **[!UICONTROL Configurar clave]**, seleccione **[!UICONTROL Zona protegida y producción]** del menú desplegable **[!UICONTROL Entorno]**.
   1. Seleccione **[!UICONTROL Guardar]**.
1. Seleccione **[!UICONTROL Continuar]**.

   ![configurar nueva clave](assets/mobile-push-apple-dev-config-key.png){zoomable="yes"}

1. Revise la configuración y seleccione **[!UICONTROL Registrar]**.
1. Descargar la clave privada `.p8`. Se utiliza en el siguiente ejercicio cuando configura las credenciales push de Journey Optimizer.
1. Tome nota de la **[!UICONTROL ID de clave]**. Se utiliza en el siguiente ejercicio cuando configura las credenciales push de Journey Optimizer.
1. Tome nota de **[!UICONTROL Id. de equipo]**. Se utiliza en el siguiente ejercicio cuando configura las credenciales push de Journey Optimizer. El ID de equipo se encuentra en la parte superior derecha de la pantalla, junto al nombre de inicio de sesión.
   ![Detalles de clave](assets/push-apple-dev-key-details.png){zoomable="yes"}

Encontrará documentación adicional [aquí](https://help.apple.com/developer-account/#/devcdfbb56a3).

>[!TAB Android]

Los siguientes pasos no son específicos de Adobe Experience Cloud y están diseñados para guiarle a través de la configuración de Firebase.

1. Acceda a la consola de Firebase.
1. Seleccione **[!UICONTROL Crear un proyecto de Firebase]**.
   1. Escriba un **[!UICONTROL nombre de proyecto]**.
   1. Seleccione **[!UICONTROL Continuar]** en **[!UICONTROL Crear un proyecto]** - **[!UICONTROL Empecemos con un nombre para su proyecto]**. Por ejemplo, `Luma Android App.`
   1. Deshabilite **[!UICONTROL Gemini en Firebase]** y seleccione **[!UICONTROL Continuar]** en **[!UICONTROL Crear un proyecto]** - **[!UICONTROL Asistencia de IA para su proyecto Firebase]**.
   1. Deshabilite **[!UICONTROL Google Analytics para este proyecto]** y seleccione **[!UICONTROL Continuar]** en **[!UICONTROL Crear un proyecto]** - **[!UICONTROL Google Analytics para su proyecto Firebase]**.
   1. Seleccione **[!UICONTROL Crear proyecto]**.
   1. Una vez que el proyecto esté listo, seleccione **[!UICONTROL Continuar]**.

1. Vuelva a la consola de Firebase y asegúrese de que el proyecto esté seleccionado en la parte superior. Por ejemplo, **[!UICONTROL aplicación para Android de Luma]**.

   ![Consola Firebase](assets/fcm-1.png){zoomable="yes"}

1. Seleccione ![Configuración](/help/assets/icons/Setting.svg) > **[!UICONTROL Configuración del proyecto]**.

1. En **[!UICONTROL Configuración del proyecto]**, seleccione **[!UICONTROL Agregar aplicación]**.
   1. En **[!UICONTROL Agregar Firebase a su aplicación]**, seleccione **[!UICONTROL Android]** como plataforma.
   1. En **[!UICONTROL Agregar Firebase a su aplicación de Android:]**
      1. En el paso 1, **[!UICONTROL Registrar aplicación]**:
         1. Introduzca un nombre de paquete Android, similar al identificador de la aplicación. Por ejemplo, `com.adobe.luma.tutorial.android`.
         1. Escriba un **[!UICONTROL apodo de aplicación]** opcional.
         1. Seleccione **[!UICONTROL Registrar aplicación]**.
      1. En el paso 2, **[!UICONTROL Descargue y luego agregue el archivo de configuración]**.
         1. Seleccione ![Descargar](/help/assets/icons/Download.svg) **[!UICONTROL Descargar google-services.json]**. Cuando genere su propia versión de la aplicación de Android, debe reemplazar el archivo `google-services.json` actual en el proyecto de Android Studio de ejemplo con la versión del archivo que genera esta nueva configuración de la aplicación.
Los demás pasos se tratan en la aplicación de ejemplo.

   La pantalla debería tener un aspecto similar al siguiente:

   ![Consola Firebase](assets/fcm-2.png){zoomable="yes"}

1. En **[!UICONTROL Configuración del proyecto]**, seleccione **[!UICONTROL Cuentas de servicio]**.
1. Seleccione **[!UICONTROL Generar nueva clave privada]**. Se genera un archivo de `luma-android-app-firebase-adminsdk-xxxx-xxxxxxxx.json`. Guarde este archivo en un lugar seguro, ya que lo necesitará en una etapa posterior.

Para obtener más información, consulte la [documentación para desarrolladores de Firebase](https://firebase.google.com/docs).

>[!ENDTABS]

### Añadir las credenciales push de la aplicación en la recopilación de datos

A continuación, debe añadir las credenciales push de la aplicación móvil para autorizar a Adobe a enviar notificaciones push en su nombre. Puede agregar credenciales push en la recopilación de datos o en Journey Optimizer. En este tutorial, se utiliza la interfaz de recopilación de datos. A continuación, las credenciales push se vinculan a una configuración de canal en Journey Optimizer.

1. En Recopilación de datos, seleccione **[!UICONTROL Superficies de la aplicación]**.
1. Seleccione **[!UICONTROL Crear superficie de aplicación]**.
1. En la interfaz **[!UICONTROL Crear superficie de aplicación]**:
   1. Escriba un **[!UICONTROL Nombre]**.
   1. Seleccione **[!UICONTROL Apple iOS]** si desea enviar notificaciones push para iOS.
      1. Escriba su **[!UICONTROL id. de aplicación]**, por ejemplo `com.adobe.luma.tutorial.swiftui`.
      1. Seleccione la zona protegida (opcional).
      1. Habilitar **[!UICONTROL credenciales push]**.
      1. Suelte el archivo de clave privada `.p8` guardado en **[!UICONTROL Arrastre y suelte el archivo]**.
      1. Escriba la **[!UICONTROL Id. de clave]**.
      1. Escriba el **[!UICONTROL Id. de equipo]**.
   1. Seleccione **[!UICONTROL Android]** si desea enviar notificaciones push para Android.
      1. Escriba su **[!UICONTROL id. de aplicación]**, por ejemplo `com.adobe.luma.tutorial.android`.
      1. Seleccione la zona protegida (opcional).
      1. Habilitar **[!UICONTROL credenciales push]**.
      1. Suelte el archivo guardado de `luma-android-app-firebase-adminsdk-xxxx-xxxxxxxx.json` en **[!UICONTROL Arrastrar y soltar el archivo]**.

   ![Crear una nueva configuración de credenciales push en Journey Optimizer](assets/add-push-credentials.png){zoomable="yes"}

1. Seleccione **[!UICONTROL Guardar]**. Si toda la información es correcta, ha creado credenciales push para asociarlas a una configuración de canal.


### Cree una configuración de canal para push en Journey Optimizer

Una vez creada una configuración de credenciales push, debe crear una configuración para poder enviar notificaciones push desde Journey Optimizer.

1. En la interfaz de Journey Optimizer, abra el menú **[!UICONTROL Canales]** > **[!UICONTROL Configuración general]** > **[!UICONTROL Configuraciones de canal]** y luego seleccione **[!UICONTROL Crear configuración de canal]**.

   ![Crear una nueva configuración de canal](assets/push-config-9.png){zoomable="yes"}

1. Introduzca un nombre y una descripción (opcional) para la configuración.

   >[!NOTE]
   >
   > Los nombres deben comenzar por una letra (A-Z). Solo puede contener caracteres alfanuméricos. También puede utilizar caracteres de guion bajo `_`, punto `.` y guion `-`.


1. Para asignar etiquetas de uso de datos principales o personalizadas a la configuración, puedes seleccionar **[!UICONTROL Administrar acceso]**. [Obtenga más información acerca del Control de acceso de nivel de objeto (OLAC)](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/access-control/object-based-access).

1. Seleccione el canal **Push**.


1. Seleccione **[!UICONTROL Acciones de marketing]** para asociar directivas de consentimiento con los mensajes que usan esta configuración. Todas las políticas de consentimiento asociadas con las acciones de marketing se aprovechan para respetar las preferencias de los clientes. [Más información sobre las acciones de marketing](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/privacy/consent/consent#surface-marketing-actions).

1. Elige tu **[!UICONTROL Plataforma]**. Puedes configurar **[!UICONTROL iOS]** y **[!UICONTROL Android]** para una configuración de canal.

1. Seleccione el **[!UICONTROL ID de aplicación]** apropiado que utilizó anteriormente para definir sus credenciales de inserción. Por ejemplo, **[!UICONTROL com.adobe.luma.tutorial.swiftui]** para iOS y **[!UICONTROL com.adobe.luma.tutorial.android]** para Android. El ![círculo de verificación](/help/assets/icons/CheckmarkCircle.svg) verde indica que las credenciales push válidas están asociadas a una configuración de canal.


   ![Configuración de canal push](assets/push-config-10.png){zoomable="yes"}

1. Seleccione **[!UICONTROL Enviar]** para guardar los cambios.




### Actualizar configuración de secuencia de datos

Para garantizar que los datos enviados desde su aplicación móvil a Edge Network se reenvíen a Journey Optimizer, actualice la configuración de Experience Edge

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y su secuencia de datos, por ejemplo **[!DNL Luma Mobile App]**.
1. Seleccione ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) para **[!UICONTROL Experience Platform]** y seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar]** en el menú contextual.
1. En la pantalla **[!UICONTROL Datastreams]** > ![Folder](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]**:

   1. Si aún no está seleccionado, seleccione **[!UICONTROL Conjunto de datos del perfil push de AJO]** de **[!UICONTROL Conjunto de datos de perfil]**. Este conjunto de datos de perfil es necesario al usar la llamada API `MobileCore.setPushIdentifier` (consulte [Registrar el token de dispositivo para notificaciones push](#register-device-token-for-push-notifications)). Esta selección también garantiza que el identificador único de las notificaciones push (también conocido como identificador push) se almacene como parte del perfil del usuario.

   1. **[!UICONTROL Adobe Journey Optimizer]** está seleccionado. Consulte [Configuración de Adobe Experience Platform](https://experienceleague.adobe.com/es/docs/experience-platform/datastreams/configure) para obtener más información.

   1. Para guardar la configuración de su secuencia de datos, seleccione **[!UICONTROL Guardar]**.

   ![Configuración de secuencia de datos de AEP](assets/datastream-aep-configuration.png){zoomable="yes"}



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
      ![Configuración de la extensión de AJO](assets/push-tags-ajo.png){zoomable="yes"}

>[!NOTE]
>
>Si no ve **[!UICONTROL Conjunto de datos de evento de experiencia de seguimiento push de AJO]** como opción, póngase en contacto con el servicio de atención al cliente.
>

## Validar la configuración con Assurance

1. Revise la sección [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo a Assurance.
1. En la IU de Assurance, seleccione **[!UICONTROL Configurar]**.
   ![configurar clic](assets/push-validate-config.png){zoomable="yes"}
1. Seleccione ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a **[!UICONTROL Push Debug]**.
1. Seleccione **[!UICONTROL Guardar]**.
   ![guardar](assets/push-validate-save.png){zoomable="yes"}
1. Seleccione **[!UICONTROL Push Debug]** en el panel de navegación izquierdo.
1. Seleccione la ficha **[!UICONTROL Validar configuración]**.
1. Seleccione su dispositivo de la lista **[!UICONTROL Cliente]**.
1. Confirme que no está recibiendo ningún error.
   ![validar](assets/push-validate-confirm.png){zoomable="yes"}
1. Seleccione la ficha **[!UICONTROL Enviar inserción de prueba]**.
1. (opcional) Cambie los detalles predeterminados de **[!UICONTROL Title]** y **[!UICONTROL Body]** y asegúrese de proporcionar todos los parámetros que espera su aplicación, como **[!UICONTROL Advanced]** > **[!UICONTROL Notification Channel]** (requerido para Android, por ejemplo `LUMA_CHANNEL_ID`).
1. Seleccione ![Error](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL Enviar notificación push de prueba]**.
1. Compruebe **[!UICONTROL resultados de la prueba]**.

   ![Probar notificaciones push desde Assurance](assets/test-push.png){zoomable="yes"}
1. Debería ver la notificación push de prueba en la aplicación.

>[!BEGINTABS]

>[!TAB iOS]

<img src="assets/luma-app-push.png" width="300" />

>[!TAB Android]

<img src="assets/luma-app-push-android.png" width="300" />

>[!ENDTABS]

## Firma

>[!IMPORTANT]
>
>La firma de una aplicación de iOS es necesaria para enviar notificaciones push en iOS y **requiere una cuenta de desarrollador de Apple de pago**. No es necesario que firme una aplicación de Android para enviar notificaciones push.


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
>Para implementar y probar las notificaciones push en una aplicación de iOS, debes tener una cuenta de desarrollador de Apple **de pago**.

>[!BEGINTABS]

>[!TAB iOS]

1. En Xcode, seleccione **[!DNL Luma]** de la lista **[!UICONTROL TARGETS]**, seleccione la pestaña **[!UICONTROL Firma y capacidades]**, seleccione el botón **[!UICONTROL + capacidad]** y, a continuación, seleccione **[!UICONTROL Notificaciones push]**. Esta selección permite que la aplicación reciba notificaciones push.

1. A continuación, debe añadir una extensión de notificación a la aplicación. Vuelva a la ficha **[!DNL General]** y seleccione el icono **[!UICONTROL +]** en la parte inferior de la sección **[!UICONTROL TARGETS]**.

1. Se le pedirá que seleccione la plantilla para el nuevo destino. Seleccione **[!UICONTROL Extensión del servicio de notificaciones]** y, a continuación, seleccione **[!UICONTROL Siguiente]**.

1. En la siguiente ventana, use `NotificationExtension` como nombre de la extensión y haga clic en el botón **[!UICONTROL Finalizar]**.

Ahora debería tener una extensión de notificación push agregada a la aplicación, similar a la pantalla siguiente.

![Extensión de notificaciones push](assets/xcode-signing-capabilities-pushnotifications.png){zoomable="yes"}

>[!TAB Android]

El proyecto de Android Studio ya está configurado para las notificaciones push. No es necesario que realice pasos adicionales para habilitar la versión de Android de la aplicación Luma para las notificaciones push. Consulte [Acerca de las notificaciones](https://developer.android.com/develop/ui/views/notifications) para obtener más información.

Las notificaciones push de Android requieren que defina un id de canal de notificación, tanto en la aplicación como al enviar una notificación push. El id. de notificación de canal utilizado en la aplicación de Android Luma es `LUMA_CHANNEL ID`.

>[!ENDTABS]


## Implementar Journey Optimizer en la aplicación

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

1. En Android Studio, asegúrese de que [aepsdk-messaing-android](https://github.com/adobe/aepsdk-messaging-android) forme parte de las dependencias de **[!UICONTROL build.gradle.kts (Módulo :app)]** en **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) **[!UICONTROL Gradle Scripts]**. Ver [Gradle](install-sdks.md#gradle).
1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** en el navegador de proyectos de Android Studio.
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



## Registrar un token de dispositivo para notificaciones push

Debe registrar el token del dispositivo para las notificaciones push.

>[!BEGINTABS]

>[!TAB iOS]

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** en el navegador del proyecto Xcode.
1. Agregar la API [`MobileCore.setPushIdentifier`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setpushidentifier) a la función `func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data)`.

   ```swift
   // Send push token to Mobile SDK
   MobileCore.setPushIdentifier(deviceToken)
   ```

   Esta función recupera el token del dispositivo exclusivo del dispositivo en el que está instalada la aplicación. A continuación, establece el token para la entrega de notificaciones push mediante la configuración que ha configurado y que depende del servicio de notificaciones push de Apple (APN).

>[!TAB Android]

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** en el navegador de proyectos de Android Studio.
1. Agregue la API [`MobileCore.setPushIdentifier`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setpushidentifier) a la función `override fun onCreate()` en `class LumaAplication : Application`, en `FirebaseMessaging.getInstance().token.addOnCompleteListener`.

   ```kotlin
   // Send push token to Mobile SDK
   MobileCore.setPushIdentifier(token)
   ```

   Esta función recupera el token del dispositivo exclusivo del dispositivo en el que está instalada la aplicación. A continuación, establece el token para la entrega de notificaciones push mediante la configuración que ha configurado y que depende de Firebase Cloud Messaging (FCM).

>[!ENDTABS]

>[!IMPORTANT]
>
>**Solo para iOS**: `MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])` determina si las notificaciones push utilizan una zona protegida de APNS o un servidor de producción para enviar notificaciones push. Al probar la aplicación en el simulador o en un dispositivo, asegúrese de que `messaging.useSandbox` está establecido en `true` para que reciba notificaciones push. Al implementar su aplicación para producción con fines de prueba mediante Testflight de Apple, asegúrese de establecer `messaging.useSandbox` en `false`; de lo contrario, la aplicación de producción no podrá recibir notificaciones push.<br/><br/>
>&#x200B;>Firebase Cloud Messaging (FCM) **no** admite el concepto de zonas protegidas para notificaciones push.


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

      ![Agregar valor a tipos de eventos](assets/ajo-update-schema-eventtype-enum.png){zoomable="yes"}

### Definición de un evento

Los eventos de Journey Optimizer permiten almacenar en déclencheur recorridos para enviar mensajes como, por ejemplo, notificaciones push. Consulte [Acerca de los eventos](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/configure-journeys/events-journeys/about-events) para obtener más información.

1. En la interfaz de usuario de Journey Optimizer, seleccione **[!UICONTROL Configuraciones]** en el carril izquierdo.

1. En la pantalla **[!UICONTROL Tablero]**, seleccione el botón **[!UICONTROL Administrar]** en el mosaico **[!UICONTROL Eventos]**.

1. En la pantalla **[!UICONTROL Eventos]**, seleccione **[!UICONTROL Crear evento]**.

1. En el panel **[!UICONTROL Editar evento de evento1]**:

   1. Escriba `LumaTestEvent` como **[!UICONTROL Nombre]** del evento.
   1. Proporcione una **[!UICONTROL descripción]**, por ejemplo `Test event to trigger push notifications in Luma app`.

   1. Seleccione el esquema del evento de experiencia de la aplicación móvil que creó anteriormente en [Crear un esquema XDM](create-schema.md) desde la lista **[!UICONTROL Esquema]**, por ejemplo **[!DNL Luma Mobile App Event Schema v.1]**.
   1. Seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) junto a la lista **[!UICONTROL Campos]**.

      ![Editar paso de evento 1](assets/ajo-edit-event1.png){zoomable="yes"}

      En el cuadro de diálogo **[!UICONTROL Campos]**, asegúrese de que los siguientes campos estén seleccionados (sobre los campos predeterminados que siempre están seleccionados (**[!UICONTROL _id]**, **[!UICONTROL id]** y **[!UICONTROL timestamp]**)). Con la lista desplegable, puede alternar entre **[!UICONTROL Seleccionado]**, **[!UICONTROL Todo]** y **[!UICONTROL Principal]**, o usar el campo ![Buscar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg).

      * **[!UICONTROL Aplicación identificada (id.)]**,
      * **[!UICONTROL Tipo de evento (eventType)]**,
      * **[!UICONTROL Principal (principal)]**.

      ![Editar campos de evento](assets/ajo-event-fields.png){zoomable="yes"}

      A continuación, seleccione **[!UICONTROL Aceptar]**.

   1. Seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) junto al campo **[!UICONTROL Condición de ID de evento]**.

      1. En el cuadro de diálogo **[!UICONTROL Agregar una condición de id. de evento]**, arrastre y suelte **[!UICONTROL Tipo de evento (eventType)]** en **[!UICONTROL Arrastrar y soltar un elemento aquí]**.
      1. En la ventana emergente, desplácese hasta la parte inferior y seleccione **[!UICONTROL application.test]** (que es el tipo de evento que agregó anteriormente a la lista de tipos de eventos como parte de [Actualizar el esquema](#update-your-schema)). A continuación, desplácese hacia arriba y seleccione **[!UICONTROL Aceptar]**.
      1. Seleccione **[!UICONTROL Aceptar]** para guardar la condición.
         ![Editar condición de evento](assets/ajo-edit-condition.png){zoomable="yes"}

   1. Seleccione **[!UICONTROL ECID (ECID)]** de la lista **[!UICONTROL Espacio de nombres]**. Automáticamente, el campo **[!UICONTROL Identificador de perfil]** se rellena con **[!UICONTROL El identificador del primer elemento del ECID de clave para el identityMap]** del mapa.
   1. Seleccione **[!UICONTROL Guardar]**.
      ![Editar paso de evento 2](assets/ajo-edit-event2.png){zoomable="yes"}

Acaba de crear una configuración de evento basada en el esquema de eventos de experiencia de la aplicación móvil creado anteriormente como parte de este tutorial. Esta configuración de evento filtrará los eventos de experiencia entrantes usando su tipo de evento específico (`application.test`), de modo que solo los eventos con ese tipo específico, iniciados desde su aplicación móvil, almacenarán en déclencheur el recorrido que genere en el siguiente paso. En una situación real, es posible que desee enviar notificaciones push desde un servicio externo. Sin embargo, se aplican los mismos conceptos: desde la aplicación externa, envíe un evento de experiencia a Experience Platform que tenga campos específicos que pueda utilizar para aplicar condiciones en antes de que estos eventos entren en déclencheur con un recorrido.

### Creación del recorrido

El siguiente paso es crear el recorrido que almacene en déclencheur el envío de la notificación push al recibir el evento correspondiente.

1. En la interfaz de usuario de Journey Optimizer, seleccione **[!UICONTROL Recorridos]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Crear Recorrido]**.
1. En el panel **[!UICONTROL Propiedades del Recorrido]**:

   1. Escriba un **[!UICONTROL Nombre]** para el recorrido, por ejemplo `Luma - Test Push Notification Journey`.
   1. Escriba una **[!UICONTROL descripción]** para el recorrido, por ejemplo `Journey for test push notifications in Luma mobile app`.
   1. Asegúrese de seleccionar **[!UICONTROL Permitir la reentrada]** y establezca **[!UICONTROL Período de espera de reentrada]** en **[!UICONTROL 30]** **[!UICONTROL Segundos]**.
   1. Seleccione **[!UICONTROL Aceptar]**.
      ![Propiedades del recorrido](assets/ajo-journey-properties.png){zoomable="yes"}

1. En el lienzo del recorrido, en **[!UICONTROL EVENTS]**, arrastra y suelta tu ![evento](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg) **[!DNL LumaTestEvent]** en el lienzo donde se muestra **[!UICONTROL Selecciona un evento de entrada o una actividad de lectura de audiencia]**.

   * En el panel **[!UICONTROL Eventos: LumaTestEvent]**, escriba una **[!UICONTROL Etiqueta]**, por ejemplo `Luma Test Event`.

1. En el menú desplegable **[!UICONTROL ACCIONES]**, arrastra y suelta ![Insertar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PushNotification_18_N.svg) **[!UICONTROL Insertar]** en el ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) que aparece a la derecha de tu actividad **[!DNL LumaTestEvent]**. En el panel **[!UICONTROL Acciones: Push]**:

   1. Proporcione una **[!UICONTROL Etiqueta]**, por ejemplo `Luma Test Push Notification`, proporcione una **[!UICONTROL Descripción]**, por ejemplo `Test push notification for Luma mobile app`, seleccione **[!UICONTROL Transaccional]** de la lista **[!UICONTROL Categoría]** y seleccione **[!DNL Luma]** de la **[!UICONTROL Superficie de inserción]**.
   1. Seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar contenido]** para comenzar a editar la notificación push real.

      ![Propiedades push](assets/ajo-push-properties.png){zoomable="yes"}

      En el editor de **[!UICONTROL notificaciones push]**:

      1. Escriba un **[!UICONTROL Título]**, por ejemplo `Luma Test Push Notification` y un **[!UICONTROL Cuerpo]**, por ejemplo `Test push notification for Luma mobile app`.
      1. Opcionalmente, puede escribir un vínculo a una imagen (.png o .jpg) en **[!UICONTROL Agregar medios]**. Si lo hace, la imagen forma parte de la notificación push. Tenga en cuenta que, si lo hace, debe encargarse de gestionar correctamente la imagen en la aplicación móvil.
      1. Para guardar y salir del editor, selecciona ![Chevron left](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronLeft_18_N.svg).

         ![Editor push](assets/ajo-push-editor.png){zoomable="yes"}

   1. Para guardar y finalizar la definición de la notificación push, seleccione **[!UICONTROL Aceptar]**.

1. El recorrido debe ser similar al siguiente. Seleccione **[!UICONTROL Publicar]** para publicar y activar su recorrido.
   ![recorrido finalizado](assets/ajo-journey-finished.png){zoomable="yes"}


## Déclencheur de la notificación push

Tiene todos los ingredientes para enviar una notificación push. Lo que queda es cómo almacenar en déclencheur esta notificación push. En esencia, es lo mismo que ha visto antes: simplemente envíe un evento de experiencia con la carga útil adecuada (como en [Eventos](events.md)).

Esta vez, el evento de experiencia que está a punto de enviar no se construye construyendo un diccionario XDM simple. Va a usar un(a) `struct` que representa una carga de notificación push. La definición de un tipo de datos dedicado es una forma alternativa de implementar la construcción de cargas útiles de evento de experiencia en la aplicación.

Tenga en cuenta que, únicamente con fines ilustrativos, envía una notificación push desde la aplicación. Un escenario más habitual es el envío del evento de experiencia (que almacena en déclencheur el recorrido de notificaciones push) desde otra aplicación o servicio.

>[!BEGINTABS]

>[!TAB iOS]

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

   El código es una representación de la siguiente carga útil simple que va a enviar al déclencheur de su recorrido de notificaciones push de prueba.

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

   Este código crea una instancia de `testPushPayload` utilizando los parámetros proporcionados a la función (`applicationId` y `eventType`) y, a continuación, llama a `sendExperienceEvent` mientras convierte la carga útil en un diccionario. Este código también tiene en cuenta los aspectos asíncronos de llamar a Adobe Experience Platform SDK mediante el uso del modelo de concurrencia de Swift, basado en `await` y `async`.

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]** en el navegador del proyecto Xcode. En la definición del botón de notificación push, añada el siguiente código para enviar la carga útil del evento de experiencia de notificación push de prueba al déclencheur del recorrido cada vez que se pulse ese botón.

   ```swift
   // Setting parameters and calling function to send push notification
   Task {
       let eventType = testPushEventType
       let applicationId = Bundle.main.bundleIdentifier ?? "No bundle id found"
       await MobileSDK.shared.sendTestPushEvent(applicationId: applicationId, eventType: eventType)
   }
   ```

>[!TAB Android]

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL xdm]** > **[!UICONTROL TestPushPayload.kt]** en el navegador de Android Studio e inspeccione el código.

   ```kotlin
   import com.google.gson.annotations.SerializedName
   
   data class TestPushPayload(
      @SerializedName("application") val application: Application,
      @SerializedName("eventType") val eventType: String
   ) {
      fun asMap(): Map<String, Any> {
         return mapOf(
               "application" to application.asMap(),
               "eventType" to eventType
         )
      }
   }
   
   data class Application(
      @SerializedName("id") val id: String
   ) {
      fun asMap(): Map<String, Any> {
         return mapOf(
               "id" to id
         )
      }
   }
   ```

   El código es una representación de la siguiente carga útil simple que va a enviar al déclencheur de su recorrido de notificaciones push de prueba.

   ```json
   {
      "eventType": string,
      "application" : [
          "id": string
      ]
   }
   ```

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** en el navegador de Android Studio y agregue el siguiente código a `func sendTestPushEvent(applicationId: String, eventType: String)`:

   ```kotlin
   // Create payload and send experience event
   val testPushPayload = TestPushPayload(
      Application(applicationId),
      eventType
   )
   sendExperienceEvent(testPushPayload.asMap())
   ```

   Este código crea una instancia de `testPushPayload` utilizando los parámetros proporcionados a la función (`applicationId` y `eventType`) y, a continuación, llama a `sendExperienceEvent` mientras convierte la carga útil en un mapa.

1. Vaya a **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.android.tutorial]** > **[!DNL views]** > **[!UICONTROL ConfigView.kt]** en el navegador de Android Studio. En la definición del botón de notificación push, añada el siguiente código para enviar la carga útil del evento de experiencia de notificación push de prueba al déclencheur del recorrido cada vez que se pulse ese botón.

   ```kotlin
   // Setting parameters and calling function to send push notification
   val eventType = testPushEventType
   val applicationId = context.packageName
   scope.launch {
         MobileSDK.shared.sendTestPushEvent(
            applicationId,
            eventType
         )
   }
   ```


>[!ENDTABS]

## Validar con la aplicación

Para validar el evento y el recorrido de las notificaciones push:

>[!BEGINTABS]

>[!TAB iOS]

1. Vuelva a compilar y ejecute la aplicación en el simulador o en un dispositivo físico desde Xcode con ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Vaya a la ficha **[!UICONTROL Configuración]**.

1. Pulse **[!UICONTROL Notificación push]**.


   Verá la notificación push en la parte superior de la aplicación.

   <img src="assets/ajo-test-push.png" width="300" />

>[!TAB Android]

1. Vuelva a compilar y ejecute la aplicación en el simulador o en un dispositivo físico desde Android Studio con ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Vaya a la ficha **[!UICONTROL Configuración]**.

1. Pulse **[!UICONTROL Notificación push]**.

   Verá la notificación push en la parte superior de la aplicación.

   <img src="assets/ajo-test-push-android.png" width="300" />

>[!ENDTABS]

El modo de gestionar y mostrar la notificación push en la propia aplicación va más allá del tema de esta sección. Cada plataforma implementa la gestión y muestra las notificaciones de una manera específica. Consulte para obtener más información:

* Para iOS: [Notificaciones de usuario](https://developer.apple.com/documentation/usernotifications)
* Para Android: [Mensajería en la nube](https://firebase.google.com/docs/cloud-messaging)

## Próximos pasos

Ahora debe tener todas las herramientas para gestionar las notificaciones push en la aplicación. Por ejemplo, puede crear un recorrido en Journey Optimizer que envíe una notificación push de bienvenida cuando un usuario de la aplicación inicie sesión. O una notificación push de confirmación cuando un usuario compra un producto en la aplicación. O bien, introduce la geovalla de una ubicación (como se ve en la lección [Places](places.md)).

>[!SUCCESS]
>
>Ahora ha habilitado la aplicación para notificaciones push mediante Journey Optimizer y la extensión de Journey Optimizer para Experience Platform Mobile SDK.
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Mobile SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=es).

Siguiente: **[Crear y enviar mensajes en la aplicación](journey-optimizer-inapp.md)**
