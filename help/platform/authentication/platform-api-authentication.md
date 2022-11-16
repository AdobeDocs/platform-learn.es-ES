---
title: Autenticación y acceso a las API de Experience Platform
description: Obtenga información sobre cómo acceder a las API de Adobe Experience Platform.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 10%

---

# Autenticar y acceder [!DNL Experience Platform] API

Para realizar llamadas a las API de Adobe Experience Platform, primero debe obtener acceso a una cuenta de desarrollador de Experience Platform.

Para obtener instrucciones paso a paso que describan cómo obtener acceso a una cuenta de desarrollador, visite el [Tutorial de autenticación de API de Experience Platform](https://www.adobe.com/go/platform-api-authentication-en).

## Creación y exportación de la API de Experience Platform a Postman

[Postman](https://www.getpostman.com/) es una herramienta que permite a los desarrolladores interactuar rápida y fácilmente con las API de Adobe Experience Platform.

La consola de Adobe Developer **Detalles de exportación para Postman** ofrece una forma sencilla de exportar todos los detalles de la cuenta necesarios para acceder e interactuar con una API de Experience Platform en un único archivo de entorno de Postman, lo que elimina la necesidad de copiar y pegar valores de la consola de Adobe Developer en Postman.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

## Generar un token de acceso con Postman

Utilice la variable [API del servicio Identity Management de Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) para obtener un token de acceso para acceder a las API de Adobe Experience Platform para uso no productivo

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

>[!WARNING]
>
> Como se indica en la colección Postman de generación de tokens de acceso a Adobe I/O, los métodos de generación indicados son adecuados para usos que no sean de producción. La firma local carga una biblioteca JavaScript desde un host de terceros, y la firma remota envía la clave privada a un servicio web administrado por un Adobe. Aunque Adobe no almacena esta clave privada, las claves de producción nunca deben compartirse con nadie.

## Interacción con las API de Adobe I/O mediante Postman

Explore la interacción con las API de Adobe I/O mediante el [Colecciones Postman de la API de Experience Platform proporcionadas por el Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), basándose en el [Variables de entorno de Adobe I/O](#export-adobe-io-integration-details-to-postman) y [token de acceso generado](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)

Tenga en cuenta que las colecciones de Postman proporcionadas por el Adobe pueden no existir para cada API de Adobe I/O, pero se proporciona el valor [Colecciones Postman de la API de Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform) se puede utilizar como guía para definir sus propias colecciones de Postman para estos casos de uso.

## Recursos adicionales

* [Consola Adobe I/O](https://console.adobe.io)
* [Muestras de Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples)
   * [Recopilación de Postman de generación de tokens de acceso a Adobes I/O](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Colecciones de Postman de las API de Adobe Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Descargar Postman](https://www.getpostman.com/)
