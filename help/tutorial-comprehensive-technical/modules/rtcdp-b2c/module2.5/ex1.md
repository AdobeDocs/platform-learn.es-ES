---
title: 'Recopilación de datos de Adobe Experience Platform y reenvío de eventos en tiempo real: creación de una propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform'
description: Crear una propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 9c64e57d-c91c-4d4c-923f-91a02edeb2ac
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 1%

---

# 2.5.1 Crear una propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform

## ¿Qué es una propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform?

Normalmente, cuando los datos se recopilan mediante la recopilación de datos de Adobe Experience Platform, se recopilan en el **lado del cliente**. **el lado del cliente** es un entorno como un sitio web o una aplicación móvil. En Introducción y Recopilación de datos, se ha analizado en profundidad la configuración de una propiedad de cliente de recopilación de datos de Adobe Experience Platform y se ha implementado esa propiedad de cliente de recopilación de datos de Adobe Experience Platform en el sitio web y la aplicación móvil, de modo que los datos se puedan recopilar allí cuando un cliente interactúe con el sitio web y la aplicación móvil.

Cuando la propiedad Adobe Experience Platform Data Collection Client recopila esos datos de interacción, el sitio web o la aplicación móvil envían una solicitud al Edge de Adobe. Edge es el entorno de recopilación de datos de Adobe y el punto de entrada para los datos del flujo de navegación en el ecosistema de Adobe. Desde Edge, los datos recopilados se envían a aplicaciones como Adobe Experience Platform, Adobe Analytics, Adobe Audience Manager o Adobe Target.

Con la adición de una propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform, ahora es posible configurar una propiedad de recopilación de datos de Adobe Experience Platform que escuche datos entrantes en Edge. Cuando la propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform que se ejecuta en Edge ve datos entrantes, tiene la capacidad de utilizarlos y reenviarlos a otro lugar. Ese otro lugar ahora también puede ser un webhook externo que no sea de Adobe, lo que permite enviar esos datos a, por ejemplo, su repositorio de datos preferido, una aplicación de toma de decisiones o cualquier otra aplicación que tenga la capacidad de abrir un webhook.

La configuración de una propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform le resulta familiar a una propiedad del lado del cliente, con la capacidad de configurar elementos de datos y reglas como en el pasado con las propiedades del cliente de recopilación de datos de Adobe Experience Platform. Sin embargo, la forma en que se accederá y se utilizarán los datos será ligeramente diferente, según el caso de uso.

Empecemos por crear la propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform.

## Crear una propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform

Vaya a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). En el menú de la izquierda, haga clic en **Reenvío de eventos**. A continuación, verá una descripción general de todas las propiedades disponibles del reenvío de eventos de recopilación de datos de Adobe Experience Platform. Haga clic en el botón **Crear propiedad**.

![Recopilación de datos Adobe Experience Platform SSF](./images/launchhome.png)

Alternativamente, si ya se han creado otras propiedades del reenvío de eventos, la interfaz de usuario tendrá un aspecto un poco diferente. En ese caso, haga clic en **Nueva propiedad**.

![Recopilación de datos Adobe Experience Platform SSF](./images/launchhomea.png)

Ahora debe escribir un nombre para la propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform. Como convención de nombres, use `--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Por ejemplo, en este ejemplo, el nombre es **vangeluw - Demo System (22/02/2022) (Edge)**. Haga clic en **Guardar**.

![Recopilación de datos Adobe Experience Platform SSF](./images/ssf1.png)

A continuación, volverá a la lista de propiedades de reenvío de eventos de recopilación de datos de Adobe Experience Platform. Haga clic en para abrir la propiedad que acaba de crear.

![Recopilación de datos Adobe Experience Platform SSF](./images/ssf2.png)

## Configuración de la extensión de conector de Adobe Cloud

En el menú de la izquierda, ve a **Extensiones**. Verá que la extensión **Core** ya está configurada.

![Recopilación de datos Adobe Experience Platform SSF](./images/ssf3.png)

Ir a **Catálogo**. Verá la extensión **Conector de nube de Adobe**, junto con muchas otras. Haga clic en **Instalar** para instalarlo.

![Recopilación de datos Adobe Experience Platform SSF](./images/ssf4.png)

A continuación, se añade la extensión. No hay ninguna configuración que hacer en este paso. Se le enviará de vuelta a la descripción general de las extensiones instaladas.

![Recopilación de datos Adobe Experience Platform SSF](./images/ssf5.png)

## 2.5.1.3 Implementar la propiedad de reenvío de eventos de recopilación de datos de Adobe Experience Platform

En el menú de la izquierda, vaya a **Flujo de publicación**. Haga clic en **Agregar biblioteca**.

![Recopilación de datos Adobe Experience Platform SSF](./images/ssf6.png)

Escriba el nombre **Main**, seleccione el entorno **Desarrollo (Development)** y haga clic en **+ Agregar todos los recursos modificados**.

![Recopilación de datos Adobe Experience Platform SSF](./images/ssf7.png)

Entonces verá esto... Haga clic en **Guardar y crear para desarrollo**.

![Recopilación de datos Adobe Experience Platform SSF](./images/ssf8.png)

A continuación, se creará la biblioteca, lo que puede tardar entre 1 y 2 minutos.

![Recopilación de datos Adobe Experience Platform SSF](./images/ssf10.png)

Paso siguiente: [2.5.2 Actualice su secuencia de datos para que los datos estén disponibles para la propiedad de reenvío de eventos de recopilación de datos](./ex2.md)

[Volver al módulo 2.5](./aep-data-collection-ssf.md)

[Volver a todos los módulos](./../../../overview.md)
