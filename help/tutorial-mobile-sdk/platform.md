---
title: Envío de datos a Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos a Adobe Experience Platform.
exl-id: fdd2c90e-8246-4d75-a6db-df3ef31946c4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 7%

---

# Envío de datos a Adobe Experience Platform

Obtenga información sobre cómo enviar datos a Adobe Experience Platform.

Esta lección opcional es relevante para todos los clientes de Real-time Customer Data Platform (CDP en tiempo real), Journey Optimizer y Customer Journey Analytics. Experience Platform, la base de los productos de Experience Cloud, es un sistema abierto que transforma todos sus datos (Adobe y no Adobe) en perfiles de cliente sólidos que se actualizan en tiempo real y que utilizan perspectivas controladas por IA para ayudarle a ofrecer las experiencias correctas en todos los canales.

La variable [evento](events.md), [ciclo vital](lifecycle-data.md)y [identidad](identity.md) los datos que haya recopilado y enviado a Platform Edge Network en lecciones anteriores se reenvían a los servicios configurados en el conjunto de datos, incluido Adobe Experience Platform.


## Requisitos previos

Su organización debe estar aprovisionada y se deben conceder permisos para Adobe Experience Platform.

Si no tiene acceso, puede [omitir esta lección](install-sdks.md).

## Objetivos de aprendizaje

En esta lección:

* Cree un conjunto de datos de Experience Platform.
* Valide los datos en el conjunto de datos.
* Habilite el esquema y el conjunto de datos para el perfil del cliente en tiempo real.
* Valide los datos en el perfil del cliente en tiempo real.
* Valide los datos en el gráfico de identidad.


## Crear un conjunto de datos

Todos los datos que se incorporan correctamente en Adobe Experience Platform se conservan dentro del lago de datos como conjuntos de datos. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan. Consulte la [documentación](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=es) para obtener más información.

1. Vaya a la interfaz del Experience Platform seleccionándola en el menú 3x3 en la parte superior derecha.
   ![menú conjunto de datos](assets/mobile-dataset-menu.png)

1. Select **[!UICONTROL Conjuntos de datos]** en el menú de navegación de la izquierda.

1. **[!UICONTROL Crear conjunto de datos]**.
   ![inicio del conjunto de datos](assets/mobile-dataset-home.png)

1. Select **[!UICONTROL Crear conjunto de datos a partir del esquema]**.
   ![inicio del conjunto de datos](assets/mobile-dataset-create.png)

1. Busque el esquema y seleccione .

1. Seleccione **[!UICONTROL Siguiente]**.
   ![configuración del conjunto de datos](assets/mobile-dataset-configure.png)

1. Proporcione un **[!UICONTROL Nombre]**, **[!UICONTROL Descripción]** y seleccione **[!UICONTROL Finalizar]**.
   ![fin del conjunto de datos](assets/mobile-dataset-finish.png)

## Actualizar el conjunto de datos

Una vez que haya creado el conjunto de datos, asegúrese de [actualizar el conjunto de datos](create-datastream.md) para agregar Adobe Experience Platform. Esta actualización garantiza los flujos de datos a Platform.

## Validar datos en el conjunto de datos

Ahora que ha creado un conjunto de datos y actualizado el conjunto de datos para enviar datos al Experience Platform, todos los datos XDM enviados a Platform Edge Network se reenvían a Platform y se dirigen al conjunto de datos.

Abra la aplicación y vaya a las pantallas en las que realiza el seguimiento de eventos. También puede almacenar en déclencheur las métricas del ciclo vital.

Abra el conjunto de datos en la interfaz de Platform. Debería ver los datos que llegan en lotes al conjunto de datos

![validación de lotes de conjuntos de datos de Platform de aterrizaje de datos](assets/mobile-platform-dataset-batches.png)

También debería poder ver ejemplos de registros y campos utilizando la variable **[!UICONTROL Vista previa del conjunto de datos]** función:
![validar el ciclo de vida enviado al conjunto de datos de Platform](assets/mobile-lifecycle-platform-dataset.png)

Una herramienta más sólida para validar datos es Platform [servicio de consultas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=es).

## Habilitar perfil de cliente en tiempo real

El perfil del cliente en tiempo real de Experience Platform le permite crear una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar sus diferentes datos de clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

### Habilitar el esquema

1. Abrir el esquema
1. Habilitar **[!UICONTROL Perfil]**
1. Select **[!UICONTROL Los datos de este esquema contendrán una identidad principal en el campo identityMap .]** en el modal
1. **[!UICONTROL Guardar]** el esquema

   ![habilitar el esquema para el perfil](assets/mobile-platform-profile-schema.png)

### Habilitar el conjunto de datos

1. Abra el conjunto de datos
1. Habilitar **[!UICONTROL Perfil]**

   ![habilitar el conjunto de datos para el perfil](assets/mobile-platform-profile-dataset.png)

### Validación de datos en el perfil

Abra la aplicación y vaya a las pantallas en las que realiza el seguimiento de eventos. Inicie sesión en la aplicación de Luma y realice una compra.

Utilice Assurance para encontrar una de las identidades pasadas en identityMap (Email, lumaCrmId o ECID):

>[!TIP]
>
>   El valor de la variable `lumaCrmId` es `112ca06ed53d3db37e4cea49cc45b71e`


![obtención de un valor de identidad](assets/mobile-platform-identity.png)

En la interfaz de Platform, vaya a **[!UICONTROL Perfiles]** > **[!UICONTROL Examinar]**, busque el valor de identidad que acaba de tomar y abra el perfil:

![buscar un valor de identidad](assets/mobile-platform-profile-lookup.png)

En el **[!UICONTROL Detalle]** puede ver información básica sobre el usuario, incluido el **[!UICONTROL ** identidades vinculadas **]**:
![detalles de perfil](assets/mobile-platform-profile-details.png)

En el **[!UICONTROL Eventos]**, puede ver los eventos recopilados de la implementación de la aplicación móvil para este usuario:

![eventos de perfil](assets/mobile-platform-profile-events.png)


En la pantalla de detalles del perfil, haga clic en el vínculo para ver el gráfico de identidad o navegue hasta **[!UICONTROL Identidades]** > **[!UICONTROL Gráfico de identidad]** y busque el valor de identidad. Esta visualización muestra todas las identidades que están vinculadas en un perfil y su origen. A continuación, se muestra un ejemplo de un gráfico de identidad construido con datos recopilados a partir de la finalización de este tutorial del SDK móvil (fuente de datos 2) y del [Tutorial del SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es) (Fuente de datos 1):

![obtención de un valor de identidad](assets/mobile-platform-profile-identitygraph.png)

Los especialistas en marketing y análisis pueden hacer mucho más con los datos capturados en el Experience Platform, incluido analizarlos en el Customer Journey Analytics y crear segmentos en Real-time Customer Data Platform. ¡Vas a empezar bien!

Siguiente: **[Mensajería push con Journey Optimizer](journey-optimizer-push.md)**

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre el SDK de Adobe Experience Platform Mobile. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
