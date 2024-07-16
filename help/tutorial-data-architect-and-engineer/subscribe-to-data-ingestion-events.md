---
title: Suscripción a eventos de ingesta de datos
seo-title: Subscribe to data ingestion events | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Suscripción a eventos de ingesta de datos
description: En esta lección, debe suscribirse a los eventos de ingesta de datos configurando un gancho web con Adobe Developer Console y una herramienta de desarrollo de ganchos web en línea. Utilizará estos eventos para monitorizar el estado de los trabajos de ingesta de datos en las lecciones posteriores.
role: Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-subscribe-to-data-ingestion-events.jpg
exl-id: f4b90832-4415-476f-b496-2f079b4fcbbc
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Suscripción a eventos de ingesta de datos

<!--25min-->

En esta lección, debe suscribirse a los eventos de ingesta de datos configurando un gancho web con Adobe Developer Console y una herramienta de desarrollo de ganchos web en línea. Utilizará estos eventos para monitorizar el estado de los trabajos de ingesta de datos en las lecciones posteriores.

**Los ingenieros de datos** querrán suscribirse a eventos de ingesta de datos fuera de este tutorial.
**Los arquitectos de datos** _pueden omitir esta lección_ e ir a la [lección de ingesta por lotes](ingest-batch-data.md).

## Permisos necesarios

En la lección [Configurar permisos](configure-permissions.md), ha configurado todos los controles de acceso necesarios para completar esta lección, en concreto:

<!--* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

>[!IMPORTANT]
>
> Estas notificaciones activadas por los eventos de ingesta de datos se aplicarán a _todas las zonas protegidas_, no solo a `Luma Tutorial`. También puede ver notificaciones procedentes de otros eventos de ingesta de datos en su cuenta.


## Configurar un webhook

En este ejercicio, crearemos un webhook usando una herramienta en línea llamada webhook.site (siéntase libre de sustituir cualquier otra herramienta de desarrollo de webhook que prefiera usar):

1. En otra ficha del explorador, abra el sitio web [https://webhook.site/](https://webhook.site/)
1. Se le asigna una dirección URL única, que debe marcar, a medida que vuelva a ella más adelante en las lecciones de ingesta de datos:

   ![Gancho de Web.Sitio](assets/ioevents-webhook-home.png)
1. Seleccione el botón **Editar** en la barra de navegación superior
1. Como cuerpo de la respuesta, escriba `$request.query.challenge$`. Las notificaciones de eventos de Adobe I/O que configuramos más adelante en esta lección envían un desafío al webhook y requieren que se incluya en el cuerpo de respuesta.
1. Seleccione el botón **Guardar**

   ![Editar la respuesta](assets/ioevents-webhook-editResponse.png)

## Configurar

1. En otra pestaña del explorador, abra [Adobe Developer Console](https://console.adobe.io/)
1. Abra su `Luma Tutorial API Project`
1. Seleccione el botón **[!UICONTROL Agregar al proyecto]** y luego seleccione **[!UICONTROL Evento]**

   ![Agregar evento](assets/ioevents-addEvents.png)
1. Filtre la lista seleccionando **[!UICONTROL Experience Platform]**
1. Seleccionar **[!UICONTROL notificaciones de plataforma]**
1. Seleccione el botón **[!UICONTROL Siguiente]**
   ![Agregar las notificaciones](assets/ioevents-addNotifications.png)
1. Seleccionar todos los eventos
1. Seleccione el botón **[!UICONTROL Siguiente]**
   ![Seleccionar las suscripciones](assets/ioevents-addSubscriptions.png)
1. En la siguiente pantalla para configurar credenciales, vuelva a seleccionar el botón **[!UICONTROL Siguiente]**
   ![Omitir la pantalla de credenciales](assets/ioevents-clickNext.png)
1. Como **[!UICONTROL nombre de registro de evento]**, escriba `Platform notifications`
1. Desplácese hacia abajo y seleccione para abrir la sección **[!UICONTROL Webhook]**
1. Como la **[!UICONTROL URL de webhook]**, pegue el valor del campo **Su URL única** de webhook.site
1. Seleccione el botón **[!UICONTROL Guardar eventos configurados]**
   ![Guardar los eventos](assets/ioevents-addWebhook.png)
1. Espere a que se guarde la configuración y debería ver que el evento `Platform notifications` está Activo con los detalles del webhook y que no hay mensajes de error
   ![Configuración guardada](assets/ioevents-webhookConfigured.png)
1. Cambie a la pestaña webhook.site y debería ver la primera solicitud al webhook, resultante de la validación de la configuración de Developer Console:
   ![Primera solicitud en webhook.site](assets/ioevents-webhook-firstRequest.png)

Eso es todo por ahora; aprenderá más sobre estas notificaciones en las próximas lecciones cuando ingrese datos.

## Recursos adicionales

* [Gancho de Web.Sitio](https://webhook.site/)
* [Documentación de notificaciones de ingesta de datos](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html)
* [Introducción a la documentación de eventos de Adobe I/O](https://www.adobe.io/apis/experienceplatform/events/docs.html)

¡Bien, finalmente empecemos [a ingerir datos](ingest-batch-data.md)!
