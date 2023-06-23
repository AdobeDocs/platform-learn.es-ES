---
title: Bootcamp - Perfil del cliente en tiempo real - De desconocido a conocido en el sitio web - Brasil
description: Bootcamp - Perfil del cliente en tiempo real - De desconocido a conocido en el sitio web - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 853a69d2-5dac-413d-bb40-ef29604a26ae
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# 1.1 Hacer desconhecido ao conhecido em nosso site

## Contexto

A Adobe Experience Platform desempenha um papel importante nessa jornada. A plataforma é o cérebro da comunicação, o **sistema de registro de experiencia**.

Plataforma é um ambiente em que a palavra cliente engloba mais do que clientes conhecidos. Um visitante desconhecido no site também é um cliente do ponto de vista da Plataforma e, como tal, todo o comportamiento de um visitante desconhecido também é publicado à Plataforma. Graças a essa abordagem, quando esse visitante eventualmente se torna um cliente conhecido, uma marca também pode que aconteceu antes daquele momento. Isso ajuda a partir de uma perspectiva de optimización de atribución e experiencia.

## Fluxo da jornada do cliente

Acceso [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Clique em **Permitir todo**.

![DSN](./images/web8.png)

Clique no ícone do Adobe da canto superior esquerdo da tela para abrir o Visualizador de perfil.

![Demostración](./images/pv1.png)

el visualizador de perfil y perfil del cliente en tiempo real com o **ID de Experience Cloud** como o identificador primario para este cliente que ainda é desconhecido.

![Demostración](./images/pv2.png)

Você também pode ver todos los Eventos de Experiência coletados com base no comportamiento do cliente. A lista está vazia no momento, mas isso muda em breve.

![Demostración](./images/pv3.png)

Acceso a una opción de menú **Servicios de aplicación** e clique no produto **Real-Time CDP**.

![Demostración](./images/pv4.png)

Você verá una página de detalles do produto. Um Evento de experiência do tipo **Vista del producto** agora foi publicado para a Adobe Experience Platform usando a implementação do Web SDK que você revisou no Módulo 1. Abra o pain Visualizador de perfil e verifique seus **Eventos de experiencia**.

![Demostración](./images/pv5.png)

Acceso a una opción de menú **Servicios de aplicación** e clique no produto **Adobe Journey Optimizer**. Mais um Evento de experiência publicado para a Adobe Experience Platform.

![Demostración](./images/pv7.png)

Abra o pain Visualizador de perfil. Agora você verá 2 Eventos de experiência do tipo **Vista del producto**. Embora o comportamiento seja anônimo, cada clique é rastreado e armazenado na Adobe Experience Platform. Depois que o cliente anônimo se tornar conhecido, poderemos mesclar todo o comportamiento anônimo automáticamente ao perfil conhecido.

![Demostración](./images/pv8.png)

Agora vamos analisar seu perfil de cliente e usar seu comportamento para personalizar sua experiência do cliente en el sitio.

Próxima etapa: [1.2 Visualiza tu perfil de cliente en tiempo real - UI](./ex2.md)

[Hoteles cerca de Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos los Módulos](../../overview.md)
