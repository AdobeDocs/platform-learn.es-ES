---
title: Implemente su código y publique su aplicación en privado
description: Implemente su código y publique su aplicación en privado
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 5a77ccdd-4000-4fb7-b696-dec40d01b41b
source-git-commit: fe162f285d67cc2a37736f80715a5c5717835e95
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 1%

---

# 1.6.4 Implementar el código y publicar la aplicación de forma privada

La publicación de la aplicación de forma privada significa que la aplicación está disponible en GenStudio for Performance Marketing sin tener que utilizar el parámetro de cadena de consulta.

## 1.6.4.1 Publicar su aplicación

Vaya a [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects){target="_blank"}.

>[!NOTE]
>
> La siguiente captura de pantalla muestra una organización específica seleccionada. Cuando vaya a través de este tutorial, es muy probable que su organización tenga un nombre diferente. Cuando se registró en este tutorial, se le proporcionaron los detalles del entorno que debe utilizar, siga esas instrucciones.

Abra el proyecto de Adobe IO con App Builder, que debe tener el nombre `--aepUserLdap-- GSPeM EXT`.

![Extensibilidad GSPeM](./images/gspemextpub1.png)

Ir a **Producción**.

![Extensibilidad GSPeM](./images/gspemextpub2.png)

Haga clic en **Publicar en privado**.

![Extensibilidad GSPeM](./images/gspemextpub3.png)

A continuación, debe rellenar una serie de campos.

![Extensibilidad GSPeM](./images/gspemextpub4.png)

Rellene los campos siguientes de esta manera:

- **Título de la aplicación**: `--aepUserLdap-- - External DAM AWS S3`.
- **Descripción de la aplicación**: `External DAM AWS S3`
- **Correo electrónico de contacto**: escribe tu dirección de correo electrónico
- **Icono de la aplicación**: descarga y usa esta imagen: [Imagen de S3](./images/s3.jpeg)
- **Nota para el revisor**: DAM externo AWS S3

Haga clic en **Enviar**.

![Extensibilidad GSPeM](./images/gspemextpub5.png)

Haga clic en **Enviar**.

![Extensibilidad GSPeM](./images/gspemextpub6.png)

## 1.6.4.2 Aprobar su aplicación

Una vez que un desarrollador envía una nueva aplicación para su publicación, se notifica a los administradores del sistema de su organización y se les pide que revisen y aprueben.

Si eres administrador del sistema, recibirás este correo electrónico y podrás hacer clic en **Mi intercambio** para iniciar el proceso.

![Extensibilidad GSPeM](./images/gspemextpub7.png)

En **Adobe Exchange**, se muestran las aplicaciones de App Builder y la aplicación que acaba de enviarse está pendiente de revisión. Haga clic en el botón **Revisar** de la aplicación `--aepUserLdap-- - External DAM AWS S3`.

![Extensibilidad GSPeM](./images/gspemextpub8.png)

Agregue un comentario y haga clic en **Aprobar**.

![Extensibilidad GSPeM](./images/gspemextpub9.png)

La aplicación ya está aprobada y funcionará automáticamente en GenStudio for Performance Marketing, sin necesidad de especificar el parámetro de cadena de consulta.

## Pasos siguientes

Ir a [Resumen y beneficios](./summary.md){target="_blank"}

Volver a [GenStudio for Performance Marketing - Extensibilidad](./genstudioext.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
