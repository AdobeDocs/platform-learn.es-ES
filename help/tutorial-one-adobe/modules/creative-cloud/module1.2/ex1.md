---
title: Introducción a Workfront Fusion
description: Introducción a Workfront Fusion
kt: 5342
doc-type: tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: a4933bd49988cd16c4382ad4327d01ae58b52bbb
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 2%

---

# 1.2.1 Introducción a Workfront Fusion

En este ejercicio, utilizará Workfront Fusion y Adobe I/O para consultar las API de los servicios de Adobe Firefly.

## 1.2.1.1 Crear nuevo escenario

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/). Haga clic para abrir **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Entonces debería ver esto. Ir a **escenarios**.

![WF Fusion](./images/wffusion2.png)

Haga clic en **Crear nuevo escenario**.

![WF Fusion](./images/wffusion3.png)

A continuación, verá un escenario vacío. Haga clic en el icono **herramientas** y seleccione **Establecer varias variables**.

![WF Fusion](./images/wffusion4.png)

Ahora necesita mover el icono **clock** al **Set multiple variables** que acaba de agregar.

![WF Fusion](./images/wffusion5.png)

Entonces verá esto...

![WF Fusion](./images/wffusion6.png)

A continuación, haga clic con el botón derecho en el signo de interrogación y seleccione **Eliminar módulo**.

![WF Fusion](./images/wffusion7.png)

A continuación, haga clic con el botón derecho en el objeto **Set multiple variables** y seleccione **Settings**.

![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Configuración de la autenticación de Adobe I/O

Ahora debe configurar las variables necesarias para autenticarse con el Adobe I/O. En el ejercicio anterior creó un proyecto de Adobe I/O. Las variables de ese proyecto de Adobe I/O ahora deben definirse en Workfront Fusion.

Deben definirse las siguientes variables:

| Clave | Valor |
|:-------------:| :---------------:| 
| `CONST_client_id` | su ID de cliente del proyecto de Adobe I/O |
| `CONST_client_secret` | Secreto del cliente del proyecto de Adobe I/O |
| `CONST_scope` | Ámbito del proyecto de Adobe I/O |

Puede encontrar estas variables yendo a [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects) y abriendo su proyecto de Adobe I/O, que se llama `--aepUserLdap-- Firefly`.

![WF Fusion](./images/wffusion9.png)

En el proyecto, haga clic en **Servidor OAuth** para ver los valores de las claves anteriores.

![WF Fusion](./images/wffusion10.png)

Con las claves y los valores anteriores, puede configurar el objeto **Set multiple variables**. Haga clic en **Agregar elemento**.

![WF Fusion](./images/wffusion11.png)

Escriba el **nombre de variable**: **CONST_client_id** y su **valor de variable**, haga clic en **Agregar**.

![WF Fusion](./images/wffusion12.png)

Haga clic en **Agregar elemento**.

![WF Fusion](./images/wffusion13.png)

Escriba el **nombre de variable**: **CONST_client_secret** y su **valor de variable**, haga clic en **Agregar**.

![WF Fusion](./images/wffusion14.png)

Haga clic en **Agregar elemento**.

![WF Fusion](./images/wffusion15.png)

Escriba el **nombre de variable**: **Ámbito_CONST** y su **valor de variable**, haga clic en **Agregar**.

![WF Fusion](./images/wffusion16.png)

Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion17.png)

Pase el ratón sobre su objeto **Set multiple variables** y haga clic en el icono **+** para agregar otro módulo.

![WF Fusion](./images/wffusion18.png)

Entonces debería ver esto.

![WF Fusion](./images/wffusion19.png)

En la barra de búsqueda, escriba **http**. Seleccione **HTTP** para abrirlo.

![WF Fusion](./images/wffusion21.png)

y luego selecciona **Realizar una solicitud**.

![WF Fusion](./images/wffusion20.png)

| Clave | Valor |
|:-------------:| :---------------:| 
| `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
| `Method` | `POST` |
| `Body Type` | `x-www-form-urlencoded` |

Haga clic en **Agregar elemento**.

![WF Fusion](./images/wffusion22.png)

Agregue elementos para cada uno de los siguientes valores:

| Clave | Valor |
|:-------------:| :---------------:| 
| `client_id` | su variable predefinida para `CONST_client_id` |
| `client_secret` | su variable predefinida para `CONST_client_secret` |
| `scope` | su variable predefinida para `CONST_scope` |
| `grant_type` | `client_credentials` |

Configuración de `client_id`.

![WF Fusion](./images/wffusion23.png)

Configuración de `client_secret`.

![WF Fusion](./images/wffusion25.png)

Configuración de `scope`.

![WF Fusion](./images/wffusion26.png)

Configuración de `grant_type`.

![WF Fusion](./images/wffusion28.png)

Información general de configuración. Desplácese hacia abajo y marque la casilla de verificación de **Analizar respuesta**. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion27.png)

Entonces debería ver esto. Haga clic en **Ejecutar una vez**.

![WF Fusion](./images/wffusion29.png)

Una vez ejecutado el escenario, debería ver esto.

![WF Fusion](./images/wffusion30.png)

Haga clic en el icono **signo de interrogación** en el objeto **Establecer varias variables** para ver qué ocurrió cuando se ejecutó ese objeto.

![WF Fusion](./images/wffusion31.png)

Haga clic en el icono **signo de interrogación** en el objeto **HTTP - Realizar una solicitud** para ver qué ocurrió cuando se ejecutó ese objeto. En **OUTPUT**, verá que el Adobe I/O devuelve el **token de acceso**.

![WF Fusion](./images/wffusion32.png)

Pase el ratón sobre el objeto **HTTP - Make a request** y haga clic en el icono **+** para agregar otro módulo.

![WF Fusion](./images/wffusion33.png)

En la barra de búsqueda, busque `tools`. Seleccione **Herramientas**.

![WF Fusion](./images/wffusion34.png)

Seleccione **Establecer múltiples variables**.

![WF Fusion](./images/wffusion35.png)

Seleccione **Agregar elemento**.

![WF Fusion](./images/wffusion36.png)

Establezca **Variable name** en `bearer_token`. Seleccione `access_token` como **valor de variable** dinámico. Seleccionar **Agregar**.

![WF Fusion](./images/wffusion37.png)

Entonces deberías tener esto. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion38.png)

Haga clic en **Ejecutar una vez** de nuevo.

![WF Fusion](./images/wffusion39.png)

Una vez que se haya ejecutado el escenario, haga clic en el icono **signo de interrogación** en el último objeto **Set multiple variables**. Luego debería ver que access_token se está almacenando en la variable `bearer_token`.

![WF Fusion](./images/wffusion40.png)

A continuación, haga clic con el botón derecho en el primer objeto **Establecer varios valores** y seleccione **Cambiar nombre**.

![WF Fusion](./images/wffusion41.png)

Establezca el nombre en **Inicializar constantes**. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion42.png)

Cambie el nombre del segundo objeto y establezca el nombre en **Autenticar en el Adobe I/O**. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion43.png)

Cambie el nombre del tercer objeto y establezca el nombre en **Set Bearer Token**. Haga clic en **Aceptar**.

![WF Fusion](./images/wffusion44.png)

Entonces deberías tener esto.

![WF Fusion](./images/wffusion45.png)

A continuación, cambie el nombre de su escenario a `--aepUSerLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffusion46.png)

Haga clic en **Guardar**.

![WF Fusion](./images/wffusion47.png)

Siguiente paso: [1.2.2 Usar API de Adobe en Workfront Fusion](./ex2.md)

[Volver al módulo 1.2](./automation.md)

[Volver a todos los módulos](./../../../overview.md)
