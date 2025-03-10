---
title: Consulte su perfil de cliente en tiempo real en acción en el centro de llamadas
description: Consulte su perfil de cliente en tiempo real en acción en el centro de llamadas
kt: 5342
doc-type: tutorial
exl-id: d3bd34a1-5577-4da7-a5a5-0f186b1a73c2
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 3%

---

# 2.1.5 Ver el perfil del cliente en tiempo real en acción en el centro de llamadas

En este ejercicio, el objetivo es hacer que revise el recorrido del cliente y actúe como un cliente real.

En este sitio web, hemos implementado Adobe Experience Platform. Cada acción se considera un evento de experiencia y se envía a Adobe Experience Platform en tiempo real, lo que hidrata el Perfil del cliente en tiempo real.

En un ejercicio anterior, comenzó como un cliente anónimo que exploraba el sitio y, después de un par de pasos, se convirtió en un cliente conocido.

Cuando ese mismo cliente finalmente atiende su teléfono y llama a su centro de llamadas, es crucial que la información de otros canales esté disponible de inmediato, para que la experiencia del centro de llamadas pueda ser relevante y personalizada.

## Utilice su aplicación CX

Vaya a [https://dsn.adobe.com](https://dsn.adobe.com). Después de iniciar sesión con su Adobe ID, verá esto. Haga clic en los 3 puntos **...** de su proyecto de aplicación CX y, a continuación, haga clic en **Editar** para abrirlo.

![Demostración](./images/cxapp3.png)

En su proyecto de aplicación CX, vaya a **Integraciones**. Haga clic en **Seleccionar entorno**.

![Demostración](./images/cxapp3a.png)

Seleccione la propiedad Recopilación de datos de Adobe Experience Platform que se creó en Introducción. Debe seleccionar la propiedad que tiene **(cx-app)** en su nombre.

![Demostración](./images/cxapp4.png)

Entonces verá esto... Haga clic en **Ejecutar**.

![Demostración](./images/cxapp4a.png)

A continuación, debe seleccionar una de las identidades y el área de nombres correspondiente y hacer clic en el **icono de búsqueda**.

![Perfil del cliente](./images/identities.png)

| Identidad | Área de nombres |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 79943948563923140522865572770524243489 |
| Experience Cloud ID (ECID) | 70559351147248820114888181867542007989 |
| ID de correo electrónico | woutervangeluwe+18112024-01@gmail.com |
| Identificador de número de móvil | +32473622044+18112024-01 |

![Demostración](./images/19.png)

Ahora verá la información que, idealmente, se mostraría en el centro de llamadas, de modo que los agentes del centro de llamadas tengan toda la información relevante disponible inmediatamente cuando hablen con un cliente.

![Demostración](./images/20.png)

## Pasos siguientes

Ir a [Resumen y beneficios](./summary.md){target="_blank"}

Volver a [Perfil del cliente en tiempo real](./real-time-customer-profile.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
