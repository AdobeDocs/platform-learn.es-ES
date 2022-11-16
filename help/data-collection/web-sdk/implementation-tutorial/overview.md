---
title: Información general
description: Información general
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 8ffa258b-6ff7-4413-aead-21b106668c65
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# Información general

La recopilación de datos sobre eventos que se producen en el explorador de un usuario es un principio fundamental de una estrategia de marketing. Adobe ha proporcionado varias herramientas para ayudarle a administrar estos datos. Aunque puede familiarizarse con cada una de estas herramientas individualmente, este tutorial intenta proporcionar una visión más amplia de lo que hace cada una de ellas y cómo trabajan juntas para lograr un objetivo común.

En este tutorial, analizaremos una estrategia para (1) estructurar y mantener los datos dentro de Adobe Experience Platform, (2) administrar los datos en el explorador y comunicar que se han producido determinados eventos, y (3) reaccionar ante dichos eventos enviando los datos relevantes a Adobe Experience Platform.

Aunque este tutorial utiliza la capa de datos del cliente de Adobe, el SDK web de Adobe Experience Platform y la función de etiquetas para una implementación más prescriptiva y sencilla, también puede combinar estas herramientas con herramientas de terceros o internas para obtener la máxima flexibilidad.

## Escenario de ejemplo

Para este tutorial, supongamos que está implementando la recopilación de datos para una página de producto sencilla en un sitio de comercio electrónico. La página del producto se carga en el explorador. Aquí, realizará un seguimiento de que el usuario ha visto el producto. El usuario decide adquirir el producto, por lo que hace clic en un botón para agregarlo al carro de compras. Aquí, realizará un seguimiento de que el usuario ha abierto un nuevo carro de compras y agregado el producto al carro enviando eventos de experiencia a Adobe Experience Platform. Finalmente, el usuario hace clic en un _Descargar la aplicación_ porque están interesados en su aplicación móvil. Realizar un seguimiento de que el usuario ha hecho clic en el vínculo.
