---
title: Activación de GenStudio for Performance Marketing Campaign en Meta
description: Activación de GenStudio for Performance Marketing Campaign en Meta
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 2c7ef715-b8af-4a5b-8873-5409b43d7cb0
source-git-commit: b8f7b370a5aba82a0dcd6e7f4f0222fe209976f7
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# 1.3.3 Activación de la campaña en Meta

>[!IMPORTANT]
>
>Para completar este ejercicio, debe tener acceso a un entorno de trabajo de AEM Assets CS Author con AEM Content Hub habilitado. Si sigue el ejercicio [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}, tendrá acceso a dicho entorno.

>[!IMPORTANT]
>
>Si ha configurado anteriormente un programa de AEM Assets CS con un entorno de Author y AEM Assets, puede ser que la zona protegida de AEM CS haya hibernado. Dado que la dehibernación de una zona protegida de este tipo tarda de 10 a 15 minutos, sería aconsejable iniciar el proceso de dehibernación ahora para que no tenga que esperar más adelante.

## 1.3.3.1 Crear campaña

En **GenStudio for Performance Marketing**, ve a **Campañas** en el menú de la izquierda. Haga clic en **+ Agregar campaña**.

![GSPeM](./images/gscampaign1.png)

Luego debería ver una descripción general de la campaña vacía.

![GSPeM](./images/gscampaign2.png)

Para el nombre de campo, use `--aepUserLdap-- - CitiSignal Fiber Launch Campaign`.

Para el campo **Descripción**, use el siguiente texto.

```
The CitiSignal Fiber Launch campaign introduces CitiSignal’s flagship fiber internet service—CitiSignal Fiber Max—to key residential markets. This campaign is designed to build awareness, drive sign-ups, and establish CitiSignal as the go-to provider for ultra-fast, reliable, and future-ready internet. The campaign will highlight the product’s benefits for remote professionals, online gamers, and smart home families, using persona-driven messaging across digital and physical channels.
```

Para el campo **Objetivo**, use el siguiente texto.

```
Generate brand awareness in target regions
Drive early sign-ups and pre-orders for CitiSignal Fiber Max
Position CitiSignal as a premium, customer-first fiber internet provider
Educate consumers on the benefits of fiber over cable or DSL
```

Para el campo **Mensajería de clave**, usa el siguiente texto.

```
Supporting Points:
Symmetrical speeds up to 2 Gbps
Whole-home Wi-Fi 6E coverage
99.99% uptime guarantee
24/7 concierge support
No data caps or throttling
 Channels:
Digital Advertising: Google Display, YouTube pre-roll, Meta (Facebook/Instagram), TikTok (for gamers)
Email Marketing: Persona-segmented drip campaigns
Social Media: Organic and paid posts with testimonials, speed demos, and influencer partnerships
Out-of-Home (OOH): Billboards, transit ads in suburban commuter corridors
Local Events: Pop-up booths at tech expos, family festivals, and gaming tournaments
Direct Mail: Personalized flyers with QR codes for early sign-up discounts
 
Target Regions:
Primary Launch Markets:
Denver Metro Area, CO
Austin, TX
Raleigh-Durham, NC
Salt Lake City, UT
Demographic Focus:
Suburban neighborhoods with high remote work density
Areas with high smart home adoption
Zip codes with underserved or dissatisfied cable customers
```

Entonces debería tener esto:

![GSPeM](./images/gscampaign3.png)

Desplácese hacia abajo para ver más campos:

![GSPeM](./images/gscampaign4.png)

Para el campo **Iniciar**, establézcalo en la fecha de hoy.

Para el campo **Fin**, establézcalo en una fecha dentro de 1 mes.

Para el campo **Estado**, establézcalo en **Activo**.

Para el campo **Canales**, establézcalo en **Meta**, **Correo electrónico**, **Medios de pago**, **Pantalla**.

Para el campo **Regiones**, seleccione una región de su elección.

Para el campo del campo **Referencias** > **Productos**: elija el producto `--aepUserLdap-- - CitiSignal Fiber Max`.

**Referencias** > **Personas**: elija las personalidades `--aepUserLdap-- - Remote Professionals`, `--aepUserLdap-- - Online Gamers`, `--aepUserLdap-- - Smart Home Families`

Debería ver lo siguiente:

![GSPeM](./images/gscampaign5.png)

Su campaña ya está lista. Haga clic en la **flecha** para regresar.

![GSPeM](./images/gscampaign6.png)

A continuación, verá su campaña en la lista. Haga clic en el icono de vista de calendario para cambiar la vista al calendario de campañas.

![GSPeM](./images/gscampaign7.png)

Luego debería ver un calendario de campañas que dé una idea más visual de qué campañas están activas en cada momento.

![GSPeM](./images/gscampaign8.png)

## 1.3.3.2 Configuración de conexión a Meta

>[!IMPORTANT]
>
>Para configurar la conexión a Meta, debe tener una cuenta de usuario de Meta disponible y esa cuenta de usuario debe agregarse a una cuenta de Meta Business.

Para configurar la conexión con Meta, haga clic en los 3 puntos **...** y seleccione **Configuración**.

![GSPeM](./images/gsconnection1.png)

Haga clic en **Conectar** para **Meta Ads**.

![GSPeM](./images/gsconnection2.png)

Inicie sesión con su cuenta Meta. Haga clic en **Continuar**.

![GSPeM](./images/gsconnection3.png)

Si su cuenta está vinculada a una cuenta de Meta Business, podrá seleccionar el portafolio de negocios que se ha configurado en Meta.

![GSPeM](./images/gsconnection5.png)

Una vez establecida correctamente la conexión, haga clic en la línea que dice **X cuentas conectadas**.

![GSPeM](./images/gsconnection4.png)

A continuación, debería ver los detalles de la cuenta de Meta Business conectada a GenStudio for Performance Marketing.

![GSPeM](./images/gsconnection6.png)

## 1.3.3.3 Crear nuevo recurso

Vaya a [https://firefly.adobe.com/](https://firefly.adobe.com/){target="_blank"}. Escriba el mensaje `a neon rabbit running very fast through space` y haga clic en **Generar**.

![GSPeM](./images/gsasset1.png)

A continuación, verá varias imágenes que se generan. Elige la imagen que más te guste, haz clic en el icono **Compartir** de la imagen y luego selecciona **Abrir en Adobe Express**.

![GSPeM](./images/gsasset2.png)

A continuación, verá que la imagen que acaba de generar está disponible en Adobe Express para editarla. Ahora debe añadir el logotipo de CitiSignal en la imagen. Para ello, ve a **Marcas**.

![GSPeM](./images/gsasset3.png)

Debería ver la plantilla de marca CitiSignal que creó en GenStudio for Performance Marketing en Adobe Express. Haga clic para seleccionar la plantilla de marca que debe tener el nombre `--aepUserLdap-- - CitiSignal`.

![GSPeM](./images/gsasset4.png)

Vaya a **Logotipos** y haga clic en el logotipo **blanco** de Citisignal para colocarlo en la imagen.

![GSPeM](./images/gsasset5.png)

Coloque el logotipo de CitiSignal en la esquina superior izquierda.

![GSPeM](./images/gsasset6.png)

A continuación, haga clic en **Compartir**.

![GSPeM](./images/gsasset7.png)

Seleccionar **AEM Assets**.

![GSPeM](./images/gsasset8.png)

Haga clic en **Seleccionar carpeta**.

![GSPeM](./images/gsasset9.png)

Seleccione el repositorio de AEM Assets CS, que debe tener el nombre `--aepUserLdap-- - CitiSignal` y, a continuación, seleccione la carpeta `--aepUserLdap-- - CitiSignal Fiber Campaign`. Haga clic en **Seleccionar**.

![GSPeM](./images/gsasset11.png)

Entonces debería ver esto. Haga clic en **Cargar 1 recurso**. La imagen se cargará en AEM Assets CS.

![GSPeM](./images/gsasset12.png)

Vaya a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Abra **Experience Manager Assets**.

![GSPeM](./images/gsasset13.png)

Seleccione el entorno de AEM Assets CS, que debería llamarse `--aepUserLdap-- - CitiSignal dev`.

![GSPeM](./images/gsasset14.png)

Vaya a **Assets** y haga doble clic en la carpeta `--aepUserLdap-- - CitiSignal Fiber Campaign`.

![GSPeM](./images/gsasset15.png)

Entonces debería ver algo similar a esto. Haga doble clic en la imagen `--aepUserLdap-- - neon rabbit`.

![GSPeM](./images/gsasset16.png)

Se mostrará la imagen `--aepUserLdap-- - neon rabbit`. Cambie **Status** a **Approved** y luego haga clic en **Guardar**

>[!IMPORTANT]
>
>Si el estado de una imagen no se establece en **Aprobada**, la imagen no será visible en GenStudio for Performance Marketing. En GenStudio for Performance Marketing solo se puede acceder a los recursos aprobados.

![GSPeM](./images/gsasset17.png)

Cambie a GenStudio for Performance Marketing. En el menú de la izquierda, ve a **Assets** y selecciona tu repositorio de AEM Assets CS, que debería llamarse `--aepUserLdap-- - CitiSignal`. A continuación, verá que la imagen que acaba de crear y aprobar está disponible en GenStudio for Performance Marketing.

![GSPeM](./images/gsasset18.png)

## 1.3.3.4 Crear y aprobar metaanuncio

## 1.3.3.5 Publicar anuncio en Meta

## Pasos siguientes

Ir a [Resumen y beneficios](./summary.md){target="_blank"}

Volver a [GenStudio for Performance Marketing](./genstudio.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}
