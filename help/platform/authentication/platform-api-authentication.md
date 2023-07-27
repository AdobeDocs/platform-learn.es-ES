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
source-git-commit: 42427df298e2c5ae734ce050e935378db51e66a1
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 18%

---

# Autenticar y acceder a las [!DNL Experience Platform]API

Obtenga información sobre cómo empezar a usar las API de Adobe Experience Platform. Este tutorial le guía a través del proceso para crear credenciales de autenticación y comenzar a realizar solicitudes de API de Experience Platform.

## Cree un proyecto en la consola de Adobe Developer y exporte un entorno de Postman{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/) es una aplicación de terceros que ayuda a los desarrolladores a interactuar rápida y fácilmente con las API de Adobe Experience Platform.

[La consola de Adobe Developer](https://developer.adobe.com/console/home) **Detalles de exportación para Postman** Esta funcionalidad proporciona una forma sencilla de exportar los detalles de la cuenta necesarios para acceder a las API de Experience Platform e interactuar con ellas en un solo archivo de entorno de Postman, lo que elimina la necesidad de copiar y pegar valores de la consola de Adobe Developer en Postman.

>[!IMPORTANT]
>
>Para acceder a [Consola de Adobe Developer](https://developer.adobe.com/console/home), debe ser un o un [Administrador del sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html) o una [Desarrollador](https://helpx.adobe.com/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.) en el [Adobe Admin Console](https://adminconsole.adobe.com).
>
> Después de crear la credencial de la API, un administrador del sistema debe asociarla con una función en el Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)




## Generación de un token de acceso con Postman{#generate-an-access-token-with-postman}

Utilice el [API del servicio Identity Management de Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) para obtener un token de acceso y acceder a las API de Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## Interacción con las API de Experience Platform mediante Postman

Explore la interacción con las API de Adobe Experience Platform mediante [Colecciones de Postman de API de Experience Platform proporcionadas por el Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), sobre la base de [Variables de entorno de la consola Adobe Developer](#export-integration-details-to-postman) y [token de acceso generado](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## Recursos a los que se hace referencia en estos vídeos

* [Consola de desarrollador de Adobe](https://developer.adobe.com/console/home)
* [Muestras de Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples)
   * [Recopilación de Postman del sistema de Identity Management para generar tokens de acceso](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Colecciones Postman de API de Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Descargar Postman](https://www.postman.com/)
