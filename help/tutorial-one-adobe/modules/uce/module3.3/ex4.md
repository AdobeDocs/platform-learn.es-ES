---
title: 'Offer decisioning: Pruebe la decisión en el sitio web de demostración'
description: Prueba de la decisión mediante el sitio web de demostración
kt: 5342
doc-type: tutorial
source-git-commit: 926f0f1f6d6b557fd7e59a89aaa3e09d831c82a6
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 2%

---

# 3.3.4 Combinación de Adobe Target y Offer Decisioning

## 3.3.4.1 Recopilar el vínculo que se puede compartir del proyecto de demostración

Para cargar el proyecto del sitio web de demostración en Adobe Target, primero debe recopilar un vínculo especial que permita a Adobe Target cargar el proyecto del sitio web de demostración.

Para ello, vaya a [https://dsn.adobe.com/projects](https://builder.adobedemo.com/projects). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en el proyecto del sitio web para abrirlo.

![RTCDP](./images/builder1.png)

Ahora va a ver esto. Ir a **Compartir**. Haga clic en **Generar vínculo** y, a continuación, copie el vínculo en el portapapeles.

![RTCDP](./images/builder2.png)

Vaya a [https://bitly.com](https://bitly.com), pegue el vínculo que ha copiado y haga clic en **Crear el vínculo**.

![RTCDP](./images/builder4.png)

Ahora obtendrá un vínculo abreviado, con este aspecto: `https://adobe.ly/3PpGcFk`. Necesitará ese vínculo en el próximo ejercicio.

![RTCDP](./images/builder5.png)

## 3.3.4.2 Recopilación

Ahora ve a la página principal de Adobe Experience Cloud al [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Haga clic en **Target**.

En la página de inicio de **Adobe Target**, verás todas las actividades existentes. Haga clic en **Crear actividad** y luego en **Segmentación de experiencias**.

Ahora selecciona **Visual** y pega el vínculo abreviado en el campo **Introducir URL de actividad**. Haga clic en **Crear**.

![RTCDP](./images/exclatcrxt1.png)

A continuación, verá que el proyecto del sitio web de demostración se carga en el Compositor de experiencias visuales.

>[!NOTE]
>
>Si el sitio web no se carga correctamente, instale y habilite esta extensión de Chrome: **Adobe Target VEC Helper** desde la tienda web de Chrome e inténtelo de nuevo.

![RTCDP](./images/vec1.png)

Haga clic en el área que contiene la oferta de Disney+. Asegúrese de seleccionar el **contenedor** completo. Haga clic en **Insertar antes** y, a continuación, seleccione **Decisión de oferta**.

![RTCDP](./images/vec3.png)

Entonces verá esta ventana emergente. Seleccione su zona protegida `--aepSandboxName--` y luego seleccione la ubicación **Web - Imagen**.

![RTCDP](./images/vec4.png)

A continuación, seleccione su decisión `--aepUserLdap-- - CitiSignal Decision`. Haga clic en **Guardar**.

![RTCDP](./images/vec5.png)

Entonces verá esto... Haga clic en **Revisar regla**.

![RTCDP](./images/vec5a.png)

Asegúrese de agregar una regla de plantilla adicional **URL** **contiene** **su-nombre-proyecto**. Haga clic en **Guardar**.

![RTCDP](./images/vec6.png)

Entonces verá esto... Haga clic en **Next**.

![RTCDP](./images/vec7.png)

Escriba un nombre para la oferta, use este nombre: `--aepUserLdap-- - XT with Offers (VEC)`. Haga clic en **Next**.

![RTCDP](./images/vec8.png)

Entonces verá esto... Defina su **métrica de objetivo** tal como se indicó. Haga clic en **Guardar y cerrar**.

![RTCDP](./images/vec9.png)

La oferta se habrá creado y se publicará. Una vez publicada la oferta, puede activarla.

![RTCDP](./images/vec11.png)

Paso siguiente: [3.3.5 Usa tu decisión en un correo electrónico y sms](./ex5.md)

[Volver al módulo 3.3](./offer-decisioning.md)

[Volver a todos los módulos](./../../../overview.md)
