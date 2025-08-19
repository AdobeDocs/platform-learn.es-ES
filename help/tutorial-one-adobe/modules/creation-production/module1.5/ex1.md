---
title: Introducción a Frame.io
description: Introducción a Frame.io
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 09e8fdfd-e02f-43ff-a4f4-fa92eb3f01a3
source-git-commit: 917ebcd2dd5d8316413a183bd2c1a048c090428c
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 1.5.1 Introducción a Frame.io

>[!NOTE]
>
> La siguiente captura de pantalla muestra un entorno específico que se está utilizando. Cuando revise este tutorial, es muy probable que su entorno tenga un nombre diferente. Cuando se registró en este tutorial, se le proporcionaron los detalles del entorno que debe utilizar, siga esas instrucciones.

Vaya a [https://next.frame.io/](https://next.frame.io/). Asegúrese de haber iniciado sesión en el entorno `--aepImsOrgName--`.

![Frame.io](./images/frameio1.png)

Si no ha iniciado sesión en el entorno derecho, haga clic en el logotipo de en la esquina inferior izquierda y haga clic en para seleccionar el entorno que necesita utilizar.

![Frame.io](./images/frameio2.png)

## 1.5.1.1: crear su área de trabajo y proyecto

Haga clic en **+ Nuevo Workspace**.

![Frame.io](./images/frameio3.png)

Para el nombre del área de trabajo, utilice: `--aepUserLdap--`. Haga clic en **Guardar**.

![Frame.io](./images/frameio4.png)

Se creará el espacio de trabajo. A continuación, debe crear un nuevo proyecto. Haga clic en **+ Nuevo proyecto**.

![Frame.io](./images/frameio5.png)

Seleccione **En blanco** y use el nombre `CitiSignal`. Haga clic en **Crear nuevo proyecto**.

![Frame.io](./images/frameio6.png)

El proyecto se ha creado. Ahora debe cargar los recursos en el proyecto. Haga clic en **Cargar**.

![Frame.io](./images/frameio7.png)

Descargue estos archivos: [https://tech-insiders.s3.us-west-2.amazonaws.com/Frame.io_Assets.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/Frame.io_Assets.zip) en su escritorio y descomprímalo en él.

![Frame.io](./images/frameio8.png)

Seleccione todos los archivos y haga clic en **Abrir**.

>[!NOTE]
>
>Como puede ver en la captura de pantalla, la carpeta **Efectos de sonido** no está seleccionada en este momento. Esto se debe a que la carga manual no admite la carga de carpetas. En un par de minutos instalará la aplicación Frame.io Transfer, que utilizará para cargar esa carpeta y sus archivos.

![Frame.io](./images/frameio9.png)

Después de un par de minutos, verá que sus archivos están disponibles en Frame.io.

![Frame.io](./images/frameio10.png)

Ahora ha cargado archivos manualmente, pero existe una forma mejor y más rápida de cargar y descargar archivos desde y hacia Frame.io. La mejor manera de hacerlo es utilizar la aplicación Frame.io Transfer.

## 1.5.1.2 Descargar y configurar la aplicación de transferencia Frame.io

Vaya a [https://frame.io/transfer](https://frame.io/transfer) y descargue la versión para su equipo.

![Frame.io](./images/frameio11.png)

Instale la aplicación y ábrala.

![Frame.io](./images/frameio12.png)

Cuando se abre la aplicación, es necesario que inicie sesión. Haga clic en **iniciar sesión**.

![Frame.io](./images/frameio13.png)

Escriba la dirección de correo electrónico de su cuenta de Adobe y haga clic en **Vamos**.

![Frame.io](./images/frameio14.png)

Tras autenticarse correctamente, haga clic en **Abrir aplicación Frame.io Transfer**.

![Frame.io](./images/frameio15.png)

Entonces debería ver esto. Para seleccionar el entorno correcto, haga clic en para abrir la lista desplegable.

![Frame.io](./images/frameio16.png)

Seleccione el entorno que necesita utilizar para este tutorial, que es `--aepImsOrgName--`.

![Frame.io](./images/frameio17.png)

A continuación, debería ver el espacio de trabajo y el proyecto creados anteriormente, junto con los archivos cargados manualmente.

Haga clic en **Cargar**.

![Frame.io](./images/frameio18.png)

Vaya a la carpeta que utilizó anteriormente, que contiene los archivos descomprimidos que descargó anteriormente. Seleccione la carpeta **Efectos de sonido** y haga clic en **Cargar**.

![Frame.io](./images/frameio19.png)

A continuación, se cargarán sus archivos.

![Frame.io](./images/frameio20.png)

Una vez cargada, verá que la nueva carpeta está disponible en Frame.io.

![Frame.io](./images/frameio21.png)

## Pasos siguientes

Ir a [1.5.2 aprobaciones con Frame.io](./ex2.md){target="_blank"}

Vuelva a [Optimizar el flujo de trabajo con Frame.io](./frameio.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
