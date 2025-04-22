---
title: Introducción a Workfront Fusion
description: Aprenda a utilizar Workfront Fusion y Adobe I/O para consultar las API de Adobe Firefly Services
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: 4b38b40c47b5c373f74a85261adce46f291303a8
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---

# 1.2.1 Introducción a Workfront Fusion

Aprenda a utilizar Workfront Fusion y Adobe I/O para consultar las API de Adobe Firefly Services.

## 1.2.1.1 Crear nuevo escenario

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Ir a **escenarios**.

![WF Fusion](./images/wffusion2.png)

Haga clic en el icono **+** para crear una carpeta nueva para su trabajo.

![WF Fusion](./images/wffusion2a.png)

Asigne un nombre a la carpeta `--aepUserLdap--` y seleccione **Guardar**.

![WF Fusion](./images/wffusion2b.png)

Seleccione su carpeta y luego seleccione **Crear nuevo escenario**.

![WF Fusion](./images/wffusion3.png)

Aparece un escenario vacío, seleccione **herramientas** y seleccione **Establecer múltiples variables**.

![WF Fusion](./images/wffusion4.png)

Mueva el icono **clock** al **Set multiple variables** que acaba de agregar.

![WF Fusion](./images/wffusion5.png)

La pantalla debería tener un aspecto similar al siguiente.

![WF Fusion](./images/wffusion6.png)

Haga clic con el botón derecho en el signo de interrogación y seleccione **Eliminar módulo**.

![WF Fusion](./images/wffusion7.png)

A continuación, haga clic con el botón derecho en **Establecer varias variables** y seleccione **Configuración**.

![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 configurar autenticación de Adobe I/O

Ahora debe configurar las variables necesarias para autenticarse en Adobe I/O. En el ejercicio anterior creó un proyecto de Adobe I/O. Las variables de ese proyecto de Adobe I/O ahora deben definirse en Workfront Fusion.

Deben definirse las siguientes variables:

| Clave | Valor |
|:-------------:| :---------------:| 
| `CONST_client_id` | su ID de cliente del proyecto de Adobe I/O |
| `CONST_client_secret` | Secreto de cliente del proyecto de Adobe I/O |
| `CONST_scope` | Ámbito del proyecto de Adobe I/O |

Para encontrar estas variables, vaya a [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects){target="_blank"} y abra el proyecto de Adobe I/O, que se llama `--aepUserLdap-- One Adobe tutorial`.

![WF Fusion](./images/wffusion9.png)

En su proyecto, seleccione **OAuth Server to-Server** para ver los valores de las claves anteriores.

![WF Fusion](./images/wffusion10.png)

Con las claves y los valores anteriores, puede configurar el objeto **Set multiple variables**. Seleccione **Agregar elemento**.

![WF Fusion](./images/wffusion11.png)

Escriba el **nombre de variable**: **CONST_client_id** y su **valor de variable**, seleccione **Agregar**.

![WF Fusion](./images/wffusion12.png)

Seleccione **Agregar elemento**.

![WF Fusion](./images/wffusion13.png)

Escriba **Nombre de variable**: **CONST_client_secret** y su **Valor de variable**, seleccione **Agregar**.

![WF Fusion](./images/wffusion14.png)

Seleccione **Agregar elemento**.

![WF Fusion](./images/wffusion15.png)

Escriba **Nombre de variable**: **CONST_scope** y su **valor de variable**, seleccione **Agregar**.

![WF Fusion](./images/wffusion16.png)

Seleccione **Aceptar**.

![WF Fusion](./images/wffusion17.png)

Pase el ratón sobre **Establecer varias variables** y seleccione el icono **+** grande para agregar otro módulo.

![WF Fusion](./images/wffusion18.png)

La pantalla debería tener un aspecto similar al siguiente.

![WF Fusion](./images/wffusion19.png)

En la barra de búsqueda, escriba **http**. Seleccione **HTTP** para abrirlo.

![WF Fusion](./images/wffusion21.png)

Seleccione **Realizar una solicitud**.

![WF Fusion](./images/wffusion20.png)

| Clave | Valor |
|:-------------:| :---------------:| 
| `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
| `Method` | `POST` |
| `Body Type` | `x-www-form-urlencoded` |

Seleccione **Agregar elemento**.

![WF Fusion](./images/wffusion22.png)

Agregue elementos para cada uno de los siguientes valores:

| Clave | Valor |
|:-------------:| :---------------:| 
| `client_id` | su variable predefinida para `CONST_client_id` |
| `client_secret` | su variable predefinida para `CONST_client_secret` |
| `scope` | su variable predefinida para `CONST_scope` |
| `grant_type` | `client_credentials` |

Configuración de `client_id`:

![WF Fusion](./images/wffusion23.png)

Configuración de `client_secret`.

![WF Fusion](./images/wffusion25.png)

Configuración de `scope`.

![WF Fusion](./images/wffusion26.png)

Configuración de `grant_type`.

![WF Fusion](./images/wffusion28.png)

Desplácese hacia abajo y marque la casilla de **Respuesta de análisis**. Seleccione **Aceptar**.

![WF Fusion](./images/wffusion27.png)

La pantalla debería tener un aspecto similar al siguiente. Seleccionar **Ejecutar una vez**.

![WF Fusion](./images/wffusion29.png)

Una vez que se haya ejecutado el escenario, la pantalla debería tener este aspecto:

![WF Fusion](./images/wffusion30.png)

Seleccione el icono **signo de interrogación** en el objeto **Set multiple variables** para ver qué ocurrió cuando se ejecutó ese objeto.

![WF Fusion](./images/wffusion31.png)

Seleccione el icono **signo de interrogación** en el objeto **HTTP - Realice una solicitud** para ver qué ocurrió cuando se ejecutó ese objeto. En **OUTPUT**, vea el **token de acceso** devuelto por Adobe I/O.

![WF Fusion](./images/wffusion32.png)

Pase el ratón sobre **HTTP - Realice una solicitud** y seleccione el icono **+** para agregar otro módulo.

![WF Fusion](./images/wffusion33.png)

En la barra de búsqueda, busque `tools`. Seleccione **Herramientas**.

![WF Fusion](./images/wffusion34.png)

Seleccione **Establecer múltiples variables**.

![WF Fusion](./images/wffusion35.png)

Seleccione **Agregar elemento**.

![WF Fusion](./images/wffusion36.png)

Establezca **Nombre de variable** en `bearer_token`. Seleccione `access_token` como **valor de variable** dinámico. Seleccione **Agregar**.

![WF Fusion](./images/wffusion37.png)

La pantalla debería tener un aspecto similar al siguiente. Seleccione **Aceptar**.

![WF Fusion](./images/wffusion38.png)

Seleccione **Ejecutar una vez** de nuevo.

![WF Fusion](./images/wffusion39.png)

Una vez que se ejecute el escenario, seleccione el icono **signo de interrogación** en el último objeto **Set multiple variables**. Debería ver que access_token se está almacenando en la variable `bearer_token`.

![WF Fusion](./images/wffusion40.png)

A continuación, haga clic con el botón derecho en el primer objeto **Establecer varios valores** y seleccione **Cambiar nombre**.

![WF Fusion](./images/wffusion41.png)

Establezca el nombre en **Inicializar constantes**. Seleccione **Aceptar**.

![WF Fusion](./images/wffusion42.png)

Cambie el nombre del segundo objeto a **Autenticar en Adobe I/O**. Seleccione **Aceptar**.

![WF Fusion](./images/wffusion43.png)

Cambie el nombre del tercer objeto a **Set Bearer Token**. Seleccione **Aceptar**.

![WF Fusion](./images/wffusion44.png)

La pantalla debería tener un aspecto similar al siguiente:

![WF Fusion](./images/wffusion45.png)

A continuación, cambie el nombre de su escenario a `--aepUserLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffusion46.png)

Seleccione **Guardar**.

![WF Fusion](./images/wffusion47.png)

## Pasos siguientes

Vaya a [Usar las API de Adobe en Workfront Fusion](./ex2.md){target="_blank"}

Volver a [Automatización del flujo de trabajo de Creative con Workfront Fusion](./automation.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
