---
title: Creación de un esquema XDM para datos web
description: Obtenga información sobre cómo crear un esquema XDM para datos web en la interfaz de recopilación de datos. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK,Schemas
jira: KT-15398
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 3%

---

# Creación de un esquema XDM para datos web

Obtenga información sobre cómo crear un esquema XDM para datos web en la interfaz de recopilación de datos de Adobe Experience Platform.

Los esquemas XDM (Experience Data Model) son los componentes básicos, los principios y las prácticas recomendadas para recopilar datos en Adobe Experience Platform.

Platform Web SDK utiliza su esquema para estandarizar los datos de eventos web, enviarlos a Platform Edge Network y, finalmente, reenviar los datos a cualquier aplicación de Experience Cloud configurada en la secuencia de datos. Este paso es fundamental, ya que define un modelo de datos estándar necesario para la ingesta de datos de experiencia del cliente en Experience Platform y permite la prestación de servicios y aplicaciones descendentes basados en estos estándares.

>[!NOTE]
>
>_No se requiere_ un esquema XDM para implementar Adobe Analytics, Adobe Target o Adobe Audience Manager con Web SDK (los datos se pueden pasar en el objeto `data` en lugar del objeto `xdm`, como verá más adelante). Se requiere un esquema XDM para las implementaciones de mayor rendimiento de las aplicaciones nativas de Platform como Journey Optimizer, Real-Time Customer Data Platform y Customer Journey Analytics. Aunque puede decidir no utilizar un esquema XDM en su propia implementación, se espera que lo haga como parte de este tutorial.

## ¿Por qué modelar los datos?

Las empresas tienen su propio idioma para comunicarse sobre su dominio. Los concesionarios de automóviles se ocupan de marcas, modelos y cilindros. Las aerolíneas se ocupan de los números de vuelo, la clase de servicio y las asignaciones de asientos. Algunos de estos términos son exclusivos de una empresa específica, otros se comparten entre un sector industrial y otros son compartidos por casi todas las empresas. Para términos que se comparten entre un sector vertical o incluso más amplio, puede empezar a hacer cosas útiles con los datos al nombrar y estructurar estos términos de una manera común.

Por ejemplo, muchas empresas se ocupan de pedidos. ¿Qué pasaría si, colectivamente, estas empresas decidieran modelar un pedido de manera similar? Por ejemplo, ¿qué sucede si el modelo de datos consiste en un objeto con una propiedad `priceTotal` que representa el precio total del pedido? ¿Qué sucedería si ese objeto también tuviera las propiedades denominadas `currencyCode` y `purchaseOrderNumber`? Tal vez el objeto de pedido contenga una propiedad denominada `payments` que sería una matriz de objetos de pago. Cada objeto representaría un pago para el pedido. Por ejemplo, quizás un cliente pagó parte del pedido con una tarjeta de regalo y el resto con una tarjeta de crédito. Puede empezar a construir un modelo con este aspecto:

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

Si todas las empresas que tratan con pedidos decidieran modelar sus datos de pedidos de una manera consistente para términos que son comunes en la industria, cosas mágicas podrían comenzar a suceder. La información se podría intercambiar de forma más fluida dentro y fuera de su organización en lugar de interpretar y traducir constantemente los datos (props y evars, ¿alguien?). El aprendizaje automático podría comprender mejor lo que significan sus datos _1} y proporcionar perspectivas procesables._ Las interfaces de usuario para la aparición de datos relevantes podrían ser más intuitivas. Sus datos podrían integrarse perfectamente con socios y proveedores que siguen el mismo modelo.

Este es el objetivo de [Experience Data Model](https://business.adobe.com/products/experience-platform/experience-data-model.html) de Adobe. XDM proporciona modelado prescriptivo para datos que son comunes en la industria, al tiempo que le permite ampliar el modelo para sus necesidades específicas. Adobe Experience Platform se basa en XDM y, como tal, los datos enviados a Experience Platform deben estar en XDM. En lugar de pensar en dónde y cómo puede transformar sus modelos de datos actuales en XDM antes de enviar los datos a Experience Platform, considere la posibilidad de adoptar XDM de forma más generalizada en toda su organización para que la traducción rara vez tenga que producirse.


>[!NOTE]
>
> Con fines de demostración, los ejercicios de esta lección crean un esquema de ejemplo para capturar el contenido visualizado y los productos comprados por los clientes en el [sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Aunque puede utilizar estos pasos para crear un esquema diferente para sus propios fines, se recomienda seguir primero junto con la creación del esquema de ejemplo para conocer las capacidades del editor de esquemas.

Para obtener más información sobre los esquemas XDM, vea la lista de reproducción [Modelar los datos de la experiencia del cliente con XDM](https://experienceleague.adobe.com/en/playlists/experience-platform-model-your-customer-experience-data-with-xdm) o consulte la [descripción general del sistema XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home).

## Objetivos de aprendizaje

Al final de esta lección, debe poder:

* Creación de un esquema XDM desde la interfaz de recopilación de datos
* Adición de grupos de campos al esquema XDM
* Creación de esquemas XDM para datos de eventos web mediante prácticas recomendadas

## Requisitos previos

Todos los permisos de usuario y aprovisionamiento necesarios para la recopilación de datos y Adobe Experience Platform se describen en la página [descripción general](overview.md).

## Creación de un esquema XDM

Los esquemas XDM son la forma estándar de describir los datos en Experience Platform, lo que permite que todos los datos que se ajustan a los esquemas se reutilicen en una organización sin conflictos o incluso se compartan entre varias organizaciones. Para obtener más información, vea los [conceptos básicos de la composición de esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition).

En este ejercicio, creará un esquema XDM utilizando los grupos de campos de línea de base recomendados para capturar datos de evento web en el [sitio de demostración de Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}:

1. Abrir la [interfaz de recopilación de datos](https://experience.adobe.com/data-collection/){target="_blank"}
1. Asegúrese de que está en la zona protegida correcta. Busque la zona protegida en la esquina superior derecha

   >[!NOTE]
   >
   >Si es cliente de una aplicación basada en Platform como Real-Time CDP o Journey Optimizer, le recomendamos que utilice una zona protegida de desarrollo para este tutorial. Si no lo está, use la zona protegida **[!UICONTROL Prod]**.

1. Ir a **[!UICONTROL Esquemas]** en el panel de navegación izquierdo
1. Seleccione el botón **[!UICONTROL Crear esquema]** en la parte superior derecha

   ![Crear esquema](assets/schema-xdm-create-schema.png)
1. Seleccione **[!UICONTROL Evento de experiencia]** en la siguiente pantalla
1. Seleccionar **[!UICONTROL Siguiente]**

   ![Evento de experiencia de esquema](assets/schema-experience-event.png)

1. Escriba el nombre del esquema en el campo **[!UICONTROL Nombre para mostrar del esquema]**, en este caso `Luma Web Event Data`

   >[!TIP]
   >
   >Una convención de nombres común para los esquemas XDM es asignar un nombre al esquema después del origen de los datos.


1. Seleccionar Finalizar

   ![Finalización de evento de experiencia de esquema](assets/schema-name-schema.png)

## Adición de grupos de campos

Como se ha indicado anteriormente, XDM es el marco principal que estandariza los datos de experiencia del cliente al proporcionar estructuras y definiciones comunes para su uso en servicios de Adobe Experience Platform descendentes. Si se cumplen los estándares XDM, _todos los datos de experiencia del cliente_ se pueden incorporar en una representación común. Este método le permite obtener información valiosa de las acciones de los clientes, definir las audiencias de los clientes mediante segmentos y expresar los atributos del cliente con fines de personalización mediante datos de varias fuentes. Consulte [Prácticas recomendadas para el modelado de datos](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/best-practices) para obtener más información.

Cuando sea posible, se recomienda utilizar grupos de campos existentes y adherirse a un modelo independiente del producto y a las convenciones de nomenclatura. Puede crear un grupo de campos personalizado para cualquier dato específico de su organización que no se ajuste a los grupos de campos predefinidos anteriores. Consulte [Creación de un esquema con el Editor de esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/create-schema-ui#create) para ver los pasos más detallados sobre los esquemas personalizados.

>[!TIP]
> 
>En este ejercicio, agrega los grupos de campos predefinidos recomendados para la recopilación de datos web: _**[!UICONTROL AEP Web SDK ExperienceEvent]**_ y _**[!UICONTROL Evento de experiencia del consumidor]**_.
>


1. En la sección **[!UICONTROL Grupos de campos]**, seleccione **[!UICONTROL Agregar]**

   ![Nuevo grupo de campos](assets/schema-new-field-group.png)

1. Buscar [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. Marque la casilla
1. Buscar [!UICONTROL `Consumer Experience Event`]
1. Marque la casilla
1. Seleccionar **[!UICONTROL Agregar grupos de campos]**

   ![Agregar grupo de campos](assets/schema-add-field-group.png)

Con ambos grupos de campos, observe que tiene acceso a los pares de clave-valor más utilizados y necesarios para la recopilación de datos en la web. El [!UICONTROL nombre para mostrar] de cada campo aparece a los especialistas en mercadotecnia en la interfaz del generador de segmentos de las aplicaciones basadas en Platform y puede cambiar el nombre para mostrar de los campos estándar para adaptarlos a sus necesidades. También puede quitar los campos que no desee. Al hacer clic en cualquier nombre de grupo de campos, la interfaz resalta qué agrupaciones de pares clave-valor pertenecen a él. En el ejemplo siguiente, verá qué campos pertenecen a **[!UICONTROL Evento de experiencia del consumidor]**.

![Grupos de campos de esquema](assets/schema-consumer-experience-event.png)

Esta lección es solo un punto de partida. Al crear su propio esquema de eventos web, debe explorar y documentar los requisitos empresariales. Este proceso es similar a la creación de un [Documento de requisitos empresariales](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document) y una [Referencia de diseño de la solución](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr) para una implementación de Adobe Analytics, pero debe incluir requisitos para _todos los destinatarios de datos descendentes_, como destinos de plataforma, destino y reenvío de eventos.


### El objeto identityMap

Hay un campo especial usado para identificar usuarios web llamado `[!UICONTROL identityMap]`.

![Datos de evento web de Luma](assets/schema-identityMap.png)

Es un objeto que se debe tener para cualquier recopilación de datos relacionados con la web, ya que aloja el Experience Cloud ID necesario para identificar a los usuarios en la web. También es la clave para configurar los ID de cliente internos para los usuarios autenticados. `[!UICONTROL identityMap]` se analiza más en la lección [Configurar identidades](configure-identities.md). Se incluye automáticamente en todos los esquemas utilizando la clase **[!UICONTROL XDM ExperienceEvent]**.


>[!IMPORTANT]
>
> Es posible habilitar **[!UICONTROL Profile]** para un esquema antes de guardar el esquema. **No lo** habilite en este momento. Una vez que un esquema está habilitado para el perfil, no se puede deshabilitar ni eliminar sin restablecer toda la zona protegida. Los campos tampoco se pueden eliminar de los esquemas en este momento, aunque es posible [eliminar los campos obsoletos en la interfaz de usuario](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/field-deprecation-ui#deprecate). Estas implicaciones son importantes que se deben tener en cuenta más adelante cuando trabaje con sus propios datos en el entorno de producción.
>
>
>Esta configuración se analiza más en la lección [Configuración de Experience Platform](setup-experience-platform.md).
>![Esquema de perfil ](assets/schema-profile.png)

Para completar esta lección, selecciona **[!UICONTROL Guardar]** en la parte superior derecha.

![Guardar esquema](assets/schema-select-save.png)


Ahora puede hacer referencia a este esquema cuando agregue la extensión Web SDK a la propiedad de etiquetas.


[Siguiente: ](configure-identities.md)

>[!NOTE]
>
>Gracias por dedicar su tiempo a conocer Adobe Experience Platform Web SDK. Si tiene preguntas, desea compartir comentarios generales o tiene sugerencias sobre contenido futuro, compártalas en esta [publicación de debate de la comunidad de Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
