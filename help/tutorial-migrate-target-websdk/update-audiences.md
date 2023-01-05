---
title: Actualización de audiencias y scripts de perfil | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre cómo actualizar las audiencias y los scripts de perfil de Adobe Target para su compatibilidad con el SDK web de Experience Platform.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Actualización de audiencias y scripts de perfil de Target para la compatibilidad con el SDK web de Platform

Después de completar las actualizaciones técnicas para migrar Target al SDK web de plataforma, es posible que tenga que actualizar algunas de sus audiencias, scripts de perfil y actividades para garantizar una transición sin problemas.

Todos los parámetros de mbox de Target deben pasarse en formato XDM con una implementación del SDK web de Platform. Antes de publicar los cambios en la producción, debe:

* Actualizar audiencias que utilicen parámetros de mbox
* Actualización de scripts de perfil que utilizan parámetros de mbox
* Actualice cualquier oferta y actividad que utilice el reemplazo del token del parámetro de mbox (por ejemplo, `${mbox.parameter_name}`)

## Ajustar audiencias

Todas las audiencias que utilicen parámetros de mbox personalizados deben actualizarse para que utilicen los nuevos nombres de parámetro XDM. Por ejemplo, un parámetro personalizado para `page_name` probablemente se asignaría a `web.webpagedetails.pageName`.

Un método para garantizar la compatibilidad con at.js y con el SDK web de plataforma es actualizar cualquier audiencia relevante para que `OR` se utilizan las condiciones siguientes:

![Cómo ver la actualización de una audiencia de Target para la compatibilidad con el SDK web de la plataforma](assets/target-audience-update.png)

## Edición de scripts de perfil

Los scripts de perfil deben actualizarse para hacer referencia a nuevos nombres de parámetros XDM, similares a las audiencias. Además del cambio de los nombres de parámetros de mbox, no hay diferencia en la forma en que funcionan los scripts de perfil entre una implementación at.js y una implementación del SDK web de Platform.

Un método para garantizar la compatibilidad es utilizar `OR` condiciones en el código de script del perfil.

Ejemplo de script de perfil:

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

Se ha actualizado el script de perfil para la compatibilidad con el SDK web de Platform:

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('page.webpagedetails.pageName') =='Product Details')){
  return true
}
```

Para obtener más información y prácticas recomendadas, consulte la documentación dedicada sobre [scripts de perfil](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html).

## Actualizar tokens de parámetro para contenido dinámico

Si tiene ofertas, diseños de recomendaciones o actividades que utilicen [reemplazo de contenido dinámico](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html), es posible que deban actualizarse en consecuencia para tener en cuenta los nuevos nombres de parámetros XDM.

Según cómo use el reemplazo de tokens para los parámetros de mbox, es posible que pueda mejorar la configuración existente para tener en cuenta tanto los nombres de parámetro antiguos como los nuevos. Sin embargo, en situaciones en las que no es posible usar código personalizado de JavaScript, como en ofertas JSON, debe crear copias y actualizar una vez completada la migración y esté activa en el sitio de producción.

Ejemplo de oferta JSON:

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

Ejemplo de oferta JSON con nombres de parámetro de SDK web de plataforma:

```JSON
{
  "pageName" : "${mbox.web.webpagedetails.pageName}",
  "layoutVariation" : "grid"
}
```

Si decide realizar ajustes después de la migración para tener en cuenta los nombres de los nuevos parámetros de mbox XDM, asegúrese de poner en pausa las actividades afectadas durante el evento de migración para evitar que los visitantes sufran errores en la visualización de la actividad.

A continuación, aprenda a [validación de la implementación de Target](validate.md).

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).