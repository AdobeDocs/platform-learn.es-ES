---
title: Bootcamp - Customer Journey Analytics - Crear una vista de datos - Brasil
description: Customer Journey Analytics - Crear una vista de datos - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Data Views
exl-id: 8cfd4467-167d-4235-a305-4596e3a7d4fb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 2%

---

# 4.3 Crie uma Visualização de Dados

## Objetivos

- Entenda a UI de Visualização de Dados
- Comprender as configurações básicas de definição de visita
- Compre a atribuição e a Persistência em uma Visualização de

## 4.3.1 Visualización de Dados

Agora, com sua conexão concluída, é possível progredir para influenciar a visualização. Uma diferença entre o Adobe Analytics e o CJA é que o CJA precisa de uma visualização de dados para limpar e prepare os dados antes da visualização.

Uma Visualização de Dados é semelhante ao conceito de Virtual Report Suites on Adobe Analytics, onde você estabelece as definições de visita com reconhecimento de contexto, filtragem e também como os componentes são chamados.

Será necesario, no es mínimo, uma Visualização de Dados por conexão. No entanto, para some s casos de uso, é ótimo ter múltiplas Visualizações de Dados para a mesma conexão, com o objetivo de fornecer insights diferentes para equipes distintos. Se você deseja que sua empresa seja por dados, deve a forma como os dados são vistos em cada equipe. Ejemplos de Alguns:

- Métricas de UX apenas para a equipe de UX Design
- Use os mesmos nomes para KPIs e para o Google Analytics e para o Customer Journey Analytics, para que a equipe de análise digital fale apenas 1 idioma.
- Visualização de Dados filtrada para mostrar, por ejemplo, dados para apenas um mercado, ou uma marca, ou apenas para Dispositivos móveis.

Na tela de **Connections** marque a caixa de seleção da conexão que você acabou de criar. Haga clic en **Crear vista de datos**.

![demostración](./images/exta.png)

Você será reorientado para o fluxo de trabalho **Crear vista de datos** flujo de trabajo.

![demostración](./images/0-v2.png)

## 4.3.2 Definición de visualización de dados

Agora você pode as definições básicas para sua Visualização de dados.

![demostración](./images/0-v2.png)

A **Connection** que você criou no exercício anterior já está selecionada. Sua conexão se chama `yourLastName – Omnichannel Data Connection`.

![demostración](./images/ext5.png)

Em, dê um nome à sua Visualização de Dados seguindo este modelo de nomenclatura: `yourLastName – Omnichannel Data View`.

Insira o mesmo valor para a descripción: `yourLastName – Omnichannel Data View`.

| Nombre | Descripción |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![demostración](./images/1-v2.png)

Para **Time Zone**, selecione o fuso horário **Berlim, Estocolmo, Roma, Berna, Bruxelas, Viena, Amsterdã GMT+01:00**. Este é um cenário realmente interessante, pois algumas empresas operam em diferentes países e geografias. Alocar o fuso horário certo para cada país evitará erros típicos de dados, como, por ejemplo, acreditar que a maioria das pessoas compra camisetas às 4h no Peru.

![demostración](./images/ext7.png)

Você também pode modificar a nomenclatura das princippais (Pessoa, Sessão e Evento). Isso não é obrigatório, mas some s clientes gostam de usar Pessoas, Visitas e Acessos em vez de Pessoa, Sessão e Eventos (convención de nomenclatura padrão do Customer Journey Analytics).

Agora você deve ter as seguintes configurações:

![demostración](./images/1-v2.png)

Haga clic en **Guardar y continuar**.

![demostración](./images/12-v2.png)

## 4.3.3 Componentes de visualización de datos

Neste exercício, você va a configurar los componentes necesarios para analizar los dados y visualizá-los usando o Analysis Workspace. Nesta IU, há três áreas principais:

- Lado esquerdo: componentes disponíveis dos datasets selecionados
- Contenido: Componentes adicionados a la visualización de Dados
- Lado direito: Configurações do componente

![demostración](./images/2-v2.png)

>[!IMPORTANT]
>
>Se você não encontrar uma métrica ou dimensão específica, verifique se o campo `Contains data` foi removido de sua visualização de dados. Caso contrario, exclua esse campo.
>
>![demostración](./images/2-v2a.png)

Agora você precisa arrastar e soltar os componentes necesarios para a análise nos **Componentes añadidos**. Para isso, você deve selecionar os componentes no menu à esquerda e arrastá-los e soltá-los na tela no meio.

Vamos comentar com o primeiro componente: **Nombre (web.webPageDetails.name)**. Pesquise esse componente e arraste-o e solte-o na tela.

![demostración](./images/3-v2.png)

Esse componente é o nome da página, como você pode derivar da leitura do campo do schema `(web.webPageDetails.name)`.

No entanto, usar **Name** como o nome não é a melhor convenção de nomenclatura para um usuário corporate compreender rapidamente essa dimensão.

Vamos mudar o nome para **Page Name**. Haga clic en no componente e o renomeie na área **Configuración de componentes**.

![demostración](./images/3-0-v2.png)

As Configurações de persistência são **Configuración de persistencia**. Os conciitos de eVars e prop não existem no CJA, mas as configurações de Persistência possibilitam um comportamento semelhante.

![demostración](./images/3-0-v21.png)

Se você não alterar essas configurações, o CJA a dimensão como um **Prop** (nível de ocorência). Além disso, podemos alterar a Persistência para tornar a dimensão uma **eVar** (persistir o valor ao longo da jornada).

Ver você não estiver familiarizado com eVars e Props, [leia mais sobre isso na documentação](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html)..

Vamos deixar o Nome da Página como Prop. **Configuración de persistencia**.

| Nombre del componente a buscar | Nuevo nombre | Configuración de persistencia |
| ----------------- |-------------| --------------------| 
| Nombre (web.webPageDetails.name) | Nombre de página |          |

Em, escolha a dimensão **phoneNumber** e solte-a na tela. O novo nome deve ser **Número de teléfono**.

![demostración](./images/3-1-v2.png)

Por fim, vamos alterar as Configurações de persistência, pois o Número do Celular deve persistir no nível do usuário.

Para alterar a Persistência, role para baixo no menu à direita e abra a aba **Persistence**:

![demostración](./images/5-v2.png)

Marque a caixa de seleção para modificar as configurações de persistência. **Más reciente** e o escopo **Persona (ventana de informes)**, pois nos preocupamos apenas com o último número de celular da pessoa. Se o cliente não preencher o celular em visitas futuras, você ainda verá esse valor preenchido.

![demostración](./images/6-v2.png)

| Nombre del componente a buscar | Nuevo nombre | Configuración de persistencia |
| ----------------- |-------------| --------------------| 
| phoneNumber | Número de teléfono | Más reciente, persona (ventana de informes) |

O próximo componente é `web.webPageDetails.pageViews.value`.

Sin menú a la esquerda, pesquise `web.webPageDetails.pageViews.value`. Arraste e solte essa métrica na tela.

Modificar el nombre para **Vistas de página** en la **configuración de componentes**.

| Nombre del componente a buscar | Nuevo nombre | Configuración de atribución |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | Page Views |         |

![demostración](./images/7-v2.png)

Para as configurações de atribuição, deixaremos em branco.

Observação: As configurações de persistência nas indicadores também podem ser alteradas no Analysis Workspace. Em algunos s casos, você pode por configurá-las aqui para evitar que os usuários de negócios tenham que pensar qual é o melhor modelo de persistência.

Em, você terá que várias Dimensões e Métricas, na tabela abaixo.

### DIMENSIONES

| Nombre del componente a buscar | Nuevo nombre | Configuración de persistencia |
| ----------------- |-------------| --------------------| 
| brandName | Nombre de marca | Más reciente, sesión |
| sensación de llamada | Sensación de llamada |          |
| ID de llamada | Tipo de interacción de llamada |          |
| callTopic | Tema de llamada | Más reciente, sesión |
| ecid | ECID | Más reciente, persona (ventana de informes) |
| email | ID de correo electrónico | Más reciente, persona (ventana de informes) |
| Tipo de pago | Tipo de pago |          |
| Método de adición de producto | Método de adición de producto | Más reciente, sesión |
| Tipo de evento | Tipo de evento |         |
| Nombre (productListItems.name) | Nombre de producto |         |
| SKU | SKU (sesión) | Más reciente, sesión |
| El ID de transacción | El ID de transacción |         |
| URL (web.webPageDetails.URL) | URL |         |
| Agente de usuario | Agente de usuario | Más reciente, sesión |

### MÉTRICA

| Nombre del componente a buscar | Nuevo nombre | Configuración de atribución |
| ----------------- |-------------| --------------------| 
| Cantidad | Cantidad |          |
| commerce.order.priceTotal | Ingresos |         |

Sua configuração deve ser semelhante ao seguinte:

![demostración](./images/11-v2.png)

Não se esqueça de Salvar sua Visualización de Dados. Então clique em **Guardar**.

![demostración](./images/12-v2s.png)

## 4.3.4 Métricas calculadas

Embora tenhamos organizado todos los componentes na Visualização de dados, você ainda deve algunos deles para que os usuários de negócios estejam prontos para iniciar suas análises.

Se você se lembra, não trouxemos especificamente Métricas como Adicionar ao Carrinho, Visualização do produto ou Compras para a Visualização de dados. Sin entanto, temos uma dimensão chamada: **Tipo de evento**. Então, vamos derivar ess tipos de interação criando 3 calculadas de punto de corte.

Vamos começar com a primeira Métrica: **Vistas del producto**.

No lado esquerdo, pesquise **Event Type** e selecione a dimensão. Em, arraste-o e solte-o na tela **Componentes incluidos**.

![demostración](./images/calcmetr1.png)

Clique para selecionar una nova métrica **Tipo de evento**.

![demostración](./images/calcmetr2.png)

Agora altere o nome e a descripção do componente para os seguintes valores:

| Nombre del componente | Descripción del componente |
| ----------------- |-------------| 
| Vistas del producto | Vistas del producto |

![demostración](./images/calcmetr3.png)

Agora vamos a contar apenas eventos de **Product Views**. Para fazer isso, role para baixo em **Configuración de componentes** até ver Valores de **Incluir valores de exclusión**. Certifique-se de a opção **Establecer valores de inclusión/exclusión**.

![demostración](./images/calcmetr4.png)

Como queremos contar apenas **Vistas del producto**, se han guardado **commerce.productViews** no hay criterios.

![demostración](./images/calcmetr5.png)

Agora a sua métrica calculada está pronta!

Em, repita o mesmo processo para os eventos **Agregar al carro** e **Comprar**.

### Añadir al carro

Primeiro, arraste e solte a mesma dimensión **Tipo de evento**.

![demostración](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois estamos usando a mesma variável. Clique em **Agregar de todos modos**:

![demostración](./images/calcmetr6.png)

Agora, siga o mesmo processo que fizemos para a métrica Visualizações de produto:
- Primeiro altere o nome e a descripção.
- Por fim, adicione **commerce.productListAdds** como criterio para contar apenas Añadir al carrito

| Nombre | Descripción | Criterios |
| ----------------- |-------------| -------------|
| Añadir al carro | Añadir al carro | commerce.productListAdds |

![demostración](./images/calcmetr6a.png)

### Compras

Primeiro, arraste e solte a mesma dimensão **Tipo de evento** como fizemos para as duas.

![demostración](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois estamos usando a mesma variável. Clique em **Agregar de todos modos**:

![demostración](./images/calcmetr7.png)

Agora, siga o mesmo processo que fizemos para as Product Views e Añadir al carrito:
- Primeiro altere o nome e a descripção.
- Por fim, adicione **commerce.purchases** como criterio para calcular el precio de compra como Compras

| Nombre | Descripción | Criterios |
| ----------------- |-------------| -------------|
| Compras | Compras | commerce.purchases |

![demostración](./images/calcmetr7a.png)

Sua configuración final deve ser semelhante ao seguinte. Haz clic en **Guardar y continuar**.

![demostración](./images/calcmetr8.png)

## 4.3.5 Componentes de la configuración de datos

Você deve ser redirecionado para esta tela:

![demostración](./images/8-v2.png)

Nesta aba, você pode modificar algumas configurações importantes para alterar a forma como os dados são processados. Vamos começar definindo o **Tiempo de espera de sesión** como 30 min. Grados de registro de datos y hora de cada evento de experiência, você pode estender o conceito de uma sessão em todos os canais. Por ejemplo, o que acontece se um cliente ligar para o call center depois de visita o site? Usando Tempos Limite de Sessão personalizado, você tem muita flexibilidade para decidir o que é uma sessão e como essa sessão irá mesclar os dados.

![demostración](./images/ext8.png)

Nesta aba você pode modificar outras coisas como os dado um/. Você não precisará fazer isso neste exercício.

![demostración](./images/10-v2.png)

Quando, grupo **Guardar y finalizar**.

![demostración](./images/13-v2.png)

>[!NOTE]
>
>Você pode voltar a esta Visualização de dados posteriormente e alterar as configurações e os componentes a qualquer momento. Como alterações afetarão a forma como os dados históricos são mostrados.

Agora você pode continuar com a parte de visualização e análise!

Próxima etapa: [4.4 Preparación de dados en Customer Journey Analytics](./ex4.md)

[Hoteles cerca de Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos los Módulos](./../../overview.md)
