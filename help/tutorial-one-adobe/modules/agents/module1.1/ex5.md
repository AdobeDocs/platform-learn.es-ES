---
title: Adobe Marketing Agent para Claude
description: Adobe Marketing Agent para Claude
kt: 5342
doc-type: tutorial
exl-id: 2563ca77-699b-4cd3-af51-1105cea03c79
source-git-commit: 2339a3a9c122a3e757c59eec3a9be54acf8d9c1e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# 1.1.5 Adobe Marketing Agent para Claude

[!BADGE Beta]

+++Beta Details
By using the Adobe Marketing Agent with Claude Beta, You hereby acknowledge that the Beta is provided “as is” without warranty of any kind. Adobe shall have no obligation to maintain, correct, update, change, modify or otherwise support the Beta. You are advised to use caution and not to rely in any way on the correct functioning or performance of such Beta and/or accompanying materials. The Beta is considered Confidential Information of Adobe.  Any “Feedback” (information regarding the Beta including but not limited to problems or defects you encounter while using the Beta, suggestions, improvements, and recommendations) provided by You to Adobe is hereby assigned to Adobe including all rights, title, and interest in and to such Feedback.

+++

## Requisitos previos

Para seguir los pasos de este laboratorio como se documenta a continuación, se requiere el siguiente acceso:

- Acceso a Real-Time CDP, Journey Optimizer y Customer Journey Analytics
- Acceso al asistente de IA en Adobe Experience Cloud
- Acceso a AEP Agent Orchestrator
- Access to Claude

## Vídeo

En este vídeo, obtendrá una explicación y una demostración de todos los pasos involucrados en este ejercicio.

>[!VIDEO](https://video.tv.adobe.com/v/3482212?quality=12&learn=on)

Este laboratorio está en desarrollo.

## 1.1.5.1 Crear aplicación personalizada en Claude.ai para CJA

>[!NOTE]
>
>El uso de Adobe Marketing Agent en Claude.ai requiere lo siguiente:
>- una versión de pago de Claude.ai

Go to [https://claude.ai/](https://claude.ai/){target="_blank"} and log in using your account details. Once you&#39;re logged in, you should see this.

![Claude.ai](./images/claude1.png)

Haga clic para abrir la cuenta y, a continuación, seleccione **Configuración**.

![Claude.ai](./images/claude2.png)

Vaya a **Conectores** y haga clic en **Ir a Personalizar**.

![Claude.ai](./images/claude2a.png)

Click **+** and then select **Add custom connector**.

![Claude.ai](./images/claude3.png)

Fill out the fields like this:

- **Name**: `Adobe Marketing Agent`
- **MCP Server URL**: ask your Adobe representative

Haga clic en **Agregar**.

![Claude.ai](./images/claude4.png)

You should then see this. Click **+** to start a new chat.

![Claude.ai](./images/claude5.png)

Click the **+** icon, go to **Connectors** and make sure **Adobe Marketing Agent** is enabled.

![Claude.ai](./images/claude6.png)

## 1.1.5.2 autenticar y establecer contexto

Antes de seguir interactuando con Adobe Marketing Agent a través de Claude.ai, debe iniciar sesión y establecer el contexto.

Escriba la siguiente solicitud y haga clic en **enviar**.

```
login to Adobe Marketing Agent
```

![Claude.ai](./images/claude7.png)

Select **Always allow**.

![Claude.ai](./images/claude8.png)

Haga clic en el vínculo para iniciar sesión en el agente de marketing de Adobe**.

![Claude.ai](./images/claude8a.png)

Haga clic en **Abrir vínculo**.

![Claude.ai](./images/claude8b.png)

Haga clic en **Permitir acceso**.

![Claude.ai](./images/claude8c.png)

Después de autenticarse correctamente, debería ver esto. Go back to Claude.

![Claude.ai](./images/claude8d.png)

Enter the following command and click **send**.

```javascript
logged in
```

![Claude.ai](./images/claude8e.png)

Ha iniciado sesión correctamente. El siguiente paso es establecer el contexto. Escriba la siguiente solicitud y haga clic en **enviar**.


```javascript
change context
```

![Claude.ai y CJA](./images/claude9.png)

Seleccione **Organización**. También puede repetir este comando para cambiar la zona protegida y la vista de datos más adelante.

![Claude.ai &amp; CJA](./images/claude10.png)

Enter the name of your instance and click **send**.

![Claude.ai y CJA](./images/claude11.png)

Seleccionar **Permitir siempre**.

![Claude.ai y CJA](./images/claude12.png)

You should then see something like this.

![Claude.ai &amp; CJA](./images/claude13.png)

If the sandbox isn&#39;t set properly yet, you can use the following command to change to the sandbox you need to use. Click **send**. Alternatively, you can use the above command `change context` and then select **sandbox**

```javascript
change sandbox to --aepSandboxName--
```

![Claude.ai &amp; CJA](./images/claude14.png)

If the dataview isn&#39;t set properly yet, you can use the following command to change to the sandbox you need to use (replace XXX in the below command by the name of your dataview). Haga clic en **enviar**. También puede usar el comando `change context` anterior y seleccionar **vista de datos**

```javascript
change dataview to XXX
```

![Claude.ai y CJA](./images/claude15.png)

Una vez que **Organization**, **Sandbox** y **Dataview** estén correctamente configurados, podrás empezar a hacer preguntas a Adobe Marketing Agent.

## Pasos siguientes

Go back to [Agent Orchestrator](./agentorchestrator.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
