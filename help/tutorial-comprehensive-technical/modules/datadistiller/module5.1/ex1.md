---
title: 'Servicio de consultas: requisitos previos'
description: 'Servicio de consultas: requisitos previos'
kt: 5342
doc-type: tutorial
exl-id: b8a404d1-7796-46e3-b245-553acdc753ae
source-git-commit: d9d9a38c1e160950ae755e352a54667c8a7b30f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 5.1.1 Requisitos previos

## Instalar la utilidad de línea de comandos PSQL

Siga las instrucciones descritas en la documentación de Adobe Experience Platform para instalar el cliente psql:
[Guía de instalación de PSQL](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html?lang=es)

Una vez que haya instalado PSQL, es posible que tenga que actualizar **PATH** ejecutando el siguiente comando en una ventana de terminal:

Para macOS (reemplace XX en el siguiente comando por el número de versión de PSQL que instaló):

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## Instalar Power BI

Solo para usuarios de Windows

[Instalar Microsoft Power BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html?lang=es)

Asegúrese de instalar la versión exacta de **npgsql** tal como se menciona en el documento; de lo contrario, no podrá conectar Power BI al servicio de consultas de Adobe Experience Platform.

## Instalar Tableau

Para usuarios de Windows o Mac

[Instalar Tableau Desktop](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html?lang=es) según la documentación.

Tableau le da un período de prueba de 14 días automáticamente.

Si desea utilizar Tableau más allá de esos 14 días, necesitará una clave de licencia.

Siguiente Paso: [5.1.2 Introducción](./ex2.md)

[Volver al módulo 5.1](./query-service.md)

[Volver a todos los módulos](../../../overview.md)
