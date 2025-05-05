---
title: 'Actualización de audiencias y scripts de perfil: Migre Target de at.js 2.x al SDK web'
description: Obtenga información sobre cómo actualizar las audiencias de Adobe Target y los scripts de perfil para la compatibilidad con el SDK web de Experience Platform.
exl-id: 2c0f85f7-6e8c-4d0b-8ed5-53897d06e563
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Actualización de audiencias de Target y scripts de perfil para la compatibilidad con el SDK web de Platform

Después de completar las actualizaciones técnicas para migrar Target al SDK web de Platform, es posible que tenga que actualizar algunas de las audiencias, los scripts de perfil y las actividades para garantizar una transición sin problemas.

Todos los parámetros de mbox de Target deben pasarse en formato XDM con una implementación de SDK web de Platform. Antes de publicar los cambios en producción, debe:

* Actualizar audiencias que utilizan parámetros de mbox
* Actualización de scripts de perfil que utilizan parámetros de mbox
* Actualice cualquier oferta y actividad que utilice el reemplazo del token del parámetro de mbox (por ejemplo, `${mbox.parameter_name}`)

## Ajuste de audiencias

Todas las audiencias que utilicen parámetros de mbox personalizados deben actualizarse para que utilicen los nuevos nombres de parámetros XDM. Por ejemplo, un parámetro personalizado de `page_name` probablemente se asignaría a `web.webpagedetails.pageName`.

Un método para garantizar la compatibilidad con at.js y el SDK web de Platform es actualizar cualquier audiencia relevante para que se utilicen las condiciones de `OR`, como se muestra a continuación:

![Cómo ver y actualizar una audiencia de Target para comprobar la compatibilidad con el SDK web de Platform](assets/target-audience-update.png){zoomable="yes"}

## Edición de scripts de perfil

Los scripts de perfil deben actualizarse para hacer referencia a nuevos nombres de parámetros XDM, de forma similar a las audiencias. Aparte del cambio de los nombres de los parámetros de mbox, no hay diferencia en la forma en que funcionan los scripts de perfil entre una implementación de at.js y una implementación de SDK web de Platform.

Un método para garantizar la compatibilidad es usar las condiciones `OR` en el código de script de perfil.

Ejemplo de script de perfil:

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

Script de perfil actualizado para la compatibilidad con el SDK web de Platform:

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

Para obtener más información y prácticas recomendadas, consulte la documentación detallada sobre [scripts de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=es).

## Actualizar tokens de parámetros para contenido dinámico

Si tiene ofertas, diseños de recomendaciones o actividades que utilizan [reemplazo de contenido dinámico](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html?lang=es), es posible que se deban actualizar en consecuencia para tener en cuenta los nuevos nombres de parámetros XDM.

Según la forma en que utilice el reemplazo de tokens para los parámetros de mbox, es posible que pueda mejorar la configuración existente para tener en cuenta los nombres de parámetros antiguos y nuevos. Sin embargo, en situaciones en las que no es posible personalizar el código JavaScript, como en las ofertas JSON, debe crear copias y realizar actualizaciones una vez completada la migración y activa en el sitio de producción.

Ejemplo de oferta JSON:

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

Ejemplo de oferta JSON con nombres de parámetros del SDK web de Platform:

```JSON
{
  "pageName" : "${mbox.web.webPagedDetails.pageName}",
  "layoutVariation" : "grid"
}
```

Si decide realizar ajustes después de la migración para tener en cuenta los nuevos nombres de parámetros de mbox XDM, asegúrese de pausar las actividades afectadas durante el evento de migración para evitar que los visitantes vean errores de visualización de la actividad.

A continuación, aprenda a [validar la implementación de Target](validate.md).

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target de at.js al SDK web. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=es#M463).
