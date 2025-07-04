---
title: 'Offer Decisioning: Prueba de la decisión'
description: 'Offer Decisioning: Prueba de la decisión'
kt: 5342
doc-type: tutorial
exl-id: c40b9b8c-9717-403c-bf02-6b8f42a59c05
source-git-commit: 2e856759e1a9b5509ad0632e28b269bcfc4ae861
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 3.3.3 Configuración de una campaña con mensajes en la aplicación

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.3.3.1 Configuración del canal de mensajes en la aplicación

En el menú de la izquierda, ve a **Canales** y luego selecciona **Configuraciones de canal**. Haga clic en **Crear configuración de canal**.

![EnLaAplicación](./images/inapp1.png)

Escriba el nombre: `--aepUserLdap--_In-app_Messages`, seleccione el canal **Mensajería en la aplicación** y, a continuación, habilite las plataformas **Web**, **iOS** y **Android**.

![EnLaAplicación](./images/inapp2.png)

Desplácese hacia abajo y debería ver esto.

![EnLaAplicación](./images/inapp3.png)

Asegúrese de que **Single page** esté habilitado.

Para **Web**, escriba la dirección URL del sitio web que se creó anteriormente como parte del módulo **Introducción**, que tiene este aspecto: `https://dsn.adobe.com/web/--aepUserLdap---XXXX`. No olvides cambiar el **XXXX** por el código único de tu sitio web.

Para **iOS** y **Android**, ingrese `com.adobe.dsn.dxdemo`.

![EnLaAplicación](./images/inapp4.png)

Desplácese hacia arriba y haga clic en **Enviar**.

![EnLaAplicación](./images/inapp5.png)

La configuración del canal ya está lista para utilizarse.

![EnLaAplicación](./images/inapp6.png)

## 3.3.3.2 Configurar una campaña programada para mensajes en la aplicación

En el menú de la izquierda, ve a **Campañas** y luego haz clic en **Crear campaña**.

![EnLaAplicación](./images/inapp7.png)

Seleccione **Programado - Marketing** y haga clic en **Crear**.

![EnLaAplicación](./images/inapp8.png)

Escriba el nombre `--aepUserLdap-- - CitiSignal Fiber Max` y haga clic en **Acciones**.

![EnLaAplicación](./images/inapp9.png)

Haga clic en **+ Agregar acción** y luego seleccione **Mensaje en la aplicación**.

![EnLaAplicación](./images/inapp10.png)

Seleccione la configuración del canal de mensajes en la aplicación que creó en el paso anterior, que se llama: `--aepUserLdap--_In-app_Messages`. Haga clic en **Editar contenido**.

![EnLaAplicación](./images/inapp11.png)

Entonces debería ver esto. Haga clic en **Modal**.

![EnLaAplicación](./images/inapp12.png)

Haga clic en **Cambiar diseño**.

![EnLaAplicación](./images/inapp13.png)

Haga clic en el icono **URL de medios** para seleccionar recursos de los AEM Assets.

![EnLaAplicación](./images/inapp14.png)

Vaya a la carpeta **citisignal-images** y seleccione el archivo de imagen **neon-rabbit.jpg**. Haga clic en **Seleccionar**.

![EnLaAplicación](./images/inapp15.png)

Para el texto **Header**, use: `CitiSignal Fiber Max`.
Para el texto **Body**, use: `Conquer lag with Fiber Max`.

![EnLaAplicación](./images/inapp16.png)

Establezca el **botón #1 texto** en: `Go to Plans`.
Establezca **target** en `com.adobe.dsn.dxdemo://plans`.

Haga clic en **Revisar para activar**.

![EnLaAplicación](./images/inapp17.png)

Haga clic en **Activar**.

![EnLaAplicación](./images/inapp18.png)

El estado de la campaña ahora se establece en **Activando**. La campaña puede tardar un par de minutos en estar activa.

![EnLaAplicación](./images/inapp19.png)

Una vez que el estado haya cambiado a **Activo**, puede probar la campaña.

![EnLaAplicación](./images/inapp20.png)

## 3.3.3.3: probar la campaña de mensajería en la aplicación en dispositivos móviles

En el dispositivo móvil, abra la aplicación. Después de iniciar la aplicación, debería ver el nuevo mensaje en la aplicación. Haga clic en el botón **Ir a Planes**.

![EnLaAplicación](./images/inapp21.png)

Luego se le redirigirá a la página **Planes**.

![EnLaAplicación](./images/inapp22.png)

## Pasos siguientes

Ir a [Resumen y beneficios](./summary.md){target="_blank"}

Volver a [Adobe Journey Optimizer: mensajes push y en la aplicación](ajopushinapp.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
