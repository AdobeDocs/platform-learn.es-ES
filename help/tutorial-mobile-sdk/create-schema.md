---
title: Creación de un esquema XDM
description: Obtenga información sobre cómo crear un esquema XDM para eventos de aplicaciones móviles.
exl-id: c6b0d030-437a-4afe-b7d5-5a7831877983
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 6%

---

# Creación de un esquema XDM

Obtenga información sobre cómo crear un esquema XDM para eventos de aplicaciones móviles.

La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. Experience Data Model (XDM), impulsado por el Adobe, es un esfuerzo por estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

## ¿Qué son los esquemas XDM?

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes que permiten a cualquier aplicación comunicarse con los servicios de Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente pueden incorporarse a una representación común que puede proporcionar perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y expresar atributos del cliente con fines de personalización.

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de manera uniforme en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Antes de poder introducir los datos en Platform, se debe componer un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se puede contener dentro de cada campo. Los esquemas constan de una clase base y de cero o más grupos de campos de esquema.

Para obtener más información sobre el modelo de composición del esquema, incluidos los principios de diseño y las prácticas recomendadas, consulte la [conceptos básicos de la composición del esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es) o el curso [Modelar los datos de la experiencia del cliente con XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm).

>[!TIP]
>
>Si está familiarizado con la referencia de diseño de soluciones (SDR) de Analytics, puede considerar un esquema como un SDR más robusto.

## Requisitos previos

Para completar la lección, debe tener permiso para crear un esquema de Experience Platform.

## Objetivos de aprendizaje

En esta lección:

* Creación de un esquema en la interfaz de recopilación de datos
* Añadir un grupo de campos estándar al esquema
* Creación y adición de un grupo de campos personalizados al esquema

## Navegar a esquemas

1. Inicie sesión en Adobe Experience Cloud.

1. Abra el conmutador de aplicaciones y seleccione **[!UICONTROL Recopilación de datos]**

   ![Menú desplegable 3x3](assets/mobile-schema-navigate1.png)

1. Asegúrese de que está en el simulador de pruebas de Experience Platform que utiliza para este tutorial.

   >[!NOTE]
   >
   > Los clientes de aplicaciones basadas en Platform como Real-Time CDP deben utilizar un entorno limitado de desarrollo para este tutorial. Otros clientes utilizarán el entorno limitado de producción predeterminado.


1. Select **[!UICONTROL Esquemas]** under **[!UICONTROL Gestión de datos]**.

   ![etiqueta pantalla de inicio](assets/mobile-schema-navigate3.png)

Ahora se encuentra en la página de esquemas principales y se le presenta una lista de los esquemas existentes. También puede ver las pestañas correspondientes a los componentes principales de un esquema:

* **Grupos de campo** son componentes reutilizables que definen uno o más campos para capturar datos específicos, como detalles personales, preferencias de hotel o dirección.
* **Clases** defina los aspectos de comportamiento de los datos que contiene el esquema. Por ejemplo: `XDM ExperienceEvent` captura series temporales, datos de eventos y `XDM Individual Profile` captura datos de atributos sobre un individuo.
* **Tipos de datos** se utilizan como tipos de campos de referencia en clases o grupos de campos de la misma manera que los campos literales básicos.

Las descripciones anteriores son una descripción general de alto nivel. Para obtener más información, consulte la [Componentes básicos del esquema](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schema-building-blocks.html?lang=es) vídeo o lectura [Aspectos básicos de la composición del esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es) en la documentación del producto.

En este tutorial, se utiliza el grupo de campos Evento de experiencia del consumidor y se crea uno personalizado para mostrar el proceso.

>[!NOTE]
>
>El Adobe sigue agregando grupos de campos más estándar y deben utilizarse siempre que sea posible, ya que los servicios de Experience Platform comprenden implícitamente estos campos y proporcionan buena coherencia cuando se utilizan en los componentes de Platform. El uso de grupos de campos estándar proporciona beneficios tangibles, como la asignación automática en las funciones de Analytics e AI en Platform.

## Arquitectura de esquema de aplicaciones de Luma

En un escenario real, el proceso de diseño de esquema podría tener este aspecto:

* Recopile los requisitos comerciales.
* Encuentre grupos de campos pregenerados para cubrir tantos requisitos como sea posible.
* Cree grupos de campos personalizados para cualquier espacio.

Para aprendizaje, se utilizan grupos de campos pregenerados y personalizados.

* **Evento de experiencia del consumidor**: Grupo de campos creado previamente que tiene muchos campos comunes.
* **Información de la aplicación**: Grupo de campos personalizados diseñado para imitar los conceptos de TrackState/TrackAction Analytics.

<!--Later in the tutorial, you can [update the schema](lifecycle-data.md) to include the **[!UICONTROL AEP Mobile Lifecycle Details]** field group.-->

## Creación de un esquema

1. Select **[!UICONTROL Crear esquema]** para que aparezca el menú desplegable de opciones, seleccione **[!UICONTROL XDM ExperienceEvent]**.

   ![Selección de ExperienceEvent en la lista desplegable](assets/mobile-schema-create.png)

1. Buscar `Consumer Experience Event`.

1. Puede obtener una vista previa de los campos o leer la descripción para obtener más información antes de seleccionar.

1. Seleccione la casilla de verificación y, a continuación, **[!UICONTROL Agregar grupos de campos]**.

   ![Selección del grupo de campos](assets/mobile-schema-select-field-groups.png)

   Se le devuelve a la pantalla de composición del esquema principal, donde puede ver todos los campos disponibles.

1. Asigne un nombre al esquema seleccionando **[!UICONTROL Esquema sin título]** desde la parte superior izquierda y, a continuación, proporcione una **[!UICONTROL Nombre para mostrar]** &amp; **[!UICONTROL Descripción]**, por ejemplo `Luma Tutorial Mobile` y `"Luma App" schema for Adobe Tutorial`

1. Seleccione **[!UICONTROL Guardar]**.

   ![Seleccionar aplicación](assets/mobile-schema-name-save.png)

>[!NOTE]
>
>Tenga en cuenta que no es necesario utilizar todos los campos de un grupo. Si resulta útil, puede considerar un esquema como una capa de datos vacía. En la aplicación, rellene los valores relevantes en el momento adecuado.
>
>La variable `Consumer Experience Event` tiene un tipo de datos llamado `Web information`, que describe eventos como vista de página y clics en vínculos. En el momento de escribir este artículo, esta función no es la misma para las aplicaciones móviles, por lo que debe crear la suya propia.

## Crear un tipo de datos personalizado

Comience creando un tipo de datos personalizado que describa los dos eventos:

* Vista de pantalla
* Interacción con la aplicación

1. Seleccione el **[!UICONTROL Tipos de datos]** y, a continuación, seleccione **[!UICONTROL Crear tipo de datos]**.

   ![Selección del menú de tipo de datos](assets/mobile-schema-datatype-create.png)

1. Denle un **[!UICONTROL Nombre para mostrar]** y **[!UICONTROL Descripción]**, por ejemplo `App Information` y `Custom data type describing "Screen Views" & "App Actions"`

   ![Proporcionar nombre y descripción](assets/mobile-schema-datatype-name.png)

   >[!TIP]
   >
   > Utilice siempre legible y descriptivo [!UICONTROL nombres para mostrar] para los campos personalizados, ya que esta práctica los hace más accesibles para los especialistas en marketing cuando los campos aparecen en servicios descendentes como el generador de segmentos.


1. Para añadir un campo, seleccione el botón (+) .

   Este campo es un objeto de contenedor para la interacción con la aplicación. Denle un caso de camello **[!UICONTROL Nombre del campo]** `appInteraction`, **[!UICONTROL nombre para mostrar]** `App Interaction`y **[!UICONTROL type]** `Object`.

1. Select **[!UICONTROL Aplicar]**.

   ![Adición de un nuevo evento de acción de aplicación](assets/mobile-schema-datatype-app-action.png)

1. Para medir la frecuencia con la que se ha producido una acción, añada un campo seleccionando el botón (+) junto al `appInteraction` objeto creado.

1. Denle un caso de camello **[!UICONTROL Nombre del campo]** `appAction`, **[!UICONTROL nombre para mostrar]** de `App Action` y **[!UICONTROL type]** `Measure`.

   Este paso equivaldría a un evento de éxito en Adobe Analytics.

1. Select **[!UICONTROL Aplicar]**.

   ![Adición de un campo de nombre de acción](assets/mobile-schema-datatype-action-name.png)

1. Añada un campo que describa el tipo de interacción seleccionando el botón (+) junto al `appInteraction` objeto.

1. Denle un **[!UICONTROL Nombre del campo]** `name`, **[!UICONTROL nombre para mostrar]** de `Name` y **[!UICONTROL type]** `String`.

   Este paso es el equivalente de una dimensión en Adobe Analytics.

   ![Seleccionar aplicación](assets/mobile-schema-datatype-apply.png)

1. Desplácese hasta la parte inferior del carril derecho y seleccione **[!UICONTROL Aplicar]**.

1. Siga el mismo patrón para crear un `appStateDetails` objeto que contiene un campo de medida llamado `screenView` y dos cadenas llamadas `screenName` y `screenType`.

1. Seleccione **[!UICONTROL Guardar]**.

   ![Estado final del tipo de datos](assets/mobile-schema-datatype-final.png)

## Agregar un grupo de campos personalizados

Ahora agregue un grupo de campos personalizado con su tipo de datos personalizado:

1. Abra el esquema que creó anteriormente en esta lección.

1. Select **[!UICONTROL Agregar]** junto a **[!UICONTROL Grupos de campo]**.

   ![Adición de un nuevo grupo de campos](assets/mobile-schema-fieldgroup-add.png)

1. Esta vez, se crea un grupo de campos personalizados seleccionando la variable **[!UICONTROL Crear nuevo grupo de campos]** botón de opción cerca de la parte superior e indique un nombre y una descripción, por ejemplo, `App Interactions` y `Fields for app interactions`.

   ![Proporcionar nombre y descripción](assets/mobile-schema-fieldgroup-name.png)

1. Desde la pantalla de composición principal, añada un campo a la raíz del esquema.

1. Seleccione el (+) situado junto al nombre del esquema.

1. En el carril derecho, proporcione una **[!UICONTROL Nombre del campo]** de `appInformation`, un nombre para mostrar de `App Information`.

1. Select `App Information` de la variable **[!UICONTROL Tipo]** , el tipo de datos que creó en el ejercicio anterior.

1. Select **[!UICONTROL Aplicar]**.

   ![Seleccionar aplicación](assets/mobile-schema-fieldgroup-apply.png)

>[!NOTE]
>
>Los grupos de campos personalizados siempre se colocan bajo el identificador de organización del Experience Cloud.
>
>`_techmarketingdemos` se reemplaza por el valor único de su organización.

Ahora tiene un esquema que utilizar para el resto del tutorial.

Siguiente: **[Cree un [!UICONTROL datastream]](create-datastream.md)**

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK de Adobe Experience Platform Mobile. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)