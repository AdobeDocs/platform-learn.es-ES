---
title: Composición de audiencia federada Arquitectura y flujo de alto nivel
seo-title: Federated Audience Composition high-level architecture & flow | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Flujo y arquitectura de alto nivel de composición de audiencia federada
description: Descripción general de la arquitectura de alto nivel y del flujo de Composición de audiencias federada.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-high-level-architecture.jpg
exl-id: 4cb0b730-4206-476b-93d9-776dfbd464ff
source-git-commit: 0564f516cfba7ea09ac9da19d94f46d984e9e00a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Flujo y arquitectura de alto nivel de composición de audiencia federada

Antes de sumergirnos en los pasos para dar soporte al escenario comercial de SecurFinancial, revisaremos la arquitectura de alto nivel y el flujo para este enfoque de CDP componible.

El módulo Federated Audience Composition de Adobe Experience Platform amplía el acceso a los conjuntos de datos del Data Warehouse sin copiar los datos subyacentes, lo que minimiza el movimiento y la duplicación de datos.

Esto también proporciona a las organizaciones la arquitectura Composable necesaria, que ya han completado el trabajo de administración de datos necesario en su almacén y desean utilizar un patrón de copia cero en el que Adobe Experience Platform se convierta en el motor de participación.

Permite a las empresas procesar rápidamente la información almacenada en uno o más almacenes de datos. Esto elimina la necesidad de introducir datos en Adobe Experience Platform. Además, proporciona acceso a nuevos conjuntos de datos que residen en almacenes de datos empresariales, pero que hasta ahora no han sido accesibles para los flujos de trabajo de experiencia del cliente. Algunos ejemplos son transacciones históricas o datos personales que serán útiles a nivel de audiencia agregada para la participación de los clientes.

![fac-Architecture](assets/fac-architecture.png)

Ahora pasaremos a crear una [conexión de Data Warehouse](data-warehouse-connection.md).
