---
title: mensajería push de Adobe Journey Optimizer
description: Obtenga información sobre cómo crear mensajes push en una aplicación móvil con el SDK móvil de Platform y Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 1%

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
* Dispositivo iOS físico para pruebas.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Registre el ID de la aplicación con el servicio de notificaciones push de Apple (APN).
* Crear un **[!UICONTROL Superficie de aplicación]** en AJO.
* Actualice su **[!UICONTROL esquema]** para incluir campos de mensajería push.
* Instalación y configuración de **[!UICONTROL Adobe Journey Optimizer]** extensión de etiqueta.
* Actualice la aplicación para incluir la extensión de etiqueta AJO.
* Valide la configuración en Assurance.
* Enviar un mensaje de prueba.


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
1. Abra Xcode y vaya a **[!UICONTROL AppDelegate]**.
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

1. Añada el `MobileCore.setPushIdentifier` a la `application(_, didRegisterForRemoteNotificationsWithDeviceToken)` función.

   ```swift {highlight="7"}
   func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       // Required to log the token
       let tokenParts = deviceToken.map { data in String(format: "%02.2hhx", data) }
       let token = tokenParts.joined()
       Logger.notifications.info("didRegisterForRemoteNotificationsWithDeviceToken - device token: \(token)")
   
       // Send push token to Experience Platform
       MobileCore.setPushIdentifier(deviceToken)
       currentDeviceToken = token
   }
   ```

   Esta función recupera el token del dispositivo exclusivo del dispositivo en el que está instalada la aplicación y lo envía a Apple de Adobe para la entrega de mensajes push.

## Validar enviando un mensaje push de prueba

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


>[!SUCCESS]
>
>Ahora ha habilitado la aplicación para notificaciones push mediante la extensión de Adobe Journey Optimizer para el SDK de Adobe Experience Platform Mobile.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Conclusión y pasos siguientes](conclusion.md)**
