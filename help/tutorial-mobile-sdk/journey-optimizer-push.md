---
title: Mensajería push de Adobe Journey Optimizer
description: Obtenga información sobre cómo crear mensajes push en una aplicación móvil con Platform Mobile SDK y Adobe Journey Optimizer.
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 2%

---

# Mensajería push de Adobe Journey Optimizer

Obtenga información sobre cómo crear mensajes push para aplicaciones móviles con Platform Mobile SDK y Adobe Journey Optimizer.

Journey Optimizer le permite crear sus recorridos y enviar mensajes a las audiencias de destino. Antes de enviar notificaciones push con Journey Optimizer, debe asegurarse de que las configuraciones e integraciones adecuadas estén implementadas. Para comprender el flujo de datos de las notificaciones push en Adobe Journey Optimizer, consulte [la documentación](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>Esta lección es opcional y solo se aplica a los usuarios de Adobe Journey Optimizer que buscan enviar mensajes push.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con SDK instalados y configurados.
* Acceso a Adobe Journey Optimizer y permisos suficientes como se describe [here](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). También necesita permisos suficientes para las siguientes funciones de Adobe Journey Optimizer.
   * Cree una superficie de aplicación.
   * Creación de un recorrido
   * Cree un mensaje.
   * Creación de ajustes preestablecidos de mensaje.
* Cuenta de desarrollador de Apple de pago con acceso suficiente para crear certificados, identificadores y claves.
* Dispositivo físico iOS para realizar pruebas.

## Objetivos de aprendizaje

En esta lección:

* Registro del ID de aplicación con el servicio de notificaciones push de Apple (APN).
* Cree un **[!UICONTROL Superficie de la aplicación]** en AJO.
* Actualice su **[!UICONTROL esquema]** para incluir los campos de mensajería push.
* Instale y configure el **[!UICONTROL Adobe Journey Optimizer]** extensión de etiqueta.
* Actualice la aplicación para incluir la extensión de etiqueta AJO.
* Valide la configuración en Assurance.
* Envíe un mensaje de prueba.


## Registro del ID de aplicación con APN

Los siguientes pasos no son específicos de Adobe Experience Cloud y están diseñados para guiarle a través de la configuración APN.

### Cree un `.p8` clave privada

1. En el portal para desarrolladores de Apple, vaya a **[!UICONTROL Claves]**.
1. Seleccione el icono + para crear una clave.
   ![crear nueva clave](assets/mobile-push-apple-dev-new-key.png)

1. Proporcione un **[!UICONTROL Nombre de clave]**.
1. Seleccione el **[!UICONTROL APN]** casilla de verificación.
1. Select **[!UICONTROL Continuar]**.
   ![configurar nueva clave](assets/mobile-push-apple-dev-config-key.png)
1. Revise la configuración y seleccione **[!UICONTROL Registro]**.
1. Descargue el `.p8` clave privada. Se utiliza en la configuración de la superficie de la aplicación.
1. Tenga en cuenta que **[!UICONTROL ID de clave]**. Se utiliza en la configuración de la superficie de la aplicación.

Puede encontrar documentación adicional [se encuentra aquí](https://help.apple.com/developer-account/#/devcdfbb56a3).

### Recupere su ID de equipo de desarrollador de Apple

1. En el portal para desarrolladores de Apple, vaya a **[!UICONTROL Membresía]**.
1. Su **[!UICONTROL ID del equipo]** aparece junto con la información de otros miembros. Se utiliza en la configuración de la superficie de la aplicación.

## Añadir las credenciales push de la aplicación en la recopilación de datos

1. En el [Interfaz de recopilación de datos](https://experience.adobe.com/data-collection/), seleccione la ficha Superficies de la aplicación en el panel izquierdo.
1. Select **[!UICONTROL Crear superficies de aplicación]** para crear una configuración.
   ![inicio de la superficie de la aplicación](assets/mobile-push-app-surface.png)
1. Escriba un **[!UICONTROL Nombre]** para la configuración, por ejemplo `Luma App Tutorial`  .
1. En Configuración de aplicaciones móviles, seleccione **[!UICONTROL Apple iOS]**.
1. Introduzca el ID del paquete de la aplicación móvil en el campo ID de la aplicación (ID del paquete de iOS) . Si va a seguir junto con la aplicación de Luma, ese valor es `com.adobe.luma.tutorial`.
1. Active el **[!UICONTROL Credenciales push]** para añadir las credenciales.
1. Arrastre y suelte `.p8` **Clave de autenticación de notificaciones push de Apple** archivo.
1. Proporcione el ID de clave, una cadena de 10 caracteres asignada durante la creación de `p8` clave de autenticación. Se encuentra en la ficha Claves de **Certificados, identificadores y perfiles** página.
1. Proporcione el ID de equipo. Este es un valor de cadena que se puede encontrar en la sección **Membresía** pestaña .
1. Seleccione **[!UICONTROL Guardar]**.
   ![configuración de superficie de la aplicación](assets/mobile-push-app-surface-config.png)

## Instalación de la extensión de etiquetas Adobe Journey Optimizer

1. Vaya a [!UICONTROL Etiquetas] > [!UICONTROL Extensiones] > [!UICONTROL Catálogo]y busque la variable **[!UICONTROL Adobe Journey Optimizer]** extensión.
1. Instale la extensión .
   ![instalar extensión ajo](assets/mobile-push-tags-install.png)
1. Select `CJM Push Tracking Experience Event Dataset` el conjunto de datos de Adobe Experience Platform.
   ![Configuración de la extensión AJO](assets/mobile-push-tags-ajo.png)
1. Select **[!UICONTROL Guardar en biblioteca y crear]**.

>[!NOTE]
>Si no ve &quot;CJM Push Tracking Experience Event Dataset&quot; como una opción, póngase en contacto con el servicio de atención al cliente.

## Implementar Adobe Journey Optimizer en la aplicación

Como se ha explicado en lecciones anteriores, la instalación de una extensión de etiqueta móvil solo proporciona la configuración. A continuación, debe instalar y registrar el SDK de mensajería. Si estos pasos no están claros, revise la [Instalación de SDK](install-sdks.md) para obtener más información.

>[!NOTE]
>
>Si ha completado el [Instalación de SDK](install-sdks.md) , el SDK ya está instalado y puede ir al paso 7.

1. Abra su `Podfile` y agregue la línea siguiente y guarde el archivo .

   `pod 'AEPMessaging', '~>1'`
1. Abra el terminal y vaya a la carpeta que contiene su `Podfile`.
1. Instalación del SDK ejecutando el comando `pod install`.
   ![validar consentimiento](assets/mobile-push-terminal-install.png)
1. Abra XCode y vaya a `AppDelegate.swift`.
1. Añada lo siguiente a su lista de importaciones.

   `import AEPMessaging`
1. Agregar `Messaging.self` a la matriz de extensiones que está registrando.
1. Añada la siguiente función al archivo .

   ```swift
   func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       MobileCore.setPushIdentifier(deviceToken)
   }
   ```

   Esta función recupera el token del dispositivo exclusivo del dispositivo en el que está instalada la aplicación y lo envía a Adobe/Apple para la entrega de mensajes push.

## Validación enviando un mensaje push de prueba

1. Consulte la [instrucciones de configuración](assurance.md) para obtener más información.
1. Instale la aplicación en su dispositivo físico.
1. Inicie la aplicación con la URL generada por Assurance.
1. Envíe la aplicación al fondo.
1. En la interfaz de usuario de Assurance, seleccione **[!UICONTROL Configurar]**.
   ![configurar clic](assets/mobile-push-validate-config.png)
1. Seleccione el **[!UICONTROL +]** junto a **[!UICONTROL Depuración push]**.
1. Seleccione **[!UICONTROL Guardar]**.
   ![guardar](assets/mobile-push-validate-save.png)
1. Select **[!UICONTROL Depuración push]** desde el panel de navegación izquierdo.
1. Seleccione el dispositivo en la **[!UICONTROL Lista de clientes]**.
1. Confirme que no está obteniendo ningún error.
   ![validate](assets/mobile-push-validate-confirm.png)
1. Desplácese hacia abajo y seleccione **[!UICONTROL Enviar notificación push de prueba]**.
1. Confirme que no recibe errores y que recibe el mensaje en su dispositivo.
   ![enviar push de prueba](assets/mobile-push-validate-send-test.png)

Siguiente: **[Conclusión y pasos siguientes](conclusion.md)**

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK de Adobe Experience Platform Mobile. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)