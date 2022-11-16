---
title: 'Servicios inteligentes: preparación de datos de Customer AI (ingesta)'
description: 'AI del cliente: preparación de datos (ingesta)'
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 60996e70-b033-4932-b614-b37014232f6e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# 5.1 AI del cliente: preparación de datos (ingesta)

Para que los servicios inteligentes puedan descubrir perspectivas a partir de los datos de eventos de marketing, los datos deben enriquecirse semánticamente y mantenerse en una estructura estándar. Los servicios inteligentes aprovechan los esquemas del Modelo de datos de experiencia (XDM) de Adobe para conseguirlo.
Específicamente, todos los conjuntos de datos que se utilizan en los servicios inteligentes deben cumplir la función **Evento de experiencia del consumidor** esquema XDM.

## 5.1.1 Crear esquema

En este ejercicio, creará un esquema que contenga la variable **Mezcla de eventos de la experiencia del consumidor**, que requiere el **Customer AI** Servicio inteligente.

Inicie sesión en Adobe Experience Platform accediendo a esta URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](../module2/images/home.png)

Antes de continuar, debe seleccionar un **entorno limitado**. El nombre del simulador de pruebas que se va a seleccionar es ``--module10sandbox--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar el simulador para pruebas apropiado, verá el cambio de pantalla y ahora estará en su simulador para pruebas dedicado.

![Ingesta de datos](../module2/images/sb1.png)

En el menú de la izquierda, haga clic en **Esquemas** y vaya a **Examinar**. Haga clic en **Crear esquema**.

![Crear nuevo esquema](./images/create-schema-button.png)

En la ventana emergente, seleccione **XDM ExperienceEvent**.

![Crear nuevo esquema](./images/xdmee.png)

Entonces verás esto.

![Crear nuevo esquema](./images/xdmee1.png)

Busque y seleccione lo siguiente **Mezclas** para agregar a este esquema:

- Evento de experiencia del consumidor

   ![Nuevo esquema CEE](./images/cee.png)

- Detalles del ID de usuario final

   ![Nuevo esquema CEE](./images/identitymap.png)

Haga clic en **Agregar grupos de campos**.

![Definición de clave de identidad](./images/addmixin.png)

Entonces verás esto. Seleccionar la mezcla **Detalles del ID de usuario final**.

![Crear nuevo esquema](./images/eui1.png)

Navegar al campo **endUserIDs._experience.emailid.id**.

![Crear nuevo esquema](./images/eui2.png)

En el menú derecho del campo **endUserIDs._experience.emailid.id**, desplácese hacia abajo y marque la casilla de verificación **Identidad**, marque la casilla de verificación **Identidad principal** y seleccione **Área de nombres de identidad** de **Correo electrónico**.

![Crear nuevo esquema](./images/eui3.png)

Navegar al campo **endUserIDs._experience.mcid.id**. Marque la casilla de verificación para **Identidad** y seleccione **Área de nombres de identidad** de **ECID**. Haga clic en **Aplicar**.

![Crear nuevo esquema](./images/eui4.png)

Asigne un nombre al esquema ahora.

Como nombre para nuestro esquema, debe utilizar esto:

- `--demoProfileLdap-- - Demo System - Customer Experience Event`

Como ejemplo, para ldap **vangeluw**, este debe ser el nombre del esquema:

- **vangeluw - Sistema de demostración - Evento de experiencia del cliente**

Eso debería darte algo así. Haga clic en el **+ Agregar** para agregar **Mezclas**.

![Crear nuevo esquema](./images/xdmee2.png)

Seleccione el nombre del esquema. Ahora debe habilitar el esquema para **Perfil**, haciendo clic en el botón **Perfil** alternar.

![Crear nuevo esquema](./images/xdmee3.png)

Entonces verás esto. Haga clic en **Habilitar**.

![Crear nuevo esquema](./images/xdmee4.png)

Ahora deberías tener esto. Haga clic en **Guardar** para guardar el esquema.

![Crear nuevo esquema](./images/xdmee5.png)

## 5.1.2 Crear conjunto de datos

En el menú de la izquierda, haga clic en **Conjuntos de datos** y vaya a **Examinar**. Haga clic en **Crear conjunto de datos**.

![Conjunto de datos](./images/createds.png)

Haga clic en **Crear conjunto de datos a partir de esquema**.

![Conjunto de datos](./images/createdatasetfromschema.png)

En la siguiente pantalla, seleccione el conjunto de datos que creó en el ejercicio anterior, que tiene el nombre **[!UICONTROL ldap - Sistema de demostración - Evento de experiencia del cliente]**. Haga clic en **Siguiente**.

![Conjunto de datos](./images/createds1.png)

Como nombre para su conjunto de datos, utilice `--demoProfileLdap-- - Demo System - Customer Experience Event Dataset`. Haga clic en **Finalizar**.

![Conjunto de datos](./images/createds2.png)

Se ha creado el conjunto de datos. Active la variable **Perfil** alternar.

![Conjunto de datos](./images/createds3.png)

Haga clic en **Habilitar**.

![Conjunto de datos](./images/createds4.png)

Ahora debería tener esto:

![Conjunto de datos](./images/createds5.png)

Ya está listo para empezar a ingerir datos de Evento de experiencias del consumidor y empezar a utilizar el servicio de AI del cliente.

## 5.1.3 Descargar datos de prueba de Experience Event

Una vez que la variable **Esquema** y **Conjunto de datos** están configuradas, ya está listo para ingerir datos de Experience Event. Dado que Customer AI requiere datos entre **2 trimestres como mínimo**, tendrá que ingerir datos preparados externamente.

Los datos preparados para los eventos de experiencia deben cumplir los requisitos y el esquema del [Mezcla XDM de Evento de experiencia del consumidor](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md).

Descargue el archivo que contiene datos de ejemplo desde esta ubicación: [https://dashboard.adobedemo.com/data](https://dashboard.adobedemo.com/data). Haga clic en el **Descargar** botón.

![Conjunto de datos](./images/dsn1.png)

Ya ha descargado un archivo denominado **retail-v1-dec2020-xl.json.zip**. Coloque el archivo en el escritorio del equipo y descomprima el archivo, después de lo cual verá un archivo denominado **retail-v1.json**. Necesitará este archivo en el próximo ejercicio.

![Conjunto de datos](./images/ingest.png)

## 5.1.4 Datos de prueba de Evento de experiencia de ingesta

En Adobe Experience Platform, vaya a **Conjuntos de datos** y abra el conjunto de datos, que tiene su nombre **[!UICONTROL ldap - Sistema de demostración - Conjunto de datos del evento de la experiencia del cliente]**.

![Conjunto de datos](./images/ingest1.png)

En el conjunto de datos, haga clic en **Elegir archivos** para agregar datos.

![Conjunto de datos](./images/ingest2.png)

En la ventana emergente, seleccione el archivo **retail-v1.json** y haga clic en **Apertura**.

![Conjunto de datos](./images/ingest3.png)

Después verá los datos que se importan y se creará un nuevo lote en la variable **Carga** estado. No se aleje de esta página hasta que se cargue el archivo.

![Conjunto de datos](./images/ingest4.png)

Una vez cargado el archivo, verá que el estado del lote cambia de **Carga** a **Procesamiento**.

![Conjunto de datos](./images/ingest5.png)

La ingesta y el procesamiento de los datos pueden tardar entre 10 y 20 minutos.

Una vez que la ingesta de datos se haya realizado correctamente, el estado del lote cambiará a **Correcto**.

![Conjunto de datos](./images/ingest7.png)

![Conjunto de datos](./images/ingest8.png)

Paso siguiente: [5.2 Customer AI: crear una nueva instancia (configurar)](./ex2.md)

[Volver al módulo 5](./intelligent-services.md)

[Volver a todos los módulos](./../../overview.md)
