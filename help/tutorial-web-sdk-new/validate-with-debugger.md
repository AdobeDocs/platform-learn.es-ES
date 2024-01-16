---
title: Validación de implementaciones de SDK web con Experience Platform Debugger
description: Obtenga información sobre cómo validar la implementación del SDK web de Platform con Adobe Experience Platform Debugger. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK,Tags,Debugger
source-git-commit: 904581df85df5d8fc4f36a4d47a37b03ef92d76f
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 1%

---

# Validación de implementaciones de SDK web con Experience Platform Debugger

Obtenga información sobre cómo validar la implementación del SDK web de Platform con Adobe Experience Platform Debugger.

Experience Platform Debugger es una extensión disponible para los navegadores Chrome y Firefox que permite ver la tecnología de Adobe implementada en las páginas web. Descargue la versión para su navegador preferido:

* [Extensión de Firefox](https://addons.mozilla.org/es/firefox/addon/adobe-experience-platform-dbg/)
* [Extensión de Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Si nunca antes ha utilizado Debugger (y este es diferente del antiguo Adobe Experience Cloud Debugger), puede que desee ver este vídeo de información general de cinco minutos:

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on)

En esta lección, se usa el [Extensión de Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) para reemplazar la propiedad de etiqueta codificada en la variable [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) con su propia propiedad.

Esta técnica se denomina cambio de entorno y será útil más adelante, cuando trabaje con etiquetas en su propio sitio web. Puede cargar el sitio web de producción en su explorador, pero con su *desarrollo* entorno de etiquetas. Esta capacidad permite realizar y validar cambios de etiquetas con seguridad en de forma independiente de las revisiones de código normales. Después de todo, esta separación de las versiones de etiquetas de marketing de las versiones de código normal es una de las principales razones por las que los clientes utilizan etiquetas.

## Objetivos de aprendizaje

Al final de esta lección, podrá utilizar Debugger para lo siguiente:

* Cargar una biblioteca de etiquetas alternativa
* Valide que el evento XDM del lado del cliente esté capturando y enviando datos según lo esperado a Platform Edge Network
* Habilite el seguimiento de Edge para ver las solicitudes del lado del servidor enviadas por Platform Edge Network
* Inicie una sesión de Adobe Experience Platform Assurance para ver el ID de Experience Cloud generado por Platform Edge Network

## Requisitos previos

Está familiarizado con las etiquetas de recopilación de datos y las [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} y haya completado las siguientes lecciones anteriores en el tutorial:

* [Configuración de un esquema XDM](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)
* [Configuración de una secuencia de datos](configure-datastream.md)
* [Extensión del SDK web instalada en la propiedad de etiqueta](install-web-sdk.md)
* [Creación de elementos de datos](create-data-elements.md)
* [Creación de identidades](create-identities.md)
* [Creación de una regla de etiqueta](create-tag-rule.md)

## Carga de bibliotecas de etiquetas alternativas con Debugger

Este tutorial utiliza una versión alojada públicamente de [Sitio web de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Abra la página principal y márquela como favorito.

![Página principal de Luma](assets/validate-luma-site.png)

Experience Platform Debugger tiene una característica interesante que le permite reemplazar una biblioteca de etiquetas existente por otra diferente. Esta técnica es útil para la validación y nos permite omitir muchos pasos de implementación en este tutorial.

1. Asegúrese de tener el sitio de Luma abierto y seleccionar el icono de extensión de Experience Platform Debugger.
1. Debugger se abrirá y mostrará algunos detalles de la implementación codificada, que no están relacionados con este tutorial (puede que tenga que volver a cargar el sitio de Luma después de abrir Debugger).
1. Confirme que Debugger es &quot;**[!UICONTROL Conectado a Luma]**&quot; como se muestra a continuación y, a continuación, seleccione el &quot;**[!UICONTROL bloquear]**&quot; para bloquear Debugger en el sitio de Luma.
1. Seleccione el **[!UICONTROL Iniciar sesión]** e inicie sesión en Adobe Experience Cloud con su ID de Adobe.
1. Ahora, vaya a **[!UICONTROL Etiquetas de Experience Platform]** en el panel de navegación izquierdo

   ![Pantalla de etiquetas de Debugger](assets/validate-launch-screen.png)

1. Seleccione el **[!UICONTROL Configuración]** pestaña
1. A la derecha de donde muestra el **[!UICONTROL Códigos incrustados de página]**, abra el **[!UICONTROL Acciones]** y seleccione. **[!UICONTROL Reemplazar]**

   ![Seleccione Acciones > Reemplazar](assets/validate-switch-environment.png)

1. Dado que se ha autenticado, Debugger va a extraer las propiedades y entornos de etiquetas disponibles. Seleccione su propiedad; en este caso `Web SDK Course 3`
1. Seleccione su `Development` entorno
1. Seleccione el **[!UICONTROL Aplicar]** botón

   ![Seleccione la propiedad de etiqueta alternativa](assets/validate-switch-selection.png)

1. El sitio web de Luma se volverá a cargar _con su propia propiedad de etiquetas_.

   ![propiedad de etiqueta reemplazada](assets/validate-switch-success.png)

A medida que continúa con el tutorial, utilizará esta técnica de asignación del sitio de Luma a su propia propiedad de etiquetas para validar la implementación del SDK web de Platform. Cuando empiece a utilizar etiquetas en el sitio web de producción, puede utilizar esta misma técnica para validar los cambios.

## Validar solicitudes de red del lado del cliente con Experience Platform Debugger

Puede utilizar Debugger para validar las señalizaciones del lado del cliente activadas desde la implementación del SDK web de Platform para ver los datos enviados a Platform Edge Network:

1. Ir a **[!UICONTROL Resumen]** en el panel de navegación izquierdo, para ver los detalles de la propiedad de etiquetas

   ![Pestaña Resumen](assets/validate-summary.png)

1. Ahora, vaya a **[!UICONTROL SDK web de Experience Platform]** en el panel de navegación izquierdo para ver la **[!UICONTROL Solicitudes de red]**
1. Abra el **[!UICONTROL eventos]** reñir

   ![Solicitud de SDK web de Adobe Experience Platform](assets/validate-aep-screen.png)

1. Observe cómo puede ver el `web.webpagedetails.pageView` tipo de evento especificado en su [!UICONTROL Actualizar variable] acción y otras variables listas para usar que se ajustan a la variable `AEP Web SDK ExperienceEvent` grupo de campos

   ![Detalles del evento](assets/validate-event-pageViews.png)

1. Desplácese hacia abajo hasta el `web` objeto, seleccione para abrirlo e inspeccionar el `webPageDetails.name`, `webPageDetails.server`, y `webPageDetails.siteSection`. Deben coincidir con el correspondiente `digitalData` variables de capa de datos en la página principal

>[!TIP]
>
> Para ver y comparar `digitalData` capa de datos en la página principal:
>
> 1. En la página de inicio de Luma, abra las herramientas para desarrolladores de navegadores. En el caso de Chrome, seleccione el botón `F12` en el teclado
> 1. Seleccione el **[!UICONTROL Consola]** pestaña
> 1. Entrar `digitalData` y seleccione `Enter` en el teclado para que aparezcan los valores de la capa de datos

![Pestaña Red](assets/validate-xdm-content.png)

También puede validar los detalles del mapa de identidad:

1. Inicie sesión en el sitio de Luma con las credenciales `test@adobe.com`/`test`

1. Vuelva a la [página principal de Luma](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Abra el **[!UICONTROL SDK web de Experience Platform]** en el panel de navegación izquierdo

   ![SDK web en Debugger](assets/identity-debugger-websdk-dark.png)

1. Seleccione el **[!UICONTROL eventos]** fila para abrir los detalles en una ventana emergente

   ![SDK web en Debugger](assets/identity-deugger-websdk-event-dark.png)

1. Busque la variable **identityMap** en la ventana emergente. Aquí debería ver `lumaCrmId` con tres claves authenticatedState, id y primary:
   ![SDK web en Debugger](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

### Validación de solicitudes del lado del cliente con herramientas de desarrollo del explorador

Estos tipos de detalles de solicitud también están visibles en las herramientas para desarrolladores web del explorador **Red** (suponiendo que el sitio web esté cargando la biblioteca de etiquetas).

1. Abra las herramientas para desarrolladores web del explorador **Red** y vuelva a cargar la página. Filtrar por llamadas con `/ee` para localizar la llamada, selecciónela y, a continuación, busque en **Encabezados** pestaña, y **Carga útil** pestaña

   ![Pestaña Red](assets/validate-dev-console.png)

1. Vaya a la **Respuesta** y observe cómo se incluye el valor de ECID en la respuesta. Copie este valor tal como lo utilizará para validar la información de perfil en el siguiente ejercicio

   ![Pestaña Red](assets/validate-dev-console-ecid.png)


## Validar solicitudes de red del lado del servidor con Experience Platform Debugger

Como aprendió en el [Configuración de una secuencia de datos](configure-datastream.md) En esta lección, el SDK web de Platform envía primero datos de la propiedad digital a Platform Edge Network. A continuación, Platform Edge Network realiza solicitudes adicionales del lado del servidor a los servicios correspondientes habilitados en el conjunto de datos.

Puede validar las solicitudes del lado del servidor habilitando el seguimiento de Edge en Debugger. Además, también puede validar la carga útil completamente procesada después de que llegue a una aplicación de Adobe utilizando [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).

En los dos ejercicios siguientes, habilite el seguimiento de Edge y vea el ID de Experience Cloud generado desde Platform Edge Network mediante Assurance.

### Habilitar seguimiento de Edge

Para habilitar el seguimiento de Edge

1. En la navegación izquierda de **[!UICONTROL Experience Platform Debugger]** select **[!UICONTROL Registros]**
1. Seleccione el **[!UICONTROL Edge]** y seleccione. **[!UICONTROL Connect]**

   ![Conectar seguimiento de Edge](assets/analytics-debugger-edgeTrace.png)

1. Está vacío por ahora

   ![Seguimiento de Edge conectado](assets/analytics-debugger-edge-connected.png)

1. Actualice la [Página de inicio de Luma](https://luma.enablementadobe.com/) y compruebe **[!UICONTROL Experience Platform Debugger]** de nuevo, para ver pasar los datos.

   ![Seguimiento de Edge de señalizaciones de Analytics](assets/validate-edge-trace.png)

En este punto, no puede ver ninguna solicitud de Platform Edge Network que vaya a una aplicación de Adobe porque no ha habilitado ninguna en la secuencia de datos. En lecciones futuras, utilice el seguimiento de Edge para ver las solicitudes salientes del lado del servidor a las aplicaciones de Adobe. Sin embargo, con Assurance aún puede ver el ID de Experience Cloud generado por Platform Edge Network.

### Iniciar una sesión de Assurance

Adobe Experience Platform Assurance es un producto de Adobe Experience Cloud que le ayuda a inspeccionar, probar, simular y validar cómo recopilar datos o servir experiencias.

Más información sobre [Garantía de Adobe](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).

Cada vez que se habilita el seguimiento de Edge, se inicia una sesión de Assurance en segundo plano.

Para ver la sesión de Assurance,

1. Con el seguimiento de Edge habilitado, puede ver un icono de vínculo de salida en la parte superior. Seleccione el icono para abrir Assurance. Se abre una nueva pestaña en el explorador.

   ![Iniciar sesión de Assurance](assets/validate-debugger-start-assurnance.png)

1. Seleccione la fila con el evento llamado Controlador de respuesta de Adobe.
1. A la derecha aparece un menú. Seleccione el `+` firmar junto a `[!UICONTROL ACPExtensionEvent]`
1. Explorar en profundidad seleccionando `[!UICONTROL payload > 0 > payload > 0 > namespace]`. El ID mostrado en la última `0` corresponde al `ECID`. Lo sabe por el valor que aparece debajo de `namespace` concordancia `ECID`

   ![Validación de ECID de Assurance](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Es posible que vea un valor ECID truncado debido al ancho de la ventana. Simplemente, seleccione la barra de control en la interfaz y arrastre a la izquierda para ver todo el ECID.

En lecciones futuras, utilice Assurance para validar cargas útiles completamente procesadas que lleguen a una aplicación de Adobe habilitada en el conjunto de datos.

Ahora que un objeto XDM se activa en una página y con los conocimientos necesarios para validar la recopilación de datos, ya puede configurar las aplicaciones de Adobe individuales mediante el SDK web de Platform.

[Siguiente: ](setup-experience-platform.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)