---
title: 'Servicios inteligentes: inteligencia artificial aplicada al cliente Crear una nueva instancia (configurar)'
description: 'AI del cliente: crear una nueva instancia (configurar)'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 3%

---

# 2.2.2 Inteligencia artificial aplicada al cliente: crear una nueva instancia (configurar)

La inteligencia artificial aplicada al cliente funciona analizando los datos de evento de experiencia del consumidor existentes para predecir puntuaciones de pérdida o tendencia de conversión. La creación de una nueva instancia de inteligencia artificial aplicada al cliente permite a los especialistas en marketing definir objetivos y medidas.

## 2.2.2.1 Configuración de una nueva instancia de inteligencia artificial aplicada al cliente

En Adobe Experience Platform, haga clic en **Servicios** en el menú de la izquierda. Aparece el explorador **Services** y muestra todos los servicios disponibles a su disposición. En la tarjeta de inteligencia artificial aplicada al cliente, haga clic en **Abrir**.

![Navegación de servicio](./images/navigatetoservice.png)

Haga clic en **Crear instancia**.

![Crear nueva instancia](./images/createnewinstance.png)

Entonces verá esto...

![Crear nueva instancia](./images/custai1.png)

Introduzca los detalles necesarios para la instancia de inteligencia artificial aplicada al cliente:

- Nombre: use `--aepUserLdap-- Product Purchase Propensity`
- Descripción: uso: **Predecir la probabilidad de que los clientes compren un producto**
- Tipo de tendencia: seleccionar **Conversión**

![Página de instalación 1](./images/setuppage1.png)

Haga clic en **Next**.

![Página de instalación 1](./images/next.png)

Entonces verá esto... Seleccione el conjunto de datos que creó en el ejercicio anterior, que se llama `--demoProfileLdap - Demo System - Customer Experience Event Dataset`. Haga clic en **Next**.

![Página de instalación 1](./images/custai2.png)

Seleccione **Se producirá** y defina el campo **commerce.purchases.value** como la variable de destino.

![Definir meta de CAI](./images/caidefinegoal.png)

Haga clic en **Next**.

![Página de instalación 1](./images/next.png)

A continuación, configure la programación para que se ejecute **Semanalmente** y establezca la hora lo más cerca posible de la hora actual. Asegúrese de que la opción **Habilitar puntuaciones para el perfil** esté habilitada.

![Definir avance de CAI](./images/caiadvancepage.png)

Haga clic en **Finalizar**.

![Página de instalación 1](./images/finish.png)

Entonces verá esta ventana emergente. Haga clic en **Aceptar**.

![Página de instalación 1](./images/finish1.png)

Después de configurar la instancia, puede verla en la lista de instancias de inteligencia artificial aplicada al cliente y también obtener una vista previa del resumen de los detalles de configuración y ejecución haciendo clic en la fila de instancias de inteligencia artificial aplicada al cliente. El panel de resumen también mostrará los detalles del error en caso de que se encuentren errores.

![Resumen de configuración de instancia](./images/caiinstancesummary.png)

>[!NOTE]
>
>Puede modificar cualquier definición o atributo siempre que el estado de la instancia de inteligencia artificial aplicada al cliente sea **Esperando formación** o **Error**

Siguiente paso: [2.2.3 inteligencia artificial aplicada al cliente - Tablero de puntuación y segmentación (predecir y tomar medidas)](./ex3.md)

[Volver al módulo 2.2](./intelligent-services.md)

[Volver a todos los módulos](./../../../overview.md)
