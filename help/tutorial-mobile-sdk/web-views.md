---
title: Administrar vistas web con el SDK de Platform Mobile
description: Obtenga información sobre cómo gestionar la recopilación de datos con WebViews en una aplicación móvil.
jira: KT-14632
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Administrar vistas web

Obtenga información sobre cómo gestionar la recopilación de datos con WebViews en una aplicación móvil.

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Comprenda por qué debe tener especial consideración para WebViews en la aplicación.
* Comprenda el código necesario para evitar problemas de seguimiento.

## Posibles problemas de seguimiento

Si envía datos desde la parte nativa de la aplicación y desde un WebView dentro de la aplicación, cada uno genera su propio ID de Experience Cloud (ECID), lo que provoca que se desconecten las visitas y se inflen los datos de visitas o visitantes. Puede encontrar más información sobre el ECID en la [Información general de ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Para solucionar esta situación no deseada, es importante pasar el ECID del usuario desde la parte nativa de la aplicación a un WebView que pueda querer utilizar en la aplicación.

La extensión de identidad de Edge de AEP utilizada dentro de WebView recopila el ECID actual y lo añade a la dirección URL en lugar de enviar una solicitud al Adobe para obtener un nuevo ID. A continuación, la implementación utiliza este ECID para solicitar la dirección URL.

## Implementación

Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Info]** > **[!DNL TermsOfServiceSheet]** y busque el `func loadUrl()` función en la `final class SwiftUIWebViewModel: ObservableObject` clase. Agregue la siguiente llamada para administrar el visor web:

```swift
// Handle web view
AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
    if let error = error {
        print("Error with Webview", error)
        return;
    }
    
    if let urlVariables: String = urlVariables {
        urlString.append("?" + urlVariables)
        guard let url = URL(string: urlString) else {
            return
        }
        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: url))
        }
    }
    Logger.aepMobileSDK.info("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
}
```

El [`AEPEdgeIdentity.Identity.getUrlVariables`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) La API configura las variables para que la dirección URL contenga toda la información relevante, como ECID, etc. En el ejemplo se utiliza un archivo local, pero los mismos conceptos se aplican a las páginas remotas.

Puede obtener más información sobre `Identity.getUrlVariables` API en [Guía de referencia de API de extensión de identidad para red perimetral](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Validación 

Para ejecutar el código:

1. Revise la [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo a Assurance.
1. Vaya a la **[!UICONTROL Configuración]** en la aplicación
1. Pulse el botón **[!DNL View...]** para mostrar el **[!DNL Terms of Use]**.

   <img src="./assets/tou1.png" width="300" /> <img src="./assets/tou2.png" width="300" />

1. En la interfaz de usuario de Assurance, busque **[!UICONTROL Variables de URL de respuesta de identidad de Edge]** evento de la **[!UICONTROL com.adobe.griffon.mobile]** proveedor.
1. Seleccione el evento y revise la **[!UICONTROL urlvariable]** en el campo **[!UICONTROL ACPExtensionEventData]** , confirmando que los siguientes parámetros están presentes en la dirección URL: `adobe_mc`, `mcmid`, y `mcorgid`.

   ![validación de webview](assets/webview-validation.png)

   Una muestra `urvariables` Campo visible a continuación:

   * Original (con caracteres de escape)

     ```html
     adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg
     ```

   * Embellecido

     ```html
     adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
     ```

Lamentablemente, la depuración de la sesión web es limitada. Por ejemplo, no puede utilizar el Adobe Experience Platform Debugger del explorador para continuar depurando la sesión de vista web.

>[!NOTE]
>
>La vinculación de visitantes mediante estos parámetros de URL se admite en el SDK web de Platform (versiones 2.11.0 o posterior) y al utilizar `VisitorAPI.js`.


>[!SUCCESS]
>
>Ahora ha configurado la aplicación para que muestre contenido basado en una URL en una vista web utilizando el mismo ECID que el ECID ya emitido por el SDK de Adobe Experience Platform Mobile.
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Identidad](identity.md)**
