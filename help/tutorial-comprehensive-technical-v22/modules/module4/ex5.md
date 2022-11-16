---
title: 'Servicio de consulta: Explore el conjunto de datos con Power BI'
description: 'Servicio de consulta: Explore el conjunto de datos con Power BI'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 0f9e6719-056b-4858-8c86-04b3beaa950e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 4.5 Servicio y Power BI de consultas

Abra Microsoft Power BI Desktop.

![start-power-bi.png](./images/start-power-bi.png)

Haga clic en **Obtener datos**.

![power-bi-get-data.png](./images/power-bi-get-data.png)

Buscar **postgres** (1), seleccione **Postgres** (2) de la lista y **Connect** (3)

![power-bi-connect-progress.png](./images/power-bi-connect-progress.png)

Vaya a Adobe Experience Platform, para **Consultas** y **Credenciales**.

![query-service-credentials.png](./images/query-service-credentials.png)

En el **Credenciales** en Adobe Experience Platform, copie la **Host** y péguelo en el **Servidor** y copie el **Base de datos** y péguelo en el **Base de datos** en Power BI y, a continuación, haga clic en Aceptar (2).

>[!IMPORTANT]
>
>Asegúrese de incluir el puerto **:80** al final del valor Server porque el servicio de consulta no utiliza actualmente el puerto predeterminado PostgreSQL de 5432.

![power-bi-connect-server.png](./images/power-bi-connect-server.png)

En el siguiente cuadro de diálogo, rellene el Nombre de usuario y la Contraseña con el Nombre de usuario y la Contraseña que se encuentran en la **Credenciales** de consultas en Adobe Experience Platform.

![query-service-credentials.png](./images/query-service-credentials.png)

En el cuadro de diálogo Navegador, ponga su **LDAP** en el campo de búsqueda (1) para localizar sus conjuntos de datos de CTAS y marque la casilla junto a cada (2). A continuación, haga clic en Cargar (3).

![power-bi-load-churn-data.png](./images/power-bi-load-churn-data.png)

Asegúrese de que la variable **Informe** (1).

![power-bi-report-tab.png](./images/power-bi-report-tab.png)

Seleccione el mapa (1) y después de añadirlo al lienzo de informes, amplíe el mapa (2).

![power-bi-select-map.png](./images/power-bi-select-map.png)

A continuación, es necesario definir las medidas y las dimensiones; para ello, debe arrastrar los campos desde el **campos** en los marcadores de posición correspondientes (ubicados en **visualizaciones**) como se indica a continuación:

![power-bi-arrastre-lat-lon.png](./images/power-bi-drag-lat-lon.png)

Como medida, utilizaremos un recuento de **customerId**. Arrastre el **crmid** del campo **campos** en la sección **Tamaño** marcador de posición:

![power-bi-arrastrar-crmid.png](./images/power-bi-drag-crmid.png)

Finalmente, para hacer algunas **callTopic** análisis, vamos a arrastrar el **callTopic** en el campo **Filtros de nivel de página** marcador de posición (es posible que tenga que desplazarse en la **visualizaciones** sección);

![power-bi-arrastre-calltopic.png](./images/power-bi-drag-calltopic.png)

Seleccionar/anular selección **callTopics** para investigar:

![power-bi-report-select-calltopic.png](./images/power-bi-report-select-calltopic.png)

Ya has terminado este ejercicio.

Paso siguiente: [API del servicio de consulta 4.7](./ex7.md)

[Volver al módulo 4](./query-service.md)

[Volver a todos los módulos](../../overview.md)
