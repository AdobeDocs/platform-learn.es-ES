---
title: 'Primeros pasos: Adobe I/O'
description: 'Primeros pasos: Adobe I/O'
kt: 5342
doc-type: tutorial
exl-id: 00f17d4f-a2c8-4e8e-a1ff-556037a60629
source-git-commit: a45283bf5263a6de5c2f83f5be35b7d03ce04d7d
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Configuración del proyecto de Adobe I/O

## Creación de un proyecto de Adobe I/O

En este ejercicio, Adobe I/O se utiliza para consultar varios extremos de Adobe. Siga estos pasos para configurar Adobe I/O.

Vaya a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Nueva integración de Adobe I/O](./images/iohome.png){zoomable="yes"}

Asegúrese de seleccionar la instancia correcta en la esquina superior derecha de la pantalla. Su instancia es `--aepImsOrgName--`.

>[!NOTE]
>
> La siguiente captura de pantalla muestra una organización específica seleccionada. Cuando vaya a través de este tutorial, es muy probable que su organización tenga un nombre diferente. Cuando se registró en este tutorial, se le proporcionaron los detalles del entorno que debe utilizar, siga esas instrucciones.

A continuación, seleccione **Crear nuevo proyecto**.

![Nueva integración de Adobe I/O](./images/iocomp.png){zoomable="yes"}

### API de Firefly Services

>[!IMPORTANT]
>
>Según la ruta de aprendizaje seleccionada, es posible que no tenga acceso a la API de Firefly Services. Solo tendrá acceso a la API de Firefly Services si se encuentra en la ruta de aprendizaje **Firefly**, **Workfront Fusion**, **ALL** o si asiste a un **taller presencial en directo**. Puede omitir este paso si no se encuentra en una de estas rutas de aprendizaje.

Entonces debería ver esto. Seleccione **+ Agregar al proyecto** y elija **API**.

![Nueva integración de Adobe I/O](./images/adobe_io_access_api.png){zoomable="yes"}

La pantalla debería tener un aspecto similar al siguiente.

![Nueva integración de Adobe I/O](./images/api1.png){zoomable="yes"}

Seleccione **Creative Cloud**, elija **Firefly - Firefly Services** y luego seleccione **Siguiente**.

![Nueva integración de Adobe I/O](./images/api3.png){zoomable="yes"}

Proporcione un nombre para su credencial: `--aepUserLdap-- - One Adobe OAuth credential` y seleccione **Siguiente**.

![Nueva integración de Adobe I/O](./images/api4.png){zoomable="yes"}

Seleccione el perfil predeterminado **Configuración predeterminada de Firefly Services** y seleccione **Guardar la API configurada**.

![Nueva integración de Adobe I/O](./images/api9.png){zoomable="yes"}

Entonces debería ver esto.

![Nueva integración de Adobe I/O](./images/api10.png){zoomable="yes"}

### API de Photoshop Services

>[!IMPORTANT]
>
>Según la ruta de aprendizaje seleccionada, es posible que no tenga acceso a la API de Photoshop Services. Solo tendrá acceso a la API de Photoshop Services si se encuentra en la ruta de aprendizaje **Firefly**, **Workfront Fusion**, **ALL** o si asiste a un **taller presencial en directo**. Puede omitir este paso si no se encuentra en una de estas rutas de aprendizaje.

Seleccione **+ Agregar al proyecto** y luego seleccione **API**.

![Almacenamiento de Azure](./images/ps2.png){zoomable="yes"}

Seleccione **Creative Cloud** y elija **Photoshop - Firefly Services**. Seleccione **Siguiente**.

![Almacenamiento de Azure](./images/ps3.png){zoomable="yes"}

Seleccione **Siguiente**.

![Almacenamiento de Azure](./images/ps4.png){zoomable="yes"}

A continuación, debe seleccionar un perfil de producto que defina qué permisos están disponibles para esta integración.

Seleccione **Configuración predeterminada de Firefly Services** y **Configuración predeterminada de Creative Cloud Automation Services**.

Seleccione **Guardar la API configurada**.

![Almacenamiento de Azure](./images/ps5.png){zoomable="yes"}

Entonces debería ver esto.

![Nueva integración de Adobe I/O](./images/ps7.png){zoomable="yes"}

### API de Adobe Experience Platform

>[!IMPORTANT]
>
>Según la ruta de aprendizaje seleccionada, es posible que no tenga acceso a la API de Adobe Experience Platform. Solo tendrá acceso a la API de Adobe Experience Platform si se encuentra en la ruta de aprendizaje **AEP + Aplicaciones**, **TODAS** o si asiste a un **taller presencial en vivo**. Puede omitir este paso si no se encuentra en una de estas rutas de aprendizaje.

Seleccione **+ Agregar al proyecto** y luego seleccione **API**.

![Almacenamiento de Azure](./images/aep1.png){zoomable="yes"}

Seleccione **Adobe Experience Platform** y elija **API de Experience Platform**. Seleccione **Siguiente**.

![Almacenamiento de Azure](./images/aep2.png){zoomable="yes"}

Seleccione **Siguiente**.

![Almacenamiento de Azure](./images/aep3.png){zoomable="yes"}

A continuación, debe seleccionar un perfil de producto que defina qué permisos están disponibles para esta integración.

Seleccione **Adobe Experience Platform - Todos los usuarios - PROD**.

>[!NOTE]
>
>El nombre del perfil de producto para AEP depende de cómo se haya configurado el entorno. Si no ve el perfil de producto mencionado anteriormente, es posible que tenga un perfil de producto denominado **Acceso predeterminado a todos los equipos de producción**. Si no está seguro de cuál elegir, pregunte al administrador del sistema de AEP.

Seleccione **Guardar la API configurada**.

![Almacenamiento de Azure](./images/aep4.png){zoomable="yes"}

Entonces debería ver esto.

![Nueva integración de Adobe I/O](./images/aep5.png){zoomable="yes"}

### Nombre de proyecto

Haga clic en el nombre del proyecto.

![Nueva integración de Adobe I/O](./images/api13.png){zoomable="yes"}

Seleccione **Editar proyecto**.

![Nueva integración de Adobe I/O](./images/api14.png){zoomable="yes"}

Escriba un nombre descriptivo para la integración: `--aepUserLdap-- One Adobe tutorial` y seleccione **Guardar**.

![Nueva integración de Adobe I/O](./images/api15.png){zoomable="yes"}

La configuración del proyecto de Adobe I/O ha finalizado.

![Nueva integración de Adobe I/O](./images/api16.png){zoomable="yes"}

## Pasos siguientes

Ir a [Opción 1: configuración de Postman](./ex7.md){target="_blank"}

Ir a [Opción 2: configuración de PostBuster](./ex8.md){target="_blank"}

Volver a [Introducción](./getting-started.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
