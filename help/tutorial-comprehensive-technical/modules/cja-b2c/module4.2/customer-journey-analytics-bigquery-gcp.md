---
title: Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector Source de BigQuery
description: Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector Source de BigQuery
kt: 5342
doc-type: tutorial
exl-id: b078d003-da25-44c5-b000-77e3b3188fb6
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# 4.2 Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector Source de BigQuery

**Autores: [Victor de la Iglesia](https://www.linkedin.com/in/victordelaiglesia/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

En este módulo, configurará su propia instancia de Google Cloud Platform, cargará datos de ejemplo en Google Cloud Platform y, a continuación, utilizará el conector de Source de BigQuery para introducir esos datos de Google Cloud Platform en Adobe Experience Platform. Por último, utilizará Customer Journey Analytics para visualizar esos datos.

Los conectores Source en Adobe Experience Platform facilitan el proceso de introducción de datos en Adobe Experience Platform. Google BigQuery es uno de los conectores ya disponibles. Gracias a Adobe Experience Platform y a BigQuery Source Connector, ahora podemos incorporar datos de Google Analytics a Analysis Workspace en Customer Journey Analytics.

Además, podemos enriquecer esos datos de Google Analytics uniéndolos con otras fuentes de datos como CRM, centro de llamadas o datos de fidelidad dentro de Customer Journey Analytics.

## Objetivos de aprendizaje

- Familiarícese con la interfaz de usuario de Google Cloud Platform y BigQuery
- Ingesta de datos de Google Analytics en Adobe Experience Platform
- Usar Customer Journey Analytics para realizar análisis de los datos de Google Analytics
- Enriquecimiento de datos de Google Analytics con datos sin conexión

## Requisitos previos

- Se prefiere estar algo familiarizado con el Customer Journey Analytics, pero no es obligatorio
- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acceso al Customer Journey Analytics
- Acceso a Google Cloud Platform y Google BigQuery
- **Descargar estos recursos**:
   - [JSON: datos de muestra: datos de fidelización](./../../../assets/json/bqLoyalty.json)

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se hace referencia en [Instalar la extensión de Chrome para la documentación del Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Ejercicios

[4.2.1 Crear su cuenta de Google Cloud Platform](./ex1.md)

Cree su cuenta de Google Cloud Platform.

[4.2.2 Cree su primera consulta en BigQuery](./ex2.md)

Aprenda a utilizar BigQuery para preparar los datos para su carga en Platform.

[4.2.3 Conexión de GCP y BigQuery con Adobe Experience Platform](./ex3.md)

Obtenga información sobre cómo configurar el conector de origen en Adobe Experience Platform.

[4.2.4 Carga de datos de BigQuery en Adobe Experience Platform](./ex4.md)

Obtenga información sobre cómo configurar el conector de origen de BigQuery en Adobe Experience Platform para introducir los datos de los Google Analytics.

[4.2.5 Analizar los datos de los Google Analytics mediante Customer Journey Analytics](./ex5.md)

Obtenga información sobre cómo analizar los datos de los Google Analytics en Customer Journey Analytics y combinarlos con los datos de fidelización.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y descripción general de las ventajas.

>[!NOTE]
>
>Gracias por dedicar su tiempo a aprender todo lo que necesita saber sobre Adobe Experience Platform y sus aplicaciones. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, póngase en contacto directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.

[Volver a todos los módulos](../../../overview.md)
