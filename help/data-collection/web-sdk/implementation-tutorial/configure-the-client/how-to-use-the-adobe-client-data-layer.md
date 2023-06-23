---
title: Cómo utilizar la capa de datos del cliente de Adobe
description: Cómo utilizar la capa de datos del cliente de Adobe
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 33a5db8c-e49b-4073-b4d7-4abe19537fcb
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Cómo utilizar la capa de datos del cliente de Adobe

Entrada [Qué es una capa de datos](whats-a-data-layer.md)Sin embargo, ha aprendido que hay dos partes a tener en cuenta al hablar de las capas de datos: el contenedor y el contenido. La capa de datos del cliente de Adobe es el contenedor. No me importa cómo... [estructurar los datos](../structuring-your-data.md) o qué fragmentos de información elige incluir en los datos. Los datos se pueden estructurar como [XDM](../structuring-your-data.md#xdm), como se muestra en los ejemplos siguientes, o puede crear su propia estructura por completo.

Lo ideal es que el equipo de ingeniería de su empresa sea responsable de insertar los datos necesarios en la capa de datos mediante código en la página. A continuación, el equipo de marketing recupera los datos de la capa de datos, preferiblemente mediante etiquetas de Adobe Experience Platform.

## Inserción de datos en la capa de datos

La capa de datos del cliente de Adobe es una matriz de JavaScript. Al crear la capa de datos del cliente de Adobe, comienza vacía:

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

Para colocar datos en la capa de datos, llame al método `push` en la matriz de capas de datos:

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

Puede insertar datos adicionales en la capa de datos en cualquier momento llamando a `push` otra vez.

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

## Definición de los datos insertados

Si ha implementado los dos `push` llamadas, tendría dos entradas en la matriz de capas de datos. La capa de datos no es especialmente útil en este estado. Normalmente, desea acceder al estado combinado de la capa de datos o, en otras palabras, a un solo objeto que sea el resultado combinado de todos los datos insertados en la capa de datos. Más adelante en el tutorial, aprenderemos a acceder a este estado combinado. Por ahora, es suficiente entender que el estado calculado de la capa de datos después de nuestras dos `push` las llamadas serían las siguientes:

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

En ocasiones, es necesario eliminar fragmentos de datos de la capa de datos. Esto es particularmente común en las aplicaciones de una sola página cuando el usuario navega de una vista a la siguiente. Por ejemplo, si el usuario navega de una vista de producto a una vista de contacto, puede tener sentido borrar cualquier dato de producto de la capa de datos, ya que ya no es pertinente para la vista activa.

Puede quitar un fragmento de datos insertando un valor de `undefined` para la clave que desea eliminar. Basándose en los ejemplos anteriores, si desea eliminar `status` desde la capa de datos, el código tendría el siguiente aspecto:

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

La capa de datos del cliente de Adobe no solo se utiliza para almacenar datos, sino también para comunicar qué eventos se producen en la página. De hecho, normalmente los datos se insertan en la capa de datos _como resultado_ de un evento que se produce en la página. Estos eventos incluyen (1) eventos de interacción, como abrir un bot de chat o escribir un término de búsqueda en una barra de búsqueda, o (2) eventos que no son de interacción, como la impresión de un anuncio o la finalización de cálculos de rendimiento de páginas web.

Para comunicar que se ha producido un evento en la página, incluya un `event` en el objeto que se inserta en la capa de datos. Por ejemplo, es posible que desee comunicar que un usuario ha introducido una consulta de búsqueda en un campo de búsqueda.

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

Más adelante, aprenderá a almacenar en déclencheur las reglas dentro de las etiquetas de Adobe Experience Platform cuando un evento en particular se inserte en la capa de datos. Tenga en cuenta también que la variable `event` la clave es _no_ incluido en el estado calculado. Recibe un tratamiento especial por parte de la capa de datos.

## Inserción de eventos y datos en la capa de datos

Notificar a los oyentes que el usuario ha introducido una consulta de búsqueda es útil, pero ¿qué sucede si desea proporcionar información adicional sobre el evento? Por ejemplo, quizás desee incluir la consulta de búsqueda del usuario. Puede proporcionar estos datos de una de las dos maneras siguientes:

1. Proporcionar datos para que **se conserva** en la capa de datos como parte del estado calculado de la capa de datos.
2. Proporcionar datos para que **no se conserva** en la capa de datos como parte del estado calculado de la capa de datos.

Normalmente, el hecho de que desee conservar los datos en la capa de datos depende de si tiene pensado hacer referencia a esos datos durante el tiempo que el usuario permanezca en la página. Si no es así, retener los datos dentro de la capa de datos puede provocar que se desorden la capa de datos.

Este es un ejemplo de inserción de un evento con datos adicionales que **se conserva** en la capa de datos:

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

Después de esto `push` tiene lugar, `siteKnowledge` se mostrará siempre en el estado calculado de la capa de datos hasta que se descargue la página (a menos que elimine o anule a propósito) `siteKnowledge`).

Por el contrario, aquí tiene un ejemplo de cómo insertar un evento con datos adicionales que **no se conserva** en la capa de datos:

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

Observe en este ejemplo que `siteKnowledge` está envuelto dentro `eventInfo`. El `eventInfo` recibe un tratamiento especial por parte de la capa de datos. Indica a la capa de datos que estos datos _debería_ se incluya con el evento que se envía a los oyentes, pero _no debe_ se conservarán dentro de la capa de datos. Una vez que se notifica el evento a los oyentes (como las etiquetas de Adobe Experience Platform), estos datos se olvidan del todo. El `siteKnowledge` La clave nunca aparecerá dentro del estado calculado de la capa de datos.

Cada vez que llama a `push`, la capa de datos del cliente de Adobe notifica a los oyentes. Más adelante, aprenderemos a escuchar estas notificaciones desde las etiquetas de Adobe Experience Platform y, en consecuencia, las reglas de déclencheur.
