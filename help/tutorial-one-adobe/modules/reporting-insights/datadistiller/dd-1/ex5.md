---
title: 'Servicio de consultas: Power BI/Tableau'
description: 'Servicio de consultas: Power BI/Tableau'
kt: 5342
doc-type: tutorial
exl-id: 4c89fa24-44a5-4a9a-bb24-39ad4650c503
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 1%

---

# 2.1.5 Generar un conjunto de datos a partir de una consulta

## Objetivo

Obtenga información sobre cómo generar conjuntos de datos a partir de resultados de consultas
Conecte Microsoft Power BI Desktop/Tableau directamente al servicio de consultas
Creación de un informe en Microsoft Power BI Desktop/Tableau Desktop

## Contexto

Una interfaz de línea de comandos para consultar datos es emocionante, pero no se presenta bien. En esta lección, le guiaremos a través de un flujo de trabajo recomendado para saber cómo puede utilizar Microsoft Power BI Desktop/Tableau directamente en el servicio de consultas para crear informes visuales para las partes interesadas.

## Crear un conjunto de datos a partir de una consulta SQL

La complejidad de la consulta afectará el tiempo que tarda el servicio de consultas en devolver los resultados. Y cuando se realiza una consulta directamente desde la línea de comandos u otras soluciones como Microsoft Power BI/Tableau, el servicio Query se configura con un tiempo de espera de 5 minutos (600 segundos). Y en algunos casos, estas soluciones se configurarán con tiempos de espera más cortos. Para ejecutar consultas más grandes y cargar por adelantado el tiempo que se tarda en devolver resultados, ofrecemos una función para generar un conjunto de datos a partir de los resultados de la consulta. Esta función utiliza la función estándar de SQL conocida como Crear tabla como seleccionar (CTAS). Está disponible en la interfaz de usuario de Platform desde la Lista de consultas y también está disponible para ejecutarse directamente desde la línea de comandos con PSQL.

En el anterior ha reemplazado **escriba su nombre** por su propio ldap antes de ejecutarlo en PSQL.

```sql
select /* enter your name */
       e.--aepTenantId--.identification.core.ecid as ecid,
       e.placeContext.geo.city as city,
       e.placeContext.geo._schema.latitude latitude,
       e.placeContext.geo._schema.longitude longitude,
       e.placeContext.geo.countryCode as countrycode,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callFeeling as callFeeling,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic as callTopic,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callContractCancelled as contractCancelled,
       l.--aepTenantId--.loyaltyDetails.level as loyaltystatus,
       l.--aepTenantId--.loyaltyDetails.points as loyaltypoints,
       l.--aepTenantId--.identification.core.crmId as crmid
from   demo_system_event_dataset_for_website_global_v1_1 e
      ,demo_system_event_dataset_for_call_center_global_v1_1 c
      ,demo_system_profile_dataset_for_crm_global_v1_1 l
where  e.--aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
and    e.web.webPageDetails.name in ('Cancel Service', 'Call Start')
and    e.--aepTenantId--.identification.core.ecid = c.--aepTenantId--.identification.core.ecid
and    l.--aepTenantId--.identification.core.ecid = e.--aepTenantId--.identification.core.ecid;
```

Vaya a la IU de Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

Para buscar la instrucción ejecutada en la interfaz de usuario de Adobe Experience Platform Query, escriba el LDAP en el campo de búsqueda:

Seleccione **Consultas**, vaya a **Registro** e introduzca su LDAP en el campo de búsqueda.

![search-query-for-ctas.png](./images/searchqueryforctas.png)

Seleccione la consulta y haga clic en **Ejecutar como CTAS**.

![search-query-for-ctas.png](./images/searchqueryforctasa.png)

Escriba `--aepUserLdap-- Callcenter Interaction Analysis` como nombre y descripción para el conjunto de datos y haga clic en **Ejecutar como CTAS**.

![create-ctas-dataset.png](./images/createctasdataset.png)

Como resultado, verá una nueva consulta con el estado **Enviado**.

![ctas-query-submitted.png](./images/ctasquerysubmitted.png)

Una vez que finalice, verá una nueva entrada para **Conjunto de datos creado** (es posible que tenga que actualizar la página).

![ctas-dataset-created.png](./images/ctasdatasetcreated.png)

Tan pronto como se cree el conjunto de datos (que puede tardar entre 5 y 10 minutos), puede continuar con el ejercicio.

## Pasos siguientes

Ir a la opción A: [2.1.6 Query Service y Power BI](./ex6.md){target="_blank"}

Ir a la opción B: [2.1.7 Query Service y Tableau](./ex7.md){target="_blank"}

Volver a [servicio de consultas](./query-service.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
