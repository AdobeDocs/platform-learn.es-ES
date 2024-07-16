---
title: Bootcamp - Perfil del cliente en tiempo real - Crear un segmento - UI - España
description: Bootcamp - Perfil del cliente en tiempo real - Crear un segmento - UI - España
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 9b8d93b5-5bed-4600-8602-b438a0893612
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 2%

---

# 1.3 Crie um: interfaz de usuario de la

Neste exercício, você irá criar um Construtor de Segmentos da Adobe Experience Platform.

## História

Acceder a [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá a página inicial da Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, você precisa selecionar um **espacio aislado**. O nome do sandbox a ser selecionado é ``Bootcamp``. No se puede escribir más **[!UICONTROL Production Prod]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropiado, você a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Ingesta de datos](./images/sb1.png)

No hay menú a la sombra, acceda a **Segmentos**. Nesta página, você tem uma visão geral de todos os. Clique no botão + Criar para cometer un crimen o un crimen o un crimen o un crimen o un crimen o un crimen o una.

![Segmentación](./images/menuseg.png)

Quando estiver no novo construtor de, você irá perciber imediatamente a opção de menu **Attributes** e a referência do **XDM Individual Profile**.

![Segmentación](./images/segmentationui.png)

Como o XDM é a linguagem que alimenta o setor de experiência, o XDM também é a base para o construtor de. Todos los dados ingeridos na plataforma devem ser mapeados em relação ao XDM e, portanto, todos los dados se tornam parte do mesmo modelo de dados, independientemente da origem desses dados. Isso oferece uma grande vantagem ao criar, pois a partir dessa interface do usuário do constructor de, é possível dados de qualquer origem no mesmo fluxo de trabalho. Os criados no Construtor de podem ser enviado para soluciones como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativação.

La lista completa de nuestros clientes para ver o producir **Real-Time CDP**.

Para este, você precisa adicionar a Evento de experiência. Você pode encontrar todos los Eventos de experiência clicando no ícone **Eventos** na barra de menu **Campos**.

![Segmentación](./images/findee.png)

Em, você va o nó **XDM ExperienceEvents** do nível superior. Haga clic en **XDM ExperienceEvent**.

![Segmentación](./images/see.png)

Obtener acceso a **elementos de lista de productos**.

![Segmentación](./images/plitems.png)

Selecione **Name** e arraste e solte o objeto **Name** do menu à esquerda na tela do constructor de na seção **Events**. Em, o seguinte será exibido:

![Segmentación](./images/eewebpdtlname.png)

O parâmetro de comparação deve ser **igual a** e, no campo de entrada, insira **Real-time CDP**.

![Segmentación](./images/pv.png)

Siempre que adiciones a un elemento para construir de la, você pode clicar no botão **Actualizar estimación** para obter uma nova estimativa da população em seu.

![Segmentación](./images/refreshest.png)

Para **Método de evaluación**, seleccione **Edge**.

![Segmentación](./images/evedge.png)

Por fim, vamos dar um nome ao seu e salvá-lo.

Como modelo de nomenclatura, use:

- `seuSobrenome - Interest in Real-Time CDP`

Em,, clique no botão **Guardar y cerrar** para guardar la.

![Segmentación](./images/segmentname.png)

Agora você irá retornar à página de visão geral do, onde verá uma visualização de amostra dos perfis de clientes que se calificam para o seu.

![Segmentación](./images/savedsegment.png)

Agora você pode continuar no próximo exercício e usar com o Adobe Target.

Próxima etapa: [1.4 Ação: envie seu para o Adobe Target](./ex4.md)

[Hoteles cerca de Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos los Módulos](../../overview.md)
