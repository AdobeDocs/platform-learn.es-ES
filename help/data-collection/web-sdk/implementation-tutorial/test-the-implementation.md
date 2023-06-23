---
title: Prueba de la implementación
description: Prueba de la implementación
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: e2213c23-d395-4c57-8c6c-0319cd0fb0ac
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# Prueba de la implementación

Ahora que tiene la página web configurada y la biblioteca de etiquetas de Adobe Experience Platform implementada, es hora de probar la implementación.

Abra la página del producto en el explorador. Para ello, haga clic en _Archivo_ entonces _Abrir archivo..._ en el explorador o puede alojar la página en un servidor web e introducir la URL adecuada.

Después de cargar la página, debería ver algo similar a esto:

![Página web](../../assets/implementation-strategy/webpage.png)

No es bonito, pero hará el trabajo.

## Inspect: los eventos de vista de página y vista de producto

Abra las herramientas para desarrolladores en el explorador y haga clic en el panel Red. Actualice la página.

En este punto, debería ver cuatro solicitudes:

1. product.html: su página web.
2. launch-###########-development.js: la biblioteca de Launch.
3. interactuar: el evento de vista de página que se envía al servidor.
4. interactuar: el evento de vista de producto que se envía al servidor.

No dude en inspeccionar las cargas útiles de cada solicitud. Por la primera `interact` solicitud, debería poder ver la carga útil que se envía con un `eventType` de `web.webpagedetails.pageViews`.

![Inspección de solicitud de vista de página](../../assets/implementation-strategy/webpage-page-viewed-inspection.png)

Por el segundo `interact` solicitud, debería poder ver la carga útil que se envía con un `eventType` de `commerce.productViews`.

![Inspección de solicitud de vista de producto](../../assets/implementation-strategy/webpage-product-view-inspection.png)

No dude en hurgar en el resto de los datos que se envían, incluida la información del producto.

## Inspect abre el carro de compras y añade eventos al carro de compras

Ahora haga clic en _Añadir al carro de compras_ botón.

Debería ver dos solicitudes adicionales, la primera con un `eventType` de `commerce.productListOpens` (para abrir un carro nuevo) y el segundo con una `eventType` de `commerce.productListAdds` (para agregar el producto al carro de compras).

## Inspect: evento de clic en el vínculo descargar aplicación

Según el explorador, si hace clic en un vínculo que lo aleja de la página actual, es posible que se borre el panel de red. Puesto que desea inspeccionar la solicitud de red para el evento de clic en vínculo que se produce justo antes de salir de la página, deberá configurar el explorador para conservar los registros de red en todas las páginas. Esto se hace marcando una _Conservar registro_ en el panel de red (Chrome, Safari, Edge) o haciendo clic en un icono de engranaje y marcando una _Conservar registros_ elemento del menú mostrado (Firefox).

Ahora haga clic en _Descargue la aplicación_ vínculo.

Deberías ver uno más `interact` solicitud para aparecer en el panel red. Si inspecciona la solicitud, debe encontrar un `eventType` de `web.webinteraction.linkClicks` así como detalles acerca del vínculo en el que se hizo clic.

## Compruebe que los datos llegan al conjunto de datos de Adobe Experience Platform

Ahora que se envían las solicitudes de, también deberá comprobar si los datos llegan correctamente al conjunto de datos de Adobe Experience Platform que ha creado. Para empezar, vaya a [!UICONTROL Conjuntos de datos] vista dentro de Adobe Experience Platform.

Seleccione el conjunto de datos que creó anteriormente.

Es posible que tenga que esperar unos minutos, pero pronto debería ver indicaciones de datos que se están procesando e insertando en el conjunto de datos. También debe ver si el procesamiento se ha realizado correctamente o no. Si falló, usted podrá ver por qué falló. Los errores suelen producirse porque los datos que envía no coinciden con el esquema y debe ajustar los datos o el esquema en consecuencia.

![Ingesta de conjuntos de datos](../../assets/implementation-strategy/dataset-ingestion.png)

## Uso de la extensión de Adobe Experience Platform Debugger

Para obtener una buena perspectiva del comportamiento de la implementación tanto en el explorador como en los servidores de Adobe, consulte la extensión del explorador de Adobe Experience Platform Debugger.

[Extensión de Adobe Experience Platform Debugger para Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Extensión de Adobe Experience Platform Debugger para Firefox](https://addons.mozilla.org/es/firefox/addon/adobe-experience-platform-dbg/)
