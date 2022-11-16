---
title: Creación de un elemento de datos y una regla para el seguimiento de descargas de aplicaciones
description: Creación de un elemento de datos y una regla para el seguimiento de descargas de aplicaciones
feature: Web SDK
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: cb322540-e8ef-4226-b537-a67c7ca273f5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# Creación de un elemento de datos y una regla para el seguimiento de descargas de aplicaciones

Como recordatorio, al rastrear cuando un usuario hace clic en el [!UICONTROL Descargar la aplicación] , se ha insertado en la capa de datos de la siguiente manera:

```js
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
```

Utilizó la variable `eventInfo` clave, que indica a la capa de datos que comunique estos datos junto con el evento, pero que _not_ conservan los datos dentro de la capa de datos. Para hacer clic en un vínculo, no es útil agregar información sobre el vínculo en el que se hizo clic a la capa de datos porque no es aplicable a otros eventos que puedan producirse más adelante en la página.

Para esta implementación, debe enviar un evento de experiencia a Adobe Experience Platform que contenga el resultado combinado de (1) el estado calculado de la capa de datos y (2) el contenido de `eventInfo`.

Para ello, primero debe crear un elemento de datos que combine estos dos fragmentos de información.

## Crear un elemento de datos

Para crear el elemento de datos adecuado, haga clic en [!UICONTROL Elementos de datos] en el menú de la izquierda. A continuación, haga clic en el [!UICONTROL Añadir elemento de datos] vínculo.

Para el nombre del elemento de datos, introduzca `computedStateAndEventInfo`. Para la variable [!UICONTROL Extensión] campo, seleccione [!UICONTROL Principal] si aún no está seleccionado. Para la variable [!UICONTROL Tipo de elemento de datos] campo, seleccione [!UICONTROL Objetos combinados]. Este elemento de datos permite combinar varios objetos en profundidad. El elemento de datos devuelve el resultado combinado.

Para el primer objeto que desee incluir en la combinación, introduzca `%event.fullState%`. Cuando se utiliza dentro de una regla activada por una [!UICONTROL Datos introducidos] del evento de regla, hace referencia al estado calculado de la capa de datos del cliente de Adobe en el momento en que se activó la regla.

Haga clic en [!UICONTROL Añadir otro].

Para el segundo objeto, introduzca `%event.eventInfo%`. Cuando se utiliza dentro de una regla activada por una [!UICONTROL Datos introducidos] evento de regla, que hace referencia a la variable `eventInfo` que se insertó en la capa de datos del cliente de Adobe.

![elemento de datos computedStateAndEventInfo](../../../assets/implementation-strategy/computed-state-and-event-info-data-element.png)

El elemento de datos ha finalizado. Guarde el elemento de datos haciendo clic en el [!UICONTROL Guardar] botón.

## Crear una regla

Para crear la regla para rastrear clics en la variable [!UICONTROL Descargar la aplicación] vínculo, primer clic [!UICONTROL Reglas] en el menú de la izquierda.

Haga clic en [!UICONTROL Añadir regla].

Para el nombre de regla, introduzca _Vínculo de la aplicación de descarga en el que se hizo clic_.

## Añadir un evento

Haga clic en el [!UICONTROL Agregar] botón debajo de [!UICONTROL Eventos]. Ahora se muestra en la vista de evento. Para la variable [!UICONTROL Extensión] campo, seleccione [!UICONTROL Capa de datos del cliente de Adobe]. Para la variable [!UICONTROL Tipo de evento] campo, seleccione [!UICONTROL Datos introducidos].

Porque solo desea que esta regla se active cuando `downloadAppClicked` se inserta en la capa de datos, seleccione la opción [!UICONTROL Evento específico] radio en [!UICONTROL Escuchar] y tipo _downloadAppClicked_ en el [!UICONTROL Evento o clave para registrarse]  campo de texto que se muestra.

![Descargar el evento en el que se hizo clic de la aplicación](../../../assets/implementation-strategy/download-app-clicked-event.png)

Haga clic en [!UICONTROL Mantener cambios].

## Añada una acción

Ahora que está de nuevo en la vista de reglas, haga clic en el botón [!UICONTROL Agregar] botón debajo de [!UICONTROL Acciones]. Ahora debería estar en la vista de acciones. Para la variable [!UICONTROL Extensión] campo, seleccione [!UICONTROL SDK web de Adobe Experience Platform]. Para la variable [!UICONTROL Tipo de acción] campo, seleccione [!UICONTROL Enviar evento].

En el lado derecho de la pantalla, busque la variable [!UICONTROL Tipo] y seleccione `web.webinteraction.linkClicks`.

Para la variable [!UICONTROL Datos XDM] , haga clic en el botón selector de elementos de datos y seleccione [!UICONTROL computedStateAndEventInfo]. Este es el elemento de datos que acaba de crear.

Para esta regla (a diferencia de las demás reglas que ha creado), marcará la variable [!UICONTROL El documento se descargará] casilla de verificación. Esto básicamente indica al SDK que el usuario se desplazará fuera de la página cuando haga clic en el vínculo. Esto es importante, ya que permite al SDK realizar la solicitud de forma que, incluso si el usuario sale de la página, la solicitud seguirá ejecutándose en segundo plano y llegará al servidor. Si esta casilla de verificación está desmarcada, la solicitud no se realiza de esta manera y, por lo tanto, es probable que se cancele cuando se descargue el documento actual.

Puede que te estés preguntando: &quot;Eso suena bien. ¿Por qué esta opción no está siempre activada?&quot;

Bueno, es un poco complicado, pero al utilizar esta función, el SDK utiliza un método de navegador llamado [`sendBeacon`](https://developer.mozilla.org/es-ES/docs/Web/API/Navigator/sendBeacon) para enviar la solicitud. Al enviar una solicitud mediante `sendBeacon`, el explorador no permite que el SDK (ni ninguna otra cosa) acceda a los datos devueltos por el servidor. Si el SDK utilizara esta función para cada solicitud, nunca podría recibir datos del servidor. Por este motivo, es importante comprobar la variable [!UICONTROL El documento se descargará] solo cuando se descargue el documento actual, en cuyo caso los datos de respuesta se pueden descartar de todos modos.

![Casilla de verificación Descargar documento](../../../assets/implementation-strategy/document-will-unload.png)

Para guardar la acción, haga clic en el botón [!UICONTROL Conservar cambios] botón.

## Guarde la regla

La regla debería estar completa.

![Descargar regla en la que se hizo clic en un vínculo de la aplicación](../../../assets/implementation-strategy/download-app-link-clicked-rule.png)

Guarde la regla haciendo clic en [!UICONTROL Guardar].
