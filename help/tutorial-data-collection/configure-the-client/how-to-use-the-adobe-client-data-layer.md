---
title: Cómo utilizar la capa de datos del cliente de Adobe
description: Cómo utilizar la capa de datos del cliente de Adobe
exl-id: b5af9e72-aa6c-4cd7-80dd-b2de762a7523
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Cómo utilizar la capa de datos del cliente de Adobe

En [¿Qué es una capa de datos?](whats-a-data-layer.md), ha aprendido que hay dos partes que se deben tener en cuenta al tratar las capas de datos: el contenedor y el contenido. La variable [Capa de datos del cliente de Adobe](https://github.com/adobe/adobe-client-data-layer) es el contenedor. No le importa cómo [estructurar los datos](../structuring-your-data.md) o qué información elige incluir en sus datos. Los datos se pueden estructurar como [XDM](../structuring-your-data.md#xdm), como se muestra en los ejemplos siguientes, o puede crear su propia estructura por completo.

Lo ideal es que el equipo de ingeniería de su empresa sea responsable de introducir los datos necesarios en la capa de datos a través del código en la página. A continuación, el equipo de marketing recupera los datos de la capa de datos, preferiblemente mediante la función Etiquetas de Adobe Experience Platform, anteriormente denominada Launch.

## Inserción de datos en la capa de datos

La capa de datos del cliente de Adobe es una matriz JavaScript. Cuando se crea la capa de datos del cliente de Adobe, esta se inicia vacía:

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

Para colocar datos en la capa de datos, llame a la función `push` en la matriz de capas de datos:

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

Puede insertar datos adicionales en la capa de datos en cualquier momento llamando a `push` de nuevo.

```js
window.adobeDataLayer.push({
  "claims": {
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
});
```

## Conocimiento de los datos insertados

Si ha implementado las dos anteriores `push` , terminaría con dos entradas en la matriz de capa de datos. La capa de datos no es útil en este estado. Normalmente, desea acceder al estado combinado de la capa de datos o, en otras palabras, a un único objeto que sea el resultado combinado de todos los datos que ha insertado en la capa de datos. Aprenda a acceder a este estado combinado más adelante en el tutorial. Por ahora, es suficiente entender que el estado calculado de la capa de datos después de nuestras dos `push` Las llamadas de serían las siguientes:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## Eliminación de datos

A veces, es necesario eliminar fragmentos de datos de la capa de datos. Esto es común en las aplicaciones de una sola página cuando el usuario navega de una vista a otra. Por ejemplo, si el usuario navega de una vista de producto a una vista de contacto, puede que sea recomendable borrar los datos de producto de la capa de datos, ya que ya no son pertinentes para la vista activa.

Puede eliminar un fragmento de datos presionando un valor de `undefined` para la clave que desee eliminar. Basándose en los ejemplos anteriores, si desea eliminar `status` desde la capa de datos, el código tendría el siguiente aspecto:

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

El estado calculado de la capa de datos ya no incluiría `status`:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## Inserción de eventos en la capa de datos

La capa de datos del cliente de Adobe no solo se utiliza para almacenar datos, sino también para comunicar qué eventos se producen en la página. De hecho, los datos suelen insertarse en la capa de datos _como resultado_ de un evento que se produce en la página. Estos eventos incluyen (1) eventos de interacción, como abrir un bot de chat o escribir un término de búsqueda en una barra de búsqueda o (2) eventos que no son de interacción, como la impresión de un anuncio o la finalización de los cálculos de rendimiento de la página web.

Para comunicar que se ha producido un evento en la página, incluya un `event` en el objeto que se inserta en la capa de datos. Por ejemplo, puede que desee comunicar que un usuario ha introducido una consulta de búsqueda en un campo de búsqueda.

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

<!--Later, you'll learn how to trigger rules within Adobe Experience Platform Tags when a particular event is pushed to the data layer.--> Also note that the `event` key is not included in the computed state. It receives special treatment by the data layer.


## Inserción de eventos y datos en la capa de datos

Notificar a los oyentes que el usuario ha introducido una consulta de búsqueda es útil, pero ¿qué sucede si desea proporcionar información adicional sobre el evento? Por ejemplo, puede que desee incluir la consulta de búsqueda del usuario. Puede proporcionar estos datos de una de las dos maneras siguientes:

1. Proporcionar datos para que **se conserva** en la capa de datos como parte del estado calculado de la capa de datos.
1. Proporcionar datos para que **no se conserva** en la capa de datos como parte del estado calculado de la capa de datos.

Si desea conservar los datos en la capa de datos, normalmente depende de si planea hacer referencia a esos datos durante el tiempo en que el usuario esté en la página. Si no es así, al retener los datos dentro de la capa de datos, se crea una capa de datos saturada.

Este es un ejemplo de cómo impulsar un evento con datos adicionales que **se conserva** en la capa de datos:

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "siteKnowledge": {
    "supportSiteSearch": {
      "term": "roller",
      "locationInPage": "topSearchBar"
    }
  }
});
```

Después de esto `push` tiene lugar, `siteKnowledge` siempre aparecerá en el estado calculado de la capa de datos hasta que se descargue la página (a menos que elimine o anule deliberadamente `siteKnowledge`).

Por el contrario, este es un ejemplo de cómo impulsar un evento con datos adicionales que **no se conserva** en la capa de datos:

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "eventInfo": {
    "siteKnowledge": {
      "supportSiteSearch": {
        "term": "roller",
        "locationInPage": "topSearchBar"
      }
    }
  }
});
```

Observe en este ejemplo que `siteKnowledge` está dentro `eventInfo`. La variable `eventInfo` recibe un tratamiento especial por parte de la capa de datos. Indica a la capa de datos que estos datos _should_ se incluya en el evento que se envía a los oyentes, pero _no debe_ se conservarán dentro de la capa de datos. Después de que se notifique el evento a los oyentes (como un administrador de etiquetas), se olvidan estos datos. La variable `siteKnowledge` La clave nunca se muestra dentro del estado calculado de la capa de datos.

Cada vez que llama a `push`, la capa de datos del cliente de Adobe notifica a los oyentes. Más tarde, aprenderá a escuchar estas notificaciones <!--from Adobe Experience Platform Tags--> y reglas de déclencheur en consecuencia.

[Siguiente: ](implement-product-page-data-layer.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre la recopilación de datos. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
