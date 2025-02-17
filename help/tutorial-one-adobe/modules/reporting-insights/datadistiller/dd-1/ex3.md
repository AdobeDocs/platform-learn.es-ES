---
title: 'Servicio de consultas: uso del servicio de consultas'
description: 'Servicio de consultas: uso del servicio de consultas'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
exl-id: ce04fa00-0247-4693-ba60-efc1746b9fec
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# 2.1.3 Uso del servicio de consultas

## Objetivo

- Buscar y explorar conjuntos de datos
- Obtenga información sobre cómo abordar objetos y atributos de modelos de datos de experiencia en las consultas

## Contexto

En este vídeo aprenderá a utilizar PSQL para recuperar información sobre los conjuntos de datos disponibles, a escribir consultas para el modelo de datos de experiencia (XDM) y a escribir sus primeras consultas de creación de informes simples con los conjuntos de datos del servicio de consulta y de Citi Signal.

## Consultas básicas

En este vídeo aprenderá acerca de los métodos para recuperar información sobre los conjuntos de datos disponibles y cómo recuperar correctamente datos con una consulta de un conjunto de datos XDM.

Todos los conjuntos de datos que hemos explorado a través de Adobe Experience Platform al principio de 1, también están disponibles para el acceso a través de una interfaz SQL como tablas. Para enumerar esas tablas, puede usar el comando **show tables;**.

Ejecute `show tables;` en su **interfaz de línea de comandos PSQL**. (no olvide terminar el comando con un punto y coma).

Copie el comando `show tables;` y péguelo en el símbolo del sistema:

![command-prompt-show-tables.png](./images/commandpromptshowtables.png)

Verá el siguiente resultado:

```text
tech-insiders:all=> show tables;
                               name                               |                                                  dataSetId                                                   |                                       dataSet                                        | description |        labels        
------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+-------------+----------------------
 ajo_bcc_feedback_event_dataset                                   | 672a07cb7728e82aefa1ec56                                                                                     | AJO BCC Feedback Event Dataset                                                       |             | 
 ajo_classification_dataset                                       | 672a07cab55b0d2aef6f9626                                                                                     | AJO Classification Dataset                                                           |             | 
 ajo_consent_service_dataset                                      | 672a07c80fd5fd2aee4155ca                                                                                     | AJO Consent Service Dataset                                                          |             | 'PROFILE'
 ajo_email_tracking_experience_event_dataset                      | 672a07c926d57d2aef020230                                                                                     | AJO Email Tracking Experience Event Dataset                  :
                               name                               |                                                  dataSetId                                                   |                                       dataSet                                        | description |        labels        
------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+-------------+----------------------
 ajo_bcc_feedback_event_dataset                                   | 672a07cb7728e82aefa1ec56                                                                                     | AJO BCC Feedback Event Dataset                                                       |             | 
 ajo_classification_dataset                                       | 672a07cab55b0d2aef6f9626                                                                                     | AJO Classification Dataset                                                           |             | 
 ajo_consent_service_dataset                                      | 672a07c80fd5fd2aee4155ca                                                                                     | AJO Consent Service Dataset                                                          |             | 'PROFILE'
 ajo_email_tracking_experience_event_dataset                      | 672a07c926d57d2aef020230                                                                                     | AJO Email Tracking Experience Event Dataset   
```

En los dos puntos, presione la barra espaciadora para ver la siguiente página del conjunto de resultados o escriba `q` para volver al símbolo del sistema.

Cada conjunto de datos de AEP tiene su tabla de servicio de consultas correspondiente. Puede encontrar la tabla de un conjunto de datos a través de la IU de conjuntos de datos:

![ui-dataset-tablename.png](./images/uidatasettablename.png)

La tabla `demo_system_event_dataset_for_website_global_v1_1` es la tabla del servicio de consultas que corresponde con el conjunto de datos `Demo System - Event Schema for Website (Global v1.1)`.

Para consultar información sobre dónde se vio un producto, seleccionaremos la información de **geo**.

Copie la consulta siguiente y péguela en el símbolo del sistema en la **interfaz de línea de comandos PSQL** y pulse Intro:

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

En el resultado de la consulta, verá que las columnas del Modelo de datos de experiencia (XDM) pueden ser tipos complejos y no solo tipos escalares. En la consulta anterior, nos gustaría identificar las ubicaciones geográficas en las que se produjo **commerce.productViews**. Para identificar un **commerce.productViews**, tenemos que navegar por el modelo XDM con **.Notación** (punto).

```text
tech-insiders:all=> select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
                 geo                  
--------------------------------------
 ("(51.59119,-1.407848)",Charlton,GB)
(1 row)
```

¿Observa que el resultado es un objeto plano en lugar de un valor único? El objeto **placecontext.geo** contiene cuatro atributos: schema, country y city. Y cuando un objeto se declara como una columna, devolverá el objeto completo como una cadena. El esquema XDM puede ser más complejo que con lo que está familiarizado, pero es muy potente y se diseñó para admitir muchas soluciones, canales y casos de uso.

Para seleccionar las propiedades individuales de un objeto, utilice **.Notación** (punto).

Copie la instrucción siguiente y péguela en el símbolo del sistema en la **interfaz de línea de comandos PSQL**:

```sql
select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

El resultado de la consulta anterior debería ser similar a este.
El resultado ahora es un conjunto de valores simples:

```text
tech-insiders:all=> select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
 longitude | latitude |   city   | countrycode 
-----------+----------+----------+-------------
 -1.407848 | 51.59119 | Charlton | GB
(1 row)
```

No se preocupe, hay una manera fácil de obtener la ruta hacia una propiedad específica. En la siguiente parte aprenderá cómo hacerlo.

Tendrá que editar una consulta, así que primero vamos a abrir un editor.

En Windows: usar **Bloc de notas**

En Mac: instale cualquier aplicación del Editor de texto que desee y ábrala.

Copie la siguiente instrucción en el editor de texto:

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Vuelva a la interfaz de usuario de Adobe Experience Platform (debe estar abierta en el explorador) o navegue hasta [Adobe Experience Platform](https://experience.adobe.com/platform).

Seleccione **Esquemas**, escriba `Demo System - Event Schema for Website` en el campo **buscar** y haga clic para abrir el esquema `Demo System - Event Schema for Website (Global v1.1) Schema`.

![browse-schema.png](./images/browseschema.png)

Explore el modelo XDM para **Sistema de demostración: esquema de eventos para el sitio web (Global v1.1)**, haciendo clic en un objeto. Expanda el árbol para **placecontext**, **geo** y **schema**. Cuando seleccione el atributo real **longitude**, verá la ruta completa en el cuadro rojo resaltado. Para copiar la ruta del atributo, haga clic en el icono Copiar ruta.

![explore-schema-for-path.png](./images/exploreschemaforpath.png)

Cambie a su bloc de notas/paréntesis y elimine **your_attribute_path_here** de la primera línea. Coloque el cursor después de **seleccionar** en la primera línea y pegue (CTRL-V).

![explore-schema-for-path.png](./images/exploreschemaforpath1.png)

Copie la instrucción modificada y péguela en el símbolo del sistema en la **interfaz de línea de comandos PSQL** y pulse Intro.

El resultado debería ser similar al siguiente:

```text
tech-insiders:all=> select placeContext.geo._schema.longitude
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
 longitude 
-----------
 -1.407848
(1 row)
```

## Pasos siguientes

Ir a [2.1.4 Consultas, consultas, consultas... y análisis de pérdida](./ex4.md){target="_blank"}

Volver a [servicio de consultas](./query-service.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
