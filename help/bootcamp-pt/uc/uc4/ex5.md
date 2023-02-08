---
title: Bootcamp - Customer Journey Analytics - Visualización usando el Customer Journey Analytics - Brasil
description: Bootcamp - Customer Journey Analytics - Visualización usando el Customer Journey Analytics - Brasil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 3272d288185415b4604fe48f18c19f8f06e6dce0
workflow-type: tm+mt
source-wordcount: '1586'
ht-degree: 1%

---

# 4.5 Customer Journey Analytics Visualização o iOS

## ones

- Entenda una interfaz de usuario de Analysis Workspace
- Conheça alguns que tornan o Analysis Workspace tão diferente.
- Analítica de CJA o Analysis Workspace

## Contexto

Neste exercício, você usará de Analysis Workspace no CJA para analisar visualizaciones ações de produtos, funis de produtos, rotatividade, etc.

Vamos usar o projeto que você criem  [4.4 Preparação de dados no Analysis Workspace](./ex4.md), então acesse [https://analytics.adobe.com](https://analytics.adobe.com).

![demostración](./images/prohome.png)

Abra seu projeto `yourLastName - Omnichannel Analysis`.

Proyecto Com seu aberto e Visualização de dados `yourLastName - Omnichannel Analysis` selesido, você está pronto para cómçar a construir suas primeiras visualizações.

![demostración](./images/prodataView1.png)

## ¿Quantas visualizações de produtos temos diariamente?

Em primeiro lugar, precisamos selecionar como datos certas para analisar os dados. Acceso a menú suspenso do calendário no lado direito da tela. Clique nele e selecione o intervalo de datos de aplicación.

>[!IMPORTANT]
>
>Selecione um intervalo de datas como **Esta semana** ou **Este mes**. Os dados disponíveis mais recentes foram absorvidos em 19 de setembro de 2022.

![demostración](./images/pro1.png)
No menú do lado esquerdo (área de componentes), encontre as métricas calculadas **Vistas del producto**. Selecione-as e arraste e solte na tela, no canto superior direito da tabela de forma livre.

![demostración](./images/pro2.png)

Automaticamente a dimensão **Día** Será cionada para criar sua primeira tabela. Agora você pode ver sua pergunta respondida imediatamente.

![demostración](./images/pro3.png)

Em seguida, clique com o botão direito do mouse no currmo da.

![demostración](./images/pro4.png)

Clique **Visualizar** e selecione **Línea** como visualização.

![demostración](./images/pro5.png)

Você como suas visualizações de produto por dia.

![demostración](./images/pro6.png)

Você podo alterar o escopo de tempo para o dia clicando em **Configuración** una visualización.

![demostración](./images/pro7.png)

Clique no ponto ao lado de **Línea** e **Administrar la fuente de datos**.

![demostración](./images/pro7a.png)

Em seguida, clique em **Bloquear selección** e selecione **Elementos seleccionados** para bloquear esta visualização para que la ssiempre exiba uma linha do tempo de Visualizações de produtos.

![demostración](./images/pro7b.png)

## 5 produtos mais vistos

¿Quais são os 5 produtos mais vistos?

Lembre-se de salvar o projeto de tempos em tempos.

| SO | Cortocircuito |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Comando +S |

Vamos cómçar a encontrar os 5 produtos mais vistos. No hay menú de lado esquerdo, encontre o Nome do produto - Dimensão.

![demostración](./images/pro8.png)

Agora arraste e solte **Nombre del producto** para substituir a dimensão **Día**:

Este será resultado.

![demostración](./images/pro10a.png)

Em seguida, tente dividir um dos produtos por Nome da marca. Pesquise **brandName** e arraste para baixo do primeiro nome do produto.

![demostración](./images/pro13.png)

Em seguida, faça um detal hamento o agente de usuário Pesquise **Agente de usuario** e arraste-o para baixo do nome da marca.

![demostración](./images/pro15.png)

Em seguida, Será exibida a tela abaixo:

![demostración](./images/pro15a.png)

Por fim, você pode adihijos mais visualizações. No lado esquerdo, em visualizações, pesquise `Donut`. Pegar `Donut`, arraste e solte na tela **Línea** 

![demostración](./images/pro18.png)

A continuación, en Tabla, seleccione las primeras 5 **Agente de usuario**  filas del desglose que hicimos en **Smartphone negro Google Pixel XL de 32 GB** > **Señal Citi**. Mientras selecciona las 5 filas, mantenga presionada la variable **CTRL** (en Windows) o **Comando** (en Mac).

Em seguida, na Tabela, selecione como primeiras 5 linhas de **Agente de usuario** do detal hamento que fizemos em **Smartphone negro Google Pixel XL de 32 GB** > **Señal Citi**. Ao selecionar como 5 linhas, sego botão **CTRL** (sin Windows) o botão **Comando** (sin Mac).

![demostración](./images/pro20.png)

Você o gráfico de donut alterado:

![demostración](./images/pro21.png)

Você pode até adaptar o diseño para ser mais legível, tornado o gráfico de **Línea** e o gráfico de **Anillo** um pouco menor para que sejam exibidos lado a lado:

![demostración](./images/pro22.png)

Clique no ponto ao lado de *Anillo** para **Administrar la fuente de datos**. Em seguida, clique em **Bloquear selección** para bloquear essa visualização para que la ssiempre exiba uma linha do tempo de Visualizações de produto.

![demostración](./images/pro22b.png)

Saiba masobre visualizações o Analysis Workspace em:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=es](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=es)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interação do produto, da visualização à compra

Existem muitas formatos de resolución esta questão. Uma delas é usar o Tipo de Interação de Produto e usá-lo em uma tabela de Dañar Lámina. Outra forma é utilizar uma **Visualización de abandonos**. Vamos uso o último, pois visualizar e analisar ao mesmo tempo.

Feche de dolor real clando aquí:

![demostración](./images/pro23.png)

Agora adicione um novo dolor em branco clicando em **+ Agregar panel en blanco**.

![demostración](./images/pro24.png)

Clique na visualização de **Visita en el orden previsto**.

![demostración](./images/pro25.png)

Selecione o mesmo intervalo de datos do exercício anterior.

![demostración](./images/prodatef.png)

Em seguida, você será:

![demostración](./images/prodatefa.png)

Encontre a dimensão **Tipo de evento** nos componentes no lado esquerdo:

![demostración](./images/pro26.png)

Clique na seta para abria dimensão:

![demostración](./images/pro27.png)

Você para todos os Tipos de eventos disponíveis.

![demostración](./images/pro28.png)

Selecione o elemento **commerce.productViews** e arraste e solte-o no campo **Agregar Touchpoint** dentro **Visualización de abandonos**.

![demostración](./images/pro29.png)

Faça o mesmo com **commerce.productListAdd** y **commerce.purchases** e solte os no campo **Agregar Touchpoint** dentro  **Visualización de abandonos**. Sua visualização agora deve ser semelhante ao seguiría:

![demostración](./images/props1.png)

Você pode fazer muitas coisas aqui. Alguns extempla: comparar ao longo do tempo, comparar cada passo por comparar por fidelidade. No entanto, se quisermos analismos coisas interessantes como por los clientes não com depois de adium item ao carrinho, uso de un melhor ferramenta do CJA: clicar com o botão direito.

Clique com o botão direito do mouse no touchpoint **commerce.productListAdd**. Em seguida, clique em **Desglose de visitas en el orden previsto en este punto de contacto**.

![demostración](./images/pro32.png)

Uma nova tabela de formato livre será criada para analisar o que as pessoas fizeram se não compraram.

![demostración](./images/pro33.png)

Altere o **Tipo de evento** por **Nombre de la página**, na nova tabela de livre, para ver em quais páginas eles estão indo, em vez da Página de confirmación mação de compra.

![demostración](./images/pro34.png)

## ¿O que as pessoas fazem no site antes de acessar una página Cancelar serviço?

Novamente, há muitas formas de realizar essa análise. Vamos usar el análise de fluxo para iniciar la parte de descoberta.

Feche de dolor real clando aquí:

![demostración](./images/pro0.png)

Agora adicione um novo dolor em branco clicando em **+ Agregar panel en blanco**.

![demostración](./images/pro0a.png)

Clique na visualização **Flujo**.

![demostración](./images/pro35.png)

Em seguida, Será exibido:

![demostración](./images/pro351.png)

Selecione o mesmo intervalo de datos do exercício anterior.

![demostración](./images/pro0b.png)

Encontre a dimensão **Nombre de la página** nos componentes no lado esquerdo:

![demostración](./images/pro36.png)

Clique na seta para abria dimensão:

![demostración](./images/pro37.png)

Você encontrará y vistas. Encontre o nome da página: **Cancelar servicio**.
Conjunto de soluciones **Cancelar servicio** na Visualização de fluxo no campo do meio:

![demostración](./images/pro38.png)

Em seguida, Será exibido:

![demostración](./images/pro40.png)

Vamos agora analisar se os clientes que visitaram a la página C **Cancelar servicio** no site também ligaram para o call center e qual foi o resultado.

Nas dimensões, retorne e encontre Tipo de interação de chamada. Conjunto de soluciones **Tipo de interacción de llamada** para substituir a primeira interação à direita em **Visualización de flujo**.

![demostración](./images/pro43.png)

Agora você visualiza o ticket de suporte dos clientes que ligaram para a central de atendimento depois de visitar página **Cancelar servicio**.

![demostración](./images/pro44.png)

Em seguida, nas dimensões, procurador **Sensación de llamada**. Arraste e solte para substituir a primeira interação à direita na visualização de fluxo.

![demostración](./images/pro46.png)

Em seguida, Será exibido:

![demostración](./images/flow.png)

Como pode ver, tamos uma análise omnichannel una visualización de flualização. Graças a isso, descobrimos que alguns clientes que estavam pensando em cancelar serviço tiveram uma avaliação positiva depois de ligar para o call center. Talvez tenhamos mudado de ideia com uma promoção?

## Qual é o desempenho dos clientes com um contato de Call center Positivo em relação aos principales KPI?

Primeiramente, vamos segmentados os dados para obrera Apenas usuários com chamaces **positive**. No CJA, os Segmentos são chamados de Filtros. Acesse para filtros na de componentes (no lado esquerdo) e clique em **+**.

![demostración](./images/pro58.png)

Dentro do Construtor de filtro, dê um nome ao filtro

| Nombre | Descripción |
| ----------------- |-------------| 
| Sentimiento de llamada - Positivo | Sentimiento de llamada - Positivo |

![demostración](./images/pro47.png)

Nos componentes (dentro do Constructor de filtro), encontre **Sensación de llamada** e arraste e solte na Definição do constructor de filtro.

![demostración](./images/pro48.png)

Agora selecione **positive** como valor para o filtro.

![demostración](./images/pro49.png)

Altere o escopo para nível **Persona**.

![demostración](./images/pro50.png)

Para finalizar, haga clic en mí **Guardar**.

![demostración](./images/pro51.png)

Então, você irá retornar para esta tela. Se ainda não retornou, feche o dolor anterior.

![demostración](./images/pro0c.png)

Agora adicione um novo dolor em branco clicando em **+ Agregar panel en blanco**.

![demostración](./images/pro24c.png)

Selecione o mesmo intervalo de datos do exercício anterior.

![demostración](./images/pro24d.png)

Clique **Tabla improvisada**.

![demostración](./images/pro52.png)

Agora arraste e solte o filtro que você acabou de criar.

![demostración](./images/pro53.png)

Hora de adiebres métricas. Comece com **Vistas del producto**. Arraste e solte na tabela de forma livre. Vê podo excluir un também **Eventos**.

![demostración](./images/pro54.png)

Faça o mesmo com **People**, **Agregar al carro** e **Compras**. Você vai com uma tabela como seguinte.

![demostración](./images/pro55.png)

Graças à primeira análise de fluxo, uma nova pergunta suru. Então decidimos criar esta tabela e verificar alguns KPI em um segmento para responder a essa pergunta. Como você pover, o tempo de muito maie do que usar SQL ou tras soluções de BI.

## Recapitulação do Analysis Workspace e do Customer Journey Analytics

O Analysis Workspace elimina el todas como limitações típicas de um relatório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics tratados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões, métricas, segmentos e granularidades de tempo) para el proyecto um. Você pode criar de forma instantânea filtros e analises, gráficos de coorte, alertas, segmentos, análises de fluxo e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

Próxima etapa: [4.6 De perspectivas a ação](./ex6.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos los Módulos](./../../overview.md)
