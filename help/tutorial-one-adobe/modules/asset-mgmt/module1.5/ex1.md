---
title: Introducción a Adobe Commerce as a Cloud Service
description: Introducción a Adobe Commerce as a Cloud Service
kt: 5342
doc-type: tutorial
exl-id: 8603c8e2-c3ba-4976-9703-cef9e63924b8
source-git-commit: 7e0214226eaee0586d036d46de39c08046d43893
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 15%

---

# 1.5.1 Introducción a Adobe Commerce as a Cloud Service

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Asegúrese de que está en el entorno correcto, que debe llamarse `--aepImsOrgName--`. Haga clic en **Commerce**.

![AEM Assets](./images/accs1.png)

## 1.5.1.1: cree su instancia de ACCS

Entonces debería ver esto. Haga clic en **+ Agregar instancia**.

![AEM Assets](./images/accs2.png)

Rellene los campos de esta manera:

- **Nombre de instancia**:

```
--aepUserLdap-- - ACCS
```

- **Entorno**: `Sandbox`
- **Región**: `North America`

Haga clic en **Agregar instancia**.

![AEM Assets](./images/accs3.png)

Su instancia se está creando. Esto puede tardar de 5 a 10 minutos.

![AEM Assets](./images/accs4.png)

Una vez que la instancia esté lista, haga clic en la instancia para abrirla.

![AEM Assets](./images/accs5.png)

## 1.5.1.2 Configurar su almacén de CitiSignal

Entonces debería ver esto. Haz clic en **Iniciar sesión con Adobe ID** y luego inicia sesión.

![AEM Assets](./images/accs6.png)

Una vez que haya iniciado sesión, debería ver esta página de inicio. El primer paso es configurar su tienda de CitiSignal en Commerce. Haga clic en **Tiendas**.

![AEM Assets](./images/accs7.png)

Haga clic en **Todas las tiendas**.

![AEM Assets](./images/accs8.png)

Haga clic en **Crear sitio web**.

![AEM Assets](./images/accs9.png)

Rellene los campos de esta manera:

- **Nombre**:

```
CitiSignal
```

- **Código**:

```
citisignal
```

Haga clic en **Guardar sitio web**.

![AEM Assets](./images/accs10.png)

Entonces deberías estar de vuelta aquí. Haga clic en **Crear tienda**.

![AEM Assets](./images/accs11.png)

Rellene los campos de esta manera:

- **Sitio web**:

```
CitiSignal
```

- **Nombre**:

```
CitiSignal
```

- **Código**:

```
citisignal
```

- **Categoría raíz**: `Default Category`

Haga clic en **Guardar tienda**.

![AEM Assets](./images/accs12.png)

Entonces deberías estar de vuelta aquí. Haga clic en **Crear vista de tienda**.

![AEM Assets](./images/accs13.png)

Rellene los campos de esta manera:

- **Almacén**:

```
CitiSignal
```

- **Nombre**:

```
CitiSignal
```

- **Código**:

```
citisignal
```

- **Estado**: `Enabled`

Haga clic en **Guardar vista de tienda**.

![AEM Assets](./images/accs14.png)

Entonces debería ver este mensaje. Haga clic en **Aceptar**.

![AEM Assets](./images/accs15.png)

Entonces deberías estar de vuelta aquí. Haga clic en el sitio web **CitiSignal** para abrirlo.

![AEM Assets](./images/accs16.png)

Marque la casilla de verificación para establecer este sitio web como el sitio web predeterminado.

Haga clic en **Guardar sitio web**.

![AEM Assets](./images/accs16a.png)

Entonces deberías estar de vuelta aquí.

![AEM Assets](./images/accs16.png)

## 1.5.1.3 Configurar categorías y productos

Vaya a **Catálogo** y luego seleccione **Categorías**.

![AEM Assets](./images/accs17.png)

Seleccione **Categoría predeterminada** y haga clic en **Agregar subcategoría**.

![AEM Assets](./images/accs18.png)

Escriba el siguiente nombre y haga clic en **Guardar**.

```
Phones
```

![AEM Assets](./images/accs19.png)

Seleccione **Categoría predeterminada** y luego haga clic en **Agregar subcategoría** de nuevo.

![AEM Assets](./images/accs20.png)

Escriba el siguiente nombre y haga clic en **Guardar**.

```
Watches
```

![AEM Assets](./images/accs21.png)

Seleccione **Categoría predeterminada** y luego haga clic en **Agregar subcategoría** de nuevo.

![AEM Assets](./images/accs20a.png)

Escriba el siguiente nombre y haga clic en **Guardar**.

```
Plans
```

![AEM Assets](./images/accs21a.png)

Seleccione **Categoría predeterminada** y luego haga clic en **Agregar subcategoría** de nuevo.

![AEM Assets](./images/accs20b.png)

Escriba el siguiente nombre y haga clic en **Guardar**.

```
Entertainment
```

![AEM Assets](./images/accs21b.png)

Luego debería tener 4 categorías creadas.

![AEM Assets](./images/accs22.png)

A continuación, ve a **Catálogo** y selecciona **Productos**.

![AEM Assets](./images/accs23.png)

Entonces debería ver esto. Haga clic en **Agregar producto**.

![AEM Assets](./images/accs24.png)

Configure el producto de esta manera:

- **Nombre de producto**:

```
iPhone Air
```

- **SKU**:

>[!NOTE]
>
>Asegúrese de que el campo SKU sea idéntico al valor siguiente y de que no haya espacios en este campo.

```
iPhone-Air
```

- **Precio**:

```
999
```

- **Cantidad**:

```
10000
```

- **Categorías**: seleccione `Phones`

Haga clic en **Guardar**.

![AEM Assets](./images/accs25.png)

Desplácese hasta **Configuraciones** y haga clic en **Crear configuraciones**.

![AEM Assets](./images/accs26.png)

Entonces debería ver esto. Haga clic en **Crear nuevo atributo**.

![AEM Assets](./images/accs27.png)

Establezca la **Etiqueta predeterminada** con el siguiente valor y, a continuación, haga clic en **Agregar opción** en **Administrar opciones**.

```
Storage
```

![AEM Assets](./images/accs28.png)

Configure la primera opción con el siguiente valor en las 3 columnas y luego haga clic en **Agregar opción** de nuevo.

```
256GB
```

![AEM Assets](./images/accs29.png)

Configure la segunda opción con el siguiente valor en las 3 columnas y luego haga clic en **Agregar opción** de nuevo.

```
512GB
```

![AEM Assets](./images/accs30.png)

Configure la tercera opción con el siguiente valor en las 3 columnas.

```
1TB
```

![AEM Assets](./images/accs31.png)

Desplácese hacia abajo hasta **Propiedades de tienda**. Establezca las siguientes opciones en **Yes**:

- **Usar en la búsqueda**
- **Permitir etiquetas de HTML en tienda**
- **Visible en páginas de catálogo en Storefront**
- **Uso en la lista de productos**

![AEM Assets](./images/accs32.png)

Desplácese hacia arriba y haga clic en **Guardar atributo**.

![AEM Assets](./images/accs33.png)

Entonces debería ver esto. Seleccione ambos atributos para **color** y **almacenamiento** y haga clic en **Siguiente**.

![AEM Assets](./images/accs34.png)

Entonces debería ver esto. Ahora debe añadir las opciones de color disponibles. Para ello, haga clic en **Crear nuevo valor**.

![AEM Assets](./images/accs35.png)

Escriba el valor `Sky-Blue` y haga clic en **Crear nuevo valor**.

![AEM Assets](./images/accs36.png)

Escriba el valor `Light-Gold` y haga clic en **Crear nuevo valor**.

![AEM Assets](./images/accs37.png)

Escriba el valor `Cloud-White` y haga clic en **Crear nuevo valor**.

![AEM Assets](./images/accs38.png)

Escriba el valor `Space-Black`. Haga clic en **Seleccionar todo**

![AEM Assets](./images/accs39.png)

Seleccione las 3 opciones en **Almacenamiento** y haga clic en **Siguiente**.

![AEM Assets](./images/accs40.png)

Deje la configuración predeterminada y haga clic en **Siguiente**.

![AEM Assets](./images/accs41.png)

Entonces debería ver esto. Haga clic en **Generar productos**.

![AEM Assets](./images/accs42.png)

Establece la **cantidad** de cada producto en `10000`. Además, asegúrese de que la columna **SKU** no contenga espacios en ninguna de las SKU.

Haga clic en **Guardar**.

![AEM Assets](./images/accs43.png)

Haga clic en **Confirmar**.

![AEM Assets](./images/accs45.png)

Desplácese hacia abajo hasta **Producto en sitios web** y marque la casilla de **CitiSignal**.

Haga clic en **Guardar**.

![AEM Assets](./images/accs44.png)

Entonces debería ver esto. Haga clic en **Atrás**.

![AEM Assets](./images/accs46.png)

Ahora verá el producto **iPhone Air** y sus variaciones en el catálogo de productos.

![AEM Assets](./images/accs47.png)

## 1.5.1.4 Importar productos

CitiSignal vende más productos, por lo que para crear los productos restantes en el catálogo de productos, ahora necesita importarlos.

Vaya a **Sistema** y luego a **Importar**.

![AEM Assets](./images/accsimp1.png)

Seleccione los siguientes valores:

- **Tipo de entidad**: `Products`
- **Comportamiento de importación**: `Add/Update`
- **Estrategia de validación**: `Skip error entries`

Haga clic en **Elegir archivo**.

![AEM Assets](./images/accsimp2.png)

Descargue este archivo en su equipo: [product_catalog_import.csv.zip](./assets/product_catalog_import.csv.zip). Extraiga el archivo en su escritorio.

![AEM Assets](./images/accsimp7.png)

Seleccione el archivo **`product_catalog_import.csv`** y haga clic en **Abrir**.

![AEM Assets](./images/accsimp3.png)

Entonces debería ver esto. Haga clic en **Comprobar datos**.

![AEM Assets](./images/accsimp4.png)

Entonces debería ver esto. Haga clic en **Importar**.

![AEM Assets](./images/accsimp5.png)

Entonces debería ver esto.

![AEM Assets](./images/accsimp6.png)

Vaya a **Catálogo** y luego a **Productos**.

![AEM Assets](./images/accsimp8.png)

Desplácese hacia abajo para buscar los productos que acaba de importar.

![AEM Assets](./images/accsimp9.png)

Siguiente paso: [Conectar ACCS a AEM Sites CS/EDS Storefront](./ex2.md){target="_blank"}

Volver a [Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
