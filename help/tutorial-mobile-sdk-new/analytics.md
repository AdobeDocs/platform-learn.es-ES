---
title: Asignación de Analytics
description: Obtenga información sobre cómo recopilar datos para Adobe Analytics en una aplicación móvil.
solution: Data Collection,Experience Platform,Analytics
hide: true
source-git-commit: e119e2bdce524c834cdaf43ed9eb9d26948b0ac6
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 2%

---

# Asignación de Analytics

Obtenga información sobre cómo asignar datos móviles a Adobe Analytics.

El [evento](events.md) Los datos que ha recopilado y enviado a Platform Edge Network en lecciones anteriores se reenvían a los servicios configurados en su conjunto de datos, incluido Adobe Analytics. Los datos se asignan a las variables correctas del grupo de informes.

## Requisitos previos

* Comprensión del seguimiento de ExperienceEvent.
* Se han enviado correctamente los datos XDM en la aplicación de ejemplo.
* Flujo de datos configurado para Adobe Analytics

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Comprenda la asignación automática de variables de Analytics.
* Configure reglas de procesamiento para asignar datos XDM a variables de Analytics.

## Asignación automática

Muchos de los campos XDM estándar se asignan automáticamente a variables de Analytics. Consulte la lista completa [aquí](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en).

### Ejemplo de #1: s.products

Un buen ejemplo es el [variable products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) que no se pueden rellenar con reglas de procesamiento. Con una implementación XDM, se pasan todos los datos necesarios en productListItems y s.products se rellenan automáticamente mediante la asignación de Analytics.

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

Daría como resultado lo siguiente:

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

Daría como resultado lo siguiente:

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

Daría como resultado lo siguiente:

```
s.events = "scAdd:321435"
```

## Validar con Assurance

Uso del [Herramienta de control de calidad Assurance](assurance.md) Puede confirmar que está enviando un ExperienceEvent, que los datos XDM son correctos y que la asignación de Analytics se está produciendo según lo esperado. Por ejemplo:

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
//Standard Field
a.x.commerce.saveforlaters.value

//Custom Field
a.x._techmarketingdemos.appinformationa.appstatedetails.screenname
```

>[!NOTE]
>
>Los campos personalizados se colocan debajo del identificador de organización de Experience Cloud.
>
>`_techmarketingdemos` se sustituye por el valor único de su organización.


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
>La primera vez que se asigna a una regla de procesamiento, la IU no muestra las variables de datos de contexto del objeto XDM. Para corregir que, seleccione cualquier valor, haga clic en Guardar y vuelva a editar. Ahora deberían aparecer todas las variables XDM.


Se puede encontrar información adicional acerca de reglas de procesamiento y datos de contexto [aquí](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>A diferencia de las implementaciones de aplicaciones móviles anteriores, no hay distinción entre vistas de página o pantalla y otros eventos. En su lugar, puede incrementar el **[!UICONTROL Vista de página]** estableciendo la variable **[!UICONTROL Nombre de página]** dimensión en una regla de procesamiento. Dado que está recopilando la información personalizada `screenName` en el tutorial, se recomienda encarecidamente asignar el nombre de pantalla a **[!UICONTROL Nombre de página]** en una regla de procesamiento.

>[!SUCCESS]
>
>Ha configurado la aplicación para asignar los objetos XDM de Experience Edge a variables de Adobe Analytics que habiliten el servicio Adobe Analytics en el conjunto de datos y utilicen reglas de procesamiento cuando corresponda.<br/> Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Experience Platform](platform.md)**
