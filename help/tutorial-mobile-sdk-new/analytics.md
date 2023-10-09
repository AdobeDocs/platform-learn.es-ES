---
title: Asignación de datos a datos de Analytics
description: Obtenga información sobre cómo recopilar y asignar datos para Adobe Analytics en una aplicación móvil.
solution: Data Collection,Experience Platform,Analytics
hide: true
exl-id: 631588df-a540-41b5-94e3-c8e1dc5f240b
source-git-commit: d7410a19e142d233a6c6597de92f112b961f5ad6
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 1%

---

# Recopilación y asignación de datos de Analytics

Obtenga información sobre cómo asignar datos móviles a Adobe Analytics.

El [evento](events.md) Los datos que ha recopilado y enviado a Platform Edge Network en lecciones anteriores se reenvían a los servicios configurados en su conjunto de datos, incluido Adobe Analytics. Los datos se asignan a las variables correctas del grupo de informes.

![Arquitectura](assets/architecture-aa.png)

## Requisitos previos

* Comprensión del seguimiento de ExperienceEvent.
* Se han enviado correctamente los datos XDM en la aplicación de ejemplo.
* Un grupo de informes de Adobe Analytics que puede utilizar para esta lección.

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

Uso del [Assurance](assurance.md) Puede confirmar que está enviando un evento de experiencia, que los datos XDM son correctos y que la asignación de Analytics se produce según lo esperado.

1. Revise la [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo a Assurance.

1. Enviar un **[!UICONTROL productListAdds]** evento (añadir un producto a la cesta).

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

### Uso de un grupo de campo

* Añada el **[!UICONTROL Extensión completa de Adobe Analytics ExperienceEvent]** grupo de campos al esquema.

  ![Grupo de campos FullExtension de Analytics ExperienceEvent](assets/schema-analytics-extension.png)

* Cree cargas XDM en la aplicación según el grupo de campos Extensión completa de Adobe Analytics ExperienceEvent, similar a lo que ha hecho en [Seguimiento de datos de eventos](events.md) lección, o
* Genere reglas en la propiedad Etiquetas que utilicen acciones de regla para adjuntar o modificar datos en el grupo de campos Extensión completa de Adobe Analytics ExperienceEvent. Consulte para obtener más información [Adjuntar datos a eventos del SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/) o [Modificación de datos en eventos del SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/).


### Usar reglas de procesamiento

Este es el aspecto que podría tener una regla de procesamiento que utilice estos datos:

* Usted **[!UICONTROL Sobrescribir el valor de]** (1) **[!UICONTROL Nombre de pantalla de la aplicación (eVar 2)]** (2) con el valor de **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3) si **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (4) **[!UICONTROL se ha establecido]** (5).

* Usted **[!UICONTROL Definir evento]** (6) **[!UICONTROL Añadir a la lista de deseos (evento 3)]** (7) a **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) Si **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL se ha establecido]** (10).

![reglas de procesamiento de analytics](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Es posible que algunas de las variables asignadas automáticamente no estén disponibles para su uso en reglas de procesamiento.
>
>
>La primera vez que se asigna a una regla de procesamiento, la interfaz no muestra las variables de datos de contexto del objeto XDM. Para corregir que, seleccione cualquier valor, haga clic en Guardar y vuelva a editar. Ahora deberían aparecer todas las variables XDM.


Se puede encontrar información adicional acerca de reglas de procesamiento y datos de contexto [aquí](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>A diferencia de las implementaciones de aplicaciones móviles anteriores, no hay distinción entre una página o vistas de pantalla y otros eventos. En su lugar, puede incrementar el **[!UICONTROL Vista de página]** estableciendo la variable **[!UICONTROL Nombre de página]** dimensión en una regla de procesamiento. Dado que está recopilando la información personalizada `screenName` en el tutorial, se recomienda encarecidamente asignar el nombre de pantalla a **[!UICONTROL Nombre de página]** en una regla de procesamiento.


>[!SUCCESS]
>
>Ha configurado la aplicación para asignar los objetos XDM de Experience Edge a variables de Adobe Analytics que habiliten el servicio Adobe Analytics en el conjunto de datos y utilicen reglas de procesamiento cuando corresponda.<br/> Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Envío de datos al Experience Platform](platform.md)**
