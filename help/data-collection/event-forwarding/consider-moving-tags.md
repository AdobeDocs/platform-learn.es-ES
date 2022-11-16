---
title: Considere la posibilidad de mover las etiquetas de proveedor al reenvío de eventos
description: Obtenga información sobre cómo evaluar una etiqueta de proveedor del lado del cliente para la distribución de datos del lado del servidor.
feature: Event Forwarding, Tags, Integrations
solution: Data Collection
kt: 9921
level: Intermediate, Experienced
role: Admin, Developer, Architect
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 3%

---

# Considere la posibilidad de abandonar el etiquetado de proveedores del lado del cliente y empezar a usar el reenvío de eventos

Existen varias razones convincentes para considerar la posibilidad de mover etiquetas de proveedor del lado del cliente fuera de navegadores y dispositivos, y a un servidor. En este artículo, analizamos cómo evaluar una etiqueta de proveedor del lado del cliente para moverla potencialmente a una propiedad de reenvío de eventos.

Esta evaluación solo es necesaria si está considerando la posibilidad de eliminar una etiqueta de proveedor del lado del cliente y sustituirla por distribución de datos del lado del servidor en una propiedad de reenvío de eventos. Este artículo supone que está familiarizado con los conceptos básicos de [recopilación de datos](https://experienceleague.adobe.com/docs/data-collection.html)y [reenvío de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html).

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) para obtener una referencia consolidada de los cambios terminológicos.

Los proveedores de navegadores están cambiando la forma en que tratan las cookies de terceros. Los proveedores y las tecnologías de publicidad y marketing suelen requerir el uso de muchas etiquetas del lado del cliente. Estos desafíos son solo dos razones convincentes por las que nuestros clientes están agregando distribución de datos del lado del servidor.

>[!NOTE]
>
>`Tag` en este artículo significa código del lado del cliente, normalmente JavaScript de un proveedor que se utiliza para la recopilación de datos en el explorador o dispositivo mientras un visitante interactúa con el sitio o la aplicación. `Website` o `site` aquí se refiere a un sitio web, una aplicación web o una aplicación para un dispositivo móvil. A menudo, una &quot;etiqueta&quot; para estos fines también se denomina píxel.

## Casos de uso y datos {#use-cases-data}

El primer paso es definir los casos de uso implementados con la etiqueta de proveedor del lado del cliente. Por ejemplo, considere el píxel Facebook (Meta). Trasladarlo desde nuestro sitio al [API de conversiones de facebook](https://exchange.adobe.com/apps/ec/105509/facebook-conversions-api-extension) con la extensión de reenvío de eventos significa documentar primero los casos de uso específicos.

Para el código de proveedor actual del lado del cliente:

- ¿Qué evento específico y otros puntos de datos se exponen y pasan a la etiqueta del lado del cliente?
- ¿Cuándo y dónde se produce esa transferencia de datos?

Es útil hacer una lista, hoja de cálculo, diagrama u otro registro de los datos y secuencia de eventos para documentar esta evaluación, incluso si solo es para su propio uso. Asegúrese de incluir etiquetas para las fuentes de datos: ¿de dónde proviene? Destinos, ¿a dónde va? Y transformaciones: ¿qué le pasa entre el origen y el destino?

En nuestro ejemplo, estamos rastreando conversiones con el píxel de Facebook cuando los visitantes interactúan con nuestro sitio después de ver una publicidad para Facebook. También podrían interactuar con nuestro sitio después de ver anuncios relacionados en otra plataforma social. Para ver estas conversiones en las herramientas de publicidad de Facebook y en los informes, los datos necesarios deben llegar a Facebook. Estos datos pueden incluir eventos de conversión como descargas, registros, cantidad de &quot;Me gusta&quot; o compras.

### Datos {#data}

Con la etiqueta de cliente existente, cuando se ejecuta o ejecuta en nuestro sitio, ¿qué sucede con los datos de nuestro caso de uso? ¿Podemos capturar los datos que necesitamos en el cliente, sin la etiqueta de proveedor, para poder enviarlos al reenvío de eventos? Al usar [etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) Para otros sistemas de administración de etiquetas, la mayoría de los datos de interacción de los visitantes están disponibles para su recopilación y distribución. Pero, ¿los datos que necesitamos para nuestro caso de uso están disponibles cuando los necesitamos, donde los necesitamos y en el formato que los necesitamos, sin la etiqueta del proveedor del lado del cliente? Estas son algunas preguntas adicionales que debe tener en cuenta:

- ¿Se requiere un ID de usuario de proveedor con cada evento?
- En caso afirmativo, ¿cómo se puede recopilar o generar sin la etiqueta del lado del cliente?
- ¿El proveedor requiere específicamente su código del lado del cliente durante la ejecución?
- ¿Qué otros datos se necesitan? ¿De dónde procederán esos datos?

La mayoría de las etiquetas de proveedores del lado del cliente no requieren muchos puntos de datos para ningún caso de uso en particular, pero es útil tener en cuenta los casos de uso y los datos requeridos durante estas evaluaciones.

## API de proveedor {#vendor-apis}

Ahora conocemos los casos de uso específicos que se van a implementar, los datos necesarios y la secuencia de eventos de origen a destino. Para determinar si el caso de uso es adecuado para el reenvío de eventos, ahora podemos investigar los detalles de la API del proveedor.

>[!IMPORTANT]
>
>Aunque muchos proveedores habilitan las API para la transferencia de servidor a servidor, también hay muchos que actualmente no tienen las API adecuadas para estos fines.

### Investigación de API {#investigate-apis}

A continuación se indican algunos pasos que podemos seguir para investigar los extremos de las API del proveedor.

¿Tiene el proveedor API diseñadas para la transferencia de datos de evento de servidor a servidor? En primer lugar, busque los requisitos para esos extremos específicos de API:

- ¿Existen puntos finales de API para enviar los datos necesarios? Para encontrar los extremos que admiten sus casos de uso, consulte la documentación para desarrolladores o API del proveedor.
- ¿Permiten la transmisión de datos de evento o solo de datos por lotes?
- ¿Qué métodos de autenticación admiten? Token, HTTP, credenciales de cliente de OAuth, versión u otra? Consulte [here](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) para métodos admitidos por el reenvío de eventos.
- ¿Cuál es el desplazamiento de la actualización de su API? ¿Es compatible esta limitación con los mínimos de reenvío de eventos? Detalles [here](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- ¿Qué datos requieren para los puntos finales relevantes?
- ¿Requieren un identificador de usuario específico del proveedor con cada llamada al extremo?
- Si requieren ese identificador, ¿dónde y cómo se puede generar o capturar sin código del lado del cliente?

En otras palabras:

- ¿El proveedor proporciona los extremos de API requeridos para nuestros casos de uso?
- ¿Tienen un método de autenticación compatible para el reenvío de eventos?
- ¿Podemos acceder a todos los datos necesarios para una implementación de reenvío de eventos (desde el lado del cliente o desde otras llamadas a la API)?

Es probable que la etiqueta sea un buen candidato para pasar del cliente a nuestros servidores en una propiedad de reenvío de eventos si podemos responder afirmativamente a esas preguntas.

Si el proveedor no tiene los extremos de API para admitir nuestros casos de uso, entonces obviamente esa etiqueta de proveedor no es un buen candidato para usar el reenvío de eventos en lugar de la etiqueta de proveedor del lado del cliente.

¿Qué sucede si tienen API, pero también requieren algún ID de visitante o usuario único con cada llamada a la API? ¿Cómo podemos acceder a ese ID si no tenemos el código de cliente (etiqueta) del proveedor en ejecución en el sitio?

Algunos proveedores están cambiando sus sistemas para el nuevo mundo sin cookies de terceros. Estos cambios incluyen el uso de identificadores únicos alternativos, como un [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) u otros [ID generado por el cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html). Si el proveedor permite un ID generado por el cliente, podemos enviarlo desde el cliente a la red perimetral de plataforma con SDK web o móvil, o posiblemente obtenerlo de una llamada de API en el reenvío de eventos. Cuando enviamos datos a ese proveedor en una regla de reenvío de eventos, simplemente incluimos ese identificador según sea necesario.

Si el proveedor requiere datos (como un ID único específico del proveedor, por ejemplo) que solo se puedan generar o acceder a ellos mediante su propia etiqueta del lado del cliente, es probable que esa etiqueta del proveedor no sea un buen candidato para moverse. _Se desaconseja intentar aplicar ingeniería inversa a una etiqueta del lado del cliente con la idea de trasladar esa recopilación de datos al reenvío de eventos sin las API adecuadas._

La variable [Conector de Adobe Experience Platform Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) puede realizar solicitudes HTTP según sea necesario con proveedores que tengan las API adecuadas para la transferencia de datos de evento de servidor a servidor. Aunque las extensiones específicas del proveedor son agradables de tener y hay más extensiones en desarrollo activo ahora mismo, podemos implementar las reglas de reenvío de eventos hoy mediante la extensión de Cloud Connector, sin esperar a que haya extensiones de proveedor adicionales.

## Herramientas {#tools}

La investigación y prueba de los extremos de API del proveedor es más sencilla con herramientas como [Postman](https://www.postman.com/)o extensiones de editor de texto como Visual Studio Code [Cliente trueno](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)o [Cliente HTTP](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## Pasos siguientes {#next-steps}

Este artículo proporcionaba una secuencia de pasos para evaluar una etiqueta del lado del cliente del proveedor y moverla potencialmente del lado del servidor en una propiedad de reenvío de eventos. Para obtener más información sobre temas relacionados, consulte estos vínculos:

- [Administración de etiquetas](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) en Adobe Experience Platform
- [Reenvío de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) para el procesamiento en el lado del servidor
- [Actualizaciones terminológicas](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) en la recopilación de datos
