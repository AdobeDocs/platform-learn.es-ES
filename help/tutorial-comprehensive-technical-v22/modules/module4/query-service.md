---
title: Servicio de consultas
description: Servicio de consultas
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 74943e52-8a7e-4db7-9407-7deeab008fa7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---

# 4. Servicio de consultas

**Autores: [Métricas de Marc](https://www.linkedin.com/in/marcmeewis/), [WOutside Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

En este módulo, obtendrá una vista previa práctica del servicio de consulta de Adobe Experience Platform. El servicio de consulta le permite realizar consultas de canales múltiples en todos los datos de aplicaciones de Adobe Experience Cloud, uniendo y analizando datos de Adobe Campaign, Analytics, Audience Manager, Target, Advertising Cloud y otros datos de clientes cargados o insertados en Adobe Experience Platform.

El servicio de consultas es una herramienta sin servidor. Admite consultas SQL y conectividad desde varias aplicaciones cliente a través de su compatibilidad PostgreSQL.
Utilizaremos datos que se hayan insertado en la plataforma mediante datos de interacción web e interacciones del centro de llamadas en combinación con datos de lealtad del cliente cargados en la plataforma.

## Objetivos de aprendizaje

- Familiarícese con la interfaz de usuario de Adobe Experience Platform
- Conectarse al servicio de consulta y ejecutar las consultas SQL
- Explorar conjuntos de datos en Adobe Experience Platform
- Conecte Tableau o Power BI al servicio de consulta de Adobe Experience Platform para crear visualizaciones e informes

## Requisitos previos

- Se prefiere cierta familiaridad con SQL, pero no es necesario
- Acceso a Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Conjuntos de datos (conjuntos de datos utilizados durante el laboratorio, precargados para usted)
- PostgreSQL
- Tableau o Microsoft Power BI Desktop
- **Descargar estos recursos**:
   - [JSON: Datos de muestra: Interacciones de sitios web](./../../assets/json/ee.json)
   - [JSON: Datos de muestra: Interacciones del centro de llamadas](./../../assets/json/callcenter.json)
   - [JSON: Datos de muestra: Fidelidad](./../../assets/json/loyalty.json)

>[!IMPORTANT]
>
>Este tutorial se creó para facilitar un formato de taller concreto. Utiliza sistemas y cuentas específicos a los que es posible que no tenga acceso. Incluso sin acceso, creemos que aún puede aprender mucho leyendo este contenido muy detallado. Si participa en uno de los talleres y necesita sus credenciales de acceso, póngase en contacto con el representante del Adobe, que le proporcionará la información necesaria.

## Información general sobre la arquitectura

Eche un vistazo a la siguiente arquitectura, que resalta los componentes que se discutirán y utilizarán en este módulo.

![Información general sobre la arquitectura](../../assets/images/architecturem7.png)

## Espacio aislado para usar

Para este módulo, utilice este simulador de pruebas: `--module7sandbox--`.

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se indica en [0.1: Instalar la extensión de Chrome para la documentación del Experience League](../module0/ex1.md)

## Ejercicios

[4.0 Requisitos previos](./ex0.md)

Deberá instalar PSQL para ejecutar las consultas en este ejercicio de habilitación. En función de su sistema operativo, deberá instalar Microsoft Power BI o Tableau. Los usuarios de Windows pueden elegir entre Power BI o Tableau. Los usuarios de Mac deben instalar Tableau.

[4.1 Introducción](./ex1.md)

En este ejercicio, explorará la interfaz de usuario del servicio de consulta de Adobe Experience Platform, obtendrá información sobre los conjuntos de datos, encontrará sus consultas y, finalmente, configurará una conexión desde PSQL.

[4.2 Uso del servicio de consulta](./ex2.md)

En este ejercicio, aprenderá sobre la sintaxis básica del servicio de consulta y podrá identificar los atributos del esquema XDM en la consulta.

[4.3 Consultas, consultas, consultas... y análisis de pérdida](./ex3.md)

En este ejercicio realizará consultas, aprenderá sobre las funciones definidas por Adobe mientras realiza análisis de pérdida. Al final de esto, escribirá una consulta para preparar un conjunto de datos para su uso en Microsoft Power BI.

[4.4 Generar un conjunto de datos a partir de una consulta](./ex4.md)

En este ejercicio, generará un conjunto de datos a partir de una consulta ejecutada en el anterior y utilizará este conjunto de datos en los próximos ejercicios.

[4.5 Servicio y Power BI de consultas](./ex5.md)

En este ejercicio, debe conectar el Power BI a Adobe Experience Platform y el servicio de consulta para realizar el análisis de interacción de Callcenter.

[4.6 Servicio de Consulta y Tableau](./ex6.md)

En este ejercicio, debe conectar Tableau a Adobe Experience Platform y Query Service para realizar el análisis de interacción de Callcenter.

[API del servicio de consulta 4.7](./ex7.md)

En este ejercicio, utilizará la API del servicio de consulta para administrar las plantillas de consulta y las programaciones de consultas.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y visión general de los beneficios.

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.

[Volver a todos los módulos](../../overview.md)
