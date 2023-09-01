---
title: Places
description: Aprenda a utilizar el servicio de localización geográfica Places en su aplicación móvil.
hide: true
source-git-commit: c31dd74cf8ff9c0856b29e82d9c8be2ad027df4a
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 3%

---

# Places

Aprenda a utilizar el servicio de localización geográfica en la aplicación.

El servicio de lugares de recopilación de datos de Adobe Experience Platform es un servicio de ubicación geográfica que permite a las aplicaciones móviles con conocimiento de ubicación comprender el contexto de la ubicación. El servicio utiliza interfaces de SDK enriquecidas y fáciles de usar, acompañadas de una base de datos flexible de puntos de interés (POI).

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
* Actualice la aplicación para incluir la extensión Places.
* Implemente el seguimiento de ubicación geográfica desde el servicio Places en la aplicación.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK adecuados instalados y configurados.


## Objetivos de aprendizaje

En esta lección, debe

* Actualice la configuración de Edge para Administración de decisiones.
* Actualice la propiedad de etiquetas con la extensión Journey Optimizer - Decisioning.
* Actualice el esquema para capturar eventos de propuesta.
* Valide la configuración en Assurance.
* Cree una decisión de oferta basada en ofertas de Journey Optimizer - Gestión de decisiones.
* Actualice la aplicación para incluir la extensión de Optimizer.
* Implemente ofertas de Administración de decisiones en la aplicación.


## Configuración

Para que el servicio Places funcione en la aplicación y en el SDK móvil, debe realizar alguna configuración.

### Definir lugares

Puede definir algunos puntos de interés en el servicio Places.

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Places]**.
1. Seleccionar ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg).
1. En el menú contextual, seleccione **[!UICONTROL Administrar bibliotecas]**.
   ![Administrar bibliotecas](assets/places-manage-libraries.png)
1. En el **[!UICONTROL Administrar bibliotecas]** diálogo, seleccione **[!UICONTROL Nuevo]**.
1. En el **[!UICONTROL Crear biblioteca]** diálogo escriba un **[!UICONTROL Nombre]**, por ejemplo `Luma`.
1. Seleccionar **[!UICONTROL Confirmar]**.
   ![Crear biblioteca](assets/places-create-library.png)
1. Para cerrar el **[!UICONTROL Administrar bibliotecas]** diálogo, seleccione **[!UICONTROL Cerrar]**.
1. Volver a entrar **[!UICONTROL Gestión de PDI]**, seleccione **[!UICONTROL Importar POI]**.
1. Seleccionar **[!UICONTROL Inicio]** en t**[!UICONTROL Los lugares de importación]Cuadro de diálogo **.
1. Seleccionar **[!UICONTROL Luma]** de la lista de bibliotecas,
1. Seleccione **[!UICONTROL Siguiente]**.
   ![Seleccionar biblioteca](assets/places-import-select-library.png)
1. Descargue la [Archivo ZIP de puntos de interés de Luma](assets/luma_pois.csv.zip) y extráigalo en una ubicación de su equipo.
1. En el **[!UICONTROL Lugares de importación]** diálogo, arrastre y suelte el extraído `luma_pois.csv` archivo en **[!UICONTROL Elegir archivo CSV: arrastrar y soltar el archivo]**. Debería ver **[!UICONTROL Validación correcta]** - **[!UICONTROL El archivo CSV se ha validado correctamente]**.
1. Seleccionar **[!UICONTROL Comenzar importación]**. Debería ver **[!UICONTROL Correcto]** - **[!UICONTROL Se han añadido correctamente 6 POI nuevos]**.
1. Seleccionar **[!UICONTROL Listo]**.
1. Entrada **[!UICONTROL Gestión de PDI]**, debería ver que se añaden seis nuevas tiendas Luma a la lista. Puede alternar entre ![Lista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) lista y ![Mapa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MapView_18_N.svg) vista de mapa.
   ![Lista de lugares](assets/places-list.png).


### Instalar extensión Places

1. Vaya a **[!UICONTROL Etiquetas]** y busque la propiedad de etiquetas móviles y ábrala.
1. Seleccionar **[!UICONTROL Extensiones]**.
1. Seleccionar **[!UICONTROL Catálogo]**.
1. Busque la variable **[!UICONTROL Adobe Journey Optimizer - Toma de decisiones]** extensión.
1. Instale la extensión de. La extensión no requiere ninguna configuración adicional.

   ![Añadir extensión de Decisioning](assets/tag-places-extension.png)

1. En el **[!UICONTROL Instalar extensión]** diálogo:
   1. Seleccionar **[!UICONTROL Luma]** desde el **[!UICONTROL Seleccione una biblioteca]** lista.
   1. Asegúrese de haber seleccionado su biblioteca de trabajo, por ejemplo **[!UICONTROL Compilación inicial]**.
   1. Seleccionar **[!UICONTROL Guardar en biblioteca y crear]** de **[!UICONTROL Guardar en biblioteca]**.
      ![Instalar extensión Places](assets/places-install-extension.png).

1. Se está reconstruyendo su biblioteca.


### Verificar el esquema

Compruebe si el esquema, tal como se define en [Crear esquema](create-schema.md), incorpora los grupos de campos y las clases necesarios para recopilar los datos de puntos de interés y geolocalización.

1. Vaya a la IU de recopilación de datos y seleccione **[!UICONTROL Esquemas]** desde el carril izquierdo.
1. Seleccionar **[!UICONTROL Examinar]** desde la barra superior.
1. Seleccione el esquema para abrirlo.
1. En el editor de esquemas, seleccione **[!UICONTROL Evento de experiencia del consumidor]**.
1. Verá un **[!UICONTROL placeContext]** objeto con objeto y campos para capturar datos de interacción y geolocalización de puntos de interés.
   ![Lugares del esquema](assets/schema-places-context.png).


### Actualice la etiqueta

La extensión Places proporciona funcionalidad para supervisar eventos de geolocalización y permite almacenar en déclencheur acciones basadas en estos eventos. Puede utilizar esta funcionalidad para minimizar la codificación de la API que debe implementar en la aplicación.

**Elementos de datos**

Primero se crean varios elementos de datos.

1. Vaya a la propiedad de etiquetas en la interfaz de usuario de la recopilación de datos.
1. Seleccionar **[!UICONTROL Elementos de datos]** desde el carril izquierdo.
1. Seleccione **[!UICONTROL Agregar elemento de datos]**.
1. En el **[!UICONTROL Crear elemento de datos]** , introduzca un nombre, por ejemplo `Name - Entered`.
1. Seleccionar **[!UICONTROL Places]** desde el **[!UICONTROL Extensión]** lista.
1. Seleccionar **[!UICONTROL Nombre]** desde el **[!UICONTROL Tipo de elemento de datos]** lista.
1. Seleccionar **[!UICONTROL Punto de interés actual]**debajo **[!UICONTROL DESTINO]**.
1. Seleccionar **[!UICONTROL Guardar en biblioteca]**.
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

Ahora va a definir reglas para trabajar con estos elementos de datos.

1. Seleccionar **[!UICONTROL Reglas]** desde el carril izquierdo.
1. Seleccionar **[!UICONTROL Agregar regla]**.
1. En el **[!UICONTROL Crear regla]** , introduzca un nombre para la regla, por ejemplo `POI - Entry`.
1. Seleccionar ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) debajo **[!UICONTROL EVENTOS]**.
   1. Seleccionar **[!UICONTROL Places]** desde el **[!UICONTROL Extensión]** lista y seleccione **[!UICONTROL Introducir POI]** desde el **[!UICONTROL Tipo de evento]** lista.
   1. Seleccione **[!UICONTROL Conservar cambios]**.
      ![Evento de etiqueta](assets/tags-event-mobile-core.png).
1. Seleccionar ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) debajo **[!UICONTROL ACCIONES]**.
   1. Seleccionar **[!UICONTROL Mobile Core]** de **[!UICONTROL Extensión]** , seleccione **[!UICONTROL Adjuntar datos]** de **[!UICONTROL Tipo de acción]** lista. Esta acción adjunta datos de carga útil.
   1. En el **[!UICONTROL Carga útil JSON]**, pegue la siguiente carga útil:

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

      El `{%% ... %%}` Los valores de también se pueden insertar fácilmente seleccionando la variable ![Datos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) junto al cuadro de diálogo y seleccionando un elemento de datos en el cuadro de diálogo.

   1. Seleccione **[!UICONTROL Conservar cambios]**.
      ![Acción Etiquetas](assets/tags-action-mobile-core.png)

1. Seleccionar ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto al **[!UICONTROL Mobile Core - Adjuntar datos]** acción.
   1. Seleccionar **[!UICONTROL Adobe Experience Platform Edge Network]** desde el **[!UICONTROL Extensión]** lista y seleccione **[!UICONTROL Reenviar evento a Edge Network]**. Esta acción garantiza que el evento y los datos de carga útil adicionales se reenvíen a la red perimetral.
   1. Seleccione **[!UICONTROL Conservar cambios]**.

1. Para guardar la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

   ![Regla](assets/tags-rule-poi-entry.png)

Vamos a crear otra regla

1. En el **[!UICONTROL Crear regla]** , introduzca un nombre para la regla, por ejemplo `POI - Exit`.
1. Seleccionar ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) debajo **[!UICONTROL EVENTOS]**.
   1. Seleccionar **[!UICONTROL Places]** desde el **[!UICONTROL Extensión]** lista y seleccione **[!UICONTROL Introducir POI]** desde el **[!UICONTROL Tipo de evento]** lista.
   1. Seleccione **[!UICONTROL Conservar cambios]**.
1. Seleccionar ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) debajo **[!UICONTROL ACCIONES]**.
   1. Seleccionar **[!UICONTROL Mobile Core]** de **[!UICONTROL Extensión]** , seleccione **[!UICONTROL Adjuntar datos]** de **[!UICONTROL Tipo de acción]** lista.
   1. En el **[!UICONTROL Carga útil JSON]**, pegue la siguiente carga útil:

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

1. Seleccionar ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto al **[!UICONTROL Mobile Core - Adjuntar datos]** acción.
   1. Seleccionar **[!UICONTROL Adobe Experience Platform Edge Network]** desde el **[!UICONTROL Extensión]** lista y seleccione **[!UICONTROL Reenviar evento a Edge Network]**.
   1. Seleccione **[!UICONTROL Conservar cambios]**.


Para asegurarse de que se publican todos los cambios en la etiqueta

1. Seleccionar **[!UICONTROL Compilación inicial]** como la biblioteca que se va a crear.
1. Seleccionar **[!UICONTROL Generar]**.
   ![Crear biblioteca](assets/tags-build-library.png)




## Validar la configuración en Assurance

Para validar la configuración en Assurance:

1. Vaya a la interfaz de usuario de Assurance.
1. Si no está disponible en el carril izquierdo. select **[!UICONTROL Configurar]** en el carril izquierdo y seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a **[!UICONTROL Eventos]** y **[!UICONTROL Mapa y simulación]** debajo **[!UICONTROL SERVICIO DE PLACES]**.
1. Seleccione **[!UICONTROL Guardar]**.
1. Seleccionar **[!UICONTROL Mapa y simulación]** en el carril izquierdo.
1. Seleccione uno de los puntos de interés definidos en el servicio Places y, en la ventana emergente, seleccione ![Engranaje](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Gears_18_N.svg) **[!UICONTROL Simular evento de entrada]**.
   ![Simular evento de entrada](assets/places-simulate.png)
1. Seleccionar **[!UICONTROL Eventos]** desde el carril izquierdo, y debería ver los eventos que ha simulado.
   ![Validación de AJO Decisioning](assets/places-events.png)


## Implementar lugares en la aplicación

Como se ha explicado en lecciones anteriores, la instalación de una extensión de etiqueta móvil solo proporciona la configuración. A continuación, debe instalar y registrar el SDK de Places. Si estos pasos no están claros, revise la [Instalación de SDK](install-sdks.md) sección.

>[!NOTE]
>
>Si ha completado la [Instalación de SDK](install-sdks.md) , el SDK de Places ya está instalado y puede omitir este paso.
>

1. En Xcode, asegúrese de que [AEP Places](https://github.com/adobe/aepsdk-places-ios) se añade a la lista de paquetes en Dependencias del paquete. Consulte [Administrador De Paquetes Swift](install-sdks.md#swift-package-manager).
1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** en el navegador del proyecto Xcode.
1. Asegurar `AEPPlaces` forma parte de su lista de importaciones.

   `import AEPPlaces`

1. Asegurar `Places.self` forma parte de la matriz de extensiones que está registrando.

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

1. Vaya a Luma > Luma > Utils > MobileSDK en el navegador del proyecto Xcode y busque la función asincrónica processRegionEvent(regionEvent: PlacesRegionEvent, forRegion region: CLRegion). Esta función es un envoltorio alrededor de [`Places.processRegionEvent`](https://developer.adobe.com/client-sdks/documentation/places/api-reference/#processregionevent) API.
1. Vaya a Luma > Luma > Vistas > Ubicación > Geoperímetro en el navegador de proyectos de Xcode.

   1. Para el botón Entry, introduzca el siguiente código

   ```swift
   Task {
       await MobileSDK.shared.processRegionEvent(regionEvent: .entry, forRegion: region)
   }
   ```

   1. Para el botón Exit (Salir), introduzca el siguiente código

   ```swift
   Task {
       await MobileSDK.shared.processRegionEvent(regionEvent: .exit, forRegion: region)
   }
   ```

En este tutorial se va más allá del tema para explicar los detalles sobre la implementación del administrador de ubicaciones en iOS.


## Validar con la aplicación

1. Abra la aplicación en un dispositivo o en el simulador.

1. Vaya a la **[!UICONTROL Ubicación]** pestaña.

1. Mueva el mapa para asegurarse de que el círculo azul en el medio esté encima de uno de sus puntos de interés, por ejemplo, Londres.

1. Pulsar el azul <img src="assets/geobutton.png" width="20" /> repetidamente hasta que vea la categoría y el nombre en la parte inferior derecha.

1. Pulse la etiqueta del punto de interés, que abre la hoja de puntos de interés cercanos.

   <img src="assets/appgeolocation.png" width="300" />

1. Pulse los botones Entrada o Salida para simular los eventos de geolocalización desde la aplicación.

   <img src="assets/appentryexit.png" width="300" />

1. Debería ver los eventos en la interfaz de usuario de Assurance.



## Pasos siguientes

Ahora debe tener todas las herramientas para empezar a añadir más funcionalidades a la funcionalidad de geolocalización en la aplicación. A medida que haya reenviado los eventos a la red perimetral y a través del flujo de datos al Experience Platform, debería ver que aparecen los eventos de experiencia para el perfil utilizado en la aplicación. Estos eventos de experiencia se pueden utilizar para almacenar en déclencheur los recorridos en Journey Optimizer (consulte [notificación push](journey-optimizer-inapp.md) y [mensajería en la aplicación](journey-optimizer-push.md) con Journey Optimizer). Por ejemplo, el ejemplo habitual de enviar al usuario de la aplicación una notificación push cuando alguien entra en la geovalla de una tienda física.

Ha visto una implementación de la funcionalidad de su aplicación, impulsada principalmente por el servicio Places y los elementos de datos y reglas definidos en la propiedad Tag. También puede implementar la misma funcionalidad directamente en la aplicación utilizando [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API (consulte [Eventos](events.md) para obtener más información) con una carga útil XDM que contiene un objeto placeContext rellenado.

>[!SUCCESS]
>
>Ahora ha habilitado la aplicación para servicios de geolocalización mediante la extensión Places en el SDK de Experience Platform Mobile.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Asignación de datos a Adobe Analytics](analytics.md)**
