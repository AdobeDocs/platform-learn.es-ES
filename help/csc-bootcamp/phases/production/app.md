---
title: CSC Bootcamp - Crear contenido de aplicación móvil
description: CSC Bootcamp - Crear contenido de aplicación móvil
doc-type: multipage-overview
exl-id: db4e91da-2077-4133-aca9-e3413990f4be
source-git-commit: 143da6340b932563a3309bb46c1c7091e0ab2ee2
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---

# Creación de contenido de aplicación móvil

## ¿Qué es la entrega de contenido sin encabezado?

Con un sistema de administración de contenido sin encabezado, el back-end y el front-end están ahora disociados. La parte sin encabezado es el back-end del contenido, ya que un CMS sin encabezado es un sistema de administración de contenido de back-end diseñado y creado explícitamente como un repositorio de contenido que hace que el contenido sea accesible a través de una API para su visualización en cualquier dispositivo.

El front-end, que se desarrolla y mantiene de forma independiente, obtiene contenido del back-end sin encabezado mediante una API de entrega de contenido, normalmente en formato JSON. Por ejemplo, esto podría ser como una aplicación web o, en nuestro caso, como una aplicación móvil.

Un back-end CMS sin encabezado generalmente requiere que el contenido esté estructurado, basado en un modelo o esquema. Esto facilita a las aplicaciones cliente que solicitan el contenido adecuado para procesar una experiencia. AEM Algunos CMS, como los CMS, pueden exponer contenido estructurado y no estructurado en formato JSON.

Una característica clave de esta topología es que el contenido servido por el CMS sin encabezado en formato JSON es contenido puro, sin información de diseño. En una implementación sin encabezado de CMS, todo el formato y el diseño se mantienen en la aplicación de front-end desacoplada.

Una ventaja clave de una topología CMS sin encabezado es la capacidad de reutilizar contenido en varios canales, que pueden utilizar diferentes implementaciones de front-end del lado del cliente. Esto puede hacer que el proceso de desarrollo de front-end sea más eficiente. Pero también significa que el proceso de desarrollo de experiencias front-end puede convertirse en un proceso centrado en el código y la TI, y que, básicamente, la TI es la propietaria de la experiencia.

## AEM ¿Cómo funciona la entrega de contenido sin encabezado en la?

AEM as a Cloud Service es una herramienta flexible para el modelo de implementación sin encabezado que ofrece tres potentes funciones:

![Entrega de contenido sin encabezado](./images/prod-app-headless.png)

1. Modelos de contenido
   - Los modelos de contenido son una representación estructurada del contenido.
   - AEM Los modelos de contenido los definen los arquitectos de información en el editor del modelo de fragmentos de contenido de la.
   - Los modelos de contenido sirven de base para los fragmentos de contenido.
1. Fragmentos de contenido
   - Los fragmentos de contenido se crean en función de un modelo de contenido.
   - AEM Creado por los autores de contenido mediante el editor de fragmentos de contenido de la.
   - Los fragmentos de contenido se almacenan en AEM Assets y se administran en la IU del administrador de Assets.
1. API de contenido para envío
   - AEM La API de GraphQL admite la entrega de fragmentos de contenido.
   - La API de REST de AEM Assets admite operaciones de CRUD de fragmentos de contenido.
   - La entrega de contenido directa también es posible con la exportación [JSON del componente principal del fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es).

## Ejercicio

Para este bootcamp, nos centraremos en la parte de &quot;contenido&quot; - después de todo, es la cadena de suministro de contenido que buscamos. Ya hemos previsto un modelo de contenido, así como las API de envío necesarias, para que pueda centrarse en lo que es importante.

Exploremos primero nuestro modelo de contenido: es el &quot;contrato&quot; que tenemos con el CMS sin encabezado, para que sepamos qué contenido puede llegar hasta nosotros y en qué formato.

- AEM Vaya al autor del en [https://author-p105462-e991028.adobeaemcloud.com/](https://author-p105462-e991028.adobeaemcloud.com/) e inicie sesión con las credenciales que proporcionamos.

- AEM En el menú Inicio de la, seleccione Herramientas \> General \> Modelos de fragmentos de contenido

![menú de modelos de fragmento de contenido](./images/prod-app-cfm.png)

- En la siguiente pantalla, obtendrá una descripción general de todos los sitios que utilizan contenido sin encabezado. Esto le permite mantener el control sobre varios sitios sin encabezado, sin tener que temer que interfieran entre sí. En nuestro caso, estamos trabajando con nuestro sitio de Adobe Bike, así que seleccione ese modelo.

![diferentes sitios sin encabezado](./images/prod-app-cfm-folder.png)

- En esta carpeta, podemos ver algunos contenidos técnicos sin encabezado que estamos utilizando en el sitio web de Adobe. ¿Te interesa saber más? No dude en ponerse en contacto con. Por ahora, vamos a centrarnos en la tarea que tenemos ante nosotros: la aplicación móvil. Pase el ratón sobre la tarjeta Página principal de la aplicación móvil y haga clic en el icono de lápiz para abrir el modelo de contenido.

![modelo de contenido de página principal de aplicación móvil](./images/prod-app-created-cfm.png)

- En el Editor del modelo de fragmentos de contenido, puede ver los detalles de un modelo de contenido determinado. En nuestro caso, podemos ver que la página principal de nuestra aplicación móvil existe del logotipo de Adobike, un encabezado, algo de texto libre opcional y un producto destacado opcional. Todos estos elementos son fáciles de configurar y actualizar, de modo que si el modelo de contenido necesita elementos adicionales, esto se puede hacer sin la interferencia del desarrollador en el lado del CMS.

![modelo de contenido de detalles](./images/prod-app-cfm-details.png)

>[!WARNING]
>
> **Tenga en cuenta que cambiar el modelo de contenido tiene implicaciones más adelante**, ya que la aplicación móvil depende de la recepción de determinada información para poder mostrar los elementos correctos. Tenga mucho cuidado al actualizar o eliminar campos, añadir campos no debería tener ningún impacto.

Ahora que tenemos una idea de de qué debería existir nuestro contenido, podemos hacer que nuestro fragmento de contenido.

- AEM Haga clic en el logotipo de la en la esquina superior izquierda para abrir la navegación y, a continuación, vaya a Navegación \> Fragmentos de contenido.

![opción de menú de fragmentos de contenido](./images/prod-cf-ui.png)

- AEM En la siguiente interfaz, se obtiene una descripción general de todo el contenido existente dentro de la interfaz de, que puede ser más o menos la siguiente. Los filtros de la izquierda se pueden utilizar para reducir si está buscando un fragmento de contenido específico. Para crear un nuevo fragmento de contenido, haremos clic en el botón Crear en la parte superior derecha.

![botón crear fragmento de contenido](./images/prod-app-create-cf.png)

- En el modal que se abre, verá que algunos campos aún no se pueden editar. Esto es lógico: en función de dónde creemos nuestro fragmento, habrá disponibles diferentes modelos.
  ![crear fragmento de contenido](./images/prod-app-create-cf-details.png)
   - En primer lugar, seleccione dónde vamos a crear el fragmento haciendo clic en el icono de carpeta junto al campo &quot;Ubicación&quot;. Expanda el árbol de contenido haciendo clic en las carpetas &quot;adobike&quot; \> &quot;en&quot; \> &quot;mobile-app&quot; y, a continuación, confirme su selección haciendo clic en el botón &quot;Elegir&quot;.

     ![seleccione la ubicación correcta](./images/prod-app-folder.png)
   - Observará que el campo &quot;Modelo de fragmento de contenido&quot; ahora se puede editar. Haga clic en la flecha situada junto al campo para abrir la lista desplegable y seleccionar el modelo de contenido que vimos anteriormente: &quot;Página principal de la aplicación móvil&quot;.
   - A continuación, asigne un título significativo al fragmento de contenido (sugerencia: incluya el número de equipo para recuperar el contenido fácilmente). Observará que el campo &quot;Nombre&quot; se rellena automáticamente para facilitarle la vida: es el nombre que utiliza el sistema para identificar el fragmento y no se debe tocar.
   - Finalmente, haga clic en el botón &quot;Crear y abrir&quot;, que como su nombre indica, creará el fragmento de contenido y lo abrirá para que pueda editarlo inmediatamente.

- Aquí, su equipo puede decidir qué contenido desea mostrar en la aplicación móvil. ![detalles del fragmento de contenido](./images/prod-cf-details.png)
   - Asegúrese de seleccionar el número de equipo para poder comprobar el contenido más adelante en la aplicación móvil.
   - Para seleccionar recursos de imagen, haga clic en el icono de carpeta para buscar en AEM Assets la imagen correcta.
   - Para el producto destacado, haga clic en el icono de búsqueda de productos para que pueda seleccionar fácilmente nuestro producto de Commerce &quot;Adobe Bike 1&quot;, de modo que los detalles relacionados con el comercio se carguen en la aplicación.
   - Asegúrese de hacer clic en el botón &quot;Guardar&quot; cuando haya terminado de guardar todo el contenido creado y publicar los cambios.

     ![cambios de publicación](./images/prod-app-publish.png)

Ahora que hemos previsto la aplicación móvil con algún contenido, estamos listos para entregar nuestra campaña.


Siguiente paso: [Fase 3: Entrega: compruebe la aplicación móvil](../delivery/app.md)

[Volver a la fase 2: Producción: Crear anuncio en redes sociales](./social.md)

[Volver a todos los módulos](../../overview.md)
