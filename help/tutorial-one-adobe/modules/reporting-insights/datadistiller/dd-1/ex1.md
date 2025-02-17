---
title: 'Servicio de consultas: requisitos previos'
description: 'Servicio de consultas: requisitos previos'
kt: 5342
doc-type: tutorial
exl-id: e9e4d478-cb8d-42a9-87a3-319e5a8b8522
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# 2.1.1 Requisitos previos

## Instalar la utilidad de línea de comandos PSQL

Siga las instrucciones descritas en la documentación de Adobe Experience Platform para instalar el cliente psql:
[Guía de instalación de PSQL](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html)

Una vez que haya instalado PSQL, es posible que tenga que actualizar **PATH** ejecutando el siguiente comando en una ventana de terminal:

Para macOS (reemplace XX en el siguiente comando por el número de versión de PSQL que instaló):

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## Instalación de Power BI

Solo para usuarios de Windows

[Instalar Microsoft Power BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html)

Asegúrese de instalar la versión exacta de **npgsql** tal como se menciona en el documento; de lo contrario, no podrá conectar Power BI al servicio de consultas de Adobe Experience Platform.

## Instalar Tableau

Para usuarios de Windows o Mac

[Instalar Tableau Desktop](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html) según la documentación.

Tableau le da un período de prueba de 14 días automáticamente.

Si desea utilizar Tableau más allá de esos 14 días, necesitará una clave de licencia.

## Pasos siguientes

Ir a [2.1.2 Introducción](./ex2.md){target="_blank"}

Volver a [servicio de consultas](./query-service.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
