---
title: Bootcamp - Customer Journey Analytics - Preparación de datos en Analysis Workspace - Brasil
description: Bootcamp - Customer Journey Analytics - Preparación de datos en Analysis Workspace - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: d56128af-dd1e-47ea-922f-85418e9da687
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4 Preparación de datos en Customer Journey Analytics

## Objetivos

- Entenda a UO do Analysis Workspace no CJA
- Entenda los conceptos de preparación de datos en Analysis Workspace
- Aprenda un fazer de datos

## 4.4.1 IU hacer Analysis Workspace en CJA

O Analysis Workspace eliminar todas como limitações típicas de um único relatório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões,, e granularidades de tempo) para um projeto. Criação instantânea de avarias e, criação de cortes para análise, criação de alertas, comparação de, análise de fluxo e de falhas e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

O Customer Journey Analytics traz essa solução além dos dados da plataforma. Ése recomienda que asista a este vídeo de visão geral de quatro minutos:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

Se você nunca usou o Analysis Workspace antes, se habla en inglés, se habla en inglés, se habla en inglés:

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### Proyecto Crie Seu

Agora é hora de criar seu primeiro projeto do CJA. Vá para a aba de projetos dentro do CJA. Clique em **Crear nuevo**.

![demostración](./images/prmenu.png)

Em, el você va a tela abaixo. Selecione **Proyecto en blanco** então clique em **Crear**.

![demostración](./images/prmenu1.png)

Você verá um projeto vazio.

![demostración](./images/premptyprojects.png)

Primeiro, certifique-se de selecionar a Visualização de dados correta no canto superior direito da tela. Neste ejemplo, a Visualização de dados a ser selecionada é `vangeluwe - Omnichannel Data View`.

![demostración](./images/prdv.png)

Em, você va a salvar el proyecto de dar un nombre a otro. Você pode usar o seguinte comando para salvar:

| SO | Método abreviado |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Comando +S |

Você verá este pop-up:

![demostración](./images/prsave.png)

Utiliza este modelo de nomenclatura:

| Nombre | Descripción |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em, grupo em **Guardar**.

![demostración](./images/prsave2.png)

## 4.4.2 Métricas calculadas

Embora tenhamos organizado todos los componentes na Visualização de dados, você ainda deve algunos deles para que os usuários de negócios estejam prontos para iniciar suas análises. Além disso, durante qualquer processo de analytics, você pode criar cálculos para profundizar a descoberta de insights.

Como ejemplo, criaremos uma Taxa de conversão calculada usando una métrica/evento Compras que definimos na Visualização de dados.

## Taxa de conversación

Vamos começar a abrir o construtor de métricas calculadas. Clique em **+** para criar sua primeira Métrica calculada en Analysis Workspace.

![demostración](./images/pradd.png)

O **Creador de métricas calculadas** va a hacer lo siguiente:

![demostración](./images/prbuilder.png)

Encontrar **Compras** una lista de métricas no menu do lado esquerdo. Em **Métricas** círculo em **Mostrar todo**

![demostración](./images/calcbuildercr1.png)

Agora arraste e solte a métrica **Compras** Una definición de la métrica calculada.

![demostración](./images/calcbuildercr2.png)

, taxa de conversación significa **Conversiones/Sesiones**. Então, vamos fazer o mesmo calculada... Encontrar una métrica **Sesiones** No hay ningún criador de definición, no hay evento **Compras**.

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

### Filtros: Cosas que hacer cerca

No hay nada que ver con el resto de los. Antes de iniciar el análisis, também é interessante criar algumas **Dimension calculados**. Isso significa, esencialmente, **segmentos** no hay Adobe Analytics. No hay Customer Journey Analytics, no hay **Filtros**.

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
