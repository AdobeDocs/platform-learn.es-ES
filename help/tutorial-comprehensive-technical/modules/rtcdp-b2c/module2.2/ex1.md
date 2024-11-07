---
title: 'Servicios inteligentes: preparación de datos de inteligencia artificial aplicada al cliente (ingesta)'
description: 'AI del cliente: preparación de datos (ingesta)'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---

# 2.2.1 AI del cliente: preparación de datos (ingesta)

Para que los servicios inteligentes descubran datos de sus eventos de marketing, los datos deben enriquecerse semánticamente y mantenerse en una estructura estándar. Los servicios inteligentes aprovechan los esquemas XDM (Experience Data Model) de Adobe para conseguirlo.
En concreto, todos los conjuntos de datos que se utilizan en Intelligent Services deben cumplir con el esquema XDM **Evento de experiencia del consumidor**.

## 2.2.1.1 Crear esquema

En este ejercicio, creará un esquema que contiene el mixin **Evento de experiencia del consumidor**, que requiere el servicio inteligente **inteligencia artificial aplicada al cliente**.

Inicie sesión en Adobe Experience Platform desde esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](../../datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--module10sandbox--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](../../datacollection/module1.2/images/sb1.png)

En el menú de la izquierda, haz clic en **Esquemas** y ve a **Examinar**. Haga clic en **Crear esquema**.

![Crear nuevo esquema](./images/create-schema-button.png)

En la ventana emergente, seleccione **XDM ExperienceEvent**.

![Crear nuevo esquema](./images/xdmee.png)

Entonces verá esto...

![Crear nuevo esquema](./images/xdmee1.png)

Busque y seleccione los **mixins** siguientes para agregarlos a este esquema:

- Evento de experiencia del consumidor

  ![Nuevo esquema CEE](./images/cee.png)

- Detalles del ID del usuario final

  ![Nuevo esquema CEE](./images/identitymap.png)

Haga clic en **Agregar grupos de campos**.

![Clave de identidad definida](./images/addmixin.png)

Entonces verá esto... Seleccione el mixin **Detalles del identificador de usuario final**.

![Crear nuevo esquema](./images/eui1.png)

Vaya al campo **endUserIDs._experience.email.id**.

![Crear nuevo esquema](./images/eui2.png)

En el menú derecho del campo **endUserIDs._experience.email.id**, desplácese hacia abajo y marque la casilla de verificación de **Identidad**, marque la casilla de verificación de **Identidad principal** y seleccione el **Área de nombres de identidad** de **Correo electrónico**.

![Crear nuevo esquema](./images/eui3.png)

Vaya al campo **endUserIDs._experience.mcid.id**. Marque la casilla de verificación de **Identidad** y seleccione el **área de nombres de identidad** de **ECID**. Haga clic en **Aplicar**.

![Crear nuevo esquema](./images/eui4.png)

Asigne un nombre al esquema ahora.

Como nombre para nuestro esquema, utilizará esto:

- `--aepUserLdap-- - Demo System - Customer Experience Event`

Por ejemplo, para ldap **vangeluw**, este debe ser el nombre del esquema:

- **vangeluw - Sistema de demostración - Evento de experiencia del cliente**

Eso debería darte algo como esto. Haga clic en el botón **+ Agregar** para agregar nuevos **mixins**.

![Crear nuevo esquema](./images/xdmee2.png)

Seleccione el nombre del esquema. Ahora debería habilitar su esquema para **Perfil**, haciendo clic en la opción **Perfil**.

![Crear nuevo esquema](./images/xdmee3.png)

Entonces verá esto... Haga clic en **Habilitar**.

![Crear nuevo esquema](./images/xdmee4.png)

Ahora debería tener esto. Haga clic en **Guardar** para guardar el esquema.

![Crear nuevo esquema](./images/xdmee5.png)

## 2.2.1.2 Crear conjunto de datos

En el menú de la izquierda, haga clic en **Conjuntos de datos** y vaya a **Examinar**. Haga clic en **Crear conjunto de datos**.

![Conjunto de datos](./images/createds.png)

Haga clic en **Crear conjunto de datos a partir del esquema**.

![Conjunto de datos](./images/createdatasetfromschema.png)

En la siguiente pantalla, seleccione el conjunto de datos que creó en el ejercicio anterior, que se llama **[!UICONTROL ldap - Sistema de demostración - Evento de experiencia del cliente]**. Haga clic en **Next**.

![Conjunto de datos](./images/createds1.png)

Como nombre para su conjunto de datos, utilice `--aepUserLdap-- - Demo System - Customer Experience Event Dataset`. Haga clic en **Finalizar**.

![Conjunto de datos](./images/createds2.png)

Se ha creado el conjunto de datos. Habilite la opción **Perfil**.

![Conjunto de datos](./images/createds3.png)

Haga clic en **Habilitar**.

![Conjunto de datos](./images/createds4.png)

Ahora debería tener esto:

![Conjunto de datos](./images/createds5.png)

Ya está listo para empezar a ingerir datos de evento de experiencias del consumidor y empezar a utilizar el servicio de inteligencia artificial aplicada al cliente.

## 2.2.1.3 Descargar datos de prueba de Experience Event

Una vez configurados el **esquema** y el **conjunto de datos**, ya puede ingerir datos de evento de experiencia. Dado que la inteligencia artificial aplicada al cliente requiere datos en **2 trimestres al menos**, necesitará ingerir datos preparados de forma externa.

Los datos preparados para los eventos de experiencia deben cumplir con los requisitos y el esquema del mixin [Consumer Experience Event XDM Mixin](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md).

Descargue el archivo que contiene datos de ejemplo de esta ubicación: [https://dashboard.adobedemo.com/data](https://dashboard.adobedemo.com/data). Haga clic en el botón **Descargar**.

![Conjunto de datos](./images/dsn1.png)

Alternativamente, si no puede acceder al vínculo anterior, también puede descargar el archivo desde esta ubicación: [https://aepmodule10.s3-us-west-2.amazonaws.com/retail-v1-dec2020-xl.json.zip](https://aepmodule10.s3-us-west-2.amazonaws.com/retail-v1-dec2020-xl.json.zip).

Ahora ha descargado un archivo denominado **retail-v1-dec2020-xl.json.zip**. Coloque el archivo en el escritorio del equipo y descomprímalo, tras lo cual verá un archivo llamado **retail-v1.json**. Necesitará este archivo en el siguiente ejercicio.

![Conjunto de datos](./images/ingest.png)

## 2.2.1.4 Ingesta de datos de prueba de Evento de experiencia

En Adobe Experience Platform, vaya a **Conjuntos de datos** y abra su conjunto de datos, que se llama **[!UICONTROL ldap - Sistema de demostración - Conjunto de datos de evento de experiencia del cliente]**.

![Conjunto de datos](./images/ingest1.png)

En su conjunto de datos, haga clic en **Elegir archivos** para agregar datos.

![Conjunto de datos](./images/ingest2.png)

En la ventana emergente, selecciona el archivo **retail-v1.json** y haz clic en **Abrir**.

![Conjunto de datos](./images/ingest3.png)

Verá los datos que se están importando y se creará un nuevo lote con el estado **Cargando**. No se aleje de esta página hasta que se haya cargado el archivo.

![Conjunto de datos](./images/ingest4.png)

Una vez que se haya cargado el archivo, verá que el estado del lote cambia de **Cargando** a **Procesando**.

![Conjunto de datos](./images/ingest5.png)

La ingesta y el procesamiento de los datos pueden tardar entre 10 y 20 minutos.

Una vez que la ingesta de datos se realice correctamente, el estado del lote cambiará a **Correcto**.

![Conjunto de datos](./images/ingest7.png)

![Conjunto de datos](./images/ingest8.png)

Siguiente paso: [2.2.2 inteligencia artificial aplicada al cliente - Crear una nueva instancia (configurar)](./ex2.md)

[Volver al módulo 2.2](./intelligent-services.md)

[Volver a todos los módulos](./../../../overview.md)
