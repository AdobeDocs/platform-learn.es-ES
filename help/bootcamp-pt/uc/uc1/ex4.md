---
title: Bootcamp - CDP en tiempo real - Construya un segmento y tome medidas - Envíe su segmento a Adobe Target - Brasil
description: Bootcamp - CDP en tiempo real - Construya un segmento y tome medidas - Envíe su segmento a Adobe Target - Brasil
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 020e9fb8a1d02b93e4e95a4274806c7926c02757
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# 1.4 Ação: envie seu segmento para o Adobe Target

Aceses [Adobe Experience Platform](https://experience.adobe.com/platform). Inicio de sesión en Depois de fazer, você irá acessar a post inicial da Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

precisa selecionar um de continuar, você **entorno limitado**. O nome do sandbox a ser seledado é Bootcamp. É possível fazer isso clicando no texto **[!UICONTROL Producción]** na linha azul na parte superior da tela. Depoes de seleê o sandbox apropiado, vocalista: una tela mutela e agora você está em seu [!UICONTROL entorno limitado] dedicado.

![Ingesta de datos](./images/sb1.png)

## 1.4.1 Ative seu segmento para o destino do Adobe Target

O Adobe Target está disponible como destino o CDP em tempo real. Para configurar sua integrração com o Adobe Target, acesse **Destinos** e **Catálogo**.

Clique **Personalización** sin menú **Categorías**. Você o cartão de destino **Adobe Target**. Clique **Activar segmentos**.

![AT](./images/atdest1.png)

Selecione o destino ``Bootcamp Target`` e clique **Siguiente**.

![AT](./images/atdest3.png)

Na lista de segmentos disponíveis, selecione o segmento que você criou em [1.3 segmento](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em seguida, clique em **Siguiente**.

![AT](./images/atdest8.png)

Na próxima página, clique em **Siguiente**.

![AT](./images/atdest9.png)

Clique **Finalizar**.

![AT](./images/atdest10.png)

Seu segmento agora está ativado para o Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destino do Adobe Target no Real-Time CDP, pode levar até uma hora para que o destino seja ativado. Este é um tempo de único devido à definição da configuração de back-end. Depois que o tempo de espera inicial de 1 hora e a configuração do back-end forem concluidos, os segmentos de borda recém-aditant que são enviados ao do Adobe Target estarão disponíveis para segmentação em tempo real.

## 1.4.2 Configurar sua atividade baseada em formulário do Adobe Target

Agora que seu segmento Real-Time CDP está configurado para ser enviado ao Adobe Target, é possível configurar sua atividade de Segmentação por experiência no Adobe Target. Neste exercício, você irá configurar uma actividade baseada en el Compositor de experiencias visuales.

Acesar una página inicial Adobe Experience Cloud acessando [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique **Target** para abrir.

![RTCDP](./images/excl.png)

En el **Adobe Target** página principal, verá todas las actividades existentes.
Haga clic en **+ Crear actividad** para crear una nueva actividad.
Na página inicial **Adobe Target**, você y as actividades existentes.
Clique **+ Crear actividad** para criar uma nova actividade.

![RTCDP](./images/exclatov.png)

Selecione **Segmentación de experiencias**.

![RTCDP](./images/exclatcrxt.png)

Selecione **Visual** e defina a **URL de actividad** como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, substitua XX por um number entre 01 e 30.

>[!IMPORTANT]
>
>Cada participante da capacitação deve use uma página da Web separada para condensão de várias experiências do Adobe Target. É possível escolher uma página da Web e encontrar un acceso URL: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas como páginas compar una URL mesma base e terminam com o número do participante.
>
>Por ejemplo, o participante 1 deve utilizar una URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar una URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Selección de espacio de trabajo **AT Bootcamp**.

Clique **Siguiente**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você no es Compositor de experiencias visuales. Pode levar de 20 a 30 segundos até que o site esteja cerrado carregado.

![RTCDP](./images/atform1.png)

Atualmente, o público padrão são **Todos los visitantes**. Clique nos **3 puntos** ao lado de **Todos los visitantes** e clique em **Cambiar audiencia**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de públicos disponibles íveis, e o segmento Adobe Experience Platform que você criou anteriormente e enviou ao Adobe Target agora faz parte dessa. Selecione o segmento que você criou anteriormente en Adobe Experience Platform. Clique **Asignar audiencia**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora faz parte dessa Atividade de segmentação por experiência.

![RTCDP](./images/atform4.png)

Antes de alterar una imagen principal, você deve clicar em **Permitir todo** no banner de cookies.

Para isso, vá para **Examinar**

![RTCDP](./images/cook1.png)

Em seguida, clique em **Permitir todo**.

![RTCDP](./images/cook2.png)

Em seguida, réplica para **Componer**.

![RTCDP](./images/cook3.png)

Ágora vamos mudar a imagem principal a inicial página do site. Clique na imagem principal padrão no site, clique em **Reemplazar contenido** e selecione **Imagen**.

![RTCDP](./images/atform5.png)

Pesquise o arquivo de imagem **rtcdp.png**. Selecione e clique em **Guardar**.

![RTCDP](./images/atform6.png)

Você a nova experiência com nova imagem para o seu Público seledado

![RTCDP](./images/atform7.png)

Clique no título sua atividade no canto superior esquerdo para renomeá-la.

![RTCDP](./images/exclatvecname.png)

Para obtener el nombre, utilice:

- `yourLastName - RTCDP - XT (VEC)`

Clique **Siguiente**.

![RTCDP](./images/atform8.png)

Clique **Siguiente**.

![RTCDP](./images/atform8a.png)

Na página **Objetivos y configuración**, acesse **Métricas de objetivo**.

![RTCDP](./images/atform9.png)

Defina un metaprincipal como **Participación** - **Tiempo en el sitio**. Clique **Guardar y cerrar**.

![RTCDP](./images/vec3.png)

Agora você está na página **Información general de actividad**. Você ainda precisa ativar sua Atividade.

![RTCDP](./images/atform10.png)

Clique no campo **Inactivo** e selecione **Activar**.

![RTCDP](./images/atform11.png)

Você receberá uma confirmação visual de que sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada no site do bootcamp.

Se agora você voltar ao seu site de demostração e visitar a página do produto para **Real-Time CDP**, você se cualificará instantaneamente para o segmento que criou e verá a actividade do Adobe Target exibida na superior inicial em tempo real.

>[!IMPORTANT]
>
>Cada participante da capacitação deve use uma página da Web separada para condensão de várias experiências do Adobe Target. É possível escolher uma página da Web e encontrar un enlace URL acessando ao: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas como páginas compar una URL mesma base e terminam com o número do participante.
>
>Por exemplo o participante 1 deve utilizar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o participante 30 deve usar una URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Próxima etapa: [1.5 Acción: enviar el segmento a Facebook](./ex5.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos los Módulos](../../overview.md)
