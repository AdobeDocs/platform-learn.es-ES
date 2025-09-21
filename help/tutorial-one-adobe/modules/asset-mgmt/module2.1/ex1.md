---
title: Cree su programa de Cloud Manager
description: Cree su programa de Cloud Manager
kt: 5342
doc-type: tutorial
exl-id: fda247eb-1865-4936-b46e-84128ccab357
source-git-commit: 490bc79332bb84520ba084ec784ea3ef48a68fb5
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 3%

---

# 1.1.1 Creación de su programa de Cloud Manager

Vaya a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. La organización que debe seleccionar es `--aepImsOrgName--`. Entonces verás algo como esto. Haga clic en **Agregar programa**.

![AEMCS](./images/aemcs1.png)

Para el **Nombre de programa**, use `--aepUserLdap-- - CitiSignal AEM+ACCS`. Seleccione la opción **Configurar una zona protegida**. Haga clic en **Continuar**.

![AEMCS](./images/aemcs2.png)

Asegúrese de que las siguientes opciones están seleccionadas:

- Sitios
- Formularios
- Recursos

Haga clic en la flecha de **Assets** para abrir la lista de opciones.

![AEMCS](./images/aemcs3.png)

Asegúrese de que las siguientes opciones están seleccionadas:

- Content Hub

Desplazarse hacia abajo en la lista.

![AEMCS](./images/aemcs3a.png)

Asegúrese de que las siguientes opciones están seleccionadas:

- Edge Delivery Services
- Medios dinámicos

Haga clic en **Crear**.

![AEMCS](./images/aemcs3b.png)

La creación del entorno tardará un poco, de 10 a 20 minutos.

![AEMCS](./images/aemcs4.png)

Una vez creados los entornos y listos para usarlos, recibirá una confirmación por correo electrónico tras la cual puede volver aquí.

![AEMCS](./images/aemcs5.png)

Una vez que hayas recibido tu confirmación por correo electrónico, vuelve a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Verá que el estado del programa ha cambiado a **Listo**. Haga clic en el programa para abrirlo.

![AEMCS](./images/aemcs6.png)

Eche un vistazo a la pestaña **Canalizaciones**. Haga clic en los 3 puntos **...** y luego haga clic en **Ejecutar**.

![AEMCS](./images/aemcs7.png)

Haga clic en **Ejecutar**.

![AEMCS](./images/aemcs8.png)

A continuación, haga clic en los 3 puntos **...** en la ficha **Entornos** y haga clic en **Ver detalles**.

![AEMCS](./images/aemcs9.png)

A continuación, verá los detalles del entorno, incluida la dirección URL del entorno **Author**, que necesitará en el siguiente ejercicio.

Eche un vistazo a la línea **Content Hub** y seleccione **Haga clic para activar**.

![AEMCS](./images/aemcs10.png)

Haga clic en **Activar**.

![AEMCS](./images/aemcsact1.png)

La activación de **Content Hub** se ha iniciado. Esto puede tardar 10 minutos o más.

![AEMCS](./images/aemcsact2.png)

Después de unos 10 minutos, se activará **Content Hub**.
A continuación, observe la línea **Dynamic Media** y seleccione **Haga clic para activar**.

![AEMCS](./images/aemcsact3.png)

Haga clic en **Activar**.

![AEMCS](./images/aemcsact4.png)

Se ha iniciado la activación de **Dynamic Media**. Esto puede tardar 10 minutos o más.

![AEMCS](./images/aemcsact5.png)

Después de unos 10 minutos, se activará **Dynamic Media**.

![AEMCS](./images/aemcsact6.png)

Una vez finalizada la ejecución de la canalización, puede continuar con el siguiente ejercicio.

Siguiente paso: [Configurar el entorno de AEM CS](./ex3.md){target="_blank"}

Volver a [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Volver a todos los módulos](./../../../overview.md){target="_blank"}
