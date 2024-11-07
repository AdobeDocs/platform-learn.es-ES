---
title: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: introducción a la recopilación de datos de Adobe Experience Platform'
description: 'Foundation: configuración de la recopilación de datos de Adobe Experience Platform y la extensión del SDK web: introducción a la recopilación de datos de Adobe Experience Platform'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 9%

---

# 1.1.3: Introducción a la recopilación de datos de Adobe Experience Platform

## Contexto

Ahora vamos a echar un vistazo más profundo a los componentes básicos de la recopilación de datos de Adobe Experience Platform para comprender qué se instala en su sitio web de demostración. Observará de cerca la extensión SDK para web de Adobe Experience Platform, configurará un elemento de datos y una regla y aprenderá a publicar una biblioteca.

## 1.1.3.1: extensión del SDK web de Adobe Experience Platform

Una extensión es un conjunto de código empaquetado que amplía la interfaz de recopilación de datos de Adobe Experience Platform y la funcionalidad de la biblioteca. La recopilación de datos de Adobe Experience Platform es la plataforma y las extensiones son como aplicaciones que se ejecutan en la plataforma. Todas las extensiones utilizadas en el tutorial se crean y administran mediante Adobe, pero los terceros pueden crear sus propias extensiones para limitar la cantidad de código personalizado que los usuarios de recopilación de datos de Adobe Experience Platform deben administrar.

Vaya a [Recopilación de datos de Adobe Experience Platform](https://experience.adobe.com/launch/) y seleccione **Etiquetas**.

Esta es la página de Propiedades de recopilación de datos de Adobe Experience Platform que vio antes.

![Página de propiedades](./images/launch1.png)

En el módulo 0, Demo System creó dos propiedades de cliente para usted: una para el sitio web y otra para la aplicación móvil. Encuéntralos buscando `--aepUserLdap--` en el cuadro **[!UICONTROL Buscar]**.

![Cuadro de búsqueda](./images/property6.png)

Abra la propiedad **Web**.

A continuación, verá la página Información general de la propiedad. Haz clic en **[!UICONTROL Extensiones]** en el carril izquierdo. Haga clic en el botón **[!UICONTROL Configurar]** de la extensión del SDK web de Adobe Experience Platform.

![Página de información general de propiedad](./images/property7.png)

Bienvenido al SDK web de Adobe Experience Platform. Aquí puede configurar la extensión con la secuencia de datos que creó en el [Ejercicio 0.2](./../../../modules/gettingstarted/gettingstarted/ex2.md), así como algunas configuraciones más avanzadas. Solo va a configurar dos opciones para este ejercicio.

El dominio de Edge predeterminado es siempre **edge.adobedc.net**. Si ha implementado una configuración CNAME en su entorno de Adobe Experience Cloud o Adobe Experience Platform, deberá actualizar el **[!UICONTROL dominio de Edge]**. Su instancia de Adobe Experience Platform está usando este dominio de Edge: `--webSdkEdgeDomain--`.

Si el dominio de Edge de su instancia es diferente del predeterminado, actualice el dominio de Edge. Un dominio de Edge permite configurar un servidor de seguimiento de origen, que a continuación utiliza una configuración CNAME en el back-end para garantizar que los datos se recopilen en el Adobe.

![Extensiones de inicio](./images/property9edgedomain.png)

Ahora, asegúrese de que el botón de opción **[!UICONTROL Elegir de la lista]** esté seleccionado en el encabezado **[!UICONTROL Datastreams]** y seleccione su secuencia de datos con el nombre: `--aepUserLdap-- - Demo System Datastream`, en la lista del cuadro **[!UICONTROL Datastream]**.

![Extensiones de inicio](./images/property9edge.png)

Haga clic en **[!UICONTROL Guardar]** para volver a la vista Extensiones.

![Página principal del SDK web de Adobe Experience Platform](./images/save.png)

## 1.1.3.2 Elementos de datos

Los Data Elements son los componentes básicos del diccionario de datos (o mapa de datos). Utilice Data Elements para recopilar, organizar y entregar datos a través de la tecnología de marketing y publicidad.

Un solo elemento de datos es una variable cuyo valor puede asignarse a cadenas de consulta, URL, valores de cookies, variables JavaScript, etc. Puede hacer referencia a este valor por su nombre de variable en toda la recopilación de datos de Adobe Experience Platform. Esta colección de Data Elements se convierte en el diccionario de los datos definidos que puede utilizar para crear reglas (eventos, condiciones y acciones). Este diccionario de datos se comparte en toda la recopilación de datos de Adobe Experience Platform para utilizarlo con cualquier extensión agregada a su propiedad.

Ahora va a editar un elemento de datos ya existente en un formato compatible con SDK web.

Haga clic en Elementos de datos en el carril izquierdo para que se le redirija a la página Elementos de datos.

![Página principal de elementos de datos](./images/dataelement1.png)

>[!NOTE]
>
>Solo está editando un elemento de datos en este ejercicio, pero puede ver el botón **[!UICONTROL Agregar elemento de datos]** en esta página, que se usaría para agregar una nueva variable al diccionario de datos. Esto se podría utilizar en toda la recopilación de datos de Adobe Experience Platform. No dude en consultar algunos de los demás elementos de datos ya existentes, la mayoría de los cuales utilizan el almacenamiento local como fuente de datos.

En la barra de búsqueda, escriba **XDM - Vista de producto** y haga clic en el elemento de datos que devuelve.

![Buscar ruleArticlePages](./images/dataelement2.png)

Esta pantalla muestra el objeto XDM que va a editar. El Experience Data Model (XDM) es un concepto que se explorará mucho más a lo largo de este Tutorial técnico, pero por ahora es suficiente para entenderlo como el formato que requiere el SDK web de Adobe Experience Platform. Agregarás un poco más de información a los datos recopilados en las páginas de artículos del sitio web de demostración.

Haga clic en el botón &quot;+&quot; junto a **web**, en la parte inferior del árbol.

Haga clic en el botón &quot;+&quot; junto a **webPageDetails**.

Haz clic en **siteSection**. Ahora ve que **siteSection** aún no está vinculada a ningún elemento de datos. Vamos a cambiar eso.

![Vaya a la sección del sitio](./images/dataelement3.png)

Desplácese hacia arriba e introduzca el texto `%Product Category%`. Haga clic en **[!UICONTROL Guardar]**.

![Guardar](./images/dataelement4.png)

En este punto, la extensión SDK para web de Adobe Experience Platform está instalada y ha actualizado un elemento de datos para recopilar datos con una estructura XDM. A continuación, vamos a comprobar las reglas que enviarán datos en el momento correcto.

## 1.1.3.3 Normas

La recopilación de datos de Adobe Experience Platform es un sistema basado en reglas. Busca la interacción de usuarios y datos asociados. Cuando se cumplen los criterios descritos en las reglas, la regla activa la extensión, script o el código del lado del cliente identificados.

Genere reglas para integrar los datos y las funciones de marketing y tecnología publicitaria que unifique productos dispares en una única solución.

Vamos a desglosar la regla que envía datos en páginas de artículos.

Haz clic en **[!UICONTROL Reglas]** en el carril izquierdo.

**[!UICONTROL Buscar]** por `Product View`.

Haga clic en la regla que devuelve.

![Medios - búsqueda de reglas de páginas de artículo](./images/rule1.png)

Veamos los elementos individuales que componen esta regla. Para todas las reglas Si se produce un **[!UICONTROL Evento]** especificado, se evalúan las **[!UICONTROL Condiciones]** y las **[!UICONTROL Acciones]** especificadas se realizarán si es necesario.

![Medios - Regla de páginas de artículo](./images/rule2.png)

Haga clic en el evento **Custom Event - Product View**. Esta es la vista que se carga.

Haga clic en el menú desplegable **Tipo de evento**.

En esta sección se enumeran algunas de las interacciones estándar que se pueden utilizar para indicar a la recopilación de datos de Adobe Experience Platform que ejecute las acciones en caso de que se cumplan las condiciones.

![Eventos](./images/rule3.png)

Haga clic en **[!UICONTROL Cancelar]** para volver a la regla.

Haga clic en la acción **Enviar evento de &quot;vista de producto&quot; a AEP**.

Aquí puede ver los datos que el SDK web de Adobe Experience Platform envía a Adobe Edge. Más específicamente, se usa la **aleación** **[!UICONTROL instancia]** del SDK web. La configuración de otra **[!UICONTROL instancia]** permitiría el uso de diferentes flujos de datos, entre otras cosas. Ha especificado el evento **[!UICONTROL Type]** como **commerce.productViews** y los datos XDM que está enviando son el elemento de datos **XDM - Product View** que cambió anteriormente.

![Acción Enviar evento](./images/rule5.png)

Ahora que ha consultado la regla, puede publicar todos los cambios en la recopilación de datos de Adobe Experience Platform.

## 1.1.3.4 Publish en una biblioteca

Finalmente, para validar la regla y el elemento de datos que acaba de actualizar, debe publicar una biblioteca que contenga los elementos editados en nuestra propiedad. Hay algunos pasos rápidos que debe seguir en la sección **[!UICONTROL Publicación]** de la recopilación de datos de Adobe Experience Platform.

Haga clic en **[!UICONTROL Flujo de publicación]** en el panel de navegación izquierdo

Haga clic en la biblioteca existente, llamada **Principal**.

![Acceso a la biblioteca](./images/publish1.png)

Haga clic en el botón **Agregar todos los recursos modificados**.

![Acceso a la biblioteca](./images/publish1a.png)

Desplácese hacia abajo para ver que la mayoría de los recursos permanecerán como **Revisión 1 (más reciente)**, pero los dos que hemos cambiado: **Elemento de datos: ruleArticlePages** y **Extensión: Adobe Experience Platform Web SDK** se marcarán con solo **Último**.

Haga clic en el botón **Guardar y generar para desarrollo**.

![Biblioteca de contenido](./images/publish2.png)

La biblioteca puede tardar unos minutos en crearse y, cuando se complete, mostrará un punto verde a la izquierda del nombre de la biblioteca.

Como puede ver en la pantalla Flujo de publicación, hay mucho más en el proceso de publicación de la recopilación de datos de Adobe Experience Platform que está fuera del ámbito de este tutorial. Solo vamos a usar una sola biblioteca en nuestro entorno de desarrollo.

Paso siguiente: [1.1.4 Recopilación de datos web del lado del cliente](./ex4.md)

[Volver al módulo 1.1](./data-ingestion-launch-web-sdk.md)

[Volver a todos los módulos](./../../../overview.md)
