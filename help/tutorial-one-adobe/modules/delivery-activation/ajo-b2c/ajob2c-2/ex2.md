---
title: 'Adobe Journey Optimizer: API meteorológica externa, acción de SMS y más: definición de una fuente de datos externa'
description: 'Adobe Journey Optimizer: API meteorológica externa, acción de SMS y más: definición de una fuente de datos externa'
kt: 5342
doc-type: tutorial
exl-id: 0ad27ffb-51fe-4bd1-b0be-feeb232039fa
source-git-commit: d19bd2e39c7ff5eb5c99fc7c747671fb80e125ee
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 4%

---

# 3.2.2 Definición de una fuente de datos externa

En este ejercicio, creará una fuente de datos externa personalizada utilizando Adobe Journey Optimizer.

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

En el menú de la izquierda, desplácese hacia abajo y haga clic en **Configuraciones**. A continuación, haga clic en el botón **Administrar** en **Fuentes de datos**.

![Demostración](./images/menudatasources.png)

Verá la lista **Fuentes de datos**.
Haga clic en **Crear Source de datos** para empezar a agregar la fuente de datos.

![Demostración](./images/dshome.png)

Verá una fuente de datos emergente vacía.

![Demostración](./images/emptyds.png)

Antes de comenzar a configurar esto, necesitas una cuenta con el servicio **Abrir mapa del tiempo**. Siga estos pasos para crear su cuenta de y obtener su clave de API.

Vaya a [https://openweathermap.org/](https://openweathermap.org/). En la página de inicio, haz clic en **Iniciar sesión**.

![Mapa del tiempo](./images/owm.png)

Haga clic en **Crear una cuenta**.

![Mapa del tiempo](./images/owm1.png)

Complete los detalles. Haga clic en **Crear cuenta**.

![Mapa del tiempo](./images/owm2.png)

A continuación, se le redirigirá a la página de su cuenta.

![Mapa del tiempo](./images/owm4.png)

En el menú, haga clic en **Claves de API** para recuperar su clave de API, que deberá configurar su origen de datos externo personalizado.

![Mapa del tiempo](./images/owm5.png)

Una **clave API** tiene el siguiente aspecto: `b2c4c36b6bb59c3458d6686b05311dc3`.

Puedes encontrar la **Documentación de la API** para el **Tiempo actual** [aquí](https://openweathermap.org/current).

Para este caso de uso, implementará la conexión con Open Weather Map en función de la ciudad en la que se encuentra el cliente, usando la **solicitud de API integrada por nombre de ciudad**.

![Mapa del tiempo](./images/owm6.png)

Vuelva a **Adobe Journey Optimizer**, a la ventana emergente **Source de datos externos** vacía.

![Demostración](./images/emptyds.png)

Como nombre para el origen de datos, use `--aepUserLdap--WeatherApi`.

Definir descripción en: `Access to the Open Weather Map`.

La dirección URL de la API de Open Weather Map es: `http://api.openweathermap.org/data/2.5/weather?units=metric`.

![Demostración](./images/dsname.png)

A continuación, debe seleccionar la Autenticación que desea utilizar.

Utilice estas variables:

| Campo | Valor |
|:-----------------------:| :-----------------------|
| Tipo | **Clave de API** |
| Nombre | **APPID** |
| Valor | **su clave API** |
| Ubicación | **Parámetro de consulta** |

![Demostración](./images/dsauth.png)

Finalmente, debe definir un **FieldGroup**, que es básicamente la solicitud que enviará a la API meteorológica. En nuestro caso, queremos usar el nombre de la Ciudad para solicitar el Tiempo Actual para esa Ciudad.

![Demostración](./images/fg.png)

Según la documentación de la API meteorológica, debe enviar un parámetro `q=City`.

![Demostración](./images/owmapi.png)

Para que coincida con la solicitud de API esperada, configure el grupo de campos de la siguiente manera:

>[!IMPORTANT]
>
>El nombre del grupo de campos debe ser único, use esta convención de nomenclatura: `--aepUserLdap--WeatherByCity`

![Demostración](./images/fg1.png)

Para la carga de respuesta, debe pegar un ejemplo de la respuesta que enviará la API meteorológica.

Puede encontrar la respuesta JSON de API esperada en la página Documentación de API [aquí](https://openweathermap.org/current), en el asunto **JSON**.

![Demostración](./images/owmapi1.png)

O puede copiar la respuesta JSON desde aquí:

```json
{
   "coord": {
      "lon": 7.367,
      "lat": 45.133
   },
   "weather": [
      {
         "id": 501,
         "main": "Rain",
         "description": "moderate rain",
         "icon": "10d"
      }
   ],
   "base": "stations",
   "main": {
      "temp": 284.2,
      "feels_like": 282.93,
      "temp_min": 283.06,
      "temp_max": 286.82,
      "pressure": 1021,
      "humidity": 60,
      "sea_level": 1021,
      "grnd_level": 910
   },
   "visibility": 10000,
   "wind": {
      "speed": 4.09,
      "deg": 121,
      "gust": 3.47
   },
   "rain": {
      "1h": 2.73
   },
   "clouds": {
      "all": 83
   },
   "dt": 1726660758,
   "sys": {
      "type": 1,
      "id": 6736,
      "country": "IT",
      "sunrise": 1726636384,
      "sunset": 1726680975
   },
   "timezone": 7200,
   "id": 3165523,
   "name": "Province of Turin",
   "cod": 200
}    
```

Copie la respuesta JSON anterior en el portapapeles y, a continuación, vaya a la pantalla de configuración de la fuente de datos personalizada.

Haga clic en el icono **Editar carga útil**.

![Demostración](./images/owmapi2.png)

Verá una ventana emergente en la que ahora tiene que pegar la respuesta JSON anterior.

![Demostración](./images/owmapi3.png)

Pegue la respuesta JSON, después de lo cual verá esto. Haga clic en **Guardar**.

![Demostración](./images/owmapi4.png)

Se ha completado la configuración de la fuente de datos personalizada. Desplácese hacia arriba y haga clic en **Guardar**.

![Demostración](./images/dssave.png)

Su origen de datos se ha creado correctamente y forma parte de la lista **Fuentes de datos**.

![Demostración](./images/dslist.png)

## Pasos siguientes

Ir a [3.2.3 Definir una acción personalizada](./ex3.md){target="_blank"}

Volver a [Adobe Journey Optimizer: fuentes de datos externas y acciones personalizadas](journey-orchestration-external-weather-api-sms.md){target="_blank"}

Volver a [Todos los módulos](./../../../../overview.md){target="_blank"}
