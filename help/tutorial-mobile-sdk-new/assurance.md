---
title: Configurar Assurance
description: Obtenga información sobre cómo implementar la extensión Assurance en una aplicación móvil.
feature: Mobile SDK,Assurance
hide: true
source-git-commit: b3cf168fc9b20ea78df0f8863a6395e9a45ed832
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 10%

---

# Assurance

Obtenga información sobre cómo configurar Adobe Experience Platform Assurance en una aplicación móvil.

Assurance, anteriormente conocido como Project Griffon, está diseñado para ayudarle a inspeccionar, probar, simular y validar la forma en que recopila datos o sirve experiencias en su aplicación móvil.

Assurance le ayuda a inspeccionar los eventos de SDK sin procesar generados por el SDK para móviles de Adobe Experience Platform. Todos los eventos recopilados por el SDK están disponibles para su inspección. Los eventos del SDK se cargan en una vista de lista, ordenados por tiempo. Cada evento tiene una vista detallada que proporciona más detalles. También se proporcionan vistas adicionales para examinar la configuración del SDK, los elementos de datos, los estados compartidos y las versiones de extensión del SDK. Obtenga más información acerca de [Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html) en la documentación del producto.


## Requisitos previos

* La aplicación se ha configurado y instalado correctamente con los SDK.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Confirme que su organización tiene acceso a (y solicítelo si no lo tiene).
* Configure la dirección URL base.
* Añada el código específico de iOS requerido.
* Conexión a una sesión.

## Confirmar acceso

Confirme que su organización tiene acceso a Assurance. Usted, como usuario, debe añadirse al perfil de Adobe Experience Platform. Consulte [Acceso de usuario](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=en) en la Guía de Assurance para obtener más información.

## Implementación

Además de la [Instalación del SDK](install-sdks.md)Sin embargo, como ha completado la lección anterior, iOS también requiere la siguiente adición para iniciar la sesión de Assurance para su aplicación.

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL SceneDelegate]** en el navegador de proyectos de Xcode.

1. Añada el siguiente código a `func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>`:

   ```swift
   // Called when the app in background is opened with a deep link.
   if let deepLinkURL = URLContexts.first?.url {
       // Start the Assurance session
       Assurance.startSession(url: deepLinkURL)
   }
   ```

   Este código inicia una sesión de garantía cuando la aplicación se encuentra en segundo plano y abierta mediante un vínculo profundo.

Puede encontrar más información [aquí](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.

## Firmar

Antes de ejecutar la aplicación por primera vez en Xcode, asegúrese de actualizar la firma.

1. Abra el proyecto  en Xcode.
1. Seleccionar **[!UICONTROL Luma]** en el navegador del proyecto.
1. Seleccione el **[!UICONTROL Luma]** objetivo.
1. Seleccione el **Firma y capacidades** pestaña.
1. Configurar **[!UICONTROL Administrar firma automáticamente]**, **[!UICONTROL Equipo]**, y **[!UICONTROL Identificador de paquete]** o use los detalles específicos de aprovisionamiento de desarrollo de Apple.

   ![Funcionalidades de firma de Xcode](assets/xcode-signing-capabilities.png){zoomable=&quot;yes&quot;}

## Configuración de una dirección URL base

1. Vaya al proyecto en Xcode.
1. Seleccionar **[!UICONTROL Luma]** en el navegador del proyecto.
1. Seleccione el **[!UICONTROL Luma]** objetivo.
1. Seleccione el **Información** pestaña.
1. Para añadir una URL base, desplácese hacia abajo hasta **Tipos de URL** y seleccione la **+** botón.
1. Establecer **Identificador** al identificador de paquete configurado en [Firma](#signing) (por ejemplo, `com.adobe.luma.tutorial.swiftui`) y establezca un **Esquemas de URL**, por ejemplo `lumatutorialswiftui`.

   ![url de garantía](assets/assurance-url-type.png)

Para obtener más información sobre los esquemas de URL en iOS, consulte [Documentación de Apple](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

Assurance funciona abriendo una dirección URL, ya sea mediante explorador o código QR. Esa URL comienza con la URL base que abre la aplicación y contiene parámetros adicionales. Estos parámetros únicos se utilizan para conectar la sesión.


## Conexión a una sesión

1. Ejecute la aplicación en el simulador o en un dispositivo físico conectado.
1. Seleccionar **[!UICONTROL Assurance]** en el carril izquierdo de la interfaz de usuario de la recopilación de datos.
1. Seleccionar **[!UICONTROL Crear sesión]**.
1. Seleccionar **[!UICONTROL Inicio]**.
1. Proporcione un **[!UICONTROL Nombre de sesión]** como `Luma Mobile App Session` y el **[!UICONTROL URL básica]**, que son los esquemas de URL introducidos en Xcode, seguidos de `://`. Por ejemplo: `lumatutorialswiftui://`.
1. Seleccione **[!UICONTROL Siguiente]**.
   ![sesión de creación de garantía](assets/assurance-create-session.png)
1. En el **[!UICONTROL Crear nueva sesión]** diálogo modal:

   Si utiliza un dispositivo físico:

   * Seleccionar **[!UICONTROL Escanear código QR]**. Utilice la cámara en el dispositivo físico para escanear el código QR y pulse el enlace para abrir la aplicación.

     ![código de control de calidad de garantía](assets/assurance-qr-code.png)

   Si utiliza un simulador:

   1. Seleccionar **[!UICONTROL Copiar vínculo]**.
   1. Copie el vínculo profundo mediante ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)  y utilice el vínculo profundo para abrir la aplicación con Safari en el simulador.
      ![Vínculo de copia de Assurance](assets/assurance-copy-link.png)

1. Cuando se carga la aplicación, aparece un cuadro de diálogo modal en el que se le solicita que introduzca el PIN que se muestra en el paso 7.

   <img src="assets/assurance-enter-pin.png" width="300">

   Introduzca el PIN y seleccione **[!UICONTROL Connect]**.


1. Si la conexión se ha realizado correctamente, verá lo siguiente:
   * Un icono de Assurance flotando en la parte superior de la aplicación.

     <img src="assets/assurance-modal.png" width="300">

   * Actualizaciones del Experience Cloud que llegan a través de la interfaz de usuario de Assurance, y muestran:

      1. Eventos de experiencia procedentes de la aplicación.
      1. Detalles de un evento seleccionado.
      1. El dispositivo y la cronología.

         ![eventos de garantía](assets/assurance-events.png)

Si tiene algún problema, consulte la [técnico](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} and [general documentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html){target="_blank"}.

>[!SUCCESS]
>
>Ahora ha configurado la aplicación para que utilice Assurance durante el resto del tutorial.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)


Siguiente: **[Consentimiento](consent.md)**
