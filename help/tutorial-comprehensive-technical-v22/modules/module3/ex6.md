---
title: Consulte su perfil de cliente en tiempo real en acción en el centro de llamadas
description: Consulte su perfil de cliente en tiempo real en acción en el centro de llamadas
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 457347ca-1ce5-4699-bd30-735abdc7b450
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 3%

---

# 3.6 Consulte su perfil de cliente en tiempo real en acción en el centro de llamadas

En este ejercicio, el objetivo es que usted recorra el recorrido del cliente y actúe como un cliente real.

En este sitio web, hemos implementado Adobe Experience Platform. Cada acción se considera un evento de experiencia y se envía a Adobe Experience Platform en tiempo real, hidratando el Perfil del cliente en tiempo real.

En un ejercicio anterior, comenzó como un cliente anónimo que estaba navegando por el sitio y, después de un par de pasos, se convirtió en un cliente conocido.

Cuando ese mismo cliente finalmente recoge su teléfono y llama a su centro de llamadas, es crucial que la información de otros canales esté disponible inmediatamente, de modo que la experiencia del centro de llamadas pueda ser relevante y personalizada.

## 3.6.1 Use su aplicación CX

Como parte de nuestro sistema de demostración, hemos creado una plantilla de aplicación CX que puede utilizarse para simular un entorno de centro de llamadas. Siga estos pasos para crear un proyecto de aplicación CX de este tipo.

Vaya a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Haga clic en **Nuevo proyecto**.

A continuación, verá su proyecto de aplicación CX. Haga clic en el proyecto para abrirlo.

![Demostración](./images/cxapp3.png)

En su proyecto de aplicación CX, vaya a **Integraciones**. Seleccione la propiedad Recopilación de datos de Adobe Experience Platform que se creó en el módulo 0. Debe seleccionar la propiedad que tiene **(habilitación)** en su nombre. A continuación, haga clic en **Ejecutar**.

![Demostración](./images/cxapp4.png)

Entonces verás esto.

![Demostración](./images/cxapp5.png)

En el panel Visor de perfiles, puede ver estas combinaciones de ID y espacios de nombres:

![Perfil del cliente](./images/identities.png)

| Identidad | Área de nombres |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 12507560687324495704459439363261812234 |
| ID de correo electrónico | woutervangeluwe+06022022-01@gmail.com |
| ID de número de móvil | +32473622044+06022022-01 |

Cuando el cliente llama a su centro de llamadas, el número de teléfono se puede utilizar para identificar al cliente. En este ejercicio, utilizará el número de teléfono para recuperar el perfil del cliente en la aplicación CX.

Select **Número de teléfono** en la lista desplegable e introduzca el número de teléfono que utilizó en el sitio web. Visita **Entrar**.

![Demostración](./images/19.png)

Ahora verá la información que idealmente se mostraría en el Centro de llamadas, de modo que los empleados del Centro de llamadas tengan toda la información relevante disponible inmediatamente al hablar con un cliente.

![Demostración](./images/20.png)

Paso siguiente: [Resumen y beneficios](./summary.md)

[Volver al módulo 3](./real-time-customer-profile.md)

[Volver a todos los módulos](../../overview.md)
