---
title: Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector de origen BigQuery
description: Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector de origen BigQuery
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c9c28b5a-d158-49fa-9533-1a295876f6c4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 3%

---

# 12. Ingesta y análisis de datos de Google Analytics en Adobe Experience Platform con el conector de origen BigQuery

**Autores: [Victor de la Iglesia](https://www.linkedin.com/in/victordelaiglesia/), [WOutside Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

En este módulo, debe configurar su propia instancia de Google Cloud Platform, cargar datos de muestra en Google Cloud Platform y, a continuación, utilizar el conector de origen BigQuery para introducir esos datos de Google Cloud Platform en Adobe Experience Platform. Por último, utilizará Customer Journey Analytics para visualizar esos datos.

Los conectores de origen en Adobe Experience Platform facilitan el proceso de obtención de datos en Adobe Experience Platform. Google BigQuery es uno de los conectores ya disponibles. Gracias a Adobe Experience Platform y al conector de origen BigQuery ahora podemos incorporar datos de Google Analytics a Analysis Workspace en Customer Journey Analytics.

Además, podemos enriquecer los datos de ese Google Analytics uniéndolos a otras fuentes de datos como CRM, Call Center o datos de fidelidad dentro de Customer Journey Analytics.

## Objetivos de aprendizaje

- Familiarícese con la interfaz de usuario de Google Cloud Platform y BigQuery
- Ingesta de datos de Google Analytics en Adobe Experience Platform
- Usar el Customer Journey Analytics para realizar un análisis de los datos de los Google Analytics
- Enriquecimiento de los datos de los Google Analytics con datos sin conexión

## Requisitos previos

- Se prefiere cierta familiaridad con el Customer Journey Analytics, pero no es necesario
- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Acceso a Customer Journey Analytics
- Acceso a Google Cloud Platform y Google BigQuery
- **Descargar estos recursos**:
   - [JSON: Datos de muestra: Datos de fidelidad](./../../assets/json/bqLoyalty.json)

>[!IMPORTANT]
>
>Este tutorial se creó para facilitar un formato de taller concreto. Utiliza sistemas y cuentas específicos a los que es posible que no tenga acceso. Incluso sin acceso, creemos que aún puede aprender mucho leyendo este contenido muy detallado. Si participa en uno de los talleres y necesita sus credenciales de acceso, póngase en contacto con el representante del Adobe, que le proporcionará la información necesaria.

## Información general sobre la arquitectura

Eche un vistazo a la siguiente arquitectura, que resalta los componentes que se discutirán y utilizarán en este módulo.

![Información general sobre la arquitectura](../../assets/images/architecturem16.png)

## Espacio aislado para usar

Para este módulo, utilice este simulador de pruebas: `--aepSandboxId--`.

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se indica en [0.1: Instalar la extensión de Chrome para la documentación del Experience League](../module0/ex1.md)

## Ejercicios

[12.1 Cree su cuenta de Google Cloud Platform](./ex1.md)

Cree su cuenta de Google Cloud Platform.

[12.2 Crear la primera consulta en BigQuery](./ex2.md)

Aprenda a utilizar BigQuery para preparar los datos para su carga en Platform.

[12.3 Conectar GCP y BigQuery a Adobe Experience Platform](./ex3.md)

Obtenga información sobre cómo configurar el conector de origen en Adobe Experience Platform.

[12.4 Cargar datos de BigQuery en Adobe Experience Platform](./ex4.md)

Aprenda a configurar el conector de origen BigQuery en Adobe Experience Platform para introducir los datos de sus Google Analytics.

[12.5 Analizar los datos de los Google Analytics mediante el Customer Journey Analytics](./ex5.md)

Obtenga información sobre cómo analizar los datos de Google Analytics en Customer Journey Analytics y combinarlos con datos de fidelidad.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y visión general de los beneficios.

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.

[Volver a todos los módulos](../../overview.md)
