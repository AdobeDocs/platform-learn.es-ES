---
title: 'Servicio de consulta: Explore el conjunto de datos con Tableau'
description: 'Servicio de consulta: Explore el conjunto de datos con Tableau'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 04209eb4-b054-4a2e-885e-61f601c3fc2c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 4.6 Servicio de Consulta y Tableau

Abra Tableau.

![start-tableau.png](./images/start-tableau.png)

En **Conexión a un servidor** select **PostgreSQL**:

![tableau-connect-postgress.png](./images/tableau-connect-postgress.png)

Vaya a Adobe Experience Platform, para **Consultas** y **Credenciales**.

![query-service-credentials.png](./images/query-service-credentials.png)

En el **Credenciales** en Adobe Experience Platform, copie la **Host** y péguelo en el **Servidor** , copie el **Base de datos** y péguelo en el **Base de datos** en Tableau, copie el **Puerto** y péguelo en el campo **Puerto** en Tableau, haga lo mismo para **Nombre de usuario** y **Contraseña**. A continuación, haga clic en **Iniciar sesión**.

Iniciar sesión:

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

Haga clic en buscar (1) e introduzca su **ldap** en el campo de búsqueda, identifique la tabla del conjunto de resultados y arrástrela (3) a la ubicación denominada **Arrastrar tablas aquí**. Cuando termine, haga clic en **Hoja 1** (3)

![tableau-arrastre-table.png](./images/tableau-drag-table.png)

Para visualizar nuestros datos en el mapa necesitamos convertir la longitud y la latitud a dimensiones. En **Medidas** select **Latitud** (1) y abra el menú desplegable del campo y seleccione **Convertir en Dimension** (2) Haga lo mismo para la variable **Longitud** medida.

![tableau-converted-dimension.png](./images/tableau-convert-dimension.png)

Arrastre el **Longitud** a la **Columnas** y **Latitud** medir a **Filas**. Asignación automática de **Bélgica** aparecerán con pequeños puntos que representan las ciudades en el conjunto de datos.

![tableau-arrastre-lon-lat.png](./images/tableau-drag-lon-lat.png)

Select **Nombres de medida** (1), abra el menú desplegable y seleccione **Agregar a hoja** (2):

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

Ahora tendrá un mapa, con puntos de varios tamaños. El tamaño indica el número de interacciones del centro de llamadas para esa ciudad específica. Para variar el tamaño de los puntos, vaya al panel derecho y abra **Valores de medida** (con el icono desplegable ). En la lista desplegable , seleccione **Editar tamaños**. Juegue con diferentes tamaños.

![tableau-vary-size-dots.png](./images/tableau-vary-size-dots.png)

Para mostrar más los datos por **Tema de llamada**, arrastre (1) el **Tema de llamada** dimensión a **Páginas**. Navegar por los distintos **Temas de llamada** usando la variable **Tema de llamada** (2) en el lado derecho de la pantalla:

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

Ya has terminado este ejercicio.

Paso siguiente: [API del servicio de consulta 4.7](./ex7.md)

[Volver al módulo 4](./query-service.md)

[Volver a todos los módulos](../../overview.md)
