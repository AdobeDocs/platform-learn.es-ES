---
title: Reemplazar la biblioteca | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre cómo migrar una implementación de Adobe Target de at.js 2.x al SDK web de Adobe Experience Platform. Los temas incluyen descripción general de la biblioteca, diferencias de implementación y otras llamadas importantes.
source-git-commit: 63edfc214c678a976fbec20e87e76d33180e61f1
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 1%

---

# Reemplazar la biblioteca at.js por el SDK web de plataforma

Obtenga información sobre cómo reemplazar la implementación de Adobe Target en la página para migrar de at.js al SDK web de Platform. Una sustitución básica consiste en los siguientes pasos:

* Revise la configuración de administración de Target y tome nota de su ID de organización de IMS
* Reemplazar la biblioteca at.js por el SDK web de plataforma
* Actualizar el fragmento de preocultación para implementaciones de biblioteca sincrónica
* Configuración del SDK web de Platform en la página

>[!NOTE]
>
>Los ejemplos proporcionados son ilustrativos y la implementación real de Target puede variar. Si la implementación de Target existente utiliza el administrador de etiquetas de recopilación de datos de Adobe, también puede consultar la [Tutorial de implementación de Platform Web SDK Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html) para obtener más información.


## Revisión de la configuración de administración de Target

El primer paso para migrar Target al SDK web de plataforma es revisar la configuración en la **[!UICONTROL Administración]** para obtener más información.

### [!UICONTROL Implementación]

#### [!UICONTROL Detalles de la cuenta]

* **[!UICONTROL ID de organización de IMS]** : Tenga en cuenta este valor, ya que es necesario configurar el SDK web de Platform.
* **[!UICONTROL Toma de decisiones en el dispositivo]** : Esta función no es compatible con el SDK web de Platform. Esta configuración se puede deshabilitar después de migrar y si ya no utiliza at.js en ninguno de sus sitios web, o si tiene algún caso de uso del lado del servidor para la toma de decisiones en dispositivos.

#### [!UICONTROL Métodos de implementación]

Todos los ajustes editables de **[!UICONTROL Métodos de implementación]** solo se aplican a at.js. Esta configuración se utiliza para generar una biblioteca at.js personalizada para la implementación. Revise esta configuración para comprobar si tiene código personalizado o está configurando cookies individuales y de terceros para casos de uso entre dominios.

La variable **[!UICONTROL Duración del perfil]** solo puede modificarla el Servicio de atención al cliente de Adobe. La duración del perfil del visitante de Target no se ve afectada por su método de implementación. Tanto at.js como el SDK web de plataforma utilizan la misma duración del perfil del visitante.

#### [!UICONTROL Privacidad]

* **[!UICONTROL Proteger direcciones IP de visitantes]** - Esta configuración afecta a las capacidades de segmentación geográfica. Tanto at.js como el SDK web de la plataforma utilizan la misma configuración de confusión de IP de back-end para fines de segmentación geográfica.

### [!UICONTROL Entornos]

El SDK web de Platform utiliza una configuración de conjunto de datos que le permite definir explícitamente una [!UICONTROL ID de entorno] para conjuntos de datos de desarrollo, ensayo y producción independientes. El caso de uso principal de esta configuración es para implementaciones de aplicaciones móviles en las que no existen direcciones URL para distinguir fácilmente los entornos. La configuración es opcional, pero se puede utilizar para garantizar que todas las solicitudes estén correctamente asociadas al entorno especificado. Esto difiere de una implementación de at.js en la que debe asignar entornos de Target en función de dominios y reglas de grupos de hosts.

>[!NOTE]
>
>Si no se especifica un ID de entorno en la configuración del conjunto de datos, Target utiliza la asignación de dominio a entorno como se especifica en la variable **Hosts** para obtener más información.

Para obtener más información, consulte [configuración de datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) guía y Target [Hosts](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) documentación.

## Implementación del SDK web de Platform

La funcionalidad de Target la proporcionan at.js y el SDK web de plataforma. Si ambas bibliotecas se utilizan al mismo tiempo, es posible que experimente problemas de procesamiento y seguimiento. Para migrar correctamente al SDK web de Platform, el primer paso es eliminar at.js y sustituirlo por el SDK web de Platform (alloy.js).

Supongamos que tenemos una implementación de Target sencilla con at.js:

* Una capa de datos cerca de la parte superior de la página proporciona información para Target y otras aplicaciones
* Una o más bibliotecas de ayuda de terceros cuyas capacidades se puedan usar en actividades de Target (por ejemplo, jQuery)
* Un fragmento de preocultación para mitigar el parpadeo
* La biblioteca at.js de Target se carga asincrónicamente con la configuración predeterminada para solicitar y procesar automáticamente actividades:

+++Ejemplo de at.js en una implementación de una página de HTML

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>
  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
  <!--prehiding snippet for Target with asynchronous deployment-->
  <script>
    ;(function(win, doc, style, timeout) {
      var STYLE_ID = 'at-body-style';

      function getParent() {
        return doc.getElementsByTagName('head')[0];
      }

      function addStyle(parent, id, def) {
        if (!parent) {
          return;
        }
        var style = doc.createElement('style');
        style.id = id;
        style.innerHTML = def;
        parent.appendChild(style);
      }

      function removeStyle(parent, id) {
        if (!parent) {
          return;
        }
        var style = doc.getElementById(id);
        if (!style) {
          return;
        }
        parent.removeChild(style);
      }
      addStyle(getParent(), STYLE_ID, style);
      setTimeout(function() {
        removeStyle(getParent(), STYLE_ID);
      }, timeout);
    }(window, document, "body {opacity: 0 !important}", 3000));
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div>Homepage Hero Banner Content</div>
</body>
</html>
```

+++

Para actualizar Target para que utilice el SDK web de plataforma, elimine primero at.js:

```HTML
<!--Target at.js library loaded asynchonously-->
<script src="/libraries/at.js" async></script>
```

Y sustitúyalo por la versión compatible actual del SDK web de Platform (alloy.js):

```HTML
<!--Platform Web SDK base code-->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
<script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
```

La versión independiente prediseñada requiere un &quot;código base&quot; añadido directamente a la página que crea una función global denominada alloy. Utilice esta función para interactuar con el SDK. Si desea especificar otra cosa para la función global, cambie la variable `alloy` nombre.

>[!TIP]
>
> Al utilizar la función de etiquetas (anteriormente Launch) para implementar el SDK web, la biblioteca alloy.js se añade a la biblioteca de etiquetas añadiendo la extensión del SDK web de Adobe Experience Platform.


Consulte la [Instalación del SDK web de Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=es) documentación para obtener más información y opciones de implementación.


## Actualizar el enfoque de preocultación de contenido

La implementación del SDK web de Platform puede requerir un fragmento de ocultamiento previo en función de si la biblioteca se carga de forma asíncrona o sincrónica.

### Implementación asíncrona

Al igual que con at.js, si la biblioteca del SDK web de Platform se carga asincrónicamente, la página puede finalizar el procesamiento antes de que Target haya realizado un intercambio de contenido. Este comportamiento puede conllevar lo que se conoce como &quot;parpadeo&quot;, por el cual el contenido predeterminado aparece brevemente antes de ser reemplazado por el contenido personalizado especificado por Target. Si desea evitar este parpadeo, Adobe recomienda añadir un fragmento preocultado especial inmediatamente antes de la referencia asíncrona de script del SDK web de Platform.

Si su implementación es asíncrona, como en el ejemplo anterior, sustituya el fragmento de preocultación de at.js por la versión siguiente compatible con el SDK web de Platform:

```HTML
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
</script>
```

El fragmento preocultado crea una etiqueta de estilo en el encabezado de la página con la definición CSS de su elección. Esta etiqueta de estilo se elimina cuando se recibe una respuesta de Target o se alcanza el tiempo de espera.

El comportamiento de preocultación se controla mediante dos configuraciones al final del fragmento.

* `body { opacity: 0 !important }` especifica la definición de CSS que se utiliza para la preocultación hasta que se carga Target. De forma predeterminada, toda la página está oculta. Puede actualizar esta definición a los selectores que desee ocultar previamente, así como a cómo desea ocultarlos. Puede incluir varias definiciones, ya que este valor es simplemente lo que se inserta en la etiqueta de estilo de preocultación. Si tiene un elemento contenedor fácil de identificar que ajuste el contenido debajo de su navegación, puede utilizar esta configuración para limitar la preocultación a ese elemento contenedor.

* `3000` especifica el tiempo de espera en milisegundos para la preocultación. Si no se recibe una respuesta de Target antes del tiempo de espera, se elimina la etiqueta de estilo de ocultamiento previo. No es habitual alcanzar este tiempo de espera.

>[!NOTE]
>
>Asegúrese de utilizar el fragmento de código correcto para el SDK web de Platform, ya que utiliza un ID de estilo diferente de `alloy-prehiding`. Si se utiliza el fragmento de preocultación para at.js, es posible que no funcione correctamente.

### Implementación sincrónica

Adobe recomienda implementar el SDK web de Platform asincrónicamente para obtener el mejor rendimiento general de la página. Sin embargo, si la biblioteca se carga sincrónicamente, el fragmento de ocultamiento previo no es necesario. En su lugar, el estilo de preocultación se especifica en la configuración del SDK web de Platform.

El estilo de preocultación para implementaciones sincrónicas se puede configurar usando la variable [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) . La configuración del SDK web de plataforma se explica en la siguiente sección.

Para obtener más información sobre cómo el SDK web de Platform puede administrar el parpadeo, consulte la sección de la guía:  [gestión del parpadeo para experiencias personalizadas](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html)

## Configuración del SDK web de Platform

El SDK web de Platform debe configurarse en cada carga de página. El siguiente ejemplo supone que todo el sitio se está actualizando al SDK web de Platform en una sola implementación:

>[!BEGINTABS]

>[!TAB JavaScript]

La variable `configure` siempre debe ser el primer comando de SDK llamado . La variable `edgeConfigId` es la variable [!UICONTROL ID de almacén de datos]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

>[!TAB Etiquetas]

En las implementaciones de etiquetas, muchos campos se rellenan automáticamente o se pueden seleccionar desde los menús desplegables. Tenga en cuenta que diferentes plataformas [!UICONTROL entornos limitados] y [!UICONTROL datastreams] se puede seleccionar para cada entorno. El conjunto de datos cambiará según el estado de la biblioteca de etiquetas en el proceso de publicación.

![configuración de la extensión de etiqueta de SDK web](assets/tags-config.png){zoomable=&quot;yes&quot;}
>[!ENDTABS]

Si planea migrar de at.js al SDK web de plataforma página por página, se necesitan las siguientes opciones de configuración:


>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled":true,
  "idMigrationEnabled":true
});
```

>[!TAB Etiquetas]

![configuración de las opciones de migración de la extensión de etiqueta SDK web](assets/tags-config-migration.png){zoomable=&quot;yes&quot;}
>[!ENDTABS]

A continuación se describen las opciones de configuración importantes relacionadas con Target:

| Opción | Descripción | Valor de ejemplo |
| --- | --- | --- |
| `edgeConfigId` | ID del conjunto de datos | `ebebf826-a01f-4458-8cec-ef61de241c93` |
| `orgId` | ID de organización de Adobe Experience Cloud | `ADB3LETTERSANDNUMBERS@AdobeOrg` |
| `targetMigrationEnabled` | Utilice esta opción para permitir que el SDK web lea y escriba las cookies mbox y mboxEdgeCluster heredadas que utiliza at.js. Esto le ayuda a mantener el perfil del visitante mientras se mueve de una página que utiliza el SDK web a una página que utiliza la biblioteca at.js y del modo contrario. | `true` |
| `idMigrationEnabled` | Si es true, el SDK lee y establece cookies AMCV antiguas. Esta opción ayuda con la transición al uso del SDK web de Platform, mientras que algunas partes del sitio pueden seguir utilizando Visitor.js. | `true` |
| `thirdPartyCookiesEnabled` | Habilita la configuración de cookies de terceros de Adobe. El SDK puede mantener el ID de visitante en un contexto de terceros para permitir que se use el mismo ID de visitante en todos los sitios. Utilice esta opción si tiene varios sitios; sin embargo, a veces esta opción no es deseada por motivos de privacidad. | `true` |
| `prehidingStyle` | Se utiliza para crear una definición de estilo CSS que oculte áreas de contenido de su página web mientras se carga contenido personalizado desde el servidor. Esto solo se utiliza con implementaciones sincrónicas del SDK. | `body { opacity: 0 !important }` |

Para obtener una lista completa de las opciones, consulte la [configuración del SDK web de Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=es) guía.

## Ejemplo de implementación

Una vez que el SDK web de Platform esté correctamente colocado, la página de ejemplo tendría este aspecto.

>[!BEGINTABS]

>[!TAB JavaScript]

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

>[!TAB Etiquetas]

Código de página:

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

En las etiquetas , agregue la extensión web SDK de Adobe Experience Platform:

![Añadir la extensión del SDK web de Adobe Experience Platform](assets/library-tags-addExtension.png){zoomable=&quot;yes&quot;}

Y agregue las configuraciones deseadas:
![configuración de las opciones de migración de la extensión de etiqueta SDK web](assets/tags-config-migration.png){zoomable=&quot;yes&quot;}


>[!ENDTABS]



Es importante tener en cuenta que, al incluir y configurar la biblioteca del SDK web de la plataforma como se muestra arriba, no se ejecuta ninguna llamada de red a la red de Adobe Edge.

A continuación, aprenda a [solicitar y aplicar actividades basadas en VEC](render-vec-activities.md) a la página.

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).