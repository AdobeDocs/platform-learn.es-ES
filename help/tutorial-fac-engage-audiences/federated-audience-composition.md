---
title: Enriquecimiento de audiencias con datos de almacén
seo-title: Enrich Audiences with warehouse data | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Enriquecimiento de audiencias con datos de almacén
description: En este ejercicio, la audiencia de Experience Platform se enriquece con los datos del almacén.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: 7e2f7bbb392eba51c0d6b9ccc8224c2081a01c7c
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 7%

---

# Enriquecimiento de las audiencias con datos de almacén

La composición de audiencias federada permite enriquecer audiencias existentes en Adobe Experience Platform (AEP) utilizando datos de audiencia compuestos que se han federado desde Enterprise Data Warehouse. Estos datos no se mantendrán en los perfiles de clientes de Adobe Experience Platform.

## Lectura de una audiencia dentro de una composición federada

En este ejercicio, utilizamos la audiencia **Visitante de página de solicitud de préstamo de SecurFinancial** almacenada en el servicio de perfil de Experience Platform para iniciar nuestra composición federada. Utiliza los datos federados de Snowflake para determinar la aprobación previa en función de la puntuación crediticia y la actividad del préstamo.

![ejemplo de composición federada](assets/snowflake-preapproval.png)

### Pasos

1. **Asigne la audiencia de AEP** al destino de composición de audiencias federada.
2. **Cree su composición** con la audiencia asignada como audiencia de lectura.
3. **Reconcilie las identidades** de la audiencia de lectura para unirse a los datos federados.

![método federado-1-1](assets/federated-method-1-1.png)

![método federado-1-2](assets/federated-method-1-2.png)

Observaremos otro ejemplo de uso de datos federados para [ofrecer personalización &quot;en el momento&quot;](deliver-in-the-moment-personalization.md).
