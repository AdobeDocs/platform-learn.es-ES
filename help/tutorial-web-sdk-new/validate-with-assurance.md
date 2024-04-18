---
title: Validación de implementaciones de SDK web con Experience Platform Assurance
description: Obtenga información sobre cómo validar la implementación del SDK web de Platform con Adobe Experience Platform Assurance. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK,Tags,Assurance
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: fe8b92c560c9676a44935005cc558388244d6aea
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 2%

---

# Validación de implementaciones de SDK web con Experience Platform Assurance

Adobe Experience Platform Assurance es un producto de Adobe Experience Cloud que le ayuda a inspeccionar, probar, simular y validar cómo recopilar datos o servir experiencias. Más información sobre [Garantía de Adobe](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).


## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Iniciar una sesión de Assurance
* Ver solicitudes enviadas a y desde Platform Edge Network

## Requisitos previos

Está familiarizado con las etiquetas de recopilación de datos y las [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} y haya completado las lecciones anteriores en el tutorial:

* [Configuración de un esquema XDM](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)
* [Configuración de una secuencia de datos](configure-datastream.md)
* [Extensión del SDK web instalada en la propiedad de etiqueta](install-web-sdk.md)
* [Creación de elementos de datos](create-data-elements.md)
* [Creación de identidades](create-identities.md)
* [Creación de una regla de etiqueta](create-tag-rule.md)
* [Validar con Debugger](validate-with-debugger.md)


## Inicio y visualización de una sesión de Assurance

Existen varias formas de iniciar una sesión de Assurance.

### Iniciar una sesión de Assurance en Debugger

Cada vez que se habilita el seguimiento de Edge en Adobe Experience Platform Debugger, se inicia una sesión de Assurance en segundo plano.

Consulte cómo hemos realizado esto en la lección de Debugger:

1. Vaya a la [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html) y use el depurador para [cambie la propiedad de etiquetas del sitio a su propia propiedad de desarrollo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. En la navegación izquierda de **[!UICONTROL Experience Platform Debugger]** select **[!UICONTROL Registros]**
1. Seleccione el **[!UICONTROL Edge]** y seleccione. **[!UICONTROL Connect]**

   ![Conectar seguimiento de Edge](assets/analytics-debugger-edgeTrace.png)
1. Con el seguimiento de Edge habilitado, puede ver un icono de vínculo de salida en la parte superior. Seleccione el icono para abrir Assurance. Se abre una nueva pestaña en el explorador.

   ![Iniciar sesión de Assurance](assets/validate-debugger-start-assurnance.png)


### Iniciar una sesión de Assurance desde la interfaz de Assurance

1. Abra el [Interfaz de recopilación de datos](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. Seleccione Assurance en el panel de navegación izquierdo
1. Seleccione Crear sesión
   ![Crear una sesión de Assurance](assets/assurance-create-session.png)
1. Seleccione Inicio
1. Asigne un nombre a la sesión, por ejemplo, `Luma Web SDK validation`
1. Como el **[!UICONTROL URL básica]** introduzcan `https://luma.enablementadobe.com/`
   ![Asignar un nombre a la sesión de Assurance](assets/assurance-name-session.png)
1. En la pantalla siguiente, seleccione **[!UICONTROL Copiar vínculo]**
1. Seleccione el icono para copiar el vínculo en el portapapeles.
1. Pegue la dirección URL en el explorador, que abrirá el sitio web de Luma con un parámetro de URL especial. `adb_validation_sessionid` e iniciar la sesión
1. En la interfaz de Assurance, debería ver un mensaje que indique que se ha conectado correctamente a la sesión y que debería ver los eventos capturados en la interfaz de Assurance.
   ![La sesión de Assurance se ha conectado](assets/assurance-success.png)

## Validar el estado actual de la implementación del SDK web.

Hay información limitada para ver en esta fase de la implementación. Un valor que podemos ver es su ID de Experience Cloud (ECID) que se genera en el Edge Network de Platform:

1. Seleccione la fila con el evento llamado Controlador de respuesta de Adobe.
1. A la derecha aparece un menú. Seleccione el `+` firmar junto a `[!UICONTROL ACPExtensionEvent]`
1. Explorar en profundidad seleccionando `[!UICONTROL payload > 0 > payload > 0 > namespace]`. El ID mostrado en la última `0` corresponde al `ECID`. Lo sabe por el valor que aparece debajo de `namespace` concordancia `ECID`

   ![Validación de ECID de Assurance](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Es posible que vea un valor ECID truncado debido al ancho de la ventana. Simplemente, seleccione la barra de control en la interfaz y arrastre a la izquierda para ver todo el ECID.

En lecciones futuras, utilice Assurance para validar cargas útiles completamente procesadas que lleguen a una aplicación de Adobe habilitada en el conjunto de datos.

Ahora que un objeto XDM se activa en una página y con los conocimientos necesarios para validar la recopilación de datos, ya puede configurar las aplicaciones de Adobe individuales mediante el SDK web de Platform.

[Siguiente: ](setup-experience-platform.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
