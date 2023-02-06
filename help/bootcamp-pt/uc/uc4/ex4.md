---
title: Bootcamp - Customer Journey Analytics - Preparación de datos en Analysis Workspace - Brasil
description: Bootcamp - Customer Journey Analytics - Preparación de datos en Analysis Workspace - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4 Preparação de dados em Customer Journey Analytics

## ones

- Entenda a UO do Analysis Workspace no CJA
- Entenda os ceitos de preparação de dados no Analysis Workspace
- Aprenda a fundir cálculos de dados

## 4.4.1 La interfaz de usuario de Analysis Workspace no es CJA

O Analysis Workspace retire el todas como limitações típicas de um relacionório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics tratados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões, métricas, segmentos e granularidades de tempo) para el proyecto um. Criação instantânea de avarias e segmentos, criação de para análise, criação de alertas, comparação de segmentos, análise de fluxo e de falhas e relatórios de curadoria e agendamento para comparar lhar com qualquer pessoa em negócio.

O Customer Journey Analytics traz essa solução além dos plataforma. É altamente recomendación ável assistir a este de vídeo geral de quatro minutos:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

Se você nunca usou en Analysis Workspace antes ante, el futuro.

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### Crie Seu Projeto

Agora é hora de criar seu primeiro projeto do CJA. Vá para a aba de projetos dentro do CJA. Clique **Crear nuevo**.

![demostración](./images/prmenu.png)

Em seguida, você verá a tela abaixo. Selecione **Proyecto en blanco** então clique em **Crear**.

![demostración](./images/prmenu1.png)

Você será um projeto vazio.

![demostración](./images/premptyprojects.png)

Primeiro, certificfique-se de seleiro a Visualização de dados corrita no canto superior direito da tela. Neste exemplo, una visualización de la ção de dados a ser selecionada é `vangeluwe - Omnichannel Data View`.

![demostración](./images/prdv.png)

Em seguida, você irá salvar seu projeto e dar um nome a ele. Você pode usar o seguinte para salvar:

| SO | Cortocircuito |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Comando +S |

Você aparecerá este pop-up:

![demostración](./images/prsave.png)

Use este modelo de nomenclatura:

| Nombre | Descripción |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em seguida, clique em **Guardar**.

![demostración](./images/prsave2.png)

## 4.4.2 Métricas calculadas

Embora tenhamos organizados todos os componentes na Visualização de dados, você ainda deve adaptar alguns para que os usuários de negócios estejam prontos para iniciar como análises. Além disso, qualquer processo de analytics, você pode criar métricas calculadas para profundidad a descoberta de perspectivas.

Como explique, criaremos uma Templo que definió el futuro de las compras na Visualização de dados.

## Taxa de conversão

Vamos cómplice a construcción de métricas calculadas. Clique **+** para criar sua primeira Métrica calculada en Analysis Workspace.

![demostración](./images/pradd.png)

O **Creador de métricas calculadas** irá aparecer:

![demostración](./images/prbuilder.png)

Encontre **Compras** lista de métricas no menú lado esquerdo. Em **Métricas** clique em **Mostrar todo**

![demostración](./images/calcbuildercr1.png)

Agora arraste e solte a la policía **Compras** una definición de la mañana calculada.

![demostración](./images/calcbuildercr2.png)

Normalmente, taxa de conversión **Conversiones/Sesiones**. Então, vamos fazer o mesmo na tela de definição de calculada. Encontrar un vestido **Sesiones** e arraste e solte-a no criador de definición ção, no hay evento **Compras**.

![demostración](./images/calcbuildercr3.png)

Observar que o el operador de división é seleestudia automaticamente.

![demostración](./images/calcbuildercr4.png)

Un taxa de conversación é comumente representada em agem. Então, vamos mudar o para el Programa e selecionar 2 casas decimais.

![demostración](./images/calcbuildercr5.png)

Finalmente, cambie el nombre y la descripción de la métrica calculada:

| Título | Descripción |
| ----------------- |-------------| 
| Tasa de conversión | Tasa de conversión |

Por fim, alterar el nombre de una descripción de la calculada:

![demostración](./images/calcbuildercr6.png)

Não se esqueça de **Salvar** a Métrica calculada.

![demostración](./images/pr9.png)

## 4.4.3 Dimensões calculadas: Filtros (segmentação) e intervalos de datos

### Filtros: Dimensões calculadas

Os cálculos não devem ser para métricas. Antes de iniciar qualquer análise, também é interessante criar algumas **Dimension calculados**. Isso encialmente. **segmentos** sin Adobe Analytics. Sin Customer Journey Analytics, ess segmentos são chamados de **Filtros**.

![demostración](./images/prfilters.png)

Una criação de filtros ajudará os usuários de negócios a iniciar o analytics com algumas dimensões calculadas valiosas. Isso irá automatizar algumas tarefas, além de ajudar na parte de adoção. Abaixo estão alguns exprés:

1. Mídia Própria, Mídia Paga,
2. Visitas novas x grabaciones
3. Clientes com carrinho Abandonado

Esses filtros criados ante ou a parte de análise você (to que você no próximo exercício).

### Intervalos de datos: Dimensões de tempo calculadas

Como calculadas dimensões de tempo são outipo de dimensões. Alguns já foram criados, mas você também pode criar suas próprias Dimensões de tempo personalizadas fasa de preparação de dados.

Essas Dimensões de tempo calculado ajudarão analistas e usuários de negócios a lembrar datas importantes e usá-las para filtrar e alterar o tempo de relatório. Perguntas e dúlabicas quando fazemos análises:

- Quando foi un Black Friday do ano passado? Entre os dias 21 e 29?
- Quando veiculamos aquela campanha de TV em dezembro?
- ¿De quando a quando fizemos como vendas de verão de 2018? Quero comparar com 2019. ¿Una versión de 2019 de la versión surcoreana del você sabe os dias exatos em?

![demostración](./images/timedimensions.png)

Agora você de concluiu o exercício de preparação de conocimiento de Analysis Workspace do CJA.

Próxima etapa: [4.5 Customer Journey Analytics Visualização iOS](./ex5.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos los Módulos](./../../overview.md)
