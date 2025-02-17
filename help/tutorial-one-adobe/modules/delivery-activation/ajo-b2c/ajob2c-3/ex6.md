---
title: 'Offer Decisioning: Pruebe su decisión con la API'
description: Prueba de la decisión mediante la API
kt: 5342
doc-type: tutorial
exl-id: 52f90b9f-32ea-49c2-af5d-8742ca8b3b4e
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# 3.3.6 Pruebe su decisión mediante la API

## 3.3.6.1 Trabajo con la API de Offer Decisioning mediante Postman

>[!IMPORTANT]
>
>Si eres empleado de Adobe, sigue las instrucciones aquí para usar [PostBuster](./../../../../modules/getting-started/gettingstarted/ex8.md).

Descargue [esta colección de Postman para Offer Decisioning](./../../../../assets/postman/postman_offer-decisioning.zip) en su equipo de escritorio y descomprímala. A continuación, tendrá esto:

![API OD](./images/unzip.png)

Ahora tiene este archivo en el escritorio:

- `_AJO- Decisioning Service.postman_collection.json`

En [Ejercicio 2.1.3 - Autenticación de Postman en Adobe I/O](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-1/ex3.md) instaló Postman. Tendrá que volver a utilizar Postman para este ejercicio.

Abra Postman e importe el archivo `_AJO- Decisioning Service.postman_collection.json`. A continuación, tendrá esta colección disponible en Postman.

![Nueva integración de Adobe I/O](./images/postmanui.png)

Ahora tiene todo lo que necesita en Postman para empezar a interactuar con Adobe Experience Platform a través de las API.

Antes de usar las siguientes API, asegúrese de volver a autenticarse con la colección **Adobe IO - OAuth** que configuró en el ejercicio 2.1.3.

![Nueva integración de Adobe I/O](./images/postmanui1.png)


### 3.3.6.2 Obtener ofertas para el perfil del cliente

Haga clic para abrir la solicitud **POST - Obtener ofertas para el perfil del cliente**. Lo primero que hay que actualizar es la variable **Header** para **x-sandbox-name**. Debe establecerlo en `--aepSandboxName--`.

![API OD](./images/api23.png)

Para esta solicitud, hay una serie de campos que deben actualizarse. Ir a **Cuerpo**.

- **xdm:placementId**
- **xdm:activityId**
- **xdm:id**
- **xdm:itemCount** (cambie a un valor de su elección)

![API OD](./images/api24.png)

Debe rellenarse el campo **xdm:activityId**. Puede recuperarlos en la interfaz de usuario de Adobe Experience Platform, como se indica a continuación.

![API OD](./images/activityid.png)

Debe rellenarse el campo **[!UICONTROL xdm:placementId]**. Puede recuperarlos en la interfaz de usuario de Adobe Experience Platform, como se indica a continuación. En el siguiente ejemplo, puede ver placementId para la ubicación **[!UICONTROL Web - Image]**.

![API OD](./images/placementid.png)

En el campo **xdm:id**, escriba la dirección de correo electrónico del perfil de cliente para el que desea solicitar una oferta. Una vez que todos los valores estén establecidos como se desea, haga clic en **[!UICONTROL Enviar]**.

![API OD](./images/api24a.png)

Finalmente, verá el resultado de qué tipo de oferta personalizada y qué recursos deben mostrarse a este cliente. En este ejemplo se solicitaron 2 elementos y, como puede ver, se devolvieron 2 ofertas personalizadas. 1 oferta para Apple Watch y otra oferta para Galaxy Watch 7.

![API OD](./images/api25.png)

Ahora ha completado este ejercicio.

## Pasos siguientes

Ir a [Resumen y beneficios](./summary.md){target="_blank"}

Volver a [Offer Decisioning](offer-decisioning.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
