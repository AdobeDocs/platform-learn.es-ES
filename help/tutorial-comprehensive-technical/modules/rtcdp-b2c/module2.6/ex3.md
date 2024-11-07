---
title: Configuración del extremo de la API HTTP en Adobe Experience Platform
description: Configuración del extremo de la API HTTP en Adobe Experience Platform
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 8%

---

# 2.6.3 Configuración del punto final de flujo de API HTTP en Adobe Experience Platform

Para poder configurar el conector del receptor de Adobe Experience Platform en Kafka, debe crear un conector de Source de API HTTP en Adobe Experience Platform. Se requiere la dirección URL del punto final de flujo de la API HTTP para configurar el conector del receptor de Adobe Experience Platform.

Para crear un conector Source de la API HTTP, inicie sesión en Adobe Experience Platform en esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Para ello, haga clic en el texto **[!UICONTROL Producción]** en la línea azul de la parte superior de la pantalla. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./../../../modules/datacollection/module1.2/images/sb1.png)

En el menú de la izquierda, ve a **Sources** y desplázate hacia abajo en el **Catálogo de orígenes** hasta que veas **HTTP API**. Haga clic en **Agregar datos**.

![Ingesta de datos](./images/kaep1.png)

Haga clic en **Nueva cuenta**. Use `--aepUserLdap-- - Kafka` como nombre para su conexión de API HTTP, en este caso **vangeluw - Kafka**. Habilite la casilla de verificación para **Compatible con XDM**. Haga clic en **Conectar con el origen**.

![Ingesta de datos](./images/kaep2.png)

Verá esto, haga clic en **Siguiente**.

![Ingesta de datos](./images/kaep3.png)

Seleccione **Conjunto de datos existente** y abra el menú desplegable. Busque y seleccione el conjunto de datos **Sistema de demostración - Conjunto de datos de evento para el centro de llamadas (Global v1.1)**.

![Ingesta de datos](./images/kaep4.png)

Haga clic en **Next**.

![Ingesta de datos](./images/kaep6.png)

Haga clic en **Next**.

![Ingesta de datos](./images/kaep7.png)

Haga clic en **Finalizar**.

![Ingesta de datos](./images/kaep8.png)

A continuación, verá una descripción general del conector Source de la API HTTP que acaba de crear.

![Ingesta de datos](./images/kaep9.png)

Deberá copiar la dirección URL de **extremo de transmisión**, que se parece a la que se muestra a continuación, ya que la necesitará en el siguiente ejercicio.

`https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`

Ha terminado este ejercicio.

Siguiente paso: [2.6.4 Instalar y configurar Kafka Connect y el conector del receptor de Adobe Experience Platform](./ex4.md)

[Volver al módulo 2.6](./aep-apache-kafka.md)

[Volver a todos los módulos](../../../overview.md)
