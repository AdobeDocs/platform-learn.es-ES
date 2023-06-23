---
title: Creación de reglas para el seguimiento de vistas de página y eventos comerciales
description: Creación de reglas para el seguimiento de vistas de página y eventos comerciales
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 2dd02462-ddb5-4f67-8b0f-4a5bf5f7d655
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# Creación de reglas para el seguimiento de vistas de página y eventos comerciales

Para realizar un seguimiento de que el usuario ha visto la página del producto, cree una regla en las etiquetas de Adobe Experience Platform. Para ello, haga clic en [!UICONTROL Reglas] en el menú de la izquierda, haga clic en [!UICONTROL Añadir regla].

Para el nombre de la regla, escriba _Página vista_.

## Añadir un evento

Haga clic en [!UICONTROL Añadir] botón debajo de [!UICONTROL Eventos]. Ahora se muestra estar en la vista de evento. Para el [!UICONTROL Extensión] , seleccione [!UICONTROL Capa de datos del cliente de Adobe]. Para el [!UICONTROL Tipo de evento] , seleccione [!UICONTROL Datos insertados].

Porque solo desea que esta regla se active cuando el `pageViewed` evento se inserta en la capa de datos, seleccione [!UICONTROL Evento específico] bajo [!UICONTROL Escuchar a] y tipo _pageViewed_ en el [!UICONTROL Evento / Clave para la que registrarse] campo de texto.

![Evento de página vista](../../../assets/implementation-strategy/page-viewed-event.png)

Haga clic en [!UICONTROL Mantener cambios].

## Añada una acción

Ahora que ha vuelto a la vista de reglas, haga clic en [!UICONTROL Añadir] botón debajo de [!UICONTROL Acciones]. Ahora debería estar en la vista de acción. Para el [!UICONTROL Extensión] , seleccione [!UICONTROL SDK web de Adobe Experience Platform]. Para el [!UICONTROL Tipo de acción] , seleccione [!UICONTROL Enviar evento]. Esta acción le permite enviar un evento de experiencia a Adobe Experience Platform Edge Network.

En el lado derecho de la pantalla, busque el [!UICONTROL Tipo] y seleccione `web.webpagedetails.pageViews`. Este es uno de los tipos de eventos de experiencia canónicos que Adobe Experience Platform proporciona de forma predeterminada. Representa una vista de página.

Para el [!UICONTROL Datos XDM] , introduzca `%event.fullState%`. Esto indica que el estado calculado (también conocido como estado completo) de la capa de datos, que se captura en el momento en que se activó la regla, debe enviarse como parte del evento de experiencia.

![Acción de página vista](../../../assets/implementation-strategy/page-viewed-action.png)

Si los datos insertados en la capa de datos desde el sitio web no se ajustan al esquema XDM, o si solo desea enviar una parte del estado calculado de la capa de datos, utilice el [!UICONTROL Objeto XDM] Tipo de elemento de datos (proporcionado por la extensión del SDK web de Adobe Experience Platform) para generar un objeto adecuado que coincida con el esquema.

Haga clic en [!UICONTROL Conservar cambios] botón.

## Guarde la regla

La regla debe estar completa.

![Regla de página vista](../../../assets/implementation-strategy/page-viewed-rule.png)

Guarde la regla haciendo clic en [!UICONTROL Guardar].

## Repetir el proceso

Repita el proceso descrito anteriormente para crear reglas cuando se vea un producto, se abra un carro de compras y se agregue un producto al carro de compras. Las únicas diferencias entre las reglas serán el nombre de la regla y el valor introducido en el [!UICONTROL Evento / Clave para la que registrarse] en el campo [!UICONTROL Datos insertados] y el evento [!UICONTROL Tipo] en el campo [!UICONTROL Enviar evento] acción. Estos son los valores de cada regla:

Regla visualizada por el producto:

* **Nombre de regla**: _Producto visualizado_
* **Evento / Clave para la que registrarse** dentro [!UICONTROL Datos insertados] evento: `productViewed`
* **Tipo** dentro [!UICONTROL Enviar evento] acción: `commerce.productViews`

Regla de carrito abierto:

* **Nombre de regla**: _Carrito abierto_
* **Evento / Clave para la que registrarse** dentro [!UICONTROL Datos insertados] evento: `cartOpened`
* **Tipo** dentro [!UICONTROL Enviar evento] acción: `commerce.productListOpens`

Producto añadido a la regla de carro de compras:

* **Nombre de regla**: _Producto Añadido Al Carro_
* **Evento / Clave para la que registrarse** dentro [!UICONTROL Datos insertados] evento: `productAddedToCart`
* **Tipo** dentro [!UICONTROL Enviar evento] acción: `commerce.productListAdds`

A continuación, gestionaremos el seguimiento de los clics en la [!UICONTROL Descargue la aplicación] vínculo.
