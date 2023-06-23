---
title: Bootcamp - Real-time CDP - Cree un segmento y tome medidas - Envíe su segmento a Adobe Target - España
description: Bootcamp - Real-time CDP - Cree un segmento y tome medidas - Envíe su segmento a Adobe Target - España
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 862afd4c-1b6c-48fe-bc1f-967c065642e0
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# 1.4 Ação: envie seu para o Adobe Target

Acceso [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá a página inicial da Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, você precisa selecionar um **espacio aislado**. O nome do sandbox a ser selecionado é Bootcamp. Posible fazer es tan clicando no texto **[!UICONTROL Producción de producción]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropiado, você a tela mudando e agora você está em seu [!UICONTROL espacio aislado] dedicado.

![Ingesta de datos](./images/sb1.png)

## 1.4.1 Active seu para o destino do Adobe Target

O Adobe Target está dispuesto como um destino do CDP em tempo real. Para configurar una integración com o Adobe Target, acesse **Destinos** e **Catálogo**.

Clique em **Personalización** no hay menú **Categorías**. Você va o cartão de destino do **Adobe Target**. Clique em **Activar segmentos**.

![EN](./images/atdest1.png)

Selecione o destino ``Bootcamp Target`` e camarilla **Siguiente**.

![EN](./images/atdest3.png)

Na lista de íveis, selecione o que você criou em [1.3 Crie um](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em, grupo em **Siguiente**.

![EN](./images/atdest8.png)

Na próxima página, clique em **Siguiente**.

![EN](./images/atdest9.png)

Clique em **Finalizar**.

![EN](./images/atdest10.png)

Seu agora está ativado para o Adobe Target.

![EN](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destino do Adobe Target no Real-Time CDP, pode levar até uma hora para que o destino seja ativado. Este é um tempo de espera único desvido à definição da configuración de back-end. Depois que o tempo de espera inicial de 1 hora e a configuração do back-end forem concluídos, os de borda recém-adiciones que são enviado ao destino do Adobe Target estarão disponíveis para segmentação em tempo real.

## 1.4.2 Configuración de la actividad en Adobe Target

Agora que seu Real-Time CDP está configurada para ser publicada en Adobe Target, é possível configurar sua atividade de Segmentação por experiência no Adobe Target. Neste exercício, você va a configurar uma atividade baseada no Compositor de experiencias visuales.

Acceso a la página inicial de Adobe Experience Cloud [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target** para abrir.

![RTCDP](./images/excl.png)

Na página inicial do **Adobe Target**, você verá todas las actividades existentes.
Clique em **+ Crear actividad** para criar uma nova atividade.

![RTCDP](./images/exclatov.png)

Selecione **Segmentación de experiencias**.

![RTCDP](./images/exclatcrxt.png)

Selecione **Visual** e- **URL de actividad** como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, substitua XX por um número entre 01 e 60.

>[!IMPORTANT]
>
>da capacitação deve usar uma página da Web para evitar a colisão de várias experiências do Adobe Target. ¿Qué es lo que buscas? Encuentra una URL de acessando: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas las páginas que comparamos a mesma URL base e terminam com o número do.
>
>Por ejemplo, o 1 deve usar una URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o 30 de los utilizan una URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Seleccione un espacio de trabajo **AT Bootcamp**.

Clique em **Siguiente**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você no está en Compositor de experiencias visuales. Pode levar de 20 a 30 segundos até que o site esteja completamente carregado.

![RTCDP](./images/atform1.png)

Atualmente, o público padrão são **Todos los visitantes**. Clique nos **3 puntos** ao lado de **Todos los visitantes** e clique em **Cambiar audiencia**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de públicos disponibles, e o da Adobe Experience Platform que você criou anteriormente e enviou ao Adobe Target agora faz parte dessa lista. Seleccione una opción o un que você criou anteriormente en Adobe Experience Platform. Clique em **Asignar audiencia**.

![RTCDP](./images/exclatvecchaud.png)

Seu da Adobe Experience Platform agora faz parte dessa Actividad de segmentación por experiencia.

![RTCDP](./images/atform4.png)

Antes de alterar a imagem principal, você deve clicar em **Permitir todo** no banner de cookies.

Para isso, vá para **Examinar**

![RTCDP](./images/cook1.png)

Em, grupo em **Permitir todo**.

![RTCDP](./images/cook2.png)

Em, retorne para **Escribir**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página inicial do site. Clique na imagem principal padrão no site, clique em **Reemplazar contenido** e selecione **Imagen**.

![RTCDP](./images/atform5.png)

Pesquise o arquivo de imagem **rtcdp.png**. Selecione e clique em **Guardar**.

![RTCDP](./images/atform6.png)

Você verá a nova experiência com a nova imagem para o seu Público selecionado

![RTCDP](./images/atform7.png)

Clique no título da sua atividade no canto superior esquerdo para renomeá-la.

![RTCDP](./images/exclatvecname.png)

Para o nome, use:

- `seuSobrenome - RTCDP - XT (VEC)`

Clique em **Siguiente**.

![RTCDP](./images/atform8.png)

Clique em **Siguiente**.

![RTCDP](./images/atform8a.png)

Na página **Objetivos y configuración**, acceso **Métricas de objetivo**.

![RTCDP](./images/atform9.png)

a Meta principal como **Participación** - **Tiempo en el sitio**. Clique em **Guardar y cerrar**.

![RTCDP](./images/vec3.png)

Agora você está na página **Resumen de actividad**. Você ainda precisa sua Atividade.

![RTCDP](./images/atform10.png)

Clique no campo **Inactivo** e selecione **Activar**.

![RTCDP](./images/atform11.png)

Você receberá uma confirmação visual de que sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada no site do bootcamp.

Se agora você voltar ao seu site de demostração e visita a página do produto para **Real-Time CDP**, você se calificará instantaneamente para o que criou e verá a atividade do Adobe Target exibida na página inicial em tempo real.

>[!IMPORTANT]
>
>da capacitação deve usar uma página da Web para evitar a colisão de várias experiências do Adobe Target. Encontrar una URL con un enlace a acessando ao: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas las páginas que comparamos a mesma URL base e terminam com o número do.
>
>Por ejemplo, o 1 deve usar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o 30 de los utilizan una URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Próxima etapa: [1.5 Ação: envie seu para o Facebook](./ex5.md)

[Hoteles cerca de Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos los Módulos](../../overview.md)
