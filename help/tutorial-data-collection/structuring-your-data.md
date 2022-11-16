---
title: Estructurar los datos
description: Estructurar los datos
exl-id: 8d176389-25a4-4718-afff-efd2f87204ed
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Estructurar los datos

Las empresas tienen su propio idioma para comunicarse sobre su dominio. Los concesionarios de automóviles se ocupan de marcas, modelos y cilindros. Las aerolíneas se ocupan de los números de vuelo, la clase de servicio y las asignaciones de asientos. Algunos de estos términos son exclusivos de una empresa específica, algunos se comparten entre los sectores y otros son compartidos por casi todas las empresas. En el caso de los términos compartidos entre un sector vertical o incluso más amplio, puede empezar a hacer cosas poderosas con los datos cuando nombra y estructura estos términos de forma común.

Por ejemplo, muchas empresas se ocupan de pedidos. ¿Qué pasaría si, colectivamente, estas empresas decidieran modelar una orden de manera similar? Por ejemplo, ¿qué sucede si el modelo de datos consiste en un objeto con un `priceTotal` propiedad que representa el precio total del pedido? ¿Qué sucede si ese objeto también tiene propiedades denominadas? `currencyCode` y `purchaseOrderNumber`? Tal vez el objeto order contenga una propiedad denominada `payments` sería una matriz de objetos de pago. Cada objeto representaría un pago para el pedido. Por ejemplo, tal vez un cliente pagó parte del pedido con una tarjeta de regalo y pagó el resto con una tarjeta de crédito. Puede empezar a construir un modelo que tenga este aspecto:

```json
{
  "order": {
    "priceTotal": 89.50,
    "currencyCode": "EUR",
    "purchaseOrderNumber": "JWN20192388410012",
    "payments": [
      {
        "paymentType": "gift_card",
        "paymentAmount": 50
      },
      {
        "paymentType": "credit_card",
        "paymentAmount": 39.50
      }
    ]
  }
}
```

Si todas las empresas que trabajan con pedidos decidieran modelar sus datos de pedidos de una manera consistente para términos que son comunes en el sector, podrían comenzar a ocurrir cosas mágicas. La información podría intercambiarse más fluidamente dentro y fuera de su organización en lugar de interpretar y traducir constantemente los datos (props y evars, ¿alguien?). El aprendizaje automático podría comprender más fácilmente cuáles son sus datos _significa_ y proporcionar perspectivas procesables. Las interfaces de usuario para mostrar datos relevantes podrían resultar más intuitivas. Sus datos podrían integrarse perfectamente con socios y proveedores que siguen el mismo modelo.

## XDM

Este es el objetivo del Adobe [Modelo de datos de experiencia](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM proporciona modelado prescriptivo para datos que son comunes en el sector, al tiempo que le permite ampliar el modelo para sus necesidades específicas. Adobe Experience Platform se basa en XDM y, como tal, los datos enviados a Experience Platform deben estar en XDM. En lugar de pensar en dónde y cómo transformar los modelos de datos actuales en XDM antes de enviar los datos al Experience Platform, considere la posibilidad de adoptar XDM de forma más generalizada en su organización para que la traducción rara vez tenga lugar.

[Siguiente: ](configure-the-server/create-a-schema.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre la recopilación de datos. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
