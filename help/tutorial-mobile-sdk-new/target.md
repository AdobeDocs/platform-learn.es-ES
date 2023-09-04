---
title: Realizar pruebas A/B con Target
description: Aprenda a utilizar una prueba A/B de Target en su aplicación móvil con el SDK móvil de Platform y Adobe Target.
solution: Data Collection,Target
feature-set: Target
feature: A/B Tests
hide: true
source-git-commit: 7435a2758bdd8340416b70faf8337e33167a7193
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 2%

---


# Realizar pruebas A/B con Target

Obtenga información sobre cómo realizar pruebas A/B en sus aplicaciones móviles con el SDK móvil de Platform y Adobe Target.

Target proporciona todo lo que debe adaptar y personalizar las experiencias de los clientes. Target le ayuda a maximizar los ingresos de sus sitios web y móviles, aplicaciones, medios sociales y otros canales digitales. Este tutorial se centra en la funcionalidad de prueba A/B de Target. Consulte la [Información general sobre las pruebas A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=en) para obtener más información.

Antes de poder realizar pruebas A/B con Target, debe asegurarse de que las configuraciones y integraciones adecuadas estén implementadas.

>[!NOTE]
>
>Esta lección es opcional y solo se aplica a los usuarios de Adobe Target que buscan realizar pruebas A/B.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.
* Acceso a Adobe Target Premium con permisos, funciones correctamente configuradas, espacios de trabajo y propiedades como se describe a continuación [aquí](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=es).
También puede utilizar Target Standard, pero el tutorial utiliza algunos conceptos avanzados (por ejemplo, propiedades de Target) que son únicos en Target Premium.


## Objetivos de aprendizaje

En esta lección, debe

* Actualice la configuración de Edge para la integración de Target.
* Actualice la propiedad de etiquetas con la extensión Journey Optimizer - Decisioning.
* Actualice el esquema para capturar eventos de propuesta.
* Valide la configuración en Assurance.
* Cree una prueba A/B sencilla en Target.
* Actualice la aplicación para incluir la extensión de Optimizer.
* Implemente la prueba A/B en la aplicación.
* Valide la implementación en Assurance.


## Configure la aplicación

>[!TIP]
>
>Si ya ha configurado la aplicación como parte de la [Ofertas de Journey Optimizer](journey-optimizer-offers.md) tutorial, puede omitir [Instalación de Adobe Journey Optimizer: extensión de etiquetas de Decisioning](#install-adobe-journey-optimizer---decisioning-tags-extension) y [Actualizar el esquema](#update-your-schema).

### Actualizar configuración de Edge

Para garantizar que los datos enviados desde la aplicación móvil a la red perimetral se reenvíen a Adobe Target, debe actualizar la configuración de Experience Edge.

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y seleccione la secuencia de datos, por ejemplo **[!UICONTROL Aplicación móvil de Luma]**.
1. Seleccionar **[!UICONTROL Añadir servicio]** y seleccione **[!UICONTROL Adobe Target]** desde el **[!UICONTROL Servicio]** lista.
1. Introduzca el objetivo **[!UICONTROL Token de propiedad]** que desee utilizar para esta integración.

   Puede encontrar sus propiedades en la interfaz de usuario de Target, en **[!UICONTROL Administration]** > **[!UICONTROL Propiedades]**. Seleccionar ![Código](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) para mostrar el token de propiedad de la propiedad que desea utilizar. El token de propiedad tiene un formato similar a `"at_property": "xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"`; sólo debe introducir el valor `xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx`.

1. Seleccione **[!UICONTROL Guardar]**.

   ![Añadir Target al conjunto de datos](assets/edge-datastream-target.png)


### Instalación de Adobe Journey Optimizer: extensión de etiquetas de Decisioning

1. Vaya a **[!UICONTROL Etiquetas]** y busque la propiedad de etiquetas móviles y ábrala.
1. Seleccionar **[!UICONTROL Extensiones]**.
1. Seleccionar **[!UICONTROL Catálogo]**.
1. Busque la variable **[!UICONTROL Adobe Journey Optimizer - Toma de decisiones]** extensión.
1. Instale la extensión de. La extensión no requiere ninguna configuración adicional.

   ![Añadir extensión de Decisioning](assets/tag-add-decisioning-extension.png)


### Actualizar el esquema

1. Vaya a la interfaz de usuario de recopilación de datos y seleccione Esquemas en el carril izquierdo.
1. Seleccionar **[!UICONTROL Examinar]** desde la barra superior.
1. Seleccione el esquema para abrirlo.
1. En el editor de esquemas, seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir]** junto a **[!UICONTROL Grupos de campos]**.
1. En el cuadro de diálogo Agregar grupos de campos, busque `proposition`, seleccione **[!UICONTROL Evento de experiencia: interacciones de propuesta]** y seleccione **[!UICONTROL Adición de grupos de campos]**.
   ![Proposición](assets/schema-fieldgroup-proposition.png)
1. para guardar los cambios en el esquema, seleccione **[!UICONTROL Guardar]** .


### Validar la configuración en Assurance

Para validar la configuración en Assurance:

1. Vaya a la interfaz de usuario de Assurance.
1. Seleccionar **[!UICONTROL Configurar]** en el carril izquierdo y seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a **[!UICONTROL Validar configuración]** debajo **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Seleccione **[!UICONTROL Guardar]**.
1. Seleccionar **[!UICONTROL Validar configuración]** en el carril izquierdo. Tanto la configuración del flujo de datos como la configuración del SDK se validan en la aplicación.
   ![Validación de AJO Decisioning](assets/ajo-decisioning-validation.png)

## Crear una prueba A/B

1. En la IU de Target, seleccione **[!UICONTROL Actividades]** desde la barra superior.
1. Seleccionar **[!UICONTROL Crear actividad]** y **[!UICONTROL Prueba A/B]** en el menú contextual.
1. En el **[!UICONTROL Crear actividad de prueba A/B]** diálogo, seleccione **[!UICONTROL Móvil]** como el **[!UICONTROL Tipo]**, seleccione un espacio de trabajo del **[!UICONTROL Elija Workspace]** y seleccione su propiedad en la lista **[!UICONTROL Elegir propiedad]** lista.
1. Seleccione **[!UICONTROL Crear]**.
   ![Crear actividad de Target](assets/target-create-activity1.png)

1. En el **[!UICONTROL Actividad sin título]** pantalla, en el **[!UICONTROL Experiencias]** paso:

   1. Entrar `luma-mobileapp-abtest` in **[!UICONTROL Seleccionar ubicación]** debajo **[!UICONTROL UBICACIÓN 1]**.
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

1. En el **[!UICONTROL Segmentación]** paso, revise la configuración de la prueba A/B. De forma predeterminada, ambas ofertas se asignan de forma equitativa entre todos los visitantes. Haga clic en **[!UICONTROL Siguiente]** para continuar.

   ![Direccionamiento](assets/taget-targeting.png)

1. En el **[!UICONTROL Objetivos y configuración]** paso:

   1. Cambie el nombre de la actividad sin título, por ejemplo, a `Luma Mobile SDK Tutorial - A/B Test Example`.
   1. Introduzca una **[!UICONTROL Objetivo]** para la prueba A/B, por ejemplo `A/B Test for Luma mobile app tutorial`.
   1. Seleccionar **[!UICONTROL Conversión]**, **[!UICONTROL Se ha hecho clic en mbox]** en el **[!UICONTROL Métrica de objetivo]** > **[!UICONTROL MI OBJETIVO PRINCIPAL]** y escriba el nombre de su ubicación (mbox), por ejemplo `luma-mobileapp-abtest`.
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

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode. Busque el ` func updatePropositionAT(ecid: String, location: String) async` función. Añada el siguiente código:

   ```swift
   Task {
       let ecid = ["ECID" : ["id" : ecid, "primary" : true] as [String : Any]]
       let identityMap = ["identityMap" : ecid]
       let xdmData = ["xdm" : identityMap]
       let decisionScope = DecisionScope(name: location)
       Optimize.clearCachedPropositions()
       Optimize.updatePropositions(for: [decisionScope], withXdm: xdmData)
   }
   ```

   Esta función

   * configura un diccionario XDM `xdmData`, que contiene el ECID para identificar el perfil para el que debe presentar la prueba A/B, y
   * define un `decisionScope`, una matriz de ubicaciones sobre dónde presentar la prueba A/B.

   A continuación, la función llama a dos API: [`Optimize.clearCachePropositions`](https://support.apple.com/en-ie/guide/mac-help/mchlp1015/mac)  y [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions). Estas funciones borran todas las propuestas almacenadas en caché y actualizan las propuestas de este perfil.

1. Vaya a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vistas]** > **[!UICONTROL Personalización]** > **[!UICONTROL TargetOffersView]** en el navegador del proyecto Xcode. Busque el `func getPropositionAT(location: String) async` e inspeccione el código de esta función. La parte más importante de esta función es la  [`Optimize.getPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#getpropositions) Llamada de API, que
   * recupera las propuestas del perfil actual en función del ámbito de decisión (que es la ubicación definida en la prueba A/B) y
   * desajusta el resultado en contenido que se pueda mostrar correctamente en la aplicación.

1. Sigue en **[!UICONTROL TargetOffersView]**, busque la variable `func updatePropositions(location: String) async` y agregue el siguiente código:

   ```swift
       Task {
           await self.updatePropositionAT(
               ecid: currentEcid,
               location: location
           )
       }
       try? await Task.sleep(seconds: 2.0)
       Task {
           await self.getPropositionAT(
               location: location
           )
       }
   ```

   Este código garantiza la actualización de las propuestas y la recuperación de los resultados mediante las funciones descritas en los pasos 5 y 6.


## Validación mediante la aplicación

1. Abra la aplicación en un dispositivo o en el simulador.

1. Vaya a la **[!UICONTROL Personalización]** pestaña.

1. Seleccionar **[!UICONTROL Personalización de Edge]**.

1. Desplácese hacia abajo hasta la parte inferior y verá una de las dos ofertas definidas en la prueba A/B en la **[!UICONTROL DESTINO]** mosaico.

   <img src="assets/target-app-offer.png" width="300">


## Validar la implementación en Assurance

Para validar la prueba A/B en Assurance:

1. Vaya a la interfaz de usuario de Assurance.
1. Seleccionar **[!UICONTROL Configurar]** en el carril izquierdo y seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto a **[!UICONTROL Revisar y simular]** debajo **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Seleccione **[!UICONTROL Guardar]**.
1. Seleccionar **[!UICONTROL Revisar y simular]** en el carril izquierdo. Tanto la configuración del flujo de datos como la configuración del SDK se validan en la aplicación.
1. Seleccionar **[!UICONTROL Solicitudes]** en la barra superior. Ya ve su **[!UICONTROL Target]** solicitudes.
   ![Validación de AJO Decisioning](assets/assurance-decisioning-requests.png)

1. Puede explorar las pestañas Simular y Lista de eventos para obtener más funcionalidad al comprobar la configuración de las ofertas de Target.

## Pasos siguientes

Ahora debe tener todas las herramientas necesarias para empezar a añadir más pruebas A/B u otras actividades de Target (como Segmentación de experiencias o Prueba multivariable), cuando corresponda y corresponda, a la aplicación de Luma.

>[!SUCCESS]
>
>Ha habilitado la aplicación para pruebas A/B y ha mostrado los resultados de una prueba A/B con Adobe Target y la extensión Adobe Journey Optimizer - Decisioning para el SDK de Adobe Experience Platform Mobile.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Conclusión y pasos siguientes](conclusion.md)**
