---
title: Creación de identidades para el SDK web de Platform
description: Obtenga información sobre cómo crear identidades en XDM y utilizar el elemento de datos del mapa de identidad para capturar los ID de usuario. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK, Tags, Identities
jira: KT-15402
exl-id: 7ca32dc8-dd86-48e0-8931-692bcbb2f446
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 3%

---

# Creación de identidades

Obtenga información sobre cómo capturar identidades con el SDK web de Adobe Experience Platform. Capture datos de identidad no autenticados y autenticados en el [sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Aprenda a utilizar los elementos de datos creados anteriormente para recopilar datos autenticados con un tipo de elemento de datos del SDK web de Platform denominado mapa de identidad.

Esta lección se centra en el elemento de datos del mapa de identidad disponible con la extensión de etiquetas del SDK web de Adobe Experience Platform. Los elementos de datos que contienen un ID de usuario autenticado y un estado de autenticación se asignan al XDM.

## Objetivos de aprendizaje

Al final de esta lección, puede hacer lo siguiente:

* Comprenda la relación entre el ID de Experience Cloud (ECID) y el ID de dispositivo de origen (FPID)
* Comprender la diferencia entre ID no autenticados y autenticados
* Creación de un elemento de datos de mapa de identidad

## Requisitos previos

Tiene una idea de lo que es una capa de datos, se ha familiarizado con la capa de datos del [sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} y sabe cómo hacer referencia a elementos de datos en las etiquetas. Debe haber completado las lecciones anteriores en el tutorial:

* [Configuración de un esquema XDM](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)
* [Configuración de una secuencia de datos](configure-datastream.md)
* [Extensión del SDK web instalada en la propiedad de etiqueta](install-web-sdk.md)
* [Creación de elementos de datos](create-data-elements.md)


## Experience Cloud ID

El [ID de Experience Cloud (ECID)](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/ecid) es un área de nombres de identidad compartida que se usa en las aplicaciones de Adobe Experience Platform y Adobe Experience Cloud. ECID proporciona la base para la identidad del cliente y es la identidad predeterminada para las propiedades digitales. ECID es el identificador ideal para rastrear el comportamiento de usuarios no autenticados, ya que siempre está presente.

<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

Obtenga más información sobre cómo se realiza el seguimiento de [ECID mediante el SDK web de Platform](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview).

Los ECID se configuran con una combinación de cookies de origen y Platform Edge Network. De forma predeterminada, el SDK web establece las cookies de identidad de origen del lado del cliente. Para tener en cuenta las restricciones del explorador sobre la duración de las cookies, puede optar por establecer sus propias cookies de identidad de origen del lado del servidor en su lugar. Estas cookies de identidad se denominan ID de dispositivos de origen (FPID).

>[!IMPORTANT]
>
>La extensión del servicio de ID de Experience Cloud [ID Service](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) no es necesaria al implementar el SDK web de Adobe Experience Platform, ya que la funcionalidad del servicio de ID está integrada en el SDK web de Platform.

## ID de dispositivo de origen (FPID)

Los FPID son cookies de origen _configuradas mediante sus propios servidores web_ que el Adobe utiliza para crear el ECID, en lugar de utilizar la cookie de origen establecida por el SDK web. Aunque la compatibilidad con el explorador puede variar, las cookies de origen tienden a ser más duraderas cuando las establece un servidor que aprovecha un registro A de DNS (para IPv4) o un registro AAAA (para IPv6), en lugar de cuando las establece un CNAME o un código JavaScript de DNS.

Una vez establecida una cookie FPID, su valor se puede recuperar y enviar al Adobe a medida que se recopilan los datos del evento. Los FPID recopilados se utilizan como semillas para generar ECID en Platform Edge Network, que siguen siendo los identificadores predeterminados en las aplicaciones de Adobe Experience Cloud.

Aunque los FPID no se utilizan en este tutorial, se le recomienda utilizar FPID en su propia implementación del SDK web. Obtenga más información sobre [ID de dispositivos de origen en el SDK web de Platform](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/first-party-device-ids)

>[!CAUTION]
>
> FPID es una forma alternativa de generar el ECID mediante una cookie configurada por los servidores web. No se utiliza para identificar usuarios autenticados.

## ID autenticado

Como se ha indicado anteriormente, a todos los visitantes de las propiedades digitales se les asigna un ECID por Adobe al utilizar el SDK web de Platform. ECID es la identidad predeterminada para rastrear comportamientos digitales no autenticados.

También puede enviar un ID de usuario autenticado para que Platform pueda crear [gráficos de identidad](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs) y Target pueda establecer su [ID de terceros](https://experienceleague.adobe.com/en/docs/target/using/audiences/visitor-profiles/3rd-party-id). La configuración del identificador autenticado se realiza mediante el tipo de elemento de datos [!UICONTROL Mapa de identidad].

Para crear el elemento de datos [!UICONTROL Identity Map]:

1. Vaya a **[!UICONTROL Elementos de datos]** y seleccione **[!UICONTROL Agregar elemento de datos]**

1. **[!UICONTROL Nombre]** el elemento de datos `identityMap.loginID`

1. Como la **[!UICONTROL extensión]**, seleccione `Adobe Experience Platform Web SDK`

1. Como **[!UICONTROL Tipo de elemento de datos]**, seleccione `Identity map`

1. Se le solicitará un área de pantalla a la derecha dentro de la **[!UICONTROL interfaz de recopilación de datos]** para que configure la identidad:

   ![Interfaz de recopilación de datos](assets/identity-identityMap-setup.png)

1. Como **[!UICONTROL Área de nombres]**, seleccione el área de nombres `lumaCrmId` que creó anteriormente en la lección [Configurar identidades](configure-identities.md). Si no aparece en la lista desplegable, escríbalo en.

1. Una vez seleccionado **[!UICONTROL Espacio de nombres]**, se debe establecer un identificador. Seleccione el elemento de datos `user.profile.attributes.username` creado anteriormente en la lección [Crear elementos de datos](create-data-elements.md#create-data-elements-to-capture-the-data-layer), que captura un ID cuando los usuarios inician sesión en el sitio de Luma.

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. Como **[!UICONTROL estado autenticado]**, seleccione **[!UICONTROL Autenticado]**
1. Seleccionar **[!UICONTROL principal]**

1. Seleccionar **[!UICONTROL Guardar]**

   ![Interfaz de recopilación de datos](assets/identity-id-namespace.png)

>[!TIP]
>
> El Adobe recomienda enviar identidades que representen a una persona, como `Luma CRM Id`, como la identidad [!UICONTROL principal].
>
> Si el mapa de identidad contiene el identificador de persona (por ejemplo, `Luma CRM Id`), entonces el identificador de persona se convierte en la identidad [!UICONTROL principal]. De lo contrario, `ECID` se convierte en la identidad [!UICONTROL principal].




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

Al final de estos pasos, debe tener los siguientes elementos de datos creados:

| Elementos de datos de la extensión principal | Elementos de datos de la extensión SDK para web de Platform |
-----------------------------|-------------------------------
| `cart.orderId` | `data.variable` |
| `cart.productInfo` | `identityMap.loginID` |
| `cart.productInfo.purchase` | `xdm.variable.content` |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `product.category` | |
| `product.productInfo.sku` | |
| `product.productInfo.title` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

Con estos elementos de datos en su lugar, está listo para empezar a enviar datos al Edge Network de Platform creando una regla en las etiquetas.

[Siguiente: ](create-tag-rule.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
