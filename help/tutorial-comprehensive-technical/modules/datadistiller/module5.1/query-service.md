---
title: Servicio de consultas
description: Servicio de consultas
kt: 5342
doc-type: tutorial
exl-id: 6eb65de3-d0e8-49d4-a702-5c9d6a1952b7
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 5.1 Servicio de consultas

En este módulo, obtendrá una vista previa práctica del servicio de consultas de Adobe Experience Platform. Query Service permite realizar consultas omnicanal en todos los datos de las aplicaciones de Adobe Experience Cloud, combinando y analizando datos en Adobe Campaign, Analytics, Audience Manager, Target, Advertising Cloud y otros datos de clientes cargados o insertados en Adobe Experience Platform.

El servicio de consultas es una herramienta sin servidor. Admite consultas SQL y conectividad desde varias aplicaciones cliente a través de su compatibilidad con PostgreSQL.
Utilizaremos datos que se hayan insertado en la plataforma mediante datos de interacción web e interacciones del centro de llamadas en combinación con datos de lealtad del cliente cargados en la plataforma.

## Objetivos de aprendizaje

- Familiarícese con la IU de Adobe Experience Platform
- Conéctese al servicio de consultas y ejecute sus consultas SQL
- Exploración de conjuntos de datos en Adobe Experience Platform
- Conecte Tableau o Power BI al servicio de consultas de Adobe Experience Platform para crear visualizaciones e informes

## Requisitos previos

- Se prefiere estar algo familiarizado con SQL, pero no es obligatorio
- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Conjuntos de datos (conjunto de datos utilizado durante el laboratorio, precargado para usted)
- PostgreSQL
- Tableau o Microsoft Power BI Desktop
- **Descargar estos recursos**:
   - [JSON: datos de muestra: interacciones con el sitio web](./../../../assets/json/ee.json)
   - [JSON: datos de muestra: interacciones del centro de llamadas](./../../../assets/json/callcenter.json)
   - [JSON: datos de muestra: lealtad](./../../../assets/json/loyalty.json)

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se hace referencia en [Instalar la extensión de Chrome para la documentación del Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Ejercicios

[5.1.1 Requisitos previos](./ex1.md)

Deberá instalar PSQL para ejecutar las consultas en este ejercicio de habilitación. Según el sistema operativo, tendrá que instalar Microsoft Power BI o Tableau. Los usuarios de Windows pueden elegir entre Power BI o Tableau. Los usuarios de Mac deben instalar Tableau.

[5.1.2 Introducción](./ex2.md)

En este ejercicio explorará la interfaz de usuario del servicio de consultas de Adobe Experience Platform, obtendrá información sobre los conjuntos de datos, buscará sus consultas y, finalmente, configurará una conexión desde PSQL.

[5.1.3 Uso del servicio de consultas](./ex3.md)

En este ejercicio aprenderá sobre la sintaxis básica del servicio de consultas y podrá identificar los atributos del esquema XDM en su consulta.

[5.1.4 Consultas, consultas, consultas, análisis de pérdida](./ex4.md)

En este ejercicio va a realizar consultas y aprenderá sobre las funciones definidas por Adobe mientras realiza análisis de pérdida. Al final de esto, escribirá una consulta para preparar un conjunto de datos para utilizarlo en Microsoft Power BI.

[5.1.5 Generar un conjunto de datos a partir de una consulta](./ex5.md)

En este ejercicio, se genera un conjunto de datos a partir de una consulta ejecutada en el ejercicio anterior y se utiliza este conjunto de datos en los ejercicios siguientes.

[5.1.6 Servicio de consultas y Power BI](./ex6.md)

En este ejercicio, conectará Power BI a Adobe Experience Platform y Query Service para realizar el análisis de interacción del centro de llamadas.

[5.1.7 Servicio de consultas y Tableau](./ex7.md)

En este ejercicio, conectará Tableau a Adobe Experience Platform y Query Service para realizar el análisis de interacción del centro de llamadas.

[5.1.8 API del servicio de consultas](./ex8.md)

En este ejercicio utilizará la API del servicio de consulta para administrar las plantillas de consulta y las programaciones de consultas.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y descripción general de las ventajas.

>[!NOTE]
>
>Gracias por dedicar su tiempo a aprender todo lo que necesita saber sobre Adobe Experience Platform y sus aplicaciones. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, póngase en contacto directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.

[Volver a todos los módulos](../../../overview.md)
