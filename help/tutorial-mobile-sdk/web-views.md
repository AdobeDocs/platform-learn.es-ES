---
title: Administrar vistas web
description: Obtenga información sobre cómo gestionar la recopilación de datos con WebViews en una aplicación móvil.
jira: KT-6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---

# Administrar vistas web

Obtenga información sobre cómo gestionar la recopilación de datos con WebViews en una aplicación móvil.

>[!INFO]
>
> Este tutorial se reemplazará con un nuevo tutorial con una nueva aplicación móvil de ejemplo a finales de noviembre de 2023

## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Comprenda por qué debe tener en cuenta consideraciones especiales para WebViews.
* Comprenda el código necesario para evitar problemas de seguimiento.

## Posibles problemas de seguimiento

Si envía datos desde la parte nativa de la aplicación y un WebView, cada uno genera su propio ID de Experience Cloud (ECID). Esto provoca que se desconecten las visitas y que se inflen los datos de visitas/visitantes. Puede encontrar más información sobre el ECID en la [Información general de ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Para resolver esta situación no deseada, es importante pasar el ECID del usuario de la parte nativa a WebView.

La extensión JavaScript del servicio de ID de Experience Cloud en WebView extrae el ECID de la URL, en lugar de enviar una solicitud al Adobe para obtener un nuevo ID. El servicio de ID utiliza este ECID para rastrear al visitante.

## Implementación

En la aplicación de ejemplo de Luma, busque `TermsOfService.swift` archivo (en el `Intro-Login_SignUp` ) y busque el siguiente código:

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

Es una forma sencilla de cargar un WebView. En este caso, se trata de un archivo local, pero los mismos conceptos se aplican a las páginas remotas.

Refactorice el código de vista web como se muestra a continuación:

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

Puede obtener más información sobre `Identity.getUrlVariables` API en [Guía de referencia de API de extensión de identidad para red perimetral](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Validación

Después de revisar la [instrucciones de configuración](assurance.md) y conectando el simulador o dispositivo a Assurance, cargue WebView y busque el `Edge Identity Response URL Variables` evento de la `com.adobe.griffon.mobile` proveedor.

Para cargar WebView, vaya a la pantalla de inicio de la aplicación Luma y seleccione el icono &quot;cuenta&quot;, seguido de &quot;Condiciones de uso&quot; en el pie de página.

Después de cargar WebView, seleccione el evento y revise la `urlvariables` en el campo `ACPExtensionEventData` , confirmando que los siguientes parámetros están presentes en la dirección URL: `adobe_mc`, `mcmid`, y `mcorgid`.

![validación de webview](assets/mobile-webview-validation.png)

Una muestra `urvariables` Campo visible a continuación:

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>La vinculación de visitantes mediante estos parámetros de URL es compatible actualmente con el SDK web de Platform (versiones 2.11.0 o posteriores) y `VisitorAPI.js`.


Siguiente: **[Identidad](identity.md)**

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)