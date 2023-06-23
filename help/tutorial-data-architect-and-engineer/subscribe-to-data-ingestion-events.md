---
title: Suscripción a eventos de ingesta de datos
seo-title: Subscribe to data ingestion events | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Suscripción a eventos de ingesta de datos
description: En esta lección, debe suscribirse a los eventos de ingesta de datos configurando un webhook con la consola de Adobe Developer y una herramienta de desarrollo de webhook en línea. Utilizará estos eventos para monitorizar el estado de los trabajos de ingesta de datos en las lecciones posteriores.
role: Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-subscribe-to-data-ingestion-events.jpg
exl-id: f4b90832-4415-476f-b496-2f079b4fcbbc
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 1%

---

# Suscripción a eventos de ingesta de datos

<!--25min-->

En esta lección, debe suscribirse a los eventos de ingesta de datos configurando un webhook con la consola de Adobe Developer y una herramienta de desarrollo de webhook en línea. Utilizará estos eventos para monitorizar el estado de los trabajos de ingesta de datos en las lecciones posteriores.

**Ingenieros de datos** querrá suscribirse a eventos de ingesta de datos fuera de este tutorial.
**Arquitectos de datos** _Puede omitir esta lección_ y vaya a la [lección de ingesta por lotes](ingest-batch-data.md).

## Permisos necesarios

En el [Configuración de permisos](configure-permissions.md) Esta lección, ha configurado todos los controles de acceso necesarios para completar esta lección, en concreto:

<!--* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

>[!IMPORTANT]
>
> Estas notificaciones activadas por los eventos de ingesta de datos se aplicarán a _todas las zonas protegidas_, no solo su `Luma Tutorial`. También puede ver notificaciones procedentes de otros eventos de ingesta de datos en su cuenta.


## Configurar un webhook

En este ejercicio, crearemos un webhook usando una herramienta en línea llamada webhook.site (siéntase libre de sustituir cualquier otra herramienta de desarrollo de webhook que prefiera usar):

1. En otra pestaña del explorador, abra el sitio web [https://webhook.site/](https://webhook.site/)
1. Se le asigna una dirección URL única, que debe marcar, a medida que vuelva a ella más adelante en las lecciones de ingesta de datos:

   ![Webhook.site](assets/ioevents-webhook-home.png)
1. Seleccione el **Editar** botón en la barra de navegación superior
1. Como cuerpo de la respuesta, introduzca. `$request.query.challenge$`. Las notificaciones de eventos de Adobe I/O que configuramos más adelante en esta lección envían un desafío al webhook y requieren que se incluya en el cuerpo de respuesta.
1. Seleccione el botón **Guardar**

   ![Editar la respuesta](assets/ioevents-webhook-editResponse.png)

## Configuración de

1. En otra pestaña del explorador, abra [Consola de Adobe Developer](https://console.adobe.io/)
1. Abra su `Luma Tutorial API Project`
1. Seleccione el **[!UICONTROL Agregar al proyecto]** y luego seleccione **[!UICONTROL Evento]**

   ![Añadir evento](assets/ioevents-addEvents.png)
1. Filtre la lista seleccionando **[!UICONTROL Experience Platform]**
1. Seleccionar **[!UICONTROL Notificaciones de Platform]**
1. Seleccione el **[!UICONTROL Siguiente]** botón
   ![Añadir las notificaciones](assets/ioevents-addNotifications.png)
1. Seleccionar todos los eventos
1. Seleccione el **[!UICONTROL Siguiente]** botón
   ![Seleccionar las suscripciones](assets/ioevents-addSubscriptions.png)
1. En la siguiente pantalla para configurar credenciales, seleccione la **[!UICONTROL Siguiente]** botón de nuevo
   ![Omitir la pantalla de credenciales](assets/ioevents-clickNext.png)
1. Como el **[!UICONTROL Nombre de registro del evento]**, introduzca `Platform notifications`
1. Desplácese hacia abajo y seleccione para abrir **[!UICONTROL Webhook]** sección
1. Como el **[!UICONTROL URL de webhook]**, pegue el valor de **Su URL única** campo de webhook.site
1. Seleccione el **[!UICONTROL Guardar eventos configurados]** botón
   ![Guarde los eventos](assets/ioevents-addWebhook.png)
1. Espere a que se guarde la configuración y debería ver que su `Platform notifications` El evento está activo con los detalles del webhook y sin mensajes de error
   ![Configuración guardada](assets/ioevents-webhookConfigured.png)
1. Cambie a la pestaña webhook.site y debería ver la primera solicitud al webhook, resultante de la validación de la configuración de Developer Console:
   ![Primera solicitud en webhook.site](assets/ioevents-webhook-firstRequest.png)

Eso es todo por ahora; aprenderá más sobre estas notificaciones en las próximas lecciones cuando ingrese datos.

## Recursos adicionales

* [Webhook.site](https://webhook.site/)
* [Documentación de notificaciones de ingesta de datos](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html)
* [Introducción a la documentación de eventos de Adobe I/O](https://www.adobe.io/apis/experienceplatform/events/docs.html)

Ok, finalmente vamos a empezar [ingesta de datos](ingest-batch-data.md)!
