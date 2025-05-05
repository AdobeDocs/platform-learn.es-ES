---
title: Recopilación de datos del ciclo vital con el SDK de Platform Mobile
description: Obtenga información sobre cómo recopilar datos del ciclo vital en una aplicación móvil.
jira: KT-14630
exl-id: 75b2dbaa-2f84-4b95-83f6-2f38a4f1d438
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 2%

---

# Recopilar datos del ciclo vital

Obtenga información sobre cómo recopilar datos del ciclo vital en una aplicación móvil.

La extensión Adobe Experience Platform Mobile SDK Lifecycle permite la recopilación de datos del ciclo vital desde la aplicación móvil. La extensión de Edge Network de Adobe Experience Platform envía estos datos del ciclo vital al Edge Network de Platform, donde se reenvían a otras aplicaciones y servicios según la configuración del flujo de datos. Obtenga más información acerca de la [extensión del ciclo vital](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/) en la documentación del producto.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados. Como parte de esta lección, ya ha iniciado la supervisión del ciclo vital. Consulte [Instalar SDK: actualizar AppDelegate](install-sdks.md#update-appdelegate) para revisarlos.
* Registró la extensión de Assurance como se describe en la [lección anterior](install-sdks.md).

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

<!--
* Add lifecycle field group to the schema.
* -->
* Habilite métricas precisas del ciclo vital iniciando/pausando correctamente la aplicación a medida que se mueve entre el primer y el segundo plano.
* Envíe datos de la aplicación al Edge Network de Platform.
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

1. Cuando se inicia, si la aplicación se reanuda desde un estado en segundo plano, iOS podría llamar al método delegado `sceneWillEnterForeground:` y aquí es donde desea almacenar en déclencheur un evento de inicio del ciclo vital. Agregar este código a `func sceneWillEnterForeground(_ scene: UIScene)`:

   ```swift
   // When in foreground start lifecycle data collection
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. Cuando la aplicación entre en segundo plano, deberá pausar la recopilación de datos del ciclo vital desde el método delegado `sceneDidEnterBackground:` de la aplicación. Agregar este código a `func sceneDidEnterBackground(_ scene: UIScene)`:

   ```swift
   // When in background pause lifecycle data collection
   MobileCore.lifecyclePause()
   ```

## Validar con Assurance

1. Revise la sección [instrucciones de configuración](assurance.md#connecting-to-a-session) para conectar su simulador o dispositivo a Assurance.
1. Envíe la aplicación al segundo plano. Compruebe si hay **[!UICONTROL eventos LifecyclePause]** en la interfaz de usuario de Assurance.
1. Traer la aplicación al primer plano. Compruebe si hay **[!UICONTROL eventos LifecycleResume]** en la interfaz de usuario de Assurance.
   ![validar ciclo de vida](assets/lifecycle-lifecycle-assurance.png)


## Reenviar datos al Edge Network de Platform

El ejercicio anterior envía los eventos en primer y segundo plano al SDK de Adobe Experience Platform Mobile. Para reenviar estos eventos al Edge Network de Platform:

1. Seleccione **[!UICONTROL Reglas]** en la propiedad Etiquetas.
   ![Crear regla](assets/rule-create.png)
1. Seleccione **[!UICONTROL Versión inicial]** como la biblioteca que se va a usar.
1. Seleccione **[!UICONTROL Crear nueva regla]**.
   ![Crear nueva regla](assets/rules-create-new.png)
1. En la pantalla **[!UICONTROL Crear regla]**, escriba `Application Status` para **[!UICONTROL Nombre]**.
1. Seleccione ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Agregar]** por debajo de **[!UICONTROL EVENTOS]**.
   ![Cuadro de diálogo Crear regla](assets/rule-create-name.png)
1. En el paso **[!UICONTROL Configuración de eventos]**:
   1. Seleccione **[!UICONTROL Mobile Core]** como la **[!UICONTROL extensión]**.
   1. Seleccione **[!UICONTROL Primer plano]** como **[!UICONTROL Tipo de evento]**.
   1. Seleccione **[!UICONTROL Conservar cambios]**.

      ![Configuración de evento de regla](assets/rule-event-configuration.png)
1. En la pantalla **[!UICONTROL Crear regla]**, selecciona ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Agregar]** junto a **[!UICONTROL Núcleo móvil - Primer plano]**.
   ![Siguiente configuración de evento](assets/rule-event-configuration-next.png)
1. En el paso **[!UICONTROL Configuración de eventos]**:
   1. Seleccione **[!UICONTROL Mobile Core]** como la **[!UICONTROL extensión]**.
   1. Seleccione **[!UICONTROL Fondo]** como **[!UICONTROL Tipo de evento]**.
   1. Seleccione **[!UICONTROL Conservar cambios]**.

      ![Configuración de evento de regla](assets/rule-event-configuration-background.png)
1. En la pantalla **[!UICONTROL Crear regla]**, seleccione ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Agregar]** debajo de **[!UICONTROL ACCIONES]**.
   ![Acción de adición de regla](assets/rule-action-button.png)
1. En el paso **[!UICONTROL Configuración de la acción]**:
   1. Seleccione **[!UICONTROL Edge Network de experiencia de Adobe]** como **[!UICONTROL extensión]**.
   1. Seleccione **[!UICONTROL Reenviar evento al Edge Network]** como **[!UICONTROL Tipo de acción]**.
   1. Seleccione **[!UICONTROL Conservar cambios]**.

      ![Configuración de acción de regla](assets/rule-action-configuration.png)
1. Seleccione **[!UICONTROL Guardar en biblioteca]**.
   ![Regla - Guardar en biblioteca](assets/rule-save-to-library.png)
1. Seleccione **[!UICONTROL Build]** para reconstruir la biblioteca.
   ![Regla - Compilación](assets/rule-build.png)

Una vez que haya creado la propiedad correctamente, los eventos se envían al Edge Network de Platform y los eventos se reenvían a otras aplicaciones y servicios según la configuración del conjunto de datos.

Debería ver los eventos **[!UICONTROL Application Close (Background)]** y **[!UICONTROL Application Launch (Foreground)]** que contienen datos XDM en Assurance.

![validar ciclo de vida enviado a Platform Edge](assets/lifecycle-edge-assurance.png)

>[!SUCCESS]
>
>Ahora ha configurado la aplicación para enviar eventos de estado de aplicación (primer plano, segundo plano) al Edge Network de Adobe Experience Platform y a todos los servicios definidos en la secuencia de datos.
>
> Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=es)

Siguiente: **[Rastrear datos de eventos](events.md)**
