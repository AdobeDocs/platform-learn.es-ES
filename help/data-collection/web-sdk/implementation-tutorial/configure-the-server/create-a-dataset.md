---
title: Crear un conjunto de datos
description: Crear un conjunto de datos
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 7705d292-a29c-4977-bcc6-f088a51713ea
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 4%

---

# Crear un conjunto de datos

Además de describir los datos que enviará a Adobe Experience Platform, necesita un lugar en el que conservar los datos. En Adobe Experience Platform, estos bloques en los que se pueden colocar datos se denominan conjuntos de datos.

Para crear un conjunto de datos, vaya al [!UICONTROL Conjuntos de datos] vista dentro de Adobe Experience Platform.

![Vista Conjuntos de datos](../../../assets/implementation-strategy/datasets-view.png)

Clic [!UICONTROL Crear conjunto de datos] en la esquina superior derecha.

Durante el proceso de creación del conjunto de datos, seleccione [!UICONTROL Crear conjunto de datos a partir de esquema] y seleccione [el esquema que ha creado anteriormente](create-a-schema.md).

![Selección de esquema](../../../assets/implementation-strategy/schema-selection.png)

Clic [!UICONTROL Siguiente] y proporcione un nombre y una descripción.

![Nombre y descripción del conjunto de datos](../../../assets/implementation-strategy/dataset-name-description.png)

Haga clic en [!UICONTROL Finalizar]. Se ha creado el conjunto de datos y está listo para recibir datos.

A medida que empiece a enviar datos a un conjunto de datos, Adobe Experience Platform validará que los datos que intenta colocar en él se ajustan al esquema aplicado. Si los datos no se ajustan al esquema, se rechazarán y no se colocarán en el conjunto de datos. Como resultado de este paso de validación, los consumidores del conjunto de datos (productos de Adobe, terceros o su propia compañía) pueden tener cierto nivel de certeza con respecto a la estructura y la limpieza de los datos del conjunto de datos.

Para obtener más información sobre la creación de conjuntos de datos, consulte [Guía de IU de conjuntos de datos](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=es).
