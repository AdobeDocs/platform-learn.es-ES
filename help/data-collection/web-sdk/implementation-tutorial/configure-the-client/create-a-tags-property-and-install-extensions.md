---
title: Creación de una propiedad de etiqueta de Adobe Experience Platform e instalación de extensiones
description: Creación de una propiedad de etiqueta de Adobe Experience Platform e instalación de extensiones
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 7403059f-b34c-48e0-9efe-b2db7a9afb27
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# Creación de una propiedad de etiqueta de Adobe Experience Platform e instalación de extensiones

Ahora que el código en la página está insertando datos y eventos en la capa de datos, es hora de que el especialista en marketing lea los datos de la capa de datos y envíe estos datos a Adobe Experience Platform. Esto generalmente requeriría dos bibliotecas JavaScript:

* Capa de datos del cliente de Adobe: En pasos anteriores, se creó una matriz de capa de datos y se insertaron objetos en ella. Para acceder a los datos, debe cargar la biblioteca JavaScript de la capa de datos del cliente de Adobe, que proporciona formas de recibir notificaciones sobre los cambios y eventos de la capa de datos y también proporciona formas sencillas de acceder a los datos.
* SDK web de Adobe Experience Platform: Esta biblioteca JavaScript se comunica con Adobe Experience Platform Edge Network. El SDK gestiona la identidad, el consentimiento, la recopilación de datos, la personalización, las audiencias y mucho más.

Aunque puede cargar estas bibliotecas individuales en su sitio web y utilizarlas directamente, le recomendamos que utilice [Etiquetas de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es). Con Etiquetas, puede incrustar un solo script en el HTML y utilizar la interfaz de usuario Etiquetas para implementar tanto la capa de datos del cliente de Adobe como el SDK web de Adobe Experience Platform. Las etiquetas también permiten crear reglas para enviar datos, entre otras cosas. Este tutorial utiliza Etiquetas para este fin y supone que dispone de un conocimiento básico del funcionamiento de Etiquetas.

## Crear una propiedad en Etiquetas

Si aún no lo ha hecho, [crear una propiedad en Etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## Instalación de la extensión de la capa de datos del cliente de Adobe

Para instalar la extensión de la capa de datos del cliente de Adobe, vaya al catálogo de extensiones, busque la extensión y haga clic en las [!UICONTROL Instalar] botón. Debería ver una pantalla de configuración.

![Instalación de la extensión de capa de datos del cliente de Adobe](../../../assets/implementation-strategy/acdl-extension-installation.png)

Para este tutorial, no es necesario cambiar los valores predeterminados. Haga clic en [!UICONTROL Guardar].

## Instalación de la extensión del SDK web de Adobe Experience Platform

A continuación, instale la extensión del SDK web de Adobe Experience Platform buscando la extensión en el catálogo de extensiones y haciendo clic en las [!UICONTROL Instalar] botón. Debería ver una pantalla de configuración.

![Instalación de la extensión del SDK web de Adobe Experience Platform](../../../assets/implementation-strategy/web-sdk-extension-installation.png)

En [Crear un conjunto de datos](../configure-the-server/create-a-datastream.md), ha creado un conjunto de datos al que Adobe Experience Platform Edge Network hace referencia para determinar dónde enviar los datos entrantes. Al realizar solicitudes desde el SDK web de Adobe Experience Platform a la red perimetral, debe indicar a qué red perimetral del almacén de datos debe hacer referencia.

Para ello, busque la [!UICONTROL Datastream] y seleccione el conjunto de datos que ha creado anteriormente. Se le presentan los mismos entornos de conjunto de datos que se vieron en [Crear un conjunto de datos](../configure-the-server/create-a-datastream.md).

![Selección del conjunto de datos](../../../assets/implementation-strategy/web-sdk-datastream-selection.png)

Como se explica en [Crear un conjunto de datos](../configure-the-server/create-a-dataset.md), estos entornos de conjuntos de datos tienen una relación con los entornos de etiquetas. Supongamos que completa la instalación de la extensión del SDK web de Adobe Experience Platform, crea una biblioteca de etiquetas que incluya la extensión y, a continuación, publica la biblioteca en un entorno de desarrollo de etiquetas. Cuando la biblioteca de etiquetas se carga en la página web y la extensión del SDK web de Adobe Experience Platform realiza una solicitud a Edge Network, la extensión incluye [!UICONTROL Entorno de desarrollo] ID de entorno de datastream. La red perimetral, a su vez, utiliza ese ID para leer la configuración de la variable [!UICONTROL Entorno de desarrollo] entorno de flujo de datos y reenviar datos a los productos de Adobe correspondientes.

En este momento, solo tiene un entorno de conjunto de datos de desarrollo, un entorno de conjunto de datos de ensayo y un entorno de flujo de datos de producción. Esta es la razón por la que la interfaz de usuario de configuración de la extensión les muestra todos preseleccionados e inmodificables. Sin embargo, es posible crear varios entornos de desarrollo de conjuntos de datos (uno para usted y otro para su compañero, tal vez) utilizando la interfaz de usuario del conjunto de datos. Si tiene varios entornos de conjuntos de datos de desarrollo, puede seleccionar cuál desea utilizar para esta propiedad de etiqueta.

Finalmente, desplácese hacia abajo y desmarque [!UICONTROL Habilitar la recopilación de datos de clic]. De forma predeterminada, el SDK rastrea automáticamente los vínculos. Sin embargo, en este tutorial, demostraremos cómo puede rastrear sus propios clics en vínculos mediante información de vínculos personalizados.

Haga clic en el [!UICONTROL Guardar] para finalizar la instalación de la extensión web SDK de Adobe Experience Platform.

Se han instalado las extensiones adecuadas. Es hora de crear reglas y elementos de datos.
