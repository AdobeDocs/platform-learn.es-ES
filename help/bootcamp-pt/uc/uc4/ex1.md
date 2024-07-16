---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasil
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
exl-id: 63933d9e-b774-483f-b547-188c77440595
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## Objetivos

- Entenda o que é o CJA
- Entenda qual é o papel do CJA
- Entenda o workflow do CJA: da conexão de dados aos insights

## 4.1.1 O que é o Customer Journey Analytics?

O Customer Journey Analytics (CJA) fornece uma interface em que os times de Analytics, Negócios e Tecnología conseguem unir todos os dados da compañía e analisar a jornada cross-channel (online e offline) do cliente de ponta a ponta. O CJA é capaz de fornecer contexto e clareza para essa jornada, trazendo uma visão accionável em cima das difíciles dades no processo de conversão e possibilitando o planejamento de experiências e nos pontos mais.

O CJA traz o Analysis Workspace conectado a Adobe Experience Platform. A Adobe Experience Platform é o cérebro da comunicação e da orquestração e, com o CJA, as marcas agora podem contextualizar e todos ess dados, para que as equipes de negócios e insights posam aprender com eles, analisando hoy a jornada on-line para off-line do cliente.

Como equipes de negócios e insights podem conversar com o CJA, fazer perguntas e obter respostas em tempo real com a interface do usuário de arrastar e soltar, apontar e clicar e fácil de usar do Analysis Workspace.

![demostración](./images/cja-adv-analysis1.png)

## 4.1.2 Principipais vantagens

Os três principantes beneficiosos para os clientes são:

- A capacidade de disponibilidad insights para todos (ou seja, democratizar o acesso aos dados).
- A capacidade de ver o cliente em uma jornada contextual (ou seja, os dados podem ser visualizado secuencialmente, abrangendo múltiplos canais on-line e off-line).
- A capacidade de aprovéitar o poder dos dados sem que haja a necesisidade (ou seja, permite que indivíduos usem dados para desbloquear insights e análises para ativação de marketing).

## 4.1.3 ## 4.1.3 Por que escolher o Customer Journey Analytics?

O CJA não se destina a substituir um aplicativo de BI atual, como Power BI, Microstrategy, Locker ou Tableau. O objetivo desses aplicativos de BI é para criar a los dolores para que todos em uma organização posam ver a los rápidamente. O objetivo do CJA é trazer poder de análise para as equipes de Marketing e Negócios, tornando-o uma ferramenta de análise obrigatória para essas pessoas



Tradicionalmente, os aplicativos de BI têm sido incapazes de a verdadeira inteligência do cliente:

- Eles não podem fazer atribuição e não fazem análises de jornada do cliente.
- Os aplicativos de BI precisam saber a pergunta com antecedência
- Como consultas interativas são limitado pela estrutura do banco de dados
- Habilidades de SQL são necesarias.
- Os aplicativos de BI não permitem que você pergunte o motivo de un.
- Os aplicativos de BI não têm conexão direta com os pontos de contato do cliente.

Portanto, usuários de negócios e analistas chegam a becos sem saída quase imediatamente, tornando a análise cara, lenta, inflexível e desconectada dos sistemas de ação.

Com o CJA você pode ter uma visão completa da jornada do cliente, usando dados offline e online, com as ferramentas certas para reduzir o tempo de insight, tornando os usuários de negócios independientes para entender por que algo aconteceu e como responder a isso.

![demostración](./images/cja-use-case.png)

## 4.1.4 Compendio del flujo de trabajo del Customer Journey Analytics

Antes de iniciar los próximos exercícios, é essencial compreender quais etapas são necesárias para trazer dados da Adobe Experience Platform para o CJA para visualizá-los e obter some s insights profundos. É o que chamamos de fluxo de trabalho do CJA. Vamos a:

![demostración](./images/cja-work-flow.jpg)

Antes de iniciar como etapas acima, não se esqueça da etapa 0, que é compreender os dados que estão disponíveis na Adobe Experience Platform.

**basura entra, basura sale.** Você deve ter uma ideia clara de quais dados estão disponíveis e como os esquemas na Adobe Experience Platform são. Compreender os dados que estão na Adobe Experience Platform como coisas, não só na parte de conexão de dados, mas também na hora de construir visualizaciones e fazer análises.

## 4.1.5 Etapa 0: Compresor de conjuntos de datos electrónicos de la Adobe Experience Platform

Faça inicia sesión en Adobe Experience Platform accediendo a una dirección URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer login, você irá a página inicial da Adobe Experience Platform.

![Ingesta de datos](../uc1/images/home.png)

Antes de continuar, você precisa selecionar um **espacio aislado**. O nome do sandbox a ser selecionado é ``Bootcamp``. Você pode fazer isso clicando no ícone **[!UICONTROL Prod]** no canto superior direito da tela. Depois de selecionar o sandbox apropiado, você a tela mudando e agora você está em seu sandbox dedicada.

![Ingesta de datos](../uc1/images/sb1.png)

esquemas y conjuntos de datos en Adobe Experience Platform.

| Conjunto de datos | Esquema |
| ----------------- |-------------| 
| Sistema de demostración: conjunto de datos de eventos para el sitio web (Global v1.1) | Sistema de demostración: Esquema de eventos para el sitio web (Global v1.1) |
| Sistema de demostración: conjunto de datos de eventos para el centro de llamadas (Global v1.1) | Sistema de demostración: esquema de eventos para el centro de llamadas (Global v1.1) |
| Sistema de demostración: conjunto de datos de eventos para asistentes de voz (Global v1.1) | Sistema de demostración: esquema de eventos para asistentes de voz (Global v1.1) |

Certifique-se de ter verificado ao menos:

- Identidades: CRMID, phoneNumber, ECID, correo electrónico. ¿Cuáles son las identidades são os primários, quais são os ários?

Você pode os abrindo do um schema e o objeto `_experienceplatform.identification.core`. Esquema de [Sistema de demostración: esquema de eventos para el sitio web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demostración](./images/identity.png)

- Explore el objeto de comércio dentro do schema [Sistema de demostración - Esquema de eventos para el sitio web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demostración](./images/commerce.png)

- Visualizar todos los [conjuntos de datos](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) y verificar los datos

Agora você está pronto para hacer uso de la interfaz de usuario del Customer Journey Analytics.

Próxima etapa: [4.2 Puenteo datasets da Adobe Experience Platform no Customer Journey Analytics](./ex2.md)

[Hoteles cerca de Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos los Módulos](../../overview.md)
