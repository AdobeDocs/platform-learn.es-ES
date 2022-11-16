---
title: Validación de implementaciones de SDK web con Experience Platform Debugger
description: Obtenga información sobre cómo validar la implementación del SDK web de Platform con Adobe Experience Platform Debugger. Esta lección forma parte del tutorial Implementar Adobe Experience Cloud con SDK web .
feature: Debugger
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 5%

---

# Validación de implementaciones de SDK web con Experience Platform Debugger

Obtenga información sobre cómo validar la implementación del SDK web de Platform con Adobe Experience Platform Debugger.

Experience Platform Debugger es una extensión disponible para exploradores Chrome y Firefox que le ayuda a ver la tecnología de Adobe implementada en sus páginas web. Descargue la versión de su navegador preferido:

* [Extensión de Firefox](https://addons.mozilla.org/es/firefox/addon/adobe-experience-platform-dbg/)
* [Extensión de Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Si nunca antes ha utilizado el depurador (y este es diferente del anterior Adobe Experience Cloud Debugger), es posible que desee ver este vídeo de descripción general de cinco minutos:

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

En esta lección, debe usar la variable [Extensión de Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) para reemplazar la propiedad tag codificada en la variable [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) con su propia propiedad.

Esta técnica se denomina cambio de entorno y será útil posteriormente, cuando trabaje con etiquetas en su propio sitio web. Puede cargar el sitio web de producción en su explorador, pero con su *desarrollo* entorno de etiquetas. Esta capacidad le permite realizar y validar cambios con seguridad en las etiquetas de forma independiente de las revisiones de código normales. Después de todo, esta separación de las versiones de etiquetas de marketing y las revisiones de código normales es una de las principales razones por las que los clientes utilizan etiquetas.

## Objetivos de aprendizaje

Al final de esta lección, podrá utilizar el depurador para:

* Cargar una biblioteca de etiquetas alternativa
* Validar que el objeto XDM captura y envía datos como se espera en la red perimetral

## Requisitos previos

Está familiarizado con las etiquetas de recopilación de datos y con el [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;} y han completado las siguientes lecciones anteriores en el tutorial:

* [Configure los permisos](configure-permissions.md)
* [Configuración de un esquema XDM](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)
* [Configurar un conjunto de datos](configure-datastream.md)
* [Extensión del SDK web instalada en la propiedad tag](install-web-sdk.md)
* [Creación de elementos de datos](create-data-elements.md)
* [Crear una regla de etiqueta](create-tag-rule.md)


## Cargar bibliotecas de etiquetas alternativas con Debugger

Este tutorial utiliza una versión de [Sitio web de la demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Abra la página principal y añádala como marcador.

![Página de inicio de Luma](assets/validate-luma-site.png)

Experience Platform Debugger tiene una excelente función que le permite reemplazar una biblioteca de etiquetas existente por otra diferente. Esta técnica es útil para la validación y nos permite omitir muchos pasos de implementación en este tutorial.

1. Asegúrese de que el sitio de Luma está abierto y seleccione el icono de extensión de Experience Platform Debugger .
1. Debugger se abrirá y mostrará algunos detalles de la implementación codificada, que no está relacionada con este tutorial (puede que tenga que volver a cargar el sitio de Luma después de abrir Debugger)
1. Confirme que Debugger es &quot;**[!UICONTROL Conectado a Luma]**&quot; como se muestra a continuación y seleccione &quot;**[!UICONTROL bloquear]**&quot; para bloquear Debugger en el sitio de Luma.
1. Seleccione el **[!UICONTROL Iniciar sesión]** e inicie sesión en Adobe Experience Cloud con su ID de Adobe.
1. Ahora vaya a **[!UICONTROL Etiquetas de Experience Platform]** en la navegación izquierda

   ![Pantalla de etiqueta de Debugger](assets/validate-launch-screen.png)

1. Seleccione el **[!UICONTROL Configuración]** ficha
1. A la derecha de donde se muestra la variable **[!UICONTROL Códigos incrustados de página]**, abra el **[!UICONTROL Acciones]** y seleccione **[!UICONTROL Reemplazar]**

   ![Seleccione Acciones > Reemplazar](assets/validate-switch-environment.png)

1. Como está autenticado, Debugger va a incorporar los entornos y las propiedades de etiquetas disponibles. Seleccione su `Web SDK Course` property
1. Seleccione su `Development` entorno
1. Seleccione el **[!UICONTROL Aplicar]** botón

   ![Seleccionar la propiedad de etiqueta alternativa](assets/validate-switch-selection.png)

1. El sitio web de Luma ahora se vuelve a cargar _con la propiedad tag_.

   ![se ha reemplazado la propiedad tag](assets/validate-switch-success.png)

A medida que continúe con el tutorial, utilizará esta técnica de asignación del sitio de Luma a su propia propiedad de etiqueta para validar la implementación del SDK web de Platform. Cuando empiece a utilizar etiquetas en el sitio web de producción, puede utilizar esta misma técnica para validar los cambios.

## Validar la implementación en Experience Platform Debugger

Puede utilizar Debugger para validar la implementación del SDK web de Platform y ver los datos enviados a Platform Edge Network:

1. Vaya a **[!UICONTROL Resumen]** en el panel de navegación izquierdo, para ver los detalles de la propiedad tag

   ![Ficha Resumen](assets/validate-summary.png)

1. Ahora vaya a **[!UICONTROL SDK web de Experience Platform]** en el panel de navegación izquierdo para ver la **[!UICONTROL Solicitudes de red]**
1. Abra el **[!UICONTROL events]** row (no se preocupe si esta captura de pantalla muestra más solicitudes que las suyas, incluye solicitudes de lecciones futuras y puede ignorar por ahora)

   ![Solicitud de SDK web de Adobe Experience Platform](assets/validate-aep-screen.png)

1. Observe cómo podemos ver el `web.webpagedetails.pageView` tipo de evento especificado en nuestra [!UICONTROL Enviar evento] y otras variables listas para usar que cumplan con el `AEP Web SDK ExperienceEvent Mixin` format

   ![Detalles del evento](assets/validate-event-pageViews.png)

1. Desplácese hacia abajo hasta el `web` seleccione para abrirlo e inspeccionar el `webPageDetails.name`, `webPageDetails.server`y `webPageDetails.siteSection`. Deben coincidir con las variables de capa de datos digitalData correspondientes de la página principal

   ![Ficha Red](assets/validate-xdm-content.png)

También puede validar los detalles del mapa de identidad:

1. Inicie sesión en el sitio de Luma con las credenciales `test@adobe.com`/`test`

1. Vuelva a la [página principal de Luma](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Abra el **[!UICONTROL SDK web de Experience Platform]** en la sección de navegación izquierda

   ![SDK web en Debugger](assets/identity-debugger-websdk-dark.png)

1. Seleccione el **[!UICONTROL events]** fila para abrir detalles en una ventana emergente

   ![SDK web en Debugger](assets/identity-deugger-websdk-event-dark.png)

1. Busque la variable **identityMap** en la ventana emergente. Aquí debería ver `lumaCrmId` con tres claves de authenticationState, id y primary:
   ![SDK web en Debugger](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)


## Validación con herramientas de desarrollo del explorador

Estos tipos de detalles de solicitud también están visibles en las herramientas para desarrolladores web del explorador **Red** (suponiendo que el sitio web esté cargando la biblioteca de etiquetas).

1. Abra las herramientas para desarrolladores web del explorador **Red** y vuelva a cargar la página. Filtre las llamadas con `/ee` para localizar la llamada, selecciónela y, a continuación, busque en la **Encabezados** y **Carga útil** ficha

   ![Ficha Red](assets/validate-dev-console.png)

1. Vaya a la **Respuesta** y observe cómo se incluye el valor ECID en la respuesta. Copie este valor tal como lo usará para validar la información de perfil en el siguiente ejercicio

   ![Ficha Red](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   >    Es posible que no vea la misma cantidad de solicitudes de carga útil que en la captura de pantalla anterior. Esta disparidad se debe a que las lecciones futuras para [configuración de Target](setup-target.md) se completaron en el momento en que se tomó la captura de pantalla. Por ahora, puede ignorar esta diferencia.

Con un objeto XDM que se activa en una página y con el conocimiento de cómo validar la recopilación de datos, está listo para configurar las aplicaciones de Adobe individuales mediante el SDK web de Platform.

[Siguiente: ](setup-experience-platform.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK web de Adobe Experience Platform. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
