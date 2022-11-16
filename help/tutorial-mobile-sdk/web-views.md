---
title: Gestión de WebViews
description: Obtenga información sobre cómo administrar la recopilación de datos con WebViews en una aplicación móvil.
kt: 6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 1%

---

# Gestión de WebViews

Obtenga información sobre cómo administrar la recopilación de datos con WebViews en una aplicación móvil.

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección:

* Comprenda por qué debe tener en cuenta consideraciones especiales para WebViews.
* Comprender el código necesario para evitar problemas de seguimiento.

## Posibles problemas de seguimiento

Si envía datos de la parte nativa de la aplicación y de WebView, cada uno genera su propio ID de Experience Cloud (ECID). Esto provoca la desconexión de las visitas y la inflación de los datos de visitas y visitantes. Puede encontrar más información sobre el ECID en la sección [Información general de ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Para resolver esta situación no deseable, es importante pasar el ECID del usuario de la parte nativa a WebView.

La extensión JavaScript del servicio de ID de Experience Cloud en WebView extrae el ECID de la dirección URL en lugar de enviar una solicitud al Adobe para obtener un nuevo ID. El servicio de ID utiliza este ECID para realizar el seguimiento del visitante.

## Implementación

En la aplicación de ejemplo de Luma, busque la variable `TermsOfService.swift` (en la variable `Intro-Login_SignUp` ) y busque el siguiente código:

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

Esta es una forma sencilla de cargar una WebView. En este caso, es un archivo local, pero los mismos conceptos se aplican a las páginas remotas.

Cambie el factor del código de la vista web como se muestra a continuación:

```swift
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
if var urlString = url?.absoluteString {
    // Adobe Experience Platform - Handle Web View
    AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
        if let error = error {
            self.simpleAlert("\(error.localizedDescription)")
            return;
        }

        if let urlVariables: String = urlVariables {
            urlString.append("?" + urlVariables)
        }

        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: URL(string: urlString)!))
        }
        print("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
    }
} else {
    self.simpleAlert("Failed to create URL for webView")
}
```

Puede obtener más información sobre la variable `Identity.getUrlVariables` en la API [Guía de referencia de la API de extensión de red perimetral ID](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network/api-reference#geturlvariables).

## Validación

Tras revisar la [instrucciones de configuración](assurance.md) y conectando el simulador o el dispositivo a Assurance, cargue WebView y busque el `Edge Identity Response URL Variables` del evento `com.adobe.griffon.mobile` proveedor.

Para cargar WebView, vaya a la pantalla principal de la aplicación de Luma, seleccione el icono &quot;cuenta&quot;, seguido de las &quot;Condiciones de uso&quot; en el pie de página.

Después de cargar WebView, seleccione el evento y revise el `urlvariables` en el campo `ACPExtensionEventData` , confirmando que los siguientes parámetros están presentes en la dirección URL: `adobe_mc`, `mcmid`y `mcorgid`.

![validación de la vista web](assets/mobile-webview-validation.png)

Un ejemplo `urvariables` se puede ver a continuación:

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>Actualmente, la vinculación de visitantes mediante estos parámetros de URL se admite en el SDK web de Platform (versiones 2.11.0 o posteriores) y `VisitorAPI.js`.


Siguiente: **[Identidad](identity.md)**

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK de Adobe Experience Platform Mobile. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)