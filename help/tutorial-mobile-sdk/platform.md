---
title: Envío de datos a Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos a Adobe Experience Platform.
solution: Data Collection,Experience Platform
feature: Mobile SDK,Data Ingestion
exl-id: fdd2c90e-8246-4d75-a6db-df3ef31946c4
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 8%

---

# Envío de datos a Adobe Experience Platform

Obtenga información sobre cómo enviar datos a Adobe Experience Platform.

>[!INFO]
>
> Este tutorial se reemplazará con un nuevo tutorial con una nueva aplicación móvil de ejemplo a finales de noviembre de 2023

Esta lección opcional es relevante para todos los clientes de Real-time Customer Data Platform (Real-Time CDP), Journey Optimizer y Customer Journey Analytics. Experience Platform, la base de los productos de Experience Cloud, es un sistema abierto que transforma todos sus datos (de Adobe y sin Adobe) en perfiles de clientes sólidos que se actualizan en tiempo real y que utiliza perspectivas impulsadas por IA para ayudarle a ofrecer las experiencias correctas en todos los canales.

El [evento](events.md), [ciclo vital](lifecycle-data.md), y [identidad](identity.md) Los datos que ha recopilado y enviado a Platform Edge Network en lecciones anteriores se reenvían a los servicios configurados en su conjunto de datos, incluido Adobe Experience Platform.


## Requisitos previos

Su organización debe estar aprovisionada y se deben conceder permisos para Adobe Experience Platform.

Si no tiene acceso, puede hacer lo siguiente [omitir esta lección](install-sdks.md).

## Objetivos de aprendizaje

En esta lección, deberá hacer lo siguiente:

* Cree un conjunto de datos de Experience Platform.
* Valide los datos del conjunto de datos.
* Habilite el esquema y el conjunto de datos para el Perfil del cliente en tiempo real.
* Validar datos en el perfil del cliente en tiempo real.
* Valide los datos en el gráfico de identidad.


## Crear un conjunto de datos

Todos los datos que se incorporan correctamente a Adobe Experience Platform se conservan dentro del lago de datos como conjuntos de datos. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan. Consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=es) para obtener más información.

1. Vaya a la interfaz del Experience Platform seleccionándola en el menú 3x3 en la parte superior derecha.
   ![menú de conjuntos de datos](assets/mobile-dataset-menu.png)

1. Seleccionar **[!UICONTROL Conjuntos de datos]** en el menú de navegación izquierdo.

1. **[!UICONTROL Crear conjunto de datos]**.
   ![inicio del conjunto de datos](assets/mobile-dataset-home.png)

1. Seleccione **[!UICONTROL Crear conjunto de datos a partir de esquema]**.
   ![inicio del conjunto de datos](assets/mobile-dataset-create.png)

1. Busque el esquema y seleccione.

1. Seleccione **[!UICONTROL Siguiente]**.
   ![conjunto de datos configurar](assets/mobile-dataset-configure.png)

1. Proporcione un **[!UICONTROL Nombre]**, **[!UICONTROL Descripción]** y seleccione **[!UICONTROL Finalizar]**.
   ![fin de conjunto de datos](assets/mobile-dataset-finish.png)

## Actualizar la secuencia de datos

Una vez creado el conjunto de datos, asegúrese de lo siguiente [actualizar la secuencia de datos](create-datastream.md) para añadir Adobe Experience Platform. Esta actualización garantiza que los datos fluyan a Platform.

## Validación de datos en el conjunto de datos

Ahora que ha creado un conjunto de datos y ha actualizado el conjunto de datos para enviar datos al Experience Platform, todos los datos XDM enviados a Platform Edge Network se reenvían a Platform y aterrizan en el conjunto de datos.

Abra la aplicación y vaya a las pantallas donde realiza el seguimiento de eventos. También puede almacenar en déclencheur las métricas del ciclo vital.

Abra el conjunto de datos en la interfaz de Platform. Debería ver los datos que llegan en lotes al conjunto de datos

![validar lotes de conjuntos de datos de Platform de aterrizaje de datos](assets/mobile-platform-dataset-batches.png)

También debería poder ver registros y campos de ejemplo utilizando **[!UICONTROL Previsualizar conjunto de datos]** función:
![validar ciclo de vida enviado a conjunto de datos de Platform](assets/mobile-lifecycle-platform-dataset.png)

Una herramienta más sólida para validar datos es la [servicio de consultas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=es).

## Activar perfil de cliente en tiempo real

El perfil del cliente en tiempo real de Experience Platform le permite crear una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los distintos datos de clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción de clientes.

### Habilitar el esquema

1. Abra el esquema
1. Activar **[!UICONTROL Perfil]**
1. Seleccionar **[!UICONTROL Los datos de este esquema contienen una identidad principal en el campo identityMap.]** en el modal
1. **[!UICONTROL Guardar]** el esquema

   ![habilitar el esquema para el perfil](assets/mobile-platform-profile-schema.png)

### Habilitar el conjunto de datos

1. Abra el conjunto de datos
1. Activar **[!UICONTROL Perfil]**

   ![habilitar el conjunto de datos para el perfil](assets/mobile-platform-profile-dataset.png)

### Validar datos en el perfil

Abra la aplicación y vaya a las pantallas donde realiza el seguimiento de eventos. Inicie sesión en la aplicación de Luma y realice una compra.

Use Assurance para encontrar una de las identidades pasadas en identityMap (correo electrónico, lumaCrmId o ECID):

>[!TIP]
>
>   El valor del `lumaCrmId` es `112ca06ed53d3db37e4cea49cc45b71e`


![obtener un valor de identidad](assets/mobile-platform-identity.png)

En la interfaz de Platform, vaya a **[!UICONTROL Perfiles]** > **[!UICONTROL Examinar]**, busque el valor de identidad que acaba de tomar y abra el perfil:

![búsqueda de un valor de identidad](assets/mobile-platform-profile-lookup.png)

En el **[!UICONTROL Detalle]** pantalla puede ver información básica sobre el usuario, incluido el **[!UICONTROL ** identidades vinculadas **]**:
![detalles del perfil](assets/mobile-platform-profile-details.png)

En el **[!UICONTROL Eventos]**, puede ver los eventos recopilados desde la implementación de la aplicación móvil para este usuario:

![eventos de perfil](assets/mobile-platform-profile-events.png)


En la pantalla de detalles del perfil, haga clic en el vínculo para ver el gráfico de identidad o ir a **[!UICONTROL Identidades]** > **[!UICONTROL Gráfico de identidad]** y busque el valor de identidad. Esta visualización muestra todas las identidades vinculadas en un perfil y su origen. Este es un ejemplo de gráfico de identidad construido a partir de datos recopilados al completar este tutorial del SDK móvil (fuente de datos 2) y el [Tutorial de SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es) (Fuente de datos 1):

![obtener un valor de identidad](assets/mobile-platform-profile-identitygraph.png)

Los especialistas en marketing y análisis pueden hacer mucho más con los datos capturados en Experience Platform, incluido analizarlos en Customer Journey Analytics y crear segmentos en Real-time Customer Data Platform. ¡Ha tenido un buen comienzo!

Siguiente: **[Mensajería push con Journey Optimizer](journey-optimizer-push.md)**

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK móvil de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
