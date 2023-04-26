---
title: 'Campo de inicio CSC: cree una página en AEM'
description: 'Campo de inicio CSC: cree una página en AEM'
doc-type: multipage-overview
source-git-commit: 989e4e2add1d45571462eccaeebcbe66a77291db
workflow-type: tm+mt
source-wordcount: '1917'
ht-degree: 2%

---

# Crear página en AEM

AEM proporciona dos entornos: el entorno de creación y el entorno de publicación. Interactúan para permitirle ofrecer contenido en su sitio web, de modo que los visitantes puedan experimentarlo.

El entorno de creación ofrece mecanismos para crear, actualizar y revisar este contenido antes de publicarlo:

- Un autor crea y revisa el contenido (que puede ser de varios tipos; por ejemplo: páginas, recursos, publicaciones, etc.)
- que, en algún momento, se publicará en su sitio web.

Como creador, deberá organizar el sitio web dentro de AEM. Esto implica crear y dar nombre a las páginas de contenido para que:

- Pueda encontrarlas con facilidad en el entorno de creación
- Los usuarios que visiten el sitio web puedan explorarlas fácilmente en el entorno de publicación

La estructura de un sitio web se puede considerar como una estructura de árbol que alberga las páginas de contenido. Los nombres de estas páginas de contenido se usan para formar las direcciones URL, mientras que el título se muestra cuando se visualiza el contenido de la página. En el ejemplo siguiente, la dirección URL accesible para la página será /content/adobike/language-masters/en.html

![estructura de página](./images/delivery-web-structure.png)

Vamos a revisar cómo agregar algunas páginas nuevas a un sitio web existente, así como cómo reutilizar parte del contenido.

## Creación de la página principal

Como se explicó en la sección anterior, AEM jerarquía de páginas funciona como una estructura de árbol. Esto significa que empezaremos con la página en el nivel más alto: la página principal.

- Vaya al autor de AEM en [https://author-p71057-e991028.adobeaemcloud.com/](https://author-p71057-e991028.adobeaemcloud.com/) e inicie sesión con las credenciales que proporcionamos.

- En el menú Inicio de AEM, seleccione Navegación \> Sitios

![seleccione el icono sitios](./images/delivery-web-aem-sites.png)

- Primero, vamos a navegar por la estructura de árbol existente hasta la ubicación en la que nos gustaría crear nuestra página principal. Navegue por la estructura de árbol seleccionando &quot;Adobike&quot; en la primera columna y luego &quot;Bootcamp&quot; en la segunda columna. A continuación, para crear una página debajo de esta página, haga clic en el botón &quot;Crear&quot; y seleccione &quot;Página&quot; en el menú que aparece.

![vuelva a buscar el contenido de bootcamp](./images/delivery-web-create-page.png)

- Se abrirá una nueva pantalla para configurar la nueva página. En primer lugar, podemos seleccionar una plantilla de página. Las plantillas de página de AEM permiten definir la estructura de una página, así como definir qué contenido se puede utilizar en esta página. Como queremos crear la página de inicio, que es una página de aterrizaje, seleccionaremos la plantilla de página de aterrizaje y luego haremos clic en el botón &quot;Siguiente&quot; para continuar.

![seleccione la plantilla correcta](./images/delivery-web-create-page-template.png)

- En la siguiente pantalla, podrá rellenar la página con información inicial. La información más importante es el título (una propiedad obligatoria, indicada con un \* ), que está diseñado para que usted asigne a su página un nombre significativo. Si no rellena el &quot;Nombre&quot;, AEM generará automáticamente la dirección URL en la que estará disponible su página, siguiendo las prácticas recomendadas de SEO. En este caso, puede dejar vacío este campo. Algunas otras propiedades también pueden ser rellenadas, puede explorar las otras pestañas, pero para el propósito de este bootcamp no rellene ninguna otra propiedad todavía. Cuando esté listo para crear su página, simplemente haga clic en el botón &quot;Crear&quot;.

![rellene las propiedades](./images/delivery-web-create-page-properties.png)

- AEM crear la página. Una vez hecho esto, aparecerá una ventana emergente que le permite abrir la página recién creada haciendo clic en el botón &quot;Abrir&quot;.

![Abra la página recién creada](./images/delivery-web-create-page-success.png)

- Ahora llegará al Editor de AEM. Este es un editor de &quot;lo que ve es lo que obtiene&quot; (o WYSIWYG), en el que puede arrastrar y soltar componentes en una página para crear su página. Veamos la navegación:
   ![editor wysiwig de aem](./images/delivery-web-page-editor-home.png)
   - En el lado izquierdo, tiene el panel lateral con los recursos que puede utilizar en sus páginas, los componentes (o bloques de construcción) que puede utilizar en esta página y una práctica vista de árbol que le muestra cómo está estructurada su página. Haga clic en cualquiera de estos iconos para abrir su vista.
   - A la derecha, verá el &quot;contenedor de diseño&quot;. Se trata de un área en la que puede soltar los componentes deseados.
   - Rellenemos nuestra página con algo de contenido. No dude en rellenar la página de inicio como prefiera. En el ejemplo siguiente, se ha utilizado un componente de imagen vinculado a la página del producto, así como dos componentes de teaser.

![la página principal](./images/delivery-web-homepage.png)

## Reutilizar experiencias aprovechando los fragmentos de experiencias

Ahora hemos creado la página principal, que está totalmente lista para nuestro lanzamiento de Adobe. Sin embargo, parte del contenido de allí, por ejemplo los puntos de venta únicos de nuestra bicicleta, puede reutilizarse en varias páginas.

Idealmente, queremos crear esta experiencia única de puntos de venta solo una vez para que podamos administrarla de forma centralizada y garantizar una experiencia personalizada pero coherente. En AEM, podemos hacerlo con &quot;Fragmentos de experiencias&quot;. Un fragmento de experiencia es un grupo de uno o más componentes que incluye contenido y diseño que se puede consultar dentro de las páginas. Pueden contener cualquier componente.

Vamos a usar esto de inmediato:

- Vaya al autor de AEM en [https://author-p71057-e991028.adobeaemcloud.com/](https://author-p71057-e991028.adobeaemcloud.com/) e inicie sesión con las credenciales que proporcionamos.

- En el menú Inicio de AEM, seleccione Navegación \> Fragmentos de experiencias

![seleccione el icono XF](./images/delivery-web-xf.png)

- En la siguiente pantalla, vamos a crear una carpeta que su equipo pueda utilizar para almacenar sus experiencias reutilizables. En la vista de columna, vaya a Adobe \> Bootcamp y, a continuación, haga clic en los botones Crear \> Carpeta.

![crear una carpeta](./images/delivery-web-create-xf-folder.png)

- En las ventanas emergentes modales, asigne a su carpeta el nombre de su equipo. Puede dejar vacío el campo de nombre, AEM lo generará automáticamente. Una vez que haya dado un nombre a la carpeta, haga clic en el botón Create para crear la carpeta.

![asígnele un nombre](./images/delivery-web-create-xf-folder-name.png)

- Ahora debería ver la carpeta emergente. Haga clic en él y, a continuación, haga clic en los botones Crear \> Fragmento de experiencia .

![crear un xf](./images/delivery-web-create-xf.png)

- Primero, vamos a seleccionar una plantilla de fragmento de experiencia. Al igual que las páginas, los fragmentos de experiencias pueden basarse en varias plantillas, cada una de las cuales prevé una experiencia predefinida. En nuestro caso, dado que queremos reutilizar nuestro contenido en nuestro sitio web, vamos a elegir una &quot;Plantilla de variación web de fragmento de experiencia&quot; al seleccionar la casilla de verificación en la parte superior izquierda y luego hacer clic en el botón &quot;Siguiente&quot;.

![seleccionar una plantilla xf](./images/delivery-web-create-xf-template.png)

- Asigne un título significativo al fragmento de experiencia, por ejemplo &quot;Adobike USPs&quot; y luego haga clic en el botón crear .

![asigne un título a xf](./images/create-xf-properties.png)

- Una vez creado el fragmento de experiencia, haga clic en el botón &quot;Abrir&quot; del modal para que podamos añadir contenido en nuestro fragmento de experiencia.

![haga clic en abrir](./images/delivery-web-create-xf-success.png)

- Al igual que cuando edita una página, puede ver un contenedor de diseño en el que puede añadir contenido.

![el editor xf](./images/delivery-web-xf-editor.png)

- Lo que haremos es copiar los componentes de la página principal. En una pestaña nueva, vaya a la página de inicio tal como se explica en el capítulo anterior, seleccione el componente que desea copiar y, a continuación, haga clic en el icono de copia.

![copiar un componente](./images/delivery-web-copy-from-home.png)

- A continuación, vuelva al fragmento de experiencia, haga clic en el contenedor de diseño y haga clic en el botón de pegado.

![pegar el componente](./images/delivery-web-paste-to-xf.png)

>[!NOTE]
>
> Sugerencia: AEM permite utilizar el &quot;modo de diseño&quot; en cualquier página o fragmento de experiencia. Esto le permite cambiar el tamaño de los componentes y optimizar las experiencias para cualquier dispositivo.

- En el menú superior, abra la lista desplegable y seleccione &quot;Diseño&quot; para entrar en el modo de diseño.

![cambiar al modo de diseño](./images/delivery-web-layout-mode.png)

- A continuación, puede seleccionar cualquier componente y cambiarle el tamaño simplemente arrastrando los controles a ambos lados del componente para ajustarlos a las columnas visibles en la pantalla.

![cambiar el tamaño de los componentes como desee](./images/delivery-web-layout-resize.png)

- De forma predeterminada, está editando todos los puntos de interrupción. Sin embargo, si desea editar para un punto de interrupción específico, puede seleccionar un dispositivo coincidente en la barra de herramientas de la parte superior de la página. A continuación, se resaltará el punto de interrupción para el que esté creando.

![seleccionar un punto de interrupción](./images/delivery-web-bp-before.png)

- Como puede ver, un diseño de dos columnas en dispositivos móviles no tiene un aspecto bueno. Vamos a crear un diseño de una columna en el móvil. Como puede verse en el escritorio, nuestra experiencia sigue siendo la misma, pero en el móvil ahora tenemos una mejor experiencia con solo una columna de contenido.

![optimizar para dispositivos móviles](./images/delivery-web-bp-after.png)

- Por último, ahora podemos reutilizar esta experiencia en la página principal. Arrastre y suelte un componente &quot;Fragmento de experiencia&quot; en la página en la ubicación en la que desea que se muestre el contenido. Puede eliminar el contenido que hemos copiado, ya que lo vamos a usar desde el fragmento de experiencia.

![arrastrar y soltar un componente xf](./images/delivery-web-xf-on-home.png)

- Abra el cuadro de diálogo de configuración del componente de fragmento de experiencia y utilice el selector de rutas para seleccionar la ubicación en la que creó el fragmento de experiencia.

![haga clic en el icono de carpeta](./images/delivery-web-xf-dialog.png)

![seleccione el XF correcto](./images/delivery-web-select-xf.png)

- Y finalmente, ahora tenemos nuestra experiencia reutilizable en nuestra página.

![la página principal actualizada](./images/delivery-web-xf-result.png)

## Creación de la página del producto

Al utilizar Adobe Commerce integrado con AEM, puede tener una página de detalles genérica del producto que se utiliza al navegar por el sitio desde las descripciones generales generadas. Sin embargo, a veces también queremos prever una página inspiradora que combine contenido específico del producto con contenido inspirador. Vamos a copiar sobre la tienda como lo hemos hecho previamente, y luego vamos a crear una página de producto inspiradora.

- Vaya al autor de AEM en [https://author-p71057-e991028.adobeaemcloud.com/](https://author-p71057-e991028.adobeaemcloud.com/) e inicie sesión con las credenciales que proporcionamos.

- En el menú Inicio de AEM, seleccione Navegación \> Sitios

![seleccione el icono sitios](./images/delivery-web-aem-sites.png)

- En la descripción general de la columna , desplácese al sitio web creado previamente hasta la tienda: Adobike \> Idiomas Masters \> Adobike \> Tienda. A continuación, seleccione la página de taller con la casilla de verificación y haga clic en Crear \> Live Copy. Sin entrar en demasiados detalles específicos, esto creará una copia de la página que puede usar en su sitio para que pueda reutilizar las páginas y el contenido ya existentes, usando AEM Administrador de varios sitios.

![crear una Live Copy](./images/delivery-web-create-lc.png)

- En la pantalla que aparece, seleccione el sitio de sus equipos como destino seleccionando la casilla junto a su nombre. A continuación, haga clic en el botón Next .

![seleccione el destino](./images/delivery-web-lc-destination.png)

- Como no vamos a profundizar en Multi Site Manager, solo puede asumir esta configuración.\
   Título: Tienda\
   Nombre: tienda\
   Configuración de lanzamiento: Configuración de lanzamiento estándar\
   Una vez configurada la Live Copy, haga clic en el botón Create .

![configurar la Live Copy](./images/delivery-web-lc-config.png)

>[!NOTE]
>
> ¿Curioso para más información sobre las Live Copies? Consulte [&quot;Creación y sincronización de Live Copies&quot;.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/reusing-content/msm/creating-live-copies.html?lang=en)

- Una vez finalizado, debería ver la tienda disponible en su sitio web. Selecciónela y luego haga clic en Crear \> Página para crear nuestra página de producto inspiradora.

![crear una página de producto](./images/delivery-web-create-pdp.png)

- Dado que queremos mostrar información del producto en la página, vamos a crear una página con la plantilla de página del producto. Selecciónela y luego haga clic en el botón Next .

![usar la plantilla de página de producto](./images/delivery-web-create-pdp-template.png)

- Complete los metadatos de la página y, a continuación, haga clic en el botón Crear , como en la página principal. Una vez creada, puede abrir la página haciendo clic en el botón abrir . Como puede ver, ya se ha rellenado con un componente de detalles del producto.

![finalizar la configuración](./images/delivery-web-pdp-initial.png)

- Primero, agregaremos nuestro fragmento de experiencia que hemos creado anteriormente. A continuación, podemos añadir cualquier contenido adicional que deseemos en la página. Finalmente, configuraremos el componente de detalles del producto para mostrar nuestro producto de Adobe seleccionando el buscador de productos en el cuadro de diálogo de configuración y luego nuestra categoría de Adobe y marcando la casilla junto al producto. A continuación, haga clic en el botón Add .

![seleccione el buscador de productos](./images/delivery-web-configure-product.png)

![seleccione el producto](./images/delivery-web-select-product.png)

- Ahora tenemos nuestra página de inspiración completa, que incluye contenido administrado centralmente e información de productos proveniente de Adobe Commerce.

![La página del producto](./images/delivery-web-pdp-result.png)

Paso siguiente: [Fase 3 - Entrega: VAYA A LA Campaña/NO VA](./go-nogo.md)

[Volver a la fase 3: Entrega Verificar aplicación móvil](./app.md)

[Volver a todos los módulos](../../overview.md)
