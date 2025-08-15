---
title: Enriquecimiento de audiencias con datos de Warehouse
seo-title: Enrich Audiences with Warehouse Data | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: Enriquecimiento de audiencias con datos de Warehouse
description: En este ejercicio, la audiencia de Experience Platform se enriquece con los datos del almacén.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 7%

---

# Enriquecimiento de audiencias con datos de Warehouse

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

Observaremos otro ejemplo del uso de datos federados para [admitir la personalización &quot;en el momento&quot;](deliver-in-the-moment-personalization.md).
