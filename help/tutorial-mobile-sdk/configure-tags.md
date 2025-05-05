---
title: Configuración de una propiedad de etiquetas para implementaciones del SDK de Platform Mobile
description: Obtenga información sobre cómo configurar una propiedad de etiqueta en la interfaz de [!UICONTROL Recopilación de datos].
feature: Mobile SDK,Tags
jira: KT-14626
exl-id: 0c4b00cc-34e3-4d08-945e-3fd2bc1b6ccf
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 4%

---

# Configuración de una propiedad de etiqueta

Obtenga información sobre cómo configurar una propiedad de etiqueta en la interfaz de [!UICONTROL Recopilación de datos].

Las etiquetas de Adobe Experience Platform son la próxima generación de funcionalidades de administración de etiquetas de Adobe. Las etiquetas ofrecen a los clientes una alternativa sencilla para implementar y gestionar las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente. Obtenga más información acerca de [Etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es) en la documentación del producto.

## Requisitos previos

Para completar la lección, debe tener permiso para crear una propiedad de etiqueta. También es útil tener una comprensión básica de las etiquetas.

>[!NOTE]
>
> Ahora, el platform launch (lado del cliente) es [Etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Instale y configure las extensiones de etiquetas móviles de.
* Genere las instrucciones de instalación del SDK.

## Configuración inicial

1. Cree una nueva propiedad de etiqueta móvil en la interfaz de recopilación de datos:
   1. Seleccione **[!UICONTROL Etiquetas]** en el panel de navegación izquierdo.
   1. Seleccionar **[!UICONTROL nueva propiedad]**

      ![crear una propiedad de etiqueta](assets/tags-new-property.png).
   1. Para **[!UICONTROL Name]**, escriba `Luma Mobile App Tutorial`.
   1. Para la **[!UICONTROL plataforma]**, seleccione **[!UICONTROL móvil]**.
   1. Seleccione **[!UICONTROL Guardar]**.

      ![configurar la propiedad de etiqueta](assets/tags-property-config.png)

      >[!NOTE]
      >
      > La configuración de consentimiento predeterminada para las implementaciones de sdk móvil basadas en Edge, como la que está haciendo en esta lección, proviene de la [!UICONTROL extensión de consentimiento] y no de la configuración de [!UICONTROL Privacidad] en la configuración de la propiedad de etiquetas. Puede añadir y configurar la extensión de consentimiento más adelante en esta lección. Para obtener más información, consulte [la documentación](https://developer.adobe.com/client-sdks/edge/consent-for-edge-network/).


1. Abra la nueva propiedad.
1. Crear una biblioteca:

   1. Vaya a **[!UICONTROL Flujo de publicación]** en el panel de navegación izquierdo.
   1. Seleccione **[!UICONTROL Agregar biblioteca]**.

      ![Seleccionar Agregar biblioteca](assets/tags-create-library.png)

   1. Para **[!UICONTROL Name]**, escriba `Initial Build`.
   1. Para el **[!UICONTROL Entorno]**, seleccione **[!UICONTROL Desarrollo (desarrollo)]**.
   1. Seleccione ![Botón Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Agregar todos los recursos modificados]**.
   1. Seleccione **[!UICONTROL Guardar y generar en desarrollo]**.

      ![Crear la biblioteca](assets/tags-save-library.png)

   1. Finalmente, seleccione **[!UICONTROL Versión inicial]** como su biblioteca de trabajo en el menú **[!UICONTROL Seleccionar una biblioteca de trabajo]**.

      ![Seleccionar como biblioteca de trabajo](assets/tags-working-library.png)
1. Compruebe las extensiones:

   1. Asegúrese de que **[!UICONTROL Versión inicial]** esté seleccionada como biblioteca predeterminada.

   1. Seleccione **[!UICONTROL Extensiones]** en el carril izquierdo.

   1. Seleccione la ficha **[!UICONTROL Instalado]**.

      Las extensiones [!UICONTROL Mobile Core] y [!UICONTROL Profile] deben estar preinstaladas.

      ![Etiquetas instaladas](assets/tags-installed.png)

## Configuración de extensión

1. Asegúrese de que está en **[!UICONTROL Extensiones]** dentro de la propiedad de su aplicación móvil.

1. Seleccione **[!UICONTROL Catálogo]**.

   ![configuración inicial](assets/tags-starting.png)

1. Utilice el campo ![Buscar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Buscar]** para encontrar la extensión **Identidad**.

   1. Busque `Identity`.

   2. Seleccione la extensión **[!UICONTROL Identity]**.

   3. Seleccione **[!UICONTROL Instalar]**.

      ![Instalación de identidad](assets/tags-identity-install.png)

   Esta extensión no requiere ninguna configuración adicional.

1. Utilice el campo ![Buscar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Buscar]** para buscar e instalar la extensión **AEP Assurance**.

   Esta extensión no requiere ninguna configuración adicional.

1. Utilice el campo ![Buscar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Buscar]** para buscar e instalar la extensión **Consentimiento**. En la pantalla de configuración:

   1. Seleccione **[!UICONTROL Pendiente]**. En este tutorial, puede administrar el consentimiento más detalladamente en la aplicación. Obtenga más información acerca de la extensión de consentimiento en [la documentación](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/).
   1. Seleccione **[!UICONTROL Guardar en biblioteca]**.

      ![configuración de consentimiento](assets/tags-extension-consent.png)

1. Utilice el campo ![Buscar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Buscar]** para buscar e instalar la extensión **Edge Network de Adobe Experience Platform**.

   1. En **[!UICONTROL Datastreams]**, seleccione la **[!UICONTROL secuencia de datos]** que creó en el [paso anterior](create-datastream.md) para cada uno de los entornos, por ejemplo **[!DNL Luma Mobile App]**.

   1. Si aún no se ha rellenado, especifique el **[!UICONTROL dominio Edge Network]** en la **[!UICONTROL configuración del dominio]**. El dominio Edge Network es el nombre de su organización, seguido de `data.adobedc.net`, por ejemplo `techmarketingdemos.data.adobedc.net`.

   1. En el menú **[!UICONTROL Guardar en biblioteca]**, seleccione **[!UICONTROL Guardar en biblioteca y crear]**.

      ![configuración de red perimetral](assets/tags-extension-edge.png)

La biblioteca se crea para las nuevas extensiones y configuraciones. Una compilación correcta se indica con un <span style="color:green">●</span> en el botón **[!UICONTROL Compilación inicial]**.


## Generar instrucciones de instalación del SDK

1. Seleccione **[!UICONTROL Entornos]** en el carril izquierdo.

1. Seleccione el icono de instalación de **[!UICONTROL Development]** ![Box](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg) .

   ![pantalla de inicio de entornos](assets/tags-environments.png)

1. En el cuadro de diálogo **[!UICONTROL Instrucciones de instalación móvil]**, seleccione la pestaña **[!UICONTROL iOS]**.

1. Puedes copiar ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) las instrucciones para configurar tu proyecto usando CocoaPods. Los CocoaPods se utilizan para administrar las versiones y descargas del SDK. Para obtener más información, consulte la [documentación de CocoaPods](https://cocoapods.org/). Si utiliza Android™ como plataforma de desarrollo, Gradle es la herramienta para administrar la versión, las descargas y las dependencias del SDK. Para obtener más información, consulte la [documentación de Gradle](https://gradle.org/)

   Las instrucciones de instalación le proporcionan un buen punto de partida para la implementación. Puede encontrar información adicional [aquí](https://developer.adobe.com/client-sdks/documentation/getting-started/get-the-sdk/).

   >[!INFO]
   >
   >Para el resto de este tutorial, **no** usará las instrucciones de CocoaPods, sino una configuración nativa basada en el Administrador de paquetes Swift (SPM).
   >

1. Seleccione la ficha **[!UICONTROL Swift]** debajo de **[!UICONTROL Agregar código de inicialización]**. Este bloque de código muestra cómo importar los SDK necesarios y registrar las extensiones en el inicio. Esto se explica con más detalle en [Instalar SDK](install-sdks.md).

1. Copie ![Copie](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) el **[!UICONTROL Id. de archivo de entorno]** y guárdelo en un lugar donde lo necesite más adelante. Este ID único apunta a su entorno de desarrollo de. Cada entorno (producción, ensayo y desarrollo) tiene su propio valor de ID único.

   ![instrucciones de instalación](assets/tags-install-instructions.png)

>[!NOTE]
>
>Las instrucciones de instalación deben considerarse un punto de partida y no una documentación definitiva. Las últimas versiones del SDK y ejemplos de código se encuentran en la [documentación](https://developer.adobe.com/client-sdks/home/) oficial.

## Arquitectura de etiquetas móviles

Si está familiarizado con la versión web de las etiquetas, anteriormente Launch, es importante comprender las diferencias en móvil.

* En la web, se procesa una propiedad de etiqueta en JavaScript que luego (normalmente) se aloja en la nube. Se hace referencia a ese archivo JavaScript directamente en el sitio web.

* En una propiedad de etiqueta móvil, las reglas y configuraciones se representan en archivos JSON alojados en la nube. La extensión principal de Mobile descarga y lee los archivos JSON en la aplicación móvil. Las extensiones son SDK independientes que funcionan juntos. Si agrega una extensión a la propiedad de etiquetas, también debe actualizar la aplicación. Si cambia una configuración de extensión o crea una regla, esos cambios se reflejarán en la aplicación una vez que publique la biblioteca de etiquetas actualizada. Esa flexibilidad le permite modificar la configuración (como el ID del grupo de informes de Adobe Analytics) o incluso cambiar el comportamiento de la aplicación (mediante elementos de datos y reglas, como verá en lecciones posteriores) sin tener que cambiar el código en la aplicación y volver a enviar la tienda de aplicaciones.

>[!SUCCESS]
>
>Ahora tiene una propiedad de etiqueta móvil para usar en el resto de este tutorial.
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=es)

Siguiente: **[Instalar SDK](install-sdks.md)**
