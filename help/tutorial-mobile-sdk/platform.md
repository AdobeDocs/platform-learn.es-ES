---
title: Envío de datos a Experience Platform con Platform Mobile SDK
description: Obtenga información sobre cómo enviar datos a Experience Platform.
solution: Data Collection,Experience Platform
feature: Mobile SDK,Data Ingestion
jira: KT-14637
exl-id: fdd2c90e-8246-4d75-a6db-df3ef31946c4
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 3%

---

# Envío de datos a Experience Platform

Obtenga información sobre cómo enviar datos de aplicaciones móviles a Adobe Experience Platform.

Esta lección opcional es relevante para todos los clientes de Real-Time Customer Data Platform (Real-Time CDP), Journey Optimizer y Customer Journey Analytics. Experience Platform, la base de los productos de Experience Cloud, es un sistema abierto que transforma todos los datos (tanto de Adobe Adobe como de otras marcas) en perfiles de cliente sólidos. Estos perfiles de clientes se actualizan en tiempo real y utilizan perspectivas impulsadas por IA para ayudarle a ofrecer las experiencias correctas en todos los canales.

Los datos de [evento](events.md), [ciclo vital](lifecycle-data.md) e [identidad](identity.md) que recopiló y envió a Platform Edge Network en lecciones anteriores se reenvían a los servicios configurados en su secuencia de datos, incluido Adobe Experience Platform.

![Arquitectura](assets/architecture-aep.png){zoomable="yes"}


## Requisitos previos

Su organización debe estar aprovisionada y se deben conceder permisos para Adobe Experience Platform.

Si no tiene acceso, [puede omitir esta lección](install-sdks.md).

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Cree un conjunto de datos de Experience Platform.
* Configure el conjunto de datos para reenviar datos a Experience Platform.
* Valide los datos del conjunto de datos.
* Habilite el esquema y el conjunto de datos para el Perfil del cliente en tiempo real.
* Validar datos en el perfil del cliente en tiempo real.
* Valide los datos en el gráfico de identidad.


## Crear un conjunto de datos

Todos los datos que se incorporan correctamente a Adobe Experience Platform se conservan dentro del lago de datos como conjuntos de datos. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos (normalmente una tabla) que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan. Consulte la [documentación](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/overview) para obtener más información.

1. Vaya a la IU de Experience Platform. Seleccione **[!UICONTROL Experience Platform]** en el menú Aplicaciones ![Aplicaciones](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) de la parte superior derecha.


1. Seleccione **[!UICONTROL Conjuntos de datos]** en el menú de navegación de la izquierda.

1. Seleccione ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Crear conjunto de datos]**.

1. Seleccione **[!UICONTROL Crear conjunto de datos a partir del esquema]**.
   ![inicio del conjunto de datos](assets/dataset-create.png){zoomable="yes"}

1. Busque su esquema. por ejemplo, usar `Luma Mobile` en el campo de búsqueda.
1. Seleccione el esquema, por ejemplo **[!DNL Luma Mobile App Event Schema]**.

1. Seleccione **[!UICONTROL Siguiente]**.
   ![conjunto de datos configurado](assets/dataset-configure.png){zoomable="yes"}

1. Proporcione **[!UICONTROL Nombre]**, por ejemplo `Luma Mobile App Events Dataset` y **[!UICONTROL Descripción]**.

1. Seleccione **[!UICONTROL Finalizar]**.
   ![fin del conjunto de datos](assets/dataset-finish.png){zoomable="yes"}


## Añadir el servicio de flujo de datos de Adobe Experience Platform

Para enviar los datos XDM de Edge Network a Adobe Experience Platform, agregue el servicio Adobe Experience Platform a la secuencia de datos que configuró como parte de [Crear una secuencia de datos](create-datastream.md).

>[!IMPORTANT]
>
>Solo puede habilitar el servicio Adobe Experience Platform cuando haya creado un conjunto de datos de evento.

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y su secuencia de datos.

1. Luego selecciona ![Agregar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Agregar servicio]**.

1. Seleccione **[!UICONTROL Adobe Experience Platform]** de la lista [!UICONTROL Service].

1. Habilite el servicio activando **[!UICONTROL Enabled]**.

1. Seleccione el **[!UICONTROL Conjunto de datos de evento]** que creó anteriormente, por ejemplo **[!DNL Luma Mobile App Event Dataset]**.

1. Seleccione **[!UICONTROL Guardar]**.

   ![Agregar Adobe Experience Platform como servicio de secuencia de datos](assets/datastream-service-aep.png){zoomable="yes"}
1. La configuración final debería tener un aspecto similar al siguiente.

   ![configuración de secuencia de datos](assets/datastream-settings.png){zoomable="yes"}


## Validar datos en el conjunto de datos

Ahora que ha creado un conjunto de datos y ha actualizado el conjunto de datos para enviar datos a Experience Platform, todos los datos XDM enviados a Platform Edge Network se reenvían a Platform y aterrizan en el conjunto de datos.

Abra la aplicación y vaya a las pantallas donde realiza el seguimiento de eventos. También puede almacenar en déclencheur las métricas del ciclo vital.

Abra el conjunto de datos en la interfaz de Platform. Debería ver los datos que llegan en lotes al conjunto de datos. Los datos suelen llegar en microlotes cada 15 minutos, por lo que es posible que no vea los datos inmediatamente.

![validar lotes de conjuntos de datos de Platform de aterrizaje de datos](assets/platform-dataset-batches.png){zoomable="yes"}

También debería ver registros y campos de ejemplo usando la función **[!UICONTROL Vista previa del conjunto de datos]**:
![validar ciclo de vida enviado al conjunto de datos de Platform](assets/lifecycle-platform-dataset.png){zoomable="yes"}

Una herramienta más sólida para validar datos es [el servicio de consultas](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/queries/explore-data) de Platform.

## Activar perfil de cliente en tiempo real

El perfil del cliente en tiempo real de Experience Platform le permite crear una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los distintos datos de clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción de clientes.

### Habilitar el esquema

1. Abra el esquema, por ejemplo **[!DNL Luma Mobile App Event Schema]**.
1. Habilitar **[!UICONTROL perfil]**.
1. Seleccione **[!UICONTROL Los datos de este esquema contienen una identidad principal en el campo identityMap.]** en el diálogo.
1. **[!UICONTROL Guardar]** el esquema.

   ![habilitar el esquema para el perfil](assets/platform-profile-schema.png){zoomable="yes"}

### Habilitar el conjunto de datos

1. Abra el conjunto de datos, por ejemplo **[!DNL Luma Mobile App Event Dataset]**.
1. Habilitar **[!UICONTROL perfil]**.

   ![habilitar el conjunto de datos para el perfil](assets/platform-profile-dataset.png){zoomable="yes"}

### Validar datos en el perfil

Abra la aplicación y vaya a las pantallas donde realiza el seguimiento de eventos como, por ejemplo: inicie sesión en la aplicación de Luma y realice una compra.

Utilice Assurance para buscar una de las identidades pasadas en el identityMap (correo electrónico, lumaCrmId o ECID), por ejemplo, el ID de CRM.

![obtener un valor de identidad](assets/platform-identity.png){zoomable="yes"}

En la interfaz de Platform,

1. Vaya a **[!UICONTROL Perfiles]** y seleccione **[!UICONTROL Examinar]** en la barra superior.
1. Especifique los detalles de identidad que acaba de tomar, por ejemplo `Luma CRM ID` para **[!UICONTROL área de nombres de identidad]** y el valor que copió para **[!UICONTROL valor de identidad]**. Luego selecciona **[!UICONTROL Ver]**.
1. Para ver los detalles, seleccione el perfil.

![buscar un valor de identidad](assets/platform-profile-lookup.png){zoomable="yes"}

En la pantalla **[!UICONTROL Detail]**, puedes ver información básica sobre el usuario, incluidas las **[!UICONTROL ** identidades vinculadas **]**:
![detalles del perfil](assets/platform-profile-details.png){zoomable="yes"}

En **[!UICONTROL Eventos]**, podrá ver los eventos recopilados de la implementación de su aplicación móvil para este usuario:

![eventos de perfil](assets/platform-profile-events.png){zoomable="yes"}


Desde la pantalla de detalles del perfil:

1. Para ver el gráfico de identidades, haz clic en el vínculo o navega a **[!UICONTROL Identidades]** y, a continuación, selecciona **[!UICONTROL Gráfico de identidades]** en la barra superior.
1. Para buscar el valor de identidad, especifique `Luma CRM ID` como **[!UICONTROL área de nombres de identidad]** y el valor copiado como **[!UICONTROL valor de identidad]**. Luego selecciona **[!UICONTROL Ver]**.

   Esta visualización muestra las identidades vinculadas en un perfil y su origen. Este es un ejemplo de un gráfico de identidades construido a partir de los datos recopilados al completar este tutorial de Mobile SDK (Data Source 2) y el [tutorial de Web SDK](https://experienceleague.adobe.com/es/docs/platform-learn/implement-web-sdk/overview) (Data Source 1):

   ![obtener un valor de identidad](assets/platform-profile-identitygraph.png){zoomable="yes"}


## Próximos pasos

Los especialistas en marketing y análisis pueden hacer mucho más con los datos capturados en Experience Platform, incluido analizarlos en Customer Journey Analytics y crear segmentos en Real-Time Customer Data Platform. ¡Ha tenido un buen comienzo!


>[!SUCCESS]
>
>Ahora ha configurado la aplicación para enviar datos no solo a Edge Network, sino también a Adobe Experience Platform.<br>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Mobile SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).
>

Siguiente: **[Crear y enviar notificaciones push](journey-optimizer-push.md)**
