---
title: 'Base: configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: recopilación de datos web del lado del cliente'
description: 'Base: configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: recopilación de datos web del lado del cliente'
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: c4ebca8d-93e0-4056-8553-c0d7e342beca
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 2%

---

# 1.4 Recopilación de datos web del lado del cliente

## 1.4.1 Validar los datos de la solicitud

### Instalación de Adobe Experience Platform Debugger

Experience Platform Debugger es una extensión disponible para exploradores Chrome y Firefox que le ayuda a ver la tecnología de Adobe implementada en sus páginas web. Descargue la versión de su navegador preferido:

- [Extensión de Firefox](https://addons.mozilla.org/es/firefox/addon/adobe-experience-platform-dbg/)

- [Extensión de Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Si nunca antes ha utilizado Debugger (y este es diferente del anterior Debugger de Adobe Experience Cloud), es posible que desee ver este vídeo de información general de cinco minutos:

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

Dado que va a cargar el sitio web de demostración en modo incógnito, debe asegurarse de que el depurador de Experience Platform también esté disponible en modo incógnito. Para ello, vaya a **chrome://extensions** en el explorador y abra la extensión de Experience Platform Debugger.

Compruebe que estas 2 configuraciones están habilitadas:

- Modo de desarrollador
- Permitir en incógnito

![Página de inicio de EXP News](./images/ext1.png)

### Abra el sitio web de demostración

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión en Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![DSN](../module0/images/web8.png)

En el **Pantallas** página, haga clic en **Ejecutar**.

![DSN](./images/web2.png)

Verá que su sitio web de demostración se abre. Seleccione la dirección URL y cópiela en el portapapeles.

![DSN](../module0/images/web3.png)

Abra una nueva ventana del explorador incógnito.

![DSN](../module0/images/web4.png)

Pegue la dirección URL del sitio web de la demostración, que copió en el paso anterior. A continuación, se le pedirá que inicie sesión con su Adobe ID.

![DSN](../module0/images/web5.png)

Seleccione su tipo de cuenta y complete el proceso de inicio de sesión.

![DSN](../module0/images/web6.png)

Verá su sitio web cargado en una ventana del navegador incógnito. Para cada demostración, tendrá que usar una ventana nueva del explorador incógnito para cargar la URL de su sitio web de demostración.

![DSN](../module0/images/web7.png)

### Use el depurador de Experience Platform para ver las llamadas que se dirigen a Edge

Asegúrese de que el sitio web de demostración está abierto y haga clic en el icono de extensión de Experience Platform Debugger .

![Página de inicio de EXP News](./images/ext2.png)

Debugger se abrirá y mostrará los detalles de la implementación creada en la propiedad de recopilación de datos de Adobe Experience Platform. Recuerde que está depurando la extensión y las reglas que acaba de editar.

Haga clic en el **[!UICONTROL Iniciar sesión]** en la parte superior derecha para autenticarse. Si ya tiene una pestaña del explorador abierta con la interfaz de recopilación de datos de Adobe Experience Platform, el paso de autenticación será automático y no tendrá que introducir de nuevo su nombre de usuario y contraseña.

![AEP Debugger](./images/validate2.png)

Pulse el botón de recarga del sitio web de la demostración para conectar el depurador a esa pestaña específica.

![AEP Debugger](./images/validate2a.png)

Confirme que Debugger es **[!UICONTROL Conectado a la página principal]** como se muestra arriba y luego haga clic en el botón **[!UICONTROL bloquear]** para bloquear Debugger en el sitio web de demostración. Si no lo hace, Debugger seguirá cambiando para exponer los detalles de implementación de la pestaña del explorador que esté centrada, lo que puede resultar confuso.

![AEP Debugger](./images/validate3.png)

A continuación, vaya a cualquier página del sitio web de demostración como, por ejemplo, la **Hombres** página de categoría.

![Extensión del SDK web de AEP Debugger](./images/validate4.png)

Ahora haga clic en **[!UICONTROL SDK web de Experience Platform]** en el panel de navegación izquierdo, para ver la **[!UICONTROL Solicitudes de red]**.

Cada solicitud contiene un **[!UICONTROL events]** fila.

![Extensión del SDK web de AEP Debugger](./images/validate5.png)

Haga clic en para abrir el **[!UICONTROL events]** fila. Observe cómo puede ver el **web.webpagedetails.pageViews** , así como otras variables listas para usar que cumplan con la **SDK web ExperienceEvent XDM** formato.

![Valor de eventos](./images/validate8.png)

Estos tipos de detalles de solicitud también se pueden ver en la pestaña Red . Filtros para solicitudes con **interactuar** para localizar las solicitudes enviadas por el SDK web. Puede encontrar todos los detalles de la carga útil XDM en los encabezados de carga útil de solicitud:

![Ficha Red](./images/validate9.png)

Paso siguiente: [1.5 Implementar Adobe Analytics y Adobe Audience Manager](./ex5.md)

[Volver al módulo 1](./data-ingestion-launch-web-sdk.md)

[Volver a todos los módulos](./../../overview.md)
