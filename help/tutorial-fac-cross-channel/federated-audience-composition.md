---
title: Enriquezca las audiencias de Experience Platform con datos federados
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Enriquezca las audiencias de Experience Platform con datos federados
description: En este ejercicio visual, una audiencia de Experience Platform se enriquece con datos federados.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: 3de9721332379f9fd3dd45768ba2ca2308e09357
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 7%

---

# Enriquecimiento de las audiencias de Experience Platform con datos federados

La composición de audiencias federada permite enriquecer audiencias existentes en Adobe Experience Platform (AEP) utilizando datos de audiencia compuestos que se han federado desde Enterprise Data Warehouse. Estos datos no se mantendrán en los perfiles de clientes de Adobe Experience Platform.

## Lectura de una audiencia de AEP en una composición federada

En este ejercicio visual, utilizamos la audiencia **Visitante de página de solicitud de préstamo de SecurFinancial** almacenada en el servicio de perfil de AEP para iniciar nuestra composición federada. Utiliza los datos federados de Snowflake para determinar la aprobación previa en función de la puntuación crediticia y la actividad del préstamo.

![ejemplo de composición federada](assets/snowflake-preapproval.png)

### Pasos

1. **Asigne la audiencia de AEP** al destino de composición de audiencias federada.
2. **Cree su composición** con la audiencia asignada como audiencia de lectura.
3. **Reconcilie las identidades** de la audiencia de lectura para unirse a los datos federados.

![método federado-1-1](assets/federated-method-1-1.png)

![método federado-1-2](assets/federated-method-1-2.png)

Observaremos otro ejemplo del uso de datos federados para [admitir la personalización &quot;en el momento&quot;](drive-in-the-moment-personalization.md).
