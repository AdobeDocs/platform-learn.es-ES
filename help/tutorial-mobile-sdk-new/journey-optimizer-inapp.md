---
title: Creación y envío de mensajes en la aplicación
description: Obtenga información sobre cómo crear y enviar mensajes en la aplicación a una aplicación móvil con el SDK móvil de Platform y Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
hide: true
source-git-commit: 5f178f4bd30f78dff3243b3f5bd2f9d11c308045
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 4%

---

# Creación y envío de mensajes en la aplicación

Obtenga información sobre cómo crear mensajes en la aplicación para aplicaciones móviles con el SDK móvil de Experience Platform y Journey Optimizer.

Journey Optimizer le permite crear campañas para enviar mensajes en la aplicación a audiencias de destino. Las campañas en Journey Optimizer se utilizan para entregar contenido único a una audiencia específica mediante varios canales. Con las campañas, las acciones se realizan simultáneamente, ya sea de forma inmediata o en función de una programación especificada. Cuando utilice recorridos (consulte la [Notificaciones push de Journey Optimizer](journey-optimizer-push.md) lección), las acciones se ejecutan de forma secuencial.

![Arquitectura](assets/architecture-ajo.png)

Antes de enviar mensajes en la aplicación con Journey Optimizer, debe asegurarse de que las configuraciones y integraciones adecuadas estén implementadas. Para comprender el flujo de datos de mensajería en la aplicación en Journey Optimizer, consulte [la documentación](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>Esta lección es opcional y solo se aplica a los usuarios de Journey Optimizer que buscan enviar mensajes en la aplicación.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.
* Configure la aplicación para Adobe Experience Platform.
* Acceso a Journey Optimizer y permisos suficientes, tal como se describe [aquí](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Además, necesita permisos suficientes para las siguientes funciones de Journey Optimizer.
   * Administrar campañas.
* Cuenta de desarrollador de Apple de pago con acceso suficiente para crear certificados, identificadores y claves.
* Dispositivo o simulador físico de iOS para realizar pruebas.


## Objetivos de aprendizaje

En esta lección, debe

* Registre el ID de la aplicación con el servicio de notificaciones push de Apple (APN).
* Crear una superficie de aplicación en AJO.
* Instale y configure la extensión de etiquetas de Journey Optimizer.
* Actualice la aplicación para registrar la extensión de etiqueta de Journey Optimizer.
* Valide la configuración en Assurance.
* Defina su propia experiencia de campaña y mensaje en la aplicación en Journey Optimizer.
* Envíe su propio mensaje en la aplicación desde la aplicación.

## Configuración

>[!TIP]
>
>Si ya ha configurado su entorno como parte de la [mensajería push de Journey Optimizer](journey-optimizer-push.md) En esta lección, es posible que ya haya realizado algunos de los pasos de esta sección de configuración.


### Añadir una superficie de aplicación en la recopilación de datos

1. Desde el [Interfaz de recopilación de datos](https://experience.adobe.com/data-collection/), seleccione **[!UICONTROL Superficies de aplicación]** en el panel izquierdo.
1. Para crear una configuración, seleccione **[!UICONTROL Crear superficie de aplicación]**.
   ![inicio de superficie de aplicación](assets/push-app-surface.png)
1. Introduzca una **[!UICONTROL Nombre]** para la configuración, por ejemplo `Luma App Tutorial`  .
1. Desde **[!UICONTROL Configuración de aplicaciones móviles]**, seleccione **[!UICONTROL Apple iOS]**.
1. Introduzca el ID del paquete de la aplicación móvil en **[!UICONTROL ID de aplicación (ID de paquete de iOS)]** field. Por ejemplo,  `com.adobe.luma.tutorial.swiftui`.
1. Seleccione **[!UICONTROL Guardar]**.

   ![configuración de superficie de aplicación](assets/push-app-surface-config.png)

### Actualizar configuración de secuencia de datos

Para garantizar que los datos enviados desde su aplicación móvil a Edge Network se reenvíen a Journey Optimizer, actualice la configuración de Experience Edge

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y seleccione la secuencia de datos, por ejemplo **[!DNL Luma Mobile App]**.
1. Seleccionar ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) para **[!UICONTROL Experience Platform]** y seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar]** en el menú contextual.
1. En el **[!UICONTROL Datastreams]** > ![Carpeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) >  **[!UICONTROL Adobe Experience Platform]** pantalla, asegúrese de **[!UICONTROL Adobe Journey Optimizer]** está seleccionado. Consulte [Configuración de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) para obtener más información.
1. Para guardar la configuración de la secuencia de datos, seleccione **[!UICONTROL Guardar]**.

   ![Configuración de flujo de datos AEP](assets/datastream-aep-configuration.png)


### Instalación de la extensión Journey Optimizer tags

Para que la aplicación funcione con Journey Optimizer, debe actualizar la propiedad de etiquetas.

1. Vaya a **[!UICONTROL Etiquetas]** > **[!UICONTROL Extensiones]** > **[!UICONTROL Catálogo]**.
1. Abra la propiedad, por ejemplo **[!DNL Luma Mobile App Tutorial]**.
1. Seleccionar **[!UICONTROL Catálogo]**.
1. Busque la variable **[!UICONTROL Adobe Journey Optimizer]** extensión.
1. Instalar la extensión.
1. En el **[!UICONTROL Instalar extensión]** diálogo
   1. Seleccione un entorno, por ejemplo **[!UICONTROL Desarrollo]**.
   1. Seleccione el **[!UICONTROL Conjunto de datos de evento de experiencia de seguimiento push AJO]** conjunto de datos del **[!UICONTROL Conjunto de datos de evento]** lista.
   1. Seleccionar **[!UICONTROL Guardar en biblioteca y crear]**.
      ![Configuración de extensión de AJO](assets/push-tags-ajo.png)

>[!NOTE]
>
>Si no lo ve... `AJO Push Tracking Experience Event Dataset` como opción, póngase en contacto con el servicio de atención al cliente.
>

### Implementar Journey Optimizer en la aplicación

Como se ha explicado en lecciones anteriores, la instalación de una extensión de etiqueta móvil solo proporciona la configuración. A continuación, debe instalar y registrar el SDK de mensajería. Si estos pasos no están claros, revise la [Instalación de SDK](install-sdks.md) sección.

>[!NOTE]
>
>Si ha completado la [Instalación de SDK](install-sdks.md) , el SDK ya está instalado y puede omitir este paso.
>

1. En Xcode, asegúrese de que [Mensajería AEP](https://github.com/adobe/aepsdk-messaging-ios.git) se añade a la lista de paquetes en Dependencias del paquete. Consulte [Administrador De Paquetes Swift](install-sdks.md#swift-package-manager).
1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** en el navegador del proyecto Xcode.
1. Asegurar `AEPMessaging` forma parte de su lista de importaciones.

   `import AEPMessaging`

1. Asegurar `Messaging.self` forma parte de la matriz de extensiones que está registrando.

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


## Validar la configuración con Assurance

1. Revise la [instrucciones de configuración](assurance.md) sección.
1. Instale la aplicación en su dispositivo físico o en el simulador.
1. Inicie la aplicación mediante la URL generada por Assurance.
1. En la IU de Assurance, seleccione **[!UICONTROL Configurar]**.
   ![configurar clic](assets/push-validate-config.png)
1. Seleccione el ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) botón situado junto a **[!UICONTROL Mensajería en la aplicación]**.
1. Seleccione **[!UICONTROL Guardar]**.
   ![guardar](assets/assurance-in-app-config.png)
1. Seleccionar **[!UICONTROL Mensajería en la aplicación]** en el panel de navegación izquierdo.
1. Seleccione el **[!UICONTROL Validación]** pestaña. Confirme que no está recibiendo ningún error.

   ![Validación en la aplicación](assets/assurance-in-app-validate.png)


## Cree su propio mensaje en la aplicación

Para crear su propio mensaje en la aplicación, debe definir una campaña en Journey Optimizer que almacene en déclencheur un mensaje en la aplicación en función de los eventos que se produzcan. Estos eventos pueden ser:

* datos enviados a Adobe Experience Platform,
* eventos de seguimiento principales, como la acción o el estado o la recopilación de datos PII, a través de las API genéricas principales de Mobile,
* eventos del ciclo vital de la aplicación, como inicio, instalación, actualización, cierre o bloqueo,
* eventos de geolocalización, como entrar o salir de un punto de interés.

En este tutorial, va a utilizar las API principales genéricas e independientes de la extensión de Mobile (consulte [API genéricas principales de Mobile](https://developer.adobe.com/client-sdks/documentation/mobile-core/#mobile-core-generic-apis)) para facilitar el seguimiento de eventos de pantallas de usuario, acciones y datos PII. Los eventos generados por estas API se publican en el centro de eventos del SDK y las extensiones los pueden utilizar. El centro de eventos del SDK proporciona la estructura de datos principal vinculada a todas las extensiones del SDK móvil de AEP, y mantiene una lista de extensiones registradas y módulos internos, una lista de detectores de eventos registrados y una base de datos de estado compartido.
El centro de eventos del SDK publica y recibe datos de eventos de extensiones registradas para simplificar las integraciones con soluciones de Adobe y de terceros. Por ejemplo, cuando se instala la extensión Optimize, todas las solicitudes e interacciones con el motor de ofertas de Journey Optimizer - Gestión de decisiones se gestionan mediante el centro de eventos.

1. En la IU de Journey Optimizer, seleccione **[!UICONTROL Campañas]** desde el carril izquierdo.
1. Seleccionar **[!UICONTROL Crear campaña]**.
1. En el **[!UICONTROL Crear campaña]** pantalla:
   1. Seleccionar **[!UICONTROL Mensaje en la aplicación]** y seleccione una superficie de aplicación de la **[!UICONTROL Superficie de aplicación]** , por ejemplo **[!DNL Luma Mobile App]**.
   1. Seleccione **[!UICONTROL Crear]**
      ![Propiedades de campaña](assets/ajo-campaign-properties.png)
1. En la pantalla Campaign definition, en **[!UICONTROL Propiedades]**, introduzca un **[!UICONTROL Nombre]** para la campaña, por ejemplo `Luma - In-App Messaging Campaign`, y a **[!UICONTROL Descripción]**, por ejemplo `In-app messaging campaign for Luma app`.
   ![Nombre de la campaña](assets/ajo-campaign-properties-name.png)
1. Desplácese hacia abajo hasta **[!UICONTROL Acción]** y seleccione **[!UICONTROL Editar contenido]**.
1. En el **[!UICONTROL Mensaje en la aplicación]** pantalla:
   1. Seleccionar **[!UICONTROL Modal]** como el **[!UICONTROL Diseño del mensaje]**.
   2. Entrar `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` para el **[!UICONTROL URL de medios]**.
   3. Introduzca una **[!UICONTROL Header]**, por ejemplo `Welcome to this Luma In-App Message` e introduzca un **[!UICONTROL Cuerpo]**, por ejemplo `Triggered by pushing that button in the app...`.
   4. Entrar **[!UICONTROL Descartar]** como el **[!UICONTROL Texto de #1 de botón (principal)]**.
   5. Observe cómo se actualiza la vista previa.
   6. Seleccionar **[!UICONTROL Revisar para activar]**.
      ![Editor en la aplicación](assets/ajo-in-app-editor.png)
1. En el **[!UICONTROL Revise para activar (Luma, campaña de mensajería en la aplicación)]** pantalla, seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) en el **[!UICONTROL Programación]** mosaico.
   ![Revisar programación seleccionar Programación](assets/ajo-review-select-schedule.png)
1. De nuevo en **[!DNL Luma - In-App Messaging Campaign]** pantalla, seleccione ![Editar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Editar déclencheur]**.
1. En el **[!UICONTROL Déclencheur de mensajes en la aplicación]** , configure los detalles de la acción de seguimiento que almacena en déclencheur el mensaje en la aplicación:
   1. Para eliminar **[!UICONTROL Evento de inicio de aplicación]**, seleccione ![Cerrar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) .
   1. Uso ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir condición]** repetidamente para generar la siguiente lógica para **[!UICONTROL Mostrar mensaje si]**.
   1. Haga clic en **[!UICONTROL Finalizado]**.
      ![lógica de déclencheur](assets/ajo-trigger-logic.png)

   Ha definido una acción de seguimiento, donde la variable **[!UICONTROL Acción]** igual a `in-app` y el **[!UICONTROL Datos de contexto]** con la acción es un par de valor clave de `"showMessage" : "true"`.

1. De nuevo en **[!DNL Luma - In-App Messaging Campaign]** pantalla, seleccione **[!UICONTROL Revisar para activar]**.
1. En el **[!UICONTROL Revise para activar (Luma, campaña de mensajería en la aplicación)]** pantalla, seleccione **[!UICONTROL Activar]**.
1. Ya ve su **[!DNL Luma - In-App Messaging Campaign]** con estado **[!UICONTROL Activo]** en el **[!UICONTROL Campañas]** lista.
   ![Lista de campañas](assets/ajo-campaign-list.png)


## Déclencheur del mensaje en la aplicación

Dispone de todos los ingredientes para enviar un mensaje en la aplicación. Lo que queda es cómo almacenar en déclencheur este mensaje en la aplicación.

1. Ir a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** en el navegador del proyecto Xcode. Busque el `func sendTrackAction(action: String, data: [String: Any]?)` y agregue el siguiente código, que llama a la función [`MobileCore.track`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) función, según los parámetros `action` y `data`.


   ```swift
   // Send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Ir a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]** en el Navegador de proyectos Xcode. Busque el código del botón Mensaje en la aplicación y añada el siguiente código:

   ```swift
   // Setting parameters and calling function to send in-app message
   Task {
       AEPService.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

## Validar con la aplicación

1. Abra la aplicación en un dispositivo o en el simulador.

1. Vaya a la **[!UICONTROL Configuración]** pestaña.

1. Tocar **[!UICONTROL Mensaje en la aplicación]**. Verá que el mensaje en la aplicación aparece en la aplicación.

   <img src="assets/ajo-in-app-message.png" width="300" />


## Validar la implementación en Assurance

Puede validar los mensajes en la aplicación en la interfaz de usuario de Assurance.

1. Seleccionar **[!UICONTROL Mensajería en la aplicación]**.
1. Seleccionar **[!UICONTROL Lista de eventos]**.
1. Seleccione una **[!UICONTROL Mostrar mensaje]** entrada.
1. Inspect el evento sin procesar, especialmente el `html`, que contiene el diseño completo y el contenido del mensaje en la aplicación.
   ![Mensaje en la aplicación de Assurance](assets/assurance-in-app-display-message.png)


## Pasos siguientes

Ahora debe tener todas las herramientas para empezar a añadir mensajes en la aplicación, cuando corresponda.  Por ejemplo, promocionar productos en función de interacciones específicas que esté rastreando en la aplicación.

>[!SUCCESS]
>
>Ha habilitado la aplicación para mensajería en la aplicación y ha agregado una campaña de mensajería en la aplicación mediante Journey Optimizer y la extensión de Journey Optimizer para el SDK de Experience Platform Mobile.<br/>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Creación y visualización de ofertas](journey-optimizer-offers.md)**
