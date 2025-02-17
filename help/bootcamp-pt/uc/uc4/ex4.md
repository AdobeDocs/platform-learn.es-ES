---
title: Bootcamp - Customer Journey Analytics - Preparación de datos en Analysis Workspace - Brasil
description: Bootcamp - Customer Journey Analytics - Preparación de datos en Analysis Workspace - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Workspace Basics, Calculated Metrics
exl-id: d56128af-dd1e-47ea-922f-85418e9da687
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# 4.4 Preparación de datos en Customer Journey Analytics

## Objetivos

- Entenda a UO do Analysis Workspace no CJA
- Entenda los conceptos de preparación de datos en Analysis Workspace
- Aprenda un fazer de datos

## 4.4.1 IU hacer Analysis Workspace en CJA

O Analysis Workspace eliminar todas como limitações típicas de um único relatório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões,, e granularidades de tempo) para um projeto. Criação instantânea de avarias e, criação de cortes para análise, criação de alertas, comparação de, análise de fluxo e de falhas e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

O Customer Journey Analytics traz essa solución além dos dados da plataforma. Ése recomienda que asista a este vídeo de visão geral de quatro minutos:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on&enablevpops)

Se você nunca usou o Analysis Workspace antes, se habla en inglés, se habla en inglés, se habla en inglés:

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on&enablevpops)

### Proyecto Crie Seu

Agora é hora de criar seu primeiro projeto do CJA. Vá para a aba de projetos dentro do CJA. Haga clic en **Crear nuevo**.

![demostración](./images/prmenu.png)

Em, el você va a tela abaixo. Seleccione **Proyecto en blanco** ficha **Crear**.

![demostración](./images/prmenu1.png)

Você verá um projeto vazio.

![demostración](./images/premptyprojects.png)

Primeiro, certifique-se de selecionar a Visualização de dados correta no canto superior direito da tela. Neste ejemplo, a Visualização de dados a ser selecionado é `vangeluwe - Omnichannel Data View`.

![demostración](./images/prdv.png)

Em, você va a salvar el proyecto de dar un nombre a otro. Você pode usar o seguinte comando para salvar:

| Sistema operativo | Método abreviado |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Comando + S |

Você verá este pop-up:

![demostración](./images/prsave.png)

Utiliza este modelo de nomenclatura:

| Nombre | Descripción |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em, grupo **Guardar**.

![demostración](./images/prsave2.png)

## 4.4.2 Métricas calculadas

Embora tenhamos organizado todos los componentes na Visualização de dados, você ainda deve algunos deles para que os usuários de negócios estejam prontos para iniciar suas análises. Além disso, durante qualquer processo de analytics, você pode criar cálculos para profundizar a descoberta de insights.

Como ejemplo, criaremos uma Taxa de conversão calculada usando una métrica/evento Compras que definimos na Visualização de dados.

## Taxa de conversación

Vamos começar a abrir o construtor de métricas calculadas. Clique em **+** para criar sua primeira Métrica calculada en Analysis Workspace.

![demostración](./images/pradd.png)

O **Creador De Métricas Calculadas**:

![demostración](./images/prbuilder.png)

Encontre **Purchases** na lista de indicadores no menu do lado esquerdo. Em **Métricas** grupo em **Mostrar todo**

![demostración](./images/calcbuildercr1.png)

Agora arraste e solte a métrica **Compras** na definição da métrica calculada.

![demostración](./images/calcbuildercr2.png)

, taxa de conversación significa **Conversiones / Sesiones**. Então, vamos fazer o mesmo calculada... Encontre a métrica **Sessions** e arraste e solte-a no criador de definição, no evento **Purchases**.

![demostración](./images/calcbuildercr3.png)

Observe que o operador de divisão é selecionado automáticamente.

![demostración](./images/calcbuildercr4.png)

A taxa de conversão é comumente representada em porcentaje agem. Então, vamos mudar o formato para el porcentaje y selección de 2 casas decimais.

![demostración](./images/calcbuildercr5.png)

Finalmente, cambie el nombre y la descripción de la métrica calculada:

| Título | Descripción |
| ----------------- |-------------| 
| Tasa de conversión | Tasa de conversión |

Por fim, altere o nome e a descripción da métrica calculada:

![demostración](./images/calcbuildercr6.png)

Não se esqueça de **Salvar** a Métrica calculada.

![demostración](./images/pr9.png)

## 4.4.3 Dimensiones calculadas: Filtros (segmentação) e intervalos de datos

### Filtros: Dimensões calculadas

No hay nada que ver con el resto de los. Antes de iniciar qualquer análise, também é interessante criar algumas **Calculated Dimensions**. Esto significa, esencialmente, **segmentos** en Adobe Analytics. No hay Customer Journey Analytics, las están en chamados de **Filters**.

![demostración](./images/prfilters.png)

A criação de filtros ajudará os usuários de negócios a iniciar o analytics com algumas dimensões calculadas valiosas. Isso algumas tarefas, além de ajudar na parte de adoção. Abaixo estão some s exSERVICE:

1. Mídia Própria, Mídia Paga,
2. Visitas novas x recorrentes
3. Clientes com carrinho abandonado

Esses filtros podem ser criados antes ou durante a parte de análise (o que você fará no próximo exercício).

### Intervalos de datos: Dimensões de tempo calculadas

Como dimensiones de tiempo são outro tipo de dimensiones calculadas. Uno de los temas más importantes de la vida diaria es la lucha contra la pobreza.

Essas Dimensões de tempo ajudarão analistas e usuários de negócios a lembrar datas importantes e usá-las para e alterar o tempo de relatório. Perguntas e dúvidas típicas quando fazemos análises:

- Quando foi a Black Friday do ano passado? ¿Entre los días 21 y 29?
- Quando veiculamos aquela campanha de TV em dezembro?
- De quando a quando fizemos as vendas de verão de 2018? Quero comparar com 2019. A propósito, você sabe os dias exatos em 2019?

![demostración](./images/timedimensions.png)

Agora você concluiu o exercício de preparação de dados usando o Analysis Workspace do CJA.

Próxima etapa: [4.5 Visualização usando Customer Journey Analytics](./ex5.md)

[Hoteles cerca de Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos los Módulos](./../../overview.md)
