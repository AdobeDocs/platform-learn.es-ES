---
title: Administrar vistas web
description: Obtenga información sobre cómo gestionar la recopilación de datos con WebViews en una aplicación móvil.
jira: KT-6987
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Administrar vistas web

Obtenga información sobre cómo gestionar la recopilación de datos con WebViews en una aplicación móvil.

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Comprenda por qué debe tener en cuenta consideraciones especiales para WebViews en la aplicación.
* Comprenda el código necesario para evitar problemas de seguimiento.

## Posibles problemas de seguimiento

Si envía datos desde la parte nativa de la aplicación y un WebView, cada uno genera su propio ID de Experience Cloud (ECID), lo que da como resultado visitas desconectadas e infladas de datos de visitas/visitantes. Puede encontrar más información sobre el ECID en la [Información general de ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Para solucionar esta situación no deseada, es importante pasar el ECID del usuario desde la parte nativa de la aplicación a un WebView que pueda querer utilizar en la aplicación.

La extensión JavaScript del servicio de ID de Experience Cloud en WebView extrae el ECID de la URL, en lugar de enviar una solicitud al Adobe para obtener un nuevo ID. El servicio de ID utiliza este ECID para rastrear al visitante.

## Implementación

En la aplicación de ejemplo de Luma, busque **[!UICONTROL TermsOfServiceSheet]** archivo (en el **[!UICONTROL Información]** ) y busque el siguiente código en la `SwiftUIWebViewModel` clase:

```swift {highlight="6-22"}
    func loadUrl() {
        let url = Bundle.main.url(forResource: "tou", withExtension: "html")
        if var urlString = url?.absoluteString {
            // Adobe Experience Platform - Handle Web View
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
        }
    }
```

La parte más importante de este código es la `AEPEdgeIdentity.Identity.getUrlVariables` cierre (resaltado). El cierre configura las variables para que la dirección URL contenga toda la información relevante, como ECID, etc. En el ejemplo se utiliza un archivo local, pero los mismos conceptos se aplican a las páginas remotas.

Puede obtener más información sobre `Identity.getUrlVariables` API en [Guía de referencia de API de extensión de identidad para red perimetral](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Validación

Para ejecutar el código:

1. Vaya a la **[!UICONTROL Configuración]** en la aplicación
1. Pulse el botón **[!UICONTROL Ver...]** para mostrar el **[!UICONTROL Condiciones de uso]**.

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

>[!NOTE]
>
>La vinculación de visitantes mediante estos parámetros de URL se admite en el SDK web de Platform (versiones 2.11.0 o posterior) y al utilizar `VisitorAPI.js`.


>[!SUCCESS]
>
>Ahora ha configurado la aplicación para que muestre contenido basado en una URL en una vista web utilizando el mismo ECID que el ECID ya emitido por el SDK de Adobe Experience Platform Mobile.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Identidad](identity.md)**
