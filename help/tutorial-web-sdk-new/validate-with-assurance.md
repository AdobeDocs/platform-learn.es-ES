---
title: Validación de implementaciones de SDK web con Experience Platform Assurance
description: Obtenga información sobre cómo validar la implementación del SDK web de Platform con Adobe Experience Platform Assurance. Esta lección forma parte del tutorial Implementación de Adobe Experience Cloud con SDK web.
feature: Web SDK,Tags,Assurance
source-git-commit: 4361d8e688ff2c2f3b5472f2cfff246efa627c7f
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# Validación de implementaciones de SDK web con Experience Platform Assurance


## Iniciar una sesión de Assurance

Adobe Experience Platform Assurance es un producto de Adobe Experience Cloud que le ayuda a inspeccionar, probar, simular y validar cómo recopilar datos o servir experiencias.

Más información sobre [Garantía de Adobe](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).

Cada vez que se habilita el seguimiento de Edge, se inicia una sesión de Assurance en segundo plano.

Para ver la sesión de Assurance,

1. Con el seguimiento de Edge habilitado, puede ver un icono de vínculo de salida en la parte superior. Seleccione el icono para abrir Assurance. Se abre una nueva pestaña en el explorador.

   ![Iniciar sesión de Assurance](assets/validate-debugger-start-assurnance.png)

1. Seleccione la fila con el evento llamado Controlador de respuesta de Adobe.
1. A la derecha aparece un menú. Seleccione el `+` firmar junto a `[!UICONTROL ACPExtensionEvent]`
1. Explorar en profundidad seleccionando `[!UICONTROL payload > 0 > payload > 0 > namespace]`. El ID mostrado en la última `0` corresponde al `ECID`. Lo sabe por el valor que aparece debajo de `namespace` concordancia `ECID`

   ![Validación de ECID de Assurance](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Es posible que vea un valor ECID truncado debido al ancho de la ventana. Simplemente, seleccione la barra de control en la interfaz y arrastre a la izquierda para ver todo el ECID.

En lecciones futuras, utilice Assurance para validar cargas útiles completamente procesadas que lleguen a una aplicación de Adobe habilitada en el conjunto de datos.

Ahora que un objeto XDM se activa en una página y con los conocimientos necesarios para validar la recopilación de datos, ya puede configurar las aplicaciones de Adobe individuales mediante el SDK web de Platform.