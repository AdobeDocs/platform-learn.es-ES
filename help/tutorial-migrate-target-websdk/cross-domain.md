---
title: Habilitar compatibilidad con dominios cruzados | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre cómo configurar Adobe Target para escenarios de aplicaciones móviles y de dominios cruzados en exploradores web mediante el SDK web de Experience Platform.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---

# Habilitar perfiles de visitante entre dominios

El SDK web de Platform admite las funciones de uso compartido de ID de visitante que permiten a los clientes ofrecer experiencias personalizadas de forma más precisa en todos los dominios. Esta capacidad le permite ofrecer una personalización uniforme en todos los dominios y mejora la precisión de los informes de actividad de los visitantes, sin depender de cookies de terceros.

## Requisitos previos

Para utilizar el uso compartido de ID entre dominios, debe utilizar la versión 2.11.0 o posterior del SDK web de Platform. Esta funcionalidad también es compatible con VisitorAPI.js versión 1.7.0 o posterior.

El uso compartido de ID entre dominios funciona añadiendo un `adobe_mc` parámetro de cadena de consulta a la dirección URL del dominio de destino. Este parámetro se utiliza para especificar el ID de visitante en lugar de generar un nuevo ID o usar un ID existente.

El dominio de destino debe utilizar cualquiera de estas bibliotecas para el uso compartido de ID entre dominios a fin de procesar la variable `adobe_mc` y comparta correctamente el ID de visitante.

## Comparación de enfoques

Antes de la implementación, determine si la implementación existente utiliza la variable `visitor.appendVisitorIDsTo()` función. Cualquier código personalizado que utilice esta función debe actualizarse para usar la nueva `appendIdentityToUrl` SDK web.

| VisitorAPI.js | SDK web de Platform |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## Al usar la variable `appendIdentityToURL` command

Para el uso compartido de ID entre dominios, la versión 2.11.0 del SDK web agrega compatibilidad con el `appendIdentityToUrl` comando. Cuando se utiliza, este comando genera la variable `adobe_mc` parámetro de cadena de consulta.

El comando acepta un objeto con una propiedad, `url`y devuelve un objeto con la dirección url de la propiedad.

Este comando no espera ninguna actualización de consentimiento. Si no se ha dado el consentimiento, la dirección URL se devuelve sin cambios.

Si no se proporciona un ECID, la variable `/acquire` se llama al extremo para generar un ECID.

A continuación se muestra un ejemplo de cómo puede implementar el uso compartido de ID entre dominios.

Este código agrega un detector de eventos para todos los clics en la página. Si el clic estaba en un vínculo a un dominio coincidente, en este caso adobe.com o behance.com, agrega la identidad a la dirección URL y redirige al usuario a esa dirección.

```Javascript
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

>[!TIP]
>
>Al utilizar la función de etiquetas (anteriormente Launch) para implementar el SDK web, el uso compartido de ID entre dominios se puede realizar sin código personalizado. Consulte la [documentación dedicada](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension) para obtener más información.

>[!NOTE]
>
>El SDK web de Platform también admite el uso compartido de ID de de móvil a web para casos de uso nativos de aplicaciones móviles. Para obtener más información, consulte la documentación dedicada sobre [uso compartido de ID entre dominios y móviles en la web](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

A continuación, aprenda a [actualizar audiencias y scripts de perfil](update-audiences.md) para garantizar la compatibilidad con el SDK web de Platform.

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).