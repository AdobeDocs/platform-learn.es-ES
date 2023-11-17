---
title: Configuración de una propiedad de etiqueta
description: Obtenga información sobre cómo configurar una propiedad de etiqueta en la [!UICONTROL Recopilación de datos] interfaz.
feature: Mobile SDK,Tags
exl-id: 0c4b00cc-34e3-4d08-945e-3fd2bc1b6ccf
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 11%

---

# Configuración de una propiedad de etiqueta

Obtenga información sobre cómo configurar una propiedad de etiqueta en la [!UICONTROL Recopilación de datos] interfaz.

>[!INFO]
>
> Este tutorial se reemplazará con un nuevo tutorial con una nueva aplicación móvil de ejemplo a finales de noviembre de 2023

Las etiquetas de Adobe Experience Platform son la próxima generación de funcionalidades de administración de etiquetas de Adobe. Las etiquetas ofrecen a los clientes una alternativa sencilla para implementar y administrar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente. Más información sobre [etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es) en la documentación del producto.

## Requisitos previos

Para completar la lección, debe tener permiso para crear una propiedad de etiqueta. También es útil tener una comprensión básica de las etiquetas.

>[!NOTE]
>
> El platform launch (lado del cliente) ahora es [etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Instale y configure las extensiones de etiquetas móviles de.
* Genere las instrucciones de instalación del SDK.

## Configuración inicial

1. Cree una nueva propiedad de etiqueta móvil:
   1. En el [Interfaz de recopilación de datos](https://experience.adobe.com/data-collection/){target="_blank"}, seleccione **[!UICONTROL Etiquetas]** en el panel de navegación izquierdo
   1. Seleccione **[!UICONTROL Nueva propiedad]**
      ![crear una propiedad de etiqueta](assets/mobile-tags-new-property.png).
   1. Para el **[!UICONTROL Nombre]**, introduzca `Mobile SDK Course`.
   1. Para el **[!UICONTROL Plataforma]**, seleccione **[!UICONTROL Móvil]**.
   1. Seleccione **[!UICONTROL Guardar]**.

      ![configuración de la propiedad tag](assets/mobile-tags-property-config.png)

      >[!NOTE]
      >
      > La configuración de consentimiento predeterminada para las implementaciones de SDK móvil basadas en Edge como la que está haciendo en este tutorial proviene del [!UICONTROL Extensión de consentimiento] y no el [!UICONTROL Privacidad] en la configuración de la propiedad etiqueta. Agregará y configurará la extensión de consentimiento más adelante en esta lección. Para obtener más información, consulte [la documentación](https://developer.adobe.com/client-sdks/documentation/privacy-and-gdpr/).


1. Abra la nueva propiedad
1. Crear una biblioteca:

   1. Ir a **[!UICONTROL Flujo de publicación]** en el panel de navegación izquierdo.
   1. Seleccionar **[!UICONTROL Añadir biblioteca]**.

      ![Seleccione Añadir biblioteca.](assets/mobile-tags-create-library.png)

   1. Para el **[!UICONTROL Nombre]**, introduzca `Initial Build`.
   1. Para el **[!UICONTROL Entorno]**, seleccione **[!UICONTROL Desarrollo]**.
   1. Seleccionar  **[!UICONTROL Añadir todos los recursos modificados]**.
   1. Seleccionar **[!UICONTROL Guardar y generar en desarrollo]**.

      ![Crear la biblioteca](assets/mobile-tags-save-library.png)

   1. Finalmente, configúrelo como su **[!UICONTROL Biblioteca de trabajo]**.
      ![Seleccione como la biblioteca de trabajo](assets/mobile-tags-working-library.png)
1. Seleccionar **[!UICONTROL Extensiones]**.

   Las extensiones Mobile Core y Profile deben estar preinstaladas.

1. Seleccionar **[!UICONTROL Catálogo]**.

   ![configuración inicial](assets/mobile-tags-starting.png)

1. Utilice el [!UICONTROL Buscar] para buscar e instalar las siguientes extensiones. Ninguna de estas extensiones requiere ninguna configuración:
   * Identidad
   * AEP Assurance

## Configuración de extensión

1. Instale el **Consentimiento** extensión.

   A los efectos de este tutorial, seleccione **[!UICONTROL Pendiente]**. Obtenga más información acerca de la extensión de consentimiento en [la documentación](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/).

   ![configuración de consentimiento](assets/mobile-tags-extension-consent.png)

1. Instale el **Adobe Experience Platform Edge Network** extensión.

   En el **[!UICONTROL Configuración de Edge]** , seleccione la secuencia de datos que creó en la [paso anterior](create-datastream.md).

1. Seleccionar **[!UICONTROL Guardar en biblioteca y crear]**.

   ![configuración de red perimetral](assets/mobile-tags-extension-edge.png)


## Generar instrucciones de instalación del SDK

1. Seleccionar **[!UICONTROL Entornos]**.

1. Seleccione el **[!UICONTROL Desarrollo]** icono de instalación.

   ![pantalla de inicio de entornos](assets/mobile-tags-environments.png)

1. Seleccionar **[!UICONTROL iOS]**.

1. Seleccionar **[!UICONTROL Swift]**.

   ![instrucciones de instalación](assets/mobile-tags-install-instructions.png)

1. Las instrucciones de instalación le proporcionan un buen punto de partida para la implementación.

   Puede encontrar información adicional [aquí](https://developer.adobe.com/client-sdks/documentation/getting-started/get-the-sdk/).

   * **[!UICONTROL Identificador de archivo de entorno]**: Este ID único apunta a su entorno de desarrollo. Tome nota de este valor. Producción/ensayo/desarrollo tendrán todos valores de ID diferentes.
   * **[!UICONTROL Podfile]**: los CocoaPods se utilizan para administrar las versiones y descargas del SDK. Para obtener más información, consulte la [documentación](https://cocoapods.org/).
   * **[!UICONTROL Código de inicialización]**: este bloque de código muestra cómo importar los SDK necesarios y registrar las extensiones en el inicio.

>[!NOTE]
>Las instrucciones de instalación deben considerarse un punto de partida y no una documentación definitiva. Las últimas versiones del SDK y ejemplos de código se encuentran en el [documentación](https://developer.adobe.com/client-sdks/documentation/).

## Arquitectura de etiquetas móviles

Si está familiarizado con la versión web de las etiquetas, anteriormente Launch, es importante comprender las diferencias en móvil.

En la web, se procesa una propiedad de etiqueta en JavaScript que luego (normalmente) se aloja en la nube. Se hace referencia a ese archivo JS directamente en el sitio web.

En una propiedad de etiqueta móvil, las reglas y configuraciones se representan en archivos JSON alojados en la nube. La extensión principal de Mobile descarga y lee los archivos JSON en la aplicación móvil. Las extensiones son SDK independientes que funcionan juntos. Si agrega una extensión a la propiedad de etiquetas, también debe actualizar la aplicación. Si cambia una configuración de extensión o crea una regla, esos cambios se reflejarán en la aplicación una vez que publique la biblioteca de etiquetas actualizada.

Siguiente: **[Instalación de SDK](install-sdks.md)**

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)