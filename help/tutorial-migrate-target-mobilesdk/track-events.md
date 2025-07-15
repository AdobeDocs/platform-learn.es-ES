---
title: 'Seguimiento de eventos de conversión: Migre la implementación de Adobe Target en su aplicación móvil a la extensión de Offer Decisioning y Target'
description: Obtenga información sobre cómo rastrear eventos de conversión de Adobe Target mediante la extensión móvil de Offer Decisioning y Target
exl-id: 7b53aab1-0922-4d9f-8bf0-f5cf98ac04c4
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Seguimiento de eventos de conversión de Target con la extensión móvil Decisioning

El objetivo de la mayoría de las actividades de Target es impulsar acciones valiosas del usuario en la aplicación, como compras, registros, clics y mucho más. Las implementaciones de Target suelen utilizar eventos de conversión personalizados para realizar un seguimiento de estas acciones, que a menudo contienen detalles adicionales sobre la conversión. Los eventos de conversión para Target se pueden rastrear con Optimizar SDK de forma similar a Target SDK. Es necesario llamar a las API específicas para rastrear los eventos de conversión, como se muestra en la tabla siguiente:

| Objetivo de actividad | Extensión de Target | Extensión de Offer Decisioning y Target |
|---|---|---|
| Seguimiento de un evento de conversión de vistas para una ubicación (ámbito) de mbox | Llamar a la API [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} cuando se visualiza la ubicación de mbox | Llame a la API [displayed](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} cuando se visualice la oferta para la ubicación mbox. Esto envía un evento con el tipo de evento decisioning.propositionDisplay a la red de Experience Edge. **Esto es esencial para aumentar los visitantes en sus actividades de Target y debe hacerse al enviar ofertas de Target normales y predeterminadas.** |
| Seguimiento de un evento de conversión de clics para una ubicación (ámbito) de mbox | Llamar a la API [clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} en cuando se hace clic en la ubicación de mbox | Llame a la API [tapped](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} cuando se haga clic en la oferta para la ubicación mbox. Esto envía un evento con el tipo de evento decisioning.propositionInteract a la red de Experience Edge. |
| Realice un seguimiento de un evento de conversión personalizado que también puede incluir datos adicionales, como parámetros de perfil de Target y detalles de pedidos | Pase los datos adicionales en el campo TargetParameters proporcionados por las API [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} y [clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} | Utilice las API [generateDisplayInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} y [generateTapInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} de métodos públicos disponibles en la oferta para la ubicación de mbox a fin de generar los datos con formato XDM para su vista y hacer clic respectivamente. A continuación, llame a la API de Edge SDK [sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#sendevent){target=_blank} para enviar estos datos XDM de seguimiento junto con cualquier dato XDM y de forma libre adicional a la red de Experience Edge. |


A continuación, aprenda a [actualizar audiencias y scripts de perfil](update-audiences.md) para garantizar la compatibilidad con la extensión de Offer Decisioning y Target.

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Offer Decisioning y Target. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
