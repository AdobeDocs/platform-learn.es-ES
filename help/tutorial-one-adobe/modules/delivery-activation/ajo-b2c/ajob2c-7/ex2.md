---
title: 'Offer Decisioning: Configuración de ofertas e ID de decisión'
description: 'Offer Decisioning: Configuración de ofertas e ID de decisión'
kt: 5342
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 13%

---

# 3.7.2 Configurar las ofertas y la decisión

## 3.7.2.1 Crear sus ofertas personalizadas

En este ejercicio, creará cuatro **Ofertas personalizadas**. Estos son los detalles que se deben tener en cuenta al crear esas ofertas:

| Nombre | Date Range | Vínculo de imagen para correo electrónico | Vínculo de imagen para web | Texto | Prioridad | Idoneidad | Idioma | Frecuencia de límite | Nombre de imagen |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|:-------:|:-------:|
| `--aepUserLdap-- - AirPods Max` | hoy - 1 mes después | https://bit.ly/4a9RJ5d | Elija de la biblioteca de Assets | `{{ profile.person.name.firstName }}, 10% discount on AirPods Max` | 25 | todos: mujeres clientes | Inglés (Estados Unidos) | 3 | Apple AirPods Max - Mujer.jpg |
| `--aepUserLdap-- - Galaxy S24` | hoy - 1 mes después | https://bit.ly/3W8yuDv | Elija de la biblioteca de Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy S24` | 15 | todos: mujeres clientes | Inglés (Estados Unidos) | 3 | Galaxy S24 - Mujer.jpg |
| `--aepUserLdap-- - Apple Watch` | hoy - 1 mes después | https://bit.ly/4fGwfxX | https://bit.ly/4fGwfxX | `{{ profile.person.name.firstName }}, 10% discount on Apple Watch` | 25 | todos: clientes hombres | Inglés (Estados Unidos) | 3 | Apple Watch - Hombre.jpg |
| `--aepUserLdap-- - Galaxy Watch 7` | hoy - 1 mes después | https://bit.ly/4gTrkeo | Elija de la biblioteca de Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy Watch 7` | 15 | todos: clientes hombres | Inglés (Estados Unidos) | 3 | Galaxy Watch7 - Hombre.jpg |

{style="table-layout:auto"}

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Pasos siguientes

Vaya a la configuración de [3.7.3 Web SDK para Experience Decisioning](./ex3.md){target="_blank"}

Volver a [Experience Decisioning](ajo-decisioning.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
