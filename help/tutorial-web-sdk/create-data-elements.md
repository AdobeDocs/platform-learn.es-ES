---
title: Creación de elementos de datos
description: Obtenga información sobre cómo crear un objeto XDM y asignarle elementos de datos en etiquetas. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Tags
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: fe03ee89bfccd0105b45383c84403b6a3d230235
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 5%

---

# Creación de elementos de datos

Obtenga información sobre cómo crear los elementos de datos esenciales necesarios para capturar datos con el SDK web de Experience Platform. Recopilar datos de contenido e identidad en [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Aprenda a utilizar el esquema XDM creado anteriormente para recopilar datos mediante el SDK web de Platform a través de un nuevo tipo de elemento de datos denominado objeto XDM.

>[!NOTE]
>
> Para fines de demostración, los ejercicios de esta lección se basan en el ejemplo utilizado durante [Configuración de un esquema](configure-schemas.md) paso; creación de objetos XDM de ejemplo que capturan el contenido visualizado y las identidades de los usuarios en la [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>Los datos de esta lección provienen de `[!UICONTROL digitalData]` en el sitio de Luma. Para ver la capa de datos, abra la consola de desarrollador y escriba `[!UICONTROL digitalData]` para ver la capa de datos completa disponible.![capa de datos digitalData](assets/data-element-data-layer.png)


Independientemente del SDK web de Platform, debe seguir creando elementos de datos dentro de la propiedad de etiquetas que se asignen a variables de recopilación de datos desde el sitio web, como una capa de datos, un atributo de HTML, etc. Una vez creados esos elementos de datos, debe asignarlos al esquema XDM creado durante la [configuración de esquemas](configure-schemas.md) lección. Para ello, la extensión del SDK web de Platform pone a disposición un nuevo tipo de elemento de datos denominado objeto XDM. Por lo tanto, la creación de elementos de datos consta de dos acciones:

1. Asignación de variables de sitio web a elementos de datos y
1. Asignación de esos elementos de datos a un objeto XDM

Para el paso 1, siga asignando la capa de datos a los elementos de datos del modo en que lo hace actualmente, utilizando cualquiera de los tipos de elementos de datos de la extensión de etiqueta principal. Para el paso 2, la extensión del SDK web de Platform crea un conjunto de nuevos tipos de elementos de datos que no estaban disponibles anteriormente:

* ID de combinación de eventos
* Mapa de identidad
* Objeto XDM

Esta lección se centra en los tipos de elementos de datos de mapa de identidad y objeto XDM. Creará objetos XDM para capturar la actividad y el estado de autenticación de los visitantes de Luma.

## Objetivos de aprendizaje

Al final de esta lección, puede hacer lo siguiente:

* Creación de elementos de datos para capturar contenido y datos de ID de inicio de sesión del usuario
* Creación de un elemento de datos de mapa de identidad
* Asignar elementos de datos a un elemento de datos de objeto XDM


## Requisitos previos

Comprenderá qué es una capa de datos y se familiarizará con el [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} capa de datos y cómo hacer referencia a elementos de datos en etiquetas. Debe haber completado los siguientes pasos anteriores en el tutorial

* [Configure los permisos](configure-permissions.md)
* [Configuración de un esquema XDM](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)
* [Configurar una secuencia de datos](configure-datastream.md)
* [Extensión del SDK web instalada en la propiedad de etiqueta](install-web-sdk.md)

>[!IMPORTANT]
>
>El [Extensión del servicio de ID de Experience Cloud](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) no es necesaria al implementar el SDK web de Adobe Experience Platform, ya que la funcionalidad del servicio de ID está integrada en el SDK web de Platform.

## Creación de elementos de datos para capturar la capa de datos

Antes de empezar a crear el objeto XDM, cree el siguiente conjunto de elementos de datos asignados a [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} capa de datos:

1. Ir a **[!UICONTROL Elementos de datos]** y seleccione **[!UICONTROL Añadir elemento de datos]** (o **[!UICONTROL Crear nuevo elemento de datos]** si no hay elementos de datos existentes en la propiedad etiqueta )

   ![Crear elemento de datos](assets/data-element-create.jpg)

1. Asigne un nombre al elemento de datos `page.pageInfo.pageName`.
1. Utilice el **[!UICONTROL Variable JavaScript]** **[!UICONTROL Tipo de elemento de datos]** para señalar a un valor de la capa de datos de Luma: `digitalData.page.pageInfo.pageName`

1. Marque las casillas de **[!UICONTROL Forzar valor en minúsculas]** y **[!UICONTROL Limpiar texto]** para estandarizar el caso y eliminar espacios superfluos.

1. Salir `None` como el **[!UICONTROL Duración del almacenamiento]** ya que este valor es diferente en cada página

1. Seleccione **[!UICONTROL Guardar]**

   ![Elemento de datos Nombre de página](assets/data-element-pageName.jpg)

Siga los mismos pasos para crear estos cuatro elementos de datos adicionales:

* **`page.pageInfo.server`**  asignado a
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  asignado a
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  asignado a
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** asignado a
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** asignado a `digitalData.cart.orderId` (utilizará esto durante la [Análisis de configuración](setup-analytics.md) lección)


>[!CAUTION]
>
>El [!UICONTROL Variable JavaScript] el tipo de elemento de datos trata las referencias de matriz como puntos en lugar de corchetes, por lo que hacer referencia al elemento de datos username como `digitalData.user[0].profile[0].attributes.username` **no funcionará**.

## Crear elemento de datos del mapa de identidad

A continuación, puede crear el elemento de datos del mapa de identidad:

1. Ir a **[!UICONTROL Elementos de datos]** y seleccione **[!UICONTROL Añadir elemento de datos]**

1. **[!UICONTROL Nombre]** el elemento de datos `identityMap.loginID`

1. Como el **[!UICONTROL Extensión]**, seleccione `Adobe Experience Platform Web SDK`

1. Como el **[!UICONTROL Tipo de elemento de datos]**, seleccione `Identity map`

1. Se mostrará un área de pantalla a la derecha dentro de **[!UICONTROL Interfaz de recopilación de datos]** para configurar la identidad:

   ![Interfaz de recopilación de datos](assets/identity-identityMap-setup.png)

1. Como el  **[!UICONTROL Área de nombres]**, seleccione la `Luma CRM Id` área de nombres que creó anteriormente en [Configurar identidades](configure-identities.md) lección.

   >[!NOTE]
   >
   >    Si no ve su `Luma CRM Id` , compruebe que también lo creó en su zona protegida de producción predeterminada. Actualmente, solo se muestran en la lista desplegable de áreas de nombres las áreas de nombres creadas en la zona protegida de producción predeterminada.

1. Después del **[!UICONTROL Área de nombres]** se ha seleccionado, se debe establecer un ID. Seleccione el `user.profile.attributes.username` Elemento de datos creado anteriormente en esta lección, que captura un ID cuando los usuarios inician sesión en el sitio de Luma.

<!--  >[!TIP]
   >
   >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
   >
   >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
-->

1. Como el **[!UICONTROL Estado autenticado]**, seleccione **[!UICONTROL Autenticado]**
1. Seleccionar **[!UICONTROL Principal]**

1. Seleccione **[!UICONTROL Guardar]**

   ![Interfaz de recopilación de datos](assets/identity-id-namespace.png)

>[!TIP]
>
> El Adobe recomienda enviar identidades que representen a una persona, como `Luma CRM Id`, como el [!UICONTROL principal] identidad.
>
> Si el mapa de identidad contiene el identificador de persona (por ejemplo, `Luma CRM Id`), el identificador de persona se convertirá en [!UICONTROL principal] identidad. De lo contrario, `ECID` se convierte en [!UICONTROL principal] identidad.





<!--
1. Once the data element is configured in **[!UICONTROL Data Collection interface]**, it can be tested on the Luma web property like any other Data Element. Enter the following script in the browser developer console
   
   
   ```
   _satellite.getVar('identityMap.loginID')
   ```  

   ![Data Collection interface](assets/identity-consoleIdentityDataElement.png)
   
   >[!NOTE]
   >
   >ECID identifier will NOT populate in the Data Element, as this is configured already with Platform Web SDK.   
-->

## Asignación de elementos de datos a objetos XDM

Todos los elementos de datos que cree deben asignarse a un objeto XDM. Este objeto debe ajustarse al esquema XDM creado durante la [Configuración de un esquema](configure-schemas.md) lección.

Existen diferentes formas de asignar elementos de datos a campos de objeto XDM. Puede asignar elementos de datos individuales a campos XDM individuales o asignar elementos de datos a objetos XDM completos, siempre que el elemento de datos coincida con el esquema de par clave-valor exacto presente en el objeto XDM. En esta lección, debe capturar datos de contenido asignándolos a campos individuales. Aprenderá a hacer lo siguiente [Asignación de un elemento de datos a un objeto XDM completo](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) en el [Análisis de configuración](setup-analytics.md) lección.

Cree un objeto XDM para capturar datos de contenido:

1. En el panel de navegación izquierdo, seleccione **[!UICONTROL Elementos de datos]**
1. Seleccione **[!UICONTROL Agregar elemento de datos]**
1. **** Asigne un nombre al elemento de datos . **`xdm.content`**
1. Como el **[!UICONTROL Extensión]** select `Adobe Experience Platform Web SDK`
1. Como el **[!UICONTROL Tipo de elemento de datos]** select `XDM object`
1. Seleccione la plataforma **[!UICONTROL Sandbox]** en el que creó el esquema XDM en durante la [Configuración de un esquema XDM](configure-schemas.md) lección, en este ejemplo `DEVELOPMENT Mobile and Web SDK Courses`
1. Como el **[!UICONTROL Esquema]**, seleccione su `Luma Web Event Data` esquema:

   ![Objeto XDM](assets/data-element-xdm.content-fields.png)

   >[!NOTE]
   >
   >La zona protegida corresponde a la zona protegida del Experience Platform en la que ha creado el esquema. Puede haber varias zonas protegidas disponibles en la instancia de Experience Platform, por lo que asegúrese de seleccionar la correcta. Trabaje siempre primero en desarrollo y después en producción.

1. Desplácese hacia abajo hasta que llegue al **`web`** objeto
1. Seleccione para abrirlo

   ![Objeto web](assets/data-element-pageviews-xdm-object.png)


1. Asigne las siguientes variables XDM web a elementos de datos

   * **`web.webPageDetials.name`** hasta `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** hasta `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** hasta `%page.pageInfo.hierarchie1%`

   ![Objeto XDM](assets/data-element-xdm.content.png)

1. A continuación, busque la `identityMap` en el esquema y selecciónelo

1. Mapa a `identityMap.loginID` elemento de datos

1. Seleccione **[!UICONTROL Guardar]**

   ![Interfaz de recopilación de datos](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)




Al final de estos pasos, debe tener los siguientes elementos de datos creados:

| Elementos de datos de la extensión CORE | Elementos de datos del SDK web de Platform |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.content` |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

Con estos elementos de datos en su lugar, está listo para empezar a enviar datos a Platform Edge Network a través del objeto XDM creando una regla en las etiquetas.

[Siguiente: ](create-tag-rule.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
