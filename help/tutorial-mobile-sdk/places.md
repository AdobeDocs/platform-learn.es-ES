---
title: Uso de Places con el SDK de Platform Mobile
description: Aprenda a utilizar el servicio de geolocalización de Places en su aplicación móvil.
jira: KT-14635
exl-id: adc2952f-cb01-4e06-9629-49fb95f22ca5
source-git-commit: 3186788dfb834f980f743cef82942b3cf468a857
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 2%

---

# Usar lugares

Aprenda a utilizar el servicio de geolocalización de Places en su aplicación.

El servicio de lugares de recopilación de datos de Adobe Experience Platform es un servicio de geolocalización que permite a las aplicaciones móviles con conocimiento de ubicación comprender el contexto de la ubicación. El servicio utiliza interfaces de SDK enriquecidas y fáciles de usar, acompañadas de una base de datos flexible de puntos de interés (POI).

## Requisitos previos

* Todas las dependencias del paquete se establecen en el proyecto Xcode.
* Extensiones registradas en AppDelegate.
* MobileCore configurado para utilizar su appId de desarrollo.
* SDK importados.
* La aplicación se creó y ejecutó correctamente con los cambios anteriores.

## Objetivos de aprendizaje

En esta lección, debe

* Obtenga información sobre cómo definir puntos de interés en el servicio Places.
* Actualice la propiedad de etiqueta con la extensión Places.
* Actualice el esquema para capturar los eventos de geolocalización.
* Valide la configuración en Assurance.
* Actualice la aplicación para registrar la extensión Places.
* Implemente el seguimiento de geolocalización desde el servicio Places en la aplicación.


## Configuración

Para que el servicio Places funcione en la aplicación y en el SDK móvil, debe realizar alguna configuración.

### Definir lugares

Puede definir algunos puntos de interés en el servicio Places.

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Places]**.
1. Seleccione ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg).
1. En el menú contextual, seleccione **[!UICONTROL Administrar bibliotecas]**.
   ![Administrar bibliotecas](assets/places-manage-libraries.png)
1. En el diálogo **[!UICONTROL Administrar bibliotecas]**, seleccione **[!UICONTROL Nuevo]**.
1. En el cuadro de diálogo **[!UICONTROL Crear biblioteca]**, escriba un **[!UICONTROL Nombre]**, por ejemplo `Luma`.
1. Seleccione **[!UICONTROL Confirmar]**.
   ![Crear biblioteca](assets/places-create-library.png)
1. Para cerrar el cuadro de diálogo **[!UICONTROL Administrar bibliotecas]**, seleccione **[!UICONTROL Cerrar]**.
1. De nuevo en **[!UICONTROL Administración de puntos de interés]**, seleccione **[!UICONTROL Importar puntos de interés]**.
1. Seleccione **[!UICONTROL Iniciar]** en el cuadro de diálogo **[!UICONTROL Importar lugares]**.
1. Seleccione **[!DNL Luma]** de la lista de bibliotecas,
1. Seleccione **[!UICONTROL Siguiente]**.
   ![Seleccionar biblioteca](assets/places-import-select-library.png)
1. Descargue el [archivo ZIP de puntos de interés de Luma](assets/luma_pois.csv.zip) y extráigalo en una ubicación de su equipo.
1. En el cuadro de diálogo **[!UICONTROL Importar lugares]**, arrastre y suelte el archivo `luma_pois.csv` extraído en **[!UICONTROL Elegir archivo CSV - Arrastrar y soltar el archivo]**. Debería ver **[!UICONTROL Validación realizada correctamente]** - **[!UICONTROL Validado correctamente el archivo CSV]**.
1. Seleccione **[!UICONTROL Comenzar importación]**. Debería ver **[!UICONTROL Éxito]** - **[!UICONTROL Se agregaron correctamente 6 POI nuevos]**.
1. Seleccione **[!UICONTROL Listo]**.
1. En **[!UICONTROL Administración de puntos de interés]**, debería ver que se agregan seis nuevas tiendas Luma a la lista. Puede alternar entre la lista ![List](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) y la vista de mapa ![Map](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MapView_18_N.svg).
   ![Lista de lugares](assets/places-list.png).


### Instalar extensión Places

1. Vaya a **[!UICONTROL Etiquetas]**, busque la propiedad de etiquetas móviles y ábrala.
1. Seleccione **[!UICONTROL Extensiones]**.
1. Seleccione **[!UICONTROL Catálogo]**.
1. Busque la extensión **[!UICONTROL Places]**.
1. Instale la extensión de.

   ![Agregar extensión de Decisioning](assets/tag-places-extension.png)

1. En el diálogo **[!UICONTROL Instalar extensión]**:
   1. Seleccione **[!DNL Luma]** de la lista **[!UICONTROL Seleccionar una biblioteca]**.
   1. Asegúrese de haber seleccionado su biblioteca de trabajo, por ejemplo **[!UICONTROL Versión inicial]**.
   1. Seleccione **[!UICONTROL Guardar en biblioteca y compilar]** de **[!UICONTROL Guardar en biblioteca]**.
      ![Instalar extensión Places](assets/places-install-extension.png).

1. Se volverá a crear su biblioteca.


### Verificar el esquema

Compruebe si el esquema, tal como se define en [Crear esquema](create-schema.md), incorpora los grupos de campos y las clases necesarios para recopilar los datos de puntos de interés y la geolocalización.

1. Vaya a la interfaz de recopilación de datos y seleccione **[!UICONTROL Esquemas]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Examinar]** en la barra superior.
1. Seleccione el esquema para abrirlo.
1. En el editor de esquemas, seleccione **[!UICONTROL Evento de experiencia del consumidor]**.
1. Verá un objeto **[!UICONTROL placeContext]** con objeto y campos para capturar la interacción de puntos de interés y los datos de geolocalización.
   ![Lugares de esquema](assets/schema-places-context.png).


### Actualizar la propiedad de etiquetas

La extensión Places para etiquetas proporciona funcionalidad para supervisar eventos de geolocalización y permite almacenar en déclencheur acciones basadas en estos eventos. Puede utilizar esta funcionalidad para minimizar la codificación de la API que debe implementar en la aplicación.

**Elementos de datos**

Primero se crean varios elementos de datos.

1. Vaya a la propiedad de etiquetas en la interfaz de usuario de la recopilación de datos.
1. Seleccione **[!UICONTROL Elementos de datos]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Agregar elemento de datos]**.
1. En la pantalla **[!UICONTROL Crear elemento de datos]**, escriba un nombre, por ejemplo `Name - Entered`.
1. Seleccione **[!UICONTROL Places]** de la lista **[!UICONTROL Extension]**.
1. Seleccione **[!UICONTROL Name]** de la lista **[!UICONTROL Tipo de elemento de datos]**.
1. Seleccione **[!UICONTROL el punto de interés actual]** debajo de **[!UICONTROL TARGET]**.
1. Seleccione **[!UICONTROL Guardar en biblioteca]**.
   ![Elemento de datos](assets/tags-create-data-element.png)

1. Repita los pasos 4-8 utilizando la información de la tabla siguiente para crear elementos de datos adicionales.

   | Nombre | Extensión | Tipo de elemento de datos | DESTINO |
   |---|---|---|---|
   | `Name - Exited` | Places | Nombre | Último PDI saliente |
   | `Category - Current` | Places | Categoría | Punto de interés actual |
   | `Category - Exited` | Places | Categoría | Último PDI saliente |
   | `City - Current` | Places | Ciudad | Punto de interés actual |
   | `City - Exited` | Places | Ciudad | Último PDI saliente |

   Debe tener la siguiente lista de elementos de datos.

   ![Lista de elementos de datos](assets/tags-data-elements-list.png)

**Reglas**

A continuación, va a definir reglas para trabajar con estos elementos de datos.

1. En su propiedad de etiquetas, seleccione **[!UICONTROL Reglas]** en el carril izquierdo.
1. Seleccione **[!UICONTROL Agregar regla]**.
1. En la pantalla **[!UICONTROL Crear regla]**, escriba un nombre para la regla, por ejemplo `POI - Entry`.
1. Seleccione ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) debajo de **[!UICONTROL EVENTOS]**.
   1. Seleccione **[!UICONTROL Places]** de la lista **[!UICONTROL Extension]** y seleccione **[!UICONTROL Enter POI]** de la lista **[!UICONTROL Event Type]**.
   1. Seleccione **[!UICONTROL Conservar cambios]**.
      ![Evento de etiqueta](assets/tags-event-mobile-core.png).
1. Seleccione ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) debajo de **[!UICONTROL ACCIONES]**.
   1. Seleccione **[!UICONTROL Mobile Core]** de la lista **[!UICONTROL Extension]**, seleccione **[!UICONTROL Adjuntar datos]** de **[!UICONTROL Tipo de acción]** en la lista. Esta acción adjunta datos de carga útil.
   1. En la **[!UICONTROL carga útil JSON]**, pegue la siguiente carga útil:

      ```json
      {
          "xdm": {
              "eventType": "location.entry",
              "placeContext": {
                  "geo": {
                      "city": "{%%City - Current%%}"
                  },
                  "POIinteraction": {
                      "poiDetail": {
                          "name": "{%%Name - Current%%}",
                          "category": "{%%Category - Current%%}"
                      },
                      "poiEntries": {
                          "value": 1
                      }
                  }
              }
          }
      }
      ```

      También puede insertar `{%% ... %%}` valores de marcador de posición de elementos de datos en el JSON al seleccionar ![Datos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg). Un cuadro de diálogo emergente le permite elegir cualquier elemento de datos que haya creado.

   1. Seleccione **[!UICONTROL Conservar cambios]**.
      ![Acción de etiquetas](assets/tags-action-mobile-core.png)

1. Seleccione ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a la acción **[!UICONTROL Núcleo móvil: adjuntar datos]**.
   1. Seleccione **[!UICONTROL Edge Network de Adobe Experience Platform]** de la lista **[!UICONTROL Extension]** y seleccione **[!UICONTROL Reenviar evento al Edge Network]**. Esta acción garantiza que el evento y los datos de carga útil adicionales se reenvíen al Edge Network de Platform.
   1. Seleccione **[!UICONTROL Conservar cambios]**.

1. Para guardar la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

   ![Regla](assets/tags-rule-poi-entry.png)

Vamos a crear otra regla

1. En la pantalla **[!UICONTROL Crear regla]**, escriba un nombre para la regla, por ejemplo `POI - Exit`.
1. Seleccione ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) debajo de **[!UICONTROL EVENTOS]**.
   1. Seleccione **[!UICONTROL Places]** de la lista **[!UICONTROL Extension]** y seleccione **[!UICONTROL Exit POI]** de la lista **[!UICONTROL Event Type]**.
   1. Seleccione **[!UICONTROL Conservar cambios]**.
1. Seleccione ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) debajo de **[!UICONTROL ACCIONES]**.
   1. Seleccione **[!UICONTROL Mobile Core]** de la lista **[!UICONTROL Extension]**, seleccione **[!UICONTROL Adjuntar datos]** de la lista **[!UICONTROL Tipo de acción]**.
   1. En la **[!UICONTROL carga útil JSON]**, pegue la siguiente carga útil:

      ```json
      {
          "xdm": {
              "eventType": "location.exit",
              "placeContext": {
                  "geo": {
                      "city": "{%%City - Exited%%}"
                  },
                  "POIinteraction": {
                      "poiExits": {
                          "value": 1
                      },
                      "poiDetail": {
                          "name": "{%%Name - Exited%%}",
                          "category": "{%%Category - Exited%%}"
                      }
                  }
              }
          }
      }
      ```

   1. Seleccione **[!UICONTROL Conservar cambios]**.

1. Seleccione ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a la acción **[!UICONTROL Núcleo móvil: adjuntar datos]**.
   1. Seleccione **[!UICONTROL Edge Network de Adobe Experience Platform]** de la lista **[!UICONTROL Extension]** y seleccione **[!UICONTROL Reenviar evento al Edge Network]**.
   1. Seleccione **[!UICONTROL Conservar cambios]**.

1. Para guardar la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

   ![Regla](assets/tags-rule-poi-exit.png)


Para asegurarse de que se publican todos los cambios en la etiqueta

1. Seleccione **[!UICONTROL Versión inicial]** como la biblioteca que generar.
1. Seleccione **[!UICONTROL Generar]**.
   ![Biblioteca de compilación](assets/tags-build-library.png)




## Validar la configuración en Assurance

Para validar la configuración en Assurance:

1. Vaya a la interfaz de usuario de Assurance.
1. Si no está disponible en el carril izquierdo, seleccione **[!UICONTROL Configurar]** en el carril izquierdo y seleccione ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a **[!UICONTROL Eventos]** y **[!UICONTROL Asignar y simular]** debajo de **[!UICONTROL SERVICIO DE LUGARES]**.
1. Seleccione **[!UICONTROL Guardar]**.
1. Seleccione **[!UICONTROL Asignar y simular]** en el carril izquierdo.
1. Mueva el mapa a una ubicación de uno de sus puntos de interés.
1. Seleccione ![engranaje](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Gears_18_N.svg) para simular puntos de interés de carga. Su punto de interés se identifica con un círculo y un alfiler.
1. Seleccione su punto de interés.
1. En la ventana emergente, seleccione ![Engranaje](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Gears_18_N.svg) **[!UICONTROL Simular evento de entrada]**.
   ![Simular evento de entrada](assets/places-simulate.png)
1. Seleccione **[!UICONTROL Eventos]** en el carril izquierdo y debería ver los eventos que ha simulado.
   ![Validación de AJO Decisioning](assets/places-events.png)


## Implementar Places en la aplicación

Como se ha explicado en lecciones anteriores, la instalación de una extensión de etiqueta móvil solo proporciona la configuración. A continuación, debe instalar y registrar el SDK de Places. Si estos pasos no están claros, revise la sección [Instalar SDK](install-sdks.md).

>[!NOTE]
>
>Si ha completado la sección [Instalar SDK](install-sdks.md), el SDK de Places ya está instalado y puede omitir este paso.
>

1. En Xcode, asegúrese de que [AEP Places](https://github.com/adobe/aepsdk-places-ios) se agregue a la lista de paquetes en Dependencias del paquete. Consulte [Administrador De Paquetes Swift](install-sdks.md#swift-package-manager).
1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL AppDelegate]** en el navegador del proyecto Xcode.
1. Asegúrese de que `AEPPlaces` forme parte de su lista de importaciones.

   ```swift
   import AEPPlaces
   ```

1. Asegúrese de que `Places.self` forme parte de la matriz de extensiones que está registrando.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode y busque la función `func processRegionEvent(regionEvent: PlacesRegionEvent, forRegion region: CLRegion) async`. Añada el siguiente código:

   ```swift
   // Process geolocation event
   Places.processRegionEvent(regionEvent, forRegion: region)
   ```

   Esta API [`Places.processRegionEvent`](https://developer.adobe.com/client-sdks/documentation/places/api-reference/#processregionevent) comunica la información de geolocalización al servicio Places.

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Location]** > **[!DNL GeofenceSheet]** en el navegador de proyectos de Xcode.

   1. Para el botón Entry, introduzca el siguiente código

   ```swift
   // Simulate geofence entry event
   Task {
       await MobileSDK.shared.processRegionEvent(regionEvent: .entry, forRegion: region)
   }
   ```

   1. Para el botón Exit (Salir), introduzca el siguiente código

   ```swift
   // Simulate geofence exit event
   Task {
       await MobileSDK.shared.processRegionEvent(regionEvent: .exit, forRegion: region)
   }
   ```

## Validar con la aplicación

1. Abra la aplicación en un dispositivo o en el simulador.

1. Vaya a la ficha **[!UICONTROL Ubicación]**.

1. Mueva (arrastre) el mapa para asegurarse de que el círculo central azul esté encima de uno de sus puntos de interés, por ejemplo Londres.

1. Tocar <img src="assets/geobutton.png" width="20" /> hasta que vea que la categoría y el nombre aparecen en la etiqueta en la ubicación roja con el pin.

1. Pulse la etiqueta del punto de interés (POI), que abre la hoja **[!UICONTROL Punto de interés cercano]**.

   <img src="assets/appgeolocation.png" width="300" />

1. Pulse los botones **[!UICONTROL Entrada]** o **[!UICONTROL Salida]** para simular los eventos de entrada y salida de geovalla desde la aplicación.

   <img src="assets/appentryexit.png" width="300" />

1. Debería ver los eventos en la interfaz de usuario de Assurance.



## Pasos siguientes

Ahora debe tener todas las herramientas para empezar a añadir más funcionalidades a la funcionalidad de geolocalización en la aplicación. A medida que reenvíe los eventos al Edge Network, una vez que haya configurado la aplicación para [Experience Platform](platform.md), debería ver los eventos de experiencia que aparecen para el perfil que se usa en la aplicación.

En la sección Journey Optimizer de este tutorial, verá que los eventos de experiencia se pueden usar para almacenar en déclencheur los recorridos (consulte [notificaciones push](journey-optimizer-inapp.md) y [mensajería en la aplicación](journey-optimizer-push.md) con Journey Optimizer). Por ejemplo, el ejemplo habitual de enviar a un usuario de la aplicación una notificación push con alguna promoción de producto cuando ese usuario entra en la geovalla de una tienda física.

Ha visto una implementación de la funcionalidad de su aplicación, impulsada principalmente por el servicio Places y los elementos de datos y reglas que definió en la propiedad de etiquetas. Como tal, minimice el código en la aplicación. Como alternativa, puede implementar la misma funcionalidad directamente en la aplicación mediante la API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) (consulte [Eventos](events.md) para obtener más información) con una carga XDM que contenga un objeto `placeContext` rellenado.

>[!SUCCESS]
>
>Ahora ha habilitado la aplicación para servicios de geolocalización mediante la extensión Places en el SDK de Experience Platform Mobile.
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Asignar datos a Adobe Analytics](analytics.md)**
