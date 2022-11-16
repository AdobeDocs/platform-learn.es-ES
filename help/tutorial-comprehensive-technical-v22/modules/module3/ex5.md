---
title: Foundation - Perfil del cliente en tiempo real - Crear un segmento - API
description: Foundation - Perfil del cliente en tiempo real - Crear un segmento - API
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 3f537efd-7281-4c0c-b809-97f266a2a337
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 3%

---

# 3.5 Crear un segmento: API

En este ejercicio, utilizará Postman y Adobe I/O para crear un segmento y almacenar los resultados de ese segmento como un conjunto de datos, mediante el uso de las API de Adobe Experience Platform.

## Historia

En el Perfil del cliente en tiempo real, todos los datos de perfil se muestran junto con los datos de evento y las suscripciones a segmentos existentes. Los datos mostrados pueden provenir de cualquier lugar, desde aplicaciones de Adobe y soluciones externas. Esta es la vista más poderosa de Adobe Experience Platform, el sistema de registro de experiencias.

## Ejercicio 3.5.1: crear un segmento a través de la API de plataforma

Vaya a Postman.

Busque la colección: **Habilitación de _Adobe Experience Platform**. En esta colección, verá una carpeta **2. Segmentación**. En este ejercicio utilizaremos estas solicitudes.

![Segmentación](./images/pmdtl.png)

A continuación, realizaremos todos los pasos necesarios para crear un segmento a través de la API. Vamos a crear un segmento simple: &quot;**ldap** - Todas las clientes femeninas&quot;.

### Paso 1: Creación de una definición de segmento

Haga clic en la solicitud denominada **Paso 1: Perfil: Creación De Una Definición De Segmento**.

![Segmentación](./images/s1_call.png)

Vaya a la **Cuerpo** de esta solicitud.

![Segmentación](./images/s1_body.png)

En el **Cuerpo** de esta solicitud, verá lo siguiente:

![Segmentación](./images/s1_bodydtl.png)

El idioma utilizado para esta solicitud se denomina Idioma de consulta de perfil o **PQL**.

Puede encontrar más información y documentación sobre PQL [here](https://experienceleague.adobe.com/docs/experience-platform/segmentation/pql/overview.html?lang=en).


Atención: actualice la variable **name** en la siguiente solicitud sustituyendo **ldap** con su **ldap**.

```json
{
    "name" : "ldap - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "ldap",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

Después de agregar el **ldap**, el cuerpo debe tener un aspecto similar al siguiente:

```json
{
    "name" : "vangeluw - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "vangeluw",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

También debe verificar el **Encabezado** - campos de su solicitud. Vaya a **Encabezados**. Verá esto:

![Postman](./images/s1_h.png)

| Clave | Valor |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Debe especificar el nombre del simulador para pruebas de Adobe Experience Platform que está utilizando. El nombre del x-sandbox debe ser `--aepSandboxId--`.

Ahora, haga clic en el azul **Enviar** para crear el segmento y ver los resultados.

![Segmentación](./images/s1_bodydtl_results.png)

Después de este paso, puede ver la definición del segmento en la interfaz de usuario de Platform. Para comprobar esto, inicie sesión en Adobe Experience Platform y vaya a **Segmentos**.

![Segmentación](./images/s1_segmentdef.png)

### Paso 2: Creación de un trabajo de POST de segmentos

En el ejercicio anterior, creó un _streaming_ segmento. Un segmento de transmisión evalúa continuamente las cualificaciones en tiempo real. Lo que estás haciendo aquí, es crear un _batch_ segmento. El segmento por lotes le ofrece una vista previa de cómo podría verse el segmento en términos de cualificaciones, pero _eso no significa que el segmento se haya ejecutado_. Actualmente, _nadie califica para este segmento_. Para que las personas califiquen, el segmento por lotes debe ejecutarse, que es exactamente lo que haremos aquí.

Ahora vamos a POST de un trabajo de segmento.

Vaya a Postman.

![Segmentación](./images/pmdtl.png)

En la colección de Postman, haga clic en la solicitud denominada **Paso 2: Trabajo de segmentos de POST** para abrirlo.

![Segmentación](./images/s2_call.png)

También debe verificar el **Encabezado** - campos de su solicitud. Vaya a **Encabezados**. Verá esto:

![Postman](./images/s2headers.png)

| Clave | Valor |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Debe especificar el nombre del simulador para pruebas de Adobe Experience Platform que está utilizando. El nombre del x-sandbox debe ser `--aepSandboxId--`.

Haga clic en el azul **Enviar** botón.

Debería ver un resultado similar:

![Segmentación](./images/s2_call_response.png)

Este trabajo de segmento se está ejecutando y esto puede tardar algún tiempo. En el paso 3, podrá comprobar el estado de este trabajo.


### Paso 3: Estado del trabajo del segmento de GET

Vaya a Postman.

![Segmentación](./images/pmdtl.png)

En la colección de Postman, haga clic en la solicitud denominada **Paso 3: Estado del trabajo del segmento de GET**.

![Segmentación](./images/s3_call.png)

También debe verificar el **Encabezado** - campos de su solicitud. Vaya a **Encabezados**. Verá esto:

![Postman](./images/s3headers.png)

| Clave | Valor |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Debe especificar el nombre del simulador para pruebas de Adobe Experience Platform que está utilizando. El nombre del x-sandbox debe ser `--aepSandboxId--`.

Haga clic en el azul **Enviar** botón.

Debería ver un resultado similar:

![Segmentación](./images/s3_status.png)

En este ejemplo, la variable **status** del trabajo está configurado en **EN COLA**.

Repita esta solicitud haciendo clic en el botón azul **Enviar** cada par de minutos hasta **status** está configurado como **CORRECTO**.

![Segmentación](./images/s3_status_succeeded.png)

Una vez que el estado sea **CORRECTO**, su trabajo de segmento se ha ejecutado y los clientes ahora cumplen los requisitos para el segmento.

Felicidades, ha completado correctamente el ejercicio de segmentación. Ahora veamos cómo se puede activar el Perfil del cliente en tiempo real en toda la empresa.

Paso siguiente: [3.6 Consulte su Perfil del cliente en tiempo real en acción en el Centro de llamadas](./ex6.md)

[Volver al módulo 3](./real-time-customer-profile.md)

[Volver a todos los módulos](../../overview.md)
