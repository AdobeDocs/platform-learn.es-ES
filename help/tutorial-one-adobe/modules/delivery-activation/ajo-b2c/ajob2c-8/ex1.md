---
title: Configuración de la base de datos relacional
description: Configuración de la base de datos relacional
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: bf3bebfa3bd79829da5352e950aed3f4ef5bf6d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 6%

---

# 3.8.1 Configuración de la base de datos relacional

Inicie sesión en Adobe Journey Optimizer en [https://experience.adobe.com](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![AJO OC](./images/aechome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`.

![AJO OC](./images/ajohome.png)

## 3.8.1.1 configuración de esquema basado en relaciones

Un esquema basado en relaciones es la definición formal del modelo de datos basado en modelos.

Especifica lo siguiente:

- El conjunto de tablas
- Las columnas de cada tabla
- Las restricciones
- Las relaciones entre tablas

La organización de esquemas o tablas en un modelo de datos basado en modelos consiste en estructurar los datos en varias tablas. Asegúrese de que cada tabla almacene un tipo de entidad/esquemas.

Al ingerir datos en para utilizarlos con Adobe Journey Optimizer Orchestrated Campaigns, están disponibles las siguientes fuentes:

- Amazon S3
- Almacenamiento en la nube de Google
- SFTP
- Snowflake
- Google BigQuery
- Zona de aterrizaje de datos
- Azure Databricks
- Carga de archivo local

El primer paso de este ejercicio es la configuración de los esquemas XDM basados en relaciones. En el menú de la izquierda, desplácese hacia abajo hasta **Administración de datos** y seleccione **Esquemas**. Haga clic en **+ Crear esquema**.

![AJO OC](./images/ajoocdata1.png)

Seleccione **Relacional**.

![AJO OC](./images/ajoocdata2.png)

Seleccione **Cargar archivo DDL** y haga clic en **Elegir archivos**.

![AJO OC](./images/ajoocdata3.png)

Ahora que los esquemas XDM relacionales están configurados y con los datos que se están ingiriendo, puede empezar a utilizar esos datos para crear la campaña orquestada en el siguiente ejercicio.

## 3.8.1.2 Ingesta de datos


## Pasos siguientes

Vaya a [Crear su campaña orquestada](./ex2.md){target="_blank"}

Volver a [Adobe Journey Optimizer: Campaigns](./ajocampaigns.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
