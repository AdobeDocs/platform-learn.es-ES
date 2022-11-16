---
title: Cambiar entornos de etiquetas con Adobe Experience Cloud Debugger
description: Aprenda a utilizar el Experience Cloud Debugger para cargar diferentes códigos incrustados de etiquetas. Esta lección forma parte del tutorial Implementación del Experience Cloud en sitios web .
exl-id: 29972a00-e5e0-4fe0-a71c-c2ca106938be
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 40%

---

# Cambiar entornos de etiquetas con el Experience Cloud Debugger

En esta lección, utilizará la variable [Extensión de Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) para reemplazar la propiedad tag codificada en la variable [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) con su propia propiedad.

Esta técnica se denomina cambio de entorno y será útil posteriormente, cuando trabaje con etiquetas en su propio sitio web. Podrá cargar su sitio web de producción en su navegador, pero con su *desarrollo* entorno de etiquetas. Esto le permite realizar y validar cambios con seguridad en las etiquetas de forma independiente de las revisiones de código normales.  Después de todo, esta separación de las versiones de etiquetas de marketing y las revisiones de código normales es una de las principales razones por las que los clientes utilizan etiquetas.

>[!NOTE]
>
>Adobe Experience Platform Launch se está integrando en Adobe Experience Platform como un conjunto de tecnologías de recopilación de datos. Se han implementado varios cambios terminológicos en la interfaz que debe tener en cuenta al usar este contenido:
>
> * El platform launch (lado del cliente) ya está **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)**
> * El servidor de platform launch está ahora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Las configuraciones de Edge ahora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)**


## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Usar Debugger para cargar un entorno de etiquetas alternativo
* Use Debugger para validar que ha cargado un entorno de etiquetas alternativo

## Obtener la dirección URL del entorno de desarrollo.

1. En la propiedad de etiqueta, abra la variable `Environments` página

1. En la fila **[!UICONTROL Desarrollo (Development)]**, haga clic en el icono ![Instalar](images/launch-installIcon.png) para abrir el modal.

1. Haga clic en el icono ![Copiar](images/launch-copyIcon.png) para copiar el código de incrustación en el portapapeles.

1. Haga clic en **[!UICONTROL Cerrar]** para cerrar el modal.

   ![Icono Instalar](images/launch-copyInstallCode.png)

## Reemplace la URL de etiqueta en el sitio de demostración de Luma

1. Abra [el sitio de ejemplo de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) en el navegador Chrome.

1. Abra la extensión de [Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) haciendo clic en el icono ![Debugger](images/icon-debugger.png).

   ![Haga clic en el icono de Debugger](images/switchEnvironments-openDebugger.png)

1. Tenga en cuenta que la propiedad de etiqueta implementada actualmente se muestra en la ficha Resumen

   ![entorno de etiquetas mostrado en Debugger](images/switchEnvironments-debuggerOnWeRetail-prod.png)

1. Vaya a la pestaña Herramientas.
1. Desplácese a la sección **[!UICONTROL Reemplazar código de incrustación de Launch]**.
1. Asegúrese de que la pestaña de Chrome con el sitio de Luma esté enfocada detrás de Debugger (no la pestaña con este tutorial ni la pestaña con la interfaz de recopilación de datos).  Pegue el código de incrustación que se encuentra en el portapapeles en el campo de entrada.
1. Alterne en la función &quot;Aplicar en luma.enablementadobe.com&quot; para que todas las páginas del sitio de Luma se asignen a la propiedad de etiqueta
1. Haga clic en el botón **[!UICONTROL Guardar]**.

   ![entorno de etiquetas mostrado en Debugger](images/switchEnvironments-debugger-save.png)

1. Vuelva a cargar el sitio de Luma y marque la pestaña Resumen de Debugger. En la sección de Launch, debería ver que se está utilizando la propiedad Desarrollo (Development). Confirme que el nombre de la propiedad coincide con la suya y que el entorno es de “desarrollo”.

   ![entorno de etiquetas mostrado en Debugger](images/switchEnvironments-debuggerOnWeRetail.png)

>[!NOTE]
>
>Debugger guarda esta configuración y reemplaza los códigos incrustados de etiquetas cada vez que vuelva al sitio de Luma. No afecta a otros sitios que visita en otras pestañas abiertas. Para impedir que Debugger sustituya el código de incrustación, haga clic en el botón **[!UICONTROL Eliminar]** junto al código de incrustación en la pestaña Herramientas de Debugger.

A medida que continúe con el tutorial, utilizará esta técnica de asignación del sitio de Luma a su propia propiedad de etiqueta para validar la implementación de etiquetas. Cuando empiece a utilizar etiquetas en el sitio web de producción, puede utilizar esta misma técnica para validar los cambios.

[Siguiente: “Añadir el servicio de ID de Adobe Experience Platform” >](id-service.md)
