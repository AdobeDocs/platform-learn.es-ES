---
title: 'Servicio de consulta: explorar el conjunto de datos con Tableau'
description: 'Servicio de consulta: explorar el conjunto de datos con Tableau'
kt: 5342
doc-type: tutorial
exl-id: 29525740-fe1f-4770-bcc9-f2ad499a2cb5
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 5.1.7 Servicio de consultas y Tableau

Abra Tableau.

![start-tableau.png](./images/start-tableau.png)

En **Conectarse a un servidor**, seleccione **PostgreSQL**:

![tableau-connect-postgress.png](./images/tableau-connect-postgress.png)

Vaya a Adobe Experience Platform, **Consultas** y **Credenciales**.

![query-service-credentials.png](./images/query-service-credentials.png)

En la página **Credentials** de Adobe Experience Platform, copie el **host** y péguelo en el campo **Server**, copie la **Base de datos** y péguela en el campo **Database** en Tableau, copie el **Puerto** y péguelo en el campo **Puerto** en Tableau, haga lo mismo para **Username** y **Contraseña**. A continuación, haga clic en **Iniciar sesión**.

Iniciar sesión:

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

Haga clic en buscar (1) e introduzca su **ldap** en el campo de búsqueda, identifique la tabla del conjunto de resultados y arrástrela (3) a la ubicación **Arrastrar tablas aquí**. Cuando termine, haga clic en **Hoja 1** (3).

![tableau-drag-table.png](./images/tableau-drag-table.png)

Para visualizar nuestros datos en el mapa necesitamos convertir la longitud y la latitud en dimensiones. En **Medidas**, seleccione **Latitud** (1), abra la lista desplegable del campo y seleccione **Convertir en Dimension** (2). Haga lo mismo para la medida **Longitude**.

![tableau-convert-dimension.png](./images/tableau-convert-dimension.png)

Arrastre la medida **Longitude** a **Columns** y la medida **Latitude** a **Rows**. Automáticamente, el mapa de **Bélgica** aparecerá con pequeños puntos que representan las ciudades dentro del conjunto de datos.

![tableau-drag-lon-lat.png](./images/tableau-drag-lon-lat.png)

Seleccione **Nombres de medida** (1), abra la lista desplegable y seleccione **Agregar a hoja** (2):

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

Ahora tendrá un mapa, con puntos de varios tamaños. El tamaño indica la cantidad de interacciones del centro de llamadas para esa ciudad específica. Para variar el tamaño de los puntos, vaya al panel derecho y abra **Valores de medida** (usando el icono desplegable). En la lista desplegable, seleccione **Editar tamaños**. Juega con diferentes tamaños.

![tableau-vary-size-dots.png](./images/tableau-vary-size-dots.png)

Para mostrar más los datos por **Tema de llamada**, arrastre (1) la dimensión **Tema de llamada** a **Páginas**. Desplácese por los diferentes **temas de llamada** usando **Tema de llamada** (2) a la derecha de la pantalla:

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

Ya ha terminado este ejercicio.

Siguiente paso: [5.1.8 API de servicio de consultas](./ex8.md)

[Volver al módulo 5.1](./query-service.md)

[Volver a todos los módulos](../../../overview.md)
