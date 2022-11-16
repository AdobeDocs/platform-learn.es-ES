---
title: Implementar una capa de datos en una página de producto
description: Implementar una capa de datos en una página de producto
exl-id: 0debf34a-48d4-4029-b790-7fd78865c334
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Implementar una capa de datos en una página de producto

Para este tutorial, debe implementar la capa de datos del cliente de Adobe para un sitio web de comercio electrónico típico. Si aún no lo ha hecho, lea [Cómo utilizar la capa de datos del cliente de Adobe](how-to-use-the-adobe-client-data-layer.md) primero para comprender la capa de datos del cliente de Adobe.

Supongamos que el usuario explora sus productos y hace clic en un rodillo de espuma para obtener más información. El usuario aterriza en la página de detalles del producto del rodillo de espuma.

## Crear una página de detalles de producto sencilla

1. Copie y pegue el siguiente código en un nuevo archivo HTML y guárdelo en su equipo.

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

Dentro de `<head>` etiqueta ahí hay un `<script>` etiqueta. Aquí es donde se coloca el código JavaScript. Aunque no es necesario colocar la variable `<script>` dentro de la variable `<head>` contenedor, se recomienda. Esto garantiza que los datos estén disponibles para la capa de datos lo antes posible para admitir una variedad de casos de uso.

## Añadir la capa de datos de Adobe

1. Dentro de `<script>` , añada este código que crea la variable `adobeDataLayer` y luego inserta la información de datos y eventos apropiada en la matriz. Los datos se ajustan al esquema XDM [creado anteriormente](../configure-the-server/create-a-schema.md).

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

En este ejemplo, ha realizado dos empujes a la capa de datos, cada uno de los cuales contiene un `event` clave. Inclusión de un `event` clave no solo comunica qué evento se ha producido en la página, sino que también simplifica la creación de reglas adecuadas dentro de las etiquetas.

La primera notificación push a la capa de datos notifica a los oyentes (reglas de etiquetas) de que el usuario ha visto la página. También agrega el nombre de página y la sección del sitio a la capa de datos.

La segunda notificación push a la capa de datos notifica a los oyentes (reglas de etiquetas) de que el usuario ha visto un producto. También agrega información del producto a la capa de datos.

## Agregar código para el seguimiento de adiciones al carro de compras

Para este tutorial, realiza un seguimiento de cuándo el usuario hace clic en el [!UICONTROL Agregar al carro] botón.

1. Copie y pegue este código después del código de capa de datos. Se llama a la función cuando el usuario hace clic en el botón [!UICONTROL Agregar al carro] botón.

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

Esta función comprueba inicialmente si ya existe un carro de compras para un usuario.  Si el carro de compras no existe, inserte un `cartOpened` a la capa de datos. Posteriormente, se presiona un `productAddedToCart` en la capa de datos. La información del producto ya existe en la capa de datos, por lo que no es necesario agregarla de nuevo.

## Agregar atributo para agregar al botón del carro de compras

1. Agregue un `onclick` a la variable [!UICONTROL Agregar al carro] botón que llama al nuevo `onAddToCartClick` función.

El resultado de la página HTML debe ser el siguiente:

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

## Añadir código para el seguimiento de descargas de aplicaciones

Una última cosa para rastrear es cuando el usuario hace clic en el _[!UICONTROL Descargar la aplicación]_ vínculo.

1. Para ello, copie y pegue este código debajo del código de adición al carro de compras. Esta función se llama cuando el usuario hace clic en el botón _[!UICONTROL Descargar la aplicación]_ vínculo.

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

En este caso, la información sobre el vínculo se ajusta dentro de un `eventInfo` clave. Como se explica en [Cómo utilizar la capa de datos del cliente de Adobe](how-to-use-the-adobe-client-data-layer.md), esto indica a la capa de datos que comunique estos datos junto con el evento, pero que _not_ conservan los datos dentro de la capa de datos. Para hacer clic en un vínculo, no es útil agregar información sobre el vínculo en el que se hizo clic a la capa de datos porque no pertenece a la página en su conjunto y no es aplicable a otros eventos que puedan producirse.

## Añadir atributo para descargar vínculo de aplicación

1. Agregue un `onclick` a la variable [!UICONTROL Descargar la aplicación] vínculo que llama a su `onDownloadAppClick` función.

El resultado de la página HTML debe ser el siguiente:

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

[Siguiente: ](create-a-tags-property-and-install-extensions.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre la recopilación de datos. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
