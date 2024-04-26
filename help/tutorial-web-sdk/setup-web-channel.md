---
title: Configuración del canal web de Journey Optimizer con el SDK web de Platform
description: Obtenga información sobre cómo implementar el canal web de Journey Optimizer mediante el SDK web de Platform. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Web Channel,Web SDK
jira: KT-15411
exl-id: ab83ce56-7f54-4341-8750-b458d0db0239
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '2892'
ht-degree: 0%

---


# Configuración del canal web de Journey Optimizer con SDK web

Obtenga información sobre cómo implementar Adobe Journey Optimizer [canal web](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/web/get-started-web) uso del SDK web de Adobe Experience Platform. Esta lección cubre los requisitos previos básicos del canal web, los pasos detallados para la configuración y una explicación detallada de un caso de uso centrado en el estado de lealtad.

Al seguir esta lección, los usuarios de Journey Optimizer están equipados para utilizar el canal web para una personalización en línea avanzada mediante el diseñador web de Journey Optimizer.

![Diagrama del SDK web y Adobe Analytics](assets/dc-websdk-ajo.png)

## Objetivos de aprendizaje

Al final de esta lección, puede hacer lo siguiente:

* Comprenda la función y la importancia del SDK web para ofrecer la experiencia del canal web.
* Comprenda el proceso de creación de una campaña de canal web de principio a fin con el ejemplo de caso de uso de Luma Loyalty Rewards.
* Configure las propiedades, acciones y programaciones de las campañas en la interfaz de.
* Comprenda la funcionalidad y las ventajas de la extensión Ayuda de edición visual de Adobe Experience Cloud.
* Aprenda a editar contenido de páginas web, incluidas imágenes, encabezados y otros elementos, con el diseñador web.
* Obtenga información sobre cómo insertar ofertas en una página web mediante el componente Decisión de oferta.
* Familiarícese con las prácticas recomendadas para garantizar la calidad y el éxito de una campaña de canal web.

## Requisitos previos

Para completar las lecciones de esta sección, primero debe:

* Completar todas las lecciones para la configuración inicial del SDK web de Platform, incluida la configuración de elementos de datos y reglas.
* Asegúrese de que la versión de la extensión de etiquetas del SDK web de Adobe Experience Platform sea la 2.16 o una posterior.
* Si utiliza el diseñador web de Journey Optimizer para crear la experiencia del canal web, asegúrese de que utiliza los exploradores Google Chrome o Microsoft® Edge.
* Asegúrese también de haber descargado y habilitado el [Extensión del explorador Ayuda de edición visual de Adobe Experience Cloud](https://chromewebstore.google.com/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
* Asegúrese de que las cookies de terceros estén permitidas en el explorador. Puede que también sea necesario deshabilitar los bloqueadores de anuncios en el explorador.

  >[!CAUTION]
  >
  > En el diseñador web de Journey Optimizer, es posible que algunos sitios web no se abran de forma fiable debido a uno de los siguientes motivos:
  > 
  > 1. El sitio web tiene estrictas políticas de seguridad.
  > 1. El sitio web está incrustado en un iframe.
  > 1. El control de calidad o el sitio de fase del cliente no son accesibles externamente (son sitios internos).

* Al crear experiencias web e incluir contenido de la biblioteca Adobe Experience Manager Assets Essentials, es necesario [configurar el subdominio para publicar este contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/web/configure-web-channel/web-delegated-subdomains).
* Si utiliza la función de experimentación de contenido, asegúrese de que el conjunto de datos web también se incluya en la configuración de creación de informes.
* Actualmente, se admiten dos tipos de implementaciones para habilitar la creación y el envío de campañas de canal web en las propiedades web:
   * Solo del lado del cliente: para modificar el sitio web, debe implementar el SDK web de Adobe Experience Platform.
   * Modo híbrido: puede utilizar la API del servidor de Platform Edge Network para solicitar personalización del lado del servidor. A continuación, la respuesta de la API se proporciona al SDK web de Adobe Experience Platform para procesar las modificaciones en el lado del cliente. Para obtener más información, consulte la documentación de la API de Adobe Experience Platform Edge Network Server. En esta publicación de blog se pueden encontrar más detalles y ejemplos de implementación para el modo híbrido.

  >[!NOTE]
  >
  >Actualmente no se admite la implementación solo del lado del servidor.




## Terminología

En primer lugar, debe comprender la terminología utilizada en las campañas del canal Web.

* **Canal web**: Un medio para la comunicación o la entrega de contenido a través de la web. En el contexto de esta guía, hace referencia al mecanismo a través del cual se entrega contenido personalizado a los visitantes del sitio web mediante el SDK web de Platform, dentro de Adobe Journey Optimizer.
* **Superficie web**: hace referencia a una propiedad web identificada por una dirección URL donde se entrega el contenido. Puede abarcar una o varias páginas web.
* **Journey Optimizer web designer**: herramienta o interfaz específica de Journey Optimizer en la que los usuarios pueden diseñar sus experiencias de canal web.
* **Ayuda de edición visual de Adobe Experience Cloud**: Extensión de explorador que ayuda a editar y diseñar visualmente experiencias de canal web.
* **Datastream**: una configuración dentro del servicio de Adobe Experience Platform que garantiza que se puedan entregar las experiencias del canal web.
* **Política de combinación**: una configuración que garantiza la activación y publicación precisas de las campañas entrantes.
* **Audiencia**: Un segmento específico de usuarios o visitantes del sitio que cumplen determinados criterios.
* **Diseñador web**: interfaz o herramienta que ayuda a editar y diseñar visualmente experiencias web sin profundizar en el código.
* **Editor de expresiones**: herramienta dentro del diseñador web que permite a los usuarios agregar personalización al contenido web, basada potencialmente en atributos de datos u otros criterios.
* **Componente de decisión de oferta**: Componente del diseñador web que ayuda a decidir qué oferta es la más adecuada para mostrarse a un visitante específico en función de la administración de decisiones.
* **Experimento de contenido**: método para probar diferentes variaciones de contenido y averiguar cuál de ellas tiene el mejor rendimiento en términos de la métrica deseada, como los clics entrantes.
* **Tratamiento**: en el contexto de los experimentos de contenido, un tratamiento hace referencia a una variación específica del contenido que se está probando con otra.
* **Simulación**: Mecanismo de previsualización para visualizar la experiencia del canal web antes de activarla para audiencias en directo.

## Configuración de la secuencia de datos

Ya ha agregado el servicio Adobe Experience Platform a su conjunto de datos. Ahora debe habilitar la opción Adobe Journey Optimizer para poder ofrecer experiencias de canal web.

Para configurar Adobe Journey Optimizer en el conjunto de datos:

1. Vaya a la [Recopilación de datos](https://experience.adobe.com/#/data-collection){target="blank"} interfaz.
1. En el panel de navegación izquierdo, seleccione **[!UICONTROL Datastreams]**.
1. Seleccione el conjunto de datos del SDK web de Luma creado anteriormente.

   ![Seleccionar secuencia de datos](assets/web-channel-select-datastream.png)

1. Seleccionar **[!UICONTROL Editar]** dentro del servicio Adobe Experience Platform.

   ![Editar secuencia de datos](assets/web-channel-edit-datastream.png)

1. Compruebe la **[!UICONTROL Adobe Journey Optimizer]** cuadro.

   ![Marque la casilla AJO](assets/web-channel-check-ajo-box.png)

1. Seleccione **[!UICONTROL Guardar]**.

Esto garantiza que el Edge Network de Adobe Experience Platform gestione correctamente los eventos entrantes de Journey Optimizer.

## Configuración de la política de combinación

Asegúrese de que se define una política de combinación con la variable **[!UICONTROL Política de combinación activa en Edge]** opción activada. Esta opción de política de combinación se emplea en los canales entrantes de Journey Optimizer para garantizar la activación y publicación precisas de las campañas entrantes en el perímetro.

Para configurar la opción en la política de combinación:

1. Vaya a la **[!UICONTROL Cliente]** > **[!UICONTROL Perfiles]** en la interfaz de Experience Platform o de Journey Optimizer.
1. Seleccione el **[!UICONTROL Políticas de combinación]** pestaña.
1. Seleccione la directiva (normalmente es mejor usar la variable [!UICONTROL Tiempo predeterminado basado] política) y cambie el **[!UICONTROL Política de combinación activa en Edge]** dentro de la opción **[!UICONTROL Configurar]** paso.

   ![Alternar política de combinación](assets/web-channel-active-on-edge-merge-policy.png)

## Configurar el conjunto de datos web para la experimentación de contenido

Para utilizar experimentos de contenido dentro de campañas del canal web, debe asegurarse de que el conjunto de datos web utilizado también se incluya en la configuración de informes. El sistema de informes de Journey Optimizer utiliza el conjunto de datos en modo de solo lectura para rellenar informes de experimentación de contenido listos para usar.

[En esta sección se detalla la adición de conjuntos de datos para informes de experimentos de contenido](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/content-experiment/reporting-configuration#add-datasets).

## Resumen de caso de uso: recompensas de fidelización

En esta lección, se utiliza un ejemplo de caso de uso de las Recompensas de fidelidad para detallar la implementación de una experiencia de canal web mediante el SDK web.

Este caso de uso le permite comprender mejor cómo Journey Optimizer puede ayudar a ofrecer las mejores experiencias entrantes a sus clientes, mediante campañas de Journey Optimizer y el diseñador web.

Dado que este tutorial está dirigido a los implementadores, vale la pena señalar que esta lección implica un trabajo sustancial de la interfaz en Journey Optimizer. Aunque estas tareas de interfaz las suelen administrar los especialistas en marketing, puede resultar beneficioso para los implementadores obtener información sobre el proceso, incluso si no suelen ser responsables de la creación de campañas de canales web.

### Crear un esquema de fidelización e introducir datos de ejemplo

Cuando los datos del SDK web se incorporan en Adobe Experience Platform, se pueden ampliar con otras fuentes de datos que haya introducido en Platform. Por ejemplo, cuando un usuario inicia sesión en el sitio de Luma, se construye un gráfico de identidades en Experience Platform y todos los demás conjuntos de datos con perfil habilitado pueden unirse para crear perfiles de cliente en tiempo real. Para ver esto en acción, cree rápidamente otro conjunto de datos en Adobe Experience Platform con algunos datos de fidelidad de muestra para que pueda utilizar Perfiles de cliente en tiempo real en campañas web de Journey Optimizer. Dado que ya ha realizado ejercicios similares, las instrucciones serán breves.

Cree el esquema de fidelización:

1. Creación de un nuevo esquema
1. Elegir **[!UICONTROL Perfil individual]** como el [!UICONTROL clase base]
1. Asignar un nombre al esquema `Luma Loyalty Schema`
1. Añada el [!UICONTROL Detalles de fidelización] grupo de campos
1. Añada el [!UICONTROL Datos demográficos] grupo de campos
1. Seleccione el `Person ID` y marcarlo como un campo [!UICONTROL Identidad] y [!UICONTROL Identidad principal] uso del `Luma CRM Id` [!UICONTROL Área de nombres de identidad].
1. Habilitar el esquema para [!UICONTROL Perfil]

   ![Esquema de fidelización](assets/web-channel-loyalty-schema.png)

Para crear el conjunto de datos e introducir los datos de ejemplo:

1. Cree un nuevo conjunto de datos a partir de `Luma Loyalty Schema`
1. Asignar un nombre al conjunto de datos `Luma Loyalty Dataset`
1. Habilitar el conjunto de datos para [!UICONTROL Perfil]
1. Descargar el archivo de muestra [luma-loyalty-forWeb.json](assets/luma-loyalty-forWeb.json)
1. Arrastre y suelte el archivo en el conjunto de datos
1. Confirme que los datos se han introducido correctamente.

   ![Esquema de fidelización](assets/web-channel-loyalty-dataset.png)

### Crear un público

Las audiencias agrupan perfiles en torno a rasgos comunes. Cree una audiencia rápida que pueda utilizar en su campaña web:

1. En la interfaz del Experience Platform, vaya a **[!UICONTROL Audiencias]** en el panel de navegación izquierdo
1. Seleccionar **[!UICONTROL Crear audiencia]**
1. Seleccionar **[!UICONTROL Generar regla]**
1. Seleccionar **[!UICONTROL Crear]**

   ![Crear un público](assets/web-campaign-create-audience.png)

1. Seleccionar **[!UICONTROL Atributos]**
1. Busque el **[!UICONTROL Lealtad]** > **[!UICONTROL Nivel]** y arrástrelo al campo **[!UICONTROL Atributos]** sección
1. Defina la audiencia como usuarios cuyos `tier` es `gold`
1. Nombrar la audiencia `Luma Loyalty Rewards – Gold Status`
1. Seleccionar **[!UICONTROL Edge]** como el **[!UICONTROL Método de evaluación]**
1. Seleccionar **[!UICONTROL Guardar]**

   ![Definición de la audiencia](assets/web-campaign-define-audience.png)

Como se trata de una audiencia muy sencilla, podemos utilizar el método de evaluación de Edge. Las audiencias de Edge se evalúan en Edge, por lo que en la misma solicitud realizada por el SDK web al Edge Network de Platform, podemos evaluar la definición de la audiencia y confirmar inmediatamente si el usuario cumple los requisitos.

### Crear campaña de recompensas de fidelización

Ahora que ha introducido nuestros datos de fidelidad de muestra y ha creado nuestro segmento, cree la campaña de canal web Loyalty Rewards en Adobe Journey Optimizer.

Para crear la campaña de muestra:

1. Abra el [Journey Optimizer](https://experience.adobe.com/journey-optimizer/home){target="_blank"} interfaz

   >[!NOTE]
   >
   > Los esquemas, conjuntos de datos y audiencias también se pueden crear en la interfaz de Journey Optimizer, ya que todos son construcciones de Experience Platform comunes.

1. Vaya a **[!UICONTROL Administración de recorrido]** > **[!UICONTROL Campañas]** en el panel de navegación izquierdo
1. Clic **[!UICONTROL Crear campaña]** en la parte superior derecha.
1. En el **[!UICONTROL Propiedades]** , especifique cómo desea ejecutar la campaña. En el caso de uso de las Recompensas de fidelización, elija **Programado**.

   ![Campaña programada](assets/web-channel-campaign-properties-scheduled.png)

1. En el **[!UICONTROL Acciones]** , seleccione la **[!UICONTROL Canal web]**. Como el  **[!UICONTROL Superficie web]**, seleccione **[!UICONTROL URL de página]**.

   >[!NOTE]
   >
   >Una superficie web hace referencia a una propiedad web identificada por una dirección URL donde se entrega el contenido. Puede corresponder a una sola dirección URL de página o abarcar varias páginas, lo que permite aplicar modificaciones en una o varias páginas web.

1. Elija la **[!UICONTROL URL de página]** opción de superficie web para implementar la experiencia en una página para esta campaña. Introduzca la dirección URL de la página de Luma. `https://luma.enablementadobe.com/content/luma/us/en.html`

1. Una vez definida la superficie web, seleccione **[!UICONTROL Crear]**.

   ![Seleccionar superficie web](assets/web-channel-web-surface.png)

1. Ahora añada algunos detalles adicionales a la nueva campaña del canal web. Primero asigne un nombre a la campaña. Llámalo. `Luma Loyalty Rewards – Gold Status`. De forma opcional, puede añadir una descripción a la campaña. Añadir también **[!UICONTROL Etiquetas]** para mejorar la taxonomía general de la campaña.

   ![Nombre de la campaña](assets/web-channel-campaign-name.png)

1. De forma predeterminada, la campaña está activa para todos los visitantes del sitio. A los efectos de este caso de uso, solo los miembros de la recompensa por estatus oro deben ver la experiencia. Para habilitar esto, haga clic en **[!UICONTROL Seleccionar audiencia]** y elija la `Luma Loyalty Rewards – Gold Status` audiencia.

1. En el **[!UICONTROL Área de nombres de identidad]** , seleccione el área de nombres para identificar a los individuos dentro del segmento elegido. Dado que está implementando la campaña en el sitio de Luma, puede elegir el área de nombres ECID. Perfiles dentro de `Luma Loyalty Rewards – Gold Status` La audiencia que no tenga el área de nombres de ECID entre sus distintas identidades no es el objetivo de la campaña del canal web.

   ![Elegir tipo de identidad](assets/web-channel-indentity-type.png)

1. Programe la campaña para que comience en la fecha actual utilizando **[!UICONTROL Inicio de campaña]** y finalizará en una semana con la opción **[!UICONTROL Fin de campaña]** opción.

   ![Programación de campañas](assets/web-channel-campaign-schedule.png)

>[!NOTE]
>
>Tenga en cuenta que, para las campañas de canal web, la experiencia web se muestra cuando el visitante abre la página. Por lo tanto, a diferencia de otros tipos de campañas en Adobe Journey Optimizer, la variable **[!UICONTROL Déclencheur de acción]** La sección no se puede configurar.

### Experimente con contenido de recompensas de fidelización

Si se desplaza hacia atrás, en la **[!UICONTROL Acción]** , si lo desea, puede crear un experimento para probar qué contenido funciona mejor para el `Luma Loyalty Rewards – Gold Status` audiencia. Vamos a crear y probar dos tratamientos como componente de la configuración de campaña.

Para crear el experimento de contenido:

1. Clic **[!UICONTROL Crear experimento]**.

   ![Crear experimento](assets/web-channel-create-content-experiment.png)

1. Primero elija una **[!UICONTROL Métrica de éxito]**. Esta es la métrica para determinar la eficacia del contenido. Elegir **[!UICONTROL Clics entrantes únicos]**, para ver qué tratamiento de contenido genera más clics en la experiencia web de CTA.

   ![Elegir métrica de éxito](assets/web-channel-content-experiment-metric.png)

1. Al configurar un experimento mediante el canal Web y elegir la variable **[!UICONTROL Clics entrantes]**, **[!UICONTROL Clics entrantes únicos]**, **[!UICONTROL Vistas de página]**, o **[!UICONTROL Vistas de página únicas]** métricas, la variable **[!UICONTROL Acción de clic]** Esta lista desplegable le permite rastrear y monitorizar con precisión los clics y las vistas en páginas específicas.

1. Si lo desea, puede designar una **[!UICONTROL Holdout]** que no recibe ninguno de los dos tratamientos. Deje esto sin marcar por ahora.

1. También puede elegir **[!UICONTROL Distribuir uniformemente]**. Marque esta opción para asegurarse de que las divisiones de tratamiento siempre se dividen uniformemente.

[Obtenga más información acerca de los experimentos de contenido en el canal web de Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/content-experiment/get-started-experiment).

### Editar contenido con el Asistente visual

Ahora, vamos a crear la experiencia del canal web. Para ello, utilice el Adobe Experience Cloud **[!UICONTROL Ayuda visual]**. Esta herramienta es una extensión de explorador compatible con Google Chrome y Microsoft® Edge. Asegúrese de haber descargado la extensión antes de intentar crear sus experiencias. Asegúrese también de que la página web incluya el SDK web.

1. Dentro de **[!UICONTROL Acción]** de la campaña, haga clic en **[!UICONTROL Editar contenido]**. Dado que ha introducido una sola dirección URL de página como superficie, debe estar preparado para empezar a trabajar en el compositor.

   ![Edición de contenido](assets/web-channel-edit-content.png)

1. Ahora, haga clic en **[!UICONTROL Editar página web]** para empezar a crear.

   ![Editar página web](assets/web-channel-edit-web-page.png)

1. Comience por editar algunos elementos con el compositor web. Utilice el menú contextual para editar el encabezado de la imagen a pantalla completa de Luma. Ajuste el estilo del panel contextual a la derecha.

   ![Añadir ediciones contextuales](assets/web-channel-some-contextual-edit.png)

1. Además, agregue personalización al contenedor mediante el complemento **[!UICONTROL Editor de expresiones]**.

   ![Adición de personalización](assets/web-channel-add-basic-personalization.png)

1. Asegúrese de que la experiencia recibe el seguimiento adecuado de los clics. Elegir **[!UICONTROL Elemento de rastreo de clics]** en el menú contextual.

   ![Seguimiento de clics](assets/web-channel-click-tracking.png)

1. Utilice el **[!UICONTROL Componente de decisión de oferta]** para insertar ofertas en la página web. Este componente utiliza **[!UICONTROL Gestión de decisiones]** para elegir la mejor oferta que se enviará a los visitantes de Luma.


### Cambios en el diseño del HTML

Hay algunos métodos disponibles si desea realizar cambios más avanzados o personalizados en el sitio como componente de la campaña de recompensas de fidelidad.

Utilice el **[!UICONTROL Componentes]** Panel para añadir HTML u otro contenido directamente al sitio de Luma.

![Exploración del panel de componentes](assets/web-channel-components-pane.png)

Agregue un nuevo componente HTML en la parte superior de la página. Edite el HTML dentro del componente desde la interfaz de diseño o **[!UICONTROL Contextual]** panel.

![Añadir HTML personalizado](assets/web-channel-add-html-component.png)

También puede añadir ediciones de HTML desde el **[!UICONTROL Modificaciones]** panel. Este panel le permite seleccionar un componente de la página y editarlo desde la interfaz del diseñador.

En el editor, añada el HTML para. `Luma Loyalty Rewards – Gold Status` audiencia. Seleccionar **[!UICONTROL Validate]**.

![Validar HTML](assets/web-channel-add-custom-html-validate.png)

Ahora, revise el nuevo componente de HTML personalizado para ver si encaja o no.

![Revisar HTML personalizado](assets/web-channel-review-custom-html.png)

Editar un componente específico mediante **[!UICONTROL Tipo de selector de CSS]** modificación.

![Modificar CSS](assets/web-channel-css-selector.png)

Añadir código personalizado mediante **Página `<head>` type** modificación.

![Modificar encabezado](assets/web-channel-page-head-modification.png)

Las posibilidades son infinitas usando el **[!UICONTROL Ayuda visual]**.

### Simular contenido de recompensas de fidelización

Consulte una vista previa de la página web modificada antes de activar la campaña. Tenga en cuenta que debe tener perfiles de prueba configurados para simular experiencias de canal web.

Para simular la experiencia:

1. Seleccionar **[!UICONTROL Simular contenido]** dentro de la campaña.

   ![Simular contenido](assets/web-channel-simulate-content.png)

1. Elija un perfil de prueba para recibir la simulación. Tenga en cuenta que el perfil de prueba debe estar en la `Luma Loyalty Rewards – Gold Status` para recibir el tratamiento adecuado.

1. Se muestra la vista previa del perfil de prueba.

### Activación de la campaña de recompensas de fidelización

Finalmente, active la campaña del canal web.

1. Seleccionar **Revisar para activar**.

1. Se le pedirá que confirme los detalles de la campaña una última vez. Seleccionar **[!UICONTROL Activar]**. La campaña puede tardar hasta 15 minutos en activarse en el sitio.

### QA de recompensas de fidelización

Hay algunos inicios de sesión que puede utilizar para simular usuarios con &quot;estado oro&quot; y cumplir los requisitos para su campaña:

1. `cleavlandeuler@emailsim.io`/`test`
1. `leftybeagen@emailsim.io`/`test`
1. `jenimartinho@emailsim.io`/`test`

Como práctica recomendada, supervise el **[!UICONTROL Web]** de los informes globales y en directo de campaña para los KPI específicos de la campaña. Para esta campaña, monitorice las impresiones de experiencia y la tasa de clics.

![Ver informe web](assets/web-channel-web-report.png)

### Validación del canal web mediante Adobe Experience Platform Debugger

La extensión de Adobe Experience Platform Debugger, disponible tanto para Chrome como para Firefox, analiza sus páginas web para identificar problemas en la implementación de las soluciones de Adobe Experience Cloud.

Puede utilizar el depurador del sitio de Luma para validar la experiencia del canal web en producción. Esta es una práctica recomendada una vez que el caso de uso de las Recompensas de fidelidad está en funcionamiento, para garantizar que todo esté configurado correctamente.

[Obtenga información sobre cómo configurar Debugger en el explorador mediante la guía aquí](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/debugger/overview).

Para iniciar la validación con el depurador:

1. Vaya a la página web de Luma con la experiencia del canal web.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. En la página web, abra el **[!UICONTROL Adobe Experience Platform Debugger]**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Vaya a **Resumen**. Compruebe que la variable **[!UICONTROL ID de flujo de datos]** coincide con el **[!UICONTROL secuencia de datos]** in **[!UICONTROL Recopilación de datos de Adobe]** para el que ha activado Adobe Journey Optimizer.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. A continuación, puede iniciar sesión en el sitio con varias cuentas de fidelidad de Luma y utilizar el depurador para validar las solicitudes enviadas al Edge Network de Adobe Experience Platform.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. En **[!UICONTROL Soluciones]** vaya a la **[!UICONTROL SDK web de Experience Platform]**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Dentro de **Configuración** pestaña, Activar/desactivar **[!UICONTROL Habilitar depuración]**. Esto habilita el registro de la sesión en un **[!UICONTROL Adobe Experience Platform Assurance]** sesión.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Inicie sesión en el sitio con varias cuentas de fidelidad de Luma y utilice el depurador para validar las solicitudes enviadas al **[!UICONTROL red de Adobe Experience Platform Edge]**. Todas estas solicitudes deben capturarse en **[!UICONTROL Assurance]** para el seguimiento del registro.
<!--
   ![ADD SCREENSHOT](#)
-->

[Siguiente: ](setup-decision-management.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
