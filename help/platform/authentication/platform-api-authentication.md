---
title: Autenticación y acceso a las API de Experience Platform
description: Obtenga información sobre cómo acceder a las API de Adobe Experience Platform.
feature: API
role: Developer
level: Beginner
jira: KT-3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 10%

---

# Autenticar y acceder a las API de [!DNL Experience Platform]

Obtenga información sobre cómo empezar a usar las API de Adobe Experience Platform. Este tutorial le guía a través del proceso para crear credenciales de autenticación y comenzar a realizar solicitudes de API de Experience Platform.

## Creación de un proyecto en Adobe Developer Console y exportación de un entorno de Postman{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/) es una aplicación de terceros que ayuda a los desarrolladores a interactuar rápida y fácilmente con las API de Adobe Experience Platform.

La capacidad de [Adobe Developer Console](https://developer.adobe.com/console/home) **Exportar detalles para Postman** proporciona una manera sencilla de exportar los detalles de la cuenta necesarios para acceder a las API de Experience Platform e interactuar con ellas en un solo archivo de entorno de Postman, lo que elimina la necesidad de copiar y pegar valores de Adobe Developer Console en Postman.

>[!IMPORTANT]
>
>Para acceder a [Adobe Developer Console](https://developer.adobe.com/console/home), debes ser [administrador del sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html) o [desarrollador](https://helpx.adobe.com/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.) en [Adobe Admin Console](https://adminconsole.adobe.com).
>
> Después de crear la credencial de la API, un administrador del sistema debe asociarla con una función en Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&enablevpops)

## Generación de un token de acceso con Postman{#generate-an-access-token-with-postman}

Use las [API del servicio Adobe Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) para obtener un token de acceso y poder acceder a las API de Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on&enablevpops)


## Interacción con las API de Experience Platform mediante Postman

Explore la interacción con las API de Adobe Experience Platform mediante las [colecciones Postman de la API de Experience Platform proporcionadas por Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), basadas en las [variables de entorno de Adobe Developer Console](#export-integration-details-to-postman) y en el [token de acceso generado](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on&enablevpops)


## Recursos a los que se hace referencia en estos vídeos

* [Consola de desarrollador de Adobe](https://developer.adobe.com/console/home)
* [Muestras de Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples)
   * [Recopilación de Identity Management System Postman para generar tokens de acceso](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Colecciones Postman de API de Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Descargar Postman](https://www.postman.com/)
