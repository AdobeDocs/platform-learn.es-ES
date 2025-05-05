---
title: Ejecutar consultas
seo-title: Run queries | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Ejecutar consultas
description: En esta lección, aprenderá a configurar, escribir y ejecutar consultas para validar los datos que ha introducido.
role: Data Architect, Data Engineer
feature: Queries
jira: KT-4348
thumbnail: 4348-run-queries.jpg
exl-id: a37531cb-96ad-4547-86af-84f7ed65f019
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Ejecutar consultas

<!-- 15 min-->
En esta lección, aprenderá a configurar, escribir y ejecutar consultas para validar los datos que ha introducido.

Adobe Experience Platform Query Service le ayuda a dar sentido a sus datos, ya que le permite utilizar SQL estándar para consultar datos en Platform. Con el servicio de consulta, puede unirse a cualquier conjunto de datos del lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, el aprendizaje automático o para su inserción en el perfil del cliente en tiempo real.

**Los arquitectos de datos** y **ingenieros de datos** necesitarán usar el servicio de consulta fuera de este tutorial.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre el servicio de consultas:
>[!VIDEO](https://video.tv.adobe.com/v/33590?learn=on&enablevpops&captions=spa)

## Permisos necesarios

En la lección [Configurar permisos](configure-permissions.md), configuró todos los controles de acceso necesarios para completar esta lección.

<!-- Settings > **[!UICONTROL Services]** > **[!UICONTROL Query Service]**
* Permission items Data Management > **[!UICONTROL View Datasets]** and  **[!UICONTROL Manage Datasets]**
* Permission item Sandboxes > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Consultas simples

Empecemos con algunas consultas simples:

1. En la interfaz de usuario de Platform, vaya a **Consultas** en el panel de navegación izquierdo
1. Seleccione el botón **Crear consulta** de la parte superior derecha para abrir un cuadro de texto para ejecutar y ejecutar consultas
1. Introduzca la siguiente consulta en el editor y pulse Mayús+Intro o Mayús+Retorno para ejecutar la consulta.

   ```
   SHOW TABLES
   ```

1. Muestra la lista de tablas disponibles

   ![MOSTRAR CONSULTA DE TABLA](assets/queries-showTables.png)


1. Ahora intente esta consulta, reemplazando `_techmarketingdemos` con su propio espacio de nombres de inquilino, que, si lo recuerda, es visible en los esquemas.

   ```
   SELECT person.name.lastName,loyalty.tier
   FROM luma_loyalty_dataset
   WHERE loyalty.tier ='gold'
   ```

   ![SELECCIONAR datos del conjunto de datos de fidelidad](assets/queries-loyaltySelect.png)

1. Si hay algún error, aparecerán mensajes detallados en la ficha **[!UICONTROL Consola]**, como se muestra a continuación
   ![Error en la consulta](assets/queries-error.png)

1. Con la consulta que realizó correctamente, **[!UICONTROL Name]** lo `Luma Gold Level Customers`
1. Seleccione el botón **[!UICONTROL Guardar]**
   ![Guardando la consulta](assets/queries-loyaltySelect-save.png)


<!--SELECT COUNT(DISTINCT (_techmarketingdemos.systemIdentifier.loyaltyId)) FROM luma_loyalty_dataset 


SELECT _techmarketingdemos.systemIdentifier.loyaltyId, COUNT(_techmarketingdemos.systemIdentifier.loyaltyId)
FROM luma_loyalty_dataset 
GROUP BY _techmarketingdemos.systemIdentifier.loyaltyId
HAVING COUNT(_techmarketingdemos.systemIdentifier.loyaltyId) > 1;-->

## Ejercicios adicionales

Más adelante se añadirán ejercicios adicionales del servicio de consulta al tutorial.
<!--
## Join Datasets

In this exercise, we will join two datasets `Luma Loyalty Dataset` and `Luma Offline Purchase` to get list of gold customers who have spend over $500 dollars in one purchase.

1. Create a new query
1. Copy and paste following query in query editor and execute, again replacing `_techmarketingdemos` with your own tenant namespace
    
    ```
    SELECT DISTINCT lopd.commerce.order.purchaseID as PurchaseId ,
        lld.person.name.firstName as LastName ,
        lld.person.name.lastName as LastName ,
        lopd.personalEmail.address as email,
        lopd.commerce.order.priceTotal as Total

    FROM luma_loyalty_dataset lld
    JOIN luma_offline_purchase_event_dataset lopd
    ON lopd._techmarketingdemos.systemIdentifier.loyaltyId = lld._techmarketingdemos.systemIdentifier.loyaltyId

    WHERE lld._techmarketingdemos.loyalty.level ='gold' AND lopd.commerce.order.priceTotal >500;
    ```

1. You should get list of Gold Customers who have spend over $500 in single purchase.

## Output datasets

1. Select on Output Dataset button
1. Provide name and description to the dataset
1. Save.
1. Go to **Datasets** under **Data Management** to find new dataset created.

-->
<!--Add content for Adobe Defined Functions-->

## Recursos adicionales

* [Documentación del servicio de consultas](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=es)
* [Referencia de API del servicio de consultas](https://www.adobe.io/experience-platform-apis/references/query-service/)

Y ahora, para la lección práctica final, [creando segmentos](build-segments.md)!
