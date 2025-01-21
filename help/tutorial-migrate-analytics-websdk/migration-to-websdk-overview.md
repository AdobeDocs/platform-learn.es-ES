---
title: Migración de Adobe Analytics a Web SDK mediante etiquetas
description: Conozca los pasos que seguirá durante la migración a Web SDK, así como las decisiones que deberá tomar en el proceso.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16755
exl-id: e578b669-42b4-46ae-b6e6-6688e5c5c772
source-git-commit: 7c0a6c769d56b3e56a5667d5aeff47b55ab6dc33
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 0%

---

# Migración de Adobe Analytics a Web SDK mediante etiquetas

Conozca los pasos para migrar una implementación de Adobe Analytics con la extensión Analytics en Experience Platform Tags (anteriormente conocida como Launch) a Web SDK, utilizando la extensión Web SDK también en Etiquetas. Cuando se utiliza la extensión Adobe Analytics en Etiquetas, se utiliza el código &quot;AppMeasurement.js&quot; entre bastidores. Por lo tanto, puede considerar esto como un tutorial que migra el AppMeasurement a Web SDK, pero este tutorial está completamente en Etiquetas y NO cubre el paso a o desde una implementación de JavaScript (con la excepción del código JavaScript que se utiliza en la IU de Etiquetas). Para migrar implementaciones de JavaScript, consulte la [documentación](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk).

## Qué obtendrá de este tutorial

Antes de pasar a los pasos para migrar su implementación de Analytics, es importante que entienda exactamente lo que estará haciendo, que está cambiando/actualizando la _implementación_ para Analytics. Al final de este tutorial, cuando vaya a los informes y todo sea igual, podría preguntarse: &quot;Ahora, ¿por qué he hecho todo eso?&quot; Existen otros documentos para describir las ventajas de utilizar Web SDK para la implementación de Analytics, pero algunos son:

1. Compatibilidad con ID de dispositivo de origen
1. Mejor rendimiento
1. Futuro de la implementación a medida que avanza hacia el uso de las aplicaciones de Adobe Experience Platform (habilitando nuevos casos de uso).

Hable con su representante de Adobe Analytics para obtener más información sobre cómo Web SDK puede ayudarle. A medida que avancemos con este tutorial, nos centraremos en _cómo_ hacer la migración.

>[!IMPORTANT]
>
>Es importante tener en cuenta que una de las principales razones por las que está realizando esta migración de la implementación es para prepararse para utilizar aplicaciones de Adobe Experience Platform, como Customer Journey Analytics, Real-Time CDP o Journey Optimizer (como se ha indicado anteriormente en #3 ). El uso de los datos del sitio web para este fin incluirá pasos adicionales que no se incluyen en este tutorial, pero este tutorial será sin duda un requisito previo para que progrese aún más su implementación. Por lo tanto, complete este tutorial y, a continuación, puede continuar para realizar los pasos necesarios para enviar estos mismos datos del sitio web al Experience Platform.

## Método de migración

Probablemente haya muchas maneras de realizar este proceso de migración, pero tenemos que hablar de dos aquí:

**Método 1:** Actualice la propiedad Tags existente a Web SDK, creando nuevos elementos de datos y realizando cambios en las reglas que ya existen en su propiedad.

**Método 2:** También puede crear una nueva propiedad (copiando la existente o creando una completamente nueva) y, a continuación, configurar esa nueva propiedad con Web SDK en lugar de con la extensión de Adobe Analytics.

**Para este tutorial de migración, vamos a usar el Método 1.** De esta forma, los códigos incrustados asociados con la propiedad ya están incrustados en los sitios de desarrollo, ensayo y producción, por lo que no será necesario cambiar ningún código incrustado. Si decide seguir con el método 2, no olvide obtener los nuevos códigos incrustados para cada entorno desde la sección **Entornos** de la nueva propiedad y colóquelos en la sección de encabezado del sitio.

>[!NOTE]
>
>Aunque vamos a editar nuestra propiedad existente en Etiquetas durante esta migración, es aconsejable tener cuidado. Por lo tanto, se recomienda encarecidamente que realice una copia de la propiedad actual antes de iniciar la migración. De ese modo, siempre puede entrar en la copia y ver cómo estaban las cosas antes de cambiarlas, extraer código de ella, etc.
>Es bueno tener cuidado, por si acaso. Vaya y haga la copia de su propiedad. Voy a esperar aquí hasta que vuelvas.

## Pasos para migrar la implementación de Analytics a Web SDK

A medida que avanza por los pasos, hay un par de advertencias que son importantes de entender:

1. En primer lugar, puede que necesite o no todos estos pasos. Por ejemplo, hay una lección sobre la migración de código personalizado. Si tiene una implementación de etiquetas que no utiliza código personalizado (incluido el uso de complementos), no necesitará esta lección. Intentamos incluir las lecciones que la mayoría de la gente necesitaría, así que al menos lea las lecciones para ver si necesita hacer ajustes en su sitio durante la migración.
1. Además, no hay forma de crear un tutorial de migración que cubra el 100 % de los casos de uso que todos utilizan. Como se indica en el elemento anterior, hemos intentado incluir las lecciones que la mayoría de las personas necesitarán y que abarcarán la mayoría de los casos de uso principales. Sin embargo, no cabe duda de que habrá casos de uso que no se tratan en este tutorial. En este caso, compruebe si las lecciones incluidas le dan una buena idea de cómo debe migrar para su caso de uso. También puede pedir a sus colegas de la [Comunidad de Experience League que recopilen datos](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/ct-p/adobe-launch-community).

El proceso de migración incluye los siguientes pasos clave:

1. Cree un grupo de informes de validación de migración.
1. Cree y configure una secuencia de datos.
1. Añada y configure la extensión Web SDK en Etiquetas (anteriormente, Adobe Launch).
1. Cree un nuevo elemento de datos para enviar datos a través de Web SDK.
1. Migre la regla de carga de página predeterminada para utilizar el elemento de datos y las acciones de Web SDK.
1. Migrar código personalizado en reglas o para complementos.
1. Publish cambia la implementación.
1. Obtenga información sobre cómo depurar y validar los cambios, y validar la regla de carga de página predeterminada y las variables asociadas a ella. Esta validación debe continuar durante toda la migración a medida que realice cambios.
1. Migrar reglas de carga de página adicionales.
1. Migrar reglas de vínculos personalizados.
1. Después de la validación completa, elimine las referencias a la extensión de Analytics y elimine la extensión en sí.
1. Una vez realizados todos los cambios, inserte la biblioteca en el entorno de ensayo y, a continuación, en la producción.
1. Una vez completado todo, vuelva a realizar la prueba. Esto es necesario porque ha realizado cambios al eliminar las referencias al código antiguo de Analytics y desea asegurarse de que todo sigue funcionando correctamente.


### NOTA PARA DOUG: después de probar el tutorial, coloque un vínculo aquí a una publicación de la comunidad en la que los clientes puedan hacer preguntas sobre el tutorial y la migración a Web SDK.
