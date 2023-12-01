---
title: Considere mover etiquetas de proveedor al reenvío de eventos
description: Obtenga información sobre cómo evaluar una etiqueta de proveedor del lado del cliente para la distribución de datos del lado del servidor.
feature: Event Forwarding, Tags, Integrations
role: Admin, Developer, Architect, Data Engineer
level: Intermediate, Experienced
jira: KT-9921
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: 7edf8fc46943ae2f1e6e2e20f4d589d7959310c8
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 3%

---

# Considere la posibilidad de abandonar el etiquetado de proveedores del lado del cliente y empezar a usar el reenvío de eventos

Existen varias razones de peso para considerar la posibilidad de mover etiquetas de proveedor del lado del cliente a un servidor o a un navegador. En este artículo, analizamos cómo evaluar una etiqueta de proveedor del lado del cliente para transferirla potencialmente a una propiedad de reenvío de eventos.

Esta evaluación solo es necesaria si está considerando la posibilidad de eliminar una etiqueta de proveedor del lado del cliente y reemplazarla por una distribución de datos del lado del servidor en una propiedad de reenvío de eventos. Este artículo da por hecho que está familiarizado con los conceptos básicos de [recopilación de datos](https://experienceleague.adobe.com/docs/data-collection.html), y [reenvío de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html).

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) para obtener una referencia consolidada de los cambios terminológicos.

Los proveedores de exploradores están cambiando el modo en que tratan las cookies de terceros. Los proveedores y tecnologías de publicidad y marketing suelen requerir el uso de muchas etiquetas del lado del cliente. Estos desafíos son solo dos razones de peso por las que nuestros clientes añaden la distribución de datos del lado del servidor.

>[!NOTE]
>
>`Tag` En este artículo, se refiere al código del lado del cliente, normalmente JavaScript de un proveedor que se utiliza para la recopilación de datos en el explorador o dispositivo mientras un visitante interactúa con el sitio o la aplicación. `Website` o `site` aquí se refiere a un sitio web, una aplicación web o una aplicación para un dispositivo móvil. Una &quot;etiqueta&quot; para estos fines también se denomina píxel.

## Casos de uso y datos {#use-cases-data}

El primer paso es definir los casos de uso implementados con la etiqueta de proveedor del lado del cliente. Por ejemplo, piense en el píxel Facebook (Meta). Trasladarlo de nuestro sitio a la [API de metaconversiones](https://exchange.adobe.com/apps/ec/109168/meta-conversions-api) con la extensión de reenvío de eventos significa documentar primero los casos de uso específicos.

Para el código de proveedor actual del lado del cliente:

- ¿Qué evento específico y qué otros puntos de datos se exponen y pasan a la etiqueta del lado del cliente?
- ¿Cuándo y dónde se produce esa transferencia de datos?

Es útil crear una lista, hoja de cálculo, diagrama u otro registro de los datos y la secuencia de eventos para documentar esta evaluación, incluso si es solo para su propio uso. Asegúrese de incluir etiquetas para las fuentes de datos, ¿de dónde provienen? Destinos... ¿a dónde va? Y transformaciones, ¿qué pasa entre origen y destino?

En nuestro ejemplo, estamos realizando un seguimiento de las conversiones con el píxel de Facebook cuando los visitantes interactúan con nuestro sitio después de ver un anuncio de Facebook. También podrían interactuar con nuestro sitio después de ver anuncios relacionados en otra plataforma social. Para ver estas conversiones en las herramientas de publicidad de Facebook y en los informes, los datos necesarios deben llegar a Facebook. Estos datos pueden incluir eventos de conversión como descargas, registros, &quot;me gusta&quot; o compras.

### Datos {#data}

Con la etiqueta del lado del cliente existente, cuando se ejecuta o ejecuta en nuestro sitio, ¿qué sucede con los datos de nuestro caso de uso? ¿Podemos capturar los datos que necesitamos en el cliente, sin la etiqueta del proveedor, para que podamos enviarlos al reenvío de eventos? Al utilizar [etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es) Para otros sistemas de administración de etiquetas, la mayoría de los datos de interacción del visitante están disponibles para su recopilación y distribución. Pero, ¿están disponibles los datos que necesitamos para nuestro caso de uso cuando los necesitamos, donde los necesitamos y en el formato que los necesitamos, sin la etiqueta de proveedor del lado del cliente? Estas son algunas preguntas de datos adicionales que deben tenerse en cuenta:

- ¿Se requiere un ID de usuario de proveedor con cada evento?
- Si es así, ¿cómo se puede recopilar o generar sin la etiqueta del lado del cliente?
- ¿Requiere el proveedor específicamente su código del lado del cliente durante la ejecución?
- ¿Qué otros datos se requieren? ¿De dónde procederán esos datos?

La mayoría de las etiquetas de proveedor del lado del cliente no requieren muchos puntos de datos para cualquier caso de uso en particular, pero es útil tener en cuenta los casos de uso y los datos necesarios durante estas evaluaciones.

## API de proveedor {#vendor-apis}

Ahora conocemos los casos de uso específicos que se deben implementar, los datos necesarios y la secuencia de eventos de origen a destino. Para determinar si el caso de uso es adecuado para el reenvío de eventos, ahora podemos investigar los detalles de la API del proveedor.

>[!IMPORTANT]
>
>Aunque muchos proveedores habilitan las API para la transferencia de servidor a servidor, también hay muchos que actualmente no las tienen adecuadas para estos fines.

### Investigación de API {#investigate-apis}

Estos son algunos pasos que podemos seguir para investigar los extremos de la API del proveedor.

¿El proveedor tiene API diseñadas para la transferencia de datos de evento de servidor a servidor? En primer lugar, busque los requisitos para esos extremos de API específicos:

- ¿Existen puntos finales de API para enviar los datos necesarios? Para encontrar los puntos de conexión compatibles con sus casos de uso, consulte la documentación de API o del desarrollador del proveedor.
- ¿Permiten la transmisión de datos de eventos o solo datos por lotes?
- ¿Con qué métodos de autenticación son compatibles? ¿Token, HTTP, versión de credenciales del cliente de OAuth u otro? Consulte [aquí](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) para métodos admitidos por el reenvío de eventos.
- ¿Cuál es el desplazamiento de actualización de su API? ¿Es compatible esa limitación con los mínimos del reenvío de eventos? Detalles [aquí](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- ¿Qué datos requieren para los extremos relevantes?
- ¿Requieren un identificador de usuario específico del proveedor con cada llamada al punto de conexión?
- Si requieren ese identificador, ¿dónde y cómo se puede generar o capturar sin código del lado del cliente?

En otras palabras:

- ¿El proveedor proporciona los puntos finales de API necesarios para nuestros casos de uso?
- ¿Tienen un método de autenticación compatible para el reenvío de eventos?
- ¿Podemos acceder a todos los datos necesarios para una implementación de reenvío de eventos (desde el lado del cliente o desde otras llamadas de API)?

Es probable que la etiqueta sea un buen candidato para pasar del cliente a nuestros servidores en una propiedad de reenvío de eventos si podemos responder afirmativamente a esas preguntas.

Si el proveedor no tiene los puntos finales de API para admitir nuestros casos de uso, obviamente esa etiqueta de proveedor no es un buen candidato para utilizar el reenvío de eventos en lugar de la etiqueta de proveedor del lado del cliente.

¿Qué sucede si tienen API, pero también requieren un ID único de visitante o usuario con cada llamada de API? ¿Cómo podemos acceder a ese ID si no tenemos el código del lado del cliente del proveedor (etiqueta) en ejecución en el sitio?

Algunos proveedores están cambiando sus sistemas para el nuevo mundo sin cookies de terceros. Estos cambios incluyen el uso de identificadores únicos alternativos, como un [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) u otros [ID generado por el cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html). Si el proveedor permite un ID generado por el cliente, podemos enviarlo desde el cliente a Platform Edge Network con SDK web o móvil, o posiblemente obtenerlo desde una llamada de API en el reenvío de eventos. Cuando enviamos datos a ese proveedor en una regla de reenvío de eventos, simplemente incluimos ese identificador según sea necesario.

Si el proveedor requiere datos (como un ID único específico del proveedor, por ejemplo) que solo se puedan generar o a los que se pueda acceder mediante su propia etiqueta del lado del cliente, es probable que esa etiqueta del proveedor no sea una buena candidata para moverse. _Se desaconseja intentar la ingeniería inversa de una etiqueta del lado del cliente con la idea de mover esa recopilación de datos al reenvío de eventos sin las API adecuadas._

El [Conector de Adobe Experience Platform Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) La extensión de puede realizar solicitudes HTTP según sea necesario con proveedores que tengan las API adecuadas para la transferencia de datos de evento de servidor a servidor. Aunque es bueno tener extensiones específicas de proveedor y hay más extensiones en desarrollo activo en este momento, podemos implementar reglas de reenvío de eventos hoy mediante la extensión de conector de nube, sin esperar extensiones de proveedor adicionales.

## Herramientas {#tools}

Investigar y probar los extremos de la API del proveedor es más fácil con herramientas como [Postman](https://www.postman.com/)o extensiones del editor de texto como Visual Studio Code [Cliente Thunder](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client), o [Cliente HTTP](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## Pasos siguientes {#next-steps}

Este artículo proporciona una secuencia de pasos para evaluar una etiqueta del lado del cliente de un proveedor y moverla potencialmente del lado del servidor en una propiedad de reenvío de eventos. Para obtener más información sobre temas relacionados, consulte estos vínculos:

- [Administración de etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es) en Adobe Experience Platform
- [Reenvío de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) para el procesamiento en el servidor
- [Actualizaciones terminológicas](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) en la recopilación de datos
