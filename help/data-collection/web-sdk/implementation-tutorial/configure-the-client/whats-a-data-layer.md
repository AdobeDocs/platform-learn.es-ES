---
title: ¿Qué es una capa de datos?
description: ¿Qué es una capa de datos?
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 747f2e60-646e-4324-993c-88568415ea59
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# ¿Qué es una capa de datos?

Al implementar tecnologías de marketing en el sitio, es probable que tenga fragmentos importantes de datos dispersos por toda la interfaz de usuario. Por ejemplo, el nombre de un producto puede estar en un encabezado de la página y el precio puede ser inferior en la página debajo de la imagen del producto. Si desea enviar esos datos a Adobe o a otro proveedor, ciertamente puede encontrar los elementos de HTML que contienen los datos buscando etiquetas o atributos de HTML concretos, extrayendo los datos de esos elementos y enviándolos. Pero, ¿qué sucede cuando el equipo de ingeniería decide mover el nombre del producto del encabezado a una barra lateral? Su implementación se rompe. Su implementación ya no puede encontrar el encabezado o, peor aún, encuentra el encabezado y envía datos irrelevantes al servidor.

Un objetivo importante de una capa de datos es resolver este problema. En su momento más sencillo, una capa de datos es un objeto JavaScript (o, como veremos más adelante, una matriz) que contiene datos sobre el producto en la página o cualquier otro dato relevante del que dependan sus tecnologías de marketing para alcanzar sus metas. Al no depender de los elementos de la interfaz de usuario para proporcionar estos datos, nuestra implementación se vuelve más sólida. La capa de datos contiene los datos y debe considerarse como un contrato. Este contrato suele ser entre el equipo de ingeniería, que coloca los datos en la capa de datos, y el equipo de marketing, que recupera los datos de la capa de datos.

Si un ingeniero está a punto de cambiar la estructura de la capa de datos, es mucho más probable que considere la posibilidad de trabajar con el equipo de marketing para poder realizar los cambios correspondientes en la implementación de marketing. Comunicación y cooperación _must_ esté establecido en su organización para garantizar una implementación sólida.

## Contenedor vs. contenido

En el sector, el término &quot;capa de datos&quot; se introduce de manera ligeramente flexible y a menudo puede conducir a confusión y a una mala comunicación. Consideremos una caja de canicas. Hay dos partes: el contenedor (el cuadro) y el contenido (los márgenes). Del mismo modo, se suele considerar que una capa de datos tiene dos partes: el contenedor (el objeto o matriz JavaScript) y el contenido (los fragmentos de datos como `priceTotal`, `currencyCode`y `purchaseOrderNumber` ).

Como este tutorial hace referencia a la capa de datos del cliente de Adobe, hace referencia al contenedor y no al contenido. Cuando hace referencia a XDM, hace referencia al contenido y no al contenedor. En el caso de la capa de datos del cliente de Adobe, no importa si el contenido es XDM o su propio modelo de datos. A la capa de datos del cliente de Adobe no le importa. Es sólo una caja. Pero, _es_ una caja con poderes especiales...

## Comunicar cambios

Al utilizar una capa de datos, puede cambiar el contenido en cualquier momento. Esa es una buena característica, ya que los datos pueden estar disponibles en diferentes momentos. Por ejemplo, es posible que tenga algunos datos sobre el usuario disponibles inmediatamente, pero es posible que tenga que realizar una solicitud asincrónica a un tercero para obtener información adicional. Esto requiere una consideración especial. Si necesita enviar estos datos asincrónicos a Adobe Experience Platform en algún momento, ¿cómo saben sus tecnologías de marketing cuándo se han agregado ciertos datos a la capa de datos y están listos para enviarse? Necesita una capa de datos más inteligente, una capa de datos basada en eventos.

Una capa de datos impulsada por eventos puede notificar que su contenido ha cambiado para que las tecnologías de marketing puedan reaccionar ante el cambio. Si se utiliza correctamente, esto puede ayudar a evitar problemas de temporización que a menudo surgen con capas de datos que no tienen forma de comunicarse cuando se producen cambios.

La capa de datos del cliente de Adobe es una capa de datos impulsada por eventos.
