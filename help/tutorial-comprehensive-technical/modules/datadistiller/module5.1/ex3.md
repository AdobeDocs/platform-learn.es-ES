---
title: 'Servicio de consultas: uso del servicio de consultas'
description: 'Servicio de consultas: uso del servicio de consultas'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
exl-id: 31c14a9b-cb62-48ab-815c-caa6e832794f
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# 5.1.3 Uso del servicio de consultas

## Objetivo

- Buscar y explorar conjuntos de datos
- Obtenga información sobre cómo abordar objetos y atributos de modelos de datos de experiencia en las consultas

## Contexto

En este vídeo aprenderá a utilizar PSQL para recuperar información sobre los conjuntos de datos disponibles, a escribir consultas para el modelo de datos de experiencia (XDM) y a escribir sus primeras consultas de creación de informes simples con los conjuntos de datos del servicio de consulta y de Citi Signal.

## Consultas básicas

En este vídeo aprenderá acerca de los métodos para recuperar información sobre los conjuntos de datos disponibles y cómo recuperar correctamente datos con una consulta de un conjunto de datos XDM.

Todos los conjuntos de datos que hemos explorado a través de Adobe Experience Platform al principio de 1, también están disponibles para el acceso a través de una interfaz SQL como tablas. Para enumerar esas tablas, puede usar el comando **show tables;**.

Ejecute **mostrar tablas;** en su **interfaz de línea de comandos PSQL**. (no olvide terminar el comando con un punto y coma).

Copie el comando **show tables;** y péguelo en el símbolo del sistema:

![command-prompt-show-tables.png](./images/command-prompt-show-tables.png)

Verá el siguiente resultado:

```text
aepenablementfy21:all=> show tables;
                            name                            |        dataSetId         |                            dataSet                             | description | resolved 
------------------------------------------------------------+--------------------------+----------------------------------------------------------------+-------------+----------
 demo_system_event_dataset_for_call_center_global_v1_1      | 5fd1a9dea30603194baeea43 | Demo System - Event Dataset for Call Center (Global v1.1)      |             | false
 demo_system_event_dataset_for_mobile_app_global_v1_1       | 5fd1a9de250e4f194bec84cd | Demo System - Event Dataset for Mobile App (Global v1.1)       |             | false
 demo_system_event_dataset_for_voice_assistants_global_v1_1 | 5fd1a9de49ee76194b85f73c | Demo System - Event Dataset for Voice Assistants (Global v1.1) |             | false
 demo_system_event_dataset_for_website_global_v1_1          | 5fd1a9dee3224d194cdfe786 | Demo System - Event Dataset for Website (Global v1.1)          |             | false
 demo_system_profile_dataset_for_loyalty_global_v1_1        | 5fd1a9de250e4f194bec84cc | Demo System - Profile Dataset for Loyalty (Global v1.1)        |             | false
 demo_system_profile_dataset_for_ml_predictions_global_v1_1 | 5fd1a9de241f58194b0cb117 | Demo System - Profile Dataset for ML Predictions (Global v1.1) |             | false
 demo_system_profile_dataset_for_mobile_app_global_v1_1     | 5fd1a9deddf353194a2e00b7 | Demo System - Profile Dataset for Mobile App (Global v1.1)     |             | false
 demo_system_profile_dataset_for_website_global_v1_1        | 5fd1a9de42a61c194dd7b810 | Demo System - Profile Dataset for Website (Global v1.1)        |             | false
 journey_step_events                                        | 5fd1a7f30268c5194bbb7e5e | Journey Step Events                                            |             | false
```

En los dos puntos, presione la barra espaciadora para ver la siguiente página del conjunto de resultados o escriba `q` para volver al símbolo del sistema.

Cada conjunto de datos de Platform tiene su tabla de servicio de consultas correspondiente. Puede encontrar la tabla de un conjunto de datos a través de la interfaz de usuario Conjuntos de datos:

![ui-dataset-tablename.png](./images/ui-dataset-tablename.png)

La tabla `demo_system_event_dataset_for_website_global_v1_1` es la tabla del servicio de consultas que corresponde con el conjunto de datos `Demo System - Event Schema for Website (Global v1.1)`.

Para consultar información sobre dónde se vio un producto, seleccionaremos la información de **geo**.

Copie la instrucción siguiente, péguela en el símbolo del sistema en la **interfaz de línea de comandos PSQL** y pulse Intro:

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

En el resultado de la consulta, verá que las columnas del Modelo de datos de experiencia (XDM) pueden ser tipos complejos y no solo tipos escalares. En la consulta anterior, nos gustaría identificar las ubicaciones geográficas en las que se produjo **commerce.productViews**. Para identificar un **commerce.productViews**, tenemos que navegar por el modelo XDM con **.Notación** (punto).

```text
aepenablementfy21:all=> select placecontext.geo
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
                  geo                   
----------------------------------------
 ("(57.4694803,-3.1269422)",Tullich,GB)
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
aepenablementfy21:all=> select placecontext.geo._schema.longitude
aepenablementfy21:all->       ,placecontext.geo._schema.latitude
aepenablementfy21:all->       ,placecontext.geo.city
aepenablementfy21:all->       ,placecontext.geo.countryCode
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  |  latitude  |  city   | countrycode 
------------+------------+---------+-------------
 -3.1269422 | 57.4694803 | Tullich | GB
(1 row)
```

No se preocupe, hay una manera fácil de obtener la ruta hacia una propiedad específica. En la siguiente parte aprenderá cómo hacerlo.

Tendrá que editar una consulta, así que primero vamos a abrir un editor.

En Windows

Haga clic en el icono **search** de la barra de herramientas de Windows, escriba **notepad** en el campo **search** y haga clic en el resultado **notepad**:

![windows-start-notepad.png](./images/windows-start-notepad.png)

En Mac

Instale [Brackets](https://github.com/adobe/brackets/releases/download/release-1.14/Brackets.Release.1.14.dmg) o use otro editor de texto de su elección si no lo tiene instalado y siga las instrucciones. Después de la instalación, busca **Brackets** mediante la búsqueda destacada de Mac y ábrelo.

Copie la instrucción siguiente en el bloc de notas o entre corchetes:

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Vuelva a la interfaz de usuario de Adobe Experience Platform (debe estar abierta en el explorador) o navegue hasta [https://platform.adobe.com](https://platform.adobe.com).

Seleccione **Esquemas**, escriba `Demo System - Event Schema for Website (Global v1.1)` en el campo **buscar** y seleccione `Demo System - Event Schema for Website (Global v1.1) Schema` de la lista.

![browse-schema.png](./images/browse-schema.png)

Explore el modelo XDM para **Sistema de demostración: esquema de eventos para el sitio web (Global v1.1)**, haciendo clic en un objeto. Expanda el árbol para **placecontext**, **geo** y **schema**. Cuando seleccione el atributo real **longitude**, verá la ruta completa en el cuadro rojo resaltado. Para copiar la ruta del atributo, haga clic en el icono Copiar ruta.

![explore-schema-for-path.png](./images/explore-schema-for-path.png)

Cambie a su bloc de notas/paréntesis y elimine **your_attribute_path_here** de la primera línea. Coloque el cursor después de **seleccionar** en la primera línea y pegue (CTRL-V).

Copie la instrucción modificada del bloc de notas/corchetes, péguela en el símbolo del sistema en la **interfaz de línea de comandos de PSQL** y presione Intro.

El resultado debería ser similar al siguiente:

```text
aepenablementfy21:all=> select placeContext.geo._schema.longitude
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  
------------
 -3.1269422
```

Paso siguiente: [5.1.4 Consultas, consultas, consultas... y análisis de pérdida](./ex4.md)

[Volver al módulo 5.1](./query-service.md)

[Volver a todos los módulos](../../../overview.md)
