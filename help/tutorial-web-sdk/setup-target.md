---
title: Configuración de Adobe Target con el SDK web de Platform
description: Obtenga información sobre cómo implementar Adobe Target mediante el SDK web de Platform. Esta lección forma parte del tutorial Implementar Adobe Experience Cloud con SDK web .
solution: Data Collection, Target
exl-id: 9084f572-5fec-4a26-8906-6d6dd1106d36
source-git-commit: edbc433e9bd72dfa9b9025063fc90c7fdc2c2774
workflow-type: tm+mt
source-wordcount: '3779'
ht-degree: 1%

---

# Configuración de Adobe Target con el SDK web de Platform

Obtenga información sobre cómo implementar Adobe Target mediante el SDK web de Platform. Obtenga información sobre cómo ofrecer experiencias y cómo pasar parámetros adicionales a Target.

[Adobe Target](https://docs.adobe.com/content/help/es-ES/experience-cloud/user-guides/home.translate.html) es la aplicación de Adobe Experience Cloud que le proporciona todo lo necesario para adaptar y personalizar la experiencia de sus clientes con el fin de maximizar los ingresos de sus sitios web, aplicaciones y otros canales digitales, tanto para PC como para móviles.

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Obtenga información sobre cómo añadir el fragmento de ocultación previa del SDK web de Platform para evitar el parpadeo al utilizar Target con códigos incrustados de etiquetas asíncronos
* Configurar un conjunto de datos para habilitar la funcionalidad de Target
* Procesar decisiones de personalización visual cuando se carga la página (antes denominado &quot;mbox global&quot;)
* Pasar datos XDM a Target y comprender la asignación a los parámetros de Target
* Pasar datos personalizados a Target, como parámetros de perfil y entidad
* Validación de una implementación de Target con Platform Web SDK


## Requisitos previos

Para completar las lecciones de esta sección, primero debe:

* Completar todas las lecciones para la configuración inicial del SDK web de Platform, incluida la configuración de reglas y elementos de datos.
* Asegúrese de que dispone de un [Función Editor o Aprobador](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80).
* Instale el [Extensión del Helper del Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) si utiliza el explorador Google Chrome.
* Obtenga información sobre cómo configurar actividades en Target. Si necesita un actualizador, los siguientes tutoriales y guías son útiles para esta lección:
   * [Usar la extensión del Compositor de experiencias visuales (VEC) Helper](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html)
   * [Usar el Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Uso del Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Crear actividades de segmentación de experiencias](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

## Agregar atenuación de parpadeo

Antes de empezar, determine si se requiere una solución de control de parpadeo adicional en función de cómo se cargue la biblioteca de etiquetas.

>[!NOTE]
>
>Este tutorial utiliza la variable [Sitio de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) que cuenta con una implementación asíncrona de etiquetas y una reducción del parpadeo. En esta sección se hace referencia para comprender cómo funciona la mitigación de parpadeo con el SDK web de Platform.


### Implementación asíncrona

Cuando una biblioteca de etiquetas se carga de forma asíncrona, la página puede finalizar el procesamiento antes de que Target haya realizado un intercambio de contenido. Este comportamiento puede conllevar lo que se conoce como &quot;parpadeo&quot;, por el cual el contenido predeterminado aparece brevemente antes de ser reemplazado por el contenido personalizado especificado por Target. Si desea evitar este parpadeo, Adobe recomienda agregar un fragmento preocultado especial inmediatamente antes del código incrustado de la etiqueta asíncrona.

Este fragmento ya está presente en el sitio de Luma, pero veamos con más detalle lo que hace este código:

```html
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
</script>
```

El fragmento de ocultamiento previo crea una etiqueta de estilo en el encabezado de la página con la definición CSS que elija. Esta etiqueta de estilo se elimina cuando se recibe una respuesta de Target o se alcanza el tiempo de espera.

El comportamiento de ocultamiento previo se controla mediante dos configuraciones al final del fragmento.

* `body { opacity: 0 !important }` especifica la definición de CSS que se utiliza para la preocultación hasta que se carga Target. De forma predeterminada, toda la página está oculta. Puede actualizar esta definición a los selectores que desee ocultar previamente, así como a cómo desea ocultarlos. Puede incluir varias definiciones, ya que este valor es simplemente lo que se inserta en la etiqueta de estilo de ocultamiento previo. Si tiene un elemento contenedor fácil de identificar que ajuste el contenido debajo de su navegación, puede utilizar esta configuración para limitar la preocultación a ese elemento contenedor.
* `3000` especifica el tiempo de espera en milisegundos para la preocultación. Si no se recibe una respuesta de Target antes del tiempo de espera, se elimina la etiqueta de estilo de ocultamiento previo. No es habitual alcanzar este tiempo de espera.

>[!NOTE]
>
>El fragmento de ocultamiento previo del SDK web de Platform es ligeramente diferente del utilizado con la biblioteca at.js de Target. Asegúrese de utilizar el fragmento de código correcto para el SDK web de Platform, ya que utiliza un ID de estilo diferente de `alloy-prehiding`. Si se utiliza el fragmento de ocultamiento previo para at.js, es posible que no funcione correctamente.

El fragmento de ocultamiento previo también está disponible dentro de las etiquetas :

1. Vaya a la **[!UICONTROL Extensiones]** sección de etiquetas
1. Select **[!UICONTROL Configurar]** para la extensión web SDK de Adobe Experience Platform
1. Seleccione el **[!UICONTROL Copiar fragmento de ocultamiento previo en el portapapeles]** botón

   ![Fragmento de ocultamiento previo de Target para implementaciones asíncronas](assets/target-flicker-async.png)

   >[!NOTE]
   >
   >El fragmento predeterminado de ocultamiento previo copiado de la extensión web SDK de Platform puede incluir una definición CSS que no existe en el sitio, como `.personalization-container { opacity: 0 !important }`. Asegúrese de comprobar y modificar el fragmento de ocultamiento previo correctamente para su sitio.

### Implementación sincrónica

Adobe recomienda implementar etiquetas de forma asíncrona, tal y como se muestra en el sitio de Luma. Sin embargo, si la biblioteca de etiquetas se carga sincrónicamente, no es necesario el fragmento de ocultamiento previo. En su lugar, el estilo de ocultamiento previo se especifica en la configuración de la extensión del SDK web de Platform.

El estilo de ocultamiento previo para implementaciones sincrónicas se puede configurar de la siguiente manera:

1. Vaya a la **[!UICONTROL Extensiones]** sección de etiquetas
1. Seleccione el **[!UICONTROL Configurar]** botón de la extensión web SDK de Platform
1. Seleccione el **[!UICONTROL Editar estilo de ocultación previa]** botón

   ![Fragmento de ocultamiento previo de Target para implementaciones asíncronas](assets/target-flicker-sync.png)

1. Modifique la CSS para incluir los selectores y métodos de ocultación que desee utilizar, por ejemplo: `body { opacity: 0 !important }` si desea ocultar previamente todo el cuerpo de la página.
1. Guarde los cambios y créelos en una biblioteca

>[!NOTE]
>
>La configuración de estilo de ocultamiento previo solo está pensada para utilizarse en implementaciones sincrónicas. Este estilo debe estar en blanco o comentarse si utiliza una implementación asincrónica de etiquetas.

Para obtener más información sobre cómo el SDK web de Platform puede administrar el parpadeo, consulte la sección de la guía: [gestión del parpadeo para experiencias personalizadas](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html).


## Configuración del conjunto de datos

Target debe estar habilitado en la configuración del conjunto de datos para que el SDK web de Platform pueda entregar cualquier actividad de Target.

Para configurar Target en el conjunto de datos:

1. Vaya a [Recopilación de datos](https://experience.adobe.com/#/data-collection){target="blank"} interfaz
1. En el panel de navegación izquierdo, seleccione **[!UICONTROL Datastreams]**
1. Seleccione el `Luma Web SDK` datastream

   ![Seleccione el conjunto de datos del SDK web de Luma](assets/datastream-luma-web-sdk.png)

1. Select **[!UICONTROL Añadir servicio]**

   ![Añadir un servicio al conjunto de datos](assets/target-datastream-addService.png)
1. Select **[!UICONTROL Adobe Target]** como el **[!UICONTROL Servicio]**
1. Si lo desea, escriba los detalles opcionales sobre la implementación de Target siguiendo las directrices que se describen a continuación.
1. Seleccione **[!UICONTROL Guardar]**

   ![Configuración del almacén de datos de Target](assets/target-datastream.png)

### Token de propiedad

Los clientes de Target Premium tienen la opción de administrar los permisos de usuario con propiedades. Las propiedades de Target le permiten establecer límites en torno a los cuales los usuarios pueden ejecutar actividades de Target. Consulte la [Permisos de Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=es) de la documentación de Target para obtener más información.

Para configurar o buscar tokens de propiedad, vaya a **Adobe Target** > **[!UICONTROL Administración]** > **[!UICONTROL Propiedades]**. La variable `</>` muestra el código de implementación. La variable `at_property` es el token de propiedad que usaría en su conjunto de datos.

![Token de propiedad de Target](assets/target-admin-properties.png)

>[!NOTE]
>
>Solo se puede especificar un token de propiedad por conjunto de datos.


### ID de entorno de Target

[Entornos](https://experienceleague.adobe.com/docs/target/using/administer/environments.html) en Target le ayuda a administrar su implementación en todas las etapas de desarrollo. Esta configuración opcional especifica qué entorno de Target va a utilizar con cada conjunto de datos.

Adobe recomienda configurar el ID de entorno de Target de forma diferente para cada uno de los conjuntos de datos de desarrollo, ensayo y producción para que las cosas sigan siendo sencillas.

Para configurar o buscar ID de entorno, vaya a **Adobe Target** > **[!UICONTROL Administración]** > **[!UICONTROL Entornos]**.

![Entornos de destino](assets/target-admin-environments.png)

>[!NOTE]
>
>Si no se especifica ningún ID de entorno de Target, se asume el entorno de destino de producción.

### Área de nombres del ID de terceros de Target

Esta configuración opcional le permite especificar qué símbolo de identidad utilizar para el ID de terceros de Target. Target solo admite la sincronización de perfiles en un único símbolo de identidad o área de nombres. Para obtener más información, consulte la [Sincronización de perfiles en tiempo real para mbox3rdPartyId](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) de la guía de Target.

Los símbolos de identidad se encuentran en la lista de identidades debajo de **Recopilación de datos** > **[!UICONTROL Cliente]** > **[!UICONTROL Identidades]**.

![Lista de identidades](assets/target-identities.png)

Para los fines de este tutorial utilizando el sitio de Luma, utilice el símbolo de identidad `lumaCrmId` configuración durante la lección acerca de [Identidades](configure-identities.md).


## Procesar decisiones de personalización visual

En primer lugar, debe comprender la terminología utilizada en las interfaces de Target y etiquetas.

* **Actividad**: Conjunto de experiencias dirigidas a una o más audiencias. Por ejemplo, una simple prueba A/B podría ser una actividad con dos experiencias.
* **Experiencia**: Conjunto de acciones dirigidas a una o más ubicaciones o ámbitos de decisión.
* **Ámbito de la decisión**: Ubicación en la que se entrega una experiencia de Target. Los ámbitos de decisión equivalen a &quot;mboxes&quot; si está familiarizado con el uso de versiones anteriores de Target.
* **Decisión de personalización**: Se debe aplicar una acción que el servidor determine. Estas decisiones pueden basarse en criterios de audiencia y en la prioridad de las actividades de Target.
* **Propuesta**: El resultado de las decisiones adoptadas por el servidor que se entregan en la respuesta del SDK web de la plataforma. Por ejemplo, intercambiar una imagen de banner sería una propuesta.

### Actualizar la regla de carga de página

Las decisiones de personalización visual de Target las entrega el SDK web de la plataforma, si Target está habilitado en el conjunto de datos. Sin embargo, _no se renderizan automáticamente_. Debe modificar la regla de carga de página global para habilitar el procesamiento automático.

1. En el [Recopilación de datos](https://experience.adobe.com/#/data-collection){target="blank"} , abra la propiedad tag que está utilizando para este tutorial.
1. Abra el `all pages - library load - AA & AT` regla
1. Seleccione el `Adobe Experience Platform Web SDK - Send event` acción
1. Habilitar **[!UICONTROL Procesar decisiones de personalización visual]** con la casilla de verificación

   ![Habilitar el procesamiento de decisiones de personalización visual](assets/target-rule-enable-visual-decisions.png)

1. Guarde los cambios y luego créelos en la biblioteca

La configuración de decisiones de personalización visual de renderización hace que el SDK web de plataforma aplique automáticamente todas las modificaciones especificadas con el Compositor de experiencias visuales de Target o &quot;mbox global&quot;.

>[!NOTE]
>
>Normalmente, la variable [!UICONTROL Procesar decisiones de personalización visual] solo debe habilitarse para una sola acción Enviar evento por carga de página completa. Si varias acciones de Enviar evento tienen esta configuración habilitada, se omiten las solicitudes de renderización posteriores.

Si prefiere renderizar o actuar sobre estas decisiones con el código personalizado, puede dejar el [!UICONTROL Procesar decisiones de personalización visual] configuración deshabilitada. El SDK web de Platform es flexible y proporciona esta capacidad para proporcionarle control total. Puede consultar la guía para obtener más información sobre [renderización manual de contenido personalizado](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html).

### Configurar una actividad de Target con el Compositor de experiencias visuales

Una vez completada la parte básica de la implementación, cree una actividad de Segmentación de experiencias (XT) en Target para validar que todo funciona correctamente. Puede consultar el tutorial de Target para [creación de actividades de segmentación de experiencias](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html) si necesita ayuda.

>[!NOTE]
>
>Si utiliza Google Chrome como navegador, la variable [Extensión del Helper del Compositor de experiencias visuales (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=en) es necesario para cargar el sitio correctamente y editarlo en el VEC.

1. Navegar a Target
1. Cree una actividad de segmentación de experiencias (XT) usando la página de inicio de Luma para la URL de la actividad

   ![Crear una nueva actividad XT](assets/target-xt-create-activity.png)

1. Modifique la página, por ejemplo, cambie el texto del banner de la página principal

   ![Modificación del VEC de Target](assets/target-xt-vec-modification.png)

1. Elija Adobe Analytics como fuente de informes con el grupo de informes adecuado y la métrica Pedidos como objetivo.

   >[!NOTE]
   >
   >Si no utiliza Adobe Analytics, seleccione Target como fuente de informes y elija otra métrica como **Participación > Vistas de página** en su lugar. Se requiere una métrica de objetivo para guardar y previsualizar la actividad.

1. Guarde la actividad
1. Si se siente cómodo con los cambios, puede activar su actividad. De lo contrario, si desea obtener una vista previa de la experiencia sin activar, puede copiar la variable [URL de vista previa de control de calidad](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).
1. Cargue la página principal de Luma y debería ver los cambios aplicados
1. Después de unas horas, debería poder ver los datos de actividad de Target y las conversiones en Adobe Analytics. Consulte la Guía de Target para obtener información detallada sobre [Creación de informes en Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/reporting.html?lang=en).



### Validar con Debugger

Si configura una actividad, debería ver el contenido renderizado en la página. Sin embargo, aunque no haya actividades activas, también puede consultar la llamada de red Enviar evento para confirmar que Target está configurado correctamente.

>[!CAUTION]
>
>Si utiliza Google Chrome y tiene la variable [Extensión del Helper del Compositor de experiencias visuales (VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=en) instalado, asegúrese de que la variable **Inserción de bibliotecas de Target** está desactivado. Si habilita esta configuración, se generarán solicitudes de Target adicionales.

1. Abra la extensión del explorador de Adobe Experience Platform Debugger.
1. Vaya a la [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) y utilice el depurador para [cambie la propiedad tag del sitio a su propia propiedad de desarrollo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Vuelva a cargar la página
1. Seleccione el **[!UICONTROL Red]** herramienta en Debugger
1. Filtrar por **[!UICONTROL SDK web de Adobe Experience Platform]**
1. Seleccione el valor de la fila eventos para la primera llamada

   ![Llamada de red en Adobe Experience Platform Debugger](assets/target-debugger-network.png)

1. Tenga en cuenta que hay claves en `query` > `personalization` y  `decisionScopes` tiene un valor de `__view__`. Este ámbito equivale al &quot;mbox global&quot; de Target. Esta llamada del SDK web de Platform solicitó decisiones a Target.

   ![__ver__ solicitud de decisionScope](assets/target-debugger-view-scope.png)

1. Cierre la superposición y seleccione los detalles del evento para la segunda llamada de red. Esta llamada solo está presente si Target ha devuelto una actividad.
1. Tenga en cuenta que hay detalles sobre la actividad y la experiencia que Target devuelve. Esta llamada del SDK web de Platform envía una notificación de que se ha renderizado una actividad de Target para el usuario e incrementa una impresión.

   ![Impresión de actividad de Target](assets/target-debugger-activity-impression.png)

## Configuración y renderización de un ámbito de decisión personalizado

Los ámbitos de decisión personalizados (anteriormente conocidos como &quot;mboxes&quot;) se pueden utilizar para ofrecer contenido de HTML o JSON de forma estructurada mediante el Compositor de experiencias basadas en formularios de Target. El SDK web de Platform no procesa automáticamente el contenido entregado a uno de estos ámbitos personalizados.

### Añadir un ámbito a la regla de carga de página

Modifique la regla de carga de página para agregar un ámbito de decisión personalizado:

1. Abra el `all pages - library load - AA & AT` regla
1. Seleccione el `Adobe Experience Platform Web SDK - Send Event` acción
1. Añada uno o más ámbitos que desee utilizar. Para este ejemplo, utilice `homepage-hero`.

   ![Ámbito personalizado](assets/target-rule-custom-scope.png)

1. Guarde los cambios y créelos en la biblioteca

>[!TIP]
>
>Para este tutorial, utilizará un solo ámbito definido manualmente para fines de demostración. Si decide utilizar varios ámbitos de decisión destinados a páginas específicas, debe considerar la posibilidad de utilizar un elemento de datos que devuelva una matriz de ámbitos condicionalmente en función de la ruta de la página. Este enfoque ayuda a mantener la implementación sencilla y escalable.

### Procesamiento de la respuesta de Target

Ahora que ha configurado el SDK web de Platform para solicitar contenido para el `homepage-hero` , debe hacer algo con la respuesta. La extensión de etiqueta del SDK web de Platform proporciona un [!UICONTROL Enviar evento finalizado] que se puede usar para almacenar en déclencheur inmediatamente una nueva regla cuando se recibe una respuesta de [!UICONTROL Enviar evento] se recibe la acción.

1. Cree una regla llamada `homepage - send event complete - render homepage-hero`.
1. Agregue un evento a la regla. Utilice la variable **SDK web de Adobe Experience Platform** y **[!UICONTROL Enviar evento finalizado]** tipo de evento.
1. Agregue una condición para restringir la regla a la página principal de Luma (ruta sin cadena de consulta igual a `/content/luma/us/en.html`).
1. Agregue una acción a la regla. Utilice la variable **Principal** extensión y **Código personalizado** tipo de acción.

   ![Renderizar regla de héroe de página principal](assets/target-rule-render-hero.png)

   >[!TIP]
   >
   >Asigne nombres descriptivos a los eventos de reglas, las condiciones y las acciones en lugar de usar los nombres predeterminados. Los sólidos nombres de componentes de reglas hacen que los resultados de búsqueda sean mucho más útiles.

1. Introduzca el código personalizado para leer y realizar una acción en las propuestas devueltas por la respuesta del SDK web de Platform. El código personalizado de este ejemplo utiliza el método descrito en la guía para [renderización manual de contenido personalizado](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#manually-rendering-content). El código se ha adaptado para la variable `homepage-hero` ámbito de ejemplo con una acción de regla de etiqueta.

   ```javascript
   var propositions = event.propositions;
   
   var heroProposition;
   if (propositions) {
      // Find the hero proposition, if it exists.
      for (var i = 0; i < propositions.length; i++) {
         var proposition = propositions[i];
         if (proposition.scope === "homepage-hero") {
            heroProposition = proposition;
            break;
         }
      }
   }
   
   var heroHtml;
   if (heroProposition) {
      // Find the item from proposition that should be rendered.
      // Rather than assuming there a single item that has HTML
      // content, find the first item whose schema indicates
      // it contains HTML content.
      for (var j = 0; j < heroProposition.items.length; j++) {
         var heroPropositionItem = heroProposition.items[j];
         if (heroPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
            heroHtml = heroPropositionItem.data.content;
            break;
         }
      }
   }
   
   if (heroHtml) {
      // Hero HTML exists. Time to render it.
      var heroElement = document.querySelector(".heroimage");
      heroElement.innerHTML = heroHtml;
      // For this example, we assume there is only a signle place to update in the HTML.
   }
   
   // Send a "display" event 
   alloy("sendEvent", {
      xdm: {
         eventType: "propositionDisplay",
         _experience: {
            decisioning: {
               propositions: [
                  {
                     id: heroProposition.id,
                     scope: heroProposition.scope,
                     scopeDetails: heroProposition.scopeDetails
                  }
               ]
            }
         }
      }
   });
   ```

1. Guarde los cambios y créelos en la biblioteca
1. Cargue la página de inicio de Luma unas cuantas veces, lo que debería ser suficiente para hacer el nuevo `homepage-hero` registro del ámbito de decisión en la interfaz de Target.

### Configurar una actividad de Target con el Compositor de experiencias basadas en formularios

Ahora que tiene una regla para procesar manualmente un ámbito de decisión personalizado, puede crear otra actividad de segmentación de experiencias (XT) en Target. Esta vez utilice el Compositor de experiencias basadas en formularios.

1. Apertura [Adobe Target](https://experience.adobe.com/target)
1. Desactivar la actividad utilizada para la lección anterior
1. Crear una actividad de segmentación de experiencias (XT) con la opción del Compositor de experiencias basadas en formularios

   ![Crear una nueva actividad XT](assets/target-xt-create-form-activity.png)

1. Seleccione el **`homepage-hero`** ubicación desde el menú desplegable ubicación y **[!UICONTROL Crear oferta HTML]** en la lista desplegable de contenido. Si la ubicación no está disponible, puede escribirla. Target rellena periódicamente nuevos nombres de ubicación después de recibir solicitudes para esa ubicación o ámbito.

   ![Crear una nueva actividad XT](assets/target-xt-form-activity.png)

1. Pegue el siguiente código en el cuadro de contenido. Este código es un banner de pantalla completa básico con una imagen de fondo diferente:

   ```html
   <div class="we-HeroImage jumbotron" style="background-image: url('/content/luma/us/en/women/_jcr_content/root/hero_image.coreimg.jpeg');">
      <div class="container cq-dd-image">
         <div class="we-HeroImage-wrapper">
            <p class="h3">New Luma Yoga Collection</p>
            <strong class="we-HeroImage-title h1">Be active with style&nbsp;</strong>
            <p>
               <a class="btn btn-primary btn-action" href="/content/luma/us/en/products.html" role="button">Shop Now</a>
            </p>
         </div>
      </div>
   </div>
   ```

1. En el [!UICONTROL Objetivos y configuración] , elija Adobe Target como fuente de informes y [!UICONTROL Participación] > [!UICONTROL Vistas de páginas] como objetivo
1. Guarde la actividad
1. Si se siente cómodo con los cambios, puede activar su actividad. De lo contrario, si desea obtener una vista previa de la experiencia sin activar, puede copiar la variable [URL de vista previa de control de calidad](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html).
1. Cargue la página principal de Luma y debería ver los cambios aplicados

>[!NOTE]
>
>El objetivo de conversión &quot;Se hizo clic en mbox&quot; no funciona automáticamente. Dado que el SDK web de Platform no procesa automáticamente los ámbitos personalizados, no rastrea clics en ubicaciones en las que elija aplicar el contenido. Puede crear su propio rastreo de clics para cada ámbito utilizando el &quot;clic&quot; `eventType` con el `_experience` detalles usando la variable `sendEvent` acción.

### Validar con Debugger

Si ha activado la actividad, debería ver el contenido renderizado en la página. Sin embargo, aunque no haya actividades activas, también puede consultar la [!UICONTROL Enviar evento] llamada de red para confirmar que Target solicita contenido para sus ámbitos personalizados.

1. Abra la extensión del explorador de Adobe Experience Platform Debugger.
1. Vaya a la [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) y utilice el depurador para [cambie la propiedad tag del sitio a su propia propiedad de desarrollo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Vuelva a cargar la página
1. Seleccione el **[!UICONTROL Red]** herramienta en Debugger
1. Filtrar por **[!UICONTROL SDK web de Adobe Experience Platform]**
1. Seleccione el valor de la fila eventos para la primera llamada

   ![Llamada de red en Adobe Experience Platform Debugger](assets/target-debugger-network.png)

1. Tenga en cuenta que hay claves en `query` > `personalization` y  `decisionScopes` tiene un valor de `__view__` como antes, pero ahora también hay un `homepage-hero` ámbito incluido. Esta llamada del SDK web de Platform solicitó a Target que tomara decisiones sobre los cambios realizados con el VEC y las `homepage-hero` ubicación.

   ![__ver__ solicitud de decisionScope](assets/target-debugger-view-scope.png)

1. Cierre la superposición y seleccione los detalles del evento para la segunda llamada de red. Esta llamada solo está presente si Target ha devuelto una actividad.
1. Tenga en cuenta que hay detalles sobre la actividad y la experiencia que Target devuelve. Esta llamada del SDK web de Platform envía una notificación de que se ha renderizado una actividad de Target para el usuario e incrementa una impresión.

   ![Impresión de actividad de Target](assets/target-debugger-activity-impression.png)

## Pasar datos adicionales a Target

En esta sección, pasará datos específicos de Target y echará un vistazo a cómo se asignan los datos XDM a los parámetros de Target.

Existen algunos puntos de datos que pueden resultar útiles para Target y que no se asignan desde el objeto XDM. Estos parámetros especiales de Target incluyen:

* [Atributos de perfil](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/methods/in-page-profile-attributes.html?lang=en)
* [Atributos de entidad de Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en)
* [Parámetros reservados de Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html?lang=en#pass-behavioral)
* Valores de categoría para [afinidad de la categoría](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html?lang=en)

### Creación de elementos de datos para parámetros de Target

Primero debe configurar algunos elementos de datos adicionales para un atributo de perfil, atributo de entidad, valor de categoría y luego construir el `data` objeto que se utiliza para pasar datos que no son XDM:

* **`target.entity.id`** asignado a `digitalData.product.0.productInfo.sku`
* **`target.entity.name`** asignado a `digitalData.product.0.productInfo.title`
* **`target.user.categoryId`** con el siguiente código personalizado para analizar la dirección URL del sitio para la categoría de nivel superior:

   ```javascript
   var cat = location.pathname.split(/[/.]+/);
   if (cat[5] == 'products') {
      return (cat[6]);
   } else if (cat[5] != 'html') { 
      return (cat[5]);
   }
   ```

* **`data.content`** con el siguiente código personalizado:

   ```javascript
   var data = {
      __adobe: {
         target: {
            "entity.id": _satellite.getVar("target.entity.id"),
            "entity.name": _satellite.getVar("target.entity.name"),
            "profile.loggedIn": _satellite.getVar("user.profile.attributes.loggedIn"),
            "user.categoryId": _satellite.getVar("target.user.categoryId")
         }
      }
   }
   return data;
   ```

### Actualizar la regla de carga de página

Para pasar datos adicionales para Target fuera del objeto XDM es necesario actualizar cualquier regla aplicable. Para este ejemplo, la única modificación que debe realizar es incluir el nuevo **data.content** elemento de datos a la regla de carga de página genérica y a la regla de vista de página del producto.

1. Abra el `all pages - library load - AA & AT` regla
1. Seleccione el `Adobe Experience Platform Web SDK - Send event` acción
1. Agregue la variable `data.content` elemento de datos al campo de datos

   ![Añadir datos de destino a una regla](assets/target-rule-data.png)

1. Guarde los cambios y créelos en la biblioteca
1. Repita los pasos del 1 al 4 para **vista de producto - carga de biblioteca - AA** regla

>[!NOTE]
>
>El ejemplo anterior utiliza un `data` objeto que no se rellena completamente en todos los tipos de página. Las etiquetas gestionan esta situación apropiadamente y omiten las claves que tienen un valor indefinido. Por ejemplo, `entity.id` y `entity.name` no se pasaría en ninguna página aparte de los detalles del producto.

### Validar con el depurador

Ahora que las reglas se han actualizado, puede validar si los datos se están pasando correctamente con Adobe Debugger.

1. Vaya a la [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) e inicie sesión con el correo electrónico `test@adobe.com` y contraseña `test`
1. Vaya a la página de detalles del producto
1. Abra la extensión del explorador de Adobe Experience Platform Debugger y [cambie la propiedad tag a su propia propiedad de desarrollo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Vuelva a cargar la página
1. Seleccione el **Red** en Debugger y filtre por **SDK web de Adobe Experience Platform**
1. Seleccione el valor de la fila eventos para la primera llamada
1. Tenga en cuenta que hay claves en `data` > `__adobe` > `target` y se rellenan con información sobre el producto, la categoría y el estado de inicio de sesión.

   ![__ver__ solicitud de decisionScope](assets/target-debugger-data.png)

### Validar en la interfaz de Target

A continuación, consulte la interfaz de Target para confirmar que se recibieron los datos y que están disponibles para su uso en audiencias y actividades. Los datos XDM se asignan automáticamente a parámetros de Target personalizados. Puede validar que Target recibió datos XDM y que están disponibles creando una audiencia.

1. Apertura [Adobe Target](https://experience.adobe.com/target)
1. Vaya a la **[!UICONTROL Audiencias]** sección
1. Cree una audiencia y elija la **[!UICONTROL Personalizado]** tipo de atributo
1. Busque la variable **[!UICONTROL Parámetro]** campo para `web`. El menú desplegable debe rellenarse con todos los campos XDM relacionados con los detalles de la página web.

A continuación, valide que el atributo de perfil de estado de inicio de sesión se haya pasado correctamente.

1. Elija la **[!UICONTROL Perfil del visitante]** tipo de atributo
1. Buscar `loggedIn`. Si el atributo está disponible en el menú desplegable, se pasó correctamente a Target. Los nuevos atributos pueden tardar varios minutos en estar disponibles en la interfaz de usuario de Target.

Si tiene Target Premium, también puede validar que los datos de la entidad se pasaron correctamente y que los datos del producto se escribieron en el catálogo de productos de Recommendations.

1. Vaya a la **[!UICONTROL Recommendations]** sección
1. Select **[!UICONTROL Buscar en el catálogo]** en la navegación del lado izquierdo
1. Busque el SKU del producto o el nombre del producto que visitó anteriormente en el sitio de Luma. El producto debe aparecer en el catálogo de productos. Los nuevos productos pueden tardar varios minutos en buscarse en el catálogo de productos de Recommendations.

Ahora que ha completado esta lección, debe tener una implementación en funcionamiento de Adobe Target mediante el SDK web de Platform.

[Siguiente: ](setup-consent.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK web de Adobe Experience Platform. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
