---
title: Crear un conjunto de datos
description: Crear un conjunto de datos
exl-id: 19a60087-2f78-4510-b127-b1007a6b7a56
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Crear un conjunto de datos

Además de describir los datos que envía a Adobe Experience Platform, necesita un lugar donde conservarlos. En Adobe Experience Platform, estos bloques en los que se pueden colocar datos se denominan conjuntos de datos.

>[!NOTE]
>
>Los conjuntos de datos no son necesarios si solo utiliza el SDK web de Platform para enviar datos a Adobe Analytics, Adobe Target y Adobe Audience Manager o mediante el reenvío de eventos. Si solo utiliza el SDK web para estos fines, puede omitir esta página del tutorial.

1. Select **[!UICONTROL Conjuntos de datos]** under [!UICONTROL Gestión de datos] del menú de la izquierda en Adobe Experience Platform.
1. A continuación, seleccione la **[!UICONTROL Crear conjunto de datos]** en la esquina superior derecha.
   ![Vista Conjuntos de datos](../assets/datasets-view.png)

## Crear un conjunto de datos a partir de un esquema

1. En el [!UICONTROL Flujo de trabajo] interfaz, seleccione el primer mosaico, **[!UICONTROL Crear conjunto de datos a partir del esquema]**.
1. Busque la variable [el esquema que creó anteriormente](create-a-schema.md) y selecciónelo.
   ![Selección de esquema](../assets/schema-selection.png)
1. Select **[!UICONTROL Siguiente]** y proporcione un nombre y una descripción.
   ![Nombre y descripción del conjunto de datos](../assets/dataset-name-description.png)
1. Select **[!UICONTROL Finalizar]**. El conjunto de datos se ha creado y está listo para recibir datos.

A medida que comienza a enviar datos a un conjunto de datos, Adobe Experience Platform valida que los datos que intenta colocar en el conjunto de datos se ajustan al esquema aplicado. Si los datos no se ajustan al esquema, los datos se rechazan y no se colocan en el conjunto de datos. Como resultado de este paso de validación, los consumidores del conjunto de datos (productos de Adobe, terceros o su propia empresa) pueden tener cierto nivel de certeza con respecto a la estructura y limpieza de los datos del conjunto de datos.

Para obtener más información sobre la creación de conjuntos de datos, consulte [Creación de conjuntos de datos e ingesta de datos](/help/platform/data-ingestion/create-datasets-and-ingest-data.md).

[Siguiente: ](create-a-datastream.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre la recopilación de datos. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)

