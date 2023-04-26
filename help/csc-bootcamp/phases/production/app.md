---
title: 'Campo de inicio CSC: Crear contenido de aplicación móvil'
description: 'Campo de inicio CSC: Crear contenido de aplicación móvil'
doc-type: multipage-overview
source-git-commit: 989e4e2add1d45571462eccaeebcbe66a77291db
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 22%

---

# Crear contenido de aplicación móvil

## ¿Qué es la entrega de contenido sin encabezado?

Con un sistema de administración de contenido sin encabezado, el servidor y el front-end están ahora disociados. La parte sin encabezado es el back-end de contenido, ya que un CMS sin encabezado es un sistema de administración de contenido solo de back-end, diseñado y creado explícitamente como repositorio de contenido que hace que el contenido sea accesible a través de una API, para su visualización en cualquier dispositivo.

El front-end, que se desarrolla y mantiene de forma independiente, obtiene contenido del back-end sin encabezado mediante una API de entrega de contenido, normalmente en formato JSON. Por ejemplo, esto podría ser como una aplicación web o, en nuestro caso, como una aplicación móvil.

Un back-end CMS sin encabezado generalmente requiere que el contenido esté estructurado, basado en un modelo o esquema. Esto facilita a las aplicaciones cliente que solicitan el contenido adecuado para procesar una experiencia. Algunos CMS, como AEM, pueden exponer contenido estructurado y no estructurado en formato JSON.

Una característica clave de esta topología es que el contenido servido por el CMS sin encabezado en formato JSON es contenido puro, sin información de diseño. En una implementación de CMS sin encabezado, todo el formato y el diseño se mantienen en la aplicación de front-end desacoplada.

Una ventaja clave de una topología CMS sin encabezado es la capacidad de reutilizar contenido en varios canales, que pueden utilizar diferentes implementaciones de front-end del lado del cliente. Esto puede hacer que el proceso de desarrollo de front-end sea más eficiente. Pero también significa que el proceso de desarrollo de experiencias front-end puede convertirse en un proceso centrado en el código y la TI, y que, básicamente, la TI es la propietaria de la experiencia.

## ¿Cómo funciona la entrega de contenido sin encabezado en AEM?

AEM as a Cloud Service es una herramienta flexible para el modelo de implementación sin encabezado que ofrece tres potentes características:

![Entrega de contenido sin encabezado](./images/prod-app-headless.png)

1. Modelos de contenido
   - Los modelos de contenido son una representación estructurada del contenido.
   - Los modelos de contenido los definen los arquitectos de información en el editor del modelo de fragmentos de contenido de AEM.
   - Los modelos de contenido sirven de base para los fragmentos de contenido.
1. Fragmentos de contenido
   - Los fragmentos de contenido se crean en función de un modelo de contenido.
   - Creado por los autores de contenido mediante el editor de fragmentos de contenido de AEM.
   - Los fragmentos de contenido se almacenan en AEM Assets y se administran en la IU del administrador de Assets.
1. API de contenido para entrega
   - La API de GraphQL de AEM es compatible con la entrega de fragmentos de contenido.
   - La API de REST de AEM Assets es compatible con las operaciones de CRUD de fragmento de contenido.
   - La entrega de contenido directa también es posible con la [Exportación JSON del componente principal del fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=en).

## Ejercicio

Para este bootcamp, nos centraremos en la parte &quot;contenido&quot; - después de todo, es la cadena de suministro de contenido que buscamos. Ya hemos previsto un modelo de contenido, así como las API de envío necesarias, para que pueda centrarse en lo que es importante.

Exploremos primero nuestro modelo de contenido: es el &quot;contrato&quot; que tenemos con el CMS sin cabeza, así que sabemos qué contenido puede venir en nuestro camino y en qué formato.

- Vaya al autor de AEM en [https://author-p105462-e991028.adobeaemcloud.com/](https://author-p105462-e991028.adobeaemcloud.com/) e inicie sesión con las credenciales que proporcionamos.

- En el menú Inicio de AEM, seleccione Herramientas \> General \> Modelos de fragmento de contenido

![menú de modelos de fragmentos de contenido](./images/prod-app-cfm.png)

- En la siguiente pantalla, obtendrá una descripción general de todos los sitios que utilizan contenido sin encabezado. Esto le permite mantener el gobierno en varios sitios sin cabeza, sin tener que temer que interfieran entre ellos. En nuestro caso, estamos trabajando con nuestro sitio Adobike, así que seleccione ese modelo.

![diferentes sitios sin encabezado](./images/prod-app-cfm-folder.png)

- En esta carpeta, podemos ver algún contenido técnico sin encabezado que estamos utilizando en el sitio web de Adobe. ¿Está interesado en saber más? Siéntase libre de contactar. Por ahora, centrémonos en la tarea antes que en las manos: la aplicación móvil. Pase el ratón sobre la tarjeta de la página principal de la aplicación móvil y haga clic en el icono de lápiz para abrir el modelo de contenido.

![modelo de contenido de la página principal de la aplicación móvil](./images/prod-app-created-cfm.png)

- En el Editor del modelo de fragmento de contenido, puede ver los detalles de un determinado modelo de contenido. En nuestro caso, podemos ver la página de inicio de nuestra aplicación móvil que existe del logotipo de Adobike, un encabezado, algún texto libre opcional y un producto destacado opcional. Todos estos elementos son fáciles de configurar y actualizar, de modo que si el modelo de contenido necesita elementos adicionales, esto se puede hacer sin interferencias del desarrollador en el lado del CMS.

![modelo de contenido de detalles](./images/prod-app-cfm-details.png)

>[!WARNING]
>
> **Tenga en cuenta que cambiar el modelo de contenido tiene implicaciones en el futuro**, ya que la aplicación móvil depende de la recepción de cierta información para poder mostrar los elementos correctos. Tenga especial cuidado al actualizar o eliminar campos, la adición de campos no debería tener ningún impacto.

Ahora que tenemos una idea de de qué debe existir nuestro contenido, podemos hacer nuestro fragmento de contenido.

- Haga clic en el AEM Logotipo en la esquina superior izquierda para abrir la navegación y, a continuación, vaya a Navegación \> Fragmentos de contenido.

![opción de menú fragmentos de contenido](./images/prod-cf-ui.png)

- En la siguiente interfaz, se obtiene una descripción general de todo el contenido existente dentro de AEM. Los filtros de la izquierda pueden utilizarse para reducir el tamaño si busca un fragmento de contenido específico. Para crear un nuevo fragmento de contenido, haga clic en el botón &quot;Crear&quot; en la parte superior derecha.

![botón crear fragmento de contenido](./images/prod-app-create-cf.png)

- En el modal que se abre, verá que algunos campos aún no se pueden editar. Esto es lógico: en función de dónde creemos nuestro fragmento, estarán disponibles diferentes modelos.
   ![crear fragmento de contenido](./images/prod-app-create-cf-details.png)
   - En primer lugar, seleccione dónde crearemos nuestro fragmento haciendo clic en el icono de carpeta situado junto al campo &quot;Ubicación&quot;. Expanda el árbol de contenido haciendo clic en las carpetas &quot;adobike&quot; \> &quot;en&quot; \> &quot;mobile-app&quot; y, a continuación, confirme la selección haciendo clic en el botón &quot;Choose&quot;.
      ![seleccione la ubicación correcta](./images/prod-app-folder.png)
   - Verá que el campo &quot;Modelo de fragmento de contenido&quot; es ahora editable. Haga clic en la flecha situada junto al campo para abrir la lista desplegable y seleccionar el modelo de contenido que hemos visto anteriormente: &quot;Página principal de la aplicación móvil&quot;.
   - A continuación, asigne un título significativo al fragmento de contenido (sugerencia: incluya su número de equipo para recuperar fácilmente el contenido). Verá que el campo &quot;Nombre&quot; se rellena automáticamente para facilitar las cosas: es el nombre que utiliza el sistema para identificar el fragmento y no se debe tocar.
   - Finalmente, haga clic en el botón &quot;Crear y abrir&quot;, que como su nombre indica creará el fragmento de contenido y lo abrirá para que pueda editarlo inmediatamente.

- Aquí, su equipo puede decidir qué contenido desea mostrar en la aplicación móvil. ![detalles del fragmento de contenido](./images/prod-cf-details.png)
   - Asegúrese de seleccionar el número de equipo para que pueda comprobar el contenido más adelante en la aplicación móvil.
   - Para seleccionar recursos de imagen, haga clic en el icono de carpeta para buscar en AEM Assets la imagen correcta.
   - Para el producto destacado, haga clic en el icono de búsqueda de productos para que pueda seleccionar fácilmente nuestro producto de comercio &quot;Adobike 1&quot;, de modo que los detalles relacionados con el comercio se carguen en la aplicación.
   - Asegúrese de hacer clic en el botón &quot;Guardar&quot; cuando haya terminado de guardar todo el contenido creado y de publicar los cambios.
      ![publicar cambios](./images/prod-app-publish.png)

Ahora que hemos previsto la aplicación móvil con cierto contenido, estamos listos para entregar nuestra campaña.


Paso siguiente: [Fase 3 - Entrega: Verificar aplicación móvil](../delivery/app.md)

[Volver a la fase 2: Producción Crear publicidad en medios sociales](./social.md)

[Volver a todos los módulos](../../overview.md)
