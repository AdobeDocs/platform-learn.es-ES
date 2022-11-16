---
title: Publicar la biblioteca
description: Publicar la biblioteca
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 2fc072df-24f2-4fea-848f-0a973deca2f8
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# Publicar la biblioteca

Ahora es el momento de implementar la biblioteca de etiquetas en el sitio web.

## Crear una biblioteca.

En primer lugar, debe crear una biblioteca que incluya las extensiones, las reglas y el elemento de datos que ha creado. Para crear una biblioteca, seleccione [!UICONTROL Flujo de publicación] en el menú de la izquierda.

Select [!UICONTROL Agregar biblioteca].

Debería ver la vista de creación de la biblioteca.

![creación de la biblioteca de etiquetas](../../../assets/implementation-strategy/tags-library-creation.png)

Asigne un nombre a la biblioteca, como _Demostración_. Select [!UICONTROL Desarrollo] en el [!UICONTROL Entorno] lista desplegable. A continuación, haga clic en [!UICONTROL Agregar todos los recursos modificados].

Ahora debería ver todas las extensiones, reglas y elementos de datos enumerados en [!UICONTROL Cambios en los recursos]. Haga clic en [!UICONTROL Guardar y crear en desarrollo].

## Agregue el código incrustado a su HTML

Ahora debe agregar una etiqueta de script al HTML de la página del producto que cargue la biblioteca de etiquetas recién creada.

Comience haciendo clic en [!UICONTROL Entornos] en el menú de la izquierda. Debería ver tres entornos diferentes en la lista.

![Entornos de etiquetas](../../../assets/implementation-strategy/tags-environments.png)

Haga clic en el icono del paquete en la [!UICONTROL Desarrollo] fila de entorno. Debería ver instrucciones para instalar el script de la biblioteca de Launch en la página.

![Instrucciones de instalación de etiquetas](../../../assets/implementation-strategy/tags-installation-instructions.png)

Copie la etiqueta de script (hay un botón de copiar en el portapapeles para mayor comodidad). Abra el HTML de página de producto e inserte la etiqueta de script antes de la etiqueta `</head>` etiqueta. El HTML final debe ser el siguiente:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
      window.onDownloadAppClick = function() {
        window.adobeDataLayer.push({
          "event": "downloadAppClicked",
          "eventInfo": {
            "web": {
              "webInteraction": {
                "URL": "https://example.com/download",
                "name": "App Download",
                "type": "download"
              }
            }
          }
        });
      };
    </script>
    <!--Swap this script tag with your own-->
    <script src="https://assets.adobedtm.com/xxxxxxxxxxxx/xxxxxxxxxxxx/launch-xxxxxxxxxxxx-development.min.js" async></script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```

Consulte la [publicación de documentación para etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html) si desea obtener más información sobre el proceso de publicación.

A continuación, probará la nueva implementación.
