---
title: Introducción | Migración de Target de at.js 2.x al SDK web
description: Obtenga información sobre cómo migrar una implementación de Adobe Target de at.js 2.x al SDK web de Adobe Experience Platform. Los temas incluyen la carga de la biblioteca JavaScript, el envío de parámetros, el procesamiento de actividades y otras llamadas importantes.
recommendations: catalog,noDisplay
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Migración de Target de at.js 2.x al SDK web de plataforma

Esta guía está dirigida a los implementadores experimentados de Adobe Target para que aprendan a migrar una implementación at.js al SDK web de Adobe Experience Platform.

Adobe Experience Platform Web SDK es una biblioteca JavaScript del lado del cliente que permite a los clientes de Adobe Experience Cloud interactuar con los servicios de Experience Cloud a través de Adobe Experience Platform Edge Network. Esta nueva biblioteca combina las funciones de las bibliotecas de aplicaciones de Adobe independientes en un único paquete ligero que puede aprovechar al máximo las nuevas funciones de Adobe Experience Platform.

## Ventajas principales

Algunas de las ventajas del SDK web de Platform comparado con la biblioteca independiente at.js son:

* Uso compartido más rápido de audiencias desde [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=es)
* Integración de Target con Journey Optimizer para admitir [entrega de offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Capacidad de uso [id de origen](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html?lang=es) para generar el ECID para la identificación de visitantes de larga duración
* Consolidación de llamadas de red entre aplicaciones de Adobe
* Un espacio más pequeño para métricas de velocidad de página mejoradas
* Una integración más estricta con Adobe Analytics que no depende de la vinculación de información desde llamadas de red independientes
* Flexibilidad de implementación adicional para los desarrolladores

Podría decirse que la mayor ventaja de la migración es para los clientes de Real-time Customer Data Platform. Real-Time CDP ofrece tremendas funciones de creación de audiencias basadas en la amplia gama de datos introducidos en el Experience Platform y su función Perfil del cliente en tiempo real. Un marco de control de datos integrado automatiza el uso responsable de esos datos. Customer AI permite utilizar fácilmente modelos de aprendizaje automático para construir modelos de inclinación y pérdida cuya salida se puede compartir con Adobe Target. Por último, los clientes de los complementos opcionales de Healthcare y Privacy &amp; Security Shield pueden utilizar la función de cumplimiento de consentimiento para aplicar fácilmente las preferencias de consentimiento de los clientes. El SDK web de plataforma es un requisito para utilizar estas funciones RTCDP en su canal web.

## Objetivos de aprendizaje

Al final de este tutorial, debería saber cómo:

* Comprender las diferencias de implementación de Target entre at.js y el SDK web de plataforma
* Configuración de la configuración inicial para la funcionalidad de Target
* Actualización de la biblioteca at.js al SDK web de Platform
* Procesar actividades del compositor de experiencias visuales y basadas en formularios
* Pasar parámetros a Target
* Seguimiento de eventos de conversión
* Habilitar compatibilidad con dominios cruzados
* Actualización de audiencias y scripts de perfil
* Validar la implementación
* Depuración de la entrega de experiencias de Target


## Requisitos previos

Para completar este tutorial, primero debe:

* Tenga una comprensión técnica de la implementación actual de Target at.js
* Asegúrese de que dispone de un [Función Editor o Editor](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) para su instancia de Target , de modo que pueda intentar crear ejemplos por su cuenta
* Instale el [Extensión del explorador del Asistente de edición visual de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) para Google Chrome
* Obtenga información sobre cómo configurar actividades en Adobe Target. Si necesita un actualizador, los siguientes tutoriales y guías son útiles para esta lección:
   * [Usar el Compositor de experiencias visuales](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Uso del Compositor de experiencias basadas en formularios](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Crear actividades de segmentación de experiencias](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

Una vez que esté listo, el primer paso para una migración correcta es [obtenga información sobre el proceso de migración](migration-overview.md) y en qué se diferencian at.js y el SDK web de plataforma .

>[!NOTE]
>
>Estamos comprometidos a ayudarle a llevar a cabo correctamente la migración de Target de at.js al SDK web. Si encuentra obstáculos con su migración o cree que falta información crítica en esta guía, indíquenoslo publicando en [esta discusión comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).