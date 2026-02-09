---
title: Publicación de la propiedad de etiquetas
description: Obtenga información sobre cómo publicar la propiedad de etiquetas del entorno de desarrollo en los entornos de ensayo y producción. Esta lección forma parte del tutorial Implementación de Experience Cloud en sitios web.
exl-id: dec70472-cecc-4630-b68e-723798f17a56
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 55%

---

# Publicación de la propiedad de etiquetas

Después de haber implementado varias soluciones clave de Adobe Experience Cloud en su entorno de desarrollo, es hora de analizar el flujo de trabajo de publicación.


>[!WARNING]
>
> Se espera que el sitio web de Luma utilizado en este tutorial se sustituya durante la semana del 16 de febrero de 2026. Es posible que el trabajo realizado como parte de este tutorial no sea aplicable al nuevo sitio web.

>[!NOTE]
>
>Adobe Experience Platform Launch se está integrando en Adobe Experience Platform como un conjunto de tecnologías de recopilación de datos. Se han implementado varios cambios terminológicos en la interfaz que debe tener en cuenta al utilizar este contenido:
>
> * Platform Launch (lado del cliente) ahora es **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)**
> * El lado del servidor de Platform Launch ahora es **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Ahora, las configuraciones de Edge son **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)**

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

1. Publicar una biblioteca de desarrollo en el entorno de ensayo.
1. Asignar una biblioteca de ensayo al sitio web de producción utilizando Debugger.
1. Publicar una biblioteca de ensayo en el entorno de producción.

## Publicar en el entorno de ensayo.

Después de crear y validar la biblioteca en el entorno de desarrollo, es hora de publicarla en el entorno de ensayo.

1. Ir a la página **[!UICONTROL Flujo de publicación]**

1. Abra el menú desplegable situado junto a la biblioteca y seleccione **[!UICONTROL Enviar para aprobación]**

   ![Enviar para aprobación](images/publishing-submitForApproval.png)

1. Haga clic en el botón **[!UICONTROL Enviar]** del cuadro de diálogo:

   ![Haga clic en Enviar en el modal](images/publishing-submit.png)

1. La biblioteca ahora aparece en la columna [!UICONTROL Enviado] en un estado sin compilar:

1. Abra el menú desplegable y seleccione **[!UICONTROL Generar para ensayo]**:

   ![Generar para ensayo](images/publishing-buildForStaging.png)

1. Una vez que aparece el icono del punto verde, la biblioteca se puede previsualizar en el entorno de ensayo.

En un escenario en tiempo real, el siguiente paso del proceso sería que el equipo de control de calidad validara los cambios en la biblioteca de ensayo. Pueden hacerlo usando Debugger.

**Para validar los cambios en la biblioteca de ensayo**

1. En su propiedad de etiquetas, abra la página [!UICONTROL Entornos]

1. En la fila [!UICONTROL Ensayo], haga clic en el ![icono Instalar](images/launch-installIcon.png) para abrir el modal.

   ![Vaya a la página Entornos y haga clic para abrir el modal](images/publishing-getStagingCode.png)

1. Haga clic en el icono ![Copiar](images/launch-copyIcon.png) para copiar el código incrustado en el portapapeles.

1. Haga clic en **[!UICONTROL Cerrar]** para cerrar el modal

   ![Icono Instalar](images/publishing-copyStagingCode.png)

1. Abra [el sitio de ejemplo de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) en el navegador Chrome.

1. Abra la [extensión de Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) haciendo clic en el icono ![Debugger](images/icon-debugger.png)

   ![Haga clic en el icono de Debugger](images/switchEnvironments-openDebugger.png)

1. Vaya a la pestaña Herramientas.

1. En la sección **[!UICONTROL Adobe Launch > Reemplazar código de incrustación de Launch]**, pegue el código de incrustación de ensayo que se encuentra en el portapapeles.
1. Activar el conmutador **[!UICONTROL Aplicar en luma.enablementadobe.com]**

1. Haga clic en el icono de disco para guardar.

   ![entorno de etiquetas mostrado en Debugger](images/switchEnvironments-debugger-save.png)

1. Vuelva a cargar y compruebe la pestaña Resumen de Debugger. En la sección de Launch, debería ver que la propiedad de ensayo está implementada y que se muestra su nombre de propiedad (por ejemplo, &quot;Tutorial de etiquetas&quot; o como haya llamado a su propiedad).

   ![entorno de etiquetas mostrado en Debugger](images/publishing-debugger-staging.png)

En realidad, una vez que el equipo de control de calidad ha cerrado sesión al revisar los cambios en el entorno de ensayo, es hora de publicar en producción.

## Publicación en producción

1. Vaya a la página [!UICONTROL Publicar].

1. En el menú desplegable, haga clic en **[!UICONTROL Aprobar para publicación]**:

   ![Aprobar para publicación](images/publishing-approveForPublishing.png)

1. Haga clic en el botón **[!UICONTROL Aprobar]** del cuadro de diálogo:

   ![Haga clic en Aprobar](images/publishing-approve.png)

1. La biblioteca ahora aparece en la columna [!UICONTROL Aprobado] en el estado sin compilar (punto amarillo):

1. Abra el menú desplegable y seleccione **[!UICONTROL Generar y publicar en producción]**:

   ![Haga clic en Generar y publicar en producción](images/publishing-buildAndPublishToProduction.png)

1. Haga clic en **[!UICONTROL Publicar]** en el cuadro de diálogo:

   ![Haga clic en Publicar](images/publishing-publish.png)

1. La biblioteca ahora aparece en la columna [!UICONTROL Publicado]:

   ![Publicadas](images/publishing-published.png)

¡Ya está! ¡Ha completado el tutorial y ha publicado su primera propiedad en etiquetas!
