---
title: Configuración del extremo de la API HTTP en Adobe Experience Platform
description: Configuración del extremo de la API HTTP en Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 621a4db7-0aff-42bf-ad42-daec6e924451
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 7%

---

# 2.6.3 Configuración del punto final de flujo de API HTTP en Adobe Experience Platform

Para poder configurar el conector del receptor de Adobe Experience Platform en Kafka, debe crear un conector de Source de API HTTP en Adobe Experience Platform. Se requiere la dirección URL del punto final de flujo de la API HTTP para configurar el conector del receptor de Adobe Experience Platform.

Para crear un conector Source de la API HTTP, inicie sesión en Adobe Experience Platform en esta dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Después de iniciar sesión, llegará a la página principal de Adobe Experience Platform.

![Ingesta de datos](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Antes de continuar, debe seleccionar una **zona protegida**. La zona protegida que se va a seleccionar se denomina ``--aepSandboxName--``. Después de seleccionar la zona protegida adecuada, verá que la pantalla cambia y ahora está en la zona protegida dedicada.

![Ingesta de datos](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

En el menú de la izquierda, ve a **Sources** y desplázate hacia abajo en el **Catálogo de orígenes** hasta que veas **HTTP API**. Haga clic en **Configuración**.

![Ingesta de datos](./images/kaep1.png)

Haga clic en **Nueva cuenta**. Use `--aepUserLdap-- - Kafka` como nombre para su conexión de API HTTP, en este caso **vangeluw - Kafka**. Habilite la casilla de verificación para **Compatible con XDM**. Haga clic en **Conectar con el origen**.

![Ingesta de datos](./images/kaep2.png)

Verá esto, haga clic en **Siguiente**.

![Ingesta de datos](./images/kaep3.png)

Seleccione **Conjunto de datos existente** y abra el menú desplegable. Busque y seleccione el conjunto de datos **Sistema de demostración - Conjunto de datos de evento para el centro de llamadas (Global v1.1)**.

Haga clic en **Next**.

![Ingesta de datos](./images/kaep4.png)

Haga clic en **Finalizar**.

![Ingesta de datos](./images/kaep8.png)

A continuación, verá una descripción general del conector Source de la API HTTP que acaba de crear.

Deberá copiar la dirección URL de **extremo de transmisión**, que se parece a la que se muestra a continuación, ya que la necesitará en el siguiente ejercicio.

`https://dcs.adobedc.net/collection/63751d0f299eeb7aa48a2f22acb284ed64de575f8640986d8e5a935741be9067`

![Ingesta de datos](./images/kaep9.png)

Ha terminado este ejercicio.

## Pasos siguientes

Vaya a [2.6.4 Instalar y configurar Kafka Connect y el conector del receptor de Adobe Experience Platform](./ex4.md){target="_blank"}

Volver a [Transmitir datos de Apache Kafka a Adobe Experience Platform](./aep-apache-kafka.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
