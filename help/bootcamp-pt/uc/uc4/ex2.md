---
title: Bootcamp - Customer Journey Analytics - Conectar conjuntos de datos de Adobe Experience Platform en Customer Journey Analytics - Brasil
description: Bootcamp - Customer Journey Analytics - Conectar conjuntos de datos de Adobe Experience Platform en Customer Journey Analytics - Brasil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 51078fca-f234-4e50-96ba-ee7f5e286869
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 4.2 Colocar los conjuntos de datos en Adobe Experience Platform sin Customer Journey Analytics

## Objetivos

- Comprender la IU da conexão de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda a ID da pessoa e a compilação de dados
- Aprenda o concepto de streaming de datos sin Recorrido del cliente

## 4.2.1 Conexão

Acceder a [analytics.adobe.com](https://analytics.adobe.com) para obtener acceso al Customer Journey Analytics.

Página inicial del Customer Journey Analytics, acceso **Connections**.

![demostración](./images/cja2.png)

Aquí você pode ver todas as diferentes conexões feitas entre o CJA e a Plataforma. Essas conexões têm o mesmo objetivo dos conjuntos de relatórios en Adobe Analytics. No entanto, a coleta dos dados é completamente diferente. Todos los dados vêm de datasets da Adobe Experience Platform.

Vamos criar sua primeira conexão. Haga clic en **Crear nueva conexión**.

![demostración](./images/cja4.png)

Você tiene una interfaz de usuario **Crear conexión**.

![demostración](./images/cja5.png)

Agora você pode dar um nome à sua conexão.

Usar este modelo de nomenclatura: `yourLastName – Omnichannel Data Connection`.

Ejemplo: `vangeluw - Omnichannel Data Connection`

Você também deve selecionar o sandbox correto para usar. No hay zona protegida de menú, zona protegida selecione seu, que deve ser `Bootcamp`. Neste ejemplo, o sandbox a ser usado é **Bootcamp**. El você também define la definición de **Cantidad promedio de eventos diarios** a **menos de 1 millón**.

![demostración](./images/cjasb.png)

Após selecionar seu sandbox, você pode começar a adicionar datasets a esta conexão. Haga clic en **Agregar conjuntos de datos**.

![demostración](./images/cjasb1.png)

## 4.2.2 Conjuntos de datos de Selecione da Adobe Experience Platform

Pesquise del conjunto de datos `Demo System - Event Dataset for Website (Global v1.1)`. Clique em **+** para agregar a dataset a esta conexão.

![demostración](./images/cja7.png)

Agora pesquise e marque as caixas de seleção `Demo System - Event Dataset for Voice Assistants (Global v1.1)` y `Demo System - Event Dataset for Call Center (Global v1.1)`.

Em, el você va a tela abaixo. Clique em **Siguiente**.

![demostración](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID da pessoa

Conjuntos de datos de O target agora é juntar ess. Para cada dataset selecionado, você verá um campo chamado **ID de persona**. Cada dataset tem seu prio campo de ID de pessoa.

![demostración](./images/cja11.png)

Como você pode ver, a maioria deles tem o ID da pessoa selecionado automáticamente. Isso ocore porque um identificador principal é selecionado em cada esquema na Adobe Experience Platform. Como ejemplo, aquí está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`, onde você pode ver que o servicio Primário está definido como `phoneNumber`.

![demostración](./images/cja13.png)

No entanto, você ainda pode influenciar qual identificador utilizado para compilar conjuntos de datos para sua conexão. Você pode usar qualquer no se ha configurado un conjunto de datos vinculado a sí mismo. Clique no menu suspenso para los IDs de la empresa disponíveis em cada dataset.

![demostración](./images/cja14.png)

, você pode diferentes IDs de pessoa para cada dataset. Isso conjuntos de datos de múltiplas origins en CJA. Imagine trazer NPS ou dados de pesquisa que seriam muito interessantes e úteis para compreender o contexto e o motivo de um mento.

O nome do campo ID da pessoa não é importante, desde que o valor nos campos ID da pessoa. Digamos que temos `email` em um dataset e `emailAddress` em outro dataset definido como ID da pessoa. Se `delaigle@adobe.com` tiver o mesmo valor para o campo ID da pessoa em ambos os datasets, o CJA poderá compilar os dados.

Atualmente, existem algumas outras limitações, como compilar o comportamento anônimo para conhecido. Consultar como perguntas frecuentes aquí: [FAQ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html).


### Compilando os dados usando o ID da pessoa

Agora que você compreende o conceito de compilar datasets usando o ID da pessoa, vamos escolher `email` como ID da pessoa para cada dataset.

![demostración](./images/cja15.png)

Acceso a cada conjunto de datos para personalizar o ID da pessoa.

![demostración](./images/cja12a.png)

Agora preencha o campo ID da pessoa escolhendo o `email` na lista suspensa.

![demostración](./images/cja17.png)

Depois de compilar os três datasets, estamos prontos para continuar.

| conjunto de datos | ID de persona |
| ----------------- |-------------| 
| Sistema de demostración: conjunto de datos de eventos para el sitio web (Global v1.1) | email |
| Sistema de demostración: conjunto de datos de eventos para asistentes de voz (Global v1.1) | email |
| Sistema de demostración: conjunto de datos de eventos para el centro de llamadas (Global v1.1) | email |

Você também precisa garantir que, para cada dataset, essas opções estejam habilitadas:

- Importar todos los novos dados
- Preencher todos os dados existentes
- Preencher tipo de fonte de dados com &quot;Otros&quot;
- Preencher a descripção com o mesmo nome do Conjunto de datos

Haga clic en **Agregar conjuntos de datos**.

![demostración](./images/cja16.png)

Clique em **Guardar** e vá para o próximo ejercicio. Depois de criar sua **Connection**, pode levar algumas horas até que seus dados estejam dispuesto no es CJA.

![demostración](./images/cja20.png)

Próxima etapa: [4.3 Crie uma Visualização de Dados](./ex3.md)

[Hoteles cerca de Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos los Módulos](./../../overview.md)
