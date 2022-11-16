---
title: 'Servicio de consultas: introducción'
description: 'Servicio de consultas: introducción'
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: dae257d2-8c94-4558-b9ce-eca38a88667b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---

# 4.1 Introducción

## 4.1.1 Familiarizarse con la IU de Adobe Experience Platform

Vaya a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](../module2/images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``--module7sandbox--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar los elementos adecuados [!UICONTROL entorno limitado], verá el cambio de pantalla y ahora estará en su [!UICONTROL entorno limitado].

![Ingesta de datos](../module2/images/sb1.png)


## 4.1.2 Explorar los datos en la plataforma

Traer datos de diferentes canales es una tarea difícil para cualquier marca. Y en este ejercicio, los clientes de Citi Signal están interactuando con Citi Signal en su sitio web, en su aplicación móvil, el sistema de puntos de venta de Citi Signal recopila datos de compras y cuentan con datos de CRM y fidelidad. Citi Signal utiliza Adobe Analytics y Adobe Launch para capturar datos en su sitio web, aplicación móvil y sistema POS, por lo que estos datos ya fluyen a Adobe Experience Platform. Empecemos explorando todos los datos para Citi Signal que ya existen en Adobe Experience Platform.

En el menú de la izquierda, vaya a **Conjuntos de datos**.

![emea-website-interaction-dataset.png](./images/emea-website-interaction-dataset.png)

Citi Signal transmite datos a Adobe Experience Platform y estos datos están disponibles en el `Demo System - Event Dataset for Website (Global v1.1)` conjunto de datos. Buscar `Demo System - Event Dataset for Website`.

![emea-callcenter-interaction-dataset.png](./images/emea-website-interaction-dataset1.png)

Los datos de interacción Callcenter de Citi Signal se capturan en el `Demo System - Event Dataset for Call Center (Global v1.1)` conjunto de datos. Buscar `Demo System - Event Dataset for Call Center` datos en el cuadro de búsqueda. Haga clic en el nombre del conjunto de datos para abrirlo.

![emea-callcenter-interaction-dataset.png](./images/emea-callcenter-interaction-dataset.png)

Después de hacer clic en el conjunto de datos, obtendrá una descripción general de la actividad del conjunto de datos, como lotes ingeridos y con errores.

![preview-interaction-dataset.png](./images/preview-interaction-dataset.png)

Haga clic en **Vista previa del conjunto de datos** para ver una muestra de los datos almacenados en `Demo System - Event Dataset for Call Center (Global v1.1)` conjunto de datos. El panel izquierdo muestra la estructura de esquema para este conjunto de datos.

![explore-interaction-dataset.png](./images/explore-interaction-dataset.png)

Haga clic en el **Cerrar** para cerrar el **Vista previa del conjunto de datos** ventana.

## 4.1.3 Introducción al servicio de consultas

Para acceder al servicio de consultas de Adobe Experience Platform, haga clic en **Consultas** en el menú de la izquierda.

![select-queries.png](./images/select-queries.png)

Accediendo a **Registro** verá la página Lista de consultas , que proporciona una lista de todas las consultas que se han ejecutado en esta organización, con la última en la parte superior.

![query-list.png](./images/query-list.png)

Haga clic en cualquier consulta SQL de la lista y observe los detalles proporcionados en el carril derecho.

![click-sql-query.png](./images/click-sql-query.png)

Puede desplazarse por la ventana para ver toda la consulta, o puede hacer clic en el icono resaltado abajo para copiar toda la consulta en el bloc de notas. No es necesario copiar la consulta en este momento.

![click-copy-query.png](./images/click-copy-query.png)

No solo puede ver las consultas que se han ejecutado, esta interfaz de usuario le permite crear nuevos conjuntos de datos a partir de consultas. Estos conjuntos de datos pueden vincularse al perfil del cliente en tiempo real de Adobe Experience Platform o utilizarse como entrada para Adobe Experience Platform Data Science Workspace.

## 4.1.4 Conectar el cliente PSQL con el servicio de consulta

El servicio de consultas admite clientes con un controlador para PostgreSQL. En esto usaremos PSQL, una interfaz de línea de comandos, y Power BI o Tableau. Conectémonos a PSQL.

Haga clic en **Credenciales**.

![queries-select-configuration.png](./images/queries-select-configuration.png)

Verá la siguiente pantalla. La pantalla Configuración proporciona información del servidor y credenciales para autenticarse en el servicio de consulta. Por ahora, nos centraremos en el lado derecho de la pantalla que contiene un comando connect para PSQL. Haga clic en el botón Copiar para copiar el comando en el portapapeles.

![copy-psql-connection.png](./images/copy-psql-connection.png)

Para Windows: Abra la línea de comandos pulsando la tecla windows, escribiendo cmd y luego haciendo clic en el resultado del símbolo del sistema.

![open-command-request.png](./images/open-command-prompt.png)

Para macOS: Abra terminal.app mediante la búsqueda de puntos destacados:

![open-terminal-osx.png](./images/open-terminal-osx.png)

Pegue el comando connect que ha copiado de la interfaz de usuario del servicio de consulta y pulse Enter en la ventana del símbolo del sistema:

Windows:

![símbolo del sistema-conectado.png](./images/command-prompt-connected.png)

MacOS:

![command-quick-Paste-osx.png](./images/command-prompt-paste-osx.png)

Ahora está conectado al servicio de consulta mediante PSQL.

En los próximos ejercicios, habrá bastante interacción con esta ventana. Nos referiremos a él como su **Interfaz de línea de comandos de PSQL**.

Ahora está listo para empezar a enviar consultas.

Paso siguiente: [4.2 Uso del servicio de consulta](./ex2.md)

[Volver al módulo 4](./query-service.md)

[Volver a todos los módulos](../../overview.md)
