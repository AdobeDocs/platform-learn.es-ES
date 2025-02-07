---
title: Introducción a los servicios de traducción de AJO
description: Introducción a los servicios de traducción de AJO
kt: 5342
doc-type: tutorial
exl-id: ee0b8650-a59f-4888-8228-4caafe4143e4
source-git-commit: 3b3c62499bfed86ab13a657a816424879cab4f42
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 2%

---

# 3.2.1 Proveedor de traducciones

## 3.2.1.1 Configuración de Microsoft Azure Translator

Vaya a [https://portal.azure.com/#home](https://portal.azure.com/#home).

![Traducciones](./images/transl1.png)

En la barra de búsqueda, escriba `translators`. A continuación, haga clic en **+ Crear**.

![Traducciones](./images/transl2.png)

Seleccione **Crear traductor**.

![Traducciones](./images/transl3.png)

Elija su **ID de suscripción** y **grupo de recursos**.
Establezca **Región** en **Global**.
Establezca **Nivel de precios** en **F0** gratis.

Seleccione **Revisar + crear**.

![Traducciones](./images/transl4.png)

Seleccione **Crear**.

![Traducciones](./images/transl5.png)

Seleccione **Ir al recurso**.

![Traducciones](./images/transl6.png)

En el menú de la izquierda, vaya a **Administración de recursos** > **Claves y extremo**. Haga clic en para copiar la clave.

![Traducciones](./images/transl7.png)

## 3.2.1.2 Diccionario local

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/). Haga clic en **Journey Optimizer**.

![Traducciones](./images/ajolp1.png)

En el menú de la izquierda, ve a **Traducciones** y luego a **Diccionario local**. Si ve este mensaje, haga clic en **Agregar configuraciones regionales predeterminadas**.

![Traducciones](./images/locale1.png)

Entonces debería ver esto.

![Traducciones](./images/locale2.png)

## 3.2.1.3 Configuración del proveedor de traducciones en AJO

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/). Haga clic en **Journey Optimizer**.

![Traducciones](./images/ajolp1.png)

En el menú de la izquierda, ve a **Traducciones** y luego a **Proveedores**. Haga clic en **Agregar proveedor**.

![Traducciones](./images/transl8.png)

En **Proveedores**, seleccione **Microsoft Translator**. Marque la casilla de verificación para habilitar el uso del proveedor de traducción. Pegue la clave copiada de los traductores de Microsoft Azure. A continuación, haga clic en **Validar credenciales**.

![Traducciones](./images/transl9.png)

Las credenciales se deben validar correctamente. Si es así, desplácese hacia abajo para seleccionar los idiomas para la traducción.

![Traducciones](./images/transl10.png)

Asegúrese de seleccionar `[en-US] English`, `[es] Spanish`, `[fr] French`, `[nl] Dutch`.

![Traducciones](./images/transl11.png)

Desplácese hacia arriba y haga clic en **Guardar**.

![Traducciones](./images/transl12.png)

Su **proveedor de traducciones** ya está listo para usarse.

![Traducciones](./images/transl13.png)

## 3.2.1.4 Configurar el proyecto de traducciones

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/). Haga clic en **Journey Optimizer**.

![Traducciones](./images/ajolp1.png)

En el menú de la izquierda, ve a **Traducciones** y luego a **Diccionario local**. Si ve este mensaje, haga clic en **Crear proyecto**.

![Traducciones](./images/ajoprovider1.png)

Escriba el nombre `--aepUserLdap-- - Translations`, establezca **Configuración regional de Source** en `[en-US] English - United States` y marque la casilla de verificación para habilitar **Publicar automáticamente traducciones aprobadas**. A continuación, haga clic en **+ Agregar configuración regional**.

![Traducciones](./images/ajoprovider1a.png)

Busque `fr`, active la casilla de verificación de `[fr] French` y luego active la casilla de verificación de **Microsoft Translator**. Haga clic en **+ Agregar configuración regional**.

![Traducciones](./images/ajoprovider2.png)

Busque `es`, active la casilla de verificación de `[es] Spanish` y luego active la casilla de verificación de **Microsoft Translator**. Haga clic en **+ Agregar configuración regional**.

![Traducciones](./images/ajoprovider3.png)

Busque `nl`, active la casilla de verificación de `[nl] Spanish` y luego active la casilla de verificación de **Microsoft Translator**. Haga clic en **+ Agregar configuración regional**.

![Traducciones](./images/ajoprovider6.png)

Haga clic en **Guardar**.

![Traducciones](./images/ajoprovider8.png)

Su proyecto **Traducciones** ya está listo para usarse.

![Traducciones](./images/ajoprovider9.png)

Ha terminado este ejercicio.

## Pasos siguientes

Vaya a [3.2.2 y cree su campaña](./ex2.md)

Volver a [Módulo 3.2](./ajotranslationsvcs.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}