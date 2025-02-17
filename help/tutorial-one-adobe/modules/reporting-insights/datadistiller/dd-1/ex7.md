---
title: 'Servicio de consulta: explorar el conjunto de datos con Tableau'
description: 'Servicio de consulta: explorar el conjunto de datos con Tableau'
kt: 5342
doc-type: tutorial
exl-id: 33ab854d-fad7-497c-affa-f58e4299c0b3
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 2.1.7 Servicio de consultas y Tableau

Abra Tableau.

![start-tableau.png](./images/starttableau.png)

En **Conectarse a un servidor**, haga clic en **Más** y, a continuación, en **PostgreSQL**.

![tableau-connect-postgress.png](./images/tableauconnectpostgress.png)

Si todavía no ha utilizado PostgeSQL con Tableau, es posible que vea esto. Haga clic en **Descargar controlador**.

![tableau-connect-postgress.png](./images/tableauconnectpostgress1.png)

Siga las instrucciones para descargar e instalar el controlador PostgreSQL.

![tableau-connect-postgress.png](./images/tableauconnectpostgress2.png)

Una vez que haya terminado de instalar el controlador, salga y reinicie Tableau Desktop. Después del reinicio, ve a **Conectarse a un servidor** de nuevo, haz clic en **Más** y luego haz clic en **PostgreSQL** de nuevo.

![tableau-connect-postgress.png](./images/tableauconnectpostgress.png)

Entonces verá esto...

![tableau-connect-postgress.png](./images/tableauconnectpostgress3.png)

Vaya a Adobe Experience Platform, **Consultas** y **Credenciales**.

![query-service-credentials.png](./images/queryservicecredentials.png)

En la página **Credentials** de Adobe Experience Platform, copie el **host** y péguelo en el campo **Server**, copie la **Base de datos** y péguela en el campo **Database** en Tableau, copie el **Puerto** y péguelo en el campo **Puerto** en Tableau, haga lo mismo para **Username** y **Contraseña**. A continuación, haga clic en **Iniciar sesión**.

![tableau-connection-dialog.png](./images/tableauconnectiondialog.png)

En la lista de tablas disponibles, busque la tabla que creó en el ejercicio anterior, que se llama `--aepUserLdap--_callcenter_interaction_analysis`. Arrástrela al lienzo.

![tableau-drag-table.png](./images/tableaudragtable.png)

Entonces verá esto... Haga clic en **Actualizar ahora**.

![tableau-drag-table.png](./images/tableaudragtable1.png)

A continuación, verá que los datos de AEP están disponibles en Tableau. Haga clic en **Hoja 1** para comenzar a trabajar con los datos.

![tableau-drag-table.png](./images/tableaudragtable2.png)

Para visualizar los datos en el mapa, debe convertir la longitud y la latitud en dimensiones. En **Medidas**, haga clic con el botón derecho en **Latitud** y seleccione **Convertir a Dimension** en el menú. Haga lo mismo para la medida **Longitude**.

![tableau-convert-dimension.png](./images/tableauconvertdimension.png)

Arrastre la medida **Longitude** a **Columns** y la medida **Latitude** a **Rows**. Automáticamente, el mapa de **Bélgica** aparecerá con pequeños puntos que representan las ciudades dentro del conjunto de datos.

![tableau-drag-lon-lat.png](./images/tableaudraglonlat.png)

Seleccione **Nombres de medida**, haga clic en **Agregar a hoja**.

![tableau-select-measure-names.png](./images/selectmeasurenames.png)

Ahora tendrá un mapa, con puntos de varios tamaños. El tamaño indica la cantidad de interacciones del centro de llamadas para esa ciudad específica. Para variar el tamaño de los puntos, vaya al panel derecho y abra **Valores de medida** (usando el icono desplegable). En la lista desplegable, seleccione **Editar tamaños**. Juega con diferentes tamaños.

![tableau-vary-size-dots.png](./images/tableauvarysizedots.png)

Para mostrar más los datos por **Tema de llamada**, arrastre la dimensión **Tema de llamada** a **Páginas**. Desplácese por los diferentes **temas de llamada** usando **Tema de llamada** a la derecha de la pantalla:

![tableau-call-topic-navigation.png](./images/tableaucalltopicnavigation.png)

Ya ha terminado este ejercicio.

## Pasos siguientes

Ir a [2.1.8 API de servicio de consultas](./ex8.md){target="_blank"}

Volver a [servicio de consultas](./query-service.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
