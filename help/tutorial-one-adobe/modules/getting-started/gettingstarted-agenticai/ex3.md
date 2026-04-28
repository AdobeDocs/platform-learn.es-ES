---
title: 'Primeros pasos: IA agente: utilice su sitio web de AEM y su zona protegida de AEP'
description: 'Primeros pasos: IA agente: utilice su sitio web de AEM y su zona protegida de AEP'
doc-type: multipage-overview
source-git-commit: bdade61b2f64a5138807a47f73d8006ce9c564fc
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# Utilice su sitio web de AEM y su zona protegida de AEP

Al utilizar los laboratorios técnicos de inteligencia artificial aplicada a la actividad del agente, utilizará un programa de AEM as a Cloud Service existente que utilice Edge Delivery Services. Este programa de AEM as a Cloud Service que utiliza Edge Delivery Services se ha creado para usted y ya está disponible al principio de Tech Labs.

## Su número

Cuando obtuvo acceso al entorno de habilitación, se le asignó un número. Este número indica qué programa de AEM as a Cloud Service debe utilizar y también qué zona protegida de AEP debe utilizar para el Tech Lab de Brand Concierge.

>[!IMPORTANT]
>
>Si aún no ha recibido este correo electrónico, no podrá ejecutar los pasos siguientes. Debe esperar hasta que reciba el siguiente correo electrónico antes de acceder a las siguientes aplicaciones de Adobe.


![DSN](./images/number.png)

## Su programa de AEM

>[!NOTE]
>
>Todas las capturas de pantalla a continuación utilizan el número 1 solo con fines ilustrativos. Debe utilizar el número que se le asignó como parte del correo electrónico que recibió al seguir los pasos a continuación.

El programa de AEM utiliza el número que se le asignó en su nombre. El nombre del programa de AEM debe ser:

- **Perspectivas técnicas - AEM + ACCS X**, donde X significa el número que se le asignó.

![DSN](./images/aem1.png)

Puede acceder a su programa de AEM y encontrarlo en [https://experience.adobe.com/cloud-manager/landing.html](https://experience.adobe.com/cloud-manager/landing.html). Asegúrese de que el entorno seleccionado sea **`--aepImsOrgName--`**. Puede verificarlo en la esquina superior derecha de la pantalla.

![DSN](./images/aem2.png)

### Deshibernación del programa de AEM

El programa de AEM que se utiliza es un programa de zona protegida. Las zonas protegidas de AEM hibernarán automáticamente después de no utilizarse durante un par de horas, lo que significa que deberá anular la hibernación de esas zonas protegidas antes de utilizarlas. Para anular la hibernación de un programa, vaya a [https://experience.adobe.com/cloud-manager/landing.html](https://experience.adobe.com/cloud-manager/landing.html). Haga clic en para abrir el programa.

![DSN](./images/aem3.png)

Entonces debería ver esto. Haga clic en los 3 puntos **...** y, a continuación, seleccione **Anular la hibernación**.

![DSN](./images/aem4.png)

Haga clic en **Enviar**. La dehibernación tarda de 10 a 15 minutos.

![DSN](./images/aem5.png)

### Repositorio de GitHub para su programa de AEM

Cada programa de AEM utiliza Edge Delivery Services para implementar el sitio web. Esto significa que el código del sitio web se aloja en un repositorio de GitHub. El repositorio de GitHub se ha creado para usted y se puede acceder a él desde:

**https://github.com/woutervangeluwe/techinsidersX-citisignal-aem-accs**, por lo que debe reemplazar X por su número.

El repositorio de GitHub debe tener este aspecto.

![DSN](./images/aem6.png)

Como parte del proceso de incorporación antes del inicio de sus sesiones de Tech Lab, se le pedirá que proporcione su nombre de usuario de GitHub. Al proporcionar su nombre de usuario de GitHub, se le agregará como colaborador al repositorio de GitHub adjunto a su sitio web para que pueda realizar cambios en él.

### Acceso al sitio web

Para acceder al sitio web, puede utilizar estas direcciones URL predeterminadas:

- **https://main--techinsidersX-citisignal-aem-accs--woutervangeluwe.aem.page/**
- **https://main--techinsidersX-citisignal-aem-accs--woutervangeluwe.aem.live/**

Debe reemplazar la X de estas direcciones URL por el número que se le asignó.

Además, se ha creado un nombre de dominio personalizado para cada sitio web, al que puede acceder mediante esta dirección URL:

- **https://techinsidersX.adobedemosystem.com/**

Debe reemplazar la X de estas direcciones URL por el número que se le asignó.

A continuación, debería poder ver su sitio web, que tiene un aspecto similar al siguiente:

![DSN](./images/aem7.png)

## Su zona protegida de AEP

>[!NOTE]
>
>Todas las capturas de pantalla a continuación utilizan el número 1 solo con fines ilustrativos. Debe utilizar el número que se le asignó como parte del correo electrónico que recibió al seguir los pasos a continuación.

Para el Tech Lab de Brand Concierge, debe utilizar una zona protegida específica de AEP. Esta zona protegida de AEP se llama: **techinsidersX**, por lo que debe reemplazar la X por el número que se le asignó.

Vaya a [https://platform.adobe.com](https://platform.adobe.com). En la esquina superior derecha de la pantalla, abra la lista desplegable para seleccionar la zona protegida.

Solo debe utilizar esta zona protegida para el Brand Concierge Tech Lab.

![DSN](./images/aep1.png)

## Pasos siguientes

Volver a [Introducción - Inteligencia artificial aplicada a la agencia](./getting-started-agentic-ai.md){target="_blank"}

Volver a [Todos los módulos](./../../../overview.md){target="_blank"}./images
