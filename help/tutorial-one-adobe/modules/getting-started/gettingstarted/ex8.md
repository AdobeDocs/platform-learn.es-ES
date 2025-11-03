---
title: 'Introducción: configuración de Postman'
description: 'Introducción: configuración de Postman'
kt: 5342
doc-type: tutorial
exl-id: fc1ee238-cce8-40a9-aba7-3605019a0077
source-git-commit: 899cb9b17702929105926f216382afcde667a1b6
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 3%

---

# Opción 2: configuración de PostBuster

>[!IMPORTANT]
>
>Si no eres empleado de Adobe, sigue las instrucciones para [instalar Postman](./ex7.md){target="_blank"}. Las siguientes instrucciones están destinadas únicamente a empleados de Adobe.

## Vídeo

En este vídeo, obtendrá una explicación y una demostración de todos los pasos involucrados en este ejercicio.

>[!VIDEO](https://video.tv.adobe.com/v/3476496?quality=12&learn=on)

## Instalar PostBuster

Vaya a [https://adobe.service-now.com/esc?id=adb_esc_kb_article&sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&sysparm_article=KB0020542){target="_blank"}.

Haga clic para descargar la última versión de **PostBuster**.

![PostBuster](./images/pb1.png)

Descargue la versión correcta para su sistema operativo.

![PostBuster](./images/pb2.png)

Una vez que la descarga haya finalizado y se haya instalado, abra PostBuster. Entonces debería ver esto. Haga clic en **Importar**.

![PostBuster](./images/pb3.png)

Descargue [postbuster.json.zip](./../../../assets/postman/postbuster.json.zip){target="_blank"} y extráigalo en su escritorio.

![PostBuster](./images/pbpb.png)

Haga clic en **Elegir un archivo**.

![PostBuster](./images/pb4.png)

Seleccione el archivo **postbuster.json**. Haga clic en **Abrir**.

![PostBuster](./images/pb5.png)

Entonces debería ver esto. Haga clic en **Analizar**.

![PostBuster](./images/pb6.png)

Haga clic en **Importar**.

![PostBuster](./images/pb7.png)

Entonces debería ver esto. Haga clic en para abrir la colección importada.

![PostBuster](./images/pb8.png)

Ahora verá su colección. Aún debe configurar un entorno para mantener algunas variables de entorno.

![PostBuster](./images/pb9.png)

Haga clic en **Entorno base** y luego haga clic en el icono **editar**.

![PostBuster](./images/pb10.png)

Entonces debería ver esto.

![PostBuster](./images/pb11.png)

Copie el siguiente marcador de posición de entorno y péguelo en el **Entorno base**; para ello, reemplace lo que se encuentra allí.

```json
{
	"CLIENT_SECRET": "",
	"API_KEY": "",
	"ACCESS_TOKEN": "",
	"SCOPES": [
		"openid",
		"AdobeID",
		"read_organizations", 
		"additional_info.projectedProductContext", 
		"session",
		"ff_apis",
		"firefly_api",
		"frame.s2s.all"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"AZURE_STORAGE_URL": "",
	"AZURE_STORAGE_CONTAINER": "",
	"AZURE_STORAGE_SAS_READ": "",
	"AZURE_STORAGE_SAS_WRITE": "",
	"FRAME_IO_BASE_URL": "https://api.frame.io",
	"FRAME_IO_ACCOUNT_ID": "",
	"FRAME_IO_WORKSPACE_ID": ""
}
```

Entonces deberías tener esto.

![PostBuster](./images/pb12.png)

## Introduzca las variables de Adobe I/O

Vaya a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"} y abra el proyecto.

![Nueva integración de Adobe I/O](./images/iopr.png)

Vaya a **OAuth Server-to-Server**.

![Nueva integración de Adobe I/O](./images/iopbvar1.png)

Ahora debe copiar los siguientes valores del proyecto de Adobe I/O y pegarlos en el entorno base de PostBuster.

- ID de cliente
- Secreto de cliente (haga clic en **Recuperar secreto de cliente**)
- ID de cuenta técnica
- ID de organización (desplácese hacia abajo para buscar el ID de su organización)

![Nueva integración de Adobe I/O](./images/iopbvar2.png)

Copie las variables anteriores una por una y péguelas en su **Entorno base** en PostBuster.

| Nombre de variable en Adobe I/O | Nombre de variable en el entorno base PostBuster |
|:-------------:| :---------------:| 
| ID de cliente | `API_KEY` |
| Secreto del cliente | `CLIENT_SECRET` |
| ID de cuenta técnica | `TECHNICAL_ACCOUNT_ID` |
| ID de organización | `IMS_ORG` |

Después de haber copiado estas variables una por una, su entorno base PostBuster debería tener este aspecto.

Haga clic en **Cerrar**.

![Nueva integración de Adobe I/O](./images/iopbvar3.png)

En la colección **Adobe IO - OAuth**, seleccione la solicitud **POST - Obtener token de acceso** y seleccione **Enviar**.

![Nueva integración de Adobe I/O](./images/iopbvar3a.png)

Debería ver una respuesta similar que contenga la siguiente información:

| Clave | Valor |
|:-------------:| :---------------:| 
| token_type | **portador** |
| access_token | **KeyJhbGciOiJS...** |
| expires_in | **86399** |

El **token de portador** de Adobe I/O tiene un valor específico (el token de acceso muy largo) y un período de caducidad, y ahora es válido durante 24 horas. Esto significa que, después de 24 horas, si desea utilizar Postman para interactuar con las API de Adobe, deberá generar un nuevo token ejecutando esta solicitud de nuevo.

![Nueva integración de Adobe I/O](./images/iopbvar4.png)

El entorno PostBuster ya está configurado y funciona. Ahora ha completado este ejercicio.

## Pasos siguientes

Ir a [Aplicaciones para instalar](./ex9.md){target="_blank"}

Volver a [Introducción](./getting-started.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
