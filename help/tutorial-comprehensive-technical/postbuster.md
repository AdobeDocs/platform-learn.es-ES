---
title: PostBuster - Empleados de Adobe
description: PostBuster - Empleados de Adobe
doc-type: multipage-overview
exl-id: a798e9d7-bb99-4390-885f-5fbd2ef4cee9
source-git-commit: 9c1b30dc0fcca6b4324ec7c8158699fa273cdc90
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# PostBuster

>[!IMPORTANT]
>
>Las siguientes instrucciones están destinadas únicamente a empleados de Adobe.

>[!IMPORTANT]
>
>Siguiendo las instrucciones siguientes, tendrá disponibles todas las colecciones de API necesarias que se utilizarán en estos ejercicios:
>
>- [2.1.3 Visualice su propio perfil de cliente en tiempo real: API](./modules/rtcdp-b2c/module2.1/ex3.md)
>- [2.3.6 Destinos SDK](./modules/rtcdp-b2c/module2.3/ex6.md)
>- [3.3.6 Pruebe su decisión con la API](./modules/ajo-b2c/module3.3/ex6.md)
>- [5.1.8 API de servicio de consulta](./modules/datadistiller/module5.1/ex8.md)

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

Seleccione el archivo **aep_tutorial.json**. Haga clic en **Abrir**.

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
		"read_organizations",
		"additional_info.projectedProductContext",
		"session",
		"ff_apis",
		"firefly_api"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"QS_QUERY_ID": "",
	"SANDBOX_NAME": ""
}
```

Entonces deberías tener esto.

![PostBuster](./assets/images/pb12.png)

Después de crear el proyecto de E/S de Adobe, el entorno debería tener este aspecto. No es necesario que haga esto ahora, ya que se abordará en una fase posterior.

![PostBuster](./assets/images/pb13.png)

>[!NOTE]
>
>![Perspectivas técnicas](./assets/images/techinsiders.png){width="50px" align="left"}
>
>Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, póngase en contacto directamente con Tech Insiders, enviando un correo electrónico a **techinsiders@adobe.com**.

[Volver a todos los módulos](./overview.md)
