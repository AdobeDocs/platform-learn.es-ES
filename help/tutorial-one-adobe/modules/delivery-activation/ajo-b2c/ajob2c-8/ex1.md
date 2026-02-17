---
title: Configuración de la base de datos relacional
description: Configuración de la base de datos relacional
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: 4d420ad101c87b58a2bcc425cd4d8da08ad04c8e
workflow-type: tm+mt
source-wordcount: '2051'
ht-degree: 4%

---

# 3.8.1 Configuración de la base de datos relacional

Inicie sesión en Adobe Journey Optimizer en [https://experience.adobe.com](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![AJO OC](./images/aechome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`.

![AJO OC](./images/ajohome.png)

## 3.8.1.1 configuración de esquema basado en relaciones

Un esquema basado en relaciones es la definición formal del modelo de datos basado en modelos.

Especifica lo siguiente:

- El conjunto de tablas
- Las columnas de cada tabla
- Las restricciones
- Las relaciones entre tablas

La organización de esquemas o tablas en un modelo de datos basado en modelos consiste en estructurar los datos en varias tablas. Asegúrese de que cada tabla almacene un tipo de entidad/esquemas.

Al ingerir datos en para utilizarlos con Adobe Journey Optimizer Orchestrated Campaigns, están disponibles las siguientes fuentes:

- Amazon S3
- Almacenamiento en la nube de Google
- SFTP
- Snowflake
- Google BigQuery
- Zona de aterrizaje de datos
- Azure Databricks
- Carga de archivo local

El primer paso de este ejercicio es la configuración de los esquemas XDM basados en relaciones. En el menú de la izquierda, desplácese hacia abajo hasta **Administración de datos** y seleccione **Esquemas**. Haga clic en **+ Crear esquema**.

![AJO OC](./images/ajoocdata1.png)

Seleccione **Relacional**.

![AJO OC](./images/ajoocdata2.png)

Seleccione **Cargar archivo DDL** y haga clic en **Elegir archivos**.

![AJO OC](./images/ajoocdata3.png)

Descargue el archivo [citisignal_ddl_tables_only.sql](./assets/citisignal_ddl_tables_only.sql) en su escritorio.

![AJO OC](./images/ajoocdata4.png)

Seleccione el archivo **`citisignal_ddl_tables_only.sql`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdata5.png)

Entonces debería ver esto. Haga clic en **Next**.

![AJO OC](./images/ajoocdata6.png)

### Identidad

Algunos de los esquemas contienen identificadores personales y esos campos deben marcarse como **Identidad**, y debe seleccionar el **Espacio de nombres** que se aplica a ese tipo de identidad específico.

**`citisignal_accounts`**

Para este esquema, vaya al campo **account_id** y establezca el tipo de **identidad** en **Sistema de demostración - CRMID**.

![AJO OC](./images/ajoocdata7.png)

**`citisignal_recipients`**

Para este esquema, vaya al campo **account_id** y establezca el tipo de **Identidad** en **Sistema de demostración - CRMID**; luego vaya al campo **correo electrónico** y establezca el tipo de **Identidad** en **Correo electrónico**.

![AJO OC](./images/ajoocdata8.png)

### Versiones

Para realizar un seguimiento de las actualizaciones de los datos que se incorporarán en estos esquemas, se requiere establecer un campo que se utilice para realizar un seguimiento de la versión de los datos cargados. El campo que se usa para esto en todos estos esquemas es el campo **lastmodified**, que contiene una marca de tiempo de los datos cargados.

Ahora necesita marcar la casilla de verificación de **Control de versiones** para el campo **lastmodified** en cada uno de estos esquemas.

**`citisignal_products`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata9.png)

**`citisignal_product_bundles`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata10.png)

**`citisignal_product_relationships`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata11.png)

**`citisignal_accounts`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata12.png)

**`citisignal_recipients`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata13.png)

**`citisignal_mobile_subscriptions`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata14.png)

**`citisignal_internet_subscriptions`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata15.png)

**`citisignal_tv_subscriptions`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata16.png)

**`citisignal_equipment_subscriptions`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata17.png)

**`citisignal_mobile_usage_summary`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata18.png)

**`citisignal_internet_usage_summary`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata19.png)

**`citisignal_offers`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata20.png)

**`citisignal_offer_eligibility`**

Marque la casilla de verificación de **versiones** para el campo **última modificación**.

![AJO OC](./images/ajoocdata21.png)

### Nombre del esquema

Al ingerir estos esquemas con fines de habilitación en una zona protegida compartida, es necesario cambiar el nombre de cada esquema para que sea único en esa zona protegida específica. El motivo para realizar este cambio es evitar conflictos de nomenclatura de esquemas.

Para este laboratorio, debe agregar el LDAP delante de cada nombre de esquema, lo que significa que cada nombre de esquema debe tener este prefijo: `--aepUserLdap--_`

**`citisignal_products`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_products`.

![AJO OC](./images/ajoocdatan9.png)

**`citisignal_product_bundles`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_product_bundles`.

![AJO OC](./images/ajoocdatan10.png)

**`citisignal_product_relationships`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_product_relationships`.

![AJO OC](./images/ajoocdatan11.png)

**`citisignal_accounts`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_accounts`.

![AJO OC](./images/ajoocdatan12.png)

**`citisignal_recipients`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_recipients`.

![AJO OC](./images/ajoocdatan13.png)

**`citisignal_mobile_subscriptions`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_mobile_subscriptions`.

![AJO OC](./images/ajoocdatan14.png)

**`citisignal_internet_subscriptions`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_internet_subscriptions`.

![AJO OC](./images/ajoocdatan15.png)

**`citisignal_tv_subscriptions`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_internet_subscriptions`.

![AJO OC](./images/ajoocdatan16.png)

**`citisignal_equipment_subscriptions`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_equipment_subscriptions`.

![AJO OC](./images/ajoocdatan17.png)

**`citisignal_mobile_usage_summary`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_mobile_usage_summary`.

![AJO OC](./images/ajoocdatan18.png)

**`citisignal_internet_usage_summary`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_internet_usage_summary`.

![AJO OC](./images/ajoocdatan19.png)

**`citisignal_offers`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_offers`.

![AJO OC](./images/ajoocdatan20.png)

**`citisignal_offer_eligibility`**

Cambie el nombre de su esquema a `--aepUserLdap--_ citisignal_offer_eligibility`.

![AJO OC](./images/ajoocdatan21.png)

Los esquemas están listos para guardarse. Haga clic en **Finalizado**.

![AJO OC](./images/ajoocdata22.png)

Entonces debería ver esto. Haga clic en **Guardar**.

![AJO OC](./images/ajoocdata23.png)

Haga clic en **Abrir trabajos**.

![AJO OC](./images/ajoocdata24.png)

Entonces debería ver esto. Debe esperar hasta que el trabajo se complete correctamente antes de continuar con el siguiente paso.

![AJO OC](./images/ajoocdata25.png)

Una vez que el trabajo se haya completado correctamente, puede continuar con el siguiente paso. Esto puede tardar de 5 a 10 minutos.

![AJO OC](./images/ajoocdata26.png)

Ahora que los esquemas XDM relacionales están configurados y con los datos que se están ingiriendo, puede empezar a utilizar esos datos para crear la campaña orquestada en el siguiente ejercicio.

## 3.8.1.2 Ingesta de datos

Ir a **Conjuntos de datos**. A continuación, debería ver un conjunto de datos creado para cada esquema que haya creado.

![AJO OC](./images/ajoocdata27.png)

Descargue el archivo [data.zip](./assets/data.zip) en su escritorio y descomprímalo.

![AJO OC](./images/ajoocdata28.png)

Abra la carpeta **data**. Debería ver un archivo CSV para cada uno de los esquemas creados. Ahora debe cargar esos datos en cada conjunto de datos correspondiente. Para este laboratorio, lo hará cargando un archivo local en cada conjunto de datos.

![AJO OC](./images/ajoocdata29.png)

**`vangeluw_citisignal_products`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_products`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas9a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_products.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas9b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas9c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas9d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas9e.png)

**`vangeluw_citisignal_product_bundles`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_product_bundles`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas10a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_product_bundles.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas10b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas10c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas10d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas10e.png)

**`vangeluw_citisignal_product_relationships`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_product_relationships`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas11a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_product_relationships.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas11b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas11c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas11d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas11e.png)

**`vangeluw_citisignal_accounts`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_accounts`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas12a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_accounts.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas12b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas12c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas12d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas12e.png)

**`vangeluw_citisignal_recipients`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_recipients`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas13a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_recipients.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas13b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas13c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas13d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas13e.png)

**`vangeluw_citisignal_mobile_subscriptions`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_mobile_subscriptions`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas14a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_mobile_subscriptions.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas14b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas14c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas14d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas14e.png)

**`vangeluw_citisignal_internet_subscriptions`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_internet_subscriptions`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas15a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_internet_subscriptions.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas15b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas15c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas15d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas15e.png)

**`vangeluw_citisignal_tv_subscriptions`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_tv_subscriptions`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas16a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_tv_subscriptions.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas16b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas16c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas16d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas16e.png)

**`vangeluw_citisignal_equipment_subscriptions`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_equipment_subscriptions`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas17a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_equipment_subscriptions.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas17b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas17c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas17d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas17e.png)

**`vangeluw_citisignal_mobile_usage_summary`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_mobile_usage_summary`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas18a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_mobile_usage_summary.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas18b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas18c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas18d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas18e.png)

**`vangeluw_citisignal_internet_usage_summary`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_internet_usage_summary`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas19a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_internet_usage_summary.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas19b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas19c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas19d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas19e.png)

**`vangeluw_citisignal_offers`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_offers`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas20a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_offers.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas20b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas20c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas20d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas20e.png)

**`vangeluw_citisignal_offer_eligibility`**

Vaya a **Orígenes**, busque `local` y haga clic en **Agregar datos** en **Carga de archivos locales**.

![AJO OC](./images/ajoocdatas10.png)

Habilite la opción para **Habilitar la captura de datos modificados**.

Seleccione el conjunto de datos `vangeluw_citisignal_offer_eligibility`.

Haga clic en **Next**.

![AJO OC](./images/ajoocdatas21a.png)

Haga clic en **Elegir archivos**. Seleccione el archivo **`citisignal_offer_eligibility.csv`** y haga clic en **abrir**.

![AJO OC](./images/ajoocdatas21b.png)

Haga clic en **Siguiente**

![AJO OC](./images/ajoocdatas21c.png)

Haga clic en **Finalizar**.

![AJO OC](./images/ajoocdatas21d.png)

Después de un par de minutos, puede ver los datos que se están ingiriendo en el conjunto de datos.

![AJO OC](./images/ajoocdatas21e.png)

Ahora se han introducido todos los datos.

## Dimension de destino de perfil 3.8.1.3

Con las campañas orquestadas, puede diseñar y entregar comunicaciones dirigidas en el nivel de entidad, aprovechando las capacidades de esquema relacional de Adobe Experience Platform. Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Cuando se incorporan datos en Experience Platform, se estructuran según un esquema XDM.

Aunque la segmentación para Campañas orquestadas funciona principalmente en esquemas relacionales, la entrega de mensajes real siempre se produce en el nivel de Perfil.

Al configurar el direccionamiento, se definen dos aspectos clave:

- Esquemas objetivo: Especifique qué esquemas relacionales son aptos para la segmentación. De forma predeterminada, se utiliza el esquema denominado Recipient, pero puede configurar alternativas como Visitors, Customers, etc.

- Vinculación de perfil: el sistema debe comprender cómo se asigna el esquema de destino al esquema de perfil. Esto se logra a través de un campo de identidad compartido, que existe tanto en el esquema de destinatario como en el esquema de perfil y se configura como un área de nombres de identidad.

Ahora debe configurar las dimensiones de destino del perfil. Vaya a **Administración** > **Configuración** y haga clic en **Administrar** en **Dimension de destino de perfil**.

![AJO OC](./images/ajoocptd1.png)

Entonces debería ver esto. Haga clic en **Crear**.

![AJO OC](./images/ajoocptd2.png)

Para el **esquema**, seleccione `--aepUserLdap--_citisignal_accounts`. Para el **valor de identidad**, seleccione **account_id**.

Haga clic en **Guardar**.

![AJO OC](./images/ajoocptd3.png)

Vuelva a hacer clic en **Crear**.

![AJO OC](./images/ajoocptd4.png)

Para el **esquema**, seleccione `--aepUserLdap--_citisignal_recipients`. Para el **valor de identidad**, seleccione **account_id**.

Haga clic en **Guardar**.

![AJO OC](./images/ajoocptd5.png)

Vuelva a hacer clic en **Crear**.

![AJO OC](./images/ajoocptd6.png)

Para el **esquema**, seleccione `--aepUserLdap--_citisignal_recipients`. Para el **valor de identidad**, seleccione **correo electrónico**.

Haga clic en **Guardar**.

![AJO OC](./images/ajoocptd7.png)

Entonces deberías tener esto.

![AJO OC](./images/ajoocptd8.png)

En el siguiente ejercicio, empezará a utilizar esos datos como parte de una campaña orquestada.

## Pasos siguientes

Vaya a [Crear su campaña orquestada](./ex2.md){target="_blank"}

Volver a [Adobe Journey Optimizer: campañas orquestadas](./ajocampaigns.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
