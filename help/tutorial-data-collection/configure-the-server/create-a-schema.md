---
title: Creación de un esquema
description: Creación de un esquema
exl-id: 0256b358-0c2c-4c59-ab23-5fe0d38880d6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Creación de un esquema

Como se explica en [Estructurar los datos](../structuring-your-data.md), los datos enviados a Adobe Experience Platform deben estar en XDM. Más específicamente, los datos deben coincidir con un _esquema_. Un esquema es básicamente una descripción del aspecto que deben tener los datos. Describe los nombres de los campos y dónde deben ubicarse dentro de los datos. También describe el tipo de valor que cada campo debe tener (por ejemplo, un booleano, una cadena con una longitud de 12 caracteres, una matriz de números).

Adobe Experience Platform proporciona algunos componentes básicos listos para usar conocidos como grupos de campos que son comunes en el sector. Por ejemplo, para el sector de los servicios financieros, existen grupos de campo para transferencias de saldos y solicitudes de préstamos. Para la industria de viajes y hospitalidad, hay grupos de campo para reservas de vuelo y alojamiento.

Se recomienda utilizar los grupos de campos integrados siempre que sea posible al crear el esquema. También comprendemos que puede necesitar campos específicos de su propia empresa. Por este motivo, puede crear sus propios grupos de campos personalizados para utilizarlos en los esquemas que cree.

Analicemos la creación de un esquema para un sitio web de comercio electrónico típico.

1. Select **[!UICONTROL Esquemas]** under [!UICONTROL Gestión de datos] en el menú de la izquierda de la interfaz de Adobe Experience Platform.
1. Select **[!UICONTROL Crear esquema]** en la esquina superior derecha, y **[!UICONTROL XDM ExperienceEvent]** en el menú desplegable.

Ahora se encuentra en el lienzo del generador de esquemas.
![Vista Esquemas](../assets/schemas-view.png)

## Agregar grupos de campos

1. En el **[!UICONTROL Grupos de campo]** a la izquierda del **[!UICONTROL Estructura]** seleccione el **[!UICONTROL + Agregar]** vínculo. En este punto, se mostrará un modal para elegir los grupos de campos que se añadirán al esquema.
1. En primer lugar, seleccione el grupo de campos denominado **[!UICONTROL ExperienceEvent del SDK web de AEP]**. Este grupo de campos agrega un conjunto de campos que admiten los datos recopilados automáticamente por el SDK web de Adobe Experience Platform.
   ![Mezcla del SDK web de AEP](../assets/aep-web-sdk-mixin.png)
1. A continuación, como el sitio web de este tutorial es un sitio web de comercio electrónico, seleccione la opción **[!UICONTROL Detalles del comercio]** grupo de campos. Este grupo de campos le permite enviar datos de comercio típicos como los productos que se están viendo, añadidos al carro y comprados.
1. Seleccione el **[!UICONTROL Agregar grupos de campos]** en la parte superior derecha del cuadro de diálogo.
   ![Mezcla de detalles comerciales](../assets/commerce-details-mixin.png)
1. En este punto, debería ver la estructura del esquema.
   ![Esquema con mezclas](../assets/schema-with-mixins.png)

## Guardar el esquema

1. Por último, proporcione un nombre y una descripción a la derecha de la pantalla y seleccione **[!UICONTROL Guardar]**.
   ![Esquema con nombre y descripción](../assets/schema-name-description.png)

Se ha creado el esquema . A continuación, vamos a aprender a crear un conjunto de datos para almacenar sus datos.

Para obtener más información sobre la creación de esquemas, consulte [Crear esquemas](/help/platform/schemas/create-schemas.md).

[Siguiente: ](create-a-dataset.md)

>[!NOTE]
>
>Gracias por invertir su tiempo en obtener información sobre la recopilación de datos. Si tiene alguna pregunta, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Experience League de debate de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
