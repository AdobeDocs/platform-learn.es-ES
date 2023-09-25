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
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%

---

# Ejecutar consultas

<!-- 15 min-->
En esta lección, aprenderá a configurar, escribir y ejecutar consultas para validar los datos que ha introducido.

Adobe Experience Platform Query Service le ayuda a dar sentido a sus datos, ya que le permite utilizar SQL estándar para consultar datos en Platform. Con el servicio de consulta, puede unirse a cualquier conjunto de datos del lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, el aprendizaje automático o para su inserción en el perfil del cliente en tiempo real.

**Arquitectos de datos** y **Ingenieros de datos** Necesitará utilizar el servicio de consulta fuera de este tutorial.

Antes de comenzar los ejercicios, vea este breve vídeo para obtener más información sobre el servicio de consultas:
>[!VIDEO](https://video.tv.adobe.com/v/29795?learn=on)

## Permisos necesarios

En el [Configuración de permisos](configure-permissions.md) Esta lección, ha configurado todos los controles de acceso necesarios para completar esta lección.

<!-- Settings > **[!UICONTROL Services]** > **[!UICONTROL Query Service]**
* Permission items Data Management > **[!UICONTROL View Datasets]** and  **[!UICONTROL Manage Datasets]**
* Permission item Sandboxes > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Consultas simples

Empecemos con algunas consultas simples:

1. En la interfaz de usuario de Platform, vaya a **Consultas** en el panel de navegación izquierdo
1. Seleccione el **Crear consulta** en la parte superior derecha para abrir un cuadro de texto para ejecutar y ejecutar consultas
1. Introduzca la siguiente consulta en el editor y pulse Mayús+Intro o Mayús+Retorno para ejecutar la consulta.

   ```
   SHOW TABLES
   ```

1. Muestra la lista de tablas disponibles

   ![MOSTRAR CONSULTA DE TABLA](assets/queries-showTables.png)


1. Ahora pruebe esta consulta, reemplazando `_techmarketingdemos` con su propia área de nombres de inquilino, que, si lo recuerda, es visible en los esquemas.

   ```
   SELECT person.name.lastName,loyalty.tier
   FROM luma_loyalty_dataset
   WHERE loyalty.tier ='gold'
   ```

   ![SELECCIONAR datos del conjunto de datos de fidelidad](assets/queries-loyaltySelect.png)

1. Si se produce algún error, aparecen mensajes detallados en la **[!UICONTROL Consola]** , como se muestra a continuación
   ![Error en la consulta](assets/queries-error.png)

1. Con la consulta correcta, **[!UICONTROL Nombre]** it `Luma Gold Level Customers`
1. Seleccione el botón **[!UICONTROL Guardar]**
   ![Guardado de la consulta](assets/queries-loyaltySelect-save.png)


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

Y ahora para la última lección práctica, [creación de segmentos](build-segments.md)!
