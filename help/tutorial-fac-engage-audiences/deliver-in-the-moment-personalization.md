---
title: Ofrezca personalización "en el momento" mediante Edge Network
seo-title: Deliver "in-the moment" personalization using Edge Network | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: Ofrezca personalización "en el momento" mediante Edge Network
description: En este ejercicio, la audiencia federada se evalúa en Edge para un retargeting instantáneo "en el momento".
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-drive-in-the-moment-personalization.jpg
exl-id: 20bfafb1-1d1b-48d8-84eb-97d4c9e03b76
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# Ofrezca personalización &quot;en el momento&quot; mediante Edge Network

La composición de audiencias federada permite enriquecer audiencias existentes en Adobe Experience Platform (AEP) utilizando datos de audiencia compuestos que se han federado desde Enterprise Data Warehouse. Estos datos no se mantendrán en Adobe Experience Platform.

En este ejercicio visual, utilizamos una audiencia federada que consulta con la puntuación crediticia y la actividad de préstamo para enriquecer la audiencia de comportamiento de los visitantes de la página web de la solicitud de préstamo.

Al evaluar esta audiencia en Edge, redireccionamos instantáneamente los visitantes de la página de solicitud de préstamo aprobada previamente con ofertas personalizadas en el sitio.

![edge-audience-enrich](assets/edge-audience-enrich.png)

## Pasos

1. **Guardar e iniciar** su composición de audiencia federada. Una vez ejecutada la composición, la audiencia federada aparecerá en el portal de audiencias.
2. **Genere una regla de audiencia** usando atributos de perfil y eventos de experiencia del servicio de perfil, incorporando su audiencia federada.

¡Vamos a terminar esto con un [resumen de aprendizajes y aprendizajes finales](conclusion.md)!
