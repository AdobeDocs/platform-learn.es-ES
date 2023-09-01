---
title: Ofertas de Adobe Journey Optimizer
description: Obtenga información sobre cómo crear y mostrar ofertas con el SDK de Platform Mobile y la administración de decisiones de Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Offers
hide: true
source-git-commit: c31dd74cf8ff9c0856b29e82d9c8be2ad027df4a
workflow-type: tm+mt
source-wordcount: '2342'
ht-degree: 3%

---

# Ofertas de Journey Optimizer

Obtenga información sobre cómo mostrar ofertas de Administración de decisiones de Journey Optimizer en sus aplicaciones móviles con el SDK móvil de Platform.

Administración de decisiones de Journey Optimizer le ayuda a ofrecer la mejor oferta y experiencia a sus clientes en todos los puntos de contacto y en el momento adecuado. Una vez diseñada, la audiencia debe segmentarse con ofertas personalizadas.

La administración de decisiones facilita la personalización con una biblioteca central de ofertas de marketing y un motor de decisión que aplica reglas y restricciones a perfiles enriquecidos en tiempo real creados por Adobe Experience Platform. Como resultado, le permite enviar a sus clientes la oferta correcta en el momento adecuado. Consulte [Acerca de Administración de decisiones](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/starting-offer-decisioning.html?lang=en) para obtener más información.


>[!NOTE]
>
>Esta lección es opcional y solo se aplica a los usuarios de Optimizadores de Recorrido que buscan utilizar la funcionalidad Gestión de decisiones para mostrar ofertas en una aplicación móvil.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.
* Acceso a Journey Optimizer: Administración de decisiones con los permisos adecuados para administrar ofertas y decisiones según se describe [aquí](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).


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

>[!TIP]
>
>Si ya ha configurado su entorno como parte de la [Configuración de pruebas A/B con Target](target.md) tutorial, puede omitir [Instalación de Adobe Journey Optimizer: extensión de etiquetas de Decisioning](#install-adobe-journey-optimizer---decisioning-tags-extension) y [Actualizar el esquema](#update-your-schema).

### Actualizar configuración de Edge

Para garantizar que los datos enviados desde su aplicación móvil a la red perimetral se reenvíen a Journey Optimizer - Gestión de decisiones, actualice la configuración de Experience Edge

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y seleccione la secuencia de datos, por ejemplo **[!UICONTROL Aplicación móvil de Luma]**.
1. Seleccionar ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) para **[!UICONTROL Experience Platform]** y seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar]** en el menú contextual.
1. En el **[!UICONTROL Datastreams]** > ![Carpeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) >  **[!UICONTROL Adobe Experience Platform]** pantalla, asegúrese de **[!UICONTROL Offer decisioning]**, **[!UICONTROL Segmentación de Edge]**, **[!UICONTROL Destinos de personalización]**, y **[!UICONTROL Adobe Journey Optimizer]** están seleccionados. Consulte [Configuración de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) para obtener más información.
1. Para guardar la configuración de la secuencia de datos, seleccione **[!UICONTROL Guardar]** .

   ![Configuración de flujo de datos AEP](assets/datastream-aep-configuration.png)


### Instalación de Journey Optimizer: extensión de etiquetas de Decisioning

1. Vaya a **[!UICONTROL Etiquetas]** y busque la propiedad de etiquetas móviles y ábrala.
1. Seleccionar **[!UICONTROL Extensiones]**.
1. Seleccionar **[!UICONTROL Catálogo]**.
1. Busque la variable **[!UICONTROL Adobe Journey Optimizer - Toma de decisiones]** extensión.
1. Instale la extensión de. La extensión no requiere ninguna configuración adicional.

   ![Añadir extensión de Decisioning](assets/tag-add-decisioning-extension.png)


### Actualizar el esquema

1. Vaya a la IU de recopilación de datos y seleccione **[!UICONTROL Esquemas]** desde el carril izquierdo.
1. Seleccionar **[!UICONTROL Examinar]** desde la barra superior.
1. Seleccione el esquema para abrirlo.
1. En el editor de esquemas, seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir]** junto a Grupos de campos.
1. En el **[!UICONTROL Adición de campos y grupos]** diálogo, ![Buscar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) buscar `proposition`, seleccione **[!UICONTROL Evento de experiencia: interacciones de propuesta]** y seleccione **[!UICONTROL Adición de grupos de campos]**.
   ![Proposición](assets/schema-fieldgroup-proposition.png)
1. Seleccionar **[!UICONTROL Guardar]** para guardar los cambios en el esquema.


## Validar la configuración en Assurance

Para validar la configuración en Assurance:

1. Vaya a la interfaz de usuario de Assurance.
1. Seleccionar **[!UICONTROL Configurar]** en el carril izquierdo y seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a **[!UICONTROL Validar configuración]** debajo **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Seleccione **[!UICONTROL Guardar]**.
1. Seleccionar **[!UICONTROL Validar configuración]** en el carril izquierdo. Tanto la configuración del flujo de datos como la configuración del SDK se validan en la aplicación.
   ![Validación de AJO Decisioning](assets/ajo-decisioning-validation.png)


## Cree ofertas

1. En la IU de Journey Optimizer, seleccione ![Ofertas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Offers_18_N.svg)  **[!UICONTROL Ofertas]** de **[!UICONTROL GESTIÓN DE DECISIONES]** en el carril izquierdo.
1. En el **[!UICONTROL Ofertas]** pantalla, seleccione **[!UICONTROL Examinar]** para ver la lista de ofertas.
1. Seleccionar **[!UICONTROL Crear oferta]**.
1. En el **[!UICONTROL Nueva oferta]** diálogo, seleccione **[!UICONTROL Oferta personalizada]** y haga clic en **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Detalles]** paso de **[!UICONTROL Crear nueva oferta personalizada]**:
   1. Introduzca una **[!UICONTROL Nombre]** para la oferta, por ejemplo `Luma - Juno Jacket`, e introduzca un **[!UICONTROL Fecha y hora de inicio]** y un **[!UICONTROL Fecha y hora de finalización]**. Fuera de estas fechas, el motor de decisión no selecciona la oferta.
   1. Seleccione **[!UICONTROL Siguiente]**.
      ![Ofertas: detalles](assets/ajo-offers-details.png)

1. En el **[!UICONTROL Añadir representaciones]** paso de **[!UICONTROL Crear nueva oferta personalizada]**:
   1. Seleccionar ![Móvil](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DevicePhone_18_N.svg) **[!UICONTROL Móvil]** de **[!UICONTROL Canal]** y seleccione. **[!UICONTROL JSON móvil]** desde el **[!UICONTROL Ubicación]** lista.
   1. Seleccionar **[!UICONTROL Personalizado]** para **[!UICONTROL Contenido]**.
   1. Seleccionar **[!UICONTROL Añadir contenido]**. En el **[!UICONTROL Añadir personalización]** diálogo:
      1. Introduzca el siguiente JSON:

         ```json
         { 
             "title": "Juno Jacket",
             "text": "On colder-than-comfortable mornings, you'll love warming up in the Juno All-Ways Performanc Jacket, designed to compete with wind and chill. Built-in Cocona&trade; technology aids evaporation, while a special zip placket and stand-up collar keep your neck protected.", 
             "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/jackets/wj06-purple_main.jpg" 
         }  
         ```

      1. Seleccione **[!UICONTROL Guardar]**.
         ![Ofertas: contenido personalizado](assets/ajo-offers-customcontent.png)
   1. Seleccione **[!UICONTROL Siguiente]**.
      ![Representaciones de ofertas](assets/ajo-offers-representations.png)

1. En el **[!UICONTROL Añadir restricciones]** paso del **[!UICONTROL Crear nueva oferta personalizada]**:
   1. Establecer **[!UICONTROL Prioridad]** hasta `10`.
   1. Alternar **[!UICONTROL Incluir límite]** apagada.
   1. Seleccione **[!UICONTROL Siguiente]**.
      ![Ofertas: restricciones](assets/ajo-offers-constraints.png)

1. En el **[!UICONTROL Revisar]** paso de **[!UICONTROL Crear nuevo elemento personalizado]** oferta:
   1. Revise la oferta y seleccione **[!UICONTROL Finalizar]**.
   1. En el **[!UICONTROL Guardar oferta]** diálogo, seleccione **[!UICONTROL Guardar y aprobar]**.

1. Repita los pasos del 3 al 8 para crear cuatro ofertas más con nombres y contenido diferentes. Todos los demás valores de configuración, como Fecha y hora de inicio o Prioridad, son similares a la primera oferta creada. Puede crear y editar ofertas duplicadas rápidamente.

   1. En la IU de Journey Optimizer, seleccione ![Ofertas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Offers_18_N.svg) **[!UICONTROL Ofertas]** en el carril izquierdo, seleccione Ofertas en la barra superior.
   1. Seleccione la fila de la oferta que ha creado.
   1. En el panel derecho, seleccione ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmall_18_N.svg) **[!UICONTROL Más acciones]** y en el menú contextual, seleccione ![Duplicar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Duplicate_18_N.svg) **[!UICONTROL Duplicar]**.

      Utilice la tabla siguiente para definir las otras cuatro ofertas.

      | Nombre de oferta | Contenido de oferta |
      |---|---|
      | Luma: confirme la botella de agua | `{ "title": "Affirm Water Bottle", "text": "You'll stay hydrated with ease with the Affirm Water Bottle by your side or in hand. Measurements on the outside help you keep track of how much you're drinking, while the screw-top lid prevents spills. A metal carabiner clip allows you to attach it to the outside of a backpack or bag for easy access.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/fitness-equipment/ug06-lb-0.jpg" }` |
      | Luma: Desiree Fitness Tee | `{ "title": "Desiree Fitness Tee", "text": "When you're too far to turn back, thank yourself for choosing the Desiree Fitness Tee. Its ultra-lightweight, ultra-breathable fabric wicks sweat away from your body and helps keeps you cool for the distance.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/tees/ws05-yellow_main.jpg" }` |
      | Luma - Adrienne Trek Jacket | `{ "title": "Adrienne Trek Jacket", "text": "You're ready for a cross-country jog or a coffee on the patio in the Adrienne Trek Jacket. Its style is unique with stand collar and drawstrings, and it fits like a jacket should.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/jackets/wj08-gray_main.jpg" }` |
      | Luma: Camiseta de fitness diaria de Aero | `{ "title": "Adrienne Trek Jacket", "text": "You're ready for a cross-country jog or a coffee on the patio in the Adrienne Trek Jacket. Its style is unique with stand collar and drawstrings, and it fits like a jacket should.", "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/women/tops/jackets/wj08-gray_main.jpg" }` |

      {style="table-layout:fixed"}

1. Finalmente, debe crear una oferta de reserva, que es una oferta enviada a los clientes si no cumplen los requisitos para otras ofertas.
   1. Seleccionar **[!UICONTROL Crear oferta]**.
   1. En el **[!UICONTROL Detalles]** paso de **[!UICONTROL Crear nueva oferta personalizada]**:
   1. Introduzca una **[!UICONTROL Nombre]** para la oferta, por ejemplo `Luma - Fallback Offer`, e introduzca un **[!UICONTROL Fecha y hora de inicio]** y un **[!UICONTROL Fecha y hora de finalización]**.
   1. Seleccione **[!UICONTROL Siguiente]**.

1. En el **[!UICONTROL Añadir representaciones]** paso del **[!UICONTROL Crear nueva oferta personalizada]** pantalla:
   1. Seleccionar ![Móvil](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DevicePhone_18_N.svg) **[!UICONTROL Móvil]** de **[!UICONTROL Canal]** y seleccione. **[!UICONTROL JSON móvil]** de **[!UICONTROL Ubicación]** lista.
   1. Seleccionar **[!UICONTROL Personalizado]** para **[!UICONTROL Contenido]**.
   1. Seleccionar **[!UICONTROL Añadir contenido]**. En el **[!UICONTROL Añadir personalización]** diálogo:
      1. Introduzca el siguiente JSON:

         ```json
         {  
             "title": "Luma",
             "text": "Your store for sports wear and equipment.", 
             "image": "https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png" 
         }  
         ```

      1. Seleccione **[!UICONTROL Guardar]**.
   1. Seleccione **[!UICONTROL Siguiente]**.


1. En el **[!UICONTROL Revisar]** paso de **[!UICONTROL Crear nuevo elemento personalizado]** oferta:
   1. Revise la oferta y seleccione **[!UICONTROL Finalizar]**.
   1. En el **[!UICONTROL Guardar oferta]** diálogo, seleccione **[!UICONTROL Guardar y aprobar]**.

Ahora debería tener la siguiente lista de ofertas.
![Lista de ofertas](assets/ajo-offers-list.png)


## Crear una colección

Para presentar una oferta al usuario de la aplicación móvil, debe definir una colección de ofertas que consista en una o más de las ofertas creadas.

1. En la IU de Journey Optimizer, seleccione **[!UICONTROL Ofertas]** desde el carril izquierdo.
1. Seleccionar **[!UICONTROL Colecciones]** desde la barra superior.
1. Seleccionar ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Crear colección]**.
1. En el **[!UICONTROL Nueva colección]** modal, introduzca un **[!UICONTROL Nombre]** para su colección, por ejemplo `Luma - Mobile App Collection`, seleccione **[!UICONTROL Crear una colección estática]** y haga clic en **[!UICONTROL Siguiente]**.
1. Entrada **[!UICONTROL Luma: recopilación de aplicaciones móviles]**, seleccione las ofertas que desee incluir en la colección. Para este tutorial, elija las cinco ofertas que ha creado.
   ![Ofertas: colección](assets/ajo-collection-offersselected.png)
1. Seleccione **[!UICONTROL Guardar]**.


## Crear una decisión

El paso final es definir una decisión, que es la combinación de uno o más ámbitos de decisión y la oferta de reserva.

Un ámbito de decisión es una combinación de una ubicación específica (por ejemplo, un HTML en un correo electrónico o JSON en una aplicación móvil) y uno o más criterios de evaluación.

Un criterio de evaluación es la combinación de

* colección de ofertas,
* reglas de elegibilidad: por ejemplo, la oferta solo está disponible para una audiencia específica,
* método de clasificación: cuando hay varias ofertas disponibles para elegir, qué método se utiliza para clasificarlas (por ejemplo, por prioridad de oferta, mediante una fórmula o un modelo de IA).

Consulte [Pasos clave para crear y administrar ofertas](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/key-steps.html?lang=en) si desea comprender mejor cómo interactúan y se relacionan entre sí las ubicaciones, las reglas, las clasificaciones, las ofertas, las representaciones, las colecciones, las decisiones, etc. Este tutorial se centra únicamente en el uso del resultado de una decisión, en lugar de en la flexibilidad para definirla.

1. En la IU de Journey Optimizer, seleccione **[!UICONTROL Ofertas]** desde el carril izquierdo.
1. Seleccionar **[!UICONTROL Decisiones]** desde la barra superior.
1. Seleccionar ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Crear decisión]**.
1. En el **[!UICONTROL Detalles]** paso de **[!UICONTROL Crear una nueva decisión de oferta]**:
   1. Introduzca una **[!UICONTROL Nombre]** para la decisión, por ejemplo `Luma - Mobile App Decision`, introduzca **[!UICONTROL Fecha y hora de inicio]** y **[!UICONTROL Fecha y hora de finalización]**.
   1. Seleccione **[!UICONTROL Siguiente]**.

1. En el **[!UICONTROL Agregar ámbitos de decisión]** paso de **[!UICONTROL Crear una nueva decisión de oferta]**:
   1. Seleccionar **[!UICONTROL JSON móvil]** de **[!UICONTROL Ubicación]** lista.
   1. En el **[!UICONTROL Criterios de evaluación]** mosaico, seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir]**.
      1. En el **[!UICONTROL Añadir colección de ofertas]** , seleccione la colección de ofertas. Por ejemplo, **[!UICONTROL Luma: recopilación de aplicaciones móviles]**.
      1. Seleccionar **[!UICONTROL Añadir]**.
         ![Decisión: Seleccionar colección](assets/ajo-decision-selectcollection.png)
   1. Asegúrese de que **[!UICONTROL Ninguno]** está seleccionado para **[!UICONTROL Idoneidad]**, y **[!UICONTROL Prioridad de ofertas]** está seleccionado como **[!UICONTROL Método de clasificación]**.
   1. Seleccione **[!UICONTROL Siguiente]**.
      ![Ámbitos de decisión](assets/ajo-decision-scopes.png).
1. En el **[!UICONTROL Añadir oferta de reserva]** paso de **[!UICONTROL Crear una nueva decisión de oferta]**:
   1. Seleccione la oferta de reserva, por ejemplo, la **[!UICONTROL Luma: oferta de reserva]**.
   1. Seleccione **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Resumen]** paso de **[!UICONTROL Crear una nueva decisión de oferta]**:
   1. Seleccione **[!UICONTROL Finalizar]**.
   1. En el **[!UICONTROL Guardar decisión de oferta]** diálogo, seleccione **[!UICONTROL Guardar y activar]**.
   1. En el **[!UICONTROL Decisiones]** pestaña, verá su decisión con el estado **[!UICONTROL Activo]**.

La decisión de oferta, que consiste en un conjunto de ofertas, ya está lista para su uso. Para utilizar la decisión en la aplicación, debe hacer referencia en el código al ámbito de decisión.

1. En la IU de Journey Optimizer, seleccione **[!UICONTROL Ofertas]**.
1. Seleccionar **[!UICONTROL Decisiones]** desde la barra superior.
1. Seleccione su decisión, por ejemplo **[!UICONTROL Luma: decisión sobre aplicaciones móviles]**.
1. En el **[!UICONTROL Ámbitos de decisión]** mosaico, seleccione ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Copiar]**.
1. En el menú contextual, seleccione **[!UICONTROL Ámbito de decisión]**.
   ![Copiar ámbito de decisión](assets/ajo-copy-decisionscope.png)
1. Utilice cualquier editor de texto para pegar el ámbito de decisión para utilizarlo posteriormente. El ámbito de decisión tiene el siguiente formato JSON.

   ```json
   {
       "xdm:activityId":"xcore:offer-activity:xxxxxxxxxxxxxxx",
       "xdm:placementId":"xcore:offer-placement:xxxxxxxxxxxxxxx"
   }
   ```

## Implementación de ofertas en la aplicación

Como se ha explicado en lecciones anteriores, la instalación de una extensión de etiqueta móvil solo proporciona la configuración. A continuación, debe instalar y registrar Optimize SDK. Si estos pasos no están claros, revise la [Instalación de SDK](install-sdks.md) sección.

>[!NOTE]
>
>Si ha completado la [Instalación de SDK](install-sdks.md) , el SDK ya está instalado y puede omitir este paso.
>

1. En Xcode, asegúrese de que [Optimización de AEP](https://github.com/adobe/aepsdk-messaging-ios.git) se añade a la lista de paquetes en Dependencias del paquete. Consulte [Administrador De Paquetes Swift](install-sdks.md#swift-package-manager).
1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** en el navegador del proyecto Xcode.
1. Asegurar `AEPOptimize` forma parte de su lista de importaciones.

   `import AEPOptimize`

1. Asegurar `Optimize.self` forma parte de la matriz de extensiones que está registrando.

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

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode. Busque el `func updatePropositionOD(ecid: String, activityId: String, placementId: String, itemCount: Int) async` función. Inspect el código que

   * configura un diccionario XDM `xdmData`, que contiene el ECID para identificar el perfil para el que debe presentar las ofertas.
   * define `decisionScope`: un objeto que se basa en la decisión que ha definido en la interfaz de usuario de Journey Optimizer - Gestión de decisiones y se define mediante el ámbito de decisión copiado de [Crear una decisión](#create-a-decision).
   * llama a dos API de: [`Optimize.clearCachePropositions`](https://support.apple.com/en-ie/guide/mac-help/mchlp1015/mac)  y [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions).   Estas funciones borran todas las propuestas almacenadas en caché y actualizan las propuestas de este perfil. La aplicación de Luma utiliza un archivo de configuración (`decisions.json`) que recupera los parámetros de ámbito en función del siguiente formato JSON:

     ```swift
     "scopes": [
         {
             "name": "luma - Mobile App Decision",
             "activityId": "xcore:offer-activity:177cdaa5e1fd589d",
             "placementId": "xcore:offer-placement:13a3b264ce69bb14",
             "itemCount": 2
         }
     ]
     ```

     Sin embargo, puede utilizar cualquier tipo de implementación para asegurarse de que las API de optimización no obtienen los parámetros adecuados (`activityId`, `placementId` y, `itemCount`), para construir un válido [`DecisionScope`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#decisionscope) para su implementación.

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vistas]** > **[!UICONTROL Personalización]** > **[!UICONTROL EdgeOffersView]** en el navegador del proyecto Xcode. Busque el `func getPropositionOD(activityId: String, placementId: String, itemCount: Int) async` e inspeccione el código de esta función. La parte más importante de esta función es la  [`Optimize.getPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#getpropositions) Llamada de API, que

   * recupera las propuestas del perfil actual en función del ámbito de decisión (que ha definido en Journey Optimizer, Gestión de decisiones) y
   * desajusta el resultado en contenido que se pueda mostrar correctamente en la aplicación.

1. Sigue en **[!UICONTROL EdgeOffersView]**, busque la variable `func updatePropositions(activityId: String, placementId: String, itemCount: Int) async` y agregue el siguiente código:

   ```swift
       Task {
           await self.updatePropositionOD(
               ecid: currentEcid,
               activityId: activityId,
               placementId: placementId,
               itemCount: itemCount
           )
       }
       try? await Task.sleep(seconds: 2.0)
       Task {
           await self.getPropositionOD(
               activityId: activityId,
               placementId: placementId,
               itemCount: itemCount
           )
       }
   ```

   Este código garantiza la actualización de las propuestas y la recuperación de los resultados mediante las funciones descritas en los pasos 5 y 6.


## Validación mediante la aplicación

1. Abra la aplicación en un dispositivo o en el simulador.

1. Vaya a la **[!UICONTROL Personalización]** pestaña.

1. Seleccionar **[!UICONTROL Personalización de Edge]**.

1. Desplácese hasta la parte superior y verá dos ofertas aleatorias mostradas desde la colección que ha definido en la **[!UICONTROL DECISIÓN LUMA - DECISIÓN DE APLICACIÓN MÓVIL]** mosaico.

   <img src="assets/ajo-app-offers.png" width="300">

   Las ofertas son aleatorias, ya que ha dado a todas las ofertas la misma prioridad y la clasificación de la decisión se basa en la prioridad.


## Validar la implementación en Assurance

Para validar la implementación de ofertas en Assurance:

1. Vaya a la interfaz de usuario de Assurance.
1. Seleccionar **[!UICONTROL Configurar]** en el carril izquierdo y seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a **[!UICONTROL Revisar y simular]** debajo **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Seleccione **[!UICONTROL Guardar]**.
1. Seleccionar **[!UICONTROL Revisar y simular]** en el carril izquierdo. Tanto la configuración del flujo de datos como la configuración del SDK se validan en la aplicación.
1. Seleccionar **[!UICONTROL Solicitudes]** en la barra superior. Ya ve su **[!UICONTROL Ofertas]** solicitudes.
   ![Validación de AJO Decisioning](assets/assurance-decisioning-requests.png)

1. Puede explorar **[!UICONTROL Simular]** y **[!UICONTROL Lista de eventos]** para obtener más funcionalidad, compruebe la configuración de Journey Optimizer Decision Management.

## Pasos siguientes

Ahora debería tener todas las herramientas para empezar a añadir más funcionalidades a su implementación de Journey Optimizer - Gestión de decisiones. Por ejemplo:

* aplique parámetros diferentes a las ofertas (por ejemplo, prioridad o límite)
* recopilar atributos de perfil en la aplicación (consulte [Perfil](profile.md)) y utilice estos atributos de perfil para crear audiencias. A continuación, utilice estas audiencias como parte de las reglas de idoneidad en su decisión.
* combinar varios ámbitos de decisión.

>[!SUCCESS]
>
>Ha habilitado la aplicación para que muestre ofertas con la extensión Journey Optimizer - Decisioning para el SDK de Experience Platform Mobile.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Realizar pruebas A/B con Target](target.md)**
