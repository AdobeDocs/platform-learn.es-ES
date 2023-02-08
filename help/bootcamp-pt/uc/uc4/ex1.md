---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasil
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 3272d288185415b4604fe48f18c19f8f06e6dce0
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## ones

- Entenda o que é o CJA
- Entenda qual é o papel do CJA
- Entenda del flujo de trabajo de CJA: datos de da conexão de dados aos

## 4.1.1 ¿O que é o Customer Journey Analytics?

O Customer Journey Analytics (Curi JA) fornece uma interface em que os times de Analytics, Negócios Tecnologia em todos os dados los dados da companhia e analisar una jornada cruzada (en línea y fuera de línea) do cliente de ponta a. O CJA é capaz de fornecer contexto e clareza para esa jornada, trazendo uma visão acionável em cima das difíciles dades no processo de conversaciones e posibles sibilitando a planejamento de experiências relevantes e personalizadas pontos mais relevantes.

O CJA traz o Analysis Workspace conectado a Adobe Experience Platform. Un Adobe Experience Platform é o cérebro da comunicação e da estração e, com o CJA, como marcas agora podem contextualizar e visualizar todos los dados, para que equipare los equipos e negócios e insights posam com eles, analisorquando toda una jornada en línea para off-line do cliente.

Como equipamientos de negócios e insights podem conversar com o CJA, fazer perguntas e obter respostas em tempo real com a interface do usuário de arrastar e soltar, apontar e clicar e fácil de usar do Analysis Workspace.

![demostración](./images/cja-adv-analysis1.png)

## 4.1.2 Principales agentes

Os três principales beneficiícios para los clientes são:

- Una capacidad de disponibilidad bilizar para todos (ou seja, democratizar o acesso os dados).
- Una capacitación de ver o cliente em uma jornada contextual (ou seja, os dados podem ser visualizados secuencialmente, abrangendo múlti plos canais on-line e off-line).
- Una capacidade aitar o poder dos dados dados sem que haja a necesariamente sidade (ou seja, que indivíduos usem para bloquear ideas e análises profundas para ativação de marketing).

## 4.1.3 ## 4.1.3 ¿Por que escolher o Customer Journey Analytics?

O CJA não se destina a substituir um aplicativo de BI atual, como Power BI, Microestrategia, Locker ou Tableau. ¿O los candidatos a visualizar se han métricas rápidamente? O do uma ferramenta de análise obrigatória para essas pessoas



Tradiciones, os aplicativos de BI têm sido incapazes de permitir verdadeira inteligente do cliente:

- Eles não podem fazer attribute ção e não fazem análises de la jornada del cliente.
- Os aplicativos de BI precisam sable a pergunta com antecedência
- Como consultas intercomunitarias são pela estrutura do banco de fondos
- Responsabilidades de SQL são necesarios.
- Os aplicativos de BI não permitem que você pergunte o fondo aconteci mento.
- Os aplicativos de BI não têm conexão direta com pontos de contato do cliente.

Portanto, usuários de negócios e analistas chegam a becos sem saída quase imediatamente, tornando a análise cara, lenta, inflexível e desconectada dos sistemas de ação.

Com o CJA você pode ter umaro completa vida en línea entender que algo aconteceu fuera de línea, y relacionados como ferramentas como certas para reduzir o tempo de insight, haciendo os usuários de negócios para independientemente algo aconteceu e como respondedores a isso.

![demostración](./images/cja-use-case.png)

## 4.1.4 Programa de fluxo de trabalho do Customer Journey Analytics

Antes de iniciar os próximos exercícios, é essencial compreender quais etapas são necesarios para trazer dados da Adobe Experience Platform para o CJA para visualizá-los e obter alguns insights blog. É o que chamamos de fluxo de trabalho do CJA. Vamos verificar:

![demostración](./images/cja-work-flow.jpg)

Antes de iniciar etapas acima, não se esqueça da etapa 0, que é compreender os dados que estão disponíveis na Adobe Experience Platform.

**La basura entra, la basura sale.** Você deve ter uma ideia clara de quais dados estão disponíveis e como os esquemas na Adobe Experience Platform são configurados. Compreender os dados que estão na Adobe Experience Platform facilitará as coisas, não só na parte de conexão de dados, mas também na hora de construir visualizações e fazer análises.

## 4.1.5 Etapa 0: Conjuntos de datos de esquemas e del integrador de Adobe Experience Platform

Inicio de sesión de Facha en Adobe Experience Platform accediendo a una URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Inicio de sesión en Depois de fazer, você irá acessar a post inicial da Adobe Experience Platform.

![Ingesta de datos](../uc1/images/home.png)

precisa selecionar um de continuar, você **entorno limitado**. O nome do sandbox a ser selector é é ``Bootcamp``. Você pode fazer isso clicando no ícone **[!UICONTROL Prod]** no canto superior direito da tela. Depoes es de seleê o sandbox apropiado, vocalista verá una tela mutela e agora você está em seu sandbox dedicado.

![Ingesta de datos](../uc1/images/sb1.png)

Verifique Esquemas de e conjuntos de datos en Adobe Experience Platform.

| Conjunto de datos | Esquema |
| ----------------- |-------------| 
| Sistema de demostración: conjunto de datos de evento para sitio web (Global v1.1) | Sistema de demostración: Esquema de eventos para sitio web (Global v1.1) |
| Sistema de demostración: conjunto de datos de evento para el centro de llamadas (Global v1.1) | Sistema de demostración: Esquema de eventos para el centro de llamadas (Global v1.1) |
| Sistema de demostración: conjunto de datos de evento para asistentes de voz (Global v1.1) | Sistema de demostración: Esquema de eventos para asistentes de voz (Global v1.1) |

Certifique-se de ter verificado ao menos:

- Identidades: CRMID, phoneNumber, ECID, correo electrónico. ¿Quais identidades são os identificadores primários, quais são os identificadores secários?

Você pode encontrar os identificadores abrindo um schema e observando o objeto `_experienceplatform.identification.core`. Verifique o esquema [Sistema de demostración: Esquema de eventos para sitio web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demostración](./images/identity.png)

- Explorar el objeto de comércio dentro del esquema [Sistema de demostración: Esquema de eventos para sitio web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demostración](./images/commerce.png)

- Visualizar todos [conjuntos de datos](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e verificará los documentos

Agora você está ahora para cómçar a utilizar una interfaz do usuário do Customer Journey Analytics.

Próxima etapa: [4.2 Conecte conjuntos de datos da Adobe Experience Platform no es Customer Journey Analytics](./ex2.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos los Módulos](../../overview.md)
