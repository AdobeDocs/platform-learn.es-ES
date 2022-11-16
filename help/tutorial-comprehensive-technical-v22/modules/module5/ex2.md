---
title: 'Servicios inteligentes: Customer AI Create a New Instance (Configure)'
description: 'AI del cliente: crear una nueva instancia (configurar)'
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: d9377c97-efed-427a-a063-aa9c6bd1a78a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 3%

---

# 5.2 Customer AI: crear una nueva instancia (configurar)

La AI del cliente funciona analizando los datos existentes de Evento de la experiencia del consumidor para predecir las puntuaciones de tendencia de pérdida o conversión. La creación de una nueva instancia de Customer AI permite a los especialistas en marketing definir objetivos y medidas.

## 5.2.1 Configuración de una nueva instancia de Customer AI

En Adobe Experience Platform, haga clic en **Servicios** en el menú de la izquierda. La variable **Servicios** aparece y muestra todos los servicios disponibles a su disposición. En la tarjeta de Customer AI, haga clic en **Apertura**.

![Navegación de servicio](./images/navigatetoservice.png)

Haga clic en **Crear instancia**.

![Crear nueva instancia](./images/createnewinstance.png)

Entonces verás esto.

![Crear nueva instancia](./images/custai1.png)

Introduzca los detalles necesarios para la instancia de Customer AI:

- Nombre: use `--demoProfileLdap-- Product Purchase Propensity`
- Descripción: use: **Predecir la probabilidad de que los clientes compren un producto**
- Tipo de propensión: select **Conversión**

![Configuración de la página 1](./images/setuppage1.png)

Haga clic en **Siguiente**.

![Configuración de la página 1](./images/next.png)

Entonces verás esto. Seleccione el conjunto de datos creado en el ejercicio anterior al que se le asigna un nombre `--demoProfileLdap - Demo System - Customer Experience Event Dataset`. Haga clic en **Siguiente**.

![Configuración de la página 1](./images/custai2.png)

Select **Ocurrirá** y definir el campo **commerce.purchases.value** como variable de destino.

![Definición del objetivo de la CAI](./images/caidefinegoal.png)

Haga clic en **Siguiente**.

![Configuración de la página 1](./images/next.png)

A continuación, configure la programación para que se ejecute **Semanal** y establezca la hora lo más cerca posible de la hora actual. Asegúrese de que la opción **Habilitar puntuaciones para perfil** está activada.

![Definir el adelanto de la CAI](./images/caiadvancepage.png)

Haga clic en **Finalizar**.

![Configuración de la página 1](./images/finish.png)

Verá esta ventana emergente. Haga clic en **Aceptar**.

![Configuración de la página 1](./images/finish1.png)

Después de configurar la instancia, puede verla en la lista de instancias de Customer AI y también obtener una vista previa del resumen de los detalles de configuración y ejecución haciendo clic en la fila de instancias de Customer AI . El panel de resumen también muestra los detalles del error en caso de que se hayan encontrado errores.

![Resumen de configuración de instancias](./images/caiinstancesummary.png)

>[!NOTE]
>
>Puede modificar cualquier definición o atributo siempre que el estado de la instancia de Customer AI sea **Esperando formación** o **Error**

Paso siguiente: [5.3 AI del cliente: panel de puntuación y segmentación (Predecir y tomar medidas)](./ex3.md)

[Volver al módulo 5](./intelligent-services.md)

[Volver a todos los módulos](./../../overview.md)
