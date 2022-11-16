---
title: 'Fundamento: configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: explicación de la recopilación de datos de Adobe Experience Platform'
description: 'Fundamento: configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: explicación de la recopilación de datos de Adobe Experience Platform'
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: f498bb8c-659c-44b4-bb2e-36ea14640773
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 6%

---

# 1.1 Explicación de la recopilación de datos de Adobe Experience Platform

## Contexto

Las marcas utilizan la recopilación de datos de Adobe Experience Platform para varios casos de uso. Se trata de un sistema Tag Management (TMS) de próxima generación que ofrece a los clientes una alternativa sencilla para implementar y gestionar todas las soluciones de análisis, marketing y publicidad necesarias para ofrecer al cliente experiencias más relevantes. La recopilación de datos de Adobe Experience Platform no supone ningún coste adicional y está disponible para cualquier cliente de Adobe Experience Cloud. Una marca podría utilizar la recopilación de datos de Adobe Experience Platform para:

- Implemente aplicaciones de Adobe Experience Cloud y Adobe Experience Platform.
- Administre los diferentes requisitos de diferentes partes de la organización al proporcionarles sus propios **Propiedad** para administrar.
- Permiten las pruebas y la administración del ciclo vital.
- Inserte etiquetas de javascript y de terceros personalizadas, todas administradas en un solo lugar.

## Explorar la interfaz de usuario

Vaya a [Recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/#/data-collection/).

Vaya a **Etiquetas**. Ahora está viendo el **[!UICONTROL Propiedades]** vista. Las propiedades enumeradas aquí son para la administración de tutoriales. Estas propiedades representan...

- Propiedades web y de aplicación
- Diferentes sitios web que sirven a los clientes de diferentes maneras. Por ejemplo, Luma Retail tendría una propiedad, Luma Travel tendría otra propiedad
- Sitios web heredados y actuales
- Un diseño específico de Adobe Analytics común a varios sitios web diferentes
- Páginas de intranet internas junto con sitios externos

![Vista Propiedades de Launch](./images/launch1.png)

Ahora, echen un vistazo al carril izquierdo.

![Iniciar carril izquierdo](./images/launch2.png)

- **[!UICONTROL Etiquetas]** proporciona información general sobre todas las propiedades del lado del cliente
- **[!UICONTROL Superficies de la aplicación]** ofrece una descripción general de todas las configuraciones de aplicación para habilitar las notificaciones push (que se utilizan o habilitan en combinación con Project Sierra).
- **[!UICONTROL Datastreams]** se exploran en el [ejercicio siguiente](./ex2.md)
- **[!UICONTROL Reenvío de eventos]** ofrece una descripción general de todas las propiedades del lado del servidor que se exploran en [Módulo 14 - Conexiones de Real-Time CDP: Reenvío de eventos](../module14/aep-data-collection-ssf.md)

## Información adicional

La recopilación de datos de Adobe Experience Platform es una herramienta muy avanzada que tiene mucho más que ver con un tutorial de Adobe Experience Platform. Es posible que las organizaciones no utilicen la recopilación de datos de Adobe Experience Platform para sus funciones de administración de etiquetas y que, en su lugar, usen soluciones de administración de etiquetas que no sean de Adobe para inyectar código y administrar etiquetas. Adobe y Adobe Professional Services admiten el uso de una solución de administración de etiquetas que no sea de Adobe.
A continuación se incluyen otras lecturas para aquellos interesados en comprender mejor la recopilación de datos de Adobe Experience Platform.

- [Guía del usuario de recopilación de datos de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)
- [Tutorial de implementación de Adobe Experience Cloud con SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=es)
- [Configurar permisos de usuario](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html)
- [Documentación de API](https://developer.adobelaunch.com/api/)

Paso siguiente: [1.2 Recopilación de datos del servidor, conjuntos de datos y redes perimetrales](./ex2.md)

[Volver al módulo 1](./data-ingestion-launch-web-sdk.md)

[Volver a todos los módulos](./../../overview.md)
