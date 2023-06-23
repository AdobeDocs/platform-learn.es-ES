---
title: Implementación de una capa de datos en una página de producto
description: Implementación de una capa de datos en una página de producto
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Implementación de una capa de datos en una página de producto

Para este tutorial, debe implementar la capa de datos del cliente de Adobe para un sitio web de comercio electrónico típico. Si aún no lo ha hecho, lea [Cómo utilizar la capa de datos del cliente de Adobe](how-to-use-the-adobe-client-data-layer.md) primero para comprender cómo funciona la capa de datos del cliente de Adobe.

Supongamos que el usuario navega por sus productos y hace clic en un rodillo de espuma para obtener más información. El usuario aterriza en la página de detalles del producto del rodillo de espuma.

Este es el HTML de la página de detalles del producto:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      // Code will go here.
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

Como habrás notado, dentro de la `<head>` etiqueta hay un `<script>` etiqueta. Aquí es donde colocará el código JavaScript. No es necesario colocar el `<script>` etiqueta dentro de `<head>`, pero insertar los datos en la capa de datos lo antes posible ayuda a garantizar que estén disponibles rápidamente para que el experto en marketing los envíe a Adobe Experience Platform antes de que el usuario abandone la página.

Dentro de `<script>` , empezará creando la etiqueta de... `adobeDataLayer` y, a continuación, inserte la información de datos y eventos adecuada en la matriz. Los datos se ajustan al esquema XDM [que ha creado anteriormente](../configure-the-server/create-a-schema.md).

```js
window.adobeDataLayer = window.adobeDataLayer || [];
window.adobeDataLayer.push({
  "event": "pageViewed",
  "web": {
    "webPageDetails": {
      "name": "Foam Roller",
      "siteSection": "Equipment"
    },
  }
});
window.adobeDataLayer.push({
  "event": "productViewed",
  "productListItems": [
    {
      "SKU": "eqfr08",
      "currencyCode": "USD",
      "name": "Foam Roller",
      "priceTotal": 18.95
    }
  ]
});
```

En este ejemplo, ha realizado dos inserciones en la capa de datos, cada una de las cuales contiene un `event` clave. Inclusión de un `event` Esta clave no solo comunica qué evento se ha producido en la página, sino que también facilita al experto en marketing la creación de reglas adecuadas dentro de las etiquetas de Adobe Experience Platform.

La primera inserción en la capa de datos notifica a los oyentes (reglas de etiquetas) que el usuario ha visto la página. También agrega el nombre de página y la sección del sitio a la capa de datos.

La segunda inserción en la capa de datos notifica a los oyentes (reglas de etiquetas) que el usuario ha visto un producto. También agrega información del producto a la capa de datos.

## Añadir al carro de compras

Es probable que también quiera rastrear cuándo el usuario hace clic en el [!UICONTROL Añadir al carro de compras] botón.

Para ello, cree una función que se llame cuando el usuario haga clic en [!UICONTROL Añadir al carro de compras] botón.

```js
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
```

Cuando se llama a esta función, primero comprueba si ya existe un carro de compras para un usuario. Normalmente, esto se haría comprobando si existe una cookie o variable en particular. Si el carro de compras no existe, insertará un `cartOpened` en la capa de datos. Posteriormente, se inserta una `productAddedToCart` en la capa de datos. La información del producto ya existe en la capa de datos, por lo que no es necesario volver a agregarla.

Añadir un `onclick` atribuir a [!UICONTROL Añadir al carro de compras] que llama al nuevo `onAddToCartClick` función.

El resultado de la página de HTML debe ser el siguiente:

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
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

## Descargue la aplicación

Una última cosa que debe hacer es rastrear cuándo el usuario hace clic en _[!UICONTROL Descargue la aplicación]_ vínculo.

Para ello, cree una función que se llame cuando el usuario haga clic en _[!UICONTROL Descargue la aplicación]_ vínculo.

```js
window.onDownloadAppClick = function(event) {
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
```

En este caso, la información sobre el vínculo se incluye dentro de un `eventInfo` clave. Como se explica en [Cómo utilizar la capa de datos del cliente de Adobe](how-to-use-the-adobe-client-data-layer.md), esto indica a la capa de datos que comunique estos datos junto con el evento, pero que _no_ conservar los datos dentro de la capa de datos. Para un clic en un vínculo, no resulta útil añadir información sobre el vínculo en el que se hizo clic a la capa de datos porque no pertenece a la página en su conjunto y no se aplica a otros eventos que pueden producirse.

Añadir un `onclick` atribuir a [!UICONTROL Descargue la aplicación] que llama a su nuevo `onDownloadAppClick` función.

El resultado de la página de HTML debe ser el siguiente:

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
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```
