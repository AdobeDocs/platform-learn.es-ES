---
title: 'Adobe Journey Optimizer: API meteorológica externa, acción de SMS y más: definición de una fuente de datos externa'
description: 'Adobe Journey Optimizer: API meteorológica externa, acción de SMS y más: definición de una fuente de datos externa'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 3%

---

# 3.2.2 Definición de una fuente de datos externa

En este ejercicio, creará una fuente de datos externa personalizada utilizando Adobe Journey Optimizer.

Inicie sesión en Adobe Journey Optimizer en [Adobe Experience Cloud](https://experience.adobe.com). Haga clic en **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Se le redirigirá a la vista **Inicio** en Journey Optimizer. Primero, asegúrese de que está usando la zona protegida correcta. La zona protegida que se va a usar se llama `--aepSandboxName--`. Para cambiar de una zona protegida a otra, haga clic en **PRODUCTION Prod (VA7)** y seleccione la zona protegida en la lista. En este ejemplo, la zona protegida se denomina **Habilitación de AEP para el año fiscal 22**. Estará en la vista **Inicio** de su zona protegida `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

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

Complete los detalles.

![Mapa del tiempo](./images/owm2.png)

Haga clic en **Crear cuenta**.

![Mapa del tiempo](./images/owm3.png)

A continuación, se le redirigirá a la página de su cuenta.

![Mapa del tiempo](./images/owm4.png)

En el menú, haga clic en **Claves de API** para recuperar su clave de API, que deberá configurar su origen de datos externo personalizado.

![Mapa del tiempo](./images/owm5.png)

Una **clave API** tiene el siguiente aspecto: `b2c4c36b6bb59c3458d6686b05311dc3`.

Puedes encontrar la **Documentación de la API** para el **Tiempo actual** [aquí](https://openweathermap.org/current).

En nuestro caso de uso, implementaremos la conexión con Open Weather Map en función de la ciudad en la que se encuentra el cliente.

![Mapa del tiempo](./images/owm6.png)

Vuelva a **Adobe Journey Optimizer**, a la ventana emergente **Source de datos externos** vacía.

![Demostración](./images/emptyds.png)

Como nombre para el origen de datos, use `--aepUserLdap--WeatherApi`. En este ejemplo, el nombre del origen de datos es `vangeluwWeatherApi `.

Definir descripción en: `Access to the Open Weather Map`.

La dirección URL de la API de Open Weather Map es: **http://api.openweathermap.org/data/2.5/weather?units=metric**

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

Según la documentación de la API meteorológica, necesitamos enviar un parámetro `q=City`.

![Demostración](./images/owmapi.png)

Para que coincida con la solicitud de API esperada, configure el grupo de campos de la siguiente manera:

>[!IMPORTANT]
>
>El nombre del grupo de campos debe ser único, use esta convención de nomenclatura: `--aepUserLdap--WeatherByCity`, así que en este caso, el nombre debe ser `vangeluwWeatherByCity`

![Demostración](./images/fg1.png)

Para la carga de respuesta, debe pegar un ejemplo de la respuesta que enviará la API meteorológica.

Puede encontrar la respuesta JSON de API esperada en la página Documentación de API [aquí](https://openweathermap.org/current).

![Demostración](./images/owmapi1.png)

O puede copiar la respuesta JSON desde aquí:

```json
{"coord": { "lon": 139,"lat": 35},
  "weather": [
    {
      "id": 800,
      "main": "Clear",
      "description": "clear sky",
      "icon": "01n"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 281.52,
    "feels_like": 278.99,
    "temp_min": 280.15,
    "temp_max": 283.71,
    "pressure": 1016,
    "humidity": 93
  },
  "wind": {
    "speed": 0.47,
    "deg": 107.538
  },
  "clouds": {
    "all": 2
  },
  "dt": 1560350192,
  "sys": {
    "type": 3,
    "id": 2019346,
    "message": 0.0065,
    "country": "JP",
    "sunrise": 1560281377,
    "sunset": 1560333478
  },
  "timezone": 32400,
  "id": 1851632,
  "name": "Shuzenji",
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

Paso siguiente: [3.2.3 Definir una acción personalizada](./ex3.md)

[Volver al módulo 3.2](journey-orchestration-external-weather-api-sms.md)

[Volver a todos los módulos](../../../overview.md)
