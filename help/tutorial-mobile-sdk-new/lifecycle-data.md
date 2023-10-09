---
title: Recopilar datos del ciclo vital
description: Obtenga información sobre cómo recopilar datos del ciclo vital en una aplicación móvil.
hide: true
exl-id: a3b26e45-2a17-4b44-aec0-fdf83526a273
source-git-commit: d7410a19e142d233a6c6597de92f112b961f5ad6
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 3%

---

# Recopilar datos del ciclo vital

Obtenga información sobre cómo recopilar datos del ciclo vital en una aplicación móvil.

La extensión Adobe Experience Platform Mobile SDK Lifecycle permite la recopilación de datos del ciclo vital desde la aplicación móvil. La extensión de red perimetral de Adobe Experience Platform envía estos datos del ciclo vital a la red perimetral de Platform, donde se reenvían a otras aplicaciones y servicios según la configuración del flujo de datos. Obtenga más información acerca de [Extensión del ciclo vital](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/) en la documentación del producto.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados. Como parte de esta lección, ya ha iniciado la supervisión del ciclo vital. Consulte [Instalación de SDK: actualizar AppDelegate](install-sdks.md#update-appdelegate) para revisar.
* Registre la extensión de Assurance como se describe en la [lección anterior](install-sdks.md).

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

<!--
* Add lifecycle field group to the schema.
* -->
* Habilite métricas precisas del ciclo vital iniciando/pausando correctamente la aplicación a medida que se mueve entre el primer y el segundo plano.
* Envíe datos de la aplicación a Platform Edge Network.
* Validar en Assurance.

<!--
## Add lifecycle field group to schema

The Consumer Experience Event field group you added in the [previous lesson](create-schema.md) already contains the lifecycle fields, so you can skip this step. If you don't use Consumer Experience Event field group in your own app, you can add the lifecycle fields by doing the following:

1. Navigate to the schema interface as described in the [previous lesson](create-schema.md).
1. Open the **Luma Mobile App Event Schema** schema and select **[!UICONTROL Add]** next to Field groups.
    ![select add](assets/lifecycle-add.png)
1. In the search bar, enter "lifecycle".
1. Select the checkbox next to **[!UICONTROL AEP Mobile Lifecycle Details]**.
1. Select **[!UICONTROL Add field groups]**.
    ![add field group](assets/lifecycle-lifecycle-field-group.png)
1. Select **[!UICONTROL Save]**.
    ![save](assets/lifecycle-lifecycle-save.png)
-->

## Cambios de implementación

Ahora puede actualizar el proyecto para registrar los eventos de ciclo vital.

1. Vaya a **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** en el navegador del proyecto Xcode.

1. Cuando se inicia, si la aplicación se reanuda desde un estado en segundo plano, iOS puede llamar a su `sceneWillEnterForeground:` método delegado y aquí es donde desea almacenar en déclencheur un evento de inicio del ciclo vital. Añadir este código a `func sceneWillEnterForeground(_ scene: UIScene)`:

   ```swift
   // When in foreground start lifecycle data collection
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. Cuando la aplicación entre en segundo plano, pausará la recopilación de datos del ciclo vital de la aplicación `sceneDidEnterBackground:` método delegado. Añadir este código a  `func sceneDidEnterBackground(_ scene: UIScene)`:

   ```swift
   // When in background pause lifecycle data collection
   MobileCore.lifecyclePause()
   ```

## Validar con Assurance

1. Revise la [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar el simulador o dispositivo a Assurance.
1. Envíe la aplicación al segundo plano. Marcar para **[!UICONTROL LifecyclePause]** en la interfaz de usuario de Assurance.
1. Traer la aplicación al primer plano. Marcar para **[!UICONTROL LifecycleResume]** en la interfaz de usuario de Assurance.
   ![validar ciclo vital](assets/lifecycle-lifecycle-assurance.png)


## Reenviar datos a Platform Edge Network

El ejercicio anterior envía los eventos en primer y segundo plano al SDK de Adobe Experience Platform Mobile. Para reenviar estos eventos a Platform Edge Network:

1. Seleccionar **[!UICONTROL Reglas]** en la propiedad Tags.
   ![Crear regla](assets/rule-create.png)
1. Seleccionar **[!UICONTROL Compilación inicial]** como la biblioteca que se va a utilizar.
1. Seleccione **[!UICONTROL Crear nueva regla]**.
   ![Crear nueva regla](assets/rules-create-new.png)
1. En el **[!UICONTROL Crear regla]** pantalla, introduzca `Application Status` para **[!UICONTROL Nombre]**.
1. Seleccionar ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir]** abajo **[!UICONTROL EVENTOS]**.
   ![Cuadro de diálogo Crear regla](assets/rule-create-name.png)
1. En el **[!UICONTROL Configuración de eventos]** paso:
   1. Seleccionar **[!UICONTROL Mobile Core]** como el **[!UICONTROL Extensión]**.
   1. Seleccionar **[!UICONTROL Primer plano]** como el **[!UICONTROL Tipo de evento]**.
   1. Seleccione **[!UICONTROL Conservar cambios]**.
      ![Configuración de eventos de regla](assets/rule-event-configuration.png)
1. De nuevo en **[!UICONTROL Crear regla]** pantalla, seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir]** junto a **[!UICONTROL Mobile Core - Primer plano]**.
   ![Configuración del siguiente evento](assets/rule-event-configuration-next.png)
1. En el **[!UICONTROL Configuración de eventos]** paso:
   1. Seleccionar **[!UICONTROL Mobile Core]** como el **[!UICONTROL Extensión]**.
   1. Seleccionar **[!UICONTROL Fondo]** como el **[!UICONTROL Tipo de evento]**.
   1. Seleccione **[!UICONTROL Conservar cambios]**.
      ![Configuración de eventos de regla](assets/rule-event-configuration-background.png)
1. De nuevo en **[!UICONTROL Crear regla]** pantalla, seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir]** debajo **[!UICONTROL ACCIONES]**.
   ![Acción de agregar regla](assets/rule-action-button.png)
1. En el **[!UICONTROL Configuración de acción]** paso:
   1. Seleccionar **[!UICONTROL Adobe Experience Edge Network]** como el **[!UICONTROL Extensión]**.
   1. Seleccionar **[!UICONTROL Reenviar evento a Edge Network]** como el **[!UICONTROL Tipo de acción]**.
   1. Seleccione **[!UICONTROL Conservar cambios]**.
      ![Configuración de acción de regla](assets/rule-action-configuration.png)
1. Seleccionar **[!UICONTROL Guardar en biblioteca]**.
   ![Regla - Guardar en biblioteca](assets/rule-save-to-library.png)
1. Seleccionar **[!UICONTROL Generar]** para reconstruir la biblioteca.
   ![Regla: compilación](assets/rule-build.png)

Una vez que haya creado la propiedad correctamente, los eventos se envían a Platform Edge Network y los eventos se reenvían a otras aplicaciones y servicios según la configuración del flujo de datos.

Debería ver **[!UICONTROL Cierre de aplicación (segundo plano)]** y **[!UICONTROL Inicio de aplicación (primer plano)]** eventos que contienen datos XDM en Assurance.

![validar ciclo de vida enviado a Platform Edge](assets/lifecycle-edge-assurance.png)

>[!SUCCESS]
>
>Ahora ha configurado la aplicación para enviar eventos de estado de aplicación (primer plano, segundo plano) a Adobe Experience Platform Edge Network y a todos los servicios definidos en la secuencia de datos.<br>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Siguiente: **[Seguimiento de datos de eventos](events.md)**
