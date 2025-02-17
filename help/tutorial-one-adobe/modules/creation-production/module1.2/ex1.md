---
title: Introducción a Workfront Fusion
description: Aprenda a utilizar Workfront Fusion y Adobe I/O para consultar las API de servicios de Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---

# 1.2.1 Introducción a Workfront Fusion

Aprenda a utilizar Workfront Fusion y Adobe I/O para consultar las API de servicios de Adobe Firefly.

## 1.2.1.1 Crear nuevo escenario

1. Vaya a [https://experience.adobe.com/](https://experience.adobe.com/). Abra **Workfront Fusion**.

   ![WF Fusion](./images/wffusion1.png)

1. Ir a **escenarios**.

   ![WF Fusion](./images/wffusion2.png)

1. Seleccione **Crear nuevo escenario**.

   ![WF Fusion](./images/wffusion2a.png)

1. Asigne un nombre a la carpeta `--aepUserLdap--` y seleccione **Guardar**.

   ![WF Fusion](./images/wffusion2b.png)

1. Seleccione su carpeta y luego seleccione **Crear nuevo escenario**.

   ![WF Fusion](./images/wffusion3.png)

1. Aparece un escenario vacío, seleccione **herramientas** y seleccione **Establecer múltiples variables**.

   ![WF Fusion](./images/wffusion4.png)

1. Mueva el icono **clock** al **Set multiple variables** que acaba de agregar.

   ![WF Fusion](./images/wffusion5.png)

   La pantalla debería tener un aspecto similar al siguiente.

   ![WF Fusion](./images/wffusion6.png)

1. Haga clic con el botón derecho en el signo de interrogación y seleccione **Eliminar módulo**.

   ![WF Fusion](./images/wffusion7.png)

1. A continuación, haga clic con el botón derecho en **Establecer varias variables** y seleccione **Configuración**.

   ![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Configuración de la autenticación de Adobe I/O

Ahora debe configurar las variables necesarias para autenticarse en Adobe I/O. En el ejercicio anterior creó un proyecto de Adobe I/O. Las variables de ese proyecto de Adobe I/O ahora deben definirse en Workfront Fusion.

Deben definirse las siguientes variables:

| Clave | Valor |
|:-------------:| :---------------:| 
| `CONST_client_id` | su ID de cliente del proyecto de Adobe I/O |
| `CONST_client_secret` | Secreto de cliente del proyecto de Adobe I/O |
| `CONST_scope` | Ámbito del proyecto de Adobe I/O |

1. Para encontrar estas variables, vaya a [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects) y abra el proyecto de Adobe I/O, que se llama `--aepUserLdap-- Firefly`.

   ![WF Fusion](./images/wffusion9.png)

1. En su proyecto, seleccione **OAuth Server to-Server** para ver los valores de las claves anteriores.

   ![WF Fusion](./images/wffusion10.png)

1. Con las claves y los valores anteriores, puede configurar el objeto **Set multiple variables**. Seleccione **Agregar elemento**.

   ![WF Fusion](./images/wffusion11.png)

1. Escriba el **nombre de variable**: **CONST_client_id** y su **valor de variable**, seleccione **Agregar**.

   ![WF Fusion](./images/wffusion12.png)

1. Seleccione **Agregar elemento**.

   ![WF Fusion](./images/wffusion13.png)

1. Escriba **Nombre de variable**: **CONST_client_secret** y su **Valor de variable**, seleccione **Agregar**.

   ![WF Fusion](./images/wffusion14.png)

1. Seleccione **Agregar elemento**.

   ![WF Fusion](./images/wffusion15.png)

1. Escriba **Nombre de variable**: **CONST_scope** y su **valor de variable**, seleccione **Agregar**.

   ![WF Fusion](./images/wffusion16.png)

1. Seleccione **Aceptar**.

   ![WF Fusion](./images/wffusion17.png)

1. Pase el ratón sobre **Establecer varias variables** y seleccione el icono **+** grande para agregar otro módulo.

   ![WF Fusion](./images/wffusion18.png)

   La pantalla debería tener un aspecto similar al siguiente.

   ![WF Fusion](./images/wffusion19.png)

1. En la barra de búsqueda, escriba **http**. Seleccione **HTTP** para abrirlo.

   ![WF Fusion](./images/wffusion21.png)

1. Seleccione **Realizar una solicitud**.

   ![WF Fusion](./images/wffusion20.png)

   | Clave | Valor |
   |:-------------:| :---------------:| 
   | `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
   | `Method` | `POST` |
   | `Body Type` | `x-www-form-urlencoded` |

1. Seleccione **Agregar elemento**.

   ![WF Fusion](./images/wffusion22.png)

1. Agregue elementos para cada uno de los siguientes valores:

   | Clave | Valor |
   |:-------------:| :---------------:| 
   | `client_id` | su variable predefinida para `CONST_client_id` |
   | `client_secret` | su variable predefinida para `CONST_client_secret` |
   | `scope` | su variable predefinida para `CONST_scope` |
   | `grant_type` | `client_credentials` |

1. Configuración de `client_id`:

   ![WF Fusion](./images/wffusion23.png)

1. Configuración de `client_secret`.

   ![WF Fusion](./images/wffusion25.png)

1. Configuración de `scope`.

   ![WF Fusion](./images/wffusion26.png)

1. Configuración de `grant_type`.

   ![WF Fusion](./images/wffusion28.png)

1. Desplácese hacia abajo y marque la casilla de **Respuesta de análisis**. Seleccione **Aceptar**.

   ![WF Fusion](./images/wffusion27.png)

1. La pantalla debería tener un aspecto similar al siguiente. Seleccionar **Ejecutar una vez**.

   ![WF Fusion](./images/wffusion29.png)

   Una vez que se haya ejecutado el escenario, la pantalla debería tener este aspecto:

   ![WF Fusion](./images/wffusion30.png)

1. Seleccione el icono **signo de interrogación** en el objeto **Set multiple variables** para ver qué ocurrió cuando se ejecutó ese objeto.

   ![WF Fusion](./images/wffusion31.png)

1. Seleccione el icono **signo de interrogación** en el objeto **HTTP - Realice una solicitud** para ver qué ocurrió cuando se ejecutó ese objeto. En **OUTPUT**, vea el **token de acceso** devuelto por Adobe I/O.

   ![WF Fusion](./images/wffusion32.png)

1. Pase el ratón sobre **HTTP - Realice una solicitud** y seleccione el icono **+** para agregar otro módulo.

   ![WF Fusion](./images/wffusion33.png)

1. En la barra de búsqueda, busque `tools`. Seleccione **Herramientas**.

   ![WF Fusion](./images/wffusion34.png)

1. Seleccione **Establecer múltiples variables**.

   ![WF Fusion](./images/wffusion35.png)

1. Seleccione **Agregar elemento**.

   ![WF Fusion](./images/wffusion36.png)

1. Establezca **Nombre de variable** en `bearer_token`. Seleccione `access_token` como **valor de variable** dinámico. Seleccione **Agregar**.

   ![WF Fusion](./images/wffusion37.png)

1. La pantalla debería tener un aspecto similar al siguiente. Seleccione **Aceptar**.

   ![WF Fusion](./images/wffusion38.png)

1. Seleccione **Ejecutar una vez** de nuevo.

   ![WF Fusion](./images/wffusion39.png)

1. Una vez que se ejecute el escenario, seleccione el icono **signo de interrogación** en el último objeto **Set multiple variables**. Debería ver que access_token se está almacenando en la variable `bearer_token`.

   ![WF Fusion](./images/wffusion40.png)

1. A continuación, haga clic con el botón derecho en el primer objeto **Establecer varios valores** y seleccione **Cambiar nombre**.

   ![WF Fusion](./images/wffusion41.png)

1. Establezca el nombre en **Inicializar constantes**. Seleccione **Aceptar**.

   ![WF Fusion](./images/wffusion42.png)

1. Cambie el nombre del segundo objeto a **Autenticar en Adobe I/O**. Seleccione **Aceptar**.

   ![WF Fusion](./images/wffusion43.png)

1. Cambie el nombre del tercer objeto a **Set Bearer Token**. Seleccione **Aceptar**.

   ![WF Fusion](./images/wffusion44.png)

   La pantalla debería tener un aspecto similar al siguiente:

   ![WF Fusion](./images/wffusion45.png)

1. A continuación, cambie el nombre de su escenario a `--aepUSerLdap-- - Adobe I/O Authentication`.

   ![WF Fusion](./images/wffusion46.png)

1. Seleccione **Guardar**.

   ![WF Fusion](./images/wffusion47.png)

## Pasos siguientes

Vaya a [Usar las API de Adobe en Workfront Fusion](./ex2.md){target="_blank"}

Volver a [Automatizar servicios de Adobe Firefly](./automation.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
