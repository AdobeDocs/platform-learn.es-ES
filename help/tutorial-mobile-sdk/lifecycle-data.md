---
title: Datos del ciclo vital
description: Obtenga información sobre cómo recopilar datos del ciclo vital en una aplicación móvil.
exl-id: 75b2dbaa-2f84-4b95-83f6-2f38a4f1d438
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# Datos del ciclo vital

Obtenga información sobre cómo recopilar datos del ciclo vital en una aplicación móvil.

La extensión de ciclo vital del SDK móvil de Adobe Experience Platform habilita los datos del ciclo vital de recopilación de su aplicación móvil. La extensión de red perimetral de Adobe Experience Platform envía estos datos del ciclo vital a la red perimetral de plataforma, donde luego se reenvían a otras aplicaciones y servicios según la configuración del conjunto de datos. Obtenga más información sobre [Extensión del ciclo vital](https://aep-sdks.gitbook.io/docs/foundation-extensions/lifecycle-for-edge-network) en la documentación del producto.


## Requisitos previos

* La aplicación se ha creado y ejecutado correctamente con SDK instalados y configurados.
* Se ha importado el SDK de Assurance.

   ```swift
   import AEPAssurance
   ```

* Registrada la extensión de garantía como se describe en la sección [lección anterior](install-sdks.md).

## Objetivos de aprendizaje

En esta lección:

* Agregue el grupo de campos del ciclo vital al esquema .
* Habilite métricas del ciclo vital precisas iniciando o pausando correctamente mientras la aplicación se mueve entre primer y segundo plano.
* Envíe datos desde la aplicación a Platform Edge Network.
* Valide en Garantía.

## Agregar grupo de campos del ciclo vital al esquema

El grupo de campos Evento de experiencia del consumidor que agregó en la variable [lección anterior](create-schema.md) ya contiene los campos del ciclo vital, por lo que puede omitir este paso. Si no utiliza el grupo de campos Evento de experiencia del consumidor en su propia aplicación, puede agregar los campos del ciclo vital haciendo lo siguiente:

1. Vaya a la interfaz de esquema como se describe en la sección [lección anterior](create-schema.md).
1. Abra el esquema &quot;Aplicación Luma&quot; y seleccione **[!UICONTROL Agregar]**.
   ![seleccionar agregar](assets/mobile-lifecycle-add.png)
1. En la barra de búsqueda, introduzca &quot;ciclo vital&quot;.
1. Seleccione la casilla de verificación situada junto a **[!UICONTROL Detalles del ciclo de vida móvil de AEP]**.
1. Select **[!UICONTROL Agregar grupos de campos]**.
   ![agregar grupo de campos](assets/mobile-lifecycle-lifecycle-field-group.png)
1. Seleccione **[!UICONTROL Guardar]**.
   ![guardar](assets/mobile-lifecycle-lifecycle-save.png)


## Cambios de implementación

Ahora puede actualizar `AppDelegate.swift` para registrar los eventos de ciclo vital:

1. Cuando se inicie, si la aplicación se reanuda desde un estado en segundo plano, iOS podría llamar a su `applicationWillEnterForeground:` método delegado. Add `lifecycleStart:`

   ```swift
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. Cuando la aplicación entre en segundo plano, ponga en pausa la recopilación de datos del ciclo vital de la aplicación `applicationDidEnterBackground:` método delegado.

   ```swift
   MobileCore.lifecyclePause()
   ```

>[!NOTE]
>
>Para iOS 13 y versiones posteriores, consulte la [documentación](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle#register-lifecycle-with-mobile-core-and-add-appropriate-start-pause-calls) para código ligeramente diferente.

## Validar con Assurance

1. Consulte la [instrucciones de configuración](assurance.md) y conecte su simulador o dispositivo a Assurance.
1. Inicie la aplicación.
1. Envíe la aplicación al fondo. Comprobar `LifecyclePause`.
1. Traer la aplicación al primer plano. Comprobar `LifecycleResume`.
   ![validar ciclo vital](assets/mobile-lifecycle-lifecycle-assurance.png)


## Reenviar datos a Platform Edge Network

El ejercicio anterior distribuye los eventos en primer y segundo plano al SDK de Mobile. Para enviar estos eventos a Platform Edge Network, siga los pasos que se indican [here](https://aep-sdks.gitbook.io/docs/foundation-extensions/lifecycle-for-edge-network#configure-a-rule-to-forward-lifecycle-metrics-to-platform). Una vez que los eventos se envían a Platform Edge Network, se reenvían a otras aplicaciones y servicios según la configuración del conjunto de datos.

Una vez que haya agregado la regla para enviar los eventos de ciclo vital a Platform Edge Network, debería ver `Application Close (Background)` y `Application Launch (Foreground)` eventos que contienen datos XDM en Assurance.

![validar el ciclo de vida enviado a Platform Edge](assets/mobile-lifecycle-edge-assurance.png)



Siguiente: **[Seguimiento de eventos](events.md)**

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK de Adobe Experience Platform Mobile. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)