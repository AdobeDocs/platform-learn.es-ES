---
title: Creación de un elemento de datos y una regla para el seguimiento de descargas de aplicaciones
description: Creación de un elemento de datos y una regla para el seguimiento de descargas de aplicaciones
feature: Web SDK
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: cb322540-e8ef-4226-b537-a67c7ca273f5
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# Creación de un elemento de datos y una regla para el seguimiento de descargas de aplicaciones

Como recordatorio, al rastrear cuándo un usuario hace clic en el [!UICONTROL Descargue la aplicación] , se insertará en la capa de datos de la siguiente manera:

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

Ha utilizado el `eventInfo` , que indica a la capa de datos que comunique estos datos junto con el evento, pero que _no_ conservar los datos dentro de la capa de datos. Para un clic en vínculo, no resulta útil añadir información sobre el vínculo en el que se hizo clic a la capa de datos porque no es aplicable a otros eventos que pueden producirse más adelante en la página.

Para esta implementación, debe enviar un evento de experiencia a Adobe Experience Platform que contenga el resultado combinado de (1) el estado calculado de la capa de datos y (2) el contenido de `eventInfo`.

Para ello, primero debe crear un elemento de datos que combine estos dos fragmentos de información.

## Crear un elemento de datos

Para crear el elemento de datos adecuado, haga clic en [!UICONTROL Elementos de datos] en el menú de la izquierda. Haga clic en el botón [!UICONTROL Añadir elemento de datos] vínculo.

Para el nombre del elemento de datos, introduzca. `computedStateAndEventInfo`. Para el [!UICONTROL Extensión] , seleccione [!UICONTROL Núcleo] si aún no está seleccionada. Para el [!UICONTROL Tipo de elemento de datos] , seleccione [!UICONTROL Objetos combinados]. Este elemento de datos le permite combinar varios objetos en profundidad. El elemento de datos devuelve el resultado combinado.

Para el primer objeto que desee incluir en la combinación, escriba `%event.fullState%`. Cuando se utiliza dentro de una regla activada por un [!UICONTROL Datos insertados] evento de regla, hace referencia al estado calculado de la capa de datos del cliente de Adobe en el momento en que se activó la regla.

Clic [!UICONTROL Añadir otro].

Para el segundo objeto, escriba `%event.eventInfo%`. Cuando se utiliza dentro de una regla activada por un [!UICONTROL Datos insertados] evento de regla, hace referencia a `eventInfo` que se insertó en la capa de datos del cliente de Adobe.

![elemento de datos computedStateAndEventInfo](../../../assets/implementation-strategy/computed-state-and-event-info-data-element.png)

El elemento de datos está completo. Guarde el elemento de datos haciendo clic en [!UICONTROL Guardar] botón.

## Crear una regla

Para crear la regla para el seguimiento de clics en la variable [!UICONTROL Descargue la aplicación] vínculo, primer clic [!UICONTROL Reglas] en el menú de la izquierda.

Haga clic en [!UICONTROL Añadir regla].

Para el nombre de la regla, escriba _Vínculo Descargar aplicación donde se hizo clic_.

## Añadir un evento

Haga clic en [!UICONTROL Añadir] botón debajo de [!UICONTROL Eventos]. Ahora se muestra estar en la vista de evento. Para el [!UICONTROL Extensión] , seleccione [!UICONTROL Capa de datos del cliente de Adobe]. Para el [!UICONTROL Tipo de evento] , seleccione [!UICONTROL Datos insertados].

Porque solo desea que esta regla se active cuando el `downloadAppClicked` evento se inserta en la capa de datos, seleccione la [!UICONTROL Evento específico] radio bajo [!UICONTROL Escuchar a] y tipo _downloadAppClicked_ en el [!UICONTROL Evento / Clave para la que registrarse]  campo de texto que se muestra.

![Descargar evento de aplicación con clic](../../../assets/implementation-strategy/download-app-clicked-event.png)

Haga clic en [!UICONTROL Mantener cambios].

## Añada una acción

Ahora que ha vuelto a la vista de reglas, haga clic en [!UICONTROL Añadir] botón debajo de [!UICONTROL Acciones]. Ahora debería estar en la vista de acción. Para el [!UICONTROL Extensión] , seleccione [!UICONTROL SDK web de Adobe Experience Platform]. Para el [!UICONTROL Tipo de acción] , seleccione [!UICONTROL Enviar evento].

En el lado derecho de la pantalla, busque el [!UICONTROL Tipo] y seleccione `web.webinteraction.linkClicks`.

Para el [!UICONTROL Datos XDM] , haga clic en el botón selector de elementos de datos y seleccione [!UICONTROL computedStateAndEventInfo]. Este es el elemento de datos que acaba de crear.

Para esta regla (a diferencia de las demás reglas que ha creado), debe comprobar las [!UICONTROL Se descargará el documento] casilla de verificación Básicamente, esto indica al SDK que el usuario se alejará de la página cuando haga clic en el vínculo. Esto es importante, ya que permite al SDK realizar la solicitud de forma que, aunque el usuario salga de la página, la solicitud seguirá ejecutándose en segundo plano y llegará al servidor. Si esta casilla de verificación no está marcada, la solicitud no se realizará de esta manera y, por lo tanto, es probable que se cancele cuando se descargue el documento actual.

Puede que te estés preguntando: &quot;Suena bien. ¿Por qué no está siempre activada esta opción?&quot;

Bueno, es un poco complicado, pero al usar esta función, el SDK usa un método de navegador llamado [`sendBeacon`](https://developer.mozilla.org/es-ES/docs/Web/API/Navigator/sendBeacon) para enviar la solicitud. Al enviar una solicitud utilizando `sendBeacon`, el explorador no permite que el SDK (ni ninguna otra cosa) acceda a los datos devueltos por el servidor. Si el SDK utilizara esta función para cada solicitud, nunca podría recibir datos del servidor. Por este motivo, es importante comprobar el [!UICONTROL Se descargará el documento] casilla de verificación solo cuando se descargue el documento actual, en cuyo caso los datos de respuesta se pueden descartar de todos modos.

![Casilla de verificación El documento descargará](../../../assets/implementation-strategy/document-will-unload.png)

Guarde la acción haciendo clic en [!UICONTROL Conservar cambios] botón.

## Guarde la regla

La regla debe estar completa.

![Descargar regla de vínculo de aplicación pulsado](../../../assets/implementation-strategy/download-app-link-clicked-rule.png)

Guarde la regla haciendo clic en [!UICONTROL Guardar].
