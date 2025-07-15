---
title: 'Actualización de audiencias de Target y scripts de perfil: Migre la implementación de Adobe Target en su aplicación móvil a la extensión de Offer Decisioning y Target'
description: Obtenga información sobre cómo actualizar las audiencias de Adobe Target y los scripts de perfil para la compatibilidad con la extensión de Offer Decisioning y Target.
exl-id: de3ce2c7-0066-496a-a8a7-994d7ce3d92c
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Actualización de audiencias de Target y scripts de perfil para la compatibilidad con la extensión móvil Decisioning


Después de completar las actualizaciones técnicas para migrar Target a la extensión de Offer Decisioning y Target, es posible que tenga que actualizar algunas de las audiencias, los scripts de perfil y las actividades para garantizar una transición sin problemas.

>[!INFO]
>
>Si migra todos los parámetros de mbox al objeto `data.__adobe.target`, no necesitará actualizar las audiencias, los scripts de perfil y las actividades como se muestra a continuación.


Si migra parámetros de mbox al objeto `xdm`, antes de publicar los cambios en producción, debería:

* Actualizar audiencias que utilizan parámetros de mbox
* Actualización de scripts de perfil que utilizan parámetros de mbox
* Actualice cualquier oferta y actividad que utilice el reemplazo del token del parámetro de mbox (por ejemplo, `${mbox.parameter_name}`)

## Ajuste de audiencias

Si migra parámetros de mbox al objeto `xdm`, las audiencias que utilizan parámetros de mbox personalizados deben actualizarse para utilizar los nuevos nombres de parámetros XDM. Por ejemplo, un parámetro personalizado de `page_name` probablemente se asignaría a `web.webpagedetails.pageName`.

Un método para garantizar la compatibilidad con la extensión de Target y con la extensión de Offer Decisioning y Target es actualizar cualquier audiencia relevante para que se utilicen las condiciones de `OR`, como se muestra a continuación:

![Cómo ver y actualizar una audiencia de Target para la compatibilidad con Offer Decisioning y la extensión de Target](assets/target-audience-update.png){zoomable="yes"}

## Edición de scripts de perfil

Si migra parámetros de mbox al objeto `xdm`, los scripts de perfil deben actualizarse para hacer referencia a los nuevos nombres de parámetros XDM, de forma similar a las audiencias. Aparte del cambio de los nombres de los parámetros de mbox, no hay diferencia en la forma en que funcionan los scripts de perfil entre una implementación de Target y Decisioning.

Un método para garantizar la compatibilidad es usar las condiciones `OR` en el código de script de perfil.

Ejemplo de script de perfil:

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

Script de perfil actualizado para la compatibilidad con Platform Web SDK:

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

Para obtener más información y prácticas recomendadas, consulte la documentación detallada sobre [scripts de perfil](https://experienceleague.adobe.com/en/docs/target/using/audiences/visitor-profiles/profile-parameters).

## Actualizar tokens de parámetros para contenido dinámico

Si migra parámetros de mbox al objeto `xdm` y tiene ofertas, diseños de recomendaciones o actividades que utilizan [reemplazo de contenido dinámico](https://experienceleague.adobe.com/en/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer), es posible que tenga que actualizarlos en consecuencia para tener en cuenta los nuevos nombres de parámetros XDM.

Según la forma en que utilice el reemplazo de tokens para los parámetros de mbox, es posible que pueda mejorar la configuración existente para tener en cuenta los nombres de parámetros antiguos y nuevos. Sin embargo, en situaciones en las que no es posible personalizar el código JavaScript, como en las ofertas JSON, debe crear copias y realizar actualizaciones una vez completada la migración y activa en el sitio de producción.

Ejemplo de oferta JSON:

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

Ejemplo de oferta JSON con nombres de parámetros de objeto XDM:

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
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Offer Decisioning y Target. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
