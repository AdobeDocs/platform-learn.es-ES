---
title: Introducción básica a las API
description: Introducción a las interfaces de programación de aplicaciones
activity: understand
doc-type: article
feature-set: Experience Platform
feature: Server API,API,Data Collection,Integrations
level: Beginner
role: User, Data Engineer, Developer
solution: Data Collection
topic: Integrations
exl-id: 9607e641-b0d5-49c1-b319-32ed0720e715
source-git-commit: ac07d62cf4bfb6a9a8b383bbfae093304d008b5f
workflow-type: tm+mt
source-wordcount: '2086'
ht-degree: 0%

---

# API 101: Una introducción básica a las API

API significa Interfaz de programación de aplicaciones. Significa exactamente lo que dice: hay interfaces entre programas y estas interfaces permiten que esos programas se comuniquen. Cuando los programadores desarrollan aplicaciones de software, a menudo necesitan su software para comunicarse con otro software o hardware. La API define el qué, cómo, cuándo, dónde y por qué de esas comunicaciones e interacciones.

Las API son una forma de resolver los desafíos empresariales con software. En la mayoría de las empresas, eso es un esfuerzo colaborativo. La colaboración siempre es más sencilla gracias a una comprensión compartida de los términos, conceptos y pasos clave.

Si piensa en hacer clic en un vínculo de una página web, el explorador utiliza bastantes API al hacer clic en el vínculo. El explorador reconoce el clic, realiza la solicitud de la página que desea visitar, recupera la página a través de Internet y, a continuación, la muestra en la pantalla. Hay muchos pasos más pequeños en el medio, pero su navegador es software que se comunica e interactúa con una variedad de API solo para mostrarle una página web. En este artículo resaltaremos términos, conceptos y pasos que son importantes al usar o discutir las API.

Al final de este artículo debería tener una comprensión clara de estos términos, conceptos y pasos fundamentales. La documentación de la API puede ser extensa y los debates sobre el uso de las API para abordar casos de uso específicos pueden ser muy detallados. Navegar por la documentación y discutir las API es más fácil y productivo, con fundamentos claros y una comprensión compartida.

>[!NOTE]
>
> Aunque hay muchas API, el enfoque aquí estará en las API web y del navegador: básicamente, cuando una aplicación de software interactúa con otra a través de Internet.

## Términos y conceptos de API

¿Qué significa una palabra o frase, y cómo puedo pensar en ello simple y fácilmente? En una API, la parte &quot;aplicación&quot; significa una aplicación de software o programa. La parte &quot;interfaz de programación&quot; hace referencia a cómo y dónde interactúa una aplicación con otra aplicación para determinados fines. En el ejemplo de nuestra página web, al hacer clic en un vínculo, el explorador envía una solicitud a un servidor para la página web.

![Imagen de hipervínculo con dirección URL de destino](../assets/api101-link-destination.png)

En esta captura de pantalla, el cursor del ratón se sitúa sobre el vínculo de Adobe Experience Platform. En la parte inferior se encuentra la barra de estado del navegador web que muestra la &quot;dirección&quot; de la página que recibirá el navegador. En otras palabras, al hacer clic en el vínculo de Adobe Experience Platform, se indica al explorador que &quot;obtenga esa página para que pueda verla aquí en mi pantalla&quot;.

Al hacer clic en un vínculo, el explorador realiza una solicitud a un servidor para obtener una página. Esta es una solicitud `GET`, uno de los métodos de solicitud que se usan comúnmente con las API web. Una cosa que el navegador necesita para cumplir la solicitud es la página &quot;dirección&quot; - ¿dónde está en la web?

### Partes de una dirección URL

![Barra de direcciones del explorador con URL](../assets/api101-address-bar.png)

La mayoría de los navegadores tienen una &quot;barra de direcciones&quot; que muestra parte o toda la &quot;dirección&quot; de una página web. Cuando el navegador &quot;obtiene&quot; la página para el enlace en el que hemos hecho clic, muestra la &quot;dirección&quot; de la página en esta barra de direcciones. Entonces, ¿cuál es la &quot;dirección&quot; de una página web?

Ese(a) `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html` de arriba es la dirección de una página en la web y se llama URL o Localizador uniforme de recursos. Las direcciones URL pueden hacer referencia a una página como esta, a un archivo de imagen, a un vídeo u otros tipos de archivo.

![Partes de una dirección URL](../assets/api101-url-parts.jpg)

Esta dirección, la URL, tiene partes específicas que son muy relevantes para las API web y del explorador.

**Esquema**

El `scheme` anterior también se denomina `protocol` con API web y suele ser `http` o `https`. El protocolo de transferencia HTTP o HyperText es la forma en que los recursos, como las páginas web, se transfieren de un servidor web a un explorador web. HTTPS es la versión segura, en la que la transferencia se produce a través de Internet mediante la seguridad destinada a evitar interferencias con el recurso que se transfiere. Es común ver un pequeño icono de candado en la barra de direcciones del navegador cuando se visualiza una página a través de HTTPS.

Para las API web, las transferencias de estos recursos se producen a través de solicitudes HTTP: solicitudes a través de HTTP, en otras palabras.

**Hosts y dominios**

`business.adobe.com` es el host del recurso que se solicita. Cuando se hace clic en el vínculo de ejemplo, el explorador utiliza esta parte de la dirección URL para encontrar el servidor en el que está alojada la página. No siempre es exactamente lo mismo que el servidor web, pero en un nivel básico podemos pensarlo como el servidor donde el navegador obtendrá la página que solicitamos.

Los nombres de dominio forman parte del Sistema de nombres de dominio, más conocido como DNS. La mayoría de las personas consideran a `adobe.com` o `example.com` como un &quot;nombre de dominio&quot;, pero hay partes relevantes para las API. `www.adobe.com` y `business.adobe.com` pueden llamarse nombres de dominio, pero las partes `www.` y `business.` se denominan subdominios. Las API suelen interactuar con una dirección URL que incluye un subdominio como `api.example.com` o `sub.www.example.com`.

Es muy común ver que el término _host_ hace referencia a un nombre de dominio completo, incluido cualquier subdominio como `business.adobe.com`. También es común ver los términos _dominio_ o _nombre de dominio_ al hacer referencia a un host sin el subdominio como `adobe.com`. Memorizar los términos específicos de cada parte y variación de un host no es importante aquí. Sin embargo, tener en cuenta que estos términos se utilizan comúnmente es importante para que pueda aclarar cualquier detalle relevante para su negocio y discusiones.

**Origen**

Origen es otro término que hay que tener en cuenta que está estrechamente relacionado con las partes de una dirección URL. En un nivel básico, un origen es aproximadamente `scheme` más `host` más `domain` como `https://business.adobe.com`. Los distintos valores suelen representar orígenes diferentes, como `https://business.adobe.com` y `http://business.adobe.com`, no son el mismo origen porque tienen esquemas diferentes. `https://www.adobe.com` y `https://business.adobe.com` tampoco son el mismo origen en muchos usos debido a los diferentes subdominios.

**Ruta**

El último bit del ejemplo de URL anterior es el `path` del recurso, la página de nuestro ejemplo. La parte `/products/experience-platform/` suele representar carpetas o directorios en el servidor web. Al igual que tenemos carpetas o directorios en nuestros equipos para documentos y fotos, también tenemos carpetas en servidores web para organizar el contenido. Y, por último, la parte `/adobe-experience-platform.html` es el nombre del archivo: la página web.

Hay otras partes más detalladas de una URL que se resaltarán en la siguiente parte de esta serie.

### API de terceros

Las API web a veces se denominan API de terceros. Piense en esto como en las partes involucradas en una transacción. En nuestro ejemplo de vínculo, usted (o más específicamente, su explorador) es el primero en la solicitud de la página. El servidor web es de segundo nivel. Entonces, ¿dónde está la tercera?

Es habitual que una página web incluya contenido o recursos de otros hosts o fuentes. En estos casos, cuando el navegador comienza a mostrar la página, realiza otro conjunto de solicitudes a esos otros hosts, o &quot;terceros&quot;, que alojan esos recursos. Esto es muy común, especialmente para contenido multimedia como vídeos o imágenes, pero también para datos que deben actualizarse en el momento en que se ven o utilizan. Obtener la hora actual del día, el clima actual o un mensaje de bienvenida personalizado para una persona específica son ejemplos en los que una API de terceros puede proporcionar el recurso adecuado en el momento adecuado. Es común que estas solicitudes provengan de estas API de terceros.

## Usos comunes de las API web

Aparte de la hora del día, el tiempo o el contenido personalizado, hay muchos usos para las API web. Las plataformas de medios sociales como Twitter, TikTok, Facebook, LinkedIn, Snapchat, Pinterest y otras tienen una variedad de API que los programadores pueden utilizar con sus aplicaciones. Y, por supuesto, el Adobe también tiene [una amplia variedad de API](https://developer.adobe.com/apis) que los programadores utilizan para que su software pueda interactuar con los productos y servicios del Adobe. Los productos y servicios de software acceden a otros productos y servicios de software a través de estas API.

## API de ejemplo

Las API de explorador permiten a los programadores interactuar directamente con las funciones del explorador. La API de batería permite que el software compruebe el estado de la batería de un dispositivo para que pueda avisarle si es necesario. La API del portapapeles permite al software copiar o pegar con el portapapeles del dispositivo. La API de pantalla completa permite al software presentar la opción para expandir la vista a la pantalla completa del dispositivo, como YouTube.

La API de acceso a datos de Adobe Experience Platform es una API web que permite a los programadores acceder y descargar archivos de conjuntos de datos de Adobe Experience Platform para que puedan utilizar los datos de perfil del cliente en sus propios programas. Es muy común que las API como esta formen parte de un proceso de automatización de software en el que el software está programado para realizar una secuencia de pasos utilizando varias API en combinación. Esto suele suponer un ahorro de costes significativo en comparación con la realización manual de estos mismos pasos.

## Extremos de API

Cuando los programadores &quot;utilizan&quot; un navegador o API web en sus programas, suelen realizar solicitudes para enviar o recibir recursos, como nuestro explorador de ejemplo que solicita una página web. La documentación de API a menudo enumera los &quot;extremos&quot; de esas solicitudes; por ejemplo: `https://platform.adobe.io/data/foundation/export/files/{dataSetFileId}`. Este es el patrón específico o &quot;extremo&quot; de la API de acceso a datos de Platform que utilizará un programador para obtener un archivo de conjunto de datos.

`{dataSetFileId}` entre llaves representa un valor que el programador necesita enviar en la solicitud. Por lo tanto, la dirección URL de la solicitud de API real sería similar a `https://platform.adobe.io/data/foundation/export/files/xyz123brb`, donde `xyz123brb` debe ser un identificador válido del archivo de conjunto de datos que el programador desea recibir.

En otras palabras, del mismo modo que el explorador obtiene una página en una dirección URL específica, las solicitudes de API obtienen recursos de un extremo específico, o los envían a, como este ejemplo de conjunto de datos.

## Métodos de solicitud HTTP

En este punto, debería quedar claro que las API web realizan solicitudes de recursos como páginas web o conjuntos de datos. Al igual que la mayoría de los conceptos de software, estas solicitudes HTTP siguen patrones repetibles. Se envía una solicitud desde una aplicación de software a otra aplicación de software que evalúa la solicitud y, a continuación, responde: el explorador solicita una página de un servidor web y responde con el contenido de la página.

Todo el proceso, desde la solicitud hasta la respuesta, implica muchos pasos más pequeños y muy detallados, pero los métodos de solicitud son sencillos. Los métodos de solicitud definen la operación que se solicita.

**`GET`**

El método de solicitud `GET` se usa al solicitar una respuesta que proporciona un recurso, como nuestra página web y los ejemplos de conjuntos de datos. Cuando hacemos clic en un vínculo en un explorador o tocamos un vínculo en un dispositivo móvil, realizamos una solicitud `GET` entre bastidores.

**`POST`**

El método `POST` envía datos con la solicitud. Puede sonar extraño que una &quot;solicitud&quot; envíe datos, pero la idea es que al realizar la solicitud de API se está pidiendo al punto de conexión (el software receptor) que acepte la solicitud, y en el caso de un `POST`, que también acepte los datos que se envían. Los datos enviados se suelen escribir en un almacén de datos, como una base de datos o un archivo, para poder guardarlos.

**`PUT`**

El método de solicitud `PUT` es similar a `POST` porque envía datos, pero si los datos que se están enviando ya existen en el extremo, un `PUT` actualizará los datos existentes reemplazándolos. Un(a) `POST` no se actualiza, simplemente envía, de modo que varias solicitudes `POST` pueden crear varios registros de los datos enviados, en lugar de actualizar cualquier registro existente.

**`PATCH`**

El método de solicitud `PATCH` se usa para enviar datos que actualizan parte de un registro existente, como cuando cambiamos nuestra dirección al actualizar nuestro perfil de cuenta. Con una solicitud `POST` se podría crear un perfil adicional y con un `PUT`, se podría reemplazar el perfil existente, pero usando el método `PATCH` simplemente actualizamos la parte relevante del registro existente, como nuestra dirección.

**`DELETE`**

El método de solicitud `DELETE` quita un recurso especificado en la solicitud, como si hacemos clic en un vínculo para eliminar completamente el perfil de la cuenta.

Hay varios más, pero esta es una lista de los métodos más comunes al trabajar con API.

### Solicitar ejemplo

Ahora que tiene los términos, conceptos y pasos básicos involucrados con las API, podemos ver un ejemplo de solicitud de API en la práctica.

La página del ejemplo de nuestro explorador tiene una dirección URL de `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html`. Cuando se hace clic en el vínculo de Adobe Experience Platform, el explorador realiza una solicitud `GET` para esta página. Como tenemos el navegador para hacer el trabajo por nosotros, todo lo que tenemos que hacer es hacer clic, pero si un programador quiere que esa solicitud se produzca en una aplicación de software, tiene que proporcionar todos los detalles necesarios para que la solicitud de API se cumpla con éxito.

Este es el aspecto que podría tener el código:

```js
fetch(
  "https://business.adobe.com/products/experience-platform/adobe-experience-platform.html",
  {
    headers: {
      accept:
        "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
      "accept-language": "en-US,en;q=0.9",
      "sec-ch-ua":
        '" Not A;Brand";v="99", "Chromium";v="101", "Microsoft Edge";v="101"',
      "sec-fetch-dest": "document",
      "sec-fetch-mode": "navigate",
      "sec-fetch-site": "none",
      "sec-fetch-user": "?1",
      "upgrade-insecure-requests": "1",
    },
    referrerPolicy: "strict-origin-when-cross-origin",
    body: null,
    method: "GET",
    mode: "cors",
    credentials: "include",
  }
);
```

En el código anterior, puede ver el `URL` que el explorador solicita y abajo, cerca de la parte inferior, está el método de solicitud `method: "GET"`. Las otras líneas de código también son partes de la solicitud, pero están fuera del ámbito de este artículo.


*[API]: interfaz de programación de aplicaciones
*[URL]: Localizador uniforme de recursos
*[HTTP]: protocolo de transferencia de hipertexto
*[DNS]: Sistema de nombres de dominio
