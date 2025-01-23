---
title: Recopilación de datos - FAC - Crear una composición federada
description: Foundation - FAC - Crear una composición federada
kt: 5342
doc-type: tutorial
exl-id: dc044a26-f16a-491e-a795-4cd16f211256
source-git-commit: f6881cc2c993941f60e440ce0c367a139ae80b00
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 3%

---

# 3.1.3 Crear una composición federada

Ahora puede configurar la composición de audiencias federadas en AEP.

Inicie sesión en Adobe Experience Platform desde esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./images/sb1.png)

## 3.1.3.1 Crear su audiencia

En el menú de la izquierda, ve a **Audiencias** y luego a **Composiciones federadas**. Haga clic en **Crear composición**.

![CARA](./images/fedcomp1.png)

Para la etiqueta, use esto: `--aepUserLdap-- - CitiSignal Fiber`. Seleccione el modelo de datos que creó en el ejercicio anterior, que se llama `--aepUserLdap-- - CitiSignal Snowflake Data Model`. Haga clic en **Crear**.

![CARA](./images/fedcomp2.png)

Entonces verá esto...

![CARA](./images/fedcomp3.png)

Haga clic en el icono **+** y luego en **Generar audiencia**.

![CARA](./images/fedcomp4.png)

Entonces verá esto... Seleccione **Crear audiencia**. Haga clic en el icono **search** para seleccionar un esquema.

![CARA](./images/fedcomp5.png)

Seleccione el esquema **CK_HOUSEHOLDS**. Haga clic en **Confirmar**.

![CARA](./images/fedcomp6.png)

A continuación, haga clic en **Continuar**.

![CARA](./images/fedcomp7.png)

Ahora puede empezar a crear la consulta que se enviará al Snowflake. Haga clic en el icono **+** y, a continuación, haga clic en **Condición personalizada**.

![CARA](./images/fedcomp8.png)

Seleccione el atributo **ISELIGIBLEFORFIBER** Haga clic en **Confirmar**.

![CARA](./images/fedcomp9.png)

Entonces verá esto... Establezca el campo **Value** en **True**. Haga clic en **Calcular** para insertar la consulta en el Snowflake y obtener una estimación de los perfiles que ahora cumplen los requisitos.

![CARA](./images/fedcomp10.png)

A continuación, haga clic de nuevo en el icono **+** y luego en **Condición personalizada** para agregar otra condición.

![CARA](./images/fedcomp11.png)

La segunda condición que se debe agregar es: `Is the user an existing CitiSignal Mobile subscriber?`. La manera de responder a esa pregunta es usar la relación entre el hogar y el cliente principal del hogar, que se define en otra tabla, **CK_PERSONS**. Puede explorar en profundidad el menú de atributos mediante el vínculo **household2person**.

![CARA](./images/fedcomp12.png)

Seleccione el atributo **ISMOBILESUB** y haga clic en **Confirmar**.

![CARA](./images/fedcomp13.png)

Establezca el campo **Value** en **True**. Vuelva a hacer clic en **Calcular** para actualizar el número de perfiles de destino. Haga clic en **Confirmar**.

![CARA](./images/fedcomp14.png)

Haga clic en el icono **+** y, a continuación, haga clic en **Guardar audiencia**.

![CARA](./images/fedcomp15.png)

Establezca la **etiqueta de audiencia** en `--aepUserLdap-- - CitiSignal Eligible for Fiber`.

Haga clic en **+ Agregar asignación de audiencia**.

![CARA](./images/fedcomp16.png)

Seleccione **HOUSEHOLD_ID** y haga clic en **Confirmar**.

![CARA](./images/fedcomp17.png)

Haga clic en **+ Agregar asignación de audiencia**.

![CARA](./images/fedcomp18.png)

Desglose haciendo clic en **Dimensión de segmentación**.

![CARA](./images/fedcomp18a.png)

Desglose haciendo clic en el vínculo **hogar2persona**.

![CARA](./images/fedcomp18b.png)

Seleccione el campo **NAME**. Haga clic en **Confirmar**.

![CARA](./images/fedcomp18c.png)

Haga clic en **+ Agregar asignación de audiencia**.

![CARA](./images/fedcomp20.png)

Desglose haciendo clic en **Dimensión de segmentación**.

![CARA](./images/fedcomp20a.png)

Desglose haciendo clic en el vínculo **hogar2persona**.

![CARA](./images/fedcomp20b.png)

Seleccione el campo **CORREO ELECTRÓNICO**. Haga clic en **Confirmar**.

![CARA](./images/fedcomp20c.png)

Entonces verá esto... Ahora necesita establecer el **campo de identidad principal**, establézcalo en **Household2person_EMAIL**.

Haga clic en **Guardar**.

![CARA](./images/fedcomp21.png)

Su composición ha finalizado. Haga clic en **Iniciar** para ejecutarlo.

La consulta ahora se inserta en Snowflake, que consultará los datos de origen allí. Los resultados se devolverán a AEP, pero los datos de origen permanecen en Snowflake.

La audiencia ahora se rellena y se puede segmentar desde el ecosistema de AEP.

![CARA](./images/fedcomp22.png)

Siguiente paso: [Resumen y beneficios](./summary.md)

[Volver al módulo 3.1](./fac.md)

[Volver a todos los módulos](../../../overview.md)
