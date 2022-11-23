---
title: Creación de un esquema XDM para datos web
description: Aprenda a crear un esquema XDM para datos web en la interfaz de recopilación de datos. Esta lección forma parte del tutorial Implementar Adobe Experience Cloud con SDK web .
feature: Schemas
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: f493b0d53bba223f78683551a1a43e25bf43ee8d
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 5%

---

# Creación de un esquema XDM para datos web

Aprenda a crear un esquema XDM para datos web en la interfaz de recopilación de datos.

Los esquemas del Modelo de datos de experiencia (XDM) son los componentes básicos, los principios y las prácticas recomendadas para componer esquemas en Adobe Experience Platform.

El SDK web de Platform utiliza su esquema para estandarizar los datos de eventos web, enviarlos a la red perimetral de plataforma y, en última instancia, reenviar los datos a cualquier aplicación Experience Cloud configurada en el conjunto de datos. Este paso es fundamental, ya que define un modelo de datos estándar necesario para la ingesta de datos de experiencia del cliente en el Experience Platform y permite servicios y aplicaciones descendentes basados en estos estándares.

>[!NOTE]
>
> Con fines de demostración, los ejercicios de esta lección crean un esquema de ejemplo para capturar el contenido visualizado y los productos comprados por los clientes en la variable [Luma Demo Site](https://luma.enablementadobe.com/content/luma/us/en.html). Aunque puede utilizar estos pasos para crear un esquema diferente para sus propios fines, se recomienda que primero siga con la creación del esquema de ejemplo para conocer las capacidades del editor de esquemas.

Para obtener más información sobre los esquemas XDM, siga el curso &quot;[Modelar los datos de la experiencia del cliente con XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)&quot; o consulte la [Información general del sistema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es).

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Crear un esquema XDM desde la interfaz de recopilación de datos
* Añadir grupos de campos al esquema XDM
* Creación de esquemas XDM para datos de eventos web mediante prácticas recomendadas

## Requisitos previos

Todos los permisos de usuario y aprovisionamiento necesarios para la recopilación de datos y Adobe Experience Platform se describen en la sección [Configuración de permisos](configure-permissions.md) lección.

## Creación de un esquema XDM

Los esquemas XDM son la forma estándar de describir los datos en Experience Platform, lo que permite que todos los datos que se ajustan a los esquemas se reutilicen en una organización sin conflictos, o incluso se compartan entre varias organizaciones. Para obtener más información, consulte la [conceptos básicos de la composición del esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es).

En este ejercicio, creará un esquema XDM utilizando los grupos de campos de línea de base recomendados para capturar datos de eventos web en la variable [Luma Demo Site](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;}:

1. Abra el [Interfaz de recopilación de datos](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. Asegúrese de que está en el simulador de pruebas correcto

   >[!NOTE]
   >
   >Si es cliente de una aplicación basada en Platform como CDP en tiempo real, recomendamos utilizar un entorno limitado de desarrollo para este tutorial.

1. Vaya a **[!UICONTROL Esquemas]** en la navegación izquierda
1. Seleccione el **[!UICONTROL Crear esquema]** en la parte superior derecha
1. En el menú desplegable, seleccione **[!UICONTROL XDM ExperienceEvent]**

![Evento de experiencia de esquema](assets/schema-XDM-experience-event.jpg)

## Agregar grupos de campos

Como se ha señalado anteriormente, XDM es el marco principal que estandariza los datos de experiencia del cliente proporcionando estructuras y definiciones comunes para su uso en los servicios descendentes de Adobe Experience Platform. Aplicando las normas XDM, _todos los datos de experiencia del cliente_ puede incorporarse a una representación común. Este método le permite obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de los clientes a través de segmentos y expresar atributos del cliente para fines de personalización mediante el uso de datos de varias fuentes. Consulte [Prácticas recomendadas para el modelado de datos](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/best-practices.html?lang=en) para obtener más información.

Cuando sea posible, se recomienda utilizar grupos de campos existentes y adherirse a un modelo independiente del producto y a las convenciones de nomenclatura. Para cualquier dato específico de su organización que no se ajuste a los grupos de campos predefinidos anteriores, puede crear un grupo de campos personalizados. Consulte [Creación de un esquema mediante el Editor de esquemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#create) para ver los pasos más detallados sobre esquemas personalizados.

>[!TIP]
> 
>En este ejercicio, se agregan los grupos de campos predefinidos recomendados para la recopilación de datos web: _**[!UICONTROL Mezcla de ExperienceEvent del SDK web de AEP]**_ y _**[!UICONTROL Evento de experiencia del consumidor]**_.

1. Keep **[!UICONTROL Usar grupo de campos existente]** botón de radio seleccionado
1. Buscar [!UICONTROL `AEP Web SDK ExperienceEvent Mixin`]
1. Marque la casilla .
1. Buscar [!UICONTROL `Consumer Experience Event`]
1. Marque la casilla .
1. Select **[!UICONTROL Agregar grupos de campos]**

   ![Agregar grupo de campos](assets/schema-add-field-group.jpg)

Con los grupos de campos seleccionados, está listo para asignar un nombre al esquema. Una convención de nomenclatura común para los esquemas XDM es nombrar el esquema después del origen de los datos:

1. En el **[!UICONTROL Composición**] seleccione `Untitled schema name`
1. En el **[!UICONTROL Propiedades del esquema]** , introduzca el **[!UICONTROL Nombre para mostrar]** `Luma Web Event Data`
1. Seleccione cualquier cosa fuera de **[!UICONTROL Nombre para mostrar]** para activar el **[!UICONTROL Guardar]** option
1. Seleccione **[!UICONTROL Guardar]**

![Datos de evento web de Luma](assets/schema-luma-web-event-data.png)

Con ambos grupos de campos, observe que tiene acceso a los pares de clave-valor más utilizados y requeridos para la recopilación de datos en la web. Al hacer clic en cualquier nombre de grupo de campos, la interfaz resalta qué agrupaciones de pares clave-valor pertenecen a él. En el ejemplo siguiente, puede ver a qué grupos pertenecen **[!UICONTROL Evento de experiencia del consumidor]**.

![Grupos de campos de esquema](assets/schema-consumer-experience-event.jpg)

Esta lección es solo un punto de partida. Al crear su propio esquema de eventos web, debe explorar y documentar los requisitos comerciales. Este proceso es similar a la creación de un [Documento de requisitos empresariales](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document.html?lang=es) y [Referencia de diseño de la solución](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html) para una implementación de Adobe Analytics, pero debe incluir requisitos para _todos los destinatarios de datos descendentes_ como Platform, Target y destinos de reenvío de eventos.


### El objeto identityMap

Se requiere un conjunto especial de datos para identificar a los usuarios web llamados `[!UICONTROL identityMap]`.

![Datos de evento web de Luma](assets/schema-identityMap.png)

Es un objeto obligatorio para cualquier recopilación de datos relacionados con la web, ya que contiene el ID de Experience Cloud necesario para identificar a los usuarios en la web. También es clave para configurar los ID de cliente internos para los usuarios autenticados. `[!UICONTROL identityMap]` se analiza más en la sección [Configurar identidades](configure-identities.md) lección. Se incluye automáticamente en todos los esquemas que utilizan la variable **[!UICONTROL XDM ExperienceEvent]** Clase .


>[!IMPORTANT]
>
> Es posible habilitar **[!UICONTROL Perfil]** para un esquema antes de guardar el esquema. **No** habilitarlo en este punto. Una vez que un esquema está habilitado para Perfil, no se puede deshabilitar ni eliminar. Además, los campos no se pueden eliminar del esquema después de este punto. Estas implicaciones son importantes de tener en cuenta más adelante cuando trabaje con sus propios datos en su entorno de producción.
>
>Esta configuración se analiza más durante la [Experience Platform de configuración](setup-experience-platform.md) lección.
>![Esquema de perfil](assets/schema-profile.png)

Ahora puede hacer referencia a este esquema al añadir la extensión del SDK web a la propiedad tag .


[Siguiente: ](configure-identities.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK web de Adobe Experience Platform. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
