---
title: Implementación del consentimiento con una plataforma de administración de consentimiento (CMP)
description: Obtenga información sobre cómo implementar y activar los datos de consentimiento obtenidos de una plataforma de administración de consentimiento (CMP) mediante la extensión SDK para web de Adobe Experience Platform en la recopilación de datos.
feature: Web SDK, Tags
level: Intermediate
doc-type: tutorial
exl-id: bee792c3-17b7-41fb-a422-289ca018097d
source-git-commit: e2594d3b30897001ce6cb2f6908d75d0154015eb
workflow-type: tm+mt
source-wordcount: '3320'
ht-degree: 2%

---

# Implementar el consentimiento con una plataforma de administración de consentimiento (CMP) mediante la extensión del SDK web de Platform

Muchas regulaciones legales de privacidad han introducido requisitos para un consentimiento activo y específico en lo que respecta a la recopilación de datos, personalización y otros casos de uso de marketing. Para cumplir estos requisitos, Adobe Experience Platform le permite capturar información de consentimiento en perfiles de clientes individuales y utilizar esas preferencias como un factor determinante en la forma en que se utilizan los datos de cada cliente en los flujos de trabajo de la plataforma descendente.

>[!NOTE]
>
>Adobe Experience Platform Launch se está integrando en Adobe Experience Platform como un conjunto de tecnologías de recopilación de datos. Se han implementado varios cambios terminológicos en la interfaz que debe tener en cuenta al utilizar este contenido:
>
> * El platform launch (lado del cliente) ahora es **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)**
> * El lado del servidor de platform launch ahora es **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Las configuraciones de Edge ahora son **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=es)**

Este tutorial muestra cómo implementar y activar los datos de consentimiento obtenidos de una plataforma de administración de consentimiento (CMP) mediante la extensión del SDK web de Platform en la recopilación de datos. Para ello, utilizaremos los estándares de Adobe y el estándar de consentimiento IAB TCF 2.0, con OneTrust o Sourcepoint como CMP de ejemplo.

Este tutorial utiliza la extensión del SDK web de Platform para enviar datos de consentimiento a Platform. Para obtener una descripción general del SDK web, consulte [esta página](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=es).

## Requisitos previos

Se enumeran los requisitos previos para utilizar el SDK web [aquí](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/prerequisite.html#fundamentals).

En esa página, hay un requisito para un &quot;Conjunto de datos de evento&quot; y, al igual que suena, este es un conjunto de datos para contener los datos de evento de experiencia. Para enviar información de consentimiento con eventos, la variable [Detalles del consentimiento de IAB TCF 2.0](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/iab/dataset.html) El grupo de campos debe añadirse al esquema de Experience Event:

![](./images/event-schema.png)

Para el estándar de consentimiento de plataforma v2.0, también necesitaremos acceso a Adobe Experience Platform para crear un esquema y un conjunto de datos de perfil individual XDM. Para ver un tutorial sobre la creación de esquemas, consulte [Creación de un esquema con el Editor de esquemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html#tutorials) y para el grupo de campos Detalles de consentimiento y preferencia requerido, consulte [Configurar un conjunto de datos para capturar datos de consentimiento y preferencia](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/dataset.html).

Este tutorial supone que tiene acceso a la recopilación de datos y que ha creado una propiedad de etiquetas del lado del cliente con la extensión del SDK web instalada y una biblioteca de trabajo creada y generada para el desarrollo. Estos temas se detallan y muestran en estos documentos:

* [Creación o configuración de una propiedad](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=en#create-or-configure-a-property)
* [Información general sobre bibliotecas](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html)
* [Información general sobre la publicación](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=es)

También vamos a usar el [Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) Extensión de Chrome para inspeccionar y validar la implementación.

Para implementar el ejemplo TCF de IAB con una CMP en su propio sitio, necesitará acceso a una CMP como OneTrust o Sourcepoint para generar los datos que proporcionan, o simplemente puede seguir aquí y ver los resultados a continuación.

## Uso del SDK web con el estándar de consentimiento de Adobe (v1.0 o v2.0)

>[!NOTE]
>
>El estándar 1.0 se está eliminando gradualmente a favor de la versión 2.0. El estándar 2.0 le permite agregar datos de consentimiento adicionales que se pueden utilizar para aplicar manualmente las preferencias de consentimiento. Las capturas de pantalla siguientes de la extensión del SDK web de Platform son de la versión [2.4.0](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html#version-2.4.0) de la extensión compatible con la versión 1.0 o 2.0 del Estándar de consentimiento de Adobe.

Para obtener más información sobre estos estándares, consulte [Compatibilidad con preferencias de consentimiento del cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html).

### Paso 1: Configurar el consentimiento en la extensión del SDK web

Después de instalar la extensión del SDK web de Platform en una propiedad de etiquetas, podemos configurar las opciones para abordar los datos de consentimiento en la pantalla de configuración de la extensión:

![](./images/pending.png)

La sección &quot;Privacidad&quot; establece el nivel de consentimiento para el SDK si el usuario no ha proporcionado previamente las preferencias de consentimiento. Esto establece el estado predeterminado para la recopilación de datos de evento y consentimiento en el SDK. La configuración elegida responde a la pregunta &quot;¿qué debe hacer el SDK si el usuario aún no ha proporcionado preferencias de consentimiento explícitas?&quot;

* En: recopile eventos que se producen antes de que el usuario proporcione preferencias de consentimiento.
* Salida: elimina eventos que se producen antes de que el usuario proporcione preferencias de consentimiento.
* Pendiente: eventos de cola que se producen antes de que el usuario proporcione preferencias de consentimiento.
* Proporcionado por el elemento de datos

Si la configuración de consentimiento predeterminada es &quot;En&quot;, esto indica al SDK que no debe esperar el consentimiento explícito y que debe recopilar los eventos que se producen antes de que el usuario proporcione las preferencias de consentimiento. Normalmente, estas preferencias se gestionan y almacenan en una CMP.

Si la configuración de consentimiento predeterminada es &quot;Fuera&quot;, esto indica al SDK que no debe recopilar ningún evento que se produzca antes de que se establezcan las preferencias de inclusión del usuario. La actividad del visitante que se produce antes de establecer la preferencia de consentimiento no se incluirá en ningún dato enviado por el SDK una vez establecido el consentimiento. Por ejemplo, si se desplaza y ve una página web antes de seleccionar el banner de consentimiento y se utiliza esta configuración de &quot;Salida&quot;, esa actividad de desplazamiento y el tiempo de visualización no se envían si el usuario proporciona posteriormente un consentimiento explícito para la recopilación de datos.

Si la configuración de consentimiento predeterminada es &quot;Pendiente&quot;, el SDK pondrá en cola cualquier evento que se produzca antes de que el usuario proporcione preferencias de consentimiento, por lo que los eventos pueden enviarse después de establecer las preferencias de consentimiento y después de que el SDK se haya configurado inicialmente durante una visita.

Con esta configuración &quot;Pendiente&quot;, si se intenta ejecutar cualquier comando que requiera preferencias de inclusión del usuario (por ejemplo, el comando de evento), el comando se colocará en la cola del SDK. Estos comandos no se procesarán hasta que haya comunicado las preferencias de inclusión del usuario al SDK.

Una vez que una CMP recopila las preferencias del usuario, podemos comunicarlas al SDK. En una sección posterior a continuación, veremos cómo obtener esos datos de inclusión y utilizarlos con la extensión del SDK web.

&quot;Proporcionado por el elemento de datos&quot; permite acceder a un elemento de datos que contiene cualquier dato de preferencia de consentimiento capturado por un código personalizado o una CMP en el sitio o en la capa de datos. Un elemento de datos utilizado para este fin debe resolverse como &quot;dentro&quot;, &quot;fuera&quot; o &quot;pendiente&quot;.

Tenga en cuenta lo siguiente: esta configuración del SDK no se mantiene para los perfiles de los usuarios; se trata de establecer el comportamiento del SDK antes de que el visitante proporcione las preferencias de consentimiento explícitas.

Para obtener más información sobre la configuración de la extensión del SDK web, consulte la [Información general sobre la extensión web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html?lang=en#configure-the-extension) y [Compatibilidad con preferencias de consentimiento del cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html).

Para este ejemplo, vamos a elegir la opción de Pendiente y seleccionar **Guardar** para guardar los ajustes de configuración.

### Paso 2: Comunicar las preferencias de consentimiento

Ahora que hemos establecido el comportamiento predeterminado del SDK, podemos utilizar etiquetas para enviar las preferencias de consentimiento explícito de un visitante a Platform. El envío de datos de consentimiento mediante el uso del estándar Adobe 1.0 o 2.0 se implementa fácilmente mediante `setConsent` acción del SDK web en las reglas de etiquetas.

#### Configuración del consentimiento con Platform Consent Standard 1.0

Vamos a crear una regla para demostrarlo. En la propiedad de etiquetas de Platform, seleccione Reglas y, a continuación, haga clic en el botón azul Agregar reglas. Asignemos a la regla el nombre &quot;setAdobeConsent&quot; y seleccione para añadir un evento. Para el Tipo de evento, elija &quot;Ventana cargada&quot; que almacenará en déclencheur esta regla cada vez que se cargue una página en nuestro sitio web. A continuación, en &quot;Acciones&quot;, seleccione &quot;Añadir&quot; para abrir la pantalla de configuración de la acción. Aquí es donde estableceremos los datos de consentimiento. Seleccione el menú desplegable &quot;Extensión&quot; y seleccione &quot;SDK web de Platform&quot;, luego seleccione el &quot;Tipo de acción&quot; y seleccione &quot;Definir consentimiento&quot;.

En &quot;Información de consentimiento&quot;, elija &quot;Rellenar un formulario&quot;. En esta acción de regla, utilizaremos el SDK web para establecer el consentimiento para el estándar de consentimiento de Adobe 1.0 rellenando el formulario mostrado:

![](./images/1-0-form.png)

Podemos elegir entre pasar &quot;Entrada&quot;, &quot;Salida&quot; o &quot;Proporcionado por el elemento de datos&quot; con esta acción Definir consentimiento. Un elemento de datos aquí debe resolverse como &quot;dentro&quot; o &quot;fuera&quot;.

En este ejemplo, seleccionaremos &quot;En&quot; para indicar que el visitante ha aceptado permitir que el SDK web envíe datos a Platform. Seleccione el botón azul &quot;Conservar cambios&quot; para guardar esta acción y, a continuación, seleccione &quot;Guardar&quot; para guardar esta regla.

Nota: Una vez que el visitante de un sitio web ha optado por no participar, el SDK no le permitirá establecer el consentimiento del usuario en.

Las reglas de etiquetas se pueden activar mediante una variedad de reglas integradas o personalizadas [eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/core/overview.html) que se puede utilizar para pasar estos datos de consentimiento en el momento adecuado durante una sesión de visitante. En el ejemplo anterior, se utilizó el evento de ventana cargada para almacenar en déclencheur la regla. En una sección posterior, utilizaremos un evento de preferencia de consentimiento de una CMP para almacenar en déclencheur una acción Definir consentimiento. Puede utilizar una acción Definir consentimiento en una regla activada por cualquier evento que prefiera que indique una configuración de preferencia de inclusión.

#### Configuración del consentimiento con Platform Consent Standard 2.0

La versión 2.0 del estándar de consentimiento de Platform funciona con [XDM](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schemas-and-experience-data-model.html?lang=es) datos. También requiere agregar el grupo de campos Detalles de consentimiento y preferencia al esquema de perfil en Platform. Consulte [Procesamiento de consentimiento en Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/overview.html) para obtener más información sobre Adobe standard versión 2.0 y este grupo de campos.

Crearemos un elemento de datos de código personalizado para pasar datos a las propiedades de recopilación y metadatos del objeto de consentimientos que se muestra en el esquema siguiente:

![](./images/collect-metadata.png)

Este grupo de campos Consentimientos y Detalles de preferencias contiene campos para [Tipo de datos XDM de consentimientos y preferencias](https://experienceleague.adobe.com/docs/experience-platform/xdm/data-types/consents.html#prerequisites) que contendrá los datos de preferencia de consentimiento que enviamos a Platform con la extensión del SDK web de Platform en nuestra acción de regla. Actualmente, las únicas propiedades requeridas para implementar Platform Consent Standard 2.0 son el valor recopilado (val) y el valor de tiempo de los metadatos, resaltados arriba en rojo.

Vamos a crear un elemento de datos para estos datos. Seleccione Elementos de datos y el botón azul Agregar elemento de datos. Llamemos a esto &quot;xdm-consent 2.0&quot; y, utilizando la extensión principal, seleccionaremos un tipo de código personalizado. Puede introducir o copiar y pegar los siguientes datos en la ventana del editor de código personalizado:

```js
var dateString = new Date().toISOString();

return {
  collect: {
    val: "y"
  },
  metadata: {
    time: dateString
  }
}
```

El campo de tiempo debe especificar cuándo actualizó el usuario por última vez sus preferencias de consentimiento. Aquí se crea una marca de tiempo como ejemplo utilizando un método estándar en el objeto Date de JavaScript. Seleccione Guardar para guardar el código personalizado y, a continuación, seleccione Guardar de nuevo para guardar el elemento de datos.

A continuación, seleccionemos Reglas y, luego, el botón azul Agregar regla e introduzca el nombre &quot;setConsent onLoad - Consent 2.0&quot;. Vamos a elegir el evento Window Loaded como déclencheur de regla y, a continuación, seleccione Añadir en Acciones. Seleccione la extensión del SDK web de Platform y, para el tipo de acción, elija Definir consentimiento. El estándar debe ser Adobe y la versión debe ser 2.0. En Valor, utilizaremos el elemento de datos que acabamos de crear que contiene los valores de recopilación y tiempo que necesitamos enviar a Platform:

![](./images/2-0-form.png)

Para revisar esta acción de ejemplo, se llama a Set Consent desde la extensión del SDK web de Platform y se pasan el estándar y la versión desde el formulario, al tiempo que se pasan los valores de tiempo de recopilación y eliminación desde el elemento de datos que hemos creado anteriormente.

Seleccione el botón azul Guardar y vuelva a intentarlo para guardar la regla.

Ahora tenemos dos reglas, una para cada uno de los estándares de consentimiento de plataforma. En la práctica, es probable que elija un estándar en los sitios. A continuación, crearemos un ejemplo utilizando el estándar de consentimiento IAB TCF 2.0.

## Uso del SDK web con el estándar de consentimiento IAB TCF 2.0

Puede obtener más información sobre la versión 2.0 del marco de transparencia y consentimiento de IAB en la [Sitio web de IAB Europe](https://iabeurope.eu/transparency-consent-framework/).

Para establecer los datos de preferencia de consentimiento mediante este estándar, se debe añadir el grupo de campos de esquema Detalles del consentimiento TCF 2.0 de IAB a nuestro esquema de Evento de experiencia en Platform:

![](./images/consentStrings.png)

Este grupo de campos contiene los campos de preferencia de consentimiento requeridos por el estándar IAB TCF 2.0. Para obtener más información sobre esquemas y grupos de campos, consulte la [Información general del sistema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es).

### Paso 1: Crear un elemento de datos de consentimiento

Para enviar datos de evento de consentimiento desde etiquetas mediante el estándar de consentimiento IAB TCF 2.0, primero configuramos un elemento de datos xdm con los campos de consentimiento requeridos:

![](./images/data-element.png)

En la propiedad del lado del cliente de etiquetas, seleccione Elementos de datos y el botón azul &quot;Agregar elemento de datos&quot;. Asignaremos el nombre &quot;xdm-permissionStrings&quot; a este elemento de datos para este ejemplo. Estos campos xdm contienen los datos de consentimiento del usuario necesarios para el estándar IAB TCF 2.0.

En el menú desplegable Extensión, elija &quot;Platform Web SDK&quot; y, para Tipo de elemento de datos, elija &quot;Objeto XDM&quot;. Debe aparecer el asignador xdm, que le permite seleccionar y expandir el elemento &quot;permissionStrings&quot; como se muestra en la captura de pantalla anterior.

Estableceremos cada una de las permissionStrings de la siguiente manera:

* **`consentStandard`**:  `IAB TCF`
* **`consentStandardVersion`**:  `2.0`
* **`consentStringValue`**:  `%IAB TCF Consent String%`
* **`containsPersonalData`**:  `False` (elegido desde el botón Seleccionar valor )
* **`gdprApplies`**:  `%IAB TCF Consent GDPR%`

El `consentStandard` y `consentStandardVersion` Los campos de son cadenas de texto para el estándar que utilizamos, que es IAB TCF versión 2.0. El `consentStringValue` hace referencia a un elemento de datos denominado &quot;IAB TCF Consent String&quot;. Los símbolos de porcentaje que rodean el texto indican el nombre de un elemento de datos, y lo veremos en un momento. El `containsPersonalData` Este campo indica si la cadena de consentimiento TCF 2.0 de IAB contiene datos personales con &quot;Verdadero&quot; o &quot;Falso&quot;. El `gdprApplies` Este campo indica &quot;true&quot; para las aplicaciones de RGPD, &quot;false&quot; para las de RGPD no se aplica o &quot;undefined&quot; para desconocido si se aplica RGPD. Actualmente, el SDK web trata &quot;undefined&quot; como &quot;true&quot;, por lo que los datos de consentimiento enviados con &quot;gdprApplied: undefined&quot; se tratan como si el visitante se encuentra en un área en la que se aplica el RGPD.

Consulte la [documentación de consentimiento](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/iab-tcf/with-launch.html#getting-started) para obtener más información sobre estas propiedades y sobre IAB TCF 2.0 en etiquetas.

### Paso 2: Crear una regla para establecer el consentimiento con el estándar IAB TCF 2.0

A continuación, creamos una regla para establecer el consentimiento con el SDK web cuando un visitante del sitio web establece o cambia los datos de consentimiento para este estándar. En esta regla, también veremos cómo capturar esas señales de cambio de consentimiento de una CMP como [OneTrust](https://www.onetrust.com/products/cookie-consent/) o [Sourcepoint](https://www.sourcepoint.com/cmp/).

#### Añadir un evento de regla

Seleccione la sección Reglas en la propiedad de etiquetas de Platform y, a continuación, haga clic en el botón azul Agregar regla. Asignemos un nombre al conjunto de reglas: Consentimiento: IAB y seleccione Añadir en Eventos. Asignemos un nombre a este evento tcfapi addEventListener y seleccione Abrir editor para abrir el editor de código personalizado.

Copie y pegue el siguiente código en la ventana del editor:

```js
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString properties in data elements
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Este código simplemente crea y ejecuta una función llamada `addEventListener`. La función comprueba si la variable `window.__tcfapi` El objeto existe y, si es así, agrega un detector de eventos según las especificaciones de la API. Puede leer más sobre estas especificaciones en la [IAB repo](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework) en GitHub. Si este oyente de eventos se agrega correctamente y el visitante del sitio web ha completado sus opciones de consentimiento y preferencias, el código establece etiquetas de variables personalizadas para el `tcData.tcString`y el indicador de las regiones de RGPD. De nuevo, para obtener más información sobre el TCF de la IAB, consulte la IAB [sitio web](https://iabeurope.eu/transparency-consent-framework/) y [Repositorio de GitHub](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework) para obtener más información técnica. Después de establecer esos valores, el código ejecuta la función de déclencheur que déclencheur esta regla para que se ejecute.

Si la variable `window.__tcfapi` el objeto no existía la primera vez que se ejecutó esta función, la función lo comprobará de nuevo cada 100 milisegundos, por lo que se puede agregar el detector de eventos. La última línea de código simplemente ejecuta el `addEventListener` función definida en las líneas de código encima de ella.

En resumen, hemos creado una función para comprobar el estado del consentimiento que establece un visitante del sitio web mediante un banner de consentimiento CMP (o personalizado). Cuando se establece esa preferencia de consentimiento, este código crea dos variables personalizadas (elementos de datos de código personalizado) que podemos utilizar en la acción de regla. Después de pegar el código anterior en la ventana del editor de código personalizado del evento, seleccione el botón azul Guardar para guardar el evento de regla.

Ahora vamos a configurar la acción de regla Establecer consentimiento para utilizar estos valores y enviarlos a Platform.

#### Añadir una acción de regla

Seleccione Añadir en la sección Acciones. En Extensión, elija SDK web de Platform en la lista desplegable. En Tipo de acción, seleccione Definir consentimiento. Asignemos un nombre a esta acción setConsent.

En la configuración de acción en Información de consentimiento, elija Rellenar un formulario. En Estándar, seleccione IAB TCF y, en Versión, introduzca 2.0. Para el valor, utilizaremos la variable personalizada de nuestro evento e introduciremos `%IAB TCF Consent String%` que proviene del [tcData](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md#tcdata) hemos capturado en nuestra función personalizada de evento de regla anterior.

En Se aplica el RGPD utilizaremos la otra variable personalizada de nuestro evento e introduciremos `%IAB TCF Consent GDPR%` que también proviene del `tcData` hemos capturado en nuestra función personalizada de evento de regla anterior. Si sabe que el RGPD se aplicará o no definitivamente a los visitantes de este sitio web, puede seleccionar Sí o No, según corresponda, en lugar de utilizar la opción de variable personalizada (elemento de datos). También puede utilizar la lógica condicional en un elemento de datos para comprobar si se aplica el RGPD y devolver el valor adecuado.

En El RGPD contiene datos personales, seleccione la opción para indicar si los datos de este usuario contienen datos personales. Un elemento de datos aquí debe resolverse como verdadero o falso.

![](./images/data-element-2-0.png)

Seleccione el botón azul Guardar para guardar la acción y el botón azul Guardar (o Guardar en biblioteca) para guardar la regla. En este punto, ha implementado correctamente el elemento de datos y la regla en las etiquetas para establecer el consentimiento mediante la extensión del SDK web con el estándar de consentimiento IAB TCF 2.0.

### Paso 3: Guardar en biblioteca y crear

Si está utilizando el [biblioteca de trabajo](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-data-elements-rules.html#use-the-working-library-feature) requisito previo, ya ha guardado estos cambios y ha creado su biblioteca de desarrollo:

![](./images/save-library.png)

### Paso 4: Inspect y validación de la recopilación de datos

En nuestro sitio, actualizamos la página y confirmamos la compilación de la biblioteca en [Depurador](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) Extensión de Chrome, en la sección de menú de etiquetas:

![](./images/build-date.png)

También podemos inspeccionar la llamada de setConsent para los estándares Adobe 1.0 o 2.0 en la sección SDK web de Debugger Platform, seleccionando en la línea Cuerpo del POST en la solicitud de red donde ve `{"consent":[{"value":{"general":"in"},"version…`:

![](./images/inspect-consent-call.png)

Para validar la llamada de setConsent y nuestra regla para el estándar IAB TCF 2.0, utilizaremos el banner de consentimiento de OneTrust en nuestro sitio de prueba para establecer nuestras preferencias de consentimiento y crear el tcData descrito anteriormente:

![](./images/banner.png)

Después de seleccionar &quot;Acepto&quot;, podemos inspeccionar la llamada de setConsent para el estándar IAB TCF 2.0 en la sección del SDK web de la plataforma de Debugger, seleccionando en la línea Cuerpo del POST en la solicitud de red donde ve `{"consent":[{"value":"someAlphaNumericCharacters…`.

![](./images/inspect-2-0.png)

Aquí vemos los datos que configuramos anteriormente en nuestros elementos de datos y reglas de etiquetas. La propiedad value contiene los datos tcString codificados que vimos anteriormente.

OneTrust, Sourcepoint y otras CMP que implementan el estándar IAB TCF 2.0 producirán datos similares en nuestras páginas. Podemos capturar esos datos y utilizarlos con la extensión del SDK web en etiquetas utilizando el evento de código personalizado en la regla que hemos creado anteriormente. El código personalizado es el mismo independientemente de la CMP utilizada para generar los datos de IAB TCF 2.0. El código personalizado también se puede utilizar con cualquiera de los estándares de consentimiento de plataforma (1.0 o 2.0).

## Envío de datos de consentimiento con eventos de experiencia

Es posible que haya notado que no hicimos referencia al elemento de datos xdm-permissionStrings que creamos anteriormente en un campo de elemento de datos en ninguna de nuestras reglas. Este elemento de datos es útil cuando necesita enviar datos de consentimiento con un evento de experiencia.

![](./images/consentStrings-data-element.png)

Dado que este elemento de datos contiene todos los campos requeridos para el estándar IAB TCF 2.0, puede simplemente hacer referencia al elemento de datos al enviar estos datos xdm con los eventos de experiencia:

![](./images/consentStrings-reference.png)

## Conclusión

Ahora que hemos inspeccionado y validado los datos, debe ver cómo implementar y activar los datos de consentimiento obtenidos de una CMP mediante la extensión SDK para web de Platform.
