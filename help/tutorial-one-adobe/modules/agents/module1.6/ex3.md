---
title: Escalar fragmentos de contenido con el servidor ChatGPT y MCP
description: Escalar fragmentos de contenido con el servidor ChatGPT y MCP
kt: 5342
doc-type: tutorial
source-git-commit: 161950ccf1f253913612b9f264e584ca3537b0cd
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 1%

---

# 1.6.3 Escalar fragmentos de contenido con el servidor ChatGPT y MCP

>[!IMPORTANT]
>
>Para completar este ejercicio, debe tener acceso a un entorno de AEM Sites y Assets CS con EDS en funcionamiento, y los distintos agentes de AEM deben estar habilitados para la organización de IMS que utilice.
>
>Si aún no cuenta con ese entorno, vaya al ejercicio [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Siga las instrucciones allí y tendrá acceso a dicho entorno.

>[!IMPORTANT]
>
>Si ha configurado anteriormente un programa AEM CS con un entorno AEM Sites y Assets CS, es posible que la zona protegida de AEM CS haya estado en hibernación. Dado que la dehibernación de una zona protegida de este tipo tarda de 10 a 15 minutos, sería aconsejable iniciar el proceso de dehibernación ahora para que no tenga que esperar más adelante.

## 1.6.3.1 Crear modelo de fragmento de contenido

Vuelva a su entorno de Adobe Experience Manager Author, a **Herramientas** y luego vaya a **Explorador de configuración**.

![Agentes de AEM](./images/aemagentscfm1.png)

Haga clic en **Crear**.

![Agentes de AEM](./images/aemagentscfm2.png)

Use `Content Fragments` para los campos **Title** y **Name**.

Asegúrese de que las opciones **Modelos de fragmentos de contenido** y **Consultas persistentes de GraphQL** estén habilitadas.

Haga clic en **Crear**.

![Agentes de AEM](./images/aemagentscfm3.png)

Vuelva al entorno de Adobe Experience Manager Author y luego vaya a **Fragmentos de contenido**.

![Agentes de AEM](./images/aemagentscf1.png)

Vaya a **Modelos de fragmentos de contenido**, seleccione su configuración **Fragmentos de contenido** y haga clic en **Crear**.

![Agentes de AEM](./images/aemagentscfm4.png)

Use el nombre `--aepUserLdap-- - CitiSignal CFM`. Haz clic en **Crear y abrir**.

![Agentes de AEM](./images/aemagentscfm5.png)

Entonces debería ver esto. Arrastre y suelte un campo **Texto de una sola línea** en el lienzo.

![Agentes de AEM](./images/aemagentscfm6.png)

Cambie el campo **Etiqueta de campo** a `Header`.

![Agentes de AEM](./images/aemagentscfm7.png)

Volver a **tipos de datos**. Arrastre y suelte un campo **Texto de una sola línea** en el lienzo.

![Agentes de AEM](./images/aemagentscfm8.png)

Cambie el campo **Etiqueta de campo** a `Subheader`.

![Agentes de AEM](./images/aemagentscfm9.png)

Volver a **tipos de datos**. Arrastre y suelte un campo **Texto multilínea** en el lienzo.

![Agentes de AEM](./images/aemagentscfm10.png)

Cambie el campo **Etiqueta de campo** a `Detail Description`.

![Agentes de AEM](./images/aemagentscfm11.png)

Volver a **tipos de datos**. Arrastre y suelte un campo **Texto de una sola línea** en el lienzo.

![Agentes de AEM](./images/aemagentscfm12.png)

Cambie el campo **Etiqueta de campo** a `CTA Text`.

![Agentes de AEM](./images/aemagentscfm13.png)

Volver a **tipos de datos**. Arrastre y suelte un campo **Texto de una sola línea** en el lienzo.

![Agentes de AEM](./images/aemagentscfm14.png)

Cambie el campo **Etiqueta de campo** a `CTA Link`. Haga clic en **Guardar**.

![Agentes de AEM](./images/aemagentscfm15.png)

Entonces debería ver esto.

![Agentes de AEM](./images/aemagentscfm16.png)

Seleccione el modelo de fragmento de contenido y haga clic en **Publicar**.

![Agentes de AEM](./images/aemagentscfm17.png)

Haga clic en **Publicar**.

![Agentes de AEM](./images/aemagentscfm18.png)

## 1.6.3.2 Crear fragmento de contenido

Vuelva al entorno de Adobe Experience Manager Author y luego vaya a **Fragmentos de contenido**.

![Agentes de AEM](./images/aemagentscf1.png)

Entonces debería ver esto. Haga clic en **Crear** y luego seleccione **Carpeta**.

![Agentes de AEM](./images/aemagentscf2.png)

Escriba el título: `--aepUserLdap-- - CF`. Haga clic en **Crear**.

![Agentes de AEM](./images/aemagentscf3.png)

Regresa a tu entorno de Adobe Experience Manager Author y luego ve a **Assets**.

![Agentes de AEM](./images/aemagentscfmm1.png)

Ir a **Archivos**.

![Agentes de AEM](./images/aemagentscfmm2.png)

Seleccione la carpeta que acaba de crear, que debe tener el nombre `--aepUserLdap-- - CF` y haga clic en **Propiedades**.

![Agentes de AEM](./images/aemagentscfmm3.png)

Vaya a **Cloud Services** y haga clic en el icono **carpeta**.

![Agentes de AEM](./images/aemagentscfmm4.png)

Seleccione la configuración de nube que creó anteriormente, que debería llamarse **Fragmentos de contenido**. Haga clic en **Seleccionar**.

![Agentes de AEM](./images/aemagentscfmm5.png)

Entonces debería ver esto. Haga clic en **Guardar y cerrar**.

![Agentes de AEM](./images/aemagentscfmm6.png)

Vuelva al entorno de Adobe Experience Manager Author y luego vaya a **Fragmentos de contenido**.

![Agentes de AEM](./images/aemagentscf1.png)

Entonces debería ver esto. Haga clic en **Crear** y luego seleccione **Fragmento de contenido**.

![Agentes de AEM](./images/aemagentscf4.png)

Seleccione el **Modelo de fragmento de contenido** que creó anteriormente, con el nombre `--aepUserLdap-- - CitiSignal CFM`. Use el nombre `--aepUserLdap-- CitiSignal Fiber Max`.

Haz clic en **Crear y abrir**.

![Agentes de AEM](./images/aemagentscf5.png)

Entonces debería ver esto.

![Agentes de AEM](./images/aemagentscf5a.png)

Rellene los campos de esta manera:

- **Encabezado**: `CitiSignal Fiber Max`
- **Subencabezado**: `Experience high speed internet now`
- **Descripción detallada**:

```
Experience the future of connectivity with CitiSignal Fiber Max, the ultimate solution for high-speed internet. Designed for homes and businesses that demand performance, Fiber Max delivers blazing-fast fiber speeds, ensuring seamless streaming, ultra-responsive gaming, and crystal-clear video calls.

Key Features:

Unmatched Speed: Enjoy lightning-fast downloads and uploads powered by cutting-edge fiber technology.
Reliable Performance: Consistent connectivity for work, entertainment, and everything in between.
Future-Ready: Built to handle the growing demands of smart homes and digital lifestyles.
Unlimited Potential: No data caps, no throttling—just pure speed.
Why Choose CitiSignal Fiber Max? Stay ahead with internet that works as hard as you do. Whether you’re powering a remote office or streaming in 4K, Fiber Max ensures you never miss a beat.
```

**Texto de CTA**: `Upgrade now by signing your new contract!`
**Vínculo de CTA**: `https://techinsiders68.adobedemosystem.com/`

Haga clic en **Publicar** y luego seleccione **Ahora**.

![Agentes de AEM](./images/aemagentscf6.png)

Haga clic en **Publicar**.

![Agentes de AEM](./images/aemagentscf7.png)

## 1.6.3.3 Configurar el servidor MCP en ChatGPT

>[!NOTE]
>
>El uso de Adobe Marketing Agent en ChatGPT requiere lo siguiente:
>- una versión de pago de ChatGPT Enterprise de OpenAI
>- uso del cliente web ChatGPT Enterprise

Vaya a [https://chatgpt.com/](https://chatgpt.com/){target="_blank"} e inicie sesión con los detalles de su cuenta. Una vez que haya iniciado sesión, debería ver esto. Haga clic en su nombre de usuario y seleccione **Configuración**.

![ChatGPT](./images/chatgpt2.png)

Vaya a **Aplicaciones** y seleccione **Configuración avanzada**.

![ChatGPT](./images/chatgpt3.png)

Active **Modo de desarrollador** y luego haga clic en **Atrás**.

![ChatGPT](./images/chatgpt4.png)

Haga clic en **Crear aplicación**.

![ChatGPT](./images/chatgpt5.png)

Rellene los campos de esta manera:

- **Nombre**: `aem`
- **URL del servidor MCP**: `https://mcp.adobeaemcloud.com/adobe/mcp/content`
- **Autenticación**: `OAuth`

Marque la casilla de verificación de **Entiendo y deseo continuar**.

Haga clic en **Crear**.

![ChatGPT](./images/chatgpt6.png)

ChatGPT intentará conectarse a su cuenta de Adobe. Seleccione **Permitir acceso** y luego tendrá que iniciar sesión con su cuenta de Adobe.

Una vez que haya iniciado sesión correctamente, debería ver que su Adobe Marketing Agent ahora está conectado correctamente.

![ChatGPT](./images/chatgpt8.png)

## 1.6.3.4: usar el servidor MCP de AEM en ChatGPT

Cierre esta ventana.

![Agent Orchestrator](./images/chatgpt8.png)

Entonces debería ver esto. Haga clic en el icono **+**, vaya a **Más** y luego seleccione **aem**.

![Agent Orchestrator](./images/chatgpt10.png)

Escriba la siguiente solicitud y haga clic en **Enviar**.

```
I just created a new custom mcp server named 'aem'. what can I do with that?
```

![Agent Orchestrator](./images/chatgpt11.png)

Entonces deberías ver algo como esto. Escriba la siguiente solicitud y haga clic en **Enviar**.

```
use the author url https://author-pXXXXXX-eXXXXXXX.adobeaemcloud.com/ from now on
```

![Agent Orchestrator](./images/chatgpt12.png)

Entonces deberías ver algo como esto. Escriba la siguiente solicitud y haga clic en **Enviar**.

```
find the content fragment --aepUserLdap-- - CitiSignal Fiber Max and make a variation called --aepUserLdap-- - CitiSignal Fiber Max (FR), then translate all fields into french
```

![Agent Orchestrator](./images/chatgpt13.png)

Haga clic en **Crear variación de fragmento**.

![Agent Orchestrator](./images/chatgpt14.png)

Haga clic en **Actualizar fragmento**.

![Agent Orchestrator](./images/chatgpt15.png)

Entonces debería ver esto. La variación del fragmento se ha creado correctamente.

![Agent Orchestrator](./images/chatgpt16.png)

Ahora también puede ver la nueva variación en la interfaz de usuario de AEM.

![Agent Orchestrator](./images/chatgpt17.png)

## Pasos siguientes

Volver a [AEM y agentes](./aemagents.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}