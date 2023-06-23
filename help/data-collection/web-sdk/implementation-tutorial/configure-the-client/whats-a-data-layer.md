---
title: Qué es una capa de datos
description: Qué es una capa de datos
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 747f2e60-646e-4324-993c-88568415ea59
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Qué es una capa de datos

Al implementar tecnologías de marketing en el sitio, es probable que tenga datos importantes repartidos por la interfaz de usuario. Por ejemplo, el nombre de un producto puede estar en un encabezado de la página y el precio puede ser más bajo en la página debajo de la imagen del producto. Si desea enviar esos datos a Adobe o a otro proveedor, puede encontrar los elementos de HTML que contienen los datos buscando etiquetas o atributos de HTML concretos, extraer los datos de esos elementos y enviarlos. Pero, ¿qué sucede cuando su equipo de ingeniería decide mover el nombre del producto del encabezado a una barra lateral? Su implementación se interrumpe. La implementación ya no puede encontrar el encabezado o, peor aún, encuentra el encabezado y envía datos irrelevantes al servidor.

Uno de los principales objetivos de una capa de datos es resolver este problema. En su forma más sencilla, una capa de datos es un objeto JavaScript (o, como veremos más adelante, una matriz) que contiene datos sobre el producto en la página o cualquier otro dato relevante en el que se basen las tecnologías de marketing para alcanzar sus objetivos. Al no depender de los elementos de la interfaz de usuario para proporcionar estos datos, nuestra implementación se vuelve más sólida. La capa de datos contiene los datos y debe considerarse un contrato. Este contrato se suele celebrar entre el equipo de ingeniería, que coloca los datos en la capa de datos, y el equipo de marketing, que recupera los datos de la capa de datos.

Si un ingeniero está a punto de cambiar la estructura de la capa de datos, es mucho más probable que considere la posibilidad de trabajar con el equipo de marketing para que se puedan realizar los cambios adecuados en la implementación de marketing. Esta comunicación y cooperación _debe_ debe establecerse en su organización para garantizar una implementación sólida.

## Contenedor frente a contenido

En el sector, el término &quot;capa de datos&quot; se utiliza de forma poco precisa y, a menudo, puede generar confusión y falta de comunicación. Considere una caja de canicas. Hay dos partes: el contenedor (la caja) y el contenido (las canicas). Del mismo modo, se suele considerar que una capa de datos tiene dos partes: el contenedor (el objeto o matriz JavaScript) y el contenido (los fragmentos de datos como `priceTotal`, `currencyCode`, y `purchaseOrderNumber` ).

Como este tutorial hace referencia a la capa de datos del cliente de Adobe, hace referencia al contenedor y no al contenido. Cuando hace referencia a XDM, hace referencia al contenido y no al contenedor. En el caso de la capa de datos del cliente de Adobe, no importa si el contenido es XDM o su propio modelo de datos. A la capa de datos del cliente de Adobe no le importa. Es sólo una caja. Pero, es _es_ una caja con poderes especiales...

## Comunicar cambios

Al utilizar una capa de datos, puede cambiar el contenido en cualquier momento. Es una buena característica, ya que los datos pueden estar disponibles en diferentes momentos. Por ejemplo, es posible que tenga algunos datos sobre el usuario disponibles inmediatamente, pero puede que necesite realizar una solicitud asincrónica a un tercero para obtener información adicional. Esto requiere una consideración especial. Si necesita enviar estos datos asincrónicos a Adobe Experience Platform en algún momento, ¿cómo saben sus tecnologías de marketing cuándo se han agregado determinados fragmentos de datos a la capa de datos y están listos para enviarse? Necesita una capa de datos más inteligente: una capa de datos impulsada por eventos.

Una capa de datos impulsada por eventos puede comunicar que su contenido ha cambiado para que las tecnologías de marketing puedan reaccionar al cambio. Si se utiliza correctamente, esto puede ayudar a evitar problemas de temporización que a menudo surgen con las capas de datos que no tienen medios para comunicarse cuando se producen cambios.

La capa de datos del cliente de Adobe es una capa de datos impulsada por evento.
