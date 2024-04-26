---
title: Creación de un esquema XDM para datos web
description: Obtenga información sobre cómo crear un esquema XDM para datos web en la interfaz de recopilación de datos. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK,Schemas
jira: KT-15398
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 1%

---

# Creación de un esquema XDM para datos web

Obtenga información sobre cómo crear un esquema XDM para datos web en la interfaz de recopilación de datos de Adobe Experience Platform.

Los esquemas XDM (Experience Data Model) son los componentes básicos, los principios y las prácticas recomendadas para recopilar datos en Adobe Experience Platform.

El SDK web de Platform utiliza su esquema para estandarizar los datos de eventos web, enviarlos al Edge Network de Platform y, finalmente, reenviar los datos a cualquier aplicación del Experience Cloud configurada en la secuencia de datos. Este paso es fundamental, ya que define un modelo de datos estándar necesario para la ingesta de datos de experiencia del cliente en Experience Platform y permite la prestación de servicios y aplicaciones descendentes basados en estos estándares.

## ¿Por qué modelar los datos?

Las empresas tienen su propio idioma para comunicarse sobre su dominio. Los concesionarios de automóviles se ocupan de marcas, modelos y cilindros. Las aerolíneas se ocupan de los números de vuelo, la clase de servicio y las asignaciones de asientos. Algunos de estos términos son exclusivos de una empresa específica, otros se comparten entre un sector industrial y otros son compartidos por casi todas las empresas. Para términos que se comparten entre un sector vertical o incluso más amplio, puede empezar a hacer cosas útiles con los datos al nombrar y estructurar estos términos de una manera común.

Por ejemplo, muchas empresas se ocupan de pedidos. ¿Qué pasaría si, colectivamente, estas empresas decidieran modelar un pedido de manera similar? Por ejemplo, ¿qué sucede si el modelo de datos consiste en un objeto con una `priceTotal` propiedad que representaba el precio total del pedido? ¿Qué sucede si ese objeto también tiene propiedades denominadas `currencyCode` y `purchaseOrderNumber`? Tal vez el objeto order contenga una propiedad denominada `payments` sería una matriz de objetos de pago. Cada objeto representaría un pago para el pedido. Por ejemplo, quizás un cliente pagó parte del pedido con una tarjeta de regalo y el resto con una tarjeta de crédito. Puede empezar a construir un modelo con este aspecto:

```json
{
  "order": {
    "priceTotal": 89.50,
    "currencyCode": "EUR",
    "purchaseOrderNumber": "JWN20192388410012",
    "payments": [
      {
        "paymentType": "gift_card",
        "paymentAmount": 50
      },
      {
        "paymentType": "credit_card",
        "paymentAmount": 39.50
      }
    ]
  }
}
```

Si todas las empresas que tratan con pedidos decidieran modelar sus datos de pedidos de una manera consistente para términos que son comunes en la industria, cosas mágicas podrían comenzar a suceder. La información se podría intercambiar de forma más fluida dentro y fuera de su organización en lugar de interpretar y traducir constantemente los datos (props y evars, ¿alguien?). El aprendizaje automático podría comprender más fácilmente qué datos _recursos_ y proporcionan perspectivas procesables. Las interfaces de usuario para la aparición de datos relevantes podrían ser más intuitivas. Sus datos podrían integrarse perfectamente con socios y proveedores que siguen el mismo modelo.

Este es el objetivo del Adobe [Modelo de datos de experiencia](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM proporciona modelado prescriptivo para datos que son comunes en la industria, al tiempo que le permite ampliar el modelo para sus necesidades específicas. Adobe Experience Platform se basa en XDM y, como tal, los datos enviados a Experience Platform deben estar en XDM. En lugar de pensar en dónde y cómo puede transformar sus modelos de datos actuales en XDM antes de enviar los datos a Experience Platform, considere la posibilidad de adoptar XDM de forma más generalizada en toda su organización para que la traducción rara vez tenga que producirse.


>[!NOTE]
>
> Con fines de demostración, los ejercicios de esta lección crean un esquema de ejemplo para capturar el contenido visualizado y los productos comprados por los clientes en [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Aunque puede utilizar estos pasos para crear un esquema diferente para sus propios fines, se recomienda seguir primero junto con la creación del esquema de ejemplo para conocer las capacidades del editor de esquemas.

Para obtener más información sobre los esquemas XDM, siga el curso [Modelar los datos de la experiencia del cliente con XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=es) o consulte la [Información general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home).

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Creación de un esquema XDM desde la interfaz de recopilación de datos
* Adición de grupos de campos al esquema XDM
* Creación de esquemas XDM para datos de eventos web mediante prácticas recomendadas

## Requisitos previos

Todos los permisos de usuario y aprovisionamiento necesarios para la recopilación de datos y Adobe Experience Platform se describen en la [descripción general](overview.md) página.

## Creación de un esquema XDM

Los esquemas XDM son la forma estándar de describir los datos en Experience Platform, lo que permite reutilizar todos los datos que se ajustan a los esquemas en una organización sin conflictos o incluso compartirlos entre varias organizaciones. Para obtener más información, consulte la [conceptos básicos de composición de esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition).

En este ejercicio, creará un esquema XDM utilizando los grupos de campos de línea de base recomendados para capturar datos de evento web en el [Sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}:

1. Abra el [Interfaz de recopilación de datos](https://launch.adobe.com/){target="_blank"}
1. Asegúrese de que está en la zona protegida correcta. Busque la zona protegida en la esquina superior derecha

   >[!NOTE]
   >
   >Si es cliente de una aplicación basada en Platform como Real-Time CDP o Journey Optimizer, le recomendamos que utilice una zona protegida de desarrollo para este tutorial. Si no lo está, use el **[!UICONTROL Prod]** zona protegida.

1. Ir a **[!UICONTROL Esquemas]** en el panel de navegación izquierdo
1. Seleccione el **[!UICONTROL Crear esquema]** botón en la parte superior derecha

   ![Crear esquema](assets/schema-xdm-create-schema.png)
1. Seleccionar **[!UICONTROL Evento de experiencia]** en la siguiente pantalla
1. Seleccionar **[!UICONTROL Siguiente]**

   ![Evento de experiencia de esquema](assets/schema-experience-event.png)

1. Introduzca el nombre del esquema en **[!UICONTROL Nombre para mostrar del esquema]** , en este caso `Luma Web Event Data`

   >[!TIP]
   >
   >Una convención de nombres común para los esquemas XDM es asignar un nombre al esquema después del origen de los datos.


1. Seleccionar Finalizar

   ![Finalización de evento de experiencia de esquema](assets/schema-name-schema.png)

## Adición de grupos de campos

Como se ha indicado anteriormente, XDM es el marco principal que estandariza los datos de experiencia del cliente al proporcionar estructuras y definiciones comunes para su uso en servicios de Adobe Experience Platform descendentes. Al cumplir con los estándares XDM, _todos los datos de experiencia del cliente_ pueden incorporarse en una representación común. Este método le permite obtener información valiosa de las acciones de los clientes, definir las audiencias de los clientes mediante segmentos y expresar los atributos del cliente con fines de personalización mediante datos de varias fuentes. Consulte [Prácticas recomendadas para el modelado de datos](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/best-practices) para obtener más información.

Cuando sea posible, se recomienda utilizar grupos de campos existentes y adherirse a un modelo independiente del producto y a las convenciones de nomenclatura. Puede crear un grupo de campos personalizado para cualquier dato específico de su organización que no se ajuste a los grupos de campos predefinidos anteriores. Consulte [Creación de un esquema con el Editor de esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/create-schema-ui#create) para ver pasos más detallados sobre esquemas personalizados.

>[!TIP]
> 
>En este ejercicio, se agregan los grupos de campos predefinidos recomendados para la recopilación de datos web: _**[!UICONTROL ExperienceEvent del SDK web de AEP]**_ y _**[!UICONTROL Evento de experiencia del consumidor]**_.
>
>
> Si solo va a implementar **Adobe Analytics** con el SDK web y no enviar ningún dato a **Experience Platform**, use el [!UICONTROL Plantilla de Adobe Analytics ExperienceEvent] grupo de campos para definir el esquema XDM. Se utiliza en el [Análisis de configuración](setup-analytics.md) lección.

1. En el **[!UICONTROL Grupos de campos]** , seleccione **[!UICONTROL Añadir]**

   ![Nuevo grupo de campos](assets/schema-new-field-group.png)

1. Buscar por [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. Marque la casilla
1. Buscar por [!UICONTROL `Consumer Experience Event`]
1. Marque la casilla
1. Seleccionar **[!UICONTROL Adición de grupos de campos]**

   ![Agregar grupo de campos](assets/schema-add-field-group.png)

Con ambos grupos de campos, observe que tiene acceso a los pares de clave-valor más utilizados y necesarios para la recopilación de datos en la web. El [!UICONTROL nombre para mostrar] Cada uno de los campos aparece a los especialistas en marketing en la interfaz del generador de segmentos de las aplicaciones basadas en Platform y puede cambiar el nombre para mostrar de los campos estándar para adaptarlos a sus necesidades. También puede quitar los campos que no desee. Al hacer clic en cualquier nombre de grupo de campos, la interfaz resalta qué agrupaciones de pares clave-valor pertenecen a él. En el siguiente ejemplo, verá a qué campos pertenecen **[!UICONTROL Evento de experiencia del consumidor]**.

![Grupos de campos de esquema](assets/schema-consumer-experience-event.png)

Esta lección es solo un punto de partida. Al crear su propio esquema de eventos web, debe explorar y documentar los requisitos empresariales. Este proceso es similar a la creación de un [Documento de requisitos empresariales](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document) y [Referencia de diseño de solución](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr) para una implementación de Adobe Analytics, pero debe incluir requisitos para _todos los destinatarios de datos descendentes_ como destinos de plataforma, Target y reenvío de eventos.


### El objeto identityMap

Hay un campo especial utilizado para identificar a los usuarios web llamado `[!UICONTROL identityMap]`.

![Datos de evento web de Luma](assets/schema-identityMap.png)

Es un objeto que se debe tener para cualquier recopilación de datos relacionados con la web, ya que aloja el ID de Experience Cloud necesario para identificar a los usuarios en la web. También es la clave para configurar los ID de cliente internos para los usuarios autenticados. `[!UICONTROL identityMap]` se analiza más en la [Configurar identidades](configure-identities.md) lección. Se incluye automáticamente en todos los esquemas utilizando **[!UICONTROL ExperienceEvent de XDM]** clase.


>[!IMPORTANT]
>
> Es posible activar **[!UICONTROL Perfil]** para un esquema antes de guardar el esquema. **No hacer** habilitarlo en este punto. Una vez que un esquema está habilitado para el perfil, no se puede deshabilitar ni eliminar sin restablecer toda la zona protegida. Los campos no se pueden eliminar de los esquemas en este punto, aunque es posible [Campos obsoletos en la IU](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/field-deprecation-ui#deprecate). Estas implicaciones son importantes que se deben tener en cuenta más adelante cuando trabaje con sus propios datos en el entorno de producción.
>
>
>Esta configuración se analiza más en la [Experience Platform de instalación](setup-experience-platform.md) lección.
>![Esquema de perfil](assets/schema-profile.png)

Para completar esta lección, seleccione **[!UICONTROL Guardar]** en la parte superior derecha.

![Guardar esquema](assets/schema-select-save.png)


Ahora puede hacer referencia a este esquema cuando agregue la extensión del SDK web a la propiedad de etiquetas.


[Siguiente: ](configure-identities.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer el SDK web de Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en este [Entrada de discusión de la comunidad Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
