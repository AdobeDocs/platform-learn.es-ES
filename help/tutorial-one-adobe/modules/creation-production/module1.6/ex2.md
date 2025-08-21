---
title: GenStudio for Performance Marketing Cree su Amazon AWS S3 bucket
description: GenStudio for Performance Marketing Cree su Amazon AWS S3 bucket
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 044677e4-7ca3-4dfe-9067-640983681ea7
source-git-commit: 1f9a868c5e4ef4aa0e09d7f5d73a951006ee6c5a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 7%

---

# 1.6.2 Crear el contenedor de AWS S3

## 1.6.2.1 Crear su S3 bucket

Vaya a [https://console.aws.amazon.com](https://console.aws.amazon.com) e inicie sesión.

>[!NOTE]
>
>Si todavía no tiene una cuenta de AWS, cree una nueva cuenta de AWS con su dirección de correo electrónico personal.

![ETL](./images/awshome.png)

Después de iniciar sesión, se le redirigirá a **AWS Management Console**.

![ETL](./images/awsconsole.png)

En la barra de búsqueda, busque **s3**. Haga clic en el primer resultado de búsqueda: **S3 - Almacenamiento escalable en la nube**.

![ETL](./images/awsconsoles3.png)

Luego verá la página principal de **Amazon S3**. Haga clic en **Crear cubo**.

![ETL](./images/s3home.png)

En la pantalla **Crear cubo**, use el nombre `--aepUserLdap---gspem-dam`.

![ETL](./images/bucketname.png)

Mantenga el resto de configuraciones predeterminadas tal cual. Desplácese hacia abajo y haga clic en **Crear cubo**.

![ETL](./images/createbucket.png)

A continuación, verá que se está creando su contenedor y se redirigirá a la página principal de Amazon S3.

![ETL](./images/S3homeb.png)

## Definición de permisos para acceder al compartimento de S3

El siguiente paso es configurar el acceso a su S3 bucket.

Para ello, vaya a [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home).

El acceso a los recursos de AWS está controlado por Identity and Access Management (IAM) de Amazon.

Ahora verá esta página.

![ETL](./images/iam.png)

En el menú de la izquierda, haga clic en **Usuarios**. Luego verá la pantalla **Usuarios**. Haga clic en **Crear usuario**.

![ETL](./images/iammenu.png)

A continuación, configure el usuario:

- Nombre de usuario: use `s3_--aepUserLdap--_gspem_dam`

Haga clic en **Next**.

![ETL](./images/configuser.png)

Entonces verá esta pantalla de permisos. Haga clic en **Adjuntar directivas directamente**.

![ETL](./images/perm1.png)

Escriba el término de búsqueda **s3** para ver todas las directivas de S3 relacionadas. Seleccione la directiva **AmazonS3FullAccess**. Desplácese hacia abajo y haga clic en **Siguiente**.

![ETL](./images/perm2.png)

Revise la configuración. Haga clic en **Crear usuario**.

![ETL](./images/review.png)

Entonces verá esto... Haga clic en **Ver usuario**.

![ETL](./images/review1.png)

Haga clic en **Credenciales de seguridad** y luego haga clic en **Crear clave de acceso**.

![ETL](./images/cred.png)

Seleccione **Aplicación que se ejecuta fuera de AWS**. Desplácese hacia abajo y haga clic en **Siguiente**.

![ETL](./images/creda.png)

Haga clic en **Crear clave de acceso**

![ETL](./images/credb.png)

Entonces verá esto... Haz clic en **Mostrar** para ver tu clave de acceso secreta:

![ETL](./images/cred1.png)

Tu **clave secreta de acceso** se está mostrando.

>[!IMPORTANT]
>
>Almacene sus credenciales en un archivo de texto en su equipo.
>
> - Id. de clave de acceso: ...
> - Clave de acceso secreta: ...
>
> Una vez que hagas clic en **Listo**, nunca volverás a ver tus credenciales.

Haga clic en **Finalizado**.

![ETL](./images/cred2.png)

Ahora ha creado correctamente un contenedor de AWS S3 y ha creado un usuario con permisos para acceder a este contenedor.

## 1.6.2.2 Cargar Assets en el contenedor de S3

En la barra de búsqueda, busque **s3**. Haga clic en el primer resultado de búsqueda: **S3 - Almacenamiento escalable en la nube**.

![ETL](./images/bucket1.png)

Haga clic para abrir el contenedor de S3 recién creado, que debe llamarse `--aepUserLdap---gspem-dam`.

![ETL](./images/bucket2.png)

Haga clic en **Cargar**.

![ETL](./images/bucket3.png)

Entonces debería ver esto.

![ETL](./images/bucket4.png)

Puede descargar los archivos de imagen de CitiSignal [aquí](./images/package.zip){target="_blank"}.

Exporte los archivos al escritorio.

![ETL](./images/bucket5.png)

Haga clic en **Agregar carpeta**.

![ETL](./images/bucket6.png)

Seleccione la carpeta **assets** de la carpeta de descarga **package**. Haga clic en **Cargar**.

![ETL](./images/bucket7.png)

Entonces debería ver esto. Vuelva a hacer clic en **Agregar carpeta**.

![ETL](./images/bucket8.png)

Seleccione la carpeta **miniaturas** de la carpeta de descarga **paquete**. Haga clic en **Cargar**.

![ETL](./images/bucket9.png)

Entonces debería ver esto. Haga clic en **Cargar**.

![ETL](./images/bucket10.png)

La carga ha finalizado. Haga clic en **Cerrar**.

![ETL](./images/bucket11.png)

Ahora debería tener esta estructura de carpetas en el compartimento de S3.

![ETL](./images/bucket12.png)

## Pasos siguientes

Vaya a [Crear su aplicación DAM externa](./ex3.md){target="_blank"}

Volver a [GenStudio for Performance Marketing - Extensibilidad](./genstudioext.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
