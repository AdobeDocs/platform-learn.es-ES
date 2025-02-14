---
title: Foundation - Ingesta de datos - Configuración de esquemas y conjuntos de identificadores
description: Foundation - Ingesta de datos - Configuración de esquemas y conjuntos de identificadores
kt: 5342
doc-type: tutorial
exl-id: 3cc1fbe3-1f40-45a3-a123-ee6f1463e7b5
source-git-commit: b78460ab562c2b435988942b219787ed07af24d4
workflow-type: tm+mt
source-wordcount: '3102'
ht-degree: 4%

---

# 1.2.2 Configuración de esquemas y definición de identificadores

En este ejercicio, se revisará la configuración de los esquemas XDM necesarios para clasificar la información de perfil y el comportamiento del cliente. En cada esquema XDM, también verá que se define un identificador principal para vincular toda la información relacionada con el cliente a.

## Historia

Antes de empezar a configurar los identificadores y los esquemas XDM, debe pensar en el contexto empresarial de lo que estamos intentando hacer:

- Desea datos
- Desea vincular datos a un cliente
- Desea crear un perfil de cliente progresivo en tiempo real

Existen dos tipos de datos que queremos capturar:

- ¿Quién es este cliente?
- ¿Qué hace este cliente?

Sin embargo, la pregunta **¿Quién es este cliente?** es una pregunta muy abierta que tiene muchas respuestas. Cuando su organización desea ver respondida esta pregunta, está buscando información demográfica como Nombre, Apellidos y Dirección. Pero también para información de contacto, como una dirección de correo electrónico o un número de teléfono móvil. Y también para información relacionada con el idioma, OptIn/OptOut y tal vez incluso imágenes de perfil. Y, por último, lo que realmente necesita saber es cómo identificaremos a este cliente en los distintos sistemas que utiliza su organización.

Lo mismo ocurre con la pregunta **¿Qué hace este cliente?**. Es una pregunta muy abierta con muchas respuestas. Cuando su organización desea ver respondida esta pregunta, está buscando cualquier interacción que un cliente haya tenido con cualquiera de sus propiedades en línea y sin conexión. ¿Qué páginas o productos se han visitado? ¿Este cliente ha añadido un producto a su carro de compras o incluso ha comprado un artículo? ¿Qué dispositivo y navegador se ha utilizado para navegar por el sitio web? ¿Qué tipo de información busca este cliente y cómo podemos utilizarla para configurar y ofrecer una experiencia agradable a este cliente? Y, por último, lo que realmente necesitamos saber es cómo identificaremos a este cliente en los distintos sistemas que utilizará su organización.

## Quién es este cliente

Capturando la respuesta a **¿Quién es este cliente?** para su organización se completó a través de la página de inicio de sesión/registro.

![Ingesta de datos](./images/pv10.png)

Desde la perspectiva de esquema, vemos esto como una **Clase**. La pregunta: **¿Quién es este cliente?** es algo que definimos en la clase **[!UICONTROL XDM Individual Profile]**.

Por lo tanto, cuando crea un esquema XDM para capturar la respuesta a **, ¿quién es este cliente?**, en primer lugar, tendrá que crear y definir 1 esquema que haga referencia a la clase **[!UICONTROL XDM Individual Profile]**.

Para especificar qué tipo de respuestas se pueden dar a esa pregunta, necesitará definir [!UICONTROL Grupos de campos]. [!UICONTROL Los grupos de campos] son extensiones de la clase Profile y tienen configuraciones muy específicas. Por ejemplo, la información demográfica como Nombre, Apellido, Sexo y Cumpleaños forma parte del [!UICONTROL Grupo de campos]: **[!UICONTROL Detalles demográficos]**.

En segundo lugar, su organización debe decidir cómo identificar a este cliente. En el caso de su organización, el identificador principal de un cliente conocido puede ser un ID de cliente específico, como una dirección de correo electrónico, por ejemplo. Pero técnicamente, hay otras formas de identificar a un cliente en su organización, como utilizar un número de teléfono móvil.
En este laboratorio, definiremos la dirección de correo electrónico como identificador principal y el número de teléfono como identificador secundario.

Por último, es importante distinguir el canal en el que se capturaron los datos. En este caso, hablaremos de los registros de sitios web y el esquema que se debe definir debe reflejar **dónde** se capturaron los datos de registro. El canal también tendrá un papel importante a la hora de influir en los datos que se capturan. Por lo tanto, es una práctica recomendada definir esquemas para cada combinación de canal, identificador principal y tipo de datos recopilados.

En función de lo anterior, los esquemas se crearon en Adobe Experience Platform.

Inicie sesión en Adobe Experience Platform desde esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./images/sb1.png)

En Adobe Experience Platform, haga clic en **[!UICONTROL Esquemas]** en el menú de la izquierda de la pantalla. Verá la lista de [!UICONTROL esquemas] disponibles. Debe crear un nuevo esquema. Para crear un nuevo esquema, haga clic en **[!UICONTROL + Crear esquema]**.

![Ingesta de datos](./images/menuschemas.png)

Seleccione **Manual** y haga clic en **Seleccionar**.

![Ingesta de datos](./images/createschemaa.png)

A continuación, seleccione **Perfil individual** y haga clic en **Siguiente**.

![Ingesta de datos](./images/createschemab.png)

Escriba el nombre de su esquema de la siguiente manera: `--aepUserLdap-- - Demo System - Profile Schema for Website`. Haga clic en **Finalizar**.

![Ingesta de datos](./images/createschemac.png)

Se crea un nuevo esquema.

![Ingesta de datos](./images/emptyschema.png)

Ahora necesita definir la respuesta a la pregunta **: ¿Quién es este cliente?** debería tener el aspecto siguiente.
En la introducción de este laboratorio, observamos la necesidad de los siguientes atributos para definir un cliente:

- Información demográfica como nombre, apellido y dirección
- Información de contacto, como dirección postal, dirección de correo electrónico o número de teléfono móvil
- Otra información vinculada a Idioma, OptIn/OptOut y tal vez incluso imágenes de perfil.
- Identificador principal de un cliente

Para que esa información forme parte del esquema, debe agregar los siguientes [!UICONTROL grupos de campos] al esquema:

- Datos demográficos (información demográfica)
- Datos personales de contacto (información de contacto)
- Detalles de consentimiento y preferencia (otra información)
- Grupo de campos de identificación de perfil personalizado de su organización (identificadores principal y secundario)

Haga clic en el botón **+Agregar** en **Grupos de campos**.

![Ingesta de datos](./images/createschemad.png)

En la pantalla **[!UICONTROL Agregar grupo de campos]**, seleccione [!UICONTROL Grupo de campos] **[!UICONTROL Detalles demográficos]**, **[!UICONTROL Detalles de contacto personal]** y **[!UICONTROL Detalles de consentimiento y preferencia]**.

Haga clic en el botón **[!UICONTROL Agregar grupos de campos]** para agregar el [!UICONTROL grupo de campos] al esquema.

![Ingesta de datos](./images/ppfd.png)

Ahora tendrá esto:

![Ingesta de datos](./images/schemathis.png)

A continuación, necesita un nuevo [!UICONTROL grupo de campos] para capturar el **[!UICONTROL identificador]** que se usa para la recopilación de datos. Como ha visto en el ejercicio anterior, existe un concepto de identificadores. El identificador principal es el más importante, ya que todos los datos recopilados se vinculan a este identificador.

Ahora creará su propio [!UICONTROL grupo de campos] personalizado y, como tal, ampliará el [!UICONTROL esquema XDM] para satisfacer los requisitos de su propia organización.

Haga clic en **[!UICONTROL + Agregar]** en **Grupos de campos** para empezar a agregar [!UICONTROL Grupo de campos].

![Ingesta de datos](./images/addmixin2.png)

En lugar de reutilizar un [!UICONTROL grupo de campos] existente, ahora creará su propio [!UICONTROL grupo de campos]. Puede hacerlo seleccionando **[!UICONTROL Crear nuevo grupo de campos]**.

![Ingesta de datos](./images/createmixin.png)

Ahora necesita proporcionar un **[!UICONTROL Nombre para mostrar]** y **[!UICONTROL Descripción]** para su nuevo [!UICONTROL grupo de campos].

Como nombre del esquema, se utiliza lo siguiente:
`--aepUserLdap-- - Profile Identification Field Group`

Haga clic en el botón **[!UICONTROL Agregar grupos de campos]** para agregar el [!UICONTROL grupo de campos] recién creado a su esquema.

![Ingesta de datos](./images/mixinname.png)

Ahora tiene esta estructura de esquema configurada.

![Ingesta de datos](./images/schemastructurem.png)

El nuevo [!UICONTROL grupo de campos] sigue vacío, así que tendrá que agregar campos a ese [!UICONTROL grupo de campos].
En la lista [!UICONTROL Grupo de campos], haga clic en su [!UICONTROL grupo de campos] personalizado.

![Ingesta de datos](./images/schemastructurem.png)

Ahora verá aparecer una serie de botones nuevos.

En el nivel superior del esquema, haga clic en el botón **[!UICONTROL + Agregar campo]**.

![Ingesta de datos](./images/clickaddfield.png)

Después de hacer clic en el botón **[!UICONTROL + Agregar campo]**, ahora verá un nuevo campo sin título en el esquema.

![Ingesta de datos](./images/tenantschema1.png)

Ahora debe introducir la información de este nuevo campo, utilizando estas definiciones de objeto:

- Nombre del campo: **`--aepUserLdap--_identification`**
- Nombre para mostrar: **`--aepUserLdap--_identification`**
- Tipo: **[!UICONTROL objeto]**
- Grupo de campos: **`--aepUserLdap-- - Profile Identification Field Group`**

Haga clic en **Aplicar**.

![Ingesta de datos](./images/tenantfielddef.png)

Ahora verá un nuevo objeto en su esquema, que representa un **[!UICONTROL objeto]** personalizado en el esquema y que recibe el nombre de su ID de inquilino de Adobe Experience Platform. Su ID de inquilino de Adobe Experience Platform es `--aepTenantId--` y es único para cada instancia de AEP.

![Ingesta de datos](./images/tenant.png)

Ahora agregará un nuevo objeto de campos 3 debajo de ese inquilino, en el objeto **identification** que acaba de crear. Para empezar a agregar cada uno de estos 3 campos, haga clic en el **+-icon** bajo **identificación** para cada campo.

![Ingesta de datos](./images/tenantfield.png)

Utilice la siguiente información para crear los 3 campos nuevos bajo el objeto **[!UICONTROL identification]**:

- ecid:
   - Nombre del campo: **`--aepUserLdap--_ecid`**
   - Nombre para mostrar: **`--aepUserLdap--ecid`**
   - Tipo: **[!UICONTROL Cadena]**
   - Grupo de campos: **`--aepUserLdap-- - Profile Identification Field Group`**

- emailId
   - Nombre del campo: **`--aepUserLdap--_emailId`**
   - Nombre para mostrar: **`--aepUserLdap--_emailId`**
   - Tipo: **[!UICONTROL Cadena]**
   - Grupo de campos: **`--aepUserLdap-- - Profile Identification Field Group`**

- mobilenr
   - Nombre del campo: **`--aepUserLdap--_mobilenr`**
   - Nombre para mostrar: **`--aepUserLdap--_mobilenr`**
   - Tipo: **[!UICONTROL Cadena]**
   - Grupo de campos: **`--aepUserLdap-- - Profile Identification Field Group`**

Así es como debe verse cada campo después de su configuración inicial de campo.

- `--aepUserLdap--_mobilenr`

![Ingesta de datos](./images/mobilenrfield.png)

Para guardar el campo, desplácese hacia abajo en **[!UICONTROL Propiedades del campo]** hasta que vea el botón **[!UICONTROL Aplicar]**. Haga clic en el botón **[!UICONTROL Aplicar]**.

![Ingesta de datos](./images/apply.png)

- `--aepUserLdap--_ecid`

![Ingesta de datos](./images/ecidfield.png)

No olvides desplazarte hacia abajo y hacer clic en **Aplicar**.

- `--aepUserLdap--_emailId`

![Ingesta de datos](./images/emailidfield.png)

No olvides desplazarte hacia abajo y hacer clic en **Aplicar**.

Cada campo está definido como tipo **[!UICONTROL Cadena]** y ahora configurará estos campos como **[!UICONTROL Identidades]**. Para este esquema, suponemos que un cliente siempre se identificará por su dirección de correo electrónico, lo que significa que debe configurar el campo **[!UICONTROL emailId]** como identificador **[!UICONTROL principal]**, y los demás campos como identificadores normales.

Sus 3 campos ahora deben definirse como **[!UICONTROL Identity]**-fields.

![Ingesta de datos](./images/3fields.png)

Para empezar a definir estos campos como **[!UICONTROL campos de identidad]**, siga estos pasos:

- Seleccione el campo **`--aepUserLdap--_emailId`**.
- En el lado derecho, en las propiedades del campo, desplácese hacia abajo hasta que vea **[!UICONTROL Identidad]**. Marque la casilla de verificación de **[!UICONTROL Identidad]**.

![Ingesta de datos](./images/emailidid.png)

- Ahora marque la casilla de verificación de **[!UICONTROL Identidad principal]**.

![Ingesta de datos](./images/emailidprimid.png)

- Por último, seleccione el área de nombres **[!UICONTROL Email]** de la lista de **[!UICONTROL Áreas de nombres]**. Identity Graph utiliza un área de nombres en Adobe Experience Platform para clasificar identificadores en áreas de nombres y definir la relación entre esas áreas de nombres. Haga clic en **[!UICONTROL Aplicar]** para guardar los cambios.

![Ingesta de datos](./images/emailidprimidns.png)

A continuación, debe definir los demás campos de **`--aepUserLdap--_ecid`** y **`--aepUserLdap--_mobilenr`** como identificadores estándar.

Seleccione el campo **`--aepUserLdap--_ecid`**. En el lado derecho, en las propiedades del campo, desplácese hacia abajo hasta que vea **[!UICONTROL Identidad]**. Marque la casilla de verificación de **[!UICONTROL Identidad]**.
A continuación, seleccione el área de nombres **[!UICONTROL ECID]** de la lista de **[!UICONTROL áreas de nombres]**.
Haga clic en **[!UICONTROL Aplicar]** para guardar los cambios.

![Ingesta de datos](./images/ecidid.png)

Seleccione el campo **`--aepUserLdap--_mobilenr`**. En el lado derecho, en las propiedades del campo, desplácese hacia abajo hasta que vea **[!UICONTROL Identidad]**. Marque la casilla de verificación de **[!UICONTROL Identidad]**.
Seleccione el área de nombres **[!UICONTROL Phone]** de la lista de **[!UICONTROL Namespaces]**.
Haga clic en **[!UICONTROL Aplicar]** para guardar los cambios.

![Ingesta de datos](./images/mobid.png)

El objeto **[!UICONTROL identification]** debería tener un aspecto similar a este, con los 3 campos de identificación que ahora también muestran un icono de **[!UICONTROL huella digital]** para mostrar que se han definido como identificadores.

![Ingesta de datos](./images/applyiden.png)

Haga clic en **[!UICONTROL Guardar]** para guardar los cambios.

![Ingesta de datos](./images/saveschema.png)

Lo último que hay que hacer aquí es activar el esquema que se vinculará al **[!UICONTROL perfil]**.
Al habilitar su esquema para Perfil, se asegura de que todos los datos enviados a Adobe Experience Platform con este esquema formarán parte del entorno Perfil del cliente en tiempo real, lo que garantiza que todos esos datos se puedan utilizar en tiempo real para consultas, segmentación y activación.

Para ello, seleccione el nombre del esquema.

![Ingesta de datos](./images/schemastructure.png)

En la ficha derecha del esquema, haga clic en **[!UICONTROL Alternar perfil]**, que está desactivada actualmente.

![Ingesta de datos](./images/upswitcherps.png)

Active el conmutador [!UICONTROL Perfil] - haciendo clic en él.

Haga clic en **[!UICONTROL Habilitar]** para habilitar este esquema para el perfil.

![Ingesta de datos](./images/sureps.png)

Su esquema está configurado para formar parte de [!UICONTROL Perfil del cliente en tiempo real]. Haga clic en **[!UICONTROL Guardar]** para guardar el esquema.

![Ingesta de datos](./images/sureyps.png)

## ¿Qué hace este cliente?

Registrando la respuesta a la pregunta **¿Qué hace este cliente?** para su organización se completó mediante, por ejemplo, una vista de producto en una página de producto.

![Ingesta de datos](./images/pv7.png)

Desde la perspectiva de esquema, vemos esto como una **[!UICONTROL Clase]**. La pregunta: **¿Qué hace este cliente?** es algo que definimos en la clase **[!UICONTROL ExperienceEvent]**.

Por lo tanto, cuando crea un [!UICONTROL esquema XDM] para capturar la respuesta a **¿Qué hace este cliente?**, en primer lugar, tendrá que crear y definir 1 esquema que haga referencia a la clase **[!UICONTROL ExperienceEvent]**.

Para especificar qué tipo de respuestas se pueden dar a esa pregunta, necesitará definir [!UICONTROL Grupo de campos]. [!UICONTROL Los grupos de campos] son extensiones de la clase [!UICONTROL ExperienceEvent] y tienen configuraciones muy específicas. Por ejemplo, la información sobre el tipo de productos que un cliente vio o agregó al carro de compras forma parte de [!UICONTROL Grupo de campos] **Detalles de Commerce**.

En segundo lugar, su organización debe decidir cómo identificará el comportamiento de este cliente. Dado que se trata de interacciones en un sitio web, es posible que su organización conozca al cliente, pero también es posible que un visitante anónimo desconocido esté activo en el sitio web. Así que no podemos usar un identificador como email-address. En este caso, su organización probablemente decida usar el [!UICONTROL Experience Cloud ID (ECID)] como identificador principal.

Por último, es importante distinguir el canal en el que se capturaron los datos. En este caso, se hablará de las interacciones del sitio web y el esquema que debe definirse debe reflejar **dónde** se capturaron los datos de interacción. El canal también tendrá un papel importante a la hora de influir en los datos que se capturan. Por lo tanto, es una práctica recomendada definir esquemas para cada combinación de canal, identificador principal y tipo de datos recopilados.

En función de lo anterior, debe configurar un esquema en Adobe Experience Platform.

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar una **[!UICONTROL zona protegida]**. La [!UICONTROL zona protegida] que se va a seleccionar se llama ``--aepSandboxName--``. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./images/sb1.png)

En Adobe Experience Platform, haz clic en **[!UICONTROL Esquemas]** en el menú de la izquierda de la pantalla y ve a **Examinar**. Debe crear un nuevo esquema. Para crear un nuevo esquema, haga clic en el botón **[!UICONTROL + Crear esquema]**.

![Ingesta de datos](./images/menuschemas.png)

Seleccione **Manual** y haga clic en **Seleccionar**.

![Ingesta de datos](./images/createschema1.png)

Seleccione **Evento de experiencia** y haga clic en **Siguiente**.

![Ingesta de datos](./images/createschema1a.png)

Escriba un nombre para el esquema, así: `--aepUserLdap-- - Demo System - Event Schema for Website`. Haga clic en **Finalizar**.

![Ingesta de datos](./images/schemaname1ee.png)

Se crea un nuevo esquema y puede configurar qué datos se recopilan con él.

![Ingesta de datos](./images/emptyschemaee.png)

Ahora necesita definir la respuesta a la pregunta **¿Qué hace este cliente?** debería tener el aspecto siguiente.
En la introducción de este laboratorio, observamos la necesidad de los siguientes atributos para definir lo que hace un cliente:

- ¿Qué páginas o productos se han visitado?
- ¿Este cliente ha agregado un producto al carro de compras o incluso ha comprado un artículo?
- ¿Qué dispositivo y navegador se ha utilizado para navegar por el sitio web?
- ¿Qué tipo de información busca este cliente y cómo podemos utilizarla para configurar y ofrecer una experiencia agradable a este cliente?
- Identificador principal de un cliente


Para que esa información forme parte del esquema, debe agregar el siguiente [!UICONTROL grupo de campos] al esquema:

- ExperienceEvent de SDK web de AEP
- Identificación de perfil personalizada de su organización [!UICONTROL Grupo de campos]

Haga clic en **+ Agregar** en **Grupos de campos**.

![Ingesta de datos](./images/eeedfg.png)

En la pantalla **[!UICONTROL Agregar grupo de campos]**, seleccione [!UICONTROL Grupo de campos] **[!UICONTROL AEP Web SDK ExperienceEvent]**. Haga clic en **[!UICONTROL Agregar grupos de campos]**.

![Ingesta de datos](./images/eeed.png)

A continuación, tendrá esto:

![Ingesta de datos](./images/eethis.png)

A continuación, debe crear un nuevo [!UICONTROL grupo de campos] para capturar el **[!UICONTROL identificador]** que se usa para la recopilación de datos.

Ahora creará su propio [!UICONTROL grupo de campos] personalizado y, como tal, ampliará el [!UICONTROL esquema XDM] para satisfacer los requisitos de su propia organización.

Un [!UICONTROL grupo de campos] está vinculado a una [!UICONTROL clase], lo que significa que no puede reutilizar el [!UICONTROL grupo de campos] creado anteriormente.

Haga clic en el botón **[!UICONTROL + Agregar]** para empezar a agregar un [!UICONTROL grupo de campos].

![Ingesta de datos](./images/addmixinee2.png)

En lugar de reutilizar un [!UICONTROL grupo de campos] existente, ahora creará su propio [!UICONTROL grupo de campos]. Seleccione **[!UICONTROL Crear nuevo grupo de campos]** e introduzca el nombre para su grupo de campos de la siguiente manera: `--aepUserLdap-- - ExperienceEvent Identification Field Group`.
Haga clic en **Agregar grupos de campos**

![Ingesta de datos](./images/createmixineew.png)

Ahora debería tener esta estructura de [!UICONTROL Esquema].

![Ingesta de datos](./images/schemastructuremee.png)

El nuevo [!UICONTROL grupo de campos] sigue vacío, así que tendrá que agregar campos a ese grupo de campos.
En la lista [!UICONTROL Grupo de campos], haga clic en su [!UICONTROL grupo de campos] personalizado.

![Ingesta de datos](./images/schemastructuremee1.png)

Ahora verá aparecer una serie de botones nuevos.

En el nivel superior del esquema, junto al nombre del esquema, haga clic en el botón **[!UICONTROL +]**.

![Ingesta de datos](./images/clickaddfieldee.png)

Después de hacer clic en el botón **+**, ahora verá un nuevo campo sin título en el esquema.

Utilice esto para definir el nuevo campo:

- Nombre del campo: **`--aepUserLdap--_identification`**
- Nombre para mostrar: **`--aepUserLdap--_identification`**
- Tipo: **[!UICONTROL objeto]**
- Grupo de campos: `--aepUserLdap-- - ExperienceEvent Identification Field Group`

Haga clic en **Aplicar**.

![Ingesta de datos](./images/tenantfielddefee.png)

El nuevo campo se creará en su ID de inquilino de Adobe Experience Platform. Su id. de inquilino de Adobe Experience Platform es `--aepTenantId--`.

![Ingesta de datos](./images/tenantee.png)

Ahora agregará 1 nuevo campo bajo el objeto **[!UICONTROL identification]**.

Haga clic en el botón **[!UICONTROL +]** junto al objeto **[!UICONTROL identification]** para crear un nuevo campo.

![Ingesta de datos](./images/tenantfieldeewv.png)

El campo ECID se definirá como tipo **[!UICONTROL Cadena]** y configurará este campo como **[!UICONTROL Identidad]**. Para el esquema **[!UICONTROL Sistema de demostración - Esquema de evento para el sitio web]**, suponemos que un cliente siempre se identificará por su [!UICONTROL ECID], lo que significa que debe configurar el campo **[!UICONTROL ECID]** como un identificador **principal**

Ahora tiene un campo vacío. Debe configurar el campo anterior como se indica.

- ecid:

   - Nombre del campo: **`--aepUserLdap--_ecidweb`**
   - Nombre para mostrar: **`--aepUserLdap--_ecidweb`**
   - Tipo: **[!UICONTROL Cadena]**
   - Grupo de campos: `--aepUserLdap-- - ExperienceEvent Identification Field Group`

Este es el aspecto que debería tener el campo `--aepUserLdap--_ecidweb` tras la configuración inicial del campo:

![Ingesta de datos](./images/ecidfieldee.png)

Desplácese hacia abajo y haga clic en **[!UICONTROL Aplicar]**.

![Ingesta de datos](./images/applywv.png)

Ahora tiene un nuevo campo, pero aún no se ha definido este campo como **[!UICONTROL Identity]**-field.

![Ingesta de datos](./images/3fieldsee.png)

Para empezar a definir estos campos como **[!UICONTROL campos de identidad]**, seleccione el campo **`--aepUserLdap--_ecidweb`**.
En el lado derecho, en las propiedades del campo, desplácese hacia abajo hasta que vea **[!UICONTROL Identidad]**. Marque la casilla de verificación de **[!UICONTROL identidad]** y marque la casilla de verificación de **[!UICONTROL identidad principal]**.
Seleccione el área de nombres **[!UICONTROL ECID]** de la lista de **[!UICONTROL áreas de nombres]**.

Haga clic en **[!UICONTROL Aplicar]** para guardar los cambios.

![Ingesta de datos](./images/ecididee.png)

El objeto **[!UICONTROL identification]** debería tener un aspecto similar a este, y el campo ecid ahora también muestra un icono de **huella digital** para mostrar que se han definido como identificadores.
Haga clic en **[!UICONTROL Guardar]** para guardar los cambios.

![Ingesta de datos](./images/applyidenee.png)

Es importante tener en cuenta que, cuando finalmente se incorporan datos en este esquema, algunos campos son obligatorios.
Por ejemplo, los campos **[!UICONTROL _id]** y **[!UICONTROL timestamp]** son campos obligatorios, que es un requisito impuesto por la clase ExperienceEvent.

- _id necesita contener un id único para una ingesta de datos específica
- la marca de tiempo debe ser la marca de tiempo de esta visita individual, con formato **`"YYYY-MM-DDTHH:MM:SSSZ"`**, como por ejemplo: **`"2024-11-18T07:20:000Z"`**

Ahora ha definido un esquema, ha vinculado los [!UICONTROL grupos de campos] existentes y los recientemente creados, y ha definido identificadores.

Lo último que hay que hacer aquí es activar el esquema que se vinculará al **[!UICONTROL perfil]**.
Al habilitar su esquema para [!UICONTROL Profile], se asegura de que todos los datos enviados a Adobe Experience Platform con este esquema formarán parte del perfil del cliente en tiempo real, lo que garantiza que todos esos datos se puedan usar en tiempo real para consultas, segmentación y activación.

Para ello, haga clic en el nombre del esquema.

![Ingesta de datos](./images/schemastructureeee.png)

En la ficha derecha del esquema, verá una opción **[!UICONTROL Perfil]**, que está desactivada actualmente. Haga clic en el conmutador [!UICONTROL Perfil] - para habilitarlo.

![Ingesta de datos](./images/upswitcheree.png)

Verá este mensaje. - ¿Por qué? Haga clic en **[!UICONTROL Habilitar]** para habilitar este esquema para el perfil.

![Ingesta de datos](./images/sureeewv.png)

El esquema ahora está configurado para formar parte del Perfil del cliente en tiempo real.

Haga clic en **[!UICONTROL Guardar]** para guardar el esquema.

![Ingesta de datos](./images/saveeewv.png)

Ya ha terminado de crear esquemas activados para utilizarlos en el perfil del cliente en tiempo real.

Veamos los conjuntos de datos en el siguiente ejercicio.

Siguiente Paso: [1.2.3 Configurar Conjuntos De Datos](./ex3.md)

[Volver al módulo 1.2](./data-ingestion.md)

[Volver a todos los módulos](../../../overview.md)
