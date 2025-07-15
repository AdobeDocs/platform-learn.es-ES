---
title: Comparación de la extensión de Target con la extensión de Offer Decisioning y Target
description: Obtenga información sobre las diferencias entre la extensión de Target y la extensión de Offer Decisioning y Target, incluidas las funciones, la configuración y el flujo de datos.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 3%

---

# Comparación de la extensión de Target con la extensión de Offer Decisioning y Target

La extensión de Offer Decisioning y Target difiere de la extensión de Adobe Target para aplicaciones móviles. Las siguientes tablas son una referencia para ayudarle a evaluar las áreas de la implementación en las que puede que tenga que centrarse durante el proceso de migración.

Después de revisar la información siguiente y evaluar la implementación técnica actual de la extensión de Target, debería poder comprender lo siguiente:

- Qué funciones de Target son compatibles con Offer Decisioning y Target
- Qué funciones de extensión de Adobe Target tienen equivalentes de Offer Decisioning y Target
- Aplicación de la configuración de Target con Offer Decisioning y Target
- Flujo de datos con la extensión Offer Decisioning y Target

## Diferencias operativas

| | Extensión de Target | Extensión de Offer Decisioning y Target |
|---|---|---|
| Proceso | Los cambios en una implementación de Target pueden seguir un proceso que tenga una cadencia o requisitos de control de calidad diferentes a los de otras aplicaciones, como Analytics. | Los cambios en una implementación de extensión de Offer Decisioning y Target deben tener en cuenta todas las aplicaciones de flujo descendente, y el control de calidad y el proceso de publicación deben ajustarse en consecuencia. |
| Colaboración | Los datos específicos de Target se pueden pasar directamente en las llamadas de Target. Si la fuente de informes de Target es Adobe Analytics (A4T), los datos específicos de Target también se pueden pasar a Adobe Analytics cuando se soliciten los métodos de seguimiento adecuados en la extensión de Target para visualizar el contenido de Target e interactuar con él. | Los datos pasados en las llamadas de extensión de Offer Decisioning y Target se pueden reenviar tanto a Target como a Analytics si la fuente de informes de Target es Adobe Analytics (A4T), Adobe Analytics está habilitado en el flujo de datos y se llama a los métodos de seguimiento adecuados en Offer Decisioning y en la extensión de Target cuando se muestra contenido de Target y se interactúa con él. |

## Diferencias básicas

| | Extensión de Target | Extensión de Offer Decisioning y Target |
|---|---|---|
| Dependencias | Solo depende de Mobile Core SDK | Depende de Mobile Core y Edge Network SDK |
| Funcionalidad de biblioteca | Admite recuperar contenido solo de Adobe Target | Compatibilidad con la recuperación de contenido desde Adobe Target y Offer Decisioning |
| Solicitudes | Las llamadas de Target son en gran medida independientes de otras llamadas de red | Las llamadas de red de Target se ponen en cola junto con las llamadas de red para otras soluciones basadas en Edge, como Mensajería en Edge SDK, y se ejecutan en serie. |
| Edge Network | Utiliza el valor del servidor de Target para el Edge Network de Adobe Experience Cloud con el código de cliente (clientcode.tt.omtrdc.net), ambos especificados en la [configuración de Target](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) en la IU de recopilación de datos | Utiliza el dominio de red de Edge especificado en Adobe Experience Platform [Configuración de Edge Network](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui) en la IU de recopilación de datos. |
| Terminología básica | mbox, TargetParameters | DecisionScope, Map (Android)/dictionary (iOS) para parámetros de Target |
| Contenido predeterminado | Permite pasar contenido predeterminado del lado del cliente en TargetRequest, que se devuelve si la llamada de red falla o genera un error. | No permite pasar contenido predeterminado del lado del cliente. No devuelve ningún contenido si la llamada de red falla o genera un error. |
| Parámetros de destino | Permite pasar TargetParameters globales por solicitud y diferentes TargetParameters por mbox | Permite pasar TargetParameters globales solo por solicitud |



## Comparación de características

| Función | Extensión de Target | Extensión de Offer Decisioning y Target (Target a través de Edge) |
|---|---|---|
| Modo de recuperación previa | Admitido | Admitido |
| Modo de ejecución | Admitido | No compatible |
| Parámetros personalizados | Admitido | Compatible* |
| Parámetros de perfil | Admitido | Compatible* |
| Parámetros de entidad | Admitido | Compatible* |
| Públicos destinatarios | Admitido | Admitido |
| Audiencias de Real-Time CDP | No compatible | Admitido |
| Atributos de Real-Time CDP | No compatible | Admitido |
| Métricas del ciclo vital | Admitido | Compatible mediante reglas de recopilación de datos |
| thirdPartyId (mbox3rdPartyId) | Admitido | Compatible mediante mapa de identidad y área de nombres de ID de terceros de Target en el conjunto de datos |
| Notificaciones (mostrar, hacer clic) | Admitido | Admitido |
| Tokens de respuesta | Admitido | Admitido |
| Vistas previas móviles (modo de control de calidad) | Admitido | Compatibilidad limitada con Assurance |

>[!IMPORTANT]
>
> \* Los parámetros enviados en una solicitud se aplican a todos los ámbitos de la solicitud. Si necesita establecer parámetros diferentes para ámbitos diferentes, debe realizar solicitudes adicionales.



## Llamadas dignas de mención

>[!NOTE]
>
>Mantenga la configuración y los ajustes de Etiquetas de extensión de Target en su lugar incluso después de haber migrado el código de la aplicación a la extensión de Offer Decisioning y Target. Esto garantizará que Target siga funcionando para los clientes que aún no han actualizado la aplicación a la nueva versión.
>
>Si utiliza la integración de Analytics para Target (A4T), asegúrese de migrar también su implementación de Analytics con la extensión Bridge de Edge al mismo tiempo que migra la implementación de Target a la extensión Offer Decisioning y Target.





>[!IMPORTANT]
>
> Mantenga la configuración de la extensión de Target en su lugar incluso después de haber migrado el código de la aplicación a la extensión de Offer Decisioning y Target. Esto garantizará que Target siga funcionando para los usuarios que aún no han actualizado su aplicación.

## Diagrama del sistema de las extensiones Offer Decisioning y Target

El diagrama siguiente debería ayudarle a comprender el flujo de datos mediante la extensión de Offer Decisioning y Target.

![Adobe Target Edge Decisioning con SDK móvil del lado del cliente](assets/diagram.png)


>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Offer Decisioning y Target. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625).
