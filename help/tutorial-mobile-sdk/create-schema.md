---
title: Creación de un esquema XDM para implementaciones de Platform Mobile SDK
description: Obtenga información sobre cómo crear un esquema XDM para eventos de aplicaciones móviles.
feature: Mobile SDK,Schemas
jira: KT-14624
exl-id: c6b0d030-437a-4afe-b7d5-5a7831877983
source-git-commit: 63987fb652a653283a05a5f35f7ce670127ae905
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 2%

---

# Creación de un esquema XDM

Obtenga información sobre cómo crear un esquema XDM para eventos de aplicaciones móviles.

La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. El modelo de datos de experiencia (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

## ¿Qué son los esquemas XDM?

XDM es una especificación documentada públicamente y diseñada para mejorar la potencia de las experiencias digitales. Proporciona estructuras y definiciones comunes que permiten a cualquier aplicación comunicarse con los servicios de Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común que puede ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir las audiencias de los clientes mediante segmentos y utilizar los atributos del cliente para fines de personalización.

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de forma coherente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Antes de poder introducir datos en Platform, se debe crear un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se pueden contener en cada campo. Los esquemas constan de una clase base y cero o más grupos de campos de esquema.

Para obtener más información sobre el modelo de composición de esquemas, incluidos los principios de diseño y las prácticas recomendadas, consulte los [conceptos básicos de la composición de esquemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es) o la lista de reproducción [Modelar los datos de la experiencia del cliente con XDM](https://experienceleague.adobe.com/es/playlists/experience-platform-model-your-customer-experience-data-with-xdm).

>[!TIP]
>
>Si está familiarizado con la Referencia de diseño de soluciones (SDR) de Analytics, puede pensar en un esquema como un SDR más robusto. Consulte [Crear y mantener un documento Diseño de referencia de la solución (DRS)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html?lang=es) para obtener más información.

## Requisitos previos

Para completar la lección, debe tener permiso para crear un esquema de Experience Platform.

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Creación de un esquema en la interfaz de recopilación de datos
* Añadir un grupo de campos estándar al esquema
* Crear y agregar un grupo de campos personalizados al esquema

## Navegar a esquemas

1. Inicie sesión en Adobe Experience Cloud.

1. Asegúrese de que está en la zona protegida de Experience Platform que está utilizando para este tutorial.

1. Abra el conmutador de aplicación ![Conmutador de aplicación](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) (en la parte superior derecha),

1. Seleccione **[!UICONTROL Recopilación de datos]** en el menú.

   ![Iniciar sesión en el Experience Cloud](assets/experiencecloud-login.png)

   >[!NOTE]
   >
   > Los clientes de aplicaciones basadas en Platform como Real-Time CDP deben utilizar una zona protegida de desarrollo para este tutorial. Otros clientes utilizan la zona protegida de producción predeterminada.


1. Seleccione **[!UICONTROL Esquemas]** en **[!UICONTROL Administración de datos]** en el carril izquierdo.

   ![pantalla de inicio de etiquetas](assets/mobile-schema-navigate.png)

Ahora se encuentra en la página de esquemas principales y se le presenta una lista de los esquemas existentes. También puede ver las pestañas correspondientes a los bloques de creación principales de un esquema:

* **Los grupos de campos** son componentes reutilizables que definen uno o más campos para capturar datos específicos, como detalles personales, preferencias de hotel o dirección.
* **Las clases** definen los aspectos de comportamiento de los datos que contiene el esquema. Por ejemplo: `XDM ExperienceEvent` captura series temporales, datos de eventos y `XDM Individual Profile` captura datos de atributos de un individuo.
* **Los tipos de datos** se utilizan como tipos de campos de referencia en clases o grupos de campos de la misma manera que los campos literales básicos.

Las descripciones anteriores son una descripción general de alto nivel. Para obtener más información, consulte el vídeo [Componentes básicos del esquema](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schema-building-blocks.html?lang=es) o lea [Aspectos básicos de la composición del esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es) en la documentación del producto.

En este tutorial, se utiliza el grupo de campos Evento de experiencia del consumidor y se crea uno personalizado para mostrar el proceso.

>[!NOTE]
>
>El Adobe sigue añadiendo grupos de campos más estándar y deben utilizarse siempre que sea posible, ya que los servicios de Experience Platform entienden implícitamente estos campos y proporcionan una mayor coherencia cuando se utilizan en todos los componentes de Platform. El uso de grupos de campos estándar proporciona beneficios tangibles, como la asignación automática en Analytics y las funciones de IA en Platform.

## Arquitectura de esquema de aplicación de Luma

En un escenario real, el proceso de diseño del esquema podría tener este aspecto:

* Reúna los requisitos empresariales.
* Busque grupos de campos creados previamente para cubrir tantos requisitos como sea posible.
* Cree grupos de campos personalizados para cualquier hueco.

Para fines de aprendizaje, utiliza grupos de campos creados previamente y personalizados.

* **Evento de experiencia del consumidor**: grupo de campos creado previamente que tiene muchos campos comunes.
* **Información de la aplicación**: grupo de campos personalizado diseñado para imitar los conceptos de TrackState/TrackAction Analytics.

<!--Later in the tutorial, you can [update the schema](lifecycle-data.md) to include the **[!UICONTROL AEP Mobile Lifecycle Details]** field group.-->

## Creación de un esquema

1. Seleccione **[!UICONTROL Crear esquema]**.

1. En el paso **[!UICONTROL Seleccionar una clase]** del asistente **[!UICONTROL Crear esquema]**, seleccione **[!UICONTROL Evento de experiencia]** debajo de **[!UICONTROL Seleccionar una clase base para este esquema]**.

1. Seleccione **[!UICONTROL Siguiente]**.

   ![Clase base del Asistente para esquemas](assets/schema-wizard-base-class.png)

1. En el paso **[!UICONTROL Nombrar y revisar]** del asistente **[!UICONTROL Crear esquema]**, escriba un **[!UICONTROL Nombre para mostrar esquema]**, por ejemplo `Luma Mobile Event Schema` y una [!UICONTROL Descripción], por ejemplo `Schema for Luma mobile app experience events`.

   >[!NOTE]
   >
   >Si va a seguir este tutorial con varias personas en una sola zona protegida o utiliza una cuenta compartida, considere anexar o anteponer una identificación como parte de las convenciones de nomenclatura. Por ejemplo, en lugar de `Luma Mobile App Event Schema`, use `Luma Mobile App Event Schema - Joe Smith`. Consulte también la nota de [Información general](overview.md).

1. Seleccione **[!UICONTROL Finalizar]** para finalizar el asistente.

   ![Nombre y revisión del esquema](assets/schema-wizard-name-and-review.png)


1. Seleccione ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **Agregar** junto a **[!UICONTROL Grupos de campos]**.

   ![Agregar grupo de campos](assets/add-field-group.png)

1. Busque `Consumer Experience Event`.

1. Seleccione ![Vista previa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Preview_18_N.svg) para obtener una vista previa de los campos o leer la descripción para obtener más detalles antes de seleccionar un grupo de campos.

1. Seleccione **Evento de experiencia del consumidor**.

1. Seleccione **[!UICONTROL Agregar grupos de campos]**.

   ![Seleccionando grupo de campos](assets/schema-select-field-groups.png)

   Volverá a la pantalla de composición del esquema principal, donde podrá ver todos los campos disponibles.

1. Seleccione **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Tenga en cuenta que no tiene que utilizar todos los campos de un grupo. También puede eliminar campos para mantener el esquema conciso y comprensible. Si resulta útil, puede considerar un esquema como una capa de datos vacía. En la aplicación, rellene los valores relevantes en el momento adecuado.

El grupo de campos [!UICONTROL Evento de experiencia del consumidor] tiene un tipo de datos denominado [!UICONTROL Información web], que describe eventos como la vista de página y los clics en vínculos. En el momento de escribir este artículo, esta función no tiene paridad de aplicación móvil, por lo que va a crear la suya propia.

## Creación de un tipo de datos personalizado

Para empezar, cree un tipo de datos personalizado que describa los dos eventos:

* Vista de pantalla
* Interacción de aplicación

1. Seleccione la ficha **[!UICONTROL Tipos de datos]**.

1. Seleccione **[!UICONTROL Crear tipo de datos]**.

   ![Seleccionar el menú de tipo de datos](assets/schema-datatype-create.png)

1. Proporcione un **[!UICONTROL nombre para mostrar]** y **[!UICONTROL Descripción]**, por ejemplo `App Information` y `Custom data type describing "Screen Views" & "App Actions"`

   ![Proporcionando nombre y descripción](assets/schema-datatype-name.png)

   >[!TIP]
   >
   > Use siempre [!UICONTROL nombres para mostrar] descriptivos y legibles para sus campos personalizados, ya que esta práctica los hace más accesibles para los especialistas en marketing cuando los campos aparecen en servicios descendentes como el generador de segmentos.


1. Para agregar un campo, selecciona el botón ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg).


1. Este campo es un objeto contenedor para la interacción con la aplicación. Proporcione un **[!UICONTROL Nombre de campo]** `appInteraction`, **[!UICONTROL Nombre para mostrar]** `App Interaction` y seleccione `Object` de la lista **[!UICONTROL Tipo]**.

1. Seleccione **[!UICONTROL Aplicar]**.

   ![Agregando nuevo evento de acción de aplicación](assets/schema-datatype-app-action.png)

1. Para medir la frecuencia con la que se ha producido una acción, agrega un campo seleccionando el botón ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto al objeto **[!UICONTROL appInteraction]** que has creado.

1. Asigne un **[!UICONTROL Nombre de campo]** `appAction`, **[!UICONTROL Nombre para mostrar]** de `App Action` y **[!UICONTROL Tipo]** `Measure`, en minúscula.

   Este paso sería el equivalente a un evento de éxito en Adobe Analytics.

1. Seleccione **[!UICONTROL Aplicar]**.

   ![Agregando campo de nombre de acción](assets/schema-datatype-action-name.png)

1. Agregue un campo que describa el tipo de interacción seleccionando el botón ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto al objeto **[!UICONTROL appInteraction]**.

1. Asigne un **[!UICONTROL nombre de campo]** `name`, **[!UICONTROL nombre para mostrar]** de `Name` y **[!UICONTROL tipo]** `String`.

   Este paso es el equivalente de una dimensión en Adobe Analytics.

   ![Seleccionando aplicar](assets/schema-datatype-apply.png)

1. Desplácese hasta la parte inferior del carril derecho y seleccione **[!UICONTROL Aplicar]**.

1. Para crear un objeto `appStateDetails` que contenga un campo **[!UICONTROL Measure]** denominado `screenView` y dos campos **[!UICONTROL String]** llamados `screenName` y `screenType`, siga los mismos pasos que al crear el objeto **[!UICONTROL appInteraction]**.

1. Seleccione **[!UICONTROL Guardar]**.

   ![Estado final del tipo de datos](assets/schema-datatype-final.png)

## Agregar un grupo de campos personalizados

Ahora añada un grupo de campos personalizados con su tipo de datos personalizado:

1. Abra el esquema que creó anteriormente en esta lección.

1. Seleccione ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Agregar]** junto a **[!UICONTROL Grupos de campos]**.

   ![Agregando nuevo grupo de campos](assets/schema-fieldgroup-add.png)

1. Seleccione **[!UICONTROL Crear nuevo grupo de campo]**.

1. Proporcione un **[!UICONTROL nombre para mostrar]** y **[!UICONTROL Descripción]**, por ejemplo, `App Interactions` y `Fields for app interactions`.

1. Seleccione **Agregar grupos de campos**.

   ![Proporcionando nombre y descripción](assets/schema-fieldgroup-name.png)

1. En la pantalla de composición principal, seleccione **[!UICONTROL Interacciones de la aplicación**].

1. Agregue un campo a la raíz del esquema seleccionando el botón ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) junto al nombre del esquema.

1. En el carril derecho, proporcione un **[!UICONTROL Nombre de campo]** de `appInformation`, un **[!UICONTROL Nombre para mostrar]** de `App Information` y un **[!UICONTROL Tipo]** de `App Information`.

1. Seleccione **[!UICONTROL Interacciones de aplicación]** de la lista desplegable **[!UICONTROL Grupo de campos]** para asignar los campos al nuevo grupo de campos.

1. Seleccione **[!UICONTROL Aplicar]**.

1. Seleccione **[!UICONTROL Guardar]**.

   ![Seleccionando aplicar](assets/schema-fieldgroup-apply.png)

>[!NOTE]
>
>Los grupos de campos personalizados siempre se colocan bajo el identificador de organización de Experience Cloud.


>[!SUCCESS]
>
>Ahora tiene un esquema para utilizar para el resto del tutorial.
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=es).

Siguiente: **[Crear un [!UICONTROL conjunto de datos]](create-datastream.md)**
