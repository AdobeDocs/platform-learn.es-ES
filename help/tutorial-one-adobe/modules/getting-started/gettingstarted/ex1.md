---
title: 'Introducción: Instale la extensión de Chrome para la documentación de Experience League'
description: 'Introducción: Instale la extensión de Chrome para la documentación de Experience League'
kt: 5342
doc-type: tutorial
source-git-commit: 6758301f639394f0d85b685a115461a63e5d760b
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%

---

# Instale la extensión de Chrome para la documentación de Experience League

## Acerca de la extensión Chrome

La documentación se ha convertido en genérica para que cualquier persona pueda reutilizarla fácilmente, utilizando cualquier instancia de Adobe Experience Platform.
Para poder reutilizar la documentación, se introdujeron **Variables de entorno** en la documentación, lo que significa que encontrará los siguientes **marcadores de posición** en la documentación. Cada marcador de posición es una variable específica para un entorno específico y la extensión de Chrome cambiará esa variable para que sea más fácil copiar código y texto de las páginas del tutorial y pegarlo en las distintas interfaces de usuario que utilizará como parte del tutorial.

A continuación se puede encontrar un ejemplo de estos valores. Actualmente, estos valores aún no se pueden usar, pero tan pronto como instale y active la extensión de Chrome, verá que estas variables cambian al texto normal y puede copiarlas y reutilizarlas.

| Nombre | Clave |
|:-------------:| :---------------:|
| ID de organización de AEP IMS | `--aepImsOrgId--` |
| ID de inquilino de AEP | `--aepTenantId--` |
| Nombre de zona protegida AEP | `--aepSandboxName--` |
| LDAP del perfil del alumno | `--aepUserLdap--` |

Por ejemplo, en la siguiente captura de pantalla puede ver una referencia a `aepTenantId`.

![DSN](./images/mod7before.png)

Una vez instalada la extensión, el mismo texto se cambia automáticamente para reflejar los valores específicos de la instancia.

![DSN](./images/mod7.png)

## Instalación de la extensión de Chrome

Para instalar esa extensión de Chrome, abra el explorador Chrome y vaya a: [https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi](https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi). Entonces verá esto...

Haga clic en **Agregar a Chrome**.

![DSN](./images/c2.png)

Entonces verá esto... Haga clic en **Agregar extensión**.

![DSN](./images/c3.png)

A continuación, se instala la extensión y se muestra una notificación similar.

![DSN](./images/c4.png)

En el menú de **extensiones**, haga clic en el icono de **pieza del rompecabezas** y ancle la extensión **Aprendizaje de plataforma - Configuración** al menú de extensión.

![DSN](./images/c6.png)

## Configuración de la extensión de Chrome

Vaya a [https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/overview](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/overview) y, a continuación, haga clic en el icono de la extensión para abrirla.

![DSN](./images/tuthome.png)

Entonces verá esta ventana emergente. Haga clic en el icono **+**.

![DSN](./images/c7.png)

Introduzca los valores como se indica a continuación, todos ellos relacionados con la instancia de Adobe Experience Platform.

![DSN](./images/c8.png)

Si no está seguro de qué valores introducir para estos campos, siga las instrucciones siguientes.

**Nombre de organización de IMS de AEP**

Cuando inicies sesión en tu instancia de Adobe Experience Platform en [https://platform.adobe.com/](https://platform.adobe.com/), encontrarás el nombre de tu instancia en la esquina superior derecha de la pantalla.

![DSN](./images/aepname.png)

**ID de organización de IMS de AEP**

El ID de organización de IMS es el identificador único de la instancia de Adobe Experience Cloud y se hace referencia a él en varias ubicaciones a lo largo de este tutorial.

La búsqueda del ID de organización de IMS se puede realizar de varias formas. Si no está seguro, consulte con uno de los administradores del sistema de su instancia para encontrar el ID.

Puede encontrarlo si va a [Admin Console](https://https://adminconsole.adobe.com/), donde puede encontrarlo como parte de la dirección URL.

![DSN](./images/aepid1.png)

También puede encontrarlo si visita **Administración de datos > Consultas** en su menú de AEP, donde puede encontrarlo en **Nombre de usuario**.

![DSN](./images/aepid2.png)

Asegúrese de copiar y pegar la parte **@AdobeOrg** junto con el ID.

**ID de inquilino de AEP**

El ID de inquilino es el identificador único de la instancia de AEP de su organización. Cuando inicie sesión en su instancia de Adobe Experience Platform en [https://platform.adobe.com/](https://platform.adobe.com/), encontrará el ID de inquilino en la dirección URL.

![DSN](./images/aeptenantid.png)

Cuando lo introduzca en la extensión de Chrome, debe asegurarse de que se agrega un guion bajo como prefijo, de modo que en este ejemplo **experienceplatform** se convierta en **_experienceplatform**.

**Nombre de zona protegida de AEP**

El nombre de la zona protegida es el nombre del entorno que utilizará en la instancia de AEP. Cuando inicie sesión en su instancia de Adobe Experience Platform en [https://platform.adobe.com/](https://platform.adobe.com/), encontrará el ID de inquilino en la dirección URL.

Antes de tomar el nombre de la zona protegida de la dirección URL, debe asegurarse de que está en la zona protegida que debe utilizar para este tutorial. Puede cambiar a la zona protegida derecha haciendo clic en el menú del conmutador de zona protegida en la esquina superior derecha de la pantalla.

![DSN](./images/aepsandboxsw.png)

En este ejemplo, el nombre de la zona protegida de AEP es **tech-insiders**.

![DSN](./images/aepsname.png)

**Su LDAP**

Este es el nombre de usuario que se utilizará como parte del tutorial. En este ejemplo, el LDAP se basa en la dirección de correo electrónico de este usuario. La dirección de correo electrónico es **vangeluw@adobe.com**, por lo que el LDAP se convierte en **vangeluw**.

El LDAP se utiliza para garantizar que la configuración que va a realizar esté vinculada a usted y no entre en conflicto con otros usuarios que puedan estar utilizando la misma instancia y zona protegida que está utilizando.

Sus valores deben ser similares a estos.
Finalmente, haga clic en **Crear nuevo**.

![DSN](./images/c8a.png)


En el menú de la izquierda de la extensión, ahora verá un nuevo icono con las iniciales de su entorno. Haga clic en ella. Luego verá la asignación entre las **variables de entorno** y los valores de instancia de Adobe Experience Platform específicos. Haga clic en **Activar configuración**.

![DSN](./images/c9.png)

Después de activar la configuración, verá un punto verde junto a las iniciales de su entorno. Esto significa que su entorno ya está activo.

![DSN](./images/c10.png)

## Verificar contenido del tutorial

Como prueba, ve a [esta página](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/datadistiller/module51/ex3).

Ahora debería ver que todas las **variables de entorno** han sido reemplazadas por sus valores verdaderos, según el entorno activado en la extensión de Chrome.

Ahora debería tener una vista similar a la siguiente, donde la variable de entorno `aepTenantId` se ha reemplazado por su ID de inquilino de AEP real, que en este caso es **_experienceplatform**.

![DSN](./images/mod7.png)

Paso siguiente: [Use el sistema de demostración siguiente para configurar la propiedad de cliente de recopilación de datos de Adobe Experience Platform](./ex2.md)

[Volver atrás a Introducción](./getting-started.md)

[Volver a todos los módulos](./../../../overview.md)
