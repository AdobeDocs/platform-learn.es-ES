---
title: Validación de implementaciones de Web SDK con Experience Platform Assurance
description: Obtenga información sobre cómo validar la implementación de SDK web de Platform con Adobe Experience Platform Assurance. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK,Tags,Assurance
jira: KT-15406
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: da65f13f95a6d1258655e8eebc76cf024221a610
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 5%

---

# Validación de implementaciones de Web SDK con Experience Platform Assurance

[Adobe Experience Platform Assurance](https://experienceleague.adobe.com/es/docs/experience-platform/assurance/home) es una característica que te ayudará a inspeccionar, probar, simular y validar la forma en que recopilas datos o sirves experiencias.

Como aprendió en la lección [Configuración de un conjunto de datos](configure-datastream.md), Platform Web SDK envía primero datos de su propiedad digital a Platform Edge Network. A continuación, Platform Edge Network reenvía los datos a los servicios habilitados en el conjunto de datos. Puede validar las solicitudes que entran y salen de Platform Edge Network mediante Assurance.

![Diagrama de validación de Web SDK y Adobe Experience Platform](assets/dc-websdk-validation.png)


## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Iniciar una sesión de Assurance
* Ver solicitudes enviadas a y desde Platform Edge Network

## Requisitos previos

Está familiarizado con las etiquetas de recopilación de datos y con el [sitio web de demostración de Luma](https://luma.enablementadobe.com){target="_blank"}, y ha completado las lecciones anteriores en el tutorial:

* [Configuración de un esquema XDM](configure-schemas.md)
* [Configuración de un área de nombres de identidad](configure-identities.md)
* [Configuración de una secuencia de datos](configure-datastream.md)
* [Extensión web SDK instalada en la propiedad tag](install-web-sdk.md)
* [Creación de elementos de datos](create-data-elements.md)
* [Captura de identidades](create-identities.md)
* [Creación de una regla de etiqueta](create-tag-rule.md)
* [Validar con Debugger](validate-with-debugger.md)


## Inicio y visualización de una sesión de Assurance

Existen varias formas de iniciar una sesión de Assurance.


### Habilitar Edge Trace en Debugger

Para habilitar el seguimiento de Edge:

1. Vaya al sitio web de demostración de [Luma](https://luma.enablementadobe.com) y use el depurador para [cambiar la propiedad de etiquetas del sitio a su propia propiedad de desarrollo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Asegúrese de haber iniciado sesión en Debugger y de que se haya mostrado el nombre de su organización. Si se muestra su nombre de usuario en su lugar, cierre la sesión e intente volver a iniciarla.
1. En la navegación izquierda de **[!UICONTROL Experience Platform Debugger]**, seleccione **[!UICONTROL Registros]**
1. Seleccione la ficha **[!UICONTROL Edge]** y seleccione **[!UICONTROL Conectar]**

   ![Conectar el seguimiento de Edge](assets/assurance-edgeTrace-connect.png)

1. Está vacío por ahora

   ![Seguimiento de Edge conectado](assets/analytics-debugger-edge-connected.png)

1. Actualice la [página principal de Luma](https://luma.enablementadobe.com/) y vuelva a comprobar **[!UICONTROL Experience Platform Debugger]** para ver cómo llegan los datos a Platform Edge Network. En futuras lecciones, podrá ver las solicitudes salientes a medida que habilite servicios en su conjunto de datos.

   ![Solicitudes en el seguimiento de Edge](assets/validate-edge-trace.png)

   Cada vez que se activa el seguimiento de Edge en Adobe Experience Platform Debugger, se inicia una sesión de Assurance en segundo plano. Aunque puede revisar la información aquí, probablemente la interfaz de Assurance le resulte mucho más útil.

1. Con el seguimiento de Edge habilitado, puede ver un icono de vínculo de salida en la parte superior. Seleccione el icono para abrir Assurance.

   ![Iniciar sesión de Assurance](assets/validate-debugger-start-assurnance.png)

1. Se abre una nueva pestaña del explorador con la interfaz de Assurance.

### Iniciar una sesión de Assurance desde la interfaz de Assurance

1. Abrir la [interfaz de recopilación de datos](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. Seleccione Assurance en el panel de navegación izquierdo
1. Seleccione Crear sesión
   ![Crear una sesión de Assurance](assets/assurance-create-session.png)
1. Use la opción **[!UICONTROL Conexión de vínculo profundo]**
1. Seleccionar **[!UICONTROL Inicio]**
1. Asigne un nombre a la sesión, por ejemplo, `Luma Web SDK validation`
1. Como **[!UICONTROL URL base]**, escriba `https://luma.enablementadobe.com/`
   ![Asigne un nombre a la sesión de Assurance](assets/assurance-name-session.png)
1. En la pantalla siguiente, seleccione **[!UICONTROL Copiar vínculo]**
1. Seleccione el icono para copiar el vínculo en el portapapeles.
1. Pegue la dirección URL en el explorador, que abrirá el sitio web de Luma con un parámetro de URL especial `adb_validation_sessionid` e iniciará la sesión
1. En la interfaz de Assurance, debería ver un mensaje que indica que se ha conectado correctamente a la sesión y que debe ver los eventos capturados en la interfaz de Assurance.
   ![La sesión de Assurance se ha conectado](assets/assurance-success.png)

## Validar el estado actual de la implementación de Web SDK.

Hay información limitada para ver en esta fase de la implementación, ya que aún no hemos habilitado ningún servicio en el conjunto de datos.

### Ver solicitudes entrantes de Web SDK con `Alloy Request`

Podemos ver la visita entrante desde Web SDK tal y como la recibe Edge:

1. Seleccionar la fila `Alloy Request`
1. Busque en Evento sin procesar (o expanda nodos en la [!UICONTROL carga útil] > `ACPExtensionEventData`) hasta que encuentre su objeto XDM con variables familiares:

   ![Solicitud de aleación](assets/assurance-alloy-request.png)


### Ver la respuesta en `Alloy Response Handle`

Como ya sabe, el Experience Cloud ID (ECID) es visible en la respuesta de Web SDK después de generarse en Platform Edge Network. Vamos a buscarlo en la respuesta, tal como se ve en Assurance:

1. Filtre y seleccione la fila con el evento denominado `Alloy Response Handle`.
1. A la derecha aparece un menú. Seleccionar el signo `+` junto a `[!UICONTROL ACPExtensionEventData]`
1. Explorar en profundidad seleccionando `[!UICONTROL payload > 0 > payload > 0 > namespace]`. El identificador mostrado bajo los últimos `0` corresponde a `ECID`. Lo sabe por el valor que aparece en `namespace` que coincide con `ECID`

   ![Respuesta de Assurance Alloy](assets/assurance-alloy-response.png)

   >[!CAUTION]
   >
   >Es posible que vea un valor ECID truncado debido al ancho de la ventana. Simplemente, seleccione la barra de control en la interfaz y arrastre a la izquierda para ver todo el ECID.

En lecciones futuras, utilice Assurance para validar cargas útiles completamente procesadas que lleguen a una aplicación de Adobe habilitada en su conjunto de datos.

Ahora que un objeto XDM se activa en una página y con los conocimientos necesarios para validar la recopilación de datos, ya puede configurar Experience Platform y las aplicaciones de Adobe individuales mediante Platform Web SDK.

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Web SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848)
