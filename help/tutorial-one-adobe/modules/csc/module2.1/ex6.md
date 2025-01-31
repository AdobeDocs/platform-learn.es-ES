---
title: AEM - Bloque personalizado avanzado
description: AEM - Bloque personalizado avanzado
kt: 5342
doc-type: tutorial
source-git-commit: 2f53c8da2cbe833120fa6555c65b8b753bfa4f8d
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 2%

---

# AEM 2.1.6 Complemento de MarTech para Edge Delivery Services de

AEM AEM El complemento MarTech le ayuda a configurar rápidamente una pila MarTech completa para su proyecto de.

>[!NOTE]
>
>AEM Actualmente, este complemento está disponible para los clientes en colaboración con Ingeniería a través de proyectos de innovación conjunta. Puede encontrar más información en [https://github.com/adobe-rnd/aem-martech](https://github.com/adobe-rnd/aem-martech).

Vaya a la carpeta que esté usando para su repositorio de **citisignal** GitHub. Haga clic con el botón derecho en el nombre de la carpeta y seleccione **Nuevo terminal en la carpeta**.

![AEMCS](./images/mtplugin1.png)

Entonces verá esto... Pegue el siguiente comando y pulse **enter**.

```
git subtree add --squash --prefix plugins/martech https://github.com/adobe/aem-experimentation.git main
```

Entonces debería ver esto.

![AEMCS](./images/mtplugin3.png)

Vaya a la carpeta que esté usando para el repositorio de **citisignal** GitHub y abra la carpeta **plugins**. Ahora debería ver una carpeta llamada **martech**.

![AEMCS](./images/mtplugin4.png)


En Visual Studio Code, abra el archivo **head.html**. Copie el siguiente código y péguelo en el archivo **head.html**.

```javascript
<link rel="preload" as="script" crossorigin="anonymous" href="/plugins/martech/src/index.js"/>
<link rel="preload" as="script" crossorigin="anonymous" href="/plugins/martech/src/alloy.min.js"/>
<link rel="preconnect" href="https://edge.adobedc.net"/>
<!-- change to adobedc.demdex.net if you enable third party cookies -->
```

Guarde los cambios.

![AEMCS](./images/mtplugin5.png)

En Visual Studio Code, vaya a la carpeta **scripts** y abra el archivo **scripts.js**. Copie el siguiente código y péguelo en el archivo **scripts.js**, en los scripts de importación existentes.

```javascript
import {
  initMartech,
  updateUserConsent,
  martechEager,
  martechLazy,
  martechDelayed,
} from '../plugins/martech/src/index.js';
```

Guarde los cambios.

![AEMCS](./images/mtplugin6.png)

```javascript
const isConsentGiven = true;
  const martechLoadedPromise = initMartech(
    // The WebSDK config
    // Documentation: https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/overview#configure-js
    {
      datastreamId: "045c5ee9-468f-47d5-ae9b-a29788f5948f",
      orgId: "907075E95BF479EC0A495C73@AdobeOrg",
      onBeforeEventSend: (payload) => {
        // set custom Target params 
        // see doc at https://experienceleague.adobe.com/en/docs/platform-learn/migrate-target-to-websdk/send-parameters#parameter-mapping-summary
        payload.data.__adobe.target ||= {};

        // set custom Analytics params
        // see doc at https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping
        payload.data.__adobe.analytics ||= {};
      },

      // set custom datastream overrides
      // see doc at:
      // - https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/datastream-overrides
      // - https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overrides
      edgeConfigOverrides: {
        // Override the datastream id
        // datastreamId: '...'

        // Override AEP event datasets
        // com_adobe_experience_platform: {
        //   datasets: {
        //     event: {
        //       datasetId: '...'
        //     }
        //   }
        // },

        // Override the Analytics report suites
        // com_adobe_analytics: {
        //   reportSuites: ['...']
        // },

        // Override the Target property token
        // com_adobe_target: {
        //   propertyToken: '...'
        // }
      },
    },
    // The library config
    {
      launchUrls: ["https://assets.adobedtm.com/b754ed1bed61/b9f7c7c484de/launch-28b548849fb9.min.js"],
      personalization: !!getMetadata('target') && isConsentGiven,
    },
  );
```

![AEMCS](./images/mtplugin8.png)

![AEMCS](./images/mtplugin7.png)

```javascript
if (main) {
    decorateMain(main);
    await Promise.all([
      martechLoadedPromise.then(martechEager),
      waitForLCP(LCP_BLOCKS),
    ]);
  }
```

![AEMCS](./images/mtplugin10.png)

```javascript
await martechLazy();
```

![AEMCS](./images/mtplugin9.png)

```javascript
window.setTimeout(() => {
    martechDelayed();
    return import('./delayed.js');
  }, 3000);
```

![AEMCS](./images/mtplugin11.png)


![AEMCS](./images/mtplugin12.png)


![AEMCS](./images/mtplugin13.png)

Ahora podrá ver los cambios en su sitio web yendo a `main--citisignal--XXX.aem.page/us/en` y/o `main--citisignal--XXX.aem.live/us/en`, después de reemplazar XXX por su cuenta de usuario de GitHub, que en este ejemplo es `woutervangeluwe`.

En este ejemplo, la dirección URL completa se convierte en lo siguiente:
`https://main--citisignal--woutervangeluwe.aem.page/us/en` o `https://main--citisignal--woutervangeluwe.aem.live/us/en`.

Siguiente paso: [Resumen y beneficios](./summary.md){target="_blank"}

[Volver al módulo 2.1](./aemcs.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
