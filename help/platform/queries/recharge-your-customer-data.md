---
title: Recargue los datos de sus clientes para ofrecer experiencias electrizantes
description: Aprenda a mitigar el impacto de los datos de baja calidad, reducir el tiempo de respuesta al valor y multiplicar el retorno de la inversión utilizando los mismos datos para multitud de casos de uso.
feature: Queries
role: Data Engineer, Data Architect, Developer
level: Beginner
jira: KT-10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# Recargue los datos de sus clientes para ofrecer experiencias electrizantes

Los datos omnicanal son un ingrediente crítico para impulsar perfiles de clientes procesables utilizados por los especialistas en marketing para organizar la activación y medir los recorridos de clientes resultantes. Sin embargo, las organizaciones se enfrentan a desafíos en la administración de la calidad, la escala y la variedad de estos datos. Requieren soluciones optimizadas para mitigar el impacto de los datos de baja calidad, reducir el tiempo de respuesta al valor y multiplicar el retorno de la inversión utilizando los mismos datos para multitud de casos de uso.
Para obtener más información, visite la [Documentación del servicio de consultas](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=es).

Este vídeo explora:

* Funciones de preparación de datos de Adobe Experience Platform que puede aprovechar
* Aumento del ROI de Adobe Real-Time CDP, Adobe Journey Optimizer y Customer Journey Analytics

>[!VIDEO](https://video.tv.adobe.com/v/342533?learn=on)

## Ejemplo de SQL

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceID AS customerId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(C._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset C
WHERE A._experience.analytics.customDimensions.eVars.eVar1 = B.personKey.sourceID
AND A.productListItems[0].sku = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

>[!NOTE]
>
>Este vídeo es un extracto de la sesión de Adobe Summit 2020 *[Recarga de datos omnicanal para electrificar experiencias](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
