---
title: 'Servicio de consulta: explorar el conjunto de datos con Power BI'
description: 'Servicio de consulta: explorar el conjunto de datos con Power BI'
kt: 5342
doc-type: tutorial
exl-id: f1125d91-2fe6-456c-9d4a-802e3f288fc0
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 2.1.6 Servicio de consultas y Power BI

Abra Microsoft Power BI Desktop.

![start-power-bi.png](./images/startpowerbi.png)

Haga clic en **Obtener datos**.

![power-bi-get-data.png](./images/powerbigetdata.png)

Busca **postgres** (1), selecciona **Postgres** (2) de la lista y **Conecta** (3).

![power-bi-connect-progress.png](./images/powerbiconnectprogress.png)

Vaya a Adobe Experience Platform, **Consultas** y **Credenciales**.

![query-service-credentials.png](./images/queryservicecredentials.png)

En la página **Credenciales** de Adobe Experience Platform, copie el **host** y péguelo en el campo **Servidor**, copie la **Base de datos** y péguela en el campo **Base de datos** de PowerBI. A continuación, haga clic en Aceptar (2).

>[!IMPORTANT]
>
>Asegúrese de incluir el puerto **:80** al final del valor del servidor porque el servicio de consultas no utiliza actualmente el puerto PostgreSQL predeterminado de 5432.

![power-bi-connect-server.png](./images/powerbiconnectserver.png)

En el siguiente cuadro de diálogo, rellene el Nombre de usuario y la Contraseña con su Nombre de usuario y Contraseña que se encuentran en las **Credenciales** de Consultas en Adobe Experience Platform.

![query-service-credentials.png](./images/queryservicecredentials.png)

En el cuadro de diálogo Navegador, coloque su **LDAP** en el campo de búsqueda (1) para localizar los conjuntos de datos de CTAS y marque la casilla junto a cada uno (2). Luego haga clic en Load (3).

![power-bi-load-churn-data.png](./images/powerbiloadchurndata.png)

Asegúrese de que la ficha **Informe** (1) esté seleccionada.

![power-bi-report-tab.png](./images/powerbireporttab.png)

Seleccione el mapa (1) y después de añadirlo al lienzo de informes, amplíe el mapa (2).

![power-bi-select-map.png](./images/powerbiselectmap.png)

A continuación, debemos definir las medidas y las dimensiones; para ello, arrastre los campos de la sección **fields** a los marcadores de posición correspondientes (ubicados en **visualizaciones**), como se indica a continuación:

![power-bi-drag-lat-lon.png](./images/powerbidraglatlon.png)

Como medida, usaremos un recuento de **customerId**. Arrastre el campo **crmid** de la sección **fields** al marcador de posición **Size**:

![power-bi-drag-crmid.png](./images/powerbidragcrmid.png)

Por último, para realizar algún análisis de **callTopic**, vamos a arrastrar el campo **callTopic** al marcador de posición **Filtros de nivel de página** (es posible que tenga que desplazarse en la sección **visualizaciones**);

![power-bi-drag-calltopic.png](./images/powerbidragcalltopic.png)

Seleccione o anule la selección de **callTopics** para investigar:

![power-bi-report-select-calltopic.png](./images/powerbireportselectcalltopic.png)

Ya ha terminado este ejercicio.

## Pasos siguientes

Ir a [2.1.8 API de servicio de consultas](./ex8.md){target="_blank"}

Volver a [servicio de consultas](./query-service.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
