---
title: PostBuster - Empleados de Adobe
description: PostBuster - Empleados de Adobe
doc-type: multipage-overview
source-git-commit: 7b559bc183dbabdb0100681b675cd3c3b8123ba6
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# PostBuster

>[!IMPORTANT]
>
>Las siguientes instrucciones están destinadas únicamente a empleados de Adobe.

## Instalar PostBuster

Vaya a [https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542).

Haga clic para descargar la última versión de **PostBuster**.

![PostBuster](./assets/images/pb1.png)

Descargue la versión correcta para su sistema operativo.

![PostBuster](./assets/images/pb2.png)

Una vez que la descarga haya finalizado y se haya instalado, abra PostBuster. Entonces debería ver esto. Haga clic en **Importar**.

![PostBuster](./assets/images/pb3.png)

Descargue [postbuster.json.zip](./assets/postman/postbuster.json.zip) y extráigalo en su escritorio.

![PostBuster](./assets/images/pbpb.png)

Haga clic en **Elegir un archivo**.

![PostBuster](./assets/images/pb4.png)

Seleccione el archivo **postbuster.json**. Haga clic en **Abrir**.

![PostBuster](./assets/images/pb5.png)

Entonces debería ver esto. Haga clic en **Analizar**.

![PostBuster](./assets/images/pb6.png)

Haga clic en **Importar**.

![PostBuster](./assets/images/pb7.png)

Entonces debería ver esto. Haga clic en para abrir la colección importada.

![PostBuster](./assets/images/pb8.png)

Ahora verá su colección. Aún debe configurar un entorno para mantener algunas variables de entorno.

![PostBuster](./assets/images/pb9.png)

Haga clic en **Entorno base** y luego haga clic en el icono **editar**.

![PostBuster](./assets/images/pb10.png)

Entonces debería ver esto.

![PostBuster](./assets/images/pb11.png)

Copie el siguiente marcador de posición de entorno y péguelo en el **Entorno base**.

```json
{
	"CLIENT_SECRET": "",
	"API_KEY": "",
	"ACCESS_TOKEN": "",
	"SCOPES": [
		"openid",
		"AdobeID",
		"ff_apis",
		"firefly_api"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"AZURE_STORAGE_URL": "",
	"AZURE_STORAGE_CONTAINER": "",
	"AZURE_STORAGE_SAS_READ": "",
	"AZURE_STORAGE_SAS_WRITE": ""
}
```

Entonces deberías tener esto.

![PostBuster](./assets/images/pb12.png)

Después de pasar por el módulo **Servicios de Firefly**, su entorno debería tener este aspecto. No es necesario que haga esto ahora, ya que se abordará en una fase posterior.

![PostBuster](./assets/images/pb13.png)

>[!NOTE]
>
>![Perspectivas técnicas](./assets/images/techinsiders.png){width="50px" align="left"}
>
>Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, póngase en contacto directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.

[Volver a todos los módulos](./overview.md)
