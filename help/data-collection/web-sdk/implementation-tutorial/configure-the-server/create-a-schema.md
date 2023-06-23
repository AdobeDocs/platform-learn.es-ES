---
title: Creación de un esquema
description: Creación de un esquema
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 25d77367-046d-46bd-9640-60fbcea263da
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# Creación de un esquema

Como se explica en [Estructuración de los datos](../structuring-your-data.md), los datos enviados a Adobe Experience Platform deben estar en XDM. Más específicamente, los datos deben coincidir con un _esquema_. Un esquema es básicamente una descripción de la apariencia que deben tener los datos. Describe los nombres de los campos y dónde deben ubicarse dentro de los datos. También describe el tipo de valor que debe tener cada campo (por ejemplo, un booleano, una cadena con una longitud de 12 caracteres, una matriz de números).

Adobe Experience Platform proporciona algunos componentes integrados conocidos como grupos de campos que son comunes en el sector. Por ejemplo, para el sector de los servicios financieros, hay grupos de campos para transferencias de saldo y solicitudes de préstamos. Para la industria de viajes y hospitalidad, hay grupos de campo para reservas de vuelo y alojamiento.

Le recomendamos que utilice los grupos de campos integrados siempre que sea posible al crear el esquema. También entendemos que puede necesitar campos específicos de su propia compañía. Por este motivo, puede crear sus propios grupos de campos personalizados para utilizarlos dentro de los esquemas que cree.

Veamos la creación de un esquema para un sitio web de comercio electrónico típico.

En primer lugar, vaya a [!UICONTROL Esquemas] vista dentro de Adobe Experience Platform.

![Vista de esquemas](../../../assets/implementation-strategy/schemas-view.png)

Seleccionar [!UICONTROL Crear esquema] en la esquina superior derecha. Se muestra un menú. Seleccionar [!UICONTROL ExperienceEvent de XDM].

En este punto, se debe mostrar un cuadro de diálogo preguntándole qué grupos de campos desea agregar al esquema. El primer grupo de campos que se debe seleccionar es el grupo de campos denominado [!UICONTROL ExperienceEvent del SDK web de AEP]. Este grupo de campos agrega un conjunto de campos que admiten los datos recopilados automáticamente por el SDK web de Adobe Experience Platform.

![Mezcla de SDK web de AEP](../../../assets/implementation-strategy/aep-web-sdk-mixin.png)

Dado que el sitio web de este tutorial es un sitio web de comercio electrónico, también debe seleccionar [!UICONTROL Detalles de comercio] grupo de campos. Este grupo le permite enviar datos de comercio típicos, como qué productos se ven, se agregan al carro de compras y se compran.

![Combinación de detalles de Commerce](../../../assets/implementation-strategy/commerce-details-mixin.png)

Haga clic en [!UICONTROL Adición de grupos de campos] en la parte superior derecha del cuadro de diálogo. En este punto, debería ver la estructura del esquema.

![Esquema con mixins](../../../assets/implementation-strategy/schema-with-mixins.png)

Los grupos de campos que ha agregado se muestran a la izquierda. Al seleccionar un grupo de campos, se resaltan los campos de la derecha que proporcionó dicho grupo de campos. Dedique un momento a explorar los campos disponibles.

Finalmente, seleccione [!UICONTROL Esquema sin título] hacia la izquierda de la pantalla, proporcione un nombre y una descripción a la derecha de la pantalla y haga clic en [!UICONTROL Guardar].

![Esquema con nombre y descripción](../../../assets/implementation-strategy/schema-name-description.png)

Se ha creado su esquema. A continuación, vamos a aprender a crear un conjunto de datos para albergar los datos.

Para obtener más información sobre la creación de esquemas, consulte [Creación de un esquema (IU)](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=es).
