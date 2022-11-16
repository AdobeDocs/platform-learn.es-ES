---
title: 'offer decisioning: Pruebe la decisión mediante el sitio web de demostración'
description: Pruebe la decisión mediante el sitio web de demostración
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: cdb2ba7d-bfc3-43ce-b9a1-1f0866322589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 4%

---

# 9.4 Combinación de Adobe Target y Offer decisioning

## 9.4.1 Recopile el vínculo que se puede compartir de su proyecto de demostración

Para cargar el proyecto del sitio web de demostración en Adobe Target, primero debe recopilar un vínculo especial que permita a Adobe Target cargar el proyecto del sitio web de demostración.

Para ello, vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión en Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![RTCDP](./images/builder1.png)

Ahora verás esto. Haga clic en **Compartir**.

![RTCDP](./images/builder2.png)

Haga clic en **Generar vínculo** y, a continuación, copie el vínculo en el portapapeles.

![RTCDP](./images/builder3.png)

Vaya a [https://bitly.com](https://bitly.com), pegue el vínculo que ha copiado y haga clic en **Abreviar**. Ahora obtendrá un vínculo abreviado, que tiene este aspecto: `https://bit.ly/3JxN7aG`. Necesitará ese vínculo en el próximo ejercicio.

![RTCDP](./images/builder4.png)

## 9.4.2 Recopilación

Ahora vaya a la página de inicio de Adobe Experience Cloud yendo a [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Haga clic en **Target**.

![RTCDP](../module6/images/excl.png)

En el **Adobe Target** página principal, verá todas las actividades existentes.

![RTCDP](../module6/images/exclatov.png)

Haga clic en **+ Crear actividad** para crear una nueva actividad.

![RTCDP](../module6/images/exclatcr.png)

Select **Segmentación de experiencias**.

![RTCDP](./images/exclatcrxt.png)

Ahora seleccione **Visual** y pegue el vínculo abreviado en el campo **Introducir URL de actividad**. Haga clic en **Siguiente**.

![RTCDP](./images/exclatcrxt1.png)

A continuación, verá que el proyecto del sitio web de demostración se está cargando en el Compositor de experiencias visuales.

![RTCDP](./images/vec1.png)

Vaya a **Examinar** modo para hacer clic **Permitir todo** en la ventana emergente de consentimiento de la cookie.

![RTCDP](./images/vec2.png)

Haga clic en el área que contiene el texto **Categorías destacadas**. Haga clic en **Insertar antes** y, a continuación, seleccione **Decisión de oferta**.

![RTCDP](./images/vec3.png)

Verá esta ventana emergente. Seleccione el entorno limitado `--aepSandboxId--` y, a continuación, seleccione la colocación **Web - Imagen**.

![RTCDP](./images/vec4.png)

A continuación, seleccione su decisión `--demoProfileLdap-- - Luma Decision`. Haga clic en **Guardar**.

![RTCDP](./images/vec5.png)

Entonces verás esto. Asegúrese de agregar una regla de plantilla adicional **URL** **contains** **your-project-name**. Clic **Guardar**.

![RTCDP](./images/vec6.png)

Entonces verás esto. Haga clic en **Siguiente**.

![RTCDP](./images/vec7.png)

Escriba un nombre para la oferta, use este nombre: `--demoProfileLdap-- - XT with Offers (VEC)`. Haga clic en **Siguiente**.

![RTCDP](./images/vec8.png)

Entonces verás esto. Defina su **Métrica de objetivo** como se indica. Haga clic en **Guardar y cerrar**.

![RTCDP](./images/vec9.png)

La oferta se ha creado y se está publicando.

![RTCDP](./images/vec10.png)

Una vez publicada la oferta, puede activarla.

Paso siguiente: [9.5 Use su decisión en un mensaje de correo electrónico y SMS](./ex5.md)

[Volver al módulo 9](./offer-decisioning.md)

[Volver a todos los módulos](./../../overview.md)
