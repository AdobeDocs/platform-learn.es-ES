---
title: Creación de reglas para el seguimiento de vistas de página y eventos de comercio
description: Creación de reglas para el seguimiento de vistas de página y eventos de comercio
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 2dd02462-ddb5-4f67-8b0f-4a5bf5f7d655
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# Creación de reglas para el seguimiento de vistas de página y eventos de comercio

Para realizar un seguimiento de que el usuario ha visto la página del producto, cree una regla dentro de las etiquetas de Adobe Experience Platform . Para ello, haga clic en [!UICONTROL Reglas] en el menú de la izquierda, haga clic en [!UICONTROL Agregar regla].

Para el nombre de regla, introduzca _Página vista_.

## Añadir un evento

Haga clic en el [!UICONTROL Agregar] botón debajo de [!UICONTROL Eventos]. Ahora se muestra en la vista de evento. Para la variable [!UICONTROL Extensión] campo, seleccione [!UICONTROL Capa de datos del cliente de Adobe]. Para la variable [!UICONTROL Tipo de evento] campo, seleccione [!UICONTROL Datos introducidos].

Porque solo desea que esta regla se active cuando `pageViewed` se inserta en la capa de datos, seleccione [!UICONTROL Evento específico] under [!UICONTROL Escuchar] y tipo _pageViewed_ en el [!UICONTROL Evento o clave para registrarse] campo de texto.

![Evento de visualización de página](../../../assets/implementation-strategy/page-viewed-event.png)

Haga clic en [!UICONTROL Mantener cambios].

## Añada una acción

Ahora que está de nuevo en la vista de reglas, haga clic en el botón [!UICONTROL Agregar] botón debajo de [!UICONTROL Acciones]. Ahora debería estar en la vista de acciones. Para la variable [!UICONTROL Extensión] campo, seleccione [!UICONTROL SDK web de Adobe Experience Platform]. Para la variable [!UICONTROL Tipo de acción] campo, seleccione [!UICONTROL Enviar evento]. Esta acción le permite enviar un evento de experiencia a Adobe Experience Platform Edge Network.

En el lado derecho de la pantalla, busque la variable [!UICONTROL Tipo] y seleccione `web.webpagedetails.pageViews`. Este es uno de los tipos canónicos de eventos de experiencias que Adobe Experience Platform proporciona de forma predeterminada. Representa una vista de página.

Para la variable [!UICONTROL Datos XDM] , introduzca `%event.fullState%`. Esto indica que el estado calculado (también conocido como estado completo) de la capa de datos, que se captura en el momento en que se activó la regla, debe enviarse como parte del evento de experiencia.

![Acción vista de página](../../../assets/implementation-strategy/page-viewed-action.png)

Si los datos introducidos en la capa de datos desde el sitio web no se ajustan al esquema XDM o si solo desea enviar una parte del estado calculado de la capa de datos, utilice la variable [!UICONTROL Objeto XDM] tipo de elemento de datos (proporcionado por la extensión web SDK de Adobe Experience Platform) para crear un objeto apropiado que coincida con su esquema.

Haga clic en el [!UICONTROL Conservar cambios] botón.

## Guarde la regla

La regla debería estar completa.

![Regla de vista de página](../../../assets/implementation-strategy/page-viewed-rule.png)

Guarde la regla haciendo clic en [!UICONTROL Guardar].

## Repita el proceso

Repita el proceso descrito anteriormente para crear reglas para cuando se vea un producto, se abra un carro de compras y se agregue un producto al carro de compras. Las únicas diferencias entre las reglas serán el nombre de la regla, el valor introducido en la variable [!UICONTROL Evento o clave para registrarse] en el campo [!UICONTROL Datos introducidos] y el [!UICONTROL Tipo] en el campo [!UICONTROL Enviar evento] acción. Estos son los valores de cada regla:

Regla visualizada del producto:

* **Nombre de la regla**: _Producto visto_
* **Evento o clave para registrarse** en [!UICONTROL Datos introducidos] evento: `productViewed`
* **Tipo** en [!UICONTROL Enviar evento] acción: `commerce.productViews`

Regla de apertura del carro de compras:

* **Nombre de la regla**: _Apertura del carro de compras_
* **Evento o clave para registrarse** en [!UICONTROL Datos introducidos] evento: `cartOpened`
* **Tipo** en [!UICONTROL Enviar evento] acción: `commerce.productListOpens`

Producto agregado a la regla del carro de compras:

* **Nombre de la regla**: _Producto agregado al carro de compras_
* **Evento o clave para registrarse** en [!UICONTROL Datos introducidos] evento: `productAddedToCart`
* **Tipo** en [!UICONTROL Enviar evento] acción: `commerce.productListAdds`

A continuación, administraremos el seguimiento de clics en la variable [!UICONTROL Descargar la aplicación] vínculo.
