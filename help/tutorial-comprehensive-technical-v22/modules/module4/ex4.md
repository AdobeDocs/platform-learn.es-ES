---
title: Servicio de consultas - Power BI/Tableau
description: Servicio de consultas - Power BI/Tableau
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 11525d05-1c19-4d41-8f47-4feb3e8aed66
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 4.4 Generar un conjunto de datos a partir de una consulta

## Objetivo

Obtenga información sobre cómo generar conjuntos de datos a partir de resultados de consultas Conecte Microsoft Power BI Desktop/Tableau directamente al servicio de consultas Creación de un informe en Microsoft Power BI Desktop/Tableau Desktop

## Contexto de la lección

Una interfaz de línea de comandos para consultar los datos es emocionante pero no está bien presente. En esta lección, le guiaremos a través de un flujo de trabajo recomendado para saber cómo puede usar Microsoft Power BI Desktop/Tableau directamente en el servicio de consultas para crear informes visuales para sus interesados.

## 4.4.1 Crear un conjunto de datos a partir de una consulta SQL

La complejidad de la consulta afectará el tiempo que tardará el servicio de consulta en devolver los resultados. Y al consultar directamente desde la línea de comandos u otras soluciones como Microsoft Power BI/Tableau, el servicio de consulta se configura con un tiempo de espera de 5 minutos (600 segundos). Y en algunos casos, estas soluciones se configurarán con tiempos de espera más cortos. Para ejecutar consultas más grandes y cargar al principio el tiempo que se tarda en devolver resultados, ofrecemos una función para generar un conjunto de datos a partir de los resultados de la consulta. Esta función utiliza la función estándar de SQL conocida como Crear tabla como Seleccionar (CTAS). Está disponible en la interfaz de usuario de Platform desde la lista de consultas y también está disponible para ejecutarse directamente desde la línea de comandos con PSQL.

En el anterior ha reemplazado **escriba su nombre** con su propio LDAP antes de ejecutarlo en PSQL.

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
       l.--aepTenantId--.identification.core.loyaltyId as crmid
from   demo_system_event_dataset_for_website_global_v1_1 e
      ,demo_system_event_dataset_for_call_center_global_v1_1 c
      ,demo_system_profile_dataset_for_loyalty_global_v1_1 l
where  e.--aepTenantId--.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal')
and    e.web.webPageDetails.name in ('Cancel Service', 'Call Start')
and    e.--aepTenantId--.identification.core.ecid = c.--aepTenantId--.identification.core.ecid
and    l.--aepTenantId--.identification.core.ecid = e.--aepTenantId--.identification.core.ecid;
```

Vaya a la interfaz de usuario de Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

Para buscar la instrucción ejecutada en la interfaz de usuario de Adobe Experience Platform Query, introduzca el LDAP en el campo de búsqueda:

Select **Consultas**, vaya a **Registro** e introduzca el LDAP en el campo de búsqueda.

![search-query-for-ctas.png](./images/search-query-for-ctas.png)

Seleccione la consulta y haga clic en **Conjunto de datos de salida**.

![search-query-for-ctas.png](./images/search-query-for-ctasa.png)

Entrar `--demoProfileLdap-- Callcenter Interaction Analysis` como nombre y descripción para el conjunto de datos y pulse el botón **Ejecutar consulta** botón

![create-ctas-dataset.png](./images/create-ctas-dataset.png)

Como resultado, verá una nueva consulta con un estado **Enviado**.

![ctas-query-submit.png](./images/ctas-query-submitted.png)

Una vez finalizada, verá una nueva entrada para **Conjunto de datos creado** (es posible que deba actualizar la página).

![ctas-dataset-created.png](./images/ctas-dataset-created.png)

Tan pronto como se cree el conjunto de datos (que puede tardar entre 5 y 10 minutos), podrá continuar con el ejercicio.

Paso siguiente: Opción A: [4.5 Servicio y Power BI de consultas](./ex5.md)

Paso siguiente: Opción B: [4.6 Servicio de Consulta y Tableau](./ex6.md)

[Volver al módulo 4](./query-service.md)

[Volver a todos los módulos](../../overview.md)
