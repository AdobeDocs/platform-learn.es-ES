---
title: Información general
description: Información general
exl-id: 527d8f73-33d0-45a6-b7a4-5e46cdb7c138
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 2%

---

# Usar la recopilación de datos de Adobe Experience Platform

La recopilación de datos sobre eventos que se producen en el explorador de un usuario es un principio fundamental de una estrategia de marketing. Adobe ha proporcionado varias herramientas para ayudarle a administrar estos datos. Aunque puede familiarizarse con cada una de estas herramientas individualmente, este tutorial intenta proporcionar una visión más amplia de lo que hace cada una de ellas y cómo trabajan juntas para lograr un objetivo común.

En este tutorial, analizamos una estrategia para:

1. Estructurar y mantener los datos en Adobe Experience Platform,
1. Administración de los datos en el explorador y comunicación de que se han producido ciertos eventos, y
1. Reaccione a estos eventos enviando datos relevantes a Adobe Experience Platform.

Mientras que este tutorial utiliza la capa de datos del cliente de Adobe, el SDK web de Adobe Experience Platform y el [!DNL Tags] para una implementación más prescriptiva y perfecta, también puede combinar estas herramientas con herramientas de terceros o internas para obtener la máxima flexibilidad.

## Escenario de ejemplo

Durante este tutorial, se implementa la recopilación de datos para una página de producto sencilla en un sitio de comercio electrónico:

1. La página del producto se carga en el explorador. Aquí realiza un seguimiento de que el usuario ha visto el producto.
1. El usuario decide adquirir el producto, por lo que hace clic en un botón para agregarlo al carro de compras. Aquí, puede realizar un seguimiento de que el usuario ha abierto un nuevo carro de compras y ha agregado el producto al carro enviando eventos de experiencia a Adobe Experience Platform.
1. Finalmente, el usuario hace clic en un _Descargar la aplicación_ porque están interesados en su aplicación móvil. Rastrea que el usuario ha hecho clic en el vínculo.

¡Empecemos!

[Siguiente: ](structuring-your-data.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre la recopilación de datos. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
