---
title: Realizar pruebas A/B en aplicaciones móviles con Target y el SDK móvil de Platform
description: Aprenda a utilizar una prueba A/B de Target en su aplicación móvil con el SDK móvil de Platform y Adobe Target.
solution: Data Collection,Target
feature-set: Target
feature: A/B Tests
jira: KT-14641
exl-id: 87546baa-2d8a-4cce-b531-bec3782d2e90
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 2%

---

# Optimización y personalización con Adobe Target

Obtenga información sobre cómo optimizar y personalizar las experiencias en sus aplicaciones móviles con el SDK móvil de Platform y Adobe Target.

Target proporciona todo lo que debe adaptar y personalizar las experiencias de los clientes. Target le ayuda a maximizar los ingresos de sus sitios web y móviles, aplicaciones, medios sociales y otros canales digitales. Target puede realizar pruebas A/B y multivariadas, recomendar productos y contenido, segmentar contenido, personalizar automáticamente el contenido con IA y mucho más. Esta lección se centra en la funcionalidad de prueba A/B de Target. Consulte la [Información general sobre las pruebas A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=en) para obtener más información.

![Arquitectura](assets/architecture-at.png)

Antes de poder realizar pruebas A/B con Target, debe asegurarse de que las configuraciones y integraciones adecuadas estén implementadas.

>[!NOTE]
>
>Esta lección es opcional y solo se aplica a los usuarios de Adobe Target que buscan realizar pruebas A/B.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.
* Acceso a Adobe Target con permisos, funciones, espacios de trabajo y propiedades correctamente configurados, tal como se describe [aquí](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=es).


## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Actualice la secuencia de datos para la integración con Target.
* Actualice la propiedad de etiquetas con la extensión Journey Optimizer - Decisioning.
* Actualice el esquema para capturar eventos de propuesta.
* Valide la configuración en Assurance.
* Cree una prueba A/B sencilla en Target.
* Actualice la aplicación para registrar la extensión de Optimizer.
* Implemente la prueba A/B en la aplicación.
* Valide la implementación en Assurance.


## Configuración

>[!TIP]
>
>Si ya ha configurado la aplicación como parte de la [Ofertas de Journey Optimizer](journey-optimizer-offers.md) En esta lección, es posible que ya haya realizado algunos de los pasos de esta sección de configuración.

### Actualizar configuración de secuencia de datos

#### Adobe Target

Para garantizar que los datos enviados desde su aplicación móvil a Experience Platform Edge Network se reenvíen a Adobe Target, debe actualizar la configuración de su flujo de datos.

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y seleccione la secuencia de datos, por ejemplo **[!DNL Luma Mobile App]**.
1. Seleccionar **[!UICONTROL Añadir servicio]** y seleccione **[!UICONTROL Adobe Target]** desde el **[!UICONTROL Servicio]** lista.
1. Si es cliente de Target Premium y desea utilizar tokens de propiedad de, introduzca el Target **[!UICONTROL Token de propiedad]** que desee utilizar para esta integración. Los usuarios de Target Standard pueden omitir este paso.

   Puede encontrar sus propiedades en la interfaz de usuario de Target, en **[!UICONTROL Administration]** > **[!UICONTROL Propiedades]**. Seleccionar ![Código](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) para mostrar el token de propiedad de la propiedad que desea utilizar. El token de propiedad tiene un formato similar a `"at_property": "xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"`; sólo debe introducir el valor `xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx`.

   De forma opcional, puede especificar un ID de entorno de destino. Target utiliza entornos para organizar sus sitios y entornos de preproducción para facilitar la administración y la creación de informes por separado. Los entornos preestablecidos incluyen Producción, Ensayo y Desarrollo. Consulte [Entornos](https://experienceleague.adobe.com/docs/target/using/administer/environments.html?lang=en) y [ID de entorno de destino](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=en#target-environment-id) para obtener más información.

   De forma opcional, puede especificar un área de nombres de ID de terceros de Target para admitir la sincronización de perfiles en un área de nombres de identidad (por ejemplo, ID de CRM). Consulte [Área de nombres de ID de terceros de Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=en#target-third-party-id-namespace) para obtener más información.

1. Seleccione **[!UICONTROL Guardar]**.

   ![Añadir Target al conjunto de datos](assets/edge-datastream-target.png)


#### Adobe Journey Optimizer

Para garantizar que los datos enviados desde su aplicación móvil a la red perimetral se reenvíen a Journey Optimizer - Gestión de decisiones, actualice la configuración de la secuencia de datos.

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y seleccione la secuencia de datos, por ejemplo **[!DNL Luma Mobile App]**.
1. Seleccionar ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) para **[!UICONTROL Experience Platform]** y seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar]** en el menú contextual.
1. En el **[!UICONTROL Datastreams]** > ![Carpeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) >  **[!UICONTROL Adobe Experience Platform]** , asegúrese de que **[!UICONTROL Offer decisioning]**, **[!UICONTROL Segmentación de Edge]**, y **[!UICONTROL Destinos de personalización]** están seleccionados. Si también sigue las lecciones de Journey Optimizer, debe seleccionar **[!UICONTROL Adobe Journey Optimizer]**. Consulte [Configuración de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) para obtener más información.
1. Para guardar la configuración de la secuencia de datos, seleccione **[!UICONTROL Guardar]** .

   ![Configuración de flujo de datos AEP](assets/datastream-aep-configuration-target.png)


### Instalación de Adobe Journey Optimizer: extensión de etiquetas de Decisioning

1. Vaya a **[!UICONTROL Etiquetas]**, busque la propiedad de etiquetas móviles y abra la propiedad.
1. Seleccionar **[!UICONTROL Extensiones]**.
1. Seleccionar **[!UICONTROL Catálogo]**.
1. Busque la variable **[!UICONTROL Adobe Journey Optimizer - Toma de decisiones]** extensión.
1. Instale la extensión de. La extensión no requiere ninguna configuración adicional.

   ![Añadir extensión de Decisioning](assets/tag-add-decisioning-extension.png)


### Actualizar el esquema

1. Vaya a la interfaz de recopilación de datos y seleccione **[!UICONTROL Esquemas]** desde el carril izquierdo.
1. Seleccionar **[!UICONTROL Examinar]** desde la barra superior.
1. Seleccione el esquema para abrirlo.
1. En el editor de esquemas, seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir]** junto a **[!UICONTROL Grupos de campos]**.
1. En el **[!UICONTROL Adición de grupos de campos]** diálogo, buscar `proposition`, seleccione **[!UICONTROL Evento de experiencia: interacciones de propuesta]** y seleccione **[!UICONTROL Adición de grupos de campos]**.
   ![Proposición](assets/schema-fieldgroup-proposition.png)
1. Para guardar los cambios en el esquema, seleccione **[!UICONTROL Guardar]**.


### Validar la configuración en Assurance

Para validar la configuración en Assurance:

1. Vaya a la interfaz de usuario de Assurance.
1. Seleccionar **[!UICONTROL Configurar]** en el carril izquierdo y seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a **[!UICONTROL Validar configuración]** debajo **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Seleccione **[!UICONTROL Guardar]**.
1. Seleccionar **[!UICONTROL Validar configuración]** en el carril izquierdo. Tanto la configuración del flujo de datos como la configuración del SDK se validan en la aplicación.
   ![Validación de AJO Decisioning](assets/ajo-decisioning-validation.png)

## Crear una prueba A/B

Existen muchos tipos de actividades que puede crear en Adobe Target e implementar en una aplicación móvil, como se menciona en la introducción. Para esta lección, debe implementar una prueba A/B.

1. En la IU de Target, seleccione **[!UICONTROL Actividades]** desde la barra superior.
1. Seleccionar **[!UICONTROL Crear actividad]** y **[!UICONTROL Prueba A/B]** en el menú contextual.
1. En el **[!UICONTROL Crear actividad de prueba A/B]** diálogo, seleccione **[!UICONTROL Móvil]** como el **[!UICONTROL Tipo]**, seleccione un espacio de trabajo del **[!UICONTROL Elija Workspace]** y seleccione su propiedad en la lista **[!UICONTROL Elegir propiedad]** lista si es cliente de Target Premium y ha especificado un token de propiedad en el conjunto de datos.
1. Seleccione **[!UICONTROL Crear]**.
   ![Crear actividad de Target](assets/target-create-activity1.png)

1. En el **[!UICONTROL Actividad sin título]** pantalla, en el **[!UICONTROL Experiencias]** paso:

   1. Entrar `luma-mobileapp-abtest` in **[!UICONTROL Seleccionar ubicación]** debajo **[!UICONTROL UBICACIÓN 1]**. Este nombre de ubicación (denominada con frecuencia como mbox) se utiliza más adelante en la implementación de la aplicación.
   1. Seleccionar ![Corchete hacia abajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) junto a **[!UICONTROL Contenido predeterminado]** y seleccione **[!UICONTROL Crear oferta JSON]** en el menú contextual.
   1. Copie el siguiente JSON en **[!UICONTROL Introduzca un objeto JSON válido]**.

      ```json
      { 
          "title": "Luma Anaolog Watch",
          "text": "Designed to stand up to your active lifestyle, this women's Luma Analog Watch features a tasteful brushed chrome finish and a stainless steel, water-resistant construction for lasting durability.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Luma_Analog_Watch.jpg" 
      }
      ```

   1. Seleccionar **[!UICONTROL + Agregar experiencia]**.

      ![Experiencia A](assets/target-create-activity-experienceA.png)

   1. Repita los pasos b y c para la experiencia B, pero en su lugar utilice el siguiente JSON:

      ```json
      { 
          "title": "Aim Analog Watch",
          "text": "The flexible, rubberized strap is contoured to conform to the shape of your wrist for a comfortable all-day fit. The face features three illuminated hands, a digital read-out of the current time, and stopwatch functions.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Aim_Watch.jpg" 
      }
      ```

   1. Seleccione **[!UICONTROL Siguiente]**.

      ![Experiencia B](assets/target-create-activity-experienceB.png)

1. En el **[!DNL Targeting]** paso, revise la configuración de la prueba A/B. De forma predeterminada, ambas ofertas se asignan de forma equitativa entre todos los visitantes. Haga clic en **[!UICONTROL Siguiente]** para continuar.

   ![Segmentación](assets/taget-targeting.png)

1. En el **[!UICONTROL Objetivos y configuración]** paso:

   1. Cambie el nombre de la actividad sin título, por ejemplo, a `Luma Mobile SDK Tutorial - A/B Test Example`.
   1. Introduzca una **[!UICONTROL Objetivo]** para la prueba A/B, por ejemplo `A/B Test for Luma mobile app tutorial`.
   1. Seleccionar **[!UICONTROL Conversión]**, **[!UICONTROL Visualizó un mbox]** en el **[!UICONTROL Métrica de objetivo]** > **[!UICONTROL MI OBJETIVO PRINCIPAL]** y escriba el nombre de su ubicación (mbox), por ejemplo `luma-mobileapp-abtest`.
   1. Seleccionar **[!UICONTROL Guardar y cerrar]**.

      ![Configuración de objetivos](assets/target-goals.png)

1. De nuevo en **[!UICONTROL Todas las actividades]** pantalla:

   1. Seleccionar ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) en su actividad de.
   1. Seleccionar ![Reproducir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg) **[!UICONTROL Activar]** para activar la prueba A/B.

   ![Activar](assets/target-activate.png)


## Implementación de Target en la aplicación

Como se ha explicado en lecciones anteriores, la instalación de una extensión de etiqueta móvil solo proporciona la configuración. A continuación, debe instalar y registrar Optimize SDK. Si estos pasos no están claros, revise la [Instalación de SDK](install-sdks.md) sección.

>[!NOTE]
>
>Si ha completado la [Instalación de SDK](install-sdks.md) , el SDK ya está instalado y puede omitir este paso.
>

1. En Xcode, asegúrese de que [Optimización de AEP](https://github.com/adobe/aepsdk-messaging-ios) se añade a la lista de paquetes en Dependencias del paquete. Consulte [Administrador De Paquetes Swift](install-sdks.md#swift-package-manager).
1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL AppDelegate]** en el navegador del proyecto Xcode.
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

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]** en el navegador del proyecto Xcode. Busque el ` func updatePropositionAT(ecid: String, location: String) async` función. Añada el siguiente código:

   ```swift
   // set up the XDM dictionary, define decision scope and call update proposition API
   Task {
       let ecid = ["ECID" : ["id" : ecid, "primary" : true] as [String : Any]]
       let identityMap = ["identityMap" : ecid]
       let xdmData = ["xdm" : identityMap]
       let decisionScope = DecisionScope(name: location)
       Optimize.clearCachedPropositions()
       Optimize.updatePropositions(for: [decisionScope], withXdm: xdmData)
   }
   ```

   Esta función:

   * configura un diccionario XDM `xdmData`, que contiene el ECID para identificar el perfil para el que debe presentar la prueba A/B, y
   * define un `decisionScope`, una matriz de ubicaciones sobre dónde presentar la prueba A/B.

   A continuación, la función llama a dos API: [`Optimize.clearCachedPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#clearpropositions) y [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions). Estas funciones borran todas las propuestas almacenadas en caché y actualizan las propuestas de este perfil. Una propuesta en este contexto es la experiencia (oferta) seleccionada en la actividad de Target (su prueba A/B) y que ha definido en [Creación de una prueba A/B](#create-an-ab-test).

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Personalization]** > **[!DNL TargetOffersView]** en el navegador del proyecto Xcode. Busque el `func onPropositionsUpdateAT(location: String) async {` e inspeccione el código de esta función. La parte más importante de esta función es la  [`Optimize.onPropositionsUpdate`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#onpropositionsupdate) Llamada de API, que:
   * recupera las propuestas del perfil actual en función del ámbito de decisión (que es la ubicación definida en la prueba A/B),
   * recupera la oferta de la propuesta,
   * desajusta el contenido de la oferta para que se pueda mostrar correctamente en la aplicación, y
   * déclencheur el `displayed()` acción en la oferta que devuelve un evento a Platform Edge Network que informa de que se muestra la oferta.

1. Sigue en **[!DNL TargetOffersView]**, agregue el siguiente código a `.onFirstAppear` modificador. Este código garantiza que la llamada de retorno para actualizar las ofertas se registre solo una vez.

   ```swift
   // Invoke callback for offer updates
   Task {
       await self.onPropositionsUpdateAT(location: location)
   }
   ```

1. Sigue en **[!DNL TargetOffersView]**, agregue el siguiente código a `.task` modificador. Este código actualiza las ofertas cuando se actualiza la vista.

   ```swift
   // Clear and update offers
   await self.updatePropositionsAT(ecid: currentEcid, location: location)
   ```

Puede enviar parámetros de Target adicionales (como parámetros de mbox, perfil, producto o pedido) en una solicitud de consulta de personalización a la red de Experience Edge, agregándolos a un diccionario de datos al llamar a [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions) API. Consulte para obtener más información [Parámetros de Target](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/#target-parameters).


## Validación mediante la aplicación

1. Vuelva a compilar y ejecute la aplicación en el simulador o en un dispositivo físico desde Xcode mediante ![Reproducir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Vaya a la **[!UICONTROL Personalización]** pestaña.

1. Desplácese hacia abajo hasta la parte inferior y verá una de las dos ofertas definidas en la prueba A/B en la **[!UICONTROL DESTINO]** mosaico.

   <img src="assets/target-app-offer.png" width="300">


## Validar la implementación en Assurance

Para validar la prueba A/B en Assurance:

1. Revise la [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo a Assurance.
1. Seleccionar **[!UICONTROL Configurar]** en el carril izquierdo y seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a **[!UICONTROL Revisar y simular]** debajo **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Seleccione **[!UICONTROL Guardar]**.
1. Seleccionar **[!UICONTROL Revisar y simular]** en el carril izquierdo. Tanto la configuración del flujo de datos como la configuración del SDK se validan en la aplicación.
1. Seleccionar **[!UICONTROL Solicitudes]** en la barra superior. Ya ve su **[!DNL Target]** solicitudes.
   ![Validación de AJO Decisioning](assets/assurance-decisioning-requests.png)

1. Puede explorar **[!UICONTROL Simular]** y **[!UICONTROL Lista de eventos]** para obtener más funcionalidad, compruebe la configuración de las ofertas de Target.

## Pasos siguientes

Ahora debe tener todas las herramientas para empezar a agregar más pruebas A/B u otras actividades de Target (como Segmentación de experiencias o Prueba multivariable), cuando corresponda y corresponda, a la aplicación. Hay información más detallada disponible en el [Repositorio de GitHub para la extensión de Optimize](https://github.com/adobe/aepsdk-optimize-ios) donde también puede encontrar un vínculo a un [tutorial](https://opensource.adobe.com/aepsdk-optimize-ios/#/tutorials/README) sobre cómo rastrear ofertas de Adobe Target.

>[!SUCCESS]
>
>Ha habilitado la aplicación para pruebas A/B y ha mostrado los resultados de una prueba A/B con Adobe Target y la extensión Adobe Journey Optimizer - Decisioning para el SDK de Adobe Experience Platform Mobile.
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Conclusión y pasos siguientes](conclusion.md)**
