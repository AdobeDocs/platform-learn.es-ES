---
title: Bootcamp - Customer Journey Analytics - Visualización con Customer Journey Analytics - Brasil
description: Bootcamp - Customer Journey Analytics - Visualización con Customer Journey Analytics - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Visualizations
exl-id: eb5eac54-22d8-428b-acac-16570f75085e
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# 4.5 Visualización del uso del Customer Journey Analytics

## Objetivos

- Entenda una interfaz de usuario para Analysis Workspace
- Conheça some s recursos que tornam o Analysis Workspace tão diferente.
- Aprenda a analizar no CJA usando o Analysis Workspace

## Contexto

Neste exercício, você o Analysis Workspace no CJA para analisar visualizaciones de productos, funis de productos, rotatividade, etc.

Vamos a usar el proyecto que você criou em [4.4 Preparación de datos en Analysis Workspace](./ex4.md), então acesse [https://analytics.adobe.com](https://analytics.adobe.com).

![demostración](./images/prohome.png)

Abra el proyecto a `yourLastName - Omnichannel Analysis`.

Com seu projeto aberto e Visualização de dados `yourLastName - Omnichannel Analysis` selecionado, você está pronto para começar a construir suas primeiras visualizaciones.

![demostración](./images/prodataView1.png)

## Quantas visualizaciones de productos temos diariamente?

Em primeiro lugar, precisamos selecionar as datas certas para analisar os dados. Acceso al menú suspenso do calendario no lado direito da tela. Clique nele e selecione o de datos aplicados.

>[!IMPORTANT]
>
>Selecione um de datos como **Esta semana** o **Este mes**. Os dados disponíveis mais recentes foram absorvidos em 19 de setembro de 2022.

![demostración](./images/pro1.png)
No hay menú do lado esquerdo (área de componentes), encontrado como calculadas de forma **Product Views**. Selecione-as e arraste e solte na tela, no canto superior dirección de la tabla de forma livre.

![demostración](./images/pro2.png)

Automaticamente a dimensão **Day** será adicionada para criar sua primeira tabela. Agora você pode ver sua pergunta respondida imediatamente.

![demostración](./images/pro3.png)

Em, la banda com o botão direito do mouse no resumo da métrica.

![demostración](./images/pro4.png)

Clique em **Visualize** e selecione **Line** como visualização.

![demostración](./images/pro5.png)

Você verá as suas visualizações de produto por dia.

![demostración](./images/pro6.png)

Você pode alterar o escopo de tempo para o dia clicando em **Configuración** na visualización.

![demostración](./images/pro7.png)

Haga clic en el botón del lado de **Línea** y **Administrar el Source de datos**.

![demostración](./images/pro7a.png)

Em, clique em **Lock Selection** e selecione **Selected Items** para esta visualización para que siempre exiba uma linha do tempo de Visualizações de produtos.

![demostración](./images/pro7b.png)

## 5 productos más vistos

Quais são os 5 productos mais vistos?

Lembre-se de guardar o projeto de tempos em tempos.

| Sistema operativo | Método abreviado |
| ----------------- |-------------| 
| Windows | Control + S |
| Mac | Comando + S |

Vamos a encontrar los 5 productos mais vistos. No menu do lado esquerdo, encontre o Nome do produto - Dimensão.

![demostración](./images/pro8.png)

Agora arraste e solte **Nombre de producto** para substituir a dimensión **Día**:

Este será un resultado.

![demostración](./images/pro10a.png)

Em,, tente, um dos produtos por Nome da marca. Pesquise **brandName** e arraste para baixo do primeiro nome do produto.

![demostración](./images/pro13.png)

Em, faça um detallhamento usando o Agente de usuário. Pesquise **agente de usuario** e arraste-o para baixo do nome da marca.

![demostración](./images/pro15.png)

Em, será exibida a tela abaixo:

![demostración](./images/pro15a.png)

Por fim, você pode adicionar mais visualizações. No lado esquerdo, em visualizações, pesquise `Donut`. Pegue `Donut`, arraste e solte na tela sollozar una visualización **Línea** 

![demostración](./images/pro18.png)

A continuación, en la tabla, seleccione las primeras 5 **filas del agente de usuario** del desglose que hicimos en **Google Pixel XL Black Smartphone de 32 GB** > **Citi Signal**. Mientras selecciona las 5 filas, mantenga presionado el botón **CTRL** (en Windows) o el botón **Comando** (en Mac).

Em, na Tabela, selecione as primeiras 5 linhas de **User Agent** do detalhamento que fizemos em **Google Pixel XL 32GB Black Smartphone** > **Citi Signal**. Seleccione como 5 linhas, segure o botão **CTRL** (sin Windows) ou o botão **Comando** (sin Mac).

![demostración](./images/pro20.png)

Você verá o gráfico de donut alterado:

![demostración](./images/pro21.png)

Você pode até o diseño para ser legível, tornando o gráfico de **Line** e o gráfico de **Donut** um pouco menor para que sejam exibidos lado a lado:

![demostración](./images/pro22.png)

Clique no ponto ao lado de *Donut** para **Administrar el Source de datos**. Em, clique em **Lock Selection** para ver la visualización para que siempre exiba uma linha do tempo de Visualizações de produto.

![demostración](./images/pro22b.png)

Saiba mais sobre visualizações usando o Analysis Workspace em:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interação do produto, da visualización à compra

Existem muitas formas de resolver esta pregunta. Uma delas é usar o Tipo de Interação de Produto e usá-lo em uma tabela de formato livre. Utra forma é usar uma **Visualización de abandonos**. Vamos a usar o último, pois e analisar ao mesmo tempo.

Feche o pain actual clicando aquí:

![demostración](./images/pro23.png)

Agregar panel en blanco **o más. Agregar panel en blanco.**

![demostración](./images/pro24.png)

Clique na visualização de **Abandonos**.

![demostración](./images/pro25.png)

Selecione o mesmo de datas do exercício anterior.

![demostración](./images/prodatef.png)

Em, el você va:

![demostración](./images/prodatefa.png)

Encontrar una dimensión **Tipo de evento** nos componentes no lado esquerdo:

![demostración](./images/pro26.png)

Clique na seta para abrir una dimensión:

![demostración](./images/pro27.png)

Você va todos os Tipos de eventos disponíveis.

![demostración](./images/pro28.png)

Selección del artículo **commerce.productViews** e arraste e solte-o no campo **Agregar Touchpoint** dentro de **Visualización de abandonos**.

![demostración](./images/pro29.png)

Faça o mesmo com **commerce.productListAdds** and **commerce.purchases** e solte-os no campo **Add Touchpoint** dentro da **Fallout Visualization**. Sua visualização agora deve ser semelhante ao seguinte:

![demostración](./images/props1.png)

Você pode fazer muitas coisas aqui. Alguno de estos ejemplos: comparar ao longo do tempo, comparar cada passo por dispositivo ou comparar por fidelidade. No entanto, se quisermos analisar coisas interessantes como porque os clientes não compram depois de adicionar um item ao carrinho, podemos usar a melhor ferramenta do CJA: clicar com o botão direito.

Clique com o botão direito do mouse no touchpoint **commerce.productListAdds**. Em, grupo **Abandonos por desglose en este punto de contacto**.

![demostración](./images/pro32.png)

Uma nova tabela de formato livre será criada para analisar o que as pessoas fizeram se não compraram.

![demostración](./images/pro33.png)

Altere o **Tipo de evento** por **Nombre de página**, na nova tabela de formato livre, para ver em quais páginas eles estão indo, em vez da Página de confirmação de compra.

![demostración](./images/pro34.png)

## O que as pessoas fazem no site antes de acessar a página Cancelar servicio?

Novamente, há muitas formas de realizar essa análise. Vamos a usar un análisis de flujo para iniciar parte da descoberta.

Feche o pain actual clicando aquí:

![demostración](./images/pro0.png)

Agregar panel en blanco **o más. Agregar panel en blanco.**

![demostración](./images/pro0a.png)

Haga clic en una visualización **Flujo**.

![demostración](./images/pro35.png)

Em, será exibido:

![demostración](./images/pro351.png)

Selecione o mesmo de datas do exercício anterior.

![demostración](./images/pro0b.png)

Encontrar una dimensión **Page Name** nos componentes no lado esquerdo:

![demostración](./images/pro36.png)

Clique na seta para abrir una dimensión:

![demostración](./images/pro37.png)

Você todas las páginas vistas. Encontre o nome da página: **Cancelar servicio**.
Arraste e solte **Cancel Service** na Visualización de flujo en campo do meio:

![demostración](./images/pro38.png)

Em, será exibido:

![demostración](./images/pro40.png)

Vamos agora analisar se os clientes que visitaram a página C **Cancelar servicio** no site também ligaram para o call center e qual foi o resultado.

Nas dimensões, retorne e encontre Tipo de interação de chamada. Arraste e solte **Tipo de interacción de llamada** para substituir a primeira interação à direita em **Visualización de flujo**.

![demostración](./images/pro43.png)

Agora você visualiza o ticket de soporte dos clientes que ligaram para a central de atendimento depois de visita a página **Cancelar servicio**.

![demostración](./images/pro44.png)

Em, nas dimensões, procure **sensación de llamada**. Arraste e solte para substituir a primeira interação à direita na visualização de fluxo.

![demostración](./images/pro46.png)

Em, será exibido:

![demostración](./images/flow.png)

Como pode ver, execute uma análise omnichannel usando a visualização de fluxo. Graças a isso, descobrimos que some s clientes que estavam pensando em cancelar o serviço tiveram uma avaliação positiva depois de ligar para o call center. Talvez tenhamos mudado de ideia com uma promoção?

## ¿Qué es lo que hace un cliente con un contato de Call center Positivo em relação aos principipais KPI?

Primeiramente, vamos a segmentar los dados para obter apenas usuários com chamadas **positivo**. No CJA, os Segmentos são chamados de Filtros. Acesse para filtros na área de componentes (no lado esquerdo) e clique em **+**.

![demostración](./images/pro58.png)

Dentro del Constructor de Filtro, dê um nome ao filtro

| Nombre | Descripción |
| ----------------- |-------------| 
| Sensación de llamada: positiva | Sensación de llamada: positiva |

![demostración](./images/pro47.png)

Nos componentes (dentro do Constructor de filtro), encontre **Call Feeling** e arraste e solte na Definição do construtor de filtro.

![demostración](./images/pro48.png)

Ágora selecione **positivo** como valor para o filtro.

![demostración](./images/pro49.png)

Altere o escopo para o nível **Persona**.

![demostración](./images/pro50.png)

Para finalizar, basta con hacer clic en **Guardar**.

![demostración](./images/pro51.png)

Então, você irá retornar para esta tela. Se ainda não retornou, feche o pain anterior.

![demostración](./images/pro0c.png)

Agregar panel en blanco **o más. Agregar panel en blanco.**

![demostración](./images/pro24c.png)

Selecione o mesmo de datas do exercício anterior.

![demostración](./images/pro24d.png)

Haga clic en **Tabla de forma libre**.

![demostración](./images/pro52.png)

Agora arraste e solte o filtro que você acabou de criar.

![demostración](./images/pro53.png)

Hora de añadir a las métricas. Comece com **Vistas del producto**. Arraste e solte na tabela de forma livre. Você também pode a la métrica **Eventos**.

![demostración](./images/pro54.png)

Faça o mesmo com **Personas**, **Agregar al carro** e **Compras**. Você vai acabar com uma tabela como a seguinte.

![demostración](./images/pro55.png)

Graças à primeira análise de fluxo, uma nova pergunta surgiu. Então decidimos criar esta tabela e s KPI em um para responder a essa pergunta. Como você pode ver, o tempo de insight é muito mais rápido do que usar SQL ou usar outras soluciones de BI.

## Recapitulación de Analysis Workspace e do Customer Journey Analytics

O Analysis Workspace eliminar todas como limitaciones típicas de una relación de Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões,, e granularidades de tempo) para um projeto. Você pode criar de forma instantánea ânea filtros e analises, gráficos de coorte,, análises de fluxo e relatórios de curadoria e agendamento para comparlhar com qualquer pessoa em seu negócio.

Próxima etapa: [4.6 De insights a ação](./ex6.md)

[Hoteles cerca de Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos los Módulos](./../../overview.md)
