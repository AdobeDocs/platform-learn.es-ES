---
title: 'Recopilación de datos: FAC: crear esquemas, modelos de datos y vínculos'
description: Foundation - FAC - Crear esquemas, modelos de datos y vínculos
kt: 5342
doc-type: tutorial
exl-id: 42004cb9-60b3-4ca8-97d9-3d169735c98f
source-git-commit: 246bb91496104818f357848f41b79523b7771638
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 2%

---

# 3.1.2 Creación de esquemas, modelos de datos y vínculos

Ahora puede configurar la base de datos federada en Adobe Experience Platform.

Inicie sesión en Adobe Experience Platform desde esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./images/sb1.png)

## 3.1.2.1 Configuración de una base de datos federada en AEP

Haga clic en **Bases de datos federadas** en el menú de la izquierda. A continuación, haga clic en **Agregar base de datos federada**.

![CARA](./images/fdb1.png)

Como **etiqueta**, use `--aepUserLdap-- - CitiSignal Snowflake` y, para el tipo, elija **Snowflake**.

En Detalles, debe rellenar las credenciales, que lucirán de esta manera:

![CARA](./images/fdb2.png)

**Servidor**:

En Snowflake, vaya a **Administración > Cuentas**. Haga clic en 3 **...** junto a su cuenta y luego en **Administrar direcciones URL**.

![CARA](./images/fdburl1.png)

Entonces verá esto... Copie la **URL actual** y péguela en el campo **Servidor** en AEP.

![CARA](./images/fdburl2.png)

**Usuario**: el nombre de usuario que creó anteriormente, en el ejercicio 1.3.1.1
**Contraseña**: la contraseña que creó anteriormente, en el ejercicio 1.3.1.1
**Base de datos**: use **CITISIGNAL**

Así que finalmente, deberías tener esto. Haga clic en **Probar conexión**. Si la prueba se realiza correctamente, haga clic en **Implementar funciones**, que creará funciones en el lado del Snowflake que son necesarias para el motor de flujo de trabajo.

Una vez que la conexión se haya probado correctamente y se hayan implementado las funciones, la configuración se almacenará.

![CARA](./images/fdb3.png)

Cuando vuelva al menú **Bases de datos federadas**, verá su conexión allí.

![CARA](./images/fdb4.png)

## 3.1.2.2 Crear esquemas en AEP

En el menú de la izquierda, haz clic en **Modelos** y luego ve a **Esquemas**. Haga clic en **Crear esquema**.

![CARA](./images/fdb5.png)

Seleccione su base de datos federada y haga clic en **+ Agregar tablas**.

![CARA](./images/fdb6.png)

Entonces verá esto... Seleccione las 5 tablas que creó en Snowflake anteriormente:

- `CK_HOUSEHOLDS`
- `CK_MOBILE_DATA_USAGE`
- `CK_MONTHLY_DATA_USAGE`
- `CK_PERSONS`
- `CK_USERS`

Haga clic en **Agregar**.

![CARA](./images/fdb7.png)

A continuación, AEP cargará la información de cada tabla y la mostrará en la interfaz de usuario.

Para cada tabla, puede:

- cambiar la etiqueta del esquema
- añadir una descripción
- cambie el nombre de todos los campos y establezca su visibilidad
- seleccione la clave principal del esquema

Para este ejercicio, no es necesario realizar cambios.

Haga clic en **Crear**.

![CARA](./images/fdb8.png)

Entonces verá esto... Puede hacer clic en cualquier esquema y revisar la información. Por ejemplo, haga clic en **CK_PERSONS**.

![CARA](./images/fdb9.png)

A continuación, verá esto, con la capacidad de editar la configuración. Haga clic en **Datos** para ver una muestra de los datos de la base de datos del Snowflake.

![CARA](./images/fdb10.png)

A continuación, verá una muestra de los datos.

![CARA](./images/fdb11.png)

## 3.1.2.3 Crear un modelo en AEP

En el menú de la izquierda, ve a **Modelos** y luego a **Modelo de datos**. Haga clic en **Crear modelo de datos**.

![CARA](./images/fdb12.png)

Para la etiqueta, use `--aepUserLdap-- - CitiSignal Snowflake Data Model`. Haga clic en **Crear**.

![CARA](./images/fdb13.png)

Haga clic en **Agregar esquemas**.

![CARA](./images/fdb14.png)

Seleccione los esquemas y haga clic en **Agregar**.

![CARA](./images/fdb15.png)

Entonces verá esto... Haga clic en **Guardar**.

### `CK_USERS` - `CK_PERSONS`

Ahora puede empezar a definir vínculos entre esquemas. Para empezar a definir un vínculo, debe hacer clic en **Crear vínculos**.

![CARA](./images/fdb16.png)

En primer lugar, definamos el vínculo entre la tabla `CK_USERS` y `CK_PERSONS`.

Haga clic en **Agregar**.

![CARA](./images/fdb18.png)


### `CK_HOUSEHOLDS` - `CK_PERSONS`

Entonces volverás a estar aquí. Haga clic en **Crear vínculos** para crear otro vínculo.

![CARA](./images/fdb17.png)

A continuación, definamos el vínculo entre la tabla `CK_HOUSEHOLDS` y `CK_PERSONS`.

![CARA](./images/fdb19.png)

### `CK_USERS` - `CK_MONTHLY_DATA_USAGE`

Entonces volverás a estar aquí. Haga clic en **Crear vínculos** para crear otro vínculo.

![CARA](./images/fdb20.png)

A continuación, definamos el vínculo entre la tabla `CK_USERS` y `CK_MONTHLY_DATA_USAGE`.

![CARA](./images/fdb21.png)


### `CK_USERS` - `CK_HOUSEHOLDS`

Entonces volverás a estar aquí. Haga clic en **Crear vínculos** para crear otro vínculo.

![CARA](./images/fdb22.png)

A continuación, definamos el vínculo entre la tabla `CK_USERS` y `CK_HOUSEHOLDS`.

![CARA](./images/fdb23.png)

### `CK_USERS` - `CK_MOBILE_DATA_USAGE`

Entonces volverás a estar aquí. Haga clic en **Crear vínculos** para crear otro vínculo.

![CARA](./images/fdb24.png)

A continuación, definamos el vínculo entre la tabla `CK_USERS` y `CK_MOBILE_DATA_USAGE`.

![CARA](./images/fdb25.png)

Entonces debería ver esto. Haga clic en **Guardar**.

![CARA](./images/fdb26.png)

Ya ha finalizado la configuración en AEP. Ahora puede empezar a utilizar los datos federados en una composición de audiencia federada.

Paso siguiente: [3.1.3 Crear una composición federada](./ex3.md)

[Volver al módulo 3.1](./fac.md)

[Volver a todos los módulos](../../../overview.md)
