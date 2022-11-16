---
title: 'Foundation: Perfil del cliente en tiempo real'
description: 'Foundation: Perfil del cliente en tiempo real'
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 050e5d99-544d-4a86-a7f6-9f103381dca5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---

# 3. Fundamento: Perfil del cliente en tiempo real

**Autor: [WOutside Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

En este módulo, profundizaremos en las funciones de Perfil del cliente en tiempo real e identidad de Adobe Experience Platform. Aprenderá cómo se pueden definir las audiencias, la función del servicio de identidad y el ID de Experience Cloud, y cómo definir las consultas del generador de segmentos para definir sus propios segmentos.

## Objetivos de aprendizaje

- Obtenga información sobre cómo visualizar el perfil de cliente en tiempo real de un cliente a través de la interfaz de usuario de Adobe Experience Platform
- Obtenga información sobre cómo crear un segmento con el Generador de segmentos de Adobe Experience Platform
- Obtenga información sobre cómo crear un segmento y almacenar los resultados del segmento en un conjunto de datos mediante las API de Adobe Experience Platform
- Obtenga información sobre el impacto de tener acceso a un perfil de cliente completo, incluido el comportamiento en tiempo real, en entornos sin conexión

## Requisitos previos

- Acceso a [Adobe Experience Platform](https://experience.adobe.com/platform)
- Acceso a [https://public.aepdemo.net](https://public.aepdemo.net)
- **Descargar estos recursos**:
   - [Colecciones de Postman](./../../assets/postman/postman_profile.zip)

>[!IMPORTANT]
>
>Este tutorial se creó para facilitar un formato de taller concreto. Utiliza sistemas y cuentas específicos a los que es posible que no tenga acceso. Incluso sin acceso, creemos que aún puede aprender mucho leyendo este contenido muy detallado. Si participa en uno de los talleres y necesita sus credenciales de acceso, póngase en contacto con el representante del Adobe, que le proporcionará la información necesaria.

## Información general sobre la arquitectura

Eche un vistazo a la siguiente arquitectura, que resalta los componentes que se discutirán y utilizarán en este módulo.

![Información general sobre la arquitectura](../../assets/images/architecturem3.png)

## Espacio aislado para usar

Para este módulo, utilice este simulador de pruebas: `--aepSandboxId--`.

>[!NOTE]
>
>No olvide instalar, configurar y utilizar la extensión de Chrome como se indica en [0.1: Instalar la extensión de Chrome para la documentación del Experience League](../module0/ex1.md)

## Ejercicios

[3.1 Visitar el sitio web](./ex1.md)

En este ejercicio, seguirá un script y recorrerá el sitio web.

[3.2 Visualizar su propio perfil de cliente en tiempo real: IU](./ex2.md)

En este ejercicio, iniciará sesión en Adobe Experience Platform y verá su propio perfil de cliente en tiempo real en la interfaz de usuario.

[3.3 Visualizar su propio perfil de cliente en tiempo real: API](./ex3.md)

En este ejercicio, utilizará Postman y Adobe I/O para ver su propio perfil de cliente en tiempo real mediante las API de Adobe Experience Platform.

[3.4 Crear un segmento: IU](./ex4.md)

En este ejercicio, creará un segmento utilizando el Generador de segmentos de Adobe Experience Platform.

[3.5 Crear un segmento: API](./ex5.md)

En este ejercicio, utilizará Postman y Adobe I/O para crear un segmento y almacenar los resultados de ese segmento como un conjunto de datos, mediante el uso de las API de Adobe Experience Platform.

[3.6 Consulte su perfil de cliente en tiempo real en acción en el centro de llamadas](./ex6.md)

En este ejercicio, suplantará a un empleado del centro de llamadas que reciba una llamada de un cliente. Para que esto tenga un impacto real en la experiencia de este cliente, necesitará acceder a toda la información disponible en tiempo real.

[Resumen y beneficios](./summary.md)

Resumen de este módulo y visión general de los beneficios.

>[!NOTE]
>
>Gracias por invertir su tiempo en aprender todo lo que hay que saber sobre Adobe Experience Platform. Si tiene preguntas, desea compartir comentarios generales de sugerencias sobre contenido futuro, póngase en contacto directamente con WOutside Van Geluwe, enviando un correo electrónico a **vangeluw@adobe.com**.

[Volver a todos los módulos](../../overview.md)
