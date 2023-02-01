---
title: Solución para la recuperación previa | Migración de Target de at.js 2.x al SDK web
description: Aprenda a implementar una solución alternativa para pasar parámetros con recuperación previa
source-git-commit: d061d2492d6d5e8e7a8a6e03ce63b9b6cd3793d8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Solución para la recuperación previa

Todos los clientes de Target que no estaban en producción con el SDK web de Experience Platform antes del 1 de octubre de 2022 realizan una solicitud a Target desde la red perimetral de Experience Platform mediante el modo de &quot;recuperación previa&quot;. La recuperación previa permite que el explorador precargue y almacene en caché las ofertas de Target, de modo que estén listas para aplicarse cuando el visitante alcance el estado correcto de la página. Esto es ventajoso en las aplicaciones de una sola página (SPA), ya que la experiencia de usuario deseada se puede representar lo más rápido posible, sin solicitudes de red adicionales. Sin embargo, hay implicaciones importantes tanto para las implementaciones SPA como para las no SPA.

En lugar de contar a un visitante en una actividad cuando el contenido de la oferta se entrega en la solicitud de red, los visitantes ahora se cuentan en actividades cuando `propositionDisplay` La solicitud sendEvent la realiza el SDK web. Estas solicitudes las realizan automáticamente las actividades del Compositor de experiencias visuales (VEC) cuando renderdecisions está establecido en true y cuando la experiencia se ha renderizado correctamente en la página. Con los ámbitos personalizados y cuando renderdecisions se establece en false, el implementador debe iniciar las solicitudes propositionDisplay de forma intencionada. Además, _todos los parámetros utilizados para fines que no sean la calificación inmediata de la actividad deben enviarse a través de un `propositionDisplay`  evento_.

## ¿Por qué se necesita la solución alternativa?

En muchas implementaciones de Target, a veces se realizan solicitudes de red importantes sin que se espere que se envíe una actividad. Por ejemplo, se pueden realizar solicitudes para:

* Registrar conversiones de pedidos
* Establecer parámetros de perfil
* scripts de perfil de déclencheur
* Enviar parámetros de entidad para rellenar el catálogo de Recommendations

Lamentablemente, en el modo de recuperación previa, no se comportan del modo esperado. En el modo de recuperación previa, estos datos no se incorporan a menos que formen parte de una `propositionDisplay`.

## ¿Cuál es la solución?

La solución consiste en tres partes:

1. Defina un ámbito personalizado como parte de su `sendEvent`
1. Utilice el ámbito personalizado en una actividad basada en formularios (la actividad puede servir contenido predeterminado)
1. Uso de un controlador de respuesta para realizar otra `sendEvent` para propositionDisplay e incluya los parámetros que necesita para capturar el orden, definir los parámetros de perfil, déclencheur del script de perfil, enviar los parámetros de entidad, etc.

Por ejemplo, a continuación se muestra un ejemplo de cómo se puede utilizar la solución para enviar un parámetro de perfil:


```JavaScript
var data = {
    "__adobe": {
        "target": {
            "profile.gender": "male"
        }
    }
};
// Send the initial event with the data object and custom decision scope
alloy("sendEvent", {
    "renderDecisions": true,
    data,
    decisionScopes: ['profile-param-example']
}).then(function(result) {
    var propositions = result.propositions;
    var ctaProposition;
    if (propositions) {
        // Find the discount proposition, if it exists.
        for (var i = 0; i < propositions.length; i++) {
            var proposition = propositions[i];
            if (proposition.scope === "profile-param-example") {
                ctaProposition = proposition;
                break;
            }
        }
    }
    if (ctaProposition) {
        // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered, and includes the data object again
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: [{
                            id: ctaProposition.id,
                            scope: ctaProposition.scope,
                            scopeDetails: ctaProposition.scopeDetails
                        }]
                    }
                }
            },
            data
        });
    }
});
```

Cuando el perfil se establece como parte de propositionDisplay, se guarda en el perfil del visitante y está disponible en solicitudes posteriores. Se puede utilizar el mismo método para informar de los detalles de conversión de pedidos y los parámetros de entidad.

En las etiquetas, utilice el tipo de evento Send Event Complete para almacenar en déclencheur un evento que contenga el sendEvent adicional.

## ¿Cómo sé si mi implementación utiliza el modo de recuperación previa?

Debe abrir un ticket del Servicio de atención al cliente para averiguar si su cuenta está usando el modo de recuperación previa.


>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).