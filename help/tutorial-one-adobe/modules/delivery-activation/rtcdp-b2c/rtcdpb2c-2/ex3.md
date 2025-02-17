---
title: 'Inteligencia artificial aplicada al cliente: panel de puntuación y segmentación (predecir y realizar acciones)'
description: 'Inteligencia artificial aplicada al cliente: panel de puntuación y segmentación (predecir y realizar acciones)'
kt: 5342
doc-type: tutorial
exl-id: a6df3ff1-f907-4185-8189-f0b39c67c943
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 1%

---

# 2.2.3 Inteligencia artificial aplicada al cliente: panel de puntuación y segmentación (predecir y actuar)

Una vez que la instancia de inteligencia artificial aplicada al cliente complete la ejecución de un modelo, le permitirá visualizar la puntuación de tendencia que se evalúa para predecir que un cliente realizará una compra en los próximos 30 días.

![IA](./images/caiinstancesummary1.png)

>[!NOTE]
>
>Solo una instancia de inteligencia artificial aplicada al cliente con un estado de **Éxito** le permitirá obtener una vista previa de las perspectivas del servicio.

## Predicción de tendencia

Ahora vamos a revisar la tendencia predicha generada por el modelo de instancia de inteligencia artificial aplicada al cliente. Haga clic en el nombre de la instancia para ver el panel.

![IA](./images/caimodels1.png)

El panel de inteligencia artificial aplicada al cliente muestra el resumen sobre la puntuación, la distribución de la población y los factores influyentes para que el modelo se evalúe.

![Descripción de IA](./images/caidescription.png)

Pase el ratón sobre los factores influyentes para ver el desglose adicional de la distribución de datos.

![Factores de influencia](./images/caiinfluencefactors.png)

## Acciones comerciales

### Segmentación de clientes

El panel de inteligencia artificial aplicada al cliente permite definir segmentos con un solo clic. Haga clic en el botón **Crear segmento** de las tarjetas de tendencia.

![Crear un segmento](./images/caiinfluencefactors1.png)

Verá que se crea una definición de segmento automáticamente.

![Regla de segmento](./images/caicreatesegment.png)

Asigne un nombre al segmento, siguiendo esta convención de nombres: `--aepUserLdap-- - Customer AI High Propensity`. Haga clic en **Publicar**.

![Regla de segmento](./images/caicreatesegment1.png)

Ahora puede utilizar este segmento para la segmentación mediante, por ejemplo, Real-time CDP, Journey Optimizer y Adobe Target.

## Cleanup

Para asegurarse de que no se conserven datos de demostración innecesarios en su entorno, asegúrese de eliminar el conjunto de datos `--aepUserLdap-- - Demo System - Customer Experience Event Dataset` una vez que haya completado correctamente este ejercicio. Si no elimina los datos de demostración, su instancia de AEP tendrá un impacto en los costes.

![Perfil](./images/cleanup.png)

## Pasos siguientes

Ir a [Resumen y beneficios](./summary.md){target="_blank"}

Volver a [Servicios inteligentes](./intelligent-services.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
