---
title: Introducción básica a las API
description: Introducción a las interfaces de programación de aplicaciones
activity: understand
doc-type: article
feature-set: Experience Platform
feature: Server API,API,Data Collection,Integrations
level: Beginner
role: User,Developer
solution: Data Collection
topic: Integrations
exl-id: 9607e641-b0d5-49c1-b319-32ed0720e715
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 0%

---

# API 101: Introducción básica a las API

API significa Interfaz de programación de aplicaciones. Significa exactamente lo que dice: hay interfaces entre los programas y estas interfaces permiten que esos programas se comuniquen. Cuando los programadores desarrollan aplicaciones de software, a menudo necesitan su software para comunicarse con otro software o hardware. La API define el qué, cómo, cuándo, dónde y por qué para esas comunicaciones e interacciones.

Las API son una forma de resolver los desafíos comerciales con software. En la mayoría de las empresas, es un esfuerzo colaborativo. La colaboración siempre es más sencilla gracias a una comprensión compartida de los términos, conceptos y pasos clave.

Si piensa en hacer clic en un vínculo de una página web, el navegador utiliza bastantes API al hacer clic en el vínculo. El explorador reconoce el clic, realiza la solicitud de la página que desea visitar, recupera la página a través de Internet y, a continuación, la muestra en la pantalla. Hay muchos pasos más pequeños entre medias, pero su navegador es un software que se comunica y interactúa con una variedad de API solo para mostrarle una página web. En este artículo resaltaremos los términos, conceptos y pasos que son importantes al usar o discutir las API.

Al final de este artículo debe tener una comprensión clara de estos términos, conceptos y pasos fundacionales. La documentación de la API puede ser extensa, y las discusiones sobre el uso de API para abordar casos de uso específicos pueden ser muy detalladas. Navegar por la documentación y discutir las API es más fácil y productivo con fundamentos claros y entendimiento compartido.

>[!NOTE]
>
> Aunque hay muchas API, el enfoque aquí será en las API de explorador y web: básicamente, cuando una aplicación de software interactúa con otra a través de Internet.

## Términos y conceptos de API

¿Qué significa una palabra o frase, y cómo puedo pensarlo de manera simple y sencilla? En una API, la parte &quot;aplicación&quot; significa una aplicación de software o un programa. La parte &quot;interfaz de programación&quot; se refiere a cómo y dónde interactúa una aplicación con otra aplicación para determinados fines. En nuestro ejemplo de página web, al hacer clic en un vínculo, el explorador envía una solicitud a un servidor para la página web.

![Imagen del hipervínculo con la dirección URL de destino](../assets/api101-link-destination.png)

En esta captura de pantalla, el cursor del ratón se sitúa sobre el vínculo de Adobe Experience Platform. En la parte inferior está la barra de estado del explorador web que muestra la &quot;dirección&quot; de la página que obtendrá el explorador. En otras palabras, hacer clic en el vínculo de Adobe Experience Platform le dice al navegador que &quot;obtenga esa página para que pueda verla aquí en mi pantalla&quot;.

Cuando se hace clic en un vínculo, el explorador realiza una solicitud a un servidor para obtener una página. Esto es un `GET` , uno de los métodos de solicitud que se utiliza comúnmente con las API web. Una cosa que el navegador necesita para cumplir la solicitud es la página &quot;dirección&quot; - ¿dónde está en la web?

### Partes de una dirección URL

![Barra de direcciones del explorador con dirección URL](../assets/api101-address-bar.png)

La mayoría de los exploradores tienen una &quot;barra de direcciones&quot; que muestra parte o la totalidad de la &quot;dirección&quot; de una página web. Cuando el explorador &quot;obtiene&quot; la página del vínculo en el que hicimos clic, muestra la &quot;dirección&quot; de la página en esta barra de direcciones. Entonces, ¿cuál es la &quot;dirección&quot; de una página web?

that `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html` arriba está la dirección de una página en la web, y se llama URL o Localizador uniforme de recursos. Las direcciones URL pueden hacer referencia a una página como esta, un archivo de imagen, un vídeo u otros tipos de archivo.

![Partes de una dirección URL](../assets/api101-url-parts.jpg)

Esta dirección, la URL, tiene partes específicas que son muy relevantes para las API de explorador y web.

**Esquema**

La variable `scheme` arriba también se denomina `protocol` con API web y normalmente `http` o `https`. El protocolo de transferencia HTTP o HyperText es el modo en que los recursos como las páginas web se transfieren de un servidor web a un explorador web. HTTPS es la versión segura, donde la transferencia se realiza a través de Internet utilizando seguridad para evitar interferencias con el recurso que se transfiere. Es común ver un pequeño icono de bloqueo en la barra de direcciones del navegador cuando se visualiza una página a través de HTTPS.

Para las API web, las transferencias de estos recursos se realizan a través de solicitudes HTTP, es decir, a través de HTTP.

**Hosts y dominios**

La variable `business.adobe.com` es el host del recurso que se solicita. Cuando se hace clic en el vínculo de ejemplo, el explorador utiliza esta parte de la dirección URL para encontrar el servidor en el que se aloja la página. No siempre es exactamente igual que el servidor web, pero en un nivel básico podemos pensar que es el servidor donde el navegador obtendrá la página que solicitamos.

Los nombres de dominio forman parte del sistema de nombres de dominio, más conocido como DNS. La mayoría de la gente piensa en `adobe.com` o `example.com` como &quot;nombre de dominio&quot;, pero hay partes relevantes para las API. `www.adobe.com` y `business.adobe.com` puede denominarse nombres de dominio, pero la variable `www.` y `business.` las partes se denominan subdominios. Las API suelen interactuar con una dirección URL que incluye un subdominio como `api.example.com` o `sub.www.example.com`.

Es muy común ver el término _host_ consulte un nombre de dominio completo que incluya cualquier subdominio como `business.adobe.com`. También es común ver los términos _domain_ o _nombre de dominio_ al hacer referencia a un host sin el subdominio como `adobe.com`. Aquí no es importante recordar los términos específicos de cada parte y la variación de un host. Sin embargo, es importante tener en cuenta que estos términos se utilizan habitualmente para que pueda aclarar cualquier detalle relevante para su negocio y sus discusiones.

**Origen**

El origen es otro término que debe tenerse en cuenta y que está estrechamente relacionado con las partes de una URL. En un nivel básico, un origen es aproximadamente la variable `scheme` además de `host` además de `domain` like `https://business.adobe.com`. Los distintos valores a menudo representan orígenes diferentes como `https://business.adobe.com` y `http://business.adobe.com` no son el mismo origen porque tienen esquemas diferentes. `https://www.adobe.com` y `https://business.adobe.com` tampoco son el mismo origen en muchos usos debido a los diferentes subdominios.

**Ruta**

El último bit del ejemplo de URL anterior es el `path` al recurso: la página de nuestro ejemplo. La variable `/products/experience-platform/` generalmente representa carpetas o directorios en el servidor web. Al igual que tenemos carpetas o directorios en nuestros ordenadores para documentos y fotos, también tenemos carpetas en servidores web para organizar el contenido. Y finalmente, el `/adobe-experience-platform.html` part es el nombre del archivo: la página web.

Hay otras partes más detalladas de una URL que se resaltarán en la siguiente parte de esta serie.

### API de terceros

Las API web a veces se denominan API de terceros. Piensen en esto como en las partes involucradas en una transacción. En nuestro ejemplo de vínculo, usted (o, más específicamente, su navegador) es el primer usuario en la solicitud de la página. El servidor web es de segundo nivel. Entonces, ¿dónde está la tercera?

Es común que una página web incluya contenido o recursos de otros hosts o fuentes. En esos casos, cuando el explorador empieza a mostrar la página, realiza otro conjunto de solicitudes a esos otros hosts, o &quot;terceros&quot;, que alojan esos recursos. Esto es muy común, especialmente para contenido multimedia como vídeos o imágenes, pero también para datos que deben actualizarse en el momento en que se ven o utilizan. Obtener la hora del día actual, el tiempo actual o un mensaje de bienvenida personalizado para una persona específica son todos ejemplos en los que una API de terceros puede proporcionar el recurso correcto en el momento adecuado. Es común que esas solicitudes provengan de estas API de terceros.

## Usos comunes para las API web

Además de la hora del día, el clima o el contenido personalizado, existen muchos usos para las API web. Las plataformas de medios sociales como Twitter, TikTok, Facebook, LinkedIn, Snapchat, Pinterest y otras tienen una variedad de API que los programadores pueden utilizar con sus aplicaciones. Y por supuesto, el Adobe también tiene [una amplia variedad de API](https://developer.adobe.com/apis) que los programadores utilizan para que su software pueda interactuar con los productos y servicios de Adobe. Los productos y servicios de software acceden a otros productos y servicios de software a través de estas API.

## API de ejemplo

Las API de navegador permiten a los programadores interactuar directamente con las funciones del navegador. La API de batería permite que el software compruebe el estado de la batería de un dispositivo para que pueda avisarle si lo necesita. La API del portapapeles permite al software copiar o pegar con el portapapeles del dispositivo. La API de pantalla completa permite al software presentar la opción para expandir la vista a pantalla completa del dispositivo, como YouTube.

La API de acceso a datos de Adobe Experience Platform es una API web que permite a los programadores acceder y descargar archivos de conjuntos de datos de Adobe Experience Platform para que puedan utilizar los datos de perfil del cliente en sus propios programas. Es muy común que API como esta formen parte de un proceso de automatización de software en el que el software está programado para realizar una secuencia de pasos usando varias API en combinación. A menudo, esto puede suponer un ahorro significativo en comparación con la realización manual de esos mismos pasos.

## Puntos finales de API

Cuando los programadores &quot;utilizan&quot; un navegador o una API web en sus programas, suelen realizar solicitudes para enviar o recibir recursos, como nuestro navegador de ejemplo que solicita una página web. La documentación de API a menudo enumera los &quot;extremos&quot; para esas solicitudes, por ejemplo: `https://platform.adobe.io/data/foundation/export/files/{dataSetFileId}`. Este es el patrón específico o &quot;punto final&quot; de la API de acceso a datos de plataforma que un programador utilizará para obtener un archivo de conjunto de datos.

La variable `{dataSetFileId}` rodeado por esas llaves representa un valor que el programador debe enviar en la solicitud. Por lo tanto, la URL en la solicitud de API real tendría un aspecto similar al siguiente `https://platform.adobe.io/data/foundation/export/files/xyz123brb` donde `xyz123brb` debe ser un ID válido del archivo del conjunto de datos que el programador desee recibir.

En otras palabras, al igual que el explorador obtiene una página en una dirección URL específica, las solicitudes de API obtienen recursos de un extremo específico como este ejemplo de conjunto de datos, o los envían a.

## Métodos de solicitud HTTP

En este punto, debe quedar claro que las API web realizan solicitudes de recursos como páginas web o conjuntos de datos. Al igual que la mayoría de los conceptos de software, estas solicitudes HTTP siguen patrones repetibles. Se envía una solicitud desde una aplicación de software a otra aplicación de software que evalúa la solicitud y luego responde: el explorador solicita una página de un servidor web y responde con el contenido de la página.

Todo el proceso, desde la solicitud hasta la respuesta, implica muchos pasos más pequeños y muy detallados, pero los métodos de solicitud son sencillos. Los métodos de solicitud definen la operación que se solicita.

**`GET`**

La variable `GET` se utiliza el método request al solicitar una respuesta que proporciona un recurso, como nuestros ejemplos de página web y conjuntos de datos. Al hacer clic en un vínculo de un navegador o pulsar un vínculo de un dispositivo móvil, se crea un `GET` solicite entre bastidores.

**`POST`**

La variable `POST` envía datos con la solicitud. Puede parecer extraño que una &quot;solicitud&quot; envíe datos, pero la idea es que hacer la solicitud de API está pidiendo al punto final (el software receptor) que acepte la solicitud y, en el caso de una `POST`, para aceptar también los datos que se están enviando. Los datos enviados suelen escribirse en un almacén de datos como una base de datos o un archivo para que se puedan guardar.

**`PUT`**

La variable `PUT` el método de solicitud es similar a `POST` ya que envía datos, pero si los datos que se envían ya existen en el punto final, una `PUT` actualizará los datos existentes reemplazándolos. A `POST` no actualiza, simplemente envía, por lo que varias `POST` Las solicitudes de pueden crear varios registros de los datos enviados, en lugar de actualizar cualquier registro existente.

**`PATCH`**

La variable `PATCH` El método request se utiliza para enviar datos que actualizan parte de un registro existente, como cuando cambiamos nuestra dirección actualizando nuestro perfil de cuenta. Con un `POST` solicitud se puede crear un perfil adicional y con un `PUT`, el perfil existente podría reemplazarse, pero utilizando la variable `PATCH` simplemente actualizamos la parte relevante del registro existente, como nuestra dirección.

**`DELETE`**

La variable `DELETE` El método request elimina un recurso especificado en la solicitud, como si hiciéramos clic en un vínculo para eliminar por completo nuestro perfil de cuenta.

Hay varios otros, pero esta es una lista de los métodos más comunes al trabajar con API.

### Ejemplo de solicitud

Ahora que tiene los términos, conceptos y pasos básicos relacionados con las API, podemos ver una solicitud de API de ejemplo en la práctica.

La página del ejemplo de nuestro navegador tiene una dirección URL de `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html`. Cuando se hace clic en el vínculo de Adobe Experience Platform, el explorador realiza una `GET` para esta página. Dado que tenemos el navegador para hacer el trabajo por nosotros, todo lo que tenemos que hacer es hacer clic, pero si un programador quiere que esa solicitud se realice en una aplicación de software, debe proporcionar todos los detalles requeridos para que la solicitud de API se complete con éxito.

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

En el código anterior, puede ver la variable `URL` el explorador solicita y, cerca de la parte inferior, está la variable `method: "GET"` método de solicitud. Las otras líneas de código también son parte de la solicitud, pero están fuera del alcance de este artículo.


*[API]: Interfaz de programación de aplicaciones *[URL]: Localizador uniforme de recursos *[HTTP]: Protocolo de transferencia de hipertexto *[DNS]: Sistema de nombres de dominio
