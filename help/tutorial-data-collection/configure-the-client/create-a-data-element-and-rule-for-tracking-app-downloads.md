---
title: Creación de un elemento de datos y una regla para el seguimiento de descargas de aplicaciones
description: Creación de un elemento de datos y una regla para el seguimiento de descargas de aplicaciones
feature: Web SDK
exl-id: 8012ba48-38ac-4fb5-9876-8f57d1c5da5d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 5%

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

Para esta implementación, envíe un evento de experiencia a Adobe Experience Platform que contenga el resultado combinado de (1) el estado calculado de la capa de datos y (2) el contenido de `eventInfo`.

Para ello, debe crear un elemento de datos que combine estos dos fragmentos de información.

## Crear un elemento de datos

Para crear el elemento de datos adecuado:

1. Haga clic en [!UICONTROL Elementos de datos] en el menú de la izquierda.
1. A continuación, haga clic en el [!UICONTROL Crear nuevo elemento de datos] vínculo.
1. Indique el nombre del elemento de datos, `computedStateAndEventInfo`.
1. Para la variable [!UICONTROL Extensión] campo, seleccione [!UICONTROL Principal] si aún no está seleccionado.
1. Para la variable [!UICONTROL Tipo de elemento de datos] campo, seleccione **[!UICONTROL Objetos combinados]**. Este elemento de datos permite combinar varios objetos. El elemento de datos devuelve el resultado combinado.
1. Agregue el primer objeto que desee incluir en la combinación. Entrar `%event.fullState%` en el [!UICONTROL Objeto (obligatorio)] campo . Cuando se utiliza dentro de una regla activada por una [!UICONTROL Datos introducidos] del evento de regla, hace referencia al estado calculado de la capa de datos del cliente de Adobe en el momento en que se activó la regla.
1. Haga clic en el  **[!UICONTROL Añadir otro]** comando.
1. Añada el segundo objeto. Entrar `%event.eventInfo%` en el [!UICONTROL Objeto (obligatorio)] campo . Cuando se utiliza dentro de una regla activada por una [!UICONTROL Datos introducidos] evento de regla, que hace referencia a la variable `eventInfo` que se insertó en la capa de datos del cliente de Adobe.
1. Guarde el elemento de datos haciendo clic en el [!UICONTROL Guardar] botón.
   ![elemento de datos computedStateAndEventInfo](../assets/computed-state-and-event-info-data-element.png)

El elemento de datos ha finalizado.

## Crear una regla

Para crear la regla para rastrear clics en la variable [!UICONTROL Descargar la aplicación] vínculo:

1. Haga clic en **[!UICONTROL Reglas]** en el menú de la izquierda.
1. Haga clic en **[!UICONTROL Añadir regla]**.
1. Entrar **_Vínculo de la aplicación de descarga en el que se hizo clic_** en el [!UICONTROL Nombre] campo .

## Añadir un evento

1. Haga clic en el **[!UICONTROL Agregar]** botón debajo de [!UICONTROL Eventos]. Ahora se muestra en la vista de evento.
1. Para la variable [!UICONTROL Extensión] campo, seleccione **[!UICONTROL Capa de datos del cliente de Adobe]**.
1. Para la variable [!UICONTROL Tipo de evento] campo, seleccione **[!UICONTROL Datos introducidos]**.
1. Haga clic en **[!UICONTROL Mantener cambios]**.
   ![Descargar el evento en el que se hizo clic de la aplicación](../assets/download-app-clicked-event.png)
Porque solo desea que esta regla se active cuando `downloadAppClicked` se inserta en la capa de datos, seleccione la opción **[!UICONTROL Evento específico]** radio en [!UICONTROL Escuchar] y tipo **_downloadAppClicked_** en el [!UICONTROL Evento o clave para registrarse]  campo de texto que se muestra.

## Añada una acción

Ahora que ha vuelto a la vista de reglas:

1. Haga clic en el botón **[!UICONTROL Añadir]** en [!UICONTROL Acciones].
1. Ahora debería estar en la vista de acciones. Para la variable [!UICONTROL Extensión] campo, seleccione **[!UICONTROL SDK web de Adobe Experience Platform]**. Para la variable [!UICONTROL Tipo de acción] campo, seleccione **[!UICONTROL Enviar evento]**.
1. En el [!UICONTROL Tipo] a la derecha, seleccione `web.webinteraction.linkClicks`.
1. Para la variable [!UICONTROL Datos XDM] , haga clic en el botón selector de elementos de datos a la derecha y seleccione **[!UICONTROL computedStateAndEventInfo]**. Este es el elemento de datos que ha creado recientemente.
1. Para esta regla (a diferencia de las demás reglas que ha creado), marque la casilla **[!UICONTROL El documento se descargará]** casilla de verificación.
   ![Casilla de verificación Descargar documento](../assets/document-will-unload.png)
1. Para guardar la acción, haga clic en el botón **[!UICONTROL Conservar cambios]** botón.

>[!TIP]
>
>La variable [!UICONTROL La función de descarga del documento] indica al SDK que el usuario sale de la página cuando hace clic en el vínculo. Esto es importante, ya que permite al SDK realizar la solicitud incluso si el usuario sale de la página, ya que la solicitud se sigue ejecutando en segundo plano y llega al servidor. Si esta casilla de verificación está desactivada, la solicitud no se realiza de esta manera y, por lo tanto, es probable que se cancele cuando se descargue el documento actual.
>
>Puede que te estés preguntando: &quot;Eso suena bien. ¿Por qué esta opción no está siempre activada?&quot;
>
>Bueno, es un poco complicado, pero al utilizar esta función, el SDK utiliza un método de navegador llamado [`sendBeacon`](https://developer.mozilla.org/es-ES/docs/Web/API/Navigator/sendBeacon) para enviar la solicitud. Al enviar una solicitud mediante `sendBeacon`, el explorador no permite que el SDK (ni ninguna otra cosa) acceda a los datos devueltos por el servidor. Si el SDK utilizara esta función para cada solicitud, nunca podría recibir datos del servidor. Por este motivo, es importante comprobar la variable [!UICONTROL El documento se descargará] solo cuando se descargue el documento actual, en cuyo caso los datos de respuesta se pueden descartar de todos modos.

## Guarde la regla

La regla debería estar completa.

1. Haga clic en **[!UICONTROL Guardar]** en la esquina superior derecha.
   ![Descargar regla en la que se hizo clic en un vínculo de la aplicación](../assets/download-app-link-clicked-rule.png)

[Siguiente: ](publish-the-library.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre la recopilación de datos. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)