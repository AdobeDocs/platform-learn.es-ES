---
title: Foundation - Ingesta de datos - Ingesta de datos desde fuentes sin conexión
description: Foundation - Ingesta de datos - Ingesta de datos desde fuentes sin conexión
kt: 5342
doc-type: tutorial
exl-id: a4909a47-0652-453b-ae65-ba4c261f087c
source-git-commit: ef26abbeb0c1076adbada57f0f18f11c7634d022
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 5%

---

# 1.2.4 Ingesta de datos desde fuentes sin conexión

En este ejercicio, el objetivo es incorporar datos externos como datos CRM en Platform.

## Objetivos de aprendizaje

- Obtenga información sobre cómo generar datos de prueba
- Obtenga información sobre cómo introducir CSV
- Aprenda a utilizar la IU web para la ingesta de datos a través de flujos de trabajo
- Comprender las funciones de control de datos de Experience Platform

## Recursos

- Macaco: [https://www.mockaroo.com/](https://www.mockaroo.com/)
- Adobe Experience Platform: [https://experience.adobe.com/platform/](https://experience.adobe.com/platform/)

## Tareas

- Cree un archivo CSV con datos de demostración. Introduzca el archivo CSV en Adobe Experience Platform utilizando los flujos de trabajo disponibles.
- Comprensión de las opciones de gobernanza de datos en Adobe Experience Platform

## Crear un conjunto de datos de CRM mediante una herramienta de generador de datos

Para este ejercicio, necesita 1000 líneas de muestra de datos CRM.

Abra la plantilla Mockaroo en [https://www.mockaroo.com/12674210](https://www.mockaroo.com/12674210).

![Ingesta de datos](./images/mockaroo.png)

En la plantilla, verá los siguientes campos:

- Identificación
- first_name
- last_name
- email
- género
- birthDate
- home_latitude
- home_longitude
- country_code
- ciudad
- país
- crmId
- consent.email
- consent.commercialEmail
- consent.any

Todos estos campos se han definido para producir datos compatibles con Platform.

Para generar el archivo CSV, haga clic en el botón **[!UICONTROL Generar datos]** que creará y descargará un archivo CSV con 1000 líneas de datos de demostración.

![Ingesta de datos](./images/dd.png)

Abra el archivo CSV para visualizar su contenido.

![Ingesta de datos](./images/excel.png)

Con el archivo CSV listo, puede continuar con la ingesta en AEP.

### Verificar el conjunto de datos

Vaya a [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar una **[!UICONTROL zona protegida]**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``.

![Ingesta de datos](./images/sb1.png)

En Adobe Experience Platform, haga clic en **[!UICONTROL Conjuntos de datos]** en el menú de la izquierda de la pantalla.

![Ingesta de datos](./images/menudatasetssb.png)

Utilizará un conjunto de datos compartido. El conjunto de datos compartido ya se ha creado y se llama **[!UICONTROL Sistema de demostración - Conjunto de datos de perfil para CRM (Global v1.1)]**. Haga clic en él para abrirlo.

![Ingesta de datos](./images/emeacrmoverview.png)

En la pantalla de información general, puede ver 3 partes principales de información.

>[!NOTE]
>
>Es posible que la vista del conjunto de datos esté vacía si no se ha producido ninguna actividad en los últimos 7 días.

![Ingesta de datos](./images/dashboard.png)

En primer lugar, el panel [!UICONTROL Actividad del conjunto de datos] muestra el número total de registros CRM en el conjunto de datos y los lotes ingeridos y su estado

![Ingesta de datos](./images/batchids.png)

En segundo lugar, desplazándose hacia abajo por la página puede comprobar cuándo se han introducido los lotes de datos, cuántos registros se han incorporado y también si el lote se ha incorporado correctamente. El **[!UICONTROL ID de lote]** es el identificador de un trabajo por lotes específico, y el **[!UICONTROL ID de lote]** es importante ya que se puede usar para solucionar problemas de por qué un lote específico no se incorporó correctamente.

Por último, la ficha de información [!UICONTROL Conjunto de datos] muestra información importante como el [!UICONTROL ID del conjunto de datos] (de nuevo, importante desde el punto de vista de la solución de problemas), el nombre del conjunto de datos y si este se habilitó para el perfil.

![Ingesta de datos](./images/datasetsettings.png)

La configuración más importante aquí es el vínculo entre el conjunto de datos y el esquema. El esquema define qué datos se pueden introducir y el aspecto que deben tener.

En este caso, estamos usando el **[!UICONTROL Sistema de demostración - Esquema de perfil para CRM (Global v1.1)]**, que está asignado a la clase de **[!UICONTROL Perfil]** y tiene extensiones implementadas, también llamadas grupos de campos.

![Ingesta de datos](./images/ds_schemalink.png)

Al hacer clic en el nombre del esquema, se le redirige a la descripción general de [!UICONTROL Schema], donde puede ver todos los campos que se han activado para este esquema.

![Ingesta de datos](./images/schemads.png)

Cada esquema debe tener definido un descriptor principal personalizado. En el caso de nuestro conjunto de datos de CRM, el esquema ha definido que el campo **[!UICONTROL crmId]** debe ser el identificador principal. Si desea crear un esquema y vincularlo al [!UICONTROL Perfil del cliente en tiempo real], debe definir un [!UICONTROL grupo de campos] personalizado que haga referencia al descriptor principal.

También puede ver que su identidad principal se encuentra en `--aepTenantId--.identification.core.crmId`, vinculada al [!UICONTROL espacio de nombres] de **[!UICONTROL Demo System - CRMID]**.

![Ingesta de datos](./images/schema_descriptor.png)

Cada esquema y, como tal, cada conjunto de datos que debería usarse en [!UICONTROL Perfil del cliente en tiempo real] debería tener un [!UICONTROL identificador principal]. Este [!UICONTROL identificador principal] es el usuario identificador de la marca para un cliente en ese conjunto de datos. En el caso de un conjunto de datos de CRM, puede ser la dirección de correo electrónico o el ID de CRM; en el caso de un conjunto de datos de centro de llamadas, puede ser el número móvil de un cliente.

Se recomienda crear un esquema independiente y específico para cada conjunto de datos y establecer el descriptor de cada conjunto de datos específicamente para que coincida con el funcionamiento de las soluciones actuales utilizadas por la marca.

### Uso de un flujo de trabajo para asignar un archivo CSV a un esquema XDM

El objetivo de este ejercicio es incorporar datos CRM en AEP. Todos los datos que se incorporan en Platform deben asignarse al esquema XDM específico. Actualmente, tiene un conjunto de datos CSV con 1000 líneas en un lado y un conjunto de datos vinculado a un esquema en el otro. Para cargar ese archivo CSV en ese conjunto de datos, debe realizarse una asignación. Para facilitar este ejercicio de asignación, tenemos **[!UICONTROL Flujos de trabajo]** disponibles en Adobe Experience Platform.

Haga clic en **[!UICONTROL Asignar CSV a esquema XDM]** y, a continuación, haga clic en **[!UICONTROL Iniciar]** para iniciar el proceso.

![Ingesta de datos](./images/workflows.png)

En la siguiente pantalla, debe seleccionar un conjunto de datos para introducir el archivo en. Puede elegir entre seleccionar un conjunto de datos ya existente o crear uno nuevo. Para este ejercicio, reutilizaremos uno existente: seleccione **[!UICONTROL Sistema de demostración - Conjunto de datos de perfil para CRM (Global v1.1)]** como se indica a continuación y deje el resto de configuraciones establecidas como predeterminadas.

Haga clic en **Next**.

![Ingesta de datos](./images/datasetselection.png)

Arrastre y suelte su archivo CSV o haga clic en **[!UICONTROL Elegir archivos]** y navegue en su equipo hasta el escritorio y seleccione su archivo CSV.

![Ingesta de datos](./images/dragdrop.png)

Después de seleccionar el archivo CSV, se cargará inmediatamente y verá una previsualización del archivo en cuestión de segundos.

Haga clic en **Next**.

![Ingesta de datos](./images/previewcsv.png)

Ahora necesita asignar los encabezados de columna del archivo CSV con una propiedad XDM en su **[!UICONTROL sistema de demostración: conjunto de datos de perfil para CRM]**.

Adobe Experience Platform ya ha hecho algunas propuestas para usted al intentar vincular los [!UICONTROL Atributos de Source] con los [!UICONTROL Campos de esquema de destino].

>[!NOTE]
>
>Si ve algún error en la pantalla de asignación, no se preocupe. Después de seguir las siguientes instrucciones, se resolverán estos errores.

![Ingesta de datos](./images/mapschema.png)

Para las [!UICONTROL asignaciones de esquema], Adobe Experience Platform ya ha intentado vincular campos. Sin embargo, no todas las propuestas de mapeo son correctas. Ahora necesita actualizar los **campos de destino** uno por uno.

#### birthDate

El campo de esquema de Source **birthDate** debe estar vinculado al campo de destino **person.birthDate**.

![Ingesta de datos](./images/tfbd.png)

#### ciudad

El campo de esquema de Source **city** debe estar vinculado al campo de destino **homeAddress.city**.

![Ingesta de datos](./images/tfcity.png)

#### país

El campo de esquema de Source **country** debe estar vinculado al campo de destino **homeAddress.country**.

![Ingesta de datos](./images/tfcountry.png)

#### country_code

El campo de esquema de Source **country_code** debe estar vinculado al campo de destino **homeAddress.countryCode**.

![Ingesta de datos](./images/tfcountrycode.png)

#### email

El campo de esquema de Source **email** debe estar vinculado al campo de destino **personalEmail.address**.

![Ingesta de datos](./images/tfemail.png)

#### crmid

El campo de esquema de Source **crmid** debe estar vinculado al campo de destino **`--aepTenantId--`.identification.core.crmId**.

![Ingesta de datos](./images/tfemail1.png)

#### first_name

El campo de esquema de Source **first_name** debe estar vinculado al campo de destino **person.name.firstName**.

![Ingesta de datos](./images/tffname.png)

#### género

El campo de esquema de Source **gender** debe estar vinculado al campo de destino **person.gender**.

![Ingesta de datos](./images/tfgender.png)

#### home_latitude

El campo de esquema de Source **home_latitude** debe estar vinculado al campo de destino **homeAddress._schema.latitude**.

![Ingesta de datos](./images/tflat.png)

#### home_longitude

El campo de esquema de Source **home_longitude** debe estar vinculado al campo de destino **homeAddress._schema.longitude**.

![Ingesta de datos](./images/tflon.png)

#### Identificación

El campo de esquema de Source **id** debe estar vinculado al campo de destino **_id**.

![Ingesta de datos](./images/tfid1.png)

#### last_name

El campo de esquema de Source **last_name** debe estar vinculado al campo de destino **person.name.lastName**.

![Ingesta de datos](./images/tflname.png)

#### consents.marketing.email.val

El campo de esquema de Source **permission.email** debe estar vinculado al campo de destino **conents.marketing.email.val**.

![Ingesta de datos](./images/cons1.png)

#### consents.marketing.commercialEmail.val

El campo de esquema de Source **permission.CommercialEmail** debe estar vinculado al campo de destino **conents.marketing.CommercialEmail.val**.

![Ingesta de datos](./images/cons2.png)

#### consents.marketing.any.val

El campo de esquema de Source **permission.any** debe estar vinculado al campo de destino **conents.marketing.any.val**.

![Ingesta de datos](./images/cons3.png)

Ahora debería tener esto. Haga clic en **Finalizar**.

![Ingesta de datos](./images/overview.png)

Después de hacer clic en **[!UICONTROL Finalizar]**, verá la descripción general de **Flujo de datos** y, después de un par de minutos, podrá actualizar la pantalla para ver si el flujo de trabajo se completó correctamente. Haga clic en **nombre del conjunto de datos de destino**.

![Ingesta de datos](./images/dfsuccess.png)

Verá el conjunto de datos donde se ha procesado su ingesta y verá un [!UICONTROL ID de lote] que se ha ingerido en este momento, con 1000 registros ingeridos y un estado de **[!UICONTROL Éxito]**. Haga clic en **[!UICONTROL Previsualizar conjunto de datos]**.

![Ingesta de datos](./images/ingestdataset.png)

Ahora verá una pequeña muestra del conjunto de datos para asegurarse de que los datos cargados son correctos.

![Ingesta de datos](./images/previewdata.png)

Una vez cargados los datos, puede definir el enfoque de control de datos correcto para su conjunto de datos.

### Adición del control de datos al conjunto de datos

Ahora que los datos del cliente se han introducido, debe asegurarse de que este conjunto de datos esté correctamente controlado para el control de uso y exportación. Haga clic en la pestaña **[!UICONTROL Control de datos]** y observe que puede establecer varios tipos de restricciones: Contrato, Identidad y Sensible, Ecosistema de socio y Personalizado.

![Ingesta de datos](./images/dsgovernance.png)

Restrinjamos los datos de identidad para todo el conjunto de datos. Pase el ratón sobre el nombre del conjunto de datos y haga clic en el icono Lápiz para editar la configuración.

![Ingesta de datos](./images/pencil.png)

Vaya a **[!UICONTROL Etiquetas de identidad]** y verá que la opción **[!UICONTROL I2]** está marcada. Esto supondrá que todos los fragmentos de información de este conjunto de datos son al menos indirectamente identificables para la persona.

Haga clic en **[!UICONTROL Guardar cambios]**.

![Ingesta de datos](./images/identity.png)

En otro módulo, profundizaremos en el marco de quién de la gobernanza de datos y las etiquetas.

Con esto, ahora ha ingerido y clasificado correctamente los datos CRM en Adobe Experience Platform.

Siguiente Paso: [1.2.5 Zona De Aterrizaje De Datos](./ex5.md)

[Volver al módulo 1.2](./data-ingestion.md)

[Volver a todos los módulos](../../../overview.md)
