---
title: Servicio de consultas - Uso del servicio de consultas
description: Servicio de consultas - Uso del servicio de consultas
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: dbf19991-cb09-43cf-887c-52996dfd2986
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# 4.2 Uso del servicio de consulta

## Objetivo

- Buscar y explorar conjuntos de datos
- Obtenga información sobre cómo abordar los objetos y atributos de los modelos de datos de experiencia en las consultas

## Contexto

En esto aprenderá a utilizar PSQL para recuperar información sobre los conjuntos de datos disponibles, a escribir consultas para el Modelo de datos de experiencia (XDM) y a escribir sus primeras consultas de informes simples utilizando los conjuntos de datos Servicio de consultas y Señal de ciudades.

## 4.2.1 Consultas básicas

En esto aprenderá sobre los métodos para recuperar información sobre los conjuntos de datos disponibles y cómo recuperar correctamente datos con una consulta desde un conjunto de datos XDM.

Todos los conjuntos de datos que hemos explorado a través de Adobe Experience Platform a principios de 1 también están disponibles para acceder a través de una interfaz SQL como tablas. Para enumerar esas tablas, puede usar la variable **mostrar tablas;** comando.

Ejecutar **mostrar tablas;** en su **Interfaz de línea de comandos de PSQL**. (no olvide finalizar el comando con un punto y coma).

Copiar el comando **mostrar tablas;** y péguelo en el símbolo del sistema:

![command-quick-show-tables.png](./images/command-prompt-show-tables.png)

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

En los dos puntos, pulse la barra espaciadora para ver la siguiente página del conjunto de resultados o escriba `q` para volver al símbolo del sistema.

Cada conjunto de datos de Platform tiene su tabla de servicio de consulta correspondiente. Puede encontrar la tabla de un conjunto de datos mediante la interfaz de usuario de conjuntos de datos:

![ui-dataset-tablename.png](./images/ui-dataset-tablename.png)

La variable `demo_system_event_dataset_for_website_global_v1_1` es la tabla de servicio de consulta que corresponde a la variable `Demo System - Event Schema for Website (Global v1.1)` conjunto de datos.

Para consultar alguna información sobre dónde se vio un producto, seleccionaremos la variable **geo** información.

Copie la siguiente instrucción y péguela en el símbolo del sistema de su **Interfaz de línea de comandos de PSQL** y pulse intro:

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

En el resultado de la consulta, verá que las columnas del Modelo de datos de experiencia (XDM) pueden ser tipos complejos y no solo escalares. En la consulta anterior, nos gustaría identificar ubicaciones geográficas donde una **commerce.productViews** ocurría. Para identificar un **commerce.productViews** tenemos que navegar por el modelo XDM utilizando el **.** (punto).

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

Observe que el resultado es un objeto plano en lugar de un solo valor? La variable **placecontext.geo** contiene cuatro atributos: esquema, país y ciudad. Y cuando un objeto se declara como una columna, devolverá todo el objeto como una cadena. El esquema XDM puede ser más complejo de lo que está familiarizado, pero es muy potente y se diseñó para admitir muchas soluciones, canales y casos de uso.

Para seleccionar las propiedades individuales de un objeto, utilice el **.** (punto).

Copie la siguiente instrucción y péguela en el símbolo del sistema de su **Interfaz de línea de comandos de PSQL**:

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

El resultado de la consulta anterior debería tener este aspecto.
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

No se preocupe, hay una manera fácil de obtener la ruta hacia una propiedad específica. En la siguiente parte aprenderá cómo.

Tendrá que editar una consulta, así que primero vamos a abrir un editor.

En Windows

Haga clic en el **búsqueda** en la barra de herramientas de windows, escriba **bloc de notas** en el **búsqueda** , haga clic en el botón **bloc de notas** resultado:

![windows-start-notepad.png](./images/windows-start-notepad.png)

En Mac

Instalar [Brackets](https://github.com/adobe/brackets/releases/download/release-1.14/Brackets.Release.1.14.dmg) o utilice otro Editor de texto de su elección si no lo tiene instalado y siga las instrucciones. Después de la instalación, busque **Brackets** mediante la búsqueda destacada de Mac y ábrala.

Copie la siguiente instrucción en el bloc de notas o entre corchetes:

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Vuelva a la interfaz de usuario de Adobe Experience Platform (debe estar abierta en el explorador) o navegue hasta [https://platform.adobe.com](https://platform.adobe.com).

Select **Esquemas**, introduzca `Demo System - Event Schema for Website (Global v1.1)` en el **búsqueda** y seleccione `Demo System - Event Schema for Website (Global v1.1) Schema` de la lista.

![browse-schema.png](./images/browse-schema.png)

Explorar el modelo XDM para **Sistema de demostración: Esquema de eventos para sitio web (Global v1.1)**, haciendo clic en un objeto. Expanda el árbol para **placecontext**, **geo** y **esquema**. Al seleccionar el atributo real **longitude**, verá la ruta completa en el cuadro rojo resaltado. Para copiar la ruta del atributo, haga clic en el icono Copiar ruta.

![explore-schema-for-path.png](./images/explore-schema-for-path.png)

Cambie a su bloc de notas/corchetes y elimine **your_attribute_path_here** de la primera línea. Coloque el cursor después de **select** en la primera línea y pegue (CTRL-V).

Copie la sentencia modificada del bloc de notas/corchetes y péguela en el símbolo del sistema de su **Interfaz de línea de comandos de PSQL** y pulse Intro.

El resultado debería ser como:

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

Paso siguiente: [4.3 Consultas, consultas, consultas... y análisis de pérdida](./ex3.md)

[Volver al módulo 4](./query-service.md)

[Volver a todos los módulos](../../overview.md)
