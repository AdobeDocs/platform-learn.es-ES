---
title: 'Real-time CDP: cree una audiencia y tome medidas . Envíe su audiencia a un destino de S3'
description: 'Real-time CDP: cree una audiencia y tome medidas . Envíe su audiencia a un destino de S3'
kt: 5342
doc-type: tutorial
exl-id: 4f858d5d-773e-4aee-949c-6031b7d5ca45
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 4%

---

# 2.3.4 Tomar medidas: enviar a su audiencia a un destino S3

Adobe Experience Platform también tiene la capacidad de compartir audiencias con destinos de marketing de correo electrónico como Salesforce Marketing Cloud, Oracle Eloqua, Oracle Responsys y Adobe Campaign.

Puede utilizar FTP o SFTP como parte de los destinos específicos para cada uno de estos destinos de marketing de correo electrónico, o puede utilizar AWS S3 para intercambiar listas de clientes entre Adobe Experience Platform y estos destinos de marketing de correo electrónico.

En este módulo, configurará un destino de este tipo utilizando un contenedor de AWS S3.

## Cree su compartimento de S3

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

En la pantalla **Crear cubo**, use el nombre `aepmodulertcdp--aepUserLdap--`

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

- Nombre de usuario: use `s3_--aepUserLdap--_rtcdp`

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

## Configuración del destino en Adobe Experience Platform

Ir a [Adobe Experience Platform](https://experience.adobe.com/platform). Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la [!UICONTROL zona protegida] adecuada, verá el cambio en la pantalla y ahora se encuentra en la [!UICONTROL zona protegida] dedicada.

![Ingesta de datos](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

En el menú de la izquierda, ve a **Destinos** y luego ve a **Catálogo**. Verá el **Catálogo de destinos**.

![RTCDP](./images/rtcdpmenudest1.png)

Haga clic en **Almacenamiento en la nube** y, a continuación, haga clic en el botón **Configurar** (o en **Activar audiencias**, según su entorno) en la tarjeta **Amazon S3**.

![RTCDP](./images/rtcdp2.png)

Seleccione **Clave de acceso** como Tipo de cuenta. Utilice las credenciales de S3 que se le proporcionaron en el paso anterior:

| Identificador de clave de acceso | Clave de acceso secreta |
|:-----------------------:| :-----------------------:|
| AKIA..... | 7Icm..... |

Haga clic en **Conectar con destino**.

![RTCDP](./images/rtcdpsfs3.png)

A continuación, verá una confirmación visual de que este destino está conectado.

![RTCDP](./images/rtcdpsfs3connected.png)

Debe proporcionar los detalles del compartimento S3 para que Adobe Experience Platform pueda conectarse al compartimento S3.

Como convención de nombres, utilice la siguiente información:

| Identificador de clave de acceso | Clave de acceso secreta |
|:-----------------------:| :-----------------------:|
| Nombre | `AWS - S3 - --aepUserLdap--` |
| Descripción | `AWS - S3 - --aepUserLdap--` |
| Nombre del cubo | `aepmodulertcdp--aepUserLdap--` |
| Ruta de carpeta | /now |

Seleccionar **audiencias**.

Para **Tipo de archivo**, seleccione **CSV** y deje la configuración predeterminada sin cambios.

![RTCDP](./images/rtcdpsfs3connect2.png)

Desplácese hacia abajo. Para **Formato de compresión**, seleccione **Ninguno**. Haga clic en **Next**.

![RTCDP](./images/rtcdpsfs3connect3.png)

Ahora, de forma opcional, puede adjuntar una política de gobernanza de datos a su nuevo destino. Haga clic en **Next**.

![RTCDP](./images/rtcdpsfs3connect2gov.png)

En la lista de audiencias, busque la audiencia que creó en el ejercicio anterior `--aepUserLdap-- - Interest in Galaxy S24` y selecciónela. Haga clic en **Next**.

![RTCDP](./images/s3a.png)

Entonces verá esto... Si lo desea, puede editar la programación y el nombre de archivo haciendo clic en el icono **lápiz**. Haga clic en **Next**.

![RTCDP](./images/s3bb.png)

Ahora puede seleccionar atributos de perfil para la exportación a AWS S3. Haga clic en **Agregar nuevo campo** y asegúrese de que el campo `--aepTenantId--.identification.core.ecid` se agrega y marca como **Clave de deduplicación**.

De forma opcional, puede añadir tantos otros atributos de perfil como sea necesario.

Una vez que haya agregado todos los campos, haga clic en **Siguiente**.

![RTCDP](./images/s3c.png)

Revise la configuración. Haga clic en **Finalizar** para finalizar la configuración.

![RTCDP](./images/s3g.png)

A continuación, volverá a la pantalla Activación de destino y verá cómo se agrega la audiencia a este destino.

Si desea agregar más exportaciones de audiencia, puede hacer clic en **Activar audiencias** para reiniciar el proceso y agregar más audiencias.

![RTCDP](./images/s3j.png)

## Pasos siguientes

Ir a [2.3.5 Realizar acción: enviar la audiencia a Adobe Target](./ex5.md){target="_blank"}

Volver a [CDP en tiempo real: cree una audiencia y tome medidas](./real-time-cdp-build-a-segment-take-action.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
