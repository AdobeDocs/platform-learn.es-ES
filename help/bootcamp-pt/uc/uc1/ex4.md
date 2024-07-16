---
title: Bootcamp - Real-time CDP - Cree un segmento y tome medidas - Envíe su segmento a Adobe Target - España
description: Bootcamp - Real-time CDP - Cree un segmento y tome medidas - Envíe su segmento a Adobe Target - España
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Segments, Integrations
exl-id: 862afd4c-1b6c-48fe-bc1f-967c065642e0
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# 1.4 Ação: envie seu para o Adobe Target

Acceder a [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá a página inicial da Adobe Experience Platform.

![Ingesta de datos](./images/home.png)

Antes de continuar, você precisa selecionar um **espacio aislado**. O nome do sandbox a ser selecionado é Bootcamp. No se puede escribir más **[!UICONTROL Production Prod]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropiado, você a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Ingesta de datos](./images/sb1.png)

## 1.4.1 Active seu para o destino do Adobe Target

O Adobe Target está dispuesto como um destino do CDP em tempo real. Para configurar una integración com en Adobe Target, acceda a **Destinos** y **Catálogo**.

Clique em **Personalization** en el menú **Categorías**. Você verá o cartão de destino do **Adobe Target**. Haga clic en **Activar segmentos**.

![A LAS](./images/atdest1.png)

Selecione o destino ``Bootcamp Target`` e clique **Siguiente**.

![A LAS](./images/atdest3.png)

Na lista de íveis, selecione o que você criou em [1.3 Crie um](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em, grupo **Siguiente**.

![A LAS](./images/atdest8.png)

En la próxima página, grupo **Siguiente**.

![A LAS](./images/atdest9.png)

Clique em **Finalizar**.

![A LAS](./images/atdest10.png)

Seu agora está ativado para o Adobe Target.

![A LAS](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destino do Adobe Target no Real-Time CDP, pode levar até uma hora para que o destino seja ativado. Este é um tempo de espera único desvido à definição da configuración de back-end. Depois que o tempo de espera inicial de 1 hora e a configuração do back-end forem concluídos, os de borda recém-adiciones que são enviado ao destino do Adobe Target estarão disponíveis para segmentação em tempo real.

## 1.4.2 Configuración de la actividad en Adobe Target

Agora que seu Real-Time CDP está configurada para ser publicada en Adobe Target, é possível configurar sua atividade de Segmentação por experiência no Adobe Target. Neste exercício, você va a configurar uma atividade baseada no Compositor de experiencias visuales.

Acceder a la página inicial de Adobe Experience Cloud accediendo a [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target** para abrir.

![RTCDP](./images/excl.png)

Na página inicial do **Adobe Target**, você verá todas las actividades existentes.
Haz clic en **+ Crear actividad** para ver la actividad de uma nova.

![RTCDP](./images/exclatov.png)

Seleccione **Segmentación de experiencias**.

![RTCDP](./images/exclatcrxt.png)

Selecione **Visual** e a **URL de actividad** como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, substitua XX por um número entre 01 e 60.

>[!IMPORTANT]
>
>da capacitação deve usar uma página da Web para evitar a colisão de várias experiências do Adobe Target. Encontrar una URL accediendo a: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas las páginas que comparamos a mesma URL base e terminam com o número do.
>
>Por ejemplo, o 1 deve usar una dirección URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o bien, 30 deve usar una dirección URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Seleccione el espacio de trabajo **AT Bootcamp**.

Clique em **Siguiente**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você no está en Compositor de experiencias visuales. Pode levar de 20 a 30 segundos até que o site esteja completamente carregado.

![RTCDP](./images/atform1.png)

Atualmente, o público padrão são **Todos los visitantes**. Clique nos **3 puntos** ao lado de **Todos los visitantes** e clique em **Cambiar audiencia**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de públicos disponibles, e o da Adobe Experience Platform que você criou anteriormente e enviou ao Adobe Target agora faz parte dessa lista. Seleccione una opción o un que você criou anteriormente en Adobe Experience Platform. Clique em **Asignar audiencia**.

![RTCDP](./images/exclatvecchaud.png)

Seu da Adobe Experience Platform agora faz parte dessa Actividad de segmentación por experiencia.

![RTCDP](./images/atform4.png)

Antes de alterar una imagen principal, você deve clicar em **Permitir todas** sin banner de cookies.

Para isso, vá para **Examinar**

![RTCDP](./images/cook1.png)

Em, grupo **Permitir todos**.

![RTCDP](./images/cook2.png)

Em, restaurado para **Componer**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página inicial do site. Clique na imagem principal padrão en el sitio, clique em **Reemplazar contenido** e selecione **Imagen**.

![RTCDP](./images/atform5.png)

Pesquise o arquivo de imagem **rtcdp.png**. Selecciona un grupo **Guardar**.

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

En la página **Objetivos y configuración**, acceda a **Métricas de objetivos**.

![RTCDP](./images/atform9.png)

una meta principal como **Participación** - **Tiempo en el sitio**. Haz clic en **Guardar y cerrar**.

![RTCDP](./images/vec3.png)

Agora você está en la página **Resumen de la actividad**. Você ainda precisa sua Atividade.

![RTCDP](./images/atform10.png)

Clique no campo **Inactivo** e selecione **Activar**.

![RTCDP](./images/atform11.png)

Você receberá uma confirmação visual de que sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada no site do bootcamp.

Se agora você voltar ao seu site de demostração e visita a página do produto para **Real-Time CDP**, você se calificará instantaneamente para o que criou e verá a atividade do Adobe Target exibida na página inicial em tempo real.

>[!IMPORTANT]
>
>da capacitação deve usar uma página da Web para evitar a colisão de várias experiências do Adobe Target. Encontrar una URL con el enlace: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas las páginas que comparamos a mesma URL base e terminam com o número do.
>
>Por ejemplo, o 1 deve usar un(a) `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, o 30 deve usar una URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Próxima etapa: [1.5 Ação: envie seu para o Facebook](./ex5.md)

[Hoteles cerca de Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos los Módulos](../../overview.md)
