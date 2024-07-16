---
title: Asignación de datos recopilados con el SDK de Platform Mobile a Adobe Analytics
description: Obtenga información sobre cómo recopilar y asignar datos para Adobe Analytics en una aplicación móvil.
solution: Data Collection,Experience Platform,Analytics
jira: KT-14636
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: 30dd0142f1f5220f30c45d58665b710a06c827a8
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 1%

---

# Recopilación y asignación de datos de Analytics

Obtenga información sobre cómo asignar datos móviles a Adobe Analytics.

Los datos de [event](events.md) que recopiló y envió al Edge Network de Platform en lecciones anteriores se reenvían a los servicios configurados en su secuencia de datos, incluido Adobe Analytics. Los datos se asignan a las variables correctas del grupo de informes.

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

Para enviar los datos XDM del Edge Network a Adobe Analytics, configure el servicio Adobe Analytics en el conjunto de datos que configuró como parte de [Crear un conjunto de datos](create-datastream.md).

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y su secuencia de datos.

1. Luego selecciona ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Agregar servicio]**.

1. Agregar **[!UICONTROL Adobe Analytics]** de la lista [!UICONTROL Service],

1. Escriba el nombre del grupo de informes de Adobe Analytics que quiera usar en **[!UICONTROL Id. del grupo de informes]**.

1. Habilite el servicio activando **[!UICONTROL Enabled]**.

1. Seleccione **[!UICONTROL Guardar]**.

   ![Agregar Adobe Analytics como servicio de secuencia de datos](assets/datastream-service-aa.png)


## Asignación automática

Muchos de los campos XDM estándar se asignan automáticamente a variables de Analytics. Consulte la lista completa [aquí](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en).

### Ejemplo de #1: s.products

Un buen ejemplo es la variable [products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en), que no se puede rellenar con reglas de procesamiento. Con una implementación XDM, pasa todos los datos necesarios en `productListItems` y `s.products` se rellenan automáticamente a través de la asignación de Analytics.

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
s.products = ";5829;1;49.99,9841;3;30.00"
```

>[!NOTE]
>
>Si `productListItems[].SKU` y `productListItems[].name` contienen datos, se utiliza el valor de `productListItems[].SKU`. Consulte [Asignación de variables de Analytics en Adobe Experience Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en) para obtener más información.


### Ejemplo de #2 - scAdd

Si observa atentamente, todos los eventos tienen dos campos: `value` (obligatorio) y `id` (opcional). El campo `value` se usa para incrementar el recuento de eventos. El campo `id` se usa para la serialización.

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

Con [Assurance](assurance.md) puede confirmar que está enviando un evento de experiencia, que los datos XDM son correctos y que la asignación de Analytics se está realizando según lo esperado.

1. Revise la sección [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar su simulador o dispositivo a Assurance.

1. Enviar un evento **[!UICONTROL productListAdds]** (agregue un producto a la cesta).

1. Vea la visita de ExperienceEvent.

   ![visita de xdm de analytics](assets/analytics-assurance-experiencevent.png)

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

1. Revise el evento **[!UICONTROL analytics.mapping]**.

   ![visita de xdm de analytics](assets/analytics-assurance-mapping.png)

Tenga en cuenta lo siguiente en la asignación de Analytics:

* **[!UICONTROL los eventos]** se han rellenado con `scAdd` según `commerce.productListAdds`.
* **[!UICONTROL pl]** (variable products) se rellenan con un valor concatenado basado en `productListItems`.
* Hay otra información interesante en este evento, incluidos todos los datos de contexto.


## Asignación con datos de contexto

Los datos XDM reenviados a Analytics se convierten en [datos de contexto](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en), incluidos los campos estándar y personalizados.

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
>`_techmarketingdemos` se ha reemplazado con el valor único de su organización.



Para asignar estos datos de contexto XDM a los datos de Analytics en el grupo de informes, puede:

### Uso de un grupo de campos

* Agregue el grupo de campos **[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]** al esquema.

  ![Grupo de campos ExperienceEvent FullExtension de Analytics](assets/schema-analytics-extension.png)

* Cree cargas XDM en la aplicación que se ajusten al grupo de campos Extensión completa de Adobe Analytics ExperienceEvent, similar a lo que ha hecho en la lección [Rastrear datos de evento](events.md), o
* Genere reglas en la propiedad Etiquetas que utilicen acciones de regla para adjuntar o modificar datos en el grupo de campos Extensión completa de Adobe Analytics ExperienceEvent. Consulte para obtener más información [Adjuntar datos a eventos de SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/) o [Modificar datos en eventos de SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/).


### eVars de comercialización

Si usa [eVars de comercialización](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/merchandising-evars.html?lang=en) en su configuración de Analytics, por ejemplo, para capturar el color de productos, como `&&products = ...;evar1=red;event10=50,...;evar1=blue;event10=60`, tiene que ampliar la carga útil de XDM que definió en [Rastrear datos de eventos](events.md) para capturar esa información de comercialización.

* En JSON:

  ```json
  {
    "productListItems": [
        {
            "SKU": "LLWS05.1-XS",
            "name": "Desiree Fitness Tee",
            "priceTotal": 24,
            "_experience": {
                "analytics": {
                    "events1to100": {
                        "event10": {
                            "value": 50
                        }
                    },
                    "customDimensions": {
                        "eVars": {
                            "eVar1": "red",
                        }
                    }
                }
            }
        }
    ],
    "eventType": "commerce.productListAdds",
    "commerce": {
        "productListAdds": {
            "value": 1
        }
    }
  }
  ```

* En el código:

  ```swift
  var xdmData: [String: Any] = [
    "productListItems": [
      [
        "name":  productName,
        "SKU": sku,
        "priceTotal": priceString,
        "_experience" : [
          "analytics": [
            "events1to100": [
              "event10": [
                "value:": value
              ]
            ],
            "customDimensions": [
              "eVars": [
                "eVar1": color
              ]
            ]
          ]
        ]
      ]
    ],
    "eventType": "commerce.productViews",
    "commerce": [
      "productViews": [
        "value": 1
      ]
    ]
  ]
  ```


### Usar reglas de procesamiento

Este es el aspecto que podría tener una regla de procesamiento que utilice estos datos:

* Ha **[!UICONTROL sobrescrito el valor de]** (1) **[!UICONTROL Nombre de pantalla de la aplicación (eVar 2)]** (2) con el valor de **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3) si **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (4) **[!UICONTROL se ha establecido]** (5).

* Ha **[!UICONTROL establecido evento]** (6) **[!UICONTROL Agregar a la lista de deseos (Evento 3)]** (7) a **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) si **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL se ha establecido]** (10).

![reglas de procesamiento de analytics](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Es posible que algunas de las variables asignadas automáticamente no estén disponibles para su uso en reglas de procesamiento.
>
>
>La primera vez que se asigna a una regla de procesamiento, la interfaz no muestra las variables de datos de contexto del objeto XDM. Para corregir que, seleccione cualquier valor, haga clic en Guardar y vuelva a editar. Ahora deberían aparecer todas las variables XDM.


Encontrará información adicional sobre reglas de procesamiento y datos de contexto [aquí](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>A diferencia de las implementaciones de aplicaciones móviles anteriores, no hay distinción entre una página o vistas de pantalla y otros eventos. En su lugar, puede aumentar la métrica **[!UICONTROL Vista de página]** estableciendo la dimensión **[!UICONTROL Nombre de página]** en una regla de procesamiento. Dado que está recopilando el campo personalizado `screenName` en el tutorial, es muy recomendable asignar el nombre de pantalla a **[!UICONTROL Nombre de página]** en una regla de procesamiento.


>[!SUCCESS]
>
>Ha configurado la aplicación para asignar los objetos XDM de Experience Edge a variables de Adobe Analytics que habiliten el servicio Adobe Analytics en el conjunto de datos y utilicen reglas de procesamiento cuando corresponda.<br/> Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Enviar datos al Experience Platform](platform.md)**
