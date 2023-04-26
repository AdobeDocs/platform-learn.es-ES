---
title: 'CSC Bootcamp : cree un banner de página de inicio de producto'
description: 'CSC Bootcamp : cree un banner de página de inicio de producto'
doc-type: multipage-overview
source-git-commit: 989e4e2add1d45571462eccaeebcbe66a77291db
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---

# Crear banner de página de inicio del producto

## Producción del banner

La automatización de contenido aporta la potencia de Adobe Creative Cloud a Experience Manager Assets, lo que permite a los especialistas en marketing automatizar la producción de recursos a escala, lo que acelera considerablemente la creación de variaciones. Usemos estas funcionalidades para generar un banner que se usará en la página principal.

- Vaya al autor de AEM en [https://author-p105462-e991028.adobeaemcloud.com/](https://author-p105462-e991028.adobeaemcloud.com/) e inicie sesión con las credenciales que proporcionamos.

- En la página de inicio, vaya a Herramientas \> Recursos \> Perfiles de procesamiento.

![Herramientas > Assets > Perfiles de procesamiento](./images/prod-processing-profiles.png)

- En la interfaz, verá todos los perfiles de procesamiento existentes. Se pueden usar para habilitar determinadas automatizaciones.

![lista de perfiles de procesamiento](./images/prod-profile-list.png)


- Las siguientes son de interés para usted:
   - Banner oscuro de Adobike: crea un banner de Adobe con una superposición oscura, basada en el recurso seleccionado
      ![banner oscuro](./images/prod-banner-dark.jpg)
   - Banner de Adobe: crea un banner de Adobe con una superposición ligera, en función del recurso seleccionado
      ![banner ligero](./images/prod-banner-light.jpg)
   - Banner verde de Adobe: crea un banner de Adobe con una superposición verde, en función del recurso seleccionado
      ![banner verde](./images/prod-banner-green.jpg)

- Una vez que haya elegido el tipo de banner que desea crear, seleccione ese perfil de procesamiento y, a continuación, seleccione &quot;Aplicar perfil a las carpetas&quot;.

![aplicar perfil a carpeta](./images/prod-apply-profile.png)

- En la siguiente pantalla, vaya a la carpeta de su equipo en AEM Assets. A continuación, en la parte superior izquierda, seleccione el botón &quot;Crear&quot; para crear una nueva carpeta y asígnele un nombre significativo, por ejemplo &quot;Crear titular oscuro&quot;.

![crear carpeta](./images/prod-create-profile-folder.png)

![crear detalles de carpeta](./images/prod-profile-folder-details.png)

- Después de crear la carpeta, marque la casilla junto a su nombre y luego haga clic en el botón &quot;Aplicar&quot; en la parte superior derecha.

![aplicar a la carpeta creada](./images/prod-select-profile-folder.png)

Ahora que hemos hecho la configuración necesaria, generemos nuestro banner.

- Haga clic en el AEM Logotipo en la esquina superior izquierda para abrir la navegación y, a continuación, vaya a Navegación \> Assets \> Archivos.

![pantalla de inicio de aem](./images/prod-select-assets.png)
![pantalla aem assets](./images/prod-select-assets-2.png)

- Busque la carpeta &quot;Recursos Adobe generados&quot; y ábrala haciendo clic en la tarjeta . Aquí es donde aparecerán los banners generados.

![recursos de adobike generados](./images/prod-generated-banners.png)

- Abra una nueva pestaña y vuelva a navegar a AEM Assets . A continuación, vaya a la carpeta a la que aplicamos el perfil de procesamiento.

- En la carpeta , cargue la imagen para la que desee crear un banner arrastrándola y soltándola en el explorador o haciendo clic en Crear \> archivos en la esquina superior derecha de la interfaz.

![cargar mediante arrastrar y colocar](./images/prod-drag-drop-banner.png)

![cargar mediante crear archivo](./images/prod-create-file.png)


- Espere un minuto para que el recurso se procese y vuelva a cargar la pantalla. Si ve el recurso en el estado &quot;Nuevo&quot;, sabe que ha finalizado el procesamiento.

![recurso en nuevo estado](./images/prod-asset-processed.png)

- Vuelva a la pestaña anterior y vuelva a cargar la pantalla aquí también. Debe observar un nuevo recurso con el estado &quot;Nuevo&quot;. Este es nuestro banner generado, ¡todo de DAM! ¿Todavía no lo veo? Espere otro minuto y vuelva a cargar la pantalla.

![banner generado](./images/prod-new-banner.png)

>[!NOTE]
>
> ¿No está satisfecho con el resultado? Siéntase libre de aplicar otro perfil de procesamiento a su carpeta y volver a cargar el recurso para generar un banner diferente (o cargar otro recurso, por supuesto). Durante la nueva carga, el sistema le preguntará qué desea hacer con el recurso existente y seleccione &quot;Reemplazar&quot;.
> ![reemplazar existente](./images/prod-replace-asset.png)

Ahora tenemos nuestro banner generado que podemos usar más adelante durante la entrega de nuestra campaña. Asegúrese de publicar el banner seleccionándolo y luego haciendo clic en el botón &quot;Publicación rápida&quot; de la cinta.

![publicar recurso](./images/prod-publish-banner.png)

## Seguimiento en Workfront

Si necesita un proceso formal y auditable de revisión y aprobación de sus recursos, Workfront es el lugar en el que debe estar.

>[!NOTE]
>
> Aunque lo mencionamos aquí explícitamente, es la intención actualizar las tareas en Workfront después de haberlas finalizado. Siempre debe esforzarse por obtener un flujo Create > Review > Approve .

- Volvamos a nuestro proyecto y expandamos el acordeón &#39;Go/No Go Banner Review&#39; para abrir la mencionada tarea haciendo clic en él:

![banner go/no go](./images/banner-gonogo.png)

- Haga clic en la sección de documentos de la tarea (columna izquierda) y, a continuación, haga clic en la carpeta vinculada de AEM Assets &quot;Final&quot;. Seleccione nuestro recurso haciendo clic en su zona y haga clic en &quot;Crear prueba&quot;. Una prueba es la capacidad de revisar contenido, por ejemplo, imagen, texto, vídeo, sitio web, etc., de manera estructurada y colaborativa, donde se recopilan comentarios, correcciones, modificaciones de las partes interesadas, se pueden comparar versiones y resultados y se puede aprobar por un solo clic.

![crear prueba](./images/wf-create-proof.png)

- Como queremos un proceso de aprobación detallado, seleccione &quot;Prueba avanzada&quot;.

![prueba avanzada](./images/wf-advanced-proof.png)

>[!NOTE]
>
> Vamos a decidir manualmente quién revisará y/o aprobará nuestra prueba en este bootcamp. En la mayoría de los casos de uso reales, utilizaríamos una plantilla preestablecida de flujos de aprobación ya definidos para cada tipo de prueba.

- De forma predeterminada, se encuentra en un tipo de flujo de trabajo &quot;básico&quot; y se selecciona su especialista de Bootcamp de Workfront como revisor y aprobador. Escriba el nombre de su especialista en Workfront de Bootcamp donde dice &quot;Escriba el nombre de contacto o la dirección de correo electrónico para agregar un destinatario:

![asignar prueba](./images/wf-proof-assign.png)

![asignar prueba](./images/wf-assign-proof-2.png)

- Configúrelos como &quot;Revisor y aprobador&quot;:

![revisor y aprobador](./images/wf-review-approve.png)

- Haga clic en &quot;Crear prueba&quot;. Workfront tardará unos minutos en generar la prueba:

![generar prueba](./images/wf-generating-proof.png)

- Su especialista en Workfront ahora habrá recibido una nueva notificación que les informa de que tienen una prueba para revisar o aprobar:

![tarea del área de trabajo](./images/wf-proof-task.png)

- Después de hacer clic en la notificación, enfrentarán su prueba y podrán realizar algunos comentarios y/o aprobar esta prueba.

   - Pueden hacer clic en &quot;Agregar comentario&quot; en la parte superior de la pantalla si tienen comentarios:

   ![Añadir comentario](./images/wf-proof-add-comment.png)

   - Luego podrán no solo añadir comentarios, sino también utilizar la pequeña barra de herramientas de punteros para definir claramente qué área necesita cambiar.

   ![Comentario de punto de conexión](./images/wf-proof-comment.png)

   - Al agregar el comentario, pueden indicarle que necesita hacer algún trabajo adicional en una nueva versión de la prueba. Actualice la pestaña de Workfront y tendrá una nueva notificación que le informará exactamente de eso. Una vez que sepa qué cambios tiene que hacer, realice los cambios en AEM y, a continuación, venga a cargar la nueva versión aquí:

   ![cargar nueva versión](./images/wf-upload-version.png)

   - Seleccione el recurso actualizado (si no se necesitan cambios en el escenario de bootcamp, vuelva a cargar el mismo recurso) y haga clic en &quot;Vincular&quot;:

   ![recurso de vínculo](./images/wf-link-new-asset.png)

   - A continuación, haga clic en &quot;crear prueba&quot; en el lado derecho.

   ![crear prueba](./images/create-new-proof.png)

   - Una vez generada la prueba (puede tardar unos minutos), su especialista en Workfront recibirá una notificación y podrá revisar y aprobar esta nueva versión con suerte.  Por ejemplo, si utilizan el botón de comparación de prueba, pueden ver una comparación en paralelo de V1 y V2 con todos los comentarios realizados.

   ![comparación de pruebas](./images/wf-proof-compare.png)

   ![tomar decisión](./images/make-decision-proof.png)

   ![aprobado](./images/approved.png)

Ahora tenemos una aprobación formal para el uso de nuestro banner. Es fácil seguir dónde estamos en el proceso y las actualizaciones que realiza automáticamente déclencheur de notificaciones, para que pueda trabajar de la manera más eficiente posible.

Paso siguiente: [Fase 2 - Producción: Crear publicidad en medios sociales](./social.md)

[Volver a la fase 1 - Planificación: Otros trabajos previos](../planning/prework.md)

[Volver a todos los módulos](../../overview.md)
