---
title: 'Primeros pasos: Adobe I/O'
description: 'Primeros pasos: Adobe I/O'
kt: 5342
doc-type: tutorial
source-git-commit: 431f7696df12c8c133aced57c0f639c682304dee
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Configuración del proyecto de Adobe I/O

## Creación de un proyecto de Adobe I/O

En este ejercicio, Adobe I/O se utiliza para consultar varios extremos de Adobe. Siga estos pasos para configurar Adobe I/O.

Vaya a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Nueva integración de Adobe I/O](./images/iohome.png){zoomable="yes"}

Asegúrese de seleccionar la instancia correcta en la esquina superior derecha de la pantalla. Su instancia es `--aepImsOrgName--`.
A continuación, seleccione **Crear nuevo proyecto**.

![Nueva integración de Adobe I/O](./images/iocomp.png){zoomable="yes"}

### API de servicios de Firefly

Entonces debería ver esto. Seleccione **+ Agregar al proyecto** y elija **API**.

![Nueva integración de Adobe I/O](./images/adobe_io_access_api.png){zoomable="yes"}

La pantalla debería tener un aspecto similar al siguiente.

![Nueva integración de Adobe I/O](./images/api1.png){zoomable="yes"}

Seleccione **Creative Cloud**, elija **Firefly - Servicios de Firefly** y luego seleccione **Siguiente**.

![Nueva integración de Adobe I/O](./images/api3.png){zoomable="yes"}

Proporcione un nombre para su credencial: `--aepUserLdap-- - One Adobe OAuth credential`y seleccione **Siguiente**.

![Nueva integración de Adobe I/O](./images/api4.png){zoomable="yes"}

Seleccione el perfil predeterminado **Configuración predeterminada de Firefly Services** y seleccione **Guardar la API configurada**.

![Nueva integración de Adobe I/O](./images/api9.png){zoomable="yes"}

Entonces debería ver esto.

![Nueva integración de Adobe I/O](./images/api10.png){zoomable="yes"}

### API de Photoshop Services

Seleccione **+ Agregar al proyecto** y luego seleccione **API**.

![Almacenamiento de Azure](./images/ps2.png){zoomable="yes"}

Seleccione **Creative Cloud** y elija **Photoshop - Servicios de Firefly**. Seleccione **Siguiente**.

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

Seleccione **+ Agregar al proyecto** y luego seleccione **API**.

![Almacenamiento de Azure](./images/aep1.png){zoomable="yes"}

Seleccione **Adobe Experience Platform** y elija **API de Experience Platform**. Seleccione **Siguiente**.

![Almacenamiento de Azure](./images/aep2.png){zoomable="yes"}

Seleccione **Siguiente**.

![Almacenamiento de Azure](./images/aep3.png){zoomable="yes"}

A continuación, debe seleccionar un perfil de producto que defina qué permisos están disponibles para esta integración.

Seleccione **Adobe Experience Platform - Todos los usuarios - PROD**.

Seleccione **Guardar la API configurada**.

![Almacenamiento de Azure](./images/aep4.png){zoomable="yes"}

Entonces debería ver esto.

![Nueva integración de Adobe I/O](./images/aep5.png){zoomable="yes"}

### Nombre de proyecto

Haga clic en el nombre del proyecto.

![Nueva integración de Adobe I/O](./images/api13.png){zoomable="yes"}

Seleccione **Editar proyecto**.

![Nueva integración de Adobe I/O](./images/api14.png){zoomable="yes"}

Escriba un nombre descriptivo para la integración: `--aepUserLdap-- One Adobe tutorial`y seleccione **Guardar**.

![Nueva integración de Adobe I/O](./images/api15.png){zoomable="yes"}

La configuración del proyecto de Adobe I/O ha finalizado.

![Nueva integración de Adobe I/O](./images/api16.png){zoomable="yes"}

## Pasos siguientes

Ir a [Opción 1: configuración de Postman](./ex7.md){target="_blank"}

Ir a [Opción 2: configuración de PostBuster](./ex8.md){target="_blank"}

Volver a [Introducción](./getting-started.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}