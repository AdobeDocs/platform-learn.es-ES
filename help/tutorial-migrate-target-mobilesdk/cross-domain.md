---
title: 'Habilitar compatibilidad entre dominios: migre Target de at.js 2.x al SDK web'
description: Obtenga información sobre cómo configurar Adobe Target para aplicaciones móviles y entre dominios en escenarios de explorador web mediante el SDK web de Experience Platform.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Habilitación de perfiles de visitantes entre dominios

El SDK web de Platform admite funciones de uso compartido de ID de visitante que permiten a los clientes ofrecer experiencias personalizadas de forma más precisa en sus dominios. Esta capacidad le permite ofrecer una personalización coherente entre dominios y mejora la precisión de los informes de actividad del visitante, sin depender de cookies de terceros.

## Requisitos previos

Para utilizar el uso compartido de ID entre dominios, debe utilizar la versión 2.11.0 o posterior del SDK web de Platform. Esta capacidad también es compatible con VisitorAPI.js versión 1.7.0 o posterior.

El uso compartido de ID entre dominios funciona adjuntando un parámetro de cadena de consulta especial `adobe_mc` a la dirección URL del dominio de destino. Este parámetro se utiliza para especificar el ID de visitante en lugar de generar un nuevo ID o utilizar un ID existente.

El dominio de destino debe utilizar cualquiera de estas bibliotecas para compartir ID entre dominios a fin de procesar el parámetro `adobe_mc` y compartir el ID de visitante correctamente.

## Comparación de enfoques

Antes de implementar, determine primero si la implementación existente usa la función `visitor.appendVisitorIDsTo()`. Cualquier código personalizado que utilice esta función debe actualizarse para utilizar el nuevo comando SDK web de `appendIdentityToUrl`.

| VisitorAPI.js | SDK web de Platform |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## Usando el comando `appendIdentityToURL`

Para el uso compartido de ID entre dominios, la versión 2.11.0 del SDK web agrega compatibilidad con el comando `appendIdentityToUrl`. Cuando se utiliza, este comando genera el parámetro de cadena de consulta `adobe_mc`.

El comando acepta un objeto con una propiedad, `url`, y devuelve un objeto con la dirección URL de la propiedad.

Este comando no espera ninguna actualización de consentimiento. Si no se ha proporcionado el consentimiento, la dirección URL se devuelve sin cambios.

Si no se proporciona un ECID, se llama al extremo `/acquire` para generar un ECID.

A continuación se muestra un ejemplo de cómo puede implementar el uso compartido de ID entre dominios.

Este código agrega un detector de eventos para todos los clics en la página. Si el clic estaba en un vínculo a un dominio coincidente, en este caso adobe.com o behance.com, agrega la identidad a la dirección URL y redirige al usuario allí.

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
>Al utilizar la función de etiquetas (anteriormente Launch) para implementar el SDK web, el uso compartido de ID entre dominios se puede realizar sin código personalizado. Consulte la [documentación dedicada](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension) para obtener más detalles.

>[!NOTE]
>
>El SDK web de Platform también admite el uso compartido de ID de móvil a web en casos de uso de aplicaciones móviles nativas. Para obtener más información, consulte la documentación sobre [uso compartido de ID de móviles a web y entre dominios](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

A continuación, aprenda a [actualizar audiencias y scripts de perfil](update-audiences.md) para garantizar la compatibilidad con el SDK web de Platform.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Optimize. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
