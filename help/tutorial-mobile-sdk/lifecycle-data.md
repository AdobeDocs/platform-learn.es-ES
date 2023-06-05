---
title: Datos del ciclo vital
description: Obtenga información sobre cómo recopilar datos del ciclo vital en una aplicación móvil.
exl-id: 75b2dbaa-2f84-4b95-83f6-2f38a4f1d438
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 2%

---

# Datos del ciclo vital

Obtenga información sobre cómo recopilar datos del ciclo vital en una aplicación móvil.

La extensión Adobe Experience Platform Mobile SDK Lifecycle permite la recopilación de datos del ciclo vital desde la aplicación móvil. La extensión de red perimetral de Adobe Experience Platform envía estos datos del ciclo vital a la red perimetral de Platform, donde se reenvían a otras aplicaciones y servicios según la configuración del flujo de datos. Obtenga más información acerca de [Extensión del ciclo vital](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/) en la documentación del producto.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con los SDK instalados y configurados.
* Se ha importado el SDK de Assurance.

   ```swift
   import AEPAssurance
   ```

* Registre la extensión de Assurance como se describe en la [lección anterior](install-sdks.md).

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Agregue el grupo de campos del ciclo vital al esquema.
* Habilite métricas precisas del ciclo vital iniciando/pausando correctamente la aplicación a medida que se mueve entre el primer y el segundo plano.
* Envíe datos de la aplicación a Platform Edge Network.
* Validar en Assurance.

## Agregar un grupo de campos de ciclo vital al esquema

El grupo de campos Evento de experiencia del consumidor que agregó en la [lección anterior](create-schema.md) ya contiene los campos del ciclo vital, por lo que puede omitir este paso. Si no utiliza el grupo de campos Evento de experiencia del consumidor en su propia aplicación, puede agregar los campos de ciclo vital de la siguiente manera:

1. Vaya a la interfaz de esquema como se describe en la [lección anterior](create-schema.md).
1. Abra el esquema &quot;Aplicación de Luma&quot; y seleccione **[!UICONTROL Añadir]**.
   ![seleccione añadir](assets/mobile-lifecycle-add.png)
1. En la barra de búsqueda, introduzca &quot;ciclo vital&quot;.
1. Seleccione la casilla que hay junto a **[!UICONTROL Detalles del ciclo de vida móvil AEP]**.
1. Seleccione **[!UICONTROL Agregar grupos de campos]**.
   ![añadir grupo de campos](assets/mobile-lifecycle-lifecycle-field-group.png)
1. Seleccione **[!UICONTROL Guardar]**.
   ![guardar](assets/mobile-lifecycle-lifecycle-save.png)


## Cambios de implementación

Ahora puede actualizar `AppDelegate.swift` para registrar los eventos de ciclo vital:

1. Cuando se inicia, si la aplicación se reanuda desde un estado en segundo plano, iOS puede llamar a su `applicationWillEnterForeground:` método delegado. Add `lifecycleStart:`

   ```swift
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. Cuando la aplicación entre en segundo plano, ponga en pausa la recopilación de datos del ciclo vital desde el `applicationDidEnterBackground:` método delegado.

   ```swift
   MobileCore.lifecyclePause()
   ```

>[!NOTE]
>
>Para iOS 13 y versiones posteriores, consulte la [documentación](https://developer.adobe.com/client-sdks/documentation/mobile-core/lifecycle/#register-lifecycle-with-mobile-core-and-add-appropriate-startpause-calls) para un código ligeramente diferente.

## Validar con Assurance

1. Revise la [instrucciones de configuración](assurance.md) y conecte el simulador o dispositivo a Assurance.
1. Inicie la aplicación.
1. Envíe la aplicación al segundo plano. Marcar para `LifecyclePause`.
1. Traer la aplicación al primer plano. Marcar para `LifecycleResume`.
   ![validar ciclo vital](assets/mobile-lifecycle-lifecycle-assurance.png)


## Reenviar datos a Platform Edge Network

El ejercicio anterior envía los eventos en primer y segundo plano al SDK de Mobile. Para enviar estos eventos a Platform Edge Network, siga los pasos que se indican [aquí](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/#configure-a-rule-to-forward-lifecycle-metrics-to-platform). Una vez que los eventos se envían a Platform Edge Network, se reenvían a otras aplicaciones y servicios según la configuración del conjunto de datos.

Una vez añadida la regla para enviar los eventos de ciclo de vida a Platform Edge Network, debería ver lo siguiente `Application Close (Background)` y `Application Launch (Foreground)` eventos que contienen datos XDM en Assurance.

![validar ciclo de vida enviado a Platform Edge](assets/mobile-lifecycle-edge-assurance.png)



Siguiente: **[Seguimiento de eventos](events.md)**

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)