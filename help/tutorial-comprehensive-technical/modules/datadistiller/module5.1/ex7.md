---
title: 'Servicio de consultas: API del servicio de consultas'
description: 'Servicio de consultas: API del servicio de consultas'
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 2%

---

# 5.1.7 API del servicio de consultas

## Objetivo

- Utilice la API del servicio de consultas para administrar plantillas de consultas y programaciones de consultas

## Contexto

En este ejercicio, ejecutará llamadas de API para administrar plantillas de consulta y programaciones de consultas mediante una colección de Postman. Definirá plantillas de consulta, ejecutará consultas regulares y consultas CTAS. Una consulta **CTAS** (cree una tabla como consulta de selección) almacena su conjunto de resultados en un conjunto de datos explícito. Mientras que las consultas regulares se almacenan en un conjunto de datos implícito (o generado por el sistema), que normalmente se exporta en formato de archivo parquet.

## Documentación

- [Ayuda del servicio de consultas de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/query/api/getting-started.html)
- [API de servicio de consultas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml)

## 5.1.7.1 API del servicio de consulta

La API del servicio de consultas permite administrar consultas no interactivas con el lago de datos de Adobe Experience Platform.

No interactivo significa que una solicitud para ejecutar una consulta no dará como resultado una respuesta inmediata. La consulta se procesará y su conjunto de resultados se almacenará en un conjunto de datos implícito o explícito (CTAS: create table as select).

## 5.1.7.2 Consulta de muestra

Como consulta de ejemplo, usará la primera consulta enumerada en [4.3: consultas, consultas, consultas... y análisis de pérdida](./ex3.md):

¿Cuántas vistas de productos tenemos diariamente?

**SQL**

```sql
select date_format( timestamp , 'yyyy-MM-dd') AS Day,
       count(*) AS productViews
from   demo_system_event_dataset_for_website_global_v1_1
where  --aepTenantId--.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal')
and eventType = 'commerce.productViews'
group by Day
limit 10;
```

## 5.1.7.3 Consultas

Abra Postman en el equipo. Como parte del módulo 3, creó un entorno de Postman e importó una colección de Postman. Siga las instrucciones de [Ejercicio 2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md) por si aún no lo ha hecho.

Como parte de la colección de Postman que importó, verá una carpeta **3. Servicio de consultas**. Si no ve esta carpeta, vuelva a descargar la [colección de Postman](./../../../assets/postman/postman_profile.zip) y vuelva a importar esa colección en Postman como se indica en el [Ejercicio 2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md).

![QS](./images/pm3.png)

>[!NOTE]
>
>En este momento, sólo la carpeta **1. Consultas** contiene solicitudes. Otras solicitudes se añadirán en una fase de capa.

Abra esa carpeta y conozca las llamadas de API del servicio de consulta para ejecutar, supervisar y descargar el conjunto de resultados de la consulta.

Una llamada del POST a [/query/queries] con la siguiente carga útil almacenará en déclencheur la ejecución de nuestra consulta;

### 5.1.7.3.1 Crear consulta

Haga clic en la solicitud **1.1 QS - Crear consulta** y vaya a **Encabezados**. A continuación, verá esto:

![Segmentación](./images/s1_call.png)

Vamos a centrarnos en este campo de encabezado:

| Clave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Debe especificar el nombre de la zona protegida de Adobe Experience Platform que está utilizando. El campo de encabezado **x-sandbox-name** debe ser `--module7sandbox--`.

Vaya a la sección **Body** de esta solicitud. En **Cuerpo** de esta solicitud, verá lo siguiente:

![Segmentación](./images/s1_bodydtl.png)

```sql
{
    "name" : "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"description": "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "module7:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

Atención: actualice la variable **name** en la siguiente solicitud reemplazando **ldap** por su **ldap** específico.

Después de agregar su **ldap** específico, el cuerpo debería tener un aspecto similar al siguiente:

```json
{
    "name" : "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "module7:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

>[!NOTE]
>
>La clave **dbName** del cuerpo de JSON anterior hace referencia a la zona protegida que se usa en la instancia de Adobe Experience Platform. Si está usando la zona protegida de PROD, dbName debe ser **prod:all**, si usa otra zona protegida como por ejemplo **module7**, dbName debe ser igual a **module7:all**.

A continuación, haga clic en el botón azul **Enviar** para crear el segmento y ver los resultados.

![Segmentación](./images/s1_bodydtl_results.png)

Cuando se realiza correctamente, la solicitud del POST devolverá la siguiente respuesta:

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "module7:all",
        "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
        "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
        "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
    },
    "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
    "elapsedTime": 0,
    "updated": "2021-01-20T13:23:13.951Z",
    "client": "API",
    "userId": "A3392DB95FFF08EE0A495E87@techacct.adobe.com",
    "created": "2021-01-20T13:23:13.951Z",
    "_links": {
        "self": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

El **estado** actual de la consulta es **ENVIADO**, una vez ejecutado su estado pasará a ser **CORRECTO**.

También puede buscar las consultas enviadas a través de la interfaz de usuario de Adobe Experience Platform, abrir [Adobe Experience Platform](https://experience.adobe.com/#/@experienceplatform/platform/home), navegar hasta **Consultas**, **Registrar** y seleccionar la consulta:

![Segmentación](./images/s1_bodydtl_results_qs.png)

### 5.1.7.3.2 Obtener consultas

Haga clic en la solicitud **1.2 QS - Obtener consultas** y vaya a **Encabezados**. A continuación, verá esto:

![Segmentación](./images/s2_call.png)

Vamos a centrarnos en este campo de encabezado:

| Clave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Debe especificar el nombre de la zona protegida de Adobe Experience Platform que está utilizando. El campo de encabezado **x-sandbox-name** debe ser `--module7sandbox--`.

Ir a **Parámetros**. A continuación, verá esto:

![Segmentación](./images/s2_call_p.png)

El parámetro **orderby** le permite especificar un criterio de ordenación basado en la propiedad **created**. Observe el signo **&#39;-&#39;** delante de created, lo que significa que el orden en que se devuelve la lista de consultas usará su fecha de creación en el orden **descendente**. La consulta debe estar en la parte superior de la lista.

A continuación, haga clic en el botón azul **Enviar** para crear el segmento y ver los resultados.

![Segmentación](./images/s2_bodydtl_results.png)

Si la solicitud se realiza correctamente, devolverá una respuesta de similar a la siguiente. El **estado** de la respuesta puede ser **ENVIADO**, **EN CURSO** o **CORRECTO**. La consulta puede tardar varios minutos en tener un estado **SUCCESS**. Puede repetir el envío de esta solicitud varias veces, hasta que vea el estado **SUCCESS**.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "module7:all",
                "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
                "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
                "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
            },
            "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
            "state": "SUCCESS",
            "rowCount": 1,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "elapsedTime": 217481,
            "updated": "2021-01-20T13:26:51.432Z",
            "client": "API",
            "userId": "A3392DB95FFF08EE0A495E87@techacct.adobe.com",
            "created": "2021-01-20T13:23:13.951Z",
            "_links": {
                "self": {
                    "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "60080ace62c49a19490c5870",
                        "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/60080ace62c49a19490c5870"
                    }
                ]
            }
        }
     ]
    },
    "version": 1
}
```

Cuando el estado sea **SUCCESS**, continúe con la siguiente solicitud.

### 5.1.7.3.3 Obtener estado de la consulta

Haga clic en la solicitud **1.3 QS - Obtener estado de la consulta** y vaya a **Encabezados**. A continuación, verá esto:

![Segmentación](./images/s3_call.png)

Vamos a centrarnos en este campo de encabezado:

| Clave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Debe especificar el nombre de la zona protegida de Adobe Experience Platform que está utilizando. El campo de encabezado **x-sandbox-name** debe ser `--module7sandbox--`.

A continuación, haga clic en el botón azul **Enviar** para crear el segmento y ver los resultados.

![Segmentación](./images/s3_bodydtl_results.png)

Si la solicitud se realiza correctamente, devolverá una respuesta de similar a la siguiente.

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "module7:all",
        "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
        "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
        "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
    },
    "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
    "state": "SUCCESS",
    "rowCount": 1,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
    "elapsedTime": 217481,
    "updated": "2021-01-20T13:26:51.432Z",
    "client": "API",
    "userId": "A3392DB95FFF08EE0A495E87@techacct.adobe.com",
    "created": "2021-01-20T13:23:13.951Z",
    "_links": {
        "self": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "referenced_datasets": [
            {
                "id": "60080ace62c49a19490c5870",
                "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/60080ace62c49a19490c5870"
            }
        ]
    }
}
```

Cuando una consulta alcanza el estado de **SUCCESS**, la respuesta también indicará el número de filas recuperadas por la consulta a través de la propiedad **rowCount**. En nuestro ejemplo, la consulta devuelve 10 filas. Veamos en la siguiente sección cómo podemos recuperar las 10 filas.

### 5.1.7.3.4 Recuperar resultado de la consulta

La respuesta **SUCCESS** anterior incluye una propiedad **referenced_datasets**, que apunta al conjunto de datos implícito que almacena el resultado de la consulta. Para obtener acceso al resultado, usamos su propiedad **href** o **id**.

Haga clic en la solicitud **1.4 QS - Obtener resultado de la consulta** y vaya a **Encabezados**. A continuación, verá esto:

![Segmentación](./images/s4_call.png)

Vamos a centrarnos en este campo de encabezado:

| Clave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Debe especificar el nombre de la zona protegida de Adobe Experience Platform que está utilizando. El campo de encabezado **x-sandbox-name** debe ser `--module7sandbox--`.

A continuación, haga clic en el botón azul **Enviar** para crear el segmento y ver los resultados.

![Segmentación](./images/s4_bodydtl_results.png)

La respuesta de esta solicitud apuntará a los archivos del conjunto de datos:

```json
{
    "60080ace62c49a19490c5870": {
        "name": "Demo System - Event Dataset for Website (Global v1.1)",
        "description": "Demo System - Event Dataset for Website (Global v1.1)",
        "enableErrorDiagnostics": false,
        "tags": {
            "adobe/siphon/partition/definition": [
                "day(timestamp, _ACP_DATE)",
                "identity(_ACP_BATCHID)"
            ],
            "aep/siphon/partitions": [
                "_ACP_DATE",
                "_ACP_BATCHID"
            ],
            "acp_granular_plugin_validation_flags": [
                "identity:enabled",
                "profile:enabled"
            ],
            "adobe/siphon/buffered-promotion-recency": [
                "live"
            ],
            "adobe/siphon/use-buffered-promotion": [
                "true"
            ],
            "adobe/pqs/table": [
                "demo_system_event_dataset_for_website_global_v1_1"
            ],
            "aep/siphon/expire-snapshot-timestamp": [
                "1611141272703"
            ],
            "acp_granular_validation_flags": [
                "requiredFieldCheck:enabled"
            ],
            "acp_validationContext": [
                "enabled"
            ],
            "adobe/siphon/table/format": [
                "iceberg"
            ],
            "unifiedProfile": [
                "enabled:true",
                "enabledAt:2021-01-20 10:49:51"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "imsOrg": "907075E95BF479EC0A495C73@AdobeOrg",
        "sandboxId": "62cd9f38-8529-4b05-8d9f-388529db0540",
        "lastBatchId": "01EWFQZ15XRNNB1FPKPW5ETRVP",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "01EWFQZ15XRNNB1FPKPW5ETRVP",
        "version": "1.0.6",
        "created": 1611139790698,
        "updated": 1611149266031,
        "createdClient": "750e24ee855b4ac18ccc4f4817f96ee1",
        "createdUser": "3A260B485E909A170A495E76@techacct.adobe.com",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "viewId": "60080ace62c49a19490c5871",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/60080ace62c49a19490c5870/views/60080ace62c49a19490c5871/files",
        "schemaMetadata": {
            "delta": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/experienceplatform/schemas/d9b88a044ad96154637965a97ed63c7b20bdf2ab3b4f642e",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

>[!NOTE]
>
>Próximamente se añadirán más ejercicios para ayudarle a interactuar con la API del servicio de consultas.

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 5.1](./query-service.md)

[Volver a todos los módulos](../../../overview.md)
