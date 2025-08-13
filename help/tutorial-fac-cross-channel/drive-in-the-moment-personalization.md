---
title: Impulsar la personalización "en el momento" en Edge
seo-title: Drive "in-the moment" personalization on the Edge | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Impulsar la personalización "en el momento" en Edge
description: En este ejercicio visual, la audiencia federada se evalúa en Edge para un retargeting instantáneo "en el momento".
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-drive-in-the-moment-personalization.jpg
hide: true
source-git-commit: 0bbdc93969b4716407ecf51499d572cb50f5a0d3
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# Impulsar la personalización &quot;en el momento&quot; en Edge

La composición de audiencias federada permite enriquecer audiencias existentes en Adobe Experience Platform (AEP) utilizando datos de audiencia compuestos que se han federado desde Enterprise Data Warehouse. Estos datos no se mantendrán en los perfiles de clientes de Adobe Experience Platform.

En este ejercicio visual, utilizamos una audiencia federada que consulta con la puntuación crediticia y la actividad de préstamo para enriquecer la audiencia de comportamiento de los visitantes de la página web de la solicitud de préstamo.

Al evaluar esta audiencia en Edge, redireccionamos instantáneamente los visitantes de la página de solicitud de préstamo aprobada previamente con ofertas personalizadas en el sitio.

![edge-audience-enrich](assets/edge-audience-enrich.png)

## Pasos

1. **Guardar e iniciar** su composición de audiencia federada. Una vez ejecutada la composición, la audiencia federada aparecerá en el portal de audiencias.
2. **Genere una regla de audiencia** usando atributos de perfil y eventos de experiencia del servicio de perfil, incorporando su audiencia federada.

¡Vamos a terminar esto con un [resumen de aprendizajes y aprendizajes finales](conclusion.md)!
