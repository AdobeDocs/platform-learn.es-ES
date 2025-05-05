---
title: Validación y solución de problemas de la implementación de la extensión Decisioning
description: Obtenga información sobre cómo validar y solucionar problemas de una implementación móvil de Adobe Target con la extensión Decisioning.
exl-id: edc6e25a-58d7-4145-97c3-bf48e980914f
source-git-commit: a4fe85580776e5d84f6deaf3c0224f0513ba8415
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Validación y solución de problemas de la implementación de la extensión Decisioning

Después de migrar la implementación de Target de la extensión de Target a la extensión de Decisioning, es importante validar que todo funciona correctamente antes de publicar los cambios en la aplicación de producción. Adobe recomienda lo siguiente, que se trata en detalle en esta página:

* Realice una validación técnica para asegurarse de que la implementación básica y las solicitudes y respuestas de Platform Mobile SDK tengan el aspecto correcto
* Asegúrese de que las actividades de Target se entreguen y representen correctamente
* Compruebe que la creación de informes funciona correctamente
* Vuelva a visitar las audiencias y los scripts de perfil para asegurarse de que son compatibles con Platform Mobile SDK y la extensión Optimizer
* Asegúrese de que las integraciones con Adobe o aplicaciones de terceros funcionan correctamente

Cada implementación de Target es diferente según la arquitectura y las funciones del sitio utilizadas. Puede utilizar las tablas siguientes como punto de partida y añadir cualquier elemento exclusivo a la implementación.

## Validación técnica y solución de problemas

La validación técnica y la resolución de problemas con Platform Mobile SDK y la extensión Decisioning se mejoran considerablemente con Assurance. Consulte las siguientes páginas de documentación para obtener más información sobre esta herramienta esencial:

* [Configuración de complementos de Decisioning en Assurance](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/assurance-setup/){target=_blank}

* [Validando la configuración de optimización de SDK](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/optimize-configuration-view/){target=_blank}

* [Revisar solicitudes y simular diferentes experiencias](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/review-simulate/){target=_blank}

Después de realizar los pasos de validación anteriores, puede estar seguro de que la implementación de Platform Mobile SDK con la extensión Decisioning está lista para pasar a producción.

¡Felicidades, ha llegado al final del tutorial! ¡Buena suerte al migrar su implementación de Adobe Target a la extensión de Decisioning!

>[!NOTE]
>
>Nos comprometemos a ayudarle a tener éxito con su migración de Target móvil de la extensión de Target a la extensión de Decisioning. Si encuentra obstáculos con la migración o cree que falta información esencial en esta guía, comuníquenoslo publicando en [esta discusión de la comunidad](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=es#M463).
