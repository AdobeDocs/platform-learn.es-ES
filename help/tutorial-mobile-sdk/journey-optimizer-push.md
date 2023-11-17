---
title: mensajería push de Adobe Journey Optimizer
description: Obtenga información sobre cómo crear mensajes push en una aplicación móvil con el SDK móvil de Platform y Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 2%

---

# mensajería push de Adobe Journey Optimizer

Obtenga información sobre cómo crear mensajes push para aplicaciones móviles con el SDK móvil de Platform y Adobe Journey Optimizer.

>[!INFO]
>
> Este tutorial se reemplazará con un nuevo tutorial con una nueva aplicación móvil de ejemplo a finales de noviembre de 2023

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

### Crear un `.p8` clave privada

1. En el portal para desarrolladores de Apple, vaya a **[!UICONTROL Claves]**.
1. Seleccione el icono + para crear una clave.
   ![crear clave nueva](assets/mobile-push-apple-dev-new-key.png)

1. Proporcione un **[!UICONTROL Nombre de clave]**.
1. Seleccione el **[!UICONTROL APN]** casilla de verificación
1. Seleccionar **[!UICONTROL Continuar]**.
   ![configurar nueva clave](assets/mobile-push-apple-dev-config-key.png)
1. Revise la configuración y seleccione **[!UICONTROL Registrar]**.
1. Descargue la `.p8` clave privada. Se utiliza en la configuración de la superficie de la aplicación.
1. Tome nota de la **[!UICONTROL ID de clave]**. Se utiliza en la configuración de la superficie de la aplicación.

Puede obtenerse documentación adicional [encontrado aquí](https://help.apple.com/developer-account/#/devcdfbb56a3).

### Recuperación del ID del equipo de desarrolladores de Apple

1. En el portal para desarrolladores de Apple, vaya a **[!UICONTROL Suscripción]**.
1. Su **[!UICONTROL Identificador de equipo]** aparece junto con el resto de la información de pertenencia. Se utiliza en la configuración de la superficie de la aplicación.

## Añadir las credenciales push de la aplicación en la recopilación de datos

1. Desde el [Interfaz de recopilación de datos](https://experience.adobe.com/data-collection/), seleccione la pestaña Superficies de la aplicación en el panel izquierdo.
1. Seleccionar **[!UICONTROL Crear superficies de aplicación]** para crear una configuración.
   ![inicio de superficie de aplicación](assets/mobile-push-app-surface.png)
1. Introduzca una **[!UICONTROL Nombre]** para la configuración, por ejemplo `Luma App Tutorial`  .
1. En Configuración de aplicaciones móviles, seleccione **[!UICONTROL Apple iOS]**.
1. Introduzca el ID del paquete de la aplicación móvil en el campo ID de aplicación (ID de paquete de iOS). Si está siguiendo junto con la aplicación de Luma, ese valor es `com.adobe.luma.tutorial`.
1. Encienda el **[!UICONTROL Credenciales push]** para añadir sus credenciales.
1. Arrastre y suelte su `.p8` **Clave de autenticación de notificación push de Apple** archivo.
1. Proporcione el ID de clave, una cadena de 10 caracteres asignada durante la creación de `p8` clave de autenticación. Se encuentra en la pestaña Claves de **Certificados, identificadores y perfiles** página.
1. Proporcione el ID de equipo. Es un valor de cadena que se puede encontrar en la variable **Suscripción** pestaña.
1. Seleccione **[!UICONTROL Guardar]**.
   ![configuración de superficie de aplicación](assets/mobile-push-app-surface-config.png)

## Instalación de la extensión Adobe Journey Optimizer tags

1. Vaya a [!UICONTROL Etiquetas] > [!UICONTROL Extensiones] > [!UICONTROL Catálogo]y busque la variable **[!UICONTROL Adobe Journey Optimizer]** extensión.
1. Instalar la extensión.
   ![instalación de la extensión ajo](assets/mobile-push-tags-install.png)
1. Seleccionar `CJM Push Tracking Experience Event Dataset` el conjunto de datos de Adobe Experience Platform.
   ![Configuración de extensión de AJO](assets/mobile-push-tags-ajo.png)
1. Seleccionar **[!UICONTROL Guardar en biblioteca y crear]**.

>[!NOTE]
>Si no ve &quot;Conjunto de datos de evento de experiencia de seguimiento push de CJM&quot; como opción, póngase en contacto con el Servicio de atención al cliente.
>

## Implementar Adobe Journey Optimizer en la aplicación

Como se ha explicado en lecciones anteriores, la instalación de una extensión de etiqueta móvil solo proporciona la configuración. A continuación, debe instalar y registrar el SDK de mensajería. Si estos pasos no están claros, consulte la [Instalación de SDK](install-sdks.md) sección.

>[!NOTE]
>
>Si ha completado la [Instalación de SDK](install-sdks.md) , el SDK ya está instalado y puede pasar al paso #7.

1. Abra su `Podfile` y agregue la línea siguiente y guarde el archivo.

   `pod 'AEPMessaging', '~>1'`
1. Abra el terminal y vaya a la carpeta que contenga su `Podfile`.
1. Instale el SDK ejecutando el comando `pod install`.
   ![validación del consentimiento](assets/mobile-push-terminal-install.png)
1. Abra XCode y vaya a `AppDelegate.swift`.
1. Añada lo siguiente a su lista de importaciones.

   `import AEPMessaging`
1. Añadir `Messaging.self` a la matriz de extensiones que está registrando.
1. Añada la siguiente función al archivo.

   ```swift
   func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       MobileCore.setPushIdentifier(deviceToken)
   }
   ```

   Esta función recupera el token del dispositivo exclusivo del dispositivo en el que está instalada la aplicación y lo envía al Adobe/Apple para la entrega de mensajes push.

## Validar enviando un mensaje push de prueba

1. Revise la [instrucciones de configuración](assurance.md) sección.
1. Instale la aplicación en su dispositivo físico.
1. Inicie la aplicación mediante la URL generada por Assurance.
1. Envíe la aplicación al segundo plano.
1. En la IU de Assurance, seleccione **[!UICONTROL Configurar]**.
   ![configurar clic](assets/mobile-push-validate-config.png)
1. Seleccione el **[!UICONTROL +]** botón situado junto a **[!UICONTROL Depuración push]**.
1. Seleccione **[!UICONTROL Guardar]**.
   ![guardar](assets/mobile-push-validate-save.png)
1. Seleccionar **[!UICONTROL Depuración push]** en el panel de navegación izquierdo.
1. Seleccione el dispositivo en la **[!UICONTROL Lista de clientes]**.
1. Confirme que no está recibiendo ningún error.
   ![validate](assets/mobile-push-validate-confirm.png)
1. Desplácese hacia abajo y seleccione **[!UICONTROL Enviar notificación push de prueba]**.
1. Confirme que no recibe los errores y que recibe el mensaje en su dispositivo.
   ![enviar inserción de prueba](assets/mobile-push-validate-send-test.png)

Siguiente: **[Conclusión y pasos siguientes](conclusion.md)**

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)