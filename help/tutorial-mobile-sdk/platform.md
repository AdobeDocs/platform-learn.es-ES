---
title: Envío de datos al Experience Platform con el SDK de Platform Mobile
description: Obtenga información sobre cómo enviar datos al Experience Platform.
solution: Data Collection,Experience Platform
feature: Mobile SDK,Data Ingestion
exl-id: fdd2c90e-8246-4d75-a6db-df3ef31946c4
source-git-commit: d353de71d8ad26d2f4d9bdb4582a62d0047fd6b1
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 5%

---

# Envío de datos al Experience Platform

Obtenga información sobre cómo enviar datos de aplicaciones móviles a Adobe Experience Platform.

Esta lección opcional es relevante para todos los clientes de Real-time Customer Data Platform (Real-Time CDP), Journey Optimizer y Customer Journey Analytics. Experience Platform, la base de los productos de Experience Cloud, es un sistema abierto que transforma todos los datos (de Adobe y sin Adobe) en perfiles de cliente sólidos. Estos perfiles de clientes se actualizan en tiempo real y utilizan perspectivas impulsadas por IA para ayudarle a ofrecer las experiencias correctas en todos los canales.

El [evento](events.md), [ciclo vital](lifecycle-data.md), y [identidad](identity.md) Los datos que ha recopilado y enviado a Platform Edge Network en lecciones anteriores se reenvían a los servicios configurados en su conjunto de datos, incluido Adobe Experience Platform.

![Arquitectura](assets/architecture-aep.png)


## Requisitos previos

Su organización debe estar aprovisionada y se deben conceder permisos para Adobe Experience Platform.

Si no tiene acceso, puede hacer lo siguiente [omitir esta lección](install-sdks.md).

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Cree un conjunto de datos de Experience Platform.
* Configure la secuencia de datos para reenviar datos al Experience Platform.
* Valide los datos del conjunto de datos.
* Habilite el esquema y el conjunto de datos para el Perfil del cliente en tiempo real.
* Validar datos en el perfil del cliente en tiempo real.
* Valide los datos en el gráfico de identidad.


## Crear un conjunto de datos

Todos los datos que se incorporan correctamente a Adobe Experience Platform se conservan dentro del lago de datos como conjuntos de datos. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos (normalmente una tabla) que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan. Consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=es) para obtener más información.

1. Vaya a la interfaz del Experience Platform seleccionándola en las aplicaciones ![Aplicaciones](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) en la parte superior derecha.


1. Seleccionar **[!UICONTROL Conjuntos de datos]** en el menú de navegación izquierdo.

1. Seleccionar ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Crear conjunto de datos]**.

1. Seleccione **[!UICONTROL Crear conjunto de datos a partir de esquema]**.
   ![inicio del conjunto de datos](assets/dataset-create.png)

1. Busque su esquema. por ejemplo, usar `Luma Mobile` en el campo de búsqueda.
1. Seleccione el esquema, por ejemplo **[!DNL Luma Mobile App Event Schema]**.

1. Seleccione **[!UICONTROL Siguiente]**.
   ![conjunto de datos configurar](assets/dataset-configure.png)

1. Proporcione un **[!UICONTROL Nombre]**, por ejemplo `Luma Mobile App Events Dataset` y una **[!UICONTROL Descripción]**.

1. Seleccione **[!UICONTROL Finalizar]**.
   ![fin de conjunto de datos](assets/dataset-finish.png)


## Añadir el servicio de flujo de datos de Adobe Experience Platform

Para enviar los datos XDM de la red perimetral a Adobe Experience Platform, agregue el servicio Adobe Experience Platform al conjunto de datos que configuró como parte de [Creación de una secuencia de datos](create-datastream.md).

>[!IMPORTANT]
>
>Solo puede habilitar el servicio Adobe Experience Platform cuando haya creado un conjunto de datos de evento.

1. En la IU de recopilación de datos, seleccione **[!UICONTROL Datastreams]** y su secuencia de datos.

1. A continuación seleccione ![Añadir](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Añadir servicio]**.

1. Seleccione **[!UICONTROL Adobe Experience Platform]** en la lista [!UICONTROL Servicio].

1. Habilitar el servicio cambiando **[!UICONTROL Habilitado]** en.

1. Seleccione el **[!UICONTROL Conjunto de datos de evento]** que creó anteriormente , por ejemplo **[!DNL Luma Mobile App Event Dataset]**.

1. Seleccione **[!UICONTROL Guardar]**.

   ![Añadir Adobe Experience Platform como servicio de flujo de datos](assets/datastream-service-aep.png)
1. La configuración final debería tener un aspecto similar al siguiente.

   ![configuración de secuencia de datos](assets/datastream-settings.png)


## Validación de datos en el conjunto de datos

Ahora que ha creado un conjunto de datos y ha actualizado el conjunto de datos para enviar datos al Experience Platform, todos los datos XDM enviados a Platform Edge Network se reenvían a Platform y aterrizan en el conjunto de datos.

Abra la aplicación y vaya a las pantallas donde realiza el seguimiento de eventos. También puede almacenar en déclencheur las métricas del ciclo vital.

Abra el conjunto de datos en la interfaz de Platform. Debería ver los datos que llegan en lotes al conjunto de datos. Los datos suelen llegar en microlotes cada 15 minutos, por lo que es posible que no vea los datos inmediatamente.

![validar lotes de conjuntos de datos de Platform de aterrizaje de datos](assets/platform-dataset-batches.png)

También debería poder ver registros y campos de ejemplo utilizando **[!UICONTROL Previsualizar conjunto de datos]** función:
![validar ciclo de vida enviado a conjunto de datos de Platform](assets/lifecycle-platform-dataset.png)

Una herramienta más sólida para validar datos es la [servicio de consultas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=es).

## Activar perfil de cliente en tiempo real

El perfil del cliente en tiempo real de Experience Platform le permite crear una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los distintos datos de clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción de clientes.

### Habilitar el esquema

1. Abra el esquema, por ejemplo **[!DNL Luma Mobile App Event Schema]**.
1. Activar **[!UICONTROL Perfil]**.
1. Seleccionar **[!UICONTROL Los datos de este esquema contienen una identidad principal en el campo identityMap.]** en el cuadro de diálogo.
1. **[!UICONTROL Guardar]** el esquema.

   ![habilitar el esquema para el perfil](assets/platform-profile-schema.png)

### Habilitar el conjunto de datos

1. Abra el conjunto de datos, por ejemplo **[!DNL Luma Mobile App Event Dataset]**.
1. Activar **[!UICONTROL Perfil]**.

   ![habilitar el conjunto de datos para el perfil](assets/platform-profile-dataset.png)

### Validar datos en el perfil

Abra la aplicación y vaya a las pantallas donde realiza el seguimiento de eventos como, por ejemplo: inicie sesión en la aplicación de Luma y realice una compra.

Use Assurance para encontrar una de las identidades pasadas en identityMap (correo electrónico, lumaCrmId o ECID), por ejemplo, el ID de CRM.

![obtener un valor de identidad](assets/platform-identity.png)

En la interfaz de Platform,

1. Vaya a **[!UICONTROL Perfiles]** y seleccione **[!UICONTROL Examinar]** desde la barra superior.
1. Especifique los detalles de identidad que acaba de recopilar, por ejemplo `Luma CRM ID` para **[!UICONTROL Área de nombres de identidad]** y el valor que ha copiado para **[!UICONTROL Valor de identidad]**. A continuación seleccione **[!UICONTROL Ver]**.
1. Para ver los detalles, seleccione el perfil.

![búsqueda de un valor de identidad](assets/platform-profile-lookup.png)

En el **[!UICONTROL Detalle]** , puede ver información básica sobre el usuario, incluido el **[!UICONTROL ** identidades vinculadas **]**:
![detalles del perfil](assets/platform-profile-details.png)

En el **[!UICONTROL Eventos]**, puede ver los eventos recopilados desde la implementación de la aplicación móvil para este usuario:

![eventos de perfil](assets/platform-profile-events.png)


Desde la pantalla de detalles del perfil:

1. Para ver el gráfico de identidad, haga clic en el vínculo o vaya a **[!UICONTROL Identidades]**, luego seleccione **[!UICONTROL Gráfico de identidad]** desde la barra superior.
1. Para buscar el valor de identidad, especifique `Luma CRM ID` como el **[!UICONTROL Área de nombres de identidad]** y el valor copiado como **[!UICONTROL Valor de identidad]**. A continuación seleccione **[!UICONTROL Ver]**.

   Esta visualización muestra todas las identidades vinculadas en un perfil y su origen. Este es un ejemplo de gráfico de identidad construido a partir de datos recopilados al completar este tutorial del SDK móvil (fuente de datos 2) y el [Tutorial de SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es) (Fuente de datos 1):

   ![obtener un valor de identidad](assets/platform-profile-identitygraph.png)


## Pasos siguientes

Los especialistas en marketing y análisis pueden hacer mucho más con los datos capturados en Experience Platform, incluido analizarlos en Customer Journey Analytics y crear segmentos en Real-time Customer Data Platform. ¡Ha tenido un buen comienzo!


>[!SUCCESS]
>
>Ahora ha configurado la aplicación para enviar datos no solo a la red perimetral, sino también a Adobe Experience Platform.<br>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Siguiente: **[Creación y envío de notificaciones push](journey-optimizer-push.md)**
