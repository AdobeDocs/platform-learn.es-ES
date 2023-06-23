---
title: Crear una propiedad de etiquetas de Adobe Experience Platform e instalar extensiones
description: Crear una propiedad de etiquetas de Adobe Experience Platform e instalar extensiones
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 7403059f-b34c-48e0-9efe-b2db7a9afb27
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# Crear una propiedad de etiquetas de Adobe Experience Platform e instalar extensiones

Ahora que el código en la página está insertando datos y eventos en la capa de datos, es hora de que el experto en marketing lea los datos de la capa de datos y los envíe a Adobe Experience Platform. Esto suele requerir dos bibliotecas de JavaScript:

* Capa de datos del cliente de Adobe: en pasos anteriores, creó una matriz de capas de datos e insertó objetos en ella. Para acceder a los datos, debe cargar la biblioteca JavaScript de la capa de datos del cliente de Adobe, que proporciona formas de recibir notificaciones de cambios y eventos de la capa de datos y también proporciona formas sencillas de acceder a los datos.
* SDK web de Adobe Experience Platform: esta biblioteca JavaScript se comunica con Adobe Experience Platform Edge Network. El SDK gestiona la identidad, el consentimiento, la recopilación de datos, la personalización, las audiencias y mucho más.

Aunque puede cargar estas bibliotecas individuales en su sitio web y utilizarlas directamente, le recomendamos que utilice [Etiquetas de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es). Con las etiquetas, puede incrustar una sola secuencia de comandos en el HTML y utilizar la interfaz de usuario de etiquetas para implementar tanto la capa de datos del cliente de Adobe como el SDK web de Adobe Experience Platform. Las etiquetas también permiten crear reglas para enviar datos, entre otras cosas. Este tutorial utiliza las etiquetas para este fin y supone que tiene una comprensión básica del funcionamiento de las etiquetas.

## Creación de una propiedad en Etiquetas

Si aún no lo ha hecho, [crear una propiedad en Etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## Instalación de la extensión de capa de datos del cliente de Adobe

Instale la extensión de la capa de datos del cliente de Adobe navegando hasta el catálogo de extensiones, buscando la extensión y haciendo clic en el correspondiente [!UICONTROL Instalar] botón. Debería ver una pantalla de configuración.

![Instalación de la extensión de capa de datos del cliente de Adobe](../../../assets/implementation-strategy/acdl-extension-installation.png)

Para este tutorial, no es necesario cambiar los valores predeterminados. Haga clic en [!UICONTROL Guardar].

## Instalación de la extensión SDK para web de Adobe Experience Platform

A continuación, instale la extensión SDK para web de Adobe Experience Platform buscando la extensión en el catálogo de extensiones y haciendo clic en la [!UICONTROL Instalar] botón. Debería ver una pantalla de configuración.

![Instalación de la extensión del SDK web de Adobe Experience Platform](../../../assets/implementation-strategy/web-sdk-extension-installation.png)

Entrada [Creación de una secuencia de datos](../configure-the-server/create-a-datastream.md), ha creado una secuencia de datos a la que Adobe Experience Platform Edge Network hace referencia para determinar dónde enviar los datos de entrada. Al realizar solicitudes desde el SDK web de Adobe Experience Platform a la red perimetral, debe indicar a qué secuencia de datos de la red perimetral debe hacer referencia.

Para ello, busque el [!UICONTROL Datastream] y seleccione la secuencia de datos creada anteriormente. Se le presentarán los mismos entornos de flujo de datos que vio en [Creación de una secuencia de datos](../configure-the-server/create-a-datastream.md).

![Selección de flujo de datos](../../../assets/implementation-strategy/web-sdk-datastream-selection.png)

Como se explica en [Creación de una secuencia de datos](../configure-the-server/create-a-dataset.md)Sin embargo, estos entornos de conjuntos de datos tienen una relación con los entornos de Etiquetas. Supongamos durante un momento que completa la instalación de la extensión del SDK web de Adobe Experience Platform, crea una biblioteca de etiquetas que incluye la extensión y, a continuación, publica la biblioteca en un entorno de desarrollo de etiquetas. Cuando la biblioteca de etiquetas se carga en la página web y la extensión del SDK web de Adobe Experience Platform realiza una solicitud a Edge Network, la extensión incluye el [!UICONTROL Entorno de desarrollo] ID de entorno de flujo de datos. Edge Network, a su vez, utiliza ese ID para leer la configuración del [!UICONTROL Entorno de desarrollo] entorno de flujo de datos y reenviar datos a los productos de Adobe adecuados.

Por el momento, solo tiene un entorno de flujo de datos de desarrollo, un entorno de flujo de datos de ensayo y un entorno de flujo de datos de producción. Por este motivo, la interfaz de usuario de configuración de la extensión muestra todas las extensiones preseleccionadas e inmodificables. Sin embargo, es posible crear varios entornos de desarrollo de flujos de datos (uno para usted y otro para su compañero, quizás) mediante la interfaz de usuario del flujo de datos. Si tuviera varios entornos de flujo de datos de desarrollo, podría seleccionar cuál desea utilizar para esta propiedad de etiqueta.

Por último, desplácese hacia abajo y desmarque [!UICONTROL Habilitar la recopilación de datos de clics]. De forma predeterminada, el SDK realiza automáticamente un seguimiento de los vínculos. Sin embargo, en este tutorial demostraremos cómo puede realizar un seguimiento de sus propios clics en vínculos mediante la información de vínculos personalizados.

Haga clic en [!UICONTROL Guardar] para finalizar la instalación de la extensión SDK para web de Adobe Experience Platform.

Se han instalado las extensiones adecuadas. Es hora de crear reglas y elementos de datos.
