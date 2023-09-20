---
title: Recopilación y asignación de datos de Analytics
description: Obtenga información sobre cómo recopilar y asignar datos para Adobe Analytics en una aplicación móvil.
solution: Data Collection,Experience Platform,Analytics
hide: true
source-git-commit: cd1efbfaa335c08cbcc22603fe349b4594cc1056
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# Recopilación y asignación de datos de Analytics

Obtenga información sobre cómo asignar datos móviles a Adobe Analytics.

El [evento](events.md) Los datos que ha recopilado y enviado a Platform Edge Network en lecciones anteriores se reenvían a los servicios configurados en su conjunto de datos, incluido Adobe Analytics. Los datos se asignan a las variables correctas del grupo de informes.

![Arquitectura](assets/architecture-aa.png)

## Requisitos previos

* Comprensión del seguimiento de ExperienceEvent.
* Se han enviado correctamente los datos XDM en la aplicación de ejemplo.
* Flujo de datos configurado para Adobe Analytics

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Configure el flujo de datos con el servicio Adobe Analytics.
* Comprenda la asignación automática de variables de Analytics.
* Configure reglas de procesamiento para asignar datos XDM a variables de Analytics.

## Añadir el servicio de flujo de datos de Adobe Analytics

Para enviar los datos XDM de la red perimetral a Adobe Analytics, configure el servicio Adobe Analytics en el conjunto de datos que ha configurado como parte de [Creación de una secuencia de datos](create-datastream.md).

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y su secuencia de datos.

1. A continuación seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir servicio]**.

1. Añadir **[!UICONTROL Adobe Analytics]** desde el [!UICONTROL Servicio] lista,

1. Introduzca el nombre del grupo de informes de Adobe Analytics que desea utilizar en **[!UICONTROL ID del grupo de informes]**.

1. Habilitar el servicio cambiando **[!UICONTROL Habilitado]** en.

1. Seleccione **[!UICONTROL Guardar]**.

   ![Añadir Adobe Analytics como servicio de flujo de datos](assets/datastream-service-aa.png)


## Asignación automática

Muchos de los campos XDM estándar se asignan automáticamente a variables de Analytics. Consulte la lista completa [aquí](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en).

### Ejemplo de #1: s.products

Un buen ejemplo es el [variable products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) que no se pueden rellenar con reglas de procesamiento. Con una implementación de XDM, se pasan todos los datos necesarios en `productListItems` y `s.products` se rellenan automáticamente mediante la asignación de Analytics.

Este objeto:

```swift
"productListItems": [
    [
      "name":  "Yoga Mat",
      "SKU": "5829",
      "priceTotal": "49.99",
      "quantity": 1
    ],
    [
      "name":  "Water Bottle",
      "SKU": "9841",
      "priceTotal": "30.00",
      "quantity": 3
    ]
]
```

resultados en:

```
s.products = ";Yoga Mat;1;49.99,;Water Bottle,3,30.00"
```

>[!NOTE]
>
>Actualmente `productListItems[N].SKU` es ignorado por la asignación automática.


### Ejemplo de #2 - scAdd

Si observa atentamente, todos los eventos tienen dos campos `value` (obligatorio) y `id` (opcional). El `value` se utiliza para incrementar el recuento de eventos. El `id` Este campo se utiliza para la serialización.

Este objeto:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

resultados en:

```
s.events = "scAdd"
```

Este objeto:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1,
    "id": "321435"
  }
}
```

resultados en:

```
s.events = "scAdd:321435"
```

## Validar con Assurance

Uso del [Assurance](assurance.md) Puede confirmar que está enviando un evento de experiencia, que los datos XDM son correctos y que la asignación de Analytics se produce según lo esperado. Por ejemplo:

1. Envíe un evento productListAdds.

1. Vea la visita de ExperienceEvent.

   ![visita de analytics xdm](assets/analytics-assurance-experiencevent.png)

1. Revise la parte XDM del JSON.

   ```json
   "xdm" : {
     "productListItems" : [ {
       "SKU" : "LLWS05.1-XS",
       "name" : "Desiree Fitness Tee",
       "priceTotal" : 24
     } ],
   "timestamp" : "2023-08-04T12:53:37.662Z",
   "eventType" : "commerce.productListAdds",
   "commerce" : {
     "productListAdds" : {
       "id" : "LLWS05.1-XS",
       "value" : 1
     }
   }
   // ...
   ```

1. Revise la **[!UICONTROL analytics.mapping]** evento.

   ![visita de analytics xdm](assets/analytics-assurance-mapping.png)

Tenga en cuenta lo siguiente en la asignación de Analytics:

* **[!UICONTROL eventos]** se rellenan con `scAdd` basado en `commerce.productListAdds`.
* **[!UICONTROL pl]** (variable products) se rellenan con un valor concatenado basado en `productListItems`.
* Hay otra información interesante en este evento, incluidos todos los datos de contexto.


## Asignación con datos de contexto

Los datos XDM reenviados a Analytics se convierten en [datos de contexto](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en) incluidos los campos estándar y personalizados.

La clave de datos de contexto se construye siguiendo esta sintaxis:

```
a.x.[xdm path]
```

Por ejemplo:

```
// Standard Field
a.x.commerce.saveforlaters.value

// Custom Field
a.x._techmarketingdemos.appinformation.appstatedetails.screenname
```

>[!NOTE]
>
>Los campos personalizados se colocan debajo del identificador de organización de Experience Cloud.
>
>`_techmarketingdemos` se sustituye por el valor único de su organización.

Para asignar estos datos de contexto XDM a los datos de Analytics en el grupo de informes, puede:

* Añada el **[!UICONTROL Extensión completa de Adobe Analytics ExperienceEvent]** grupo de campos al esquema.

  ![Grupo de campos FullExtension de Analytics ExperienceEvent](assets/schema-analytics-extension.png)
* Genere reglas en la propiedad Tags para asignar los datos de contexto a los campos del grupo de campos Extensión completa de Adobe Analytics ExperienceEvent. Por ejemplo, asignación `_techmarketingdemo.appinformation.appstatedetails.screenname` hasta `_experience.analytics.customDimensions.eVars.eVar2`.

<!-- Old processing rules section
Here is what a processing rule using this data might look like:

* You **[!UICONTROL Overwrite value of]** (1) **[!UICONTROL App Screen Name (eVar2)]** (2) with the value of **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3) if **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (4) **[!UICONTROL is set]** (5).

* You **[!UICONTROL Set event]** (6) **[!UICONTROL Add to Wishlist (Event 3)]** (7) to **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) if **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL is set]** (10).

![analytics processing rules](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Some of the automatically mapped variables may not be available for use in processing rules.
>
>
>The first time you map to a processing rule, the interface does not show you the context data variables from the XDM object. To fix that select any value, Save, and come back to edit. All XDM variables should now appear.


Additional information about processing rules and context data can be found [here](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>Unlike previous mobile app implementations, there is no distinction between a page / screen views and other events. Instead you can increment the **[!UICONTROL Page View]** metric by setting the **[!UICONTROL Page Name]** dimension in a processing rule. Since you are collecting the custom `screenName` field in the tutorial, it is highly recommended to map screen name to **[!UICONTROL Page Name]** in a processing rule.

-->

>[!SUCCESS]
>
>Ha configurado la aplicación para asignar los objetos XDM de Experience Edge a variables de Adobe Analytics que habiliten el servicio Adobe Analytics en el conjunto de datos y utilicen reglas de procesamiento cuando corresponda.<br/> Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Experience Platform](platform.md)**
