---
title: Autenticación y acceso a las API de Experience Platform
description: Obtenga información sobre cómo acceder a las API de Adobe Experience Platform.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 60f509ef55ce121f572466a8f13953dba982a0ce
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 15%

---

# Autenticación y acceso [!DNL Experience Platform] API

Para realizar solicitudes a las API de Adobe Experience Platform, debe tener una cuenta de desarrollador de Experience Platform.

## Cree un proyecto en la consola de Adobe Developer y exporte un entorno de Postman

[[!DNL Postman]](https://www.postman.com/) es una herramienta que permite a los desarrolladores interactuar rápida y fácilmente con las API de Adobe Experience Platform.

La consola de Adobe Developer **Detalles de exportación para Postman** Esta funcionalidad proporciona una forma sencilla de exportar todos los detalles de la cuenta necesarios para acceder a una API de Experience Platform e interactuar con ella en un solo archivo de entorno de Postman, lo que elimina la necesidad de copiar y pegar valores de la consola de Adobe Developer en Postman.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

>[!IMPORTANT]
>
>Después de crear la credencial de la API, un administrador del sistema de su empresa debe asociar la credencial con una función de Experience Platform.


## Generación de un token de acceso con Postman

Utilice el [API del servicio Identity Management de Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) para obtener un token de acceso y acceder a las API de Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## Interacción con las API de Experience Platform mediante Postman

Explore la interacción con las API de Adobe Experience Platform mediante [Colecciones de Postman de API de Experience Platform proporcionadas por el Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), sobre la base de [Variables de entorno de la consola Adobe Developer](#export-adobe-io-integration-details-to-postman) y [token de acceso generado](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## Recursos adicionales

* [Consola de desarrollador de Adobe](https://developer.adobe.com/console/home)
* [Muestras de Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples)
   * [Recopilación de Postman del sistema de Identity Management para generar tokens de acceso](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Colecciones Postman de API de Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Descargar Postman](https://www.postman.com/)
