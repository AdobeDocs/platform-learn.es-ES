---
title: Foundation - Perfil del cliente en tiempo real - Visualice su propio perfil de cliente en tiempo real - API
description: Foundation - Perfil del cliente en tiempo real - Visualice su propio perfil de cliente en tiempo real - API
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '2637'
ht-degree: 1%

---

# 2.1.3 Visualice su propio perfil de cliente en tiempo real: API

En este ejercicio, utilizará Postman y Adobe I/O para consultar las API de Adobe Experience Platform y ver su propio perfil de cliente en tiempo real.

## Historia

En el Perfil del cliente en tiempo real, todos los datos de perfil se muestran junto con los datos de evento, así como las suscripciones a segmentos existentes. Los datos mostrados pueden proceder de cualquier lugar, de aplicaciones de Adobe y soluciones externas. Esta es la vista más potente de Adobe Experience Platform, el sistema de registro de experiencias.

El perfil del cliente en tiempo real lo pueden consumir todas las aplicaciones de Adobe, pero también soluciones externas como centros de llamadas o aplicaciones de clientelización en tienda. La manera de hacerlo es conectar esas soluciones externas a las API de Adobe Experience Platform.

## 2.1.3.1 Sus identificadores

En el panel Visor de perfiles del sitio web, puede encontrar varias identidades. Cada identidad está vinculada a un área de nombres.

![Perfil del cliente](./images/identities.png)

En el panel de rayos X, podemos ver 4 combinaciones diferentes de ID y áreas de nombres:

| Identidad | Área de nombres |
|:-------------:| :---------------:|
| ID DEL Experience Cloud (ECID) | 12507560687324495704459439363261812234 |
| ID de correo electrónico | woutervangeluwe+06022022-01@gmail.com |
| Identificador de número de móvil | +32473622044+06022022-01 |

Recuerde estos identificadores para el siguiente paso.

Con estos ID en mente, vaya a Postman.

## 2.1.3.2 Configuración del proyecto de Adobe I/O

En este ejercicio utilizará Adobe I/O de forma bastante intensiva para consultar las API de Platform. Siga los siguientes pasos para configurar el Adobe I/O.

Ir a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home)

![Nueva integración de Adobe I/O](./images/iohome.png)

Asegúrese de seleccionar la instancia de Adobe Experience Platform correcta en la esquina superior derecha de la pantalla. Su instancia es `--envName--`.

![Nueva integración de Adobe I/O](./images/iocomp.png)

Haga clic en **Crear nuevo proyecto**.

![Adobe I/O Nueva integración](./images/adobe_io_new_integration.png) o
![Nueva integración de Adobe I/O](./images/adobe_io_new_integration1.png)

Seleccione **+ Agregar al proyecto** y seleccione **API**.

![Nueva integración de Adobe I/O](./images/adobe_io_access_api.png)

A continuación, verá esto:

![Nueva integración de Adobe I/O](./images/api1.png)

Haz clic en el icono **Adobe Experience Platform**.
/images/api2.png)

Haga clic en **API de Experience Platform**.

![Nueva integración de Adobe I/O](./images/api3.png)

Haga clic en **Next**.

![Nueva integración de Adobe I/O](./images/next.png)

Ahora puede optar por que Adobe I/O genere el par de claves de seguridad o cargar uno existente.

Elija **Opción 1 - Generar un par de claves**.

![Nueva integración de Adobe I/O](./images/api4.png)

Haga clic en **Generar par de claves**.

![Nueva integración de Adobe I/O](./images/generate.png)

Verás un spinner por unos 30 segundos.

![Nueva integración de Adobe I/O](./images/spin.png)

Verá esto y el par de claves generado se descargará como archivo zip: **config.zip**.

Descomprima el archivo **config.zip** en su escritorio y verá que contiene 2 archivos:

![Nueva integración de Adobe I/O](./images/zip.png)

- **certificate_pub.crt** es su certificado de clave pública. Desde el punto de vista de la seguridad, este es el certificado que se utiliza libremente para configurar integraciones con aplicaciones en línea.
- **private.key** es su clave privada. Esto nunca, nunca debe ser compartido con nadie. La clave privada es lo que utiliza para autenticarse en la implementación de la API y se supone que es un secreto. Si comparte la clave privada con cualquier persona, puede acceder a su implementación y utilizar la API para introducir datos maliciosos en Platform y extraer todos los datos que se encuentran en Platform.

![Nueva integración de Adobe I/O](./images/config.png)

Asegúrese de guardar el archivo **config.zip** en una ubicación segura, ya que lo necesitará para los siguientes pasos y para acceder en el futuro a las API de Adobe Experience Platform y de Adobe I/O.

Haga clic en **Next**.

![Nueva integración de Adobe I/O](./images/next.png)

Ahora tiene que seleccionar los **perfiles de producto** para su integración.

Seleccione los perfiles de producto necesarios.

**Para su información**: en su instancia de Adobe Experience Platform, los perfiles de producto tendrán un nombre diferente. Debe seleccionar al menos un perfil de producto con los derechos de acceso adecuados, que se configuran en Adobe Admin Console.

![Nueva integración de Adobe I/O](./images/api9.png)

Haga clic en **Guardar API configurada**.

![Nueva integración de Adobe I/O](./images/saveconfig.png)

Verás un giro por un par de segundos.

![Nueva integración de Adobe I/O](./images/api10.png)

Y a continuación, verá su integración.

![Nueva integración de Adobe I/O](./images/api11.png)

Haga clic en el botón **Descargar para Postman** y, a continuación, haga clic en **Cuenta de servicio (JWT)** para descargar un entorno de Postman (espere hasta que se descargue el entorno, puede tardar un par de segundos).

![Nueva integración de Adobe I/O](./images/iopm.png)

Desplácese hacia abajo hasta que vea **Service Account (JWT)**, que es donde puede encontrar todos los detalles de integración que se utilizan para configurar la integración con Adobe Experience Platform.

![Nueva integración de Adobe I/O](./images/api12.png)

Su proyecto de IO tiene actualmente un nombre genérico. Debe asignar un nombre descriptivo a la integración. Haga clic en **Proyecto 1** (o nombre similar) como se indica

![Nueva integración de Adobe I/O](./images/api13.png)

Haga clic en **Editar proyecto**.

![Nueva integración de Adobe I/O](./images/api14.png)

Introduzca un nombre y una descripción para la integración. Como convención de nombres, utilizaremos `AEP API --aepUserLdap--`. Reemplace ldap por su ldap.
Por ejemplo, si su ldap es vangeluw, el nombre y la descripción de la integración se convierten en vangeluw de la API de AEP.

Escriba `AEP API --aepUserLdap--` como **Título del proyecto**. Haga clic en **Guardar**.

![Nueva integración de Adobe I/O](./images/api15.png)

La integración de Adobe I/O ha finalizado.

![Nueva integración de Adobe I/O](./images/api16.png)

## 2.1.3.3 Autenticación de Postman en el Adobe I/O

Vaya a [https://www.getpostman.com/](https://www.getpostman.com/).

Haz clic en **Comenzar**.

![Nueva integración de Adobe I/O](./images/getstarted.png)

A continuación, descargue e instale Postman.

![Nueva integración de Adobe I/O](./images/downloadpostman.png)

Después de la instalación de Postman, inicie la aplicación.

En Postman, hay 2 conceptos: entornos y colecciones.

- El entorno contiene todas las variables de entorno que son más o menos coherentes. En el entorno, encontrará cosas como la organización IMS de nuestro entorno de plataforma, junto con credenciales de seguridad como su clave privada y otras. El archivo de entorno es el que descargó durante la configuración de Adobe I/O del ejercicio anterior. Su nombre es: **service.postman_environment.json**.

- La colección contiene una serie de solicitudes de API que puede utilizar. Utilizaremos 2 colecciones
   - 1 colección para autenticación en Adobe I/0
   - 1 Colección para los ejercicios de este módulo
   - 1 colección para los ejercicios del módulo Real-Time CDP, para la creación de destinos

Descargue el archivo [postman.zip](./../../../assets/postman/postman_profile.zip) en su escritorio local.

En este archivo **postman.zip** encontrará los siguientes archivos:

- `_Adobe I-O - Token.postman_collection.json`
- `_Adobe Experience Platform Enablement.postman_collection.json`
- `Destination_Authoring_API.json`

Descomprima el archivo **postman.zip** y almacene estos 3 archivos en una carpeta del equipo de escritorio, junto con el entorno de Postman descargado del Adobe I/O. Debe tener estos 4 archivos en esa carpeta:

![Nueva integración de Adobe I/O](./images/pmfolder.png)

Vuelva a Postman. Haga clic en **Importar**.

![Nueva integración de Adobe I/O](./images/postmanui.png)

Haga clic en **Cargar archivos**.

![Nueva integración de Adobe I/O](./images/choosefiles.png)

Vaya a la carpeta del escritorio en la que extrajo los 4 archivos descargados. Seleccione estos 4 archivos al mismo tiempo y haga clic en **Abrir**.

![Nueva integración de Adobe I/O](./images/selectfiles.png)

Después de hacer clic en **Abrir**, Postman le mostrará una descripción general del entorno y las colecciones que está a punto de importar. Haga clic en **Importar**.

![Nueva integración de Adobe I/O](./images/impconfirm.png)

Ahora tiene todo lo que necesita en Postman para empezar a interactuar con Adobe Experience Platform a través de las API.

Lo primero que debe hacer es asegurarse de que está autenticado correctamente. Para autenticarse, debe solicitar un token de acceso.

Asegúrese de haber seleccionado el entorno adecuado antes de ejecutar cualquier solicitud. Puede comprobar el Entorno seleccionado actualmente comprobando la lista desplegable Entorno en la esquina superior derecha.

El entorno seleccionado debe tener un nombre similar a este:

![Postman](./images/envselemea.png)

Haga clic en el icono **ojo** y, a continuación, haga clic en **Editar** para actualizar la clave privada en el archivo de entorno.

![Postman](./images/gear.png)

Entonces verá esto... Todos los campos están rellenados previamente, excepto el campo **PRIVATE_KEY**.

![Postman](./images/pk2.png)

La clave privada se ha generado al crear el proyecto de Adobe I/O. Se descargó como un archivo zip, llamado **config.zip**. Extraiga ese archivo zip a su escritorio.

![Postman](./images/pk3.png)

Abra la carpeta **config** y abra el archivo **private.key** con el editor de texto que prefiera.

![Postman](./images/pk4.png)

Verá algo similar a esto, copie todo el texto en el portapapeles.

![Postman](./images/pk5.png)

Vuelva a Postman y pegue la clave privada en los campos junto a la variable **PRIVATE_KEY**, para las columnas **VALOR INICIAL** y **VALOR ACTUAL**. Haga clic en **Guardar**.

![Postman](./images/pk6.png)

El entorno y las colecciones de Postman ya están configurados y funcionan. Ahora puede autenticarse desde Postman en el Adobe I/O.

Para ello, debe cargar una biblioteca externa que se encargue del cifrado y el descifrado de la comunicación. Para cargar esta biblioteca, debe ejecutar la solicitud con el nombre **INIT: Load Crypto Library for RS256**. Seleccione esta solicitud en el **_Adobe I/O - Recopilación de tokens** y verá que se muestra en medio de la pantalla.

![Postman](./images/iocoll.png)

![Postman](./images/cryptolib.png)

Haga clic en el botón azul **Enviar**. Después de un par de segundos, debería ver una respuesta en la sección **Body** de Postman:

![Postman](./images/cryptoresponse.png)

Con la biblioteca criptográfica ahora cargada, podemos autenticarnos en el Adobe I/O.

En **\_Adobe I/O - Recopilación de tokens**, seleccione la solicitud con el nombre **IMS: JWT Generate + Auth**. Nuevamente, verá los detalles de la solicitud en el centro de la pantalla.

![Postman](./images/ioauth.png)

Haga clic en el botón azul **Enviar**. Después de un par de segundos, debería ver una respuesta en la sección **Body** de Postman:

![Postman](./images/ioauthresp.png)

Si la configuración se ha realizado correctamente, debería ver una respuesta similar que contenga la siguiente información:

| Clave | Valor |
|:-------------:| :---------------:| 
| token_type | **portador** |
| access_token | **eyJ4NXUiOiJpbXNfbmEx...QT7mqZkumN1tdsPEioOEl4087Dg** |
| expires_in | **86399973** |

El Adobe I/O le ha proporcionado un token de **bearer**, con un valor específico (este access_token muy largo) y un período de caducidad.

El token que hemos recibido ahora es válido durante 24 horas. Esto significa que, después de 24 horas, si desea utilizar Postman para autenticarse en el Adobe I/O, deberá generar un nuevo token ejecutando esta solicitud de nuevo.

## 2.1.3.4 API del perfil del cliente en tiempo real, esquema: perfil

Ahora puede continuar y enviar su primera solicitud a las API de perfil del cliente en tiempo real de Platform.

En Postman, busque la colección **_Adobe Experience Platform Enablement**.

![Postman](./images/coll_enablement.png)

En **1. Servicio de perfil unificado**, seleccione la primera solicitud con el nombre **UPS - Perfil de GET por ID de entidad y NS**.

![Postman](./images/upscall.png)

Para esta solicitud, hay tres variables requeridas:

| Clave | Valor | Definición |
|:-------------:| :---------------:| :---------------:| 
| entityId | **id** | el ID de cliente específico |
| entityIdNS | **espacio de nombres** | el área de nombres específica aplicable al ID |
| schema.name | **_xdm.context.profile** | el esquema específico para el que desea recibir información |

Por lo tanto, si desea solicitar a las API de Adobe Experience Platform que le devuelvan toda la información de perfil para su propio ECID, deberá configurar la solicitud de la siguiente manera:

| Clave | Valor |
|:-------------:| :---------------:| 
| entityId | **yourECID** |
| entityIdNS | **ecid** |
| schema.name | **_xdm.context.profile** |

![Postman](./images/callecid.png)

También debe verificar los campos **Header** - de su solicitud. Vaya a **Encabezados**. A continuación, verá esto:

![Postman](./images/callecidheaders.png)

| Clave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>Debe especificar el nombre de la zona protegida de Adobe Experience Platform que está utilizando. x-sandbox-name debe ser `--aepSandboxName--`.

Haga clic en **Enviar** para enviar la solicitud a Platform.

Debería obtener una respuesta inmediata de Platform, que le muestre algo similar a esto:

![Postman](./images/callecidresponse.png)

Esta es la respuesta completa de Platform:

```javascript
{
    "A28iM3aJBJRbEQpOnUh5HOM9": {
        "entityId": "A28iM3aJBJRbEQpOnUh5HOM9",
        "mergePolicy": {
            "id": "e632ccb8-882a-4b5e-8375-96a1ba3df1aa"
        },
        "sources": [
            "61fe23c5be4b5f19485dc379",
            "profile-streaming-segment",
            "61fe23cfa07c1219489b3ba4"
        ],
        "tags": [
            "1644130566774:1542:232:va7",
            "0a1e9dd4-940a-46ec-9114-7e371cf5c4d0",
            "aep_ups_partitioned_profile_cdc_low_lag_sla_0:106:1090888313",
            "a6fed09e-2c56-403e-8692-4e99e4779dfa:IRL1",
            "1644419616318:2989:31:va7",
            "aep_ups_profile_change_event_prod_va7:71:7946633524-8361f22c-c09e-4364-b24b-b57435c4d14f"
        ],
        "identityGraph": [
            "BUF9zMKLrXq72p4HpbsHv1SSBnr0LTAxQGdtYWlsLmNvbQ",
            "GkicrkFjgmCjUg",
            "GtCbrkFjgkSOFg",
            "A2-AP9zOsakzNTe9Rqwf7Wse",
            "BkFuK4QcJpSPByuSBnr0LTAx",
            "A28jSB484ziuECF3fEoXmFlF",
            "A28iM3aJBJRbEQpOnUh5HOM9"
        ],
        "entity": {
            "_experienceplatform": {
                "individualCharacteristics": {},
                "loyaltyDetails": {
                    "level": "Basic",
                    "points": 0
                },
                "identification": {
                    "core": {
                        "phoneNumber": "+32473622044+06022022-01",
                        "email": "woutervangeluwe+06022022-01@gmail.com",
                        "loyaltyId": "5415776",
                        "ecid": "12019606991718502754997192487345616673",
                        "crmId": "1478212"
                    }
                }
            },
            "personalEmail": {
                "address": "woutervangeluwe+06022022-01@gmail.com"
            },
            "_repo": {
                "createDate": "2022-02-06T06:56:06.424Z"
            },
            "testProfile": true,
            "homeAddress": {
                "postalCode": "1831",
                "city": "Diegem",
                "street1": "Culliganlaan 2F"
            },
            "mobilePhone": {
                "number": "+32473622044+06022022-01"
            },
            "segmentMembership": {
                "ups": {
                    "bc999ded-b6d7-40d4-87a7-d3a280b950e3": {
                        "lastQualificationTime": "2022-02-09T20:38:33Z",
                        "status": "exited"
                    },
                    "23b1cd4e-d62f-44bd-8392-3095a33109c4": {
                        "lastQualificationTime": "2022-02-09T20:38:33Z",
                        "status": "exited"
                    },
                    "f0807704-a1c8-4ac4-85dd-60db2fbf18f1": {
                        "lastQualificationTime": "2022-02-09T20:38:33Z",
                        "status": "existing"
                    }
                }
            },
            "person": {
                "name": {
                    "lastName": "Van Geluwe",
                    "firstName": "Wouter"
                },
                "gender": "female",
                "birthDate": "1982-07-08"
            },
            "userActivityRegions": {
                "IRL1": {
                    "captureTimestamp": "2022-02-09T15:21:11Z"
                }
            },
            "identityMap": {
                "email": [
                    {
                        "id": "woutervangeluwe+06022022-01@gmail.com"
                    }
                ],
                "crmid": [
                    {
                        "id": "1478212"
                    }
                ],
                "ecid": [
                    {
                        "id": "12507560687324495704459439363261812234"
                    },
                    {
                        "id": "12019606991718502754997192487345616673"
                    },
                    {
                        "id": "38335942889672702722192106363935964471"
                    }
                ],
                "phone": [
                    {
                        "id": "+32473622044+06022022-01"
                    }
                ],
                "loyaltyid": [
                    {
                        "id": "5415776"
                    }
                ]
            }
        },
        "lastModifiedAt": "2022-02-09T20:38:36Z"
    }
}
```

Estos son todos los datos de perfil disponibles en Platform para este ECID.

No es necesario que utilice el ECID para solicitar datos de perfil al Perfil del cliente en tiempo real de Platform; puede utilizar cualquier ID en cualquier área de nombres para solicitar estos datos.

Volvamos a Postman y supongamos que somos el centro de llamadas y enviemos una solicitud a Platform especificando el área de nombres de **Phone** y su número de móvil.

Por lo tanto, si desea solicitar a las API de Platform que le devuelvan toda la información de perfil de un teléfono específico, deberá configurar la solicitud de la siguiente manera:

| Clave | Valor |
|:-------------:| :---------------:| 
| entityId | **tu número de teléfono** |
| entityIdNS | **teléfono** (reemplazar ecid por teléfono) |
| schema.name | **_xdm.context.profile** |

Si tu número de teléfono contiene símbolos especiales como **+**, tienes que seleccionar tu número de teléfono completo, hacer clic con el botón derecho y hacer clic en **EncodeURIComponent**.

![Postman](./images/encodephone.png)

A continuación, tendrá esto:

![Postman](./images/callmobilenr.png)

También debe verificar los campos **Header** - de su solicitud. Vaya a **Encabezados**. A continuación, verá esto:

![Postman](./images/callecidheaders.png)

| Clave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>Debe especificar el nombre de la zona protegida de Adobe Experience Platform que está utilizando. x-sandbox-name debe ser `--aepSandboxName--`.

Haga clic en el botón azul **Enviar** y verifique la respuesta.

![Postman](./images/callmobilenrresponse.png)

Hagamos lo mismo con tu dirección de correo electrónico especificando el área de nombres de **email** y tu dirección de correo electrónico.

Por lo tanto, si desea solicitar a las API de Platform que le devuelvan toda la información de perfil de una dirección de correo electrónico específica, deberá configurar la solicitud de la siguiente manera:

| Clave | Valor |
|:-------------:| :---------------:| 
| entityId | **su correo electrónico** |
| entityIdNS | **correo electrónico** (reemplazar teléfono por correo electrónico) |
| schema.name | **_xdm.context.profile** |

Si su dirección de correo electrónico contiene símbolos especiales como **+**, debe seleccionar su dirección de correo electrónico completa, hacer clic con el botón secundario y hacer clic en **EncodeURIComponent**.

![Postman](./images/encodeemail.png)

A continuación, tendrá esto:

![Postman](./images/callemail.png)

También debe verificar los campos **Header** - de su solicitud. Vaya a **Encabezados**. A continuación, verá esto:

![Postman](./images/callecidheaders.png)

| Clave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>Debe especificar el nombre de la zona protegida de Adobe Experience Platform que está utilizando. x-sandbox-name debe ser `--aepSandboxName--`.

Haga clic en el botón azul **Enviar** y verifique la respuesta.

![Postman](./images/callemailresponse.png)

Se trata de un tipo muy importante de flexibilidad que se ofrece a las marcas. Esto significa que cualquier entorno puede enviar una solicitud a Platform, utilizando su propio ID y área de nombres, sin tener que comprender la complejidad de varias áreas de nombres e ID.

A modo de ejemplo:

- el centro de llamadas solicitará datos de Platform usando el área de nombres **phone**
- el sistema de fidelización solicitará datos de Platform mediante el espacio de nombres **email**
- las aplicaciones en línea podrían usar el espacio de nombres **ecid**

El centro de llamadas no sabe necesariamente qué tipo de identificador se utiliza en el sistema de fidelización y el sistema de fidelización no sabe necesariamente qué tipo de identificador se utiliza en las aplicaciones en línea. Cada sistema individual puede utilizar la información que tiene y que comprende para obtener la información que necesita, cuando la necesita.

## 2.1.3.5 API del perfil del cliente en tiempo real, esquema: Perfil y ExperienceEvent

Después de haber consultado correctamente las API de Platform para obtener datos de perfil, hagamos lo mismo con los datos de ExperienceEvent.

En Postman, busque la colección **_Adobe Experience Platform Enablement**.

![Postman](./images/coll_enablement.png)

En **1. Servicio de perfil unificado**, seleccione la segunda solicitud con el nombre **UPS - Perfil de GET &amp; EE por ID de entidad &amp; NS**.

![Postman](./images/upseecall.png)

Para esta solicitud, hay cuatro variables requeridas:

| Clave | Valor | Definición |
|:-------------:| :---------------:|  :---------------:| 
| schema.name | **_xdm.context.experienceevent** | el esquema específico para el que desea recibir información. En este caso, buscamos datos que estén asignados al esquema ExperienceEvent. |
| relatedSchema.name | **_xdm.context.profile** | Mientras buscamos datos asignados al esquema de ExperienceEvent, necesitamos especificar una identidad para la que queramos recibir esos datos. El esquema que tiene acceso a la identidad es el esquema de perfil, por lo que relatedSchema es el esquema de perfil. |
| relatedEntityId | **id** | el ID de cliente específico |
| relatedEntityIdNS | **espacio de nombres** | el área de nombres específica aplicable al ID |

Por lo tanto, si desea solicitar a las API de Platform que le devuelvan toda la información de perfil para su propio ecid, deberá configurar la solicitud de la siguiente manera:

| Clave | Valor |
|:-------------:| :---------------:| 
| schema.name | **_xdm.context.experienceevent** |
| relatedSchema.name | **_xdm.context.profile** |
| relatedEntityId | **yourECID** |
| relatedEntityIdNS | **ecid** |

![Postman](./images/eecallecid.png)

También debe verificar los campos **Header** - de su solicitud. Vaya a **Encabezados**. A continuación, verá esto:

![Postman](./images/eecallecidheaders.png)

| Clave | Valor |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>Debe especificar el nombre de la zona protegida de Adobe Experience Platform que está utilizando. x-sandbox-name debe ser `--aepSandboxName--`.

Haga clic en **Enviar** para enviar la solicitud a Platform.

Debería obtener una respuesta inmediata de Platform, que le muestre algo similar a esto:

![Postman](./images/eecallecidresponse.png)

A continuación se muestra la respuesta completa de Platform. En este ejemplo, hay ocho ExperienceEvents vinculados al ECID de este cliente. Eche un vistazo a lo siguiente para ver las diferentes variables de la solicitud, ya que lo que ve a continuación es la consecuencia directa de la configuración en Launch en ejercicios anteriores.

Además, cuando el panel de rayos X muestra información de ExperienceEvent, está utilizando la siguiente carga útil para analizar y recuperar la información, como el nombre del producto (busque productName en la siguiente carga útil) y la URL de imagen del producto (busque productImageUrl en la siguiente carga útil).

```javascript
{
    "_page": {
        "orderby": "timestamp",
        "start": "d686ab8a-2d0c-4722-9ff5-bfc1020b0b55-0",
        "count": 31,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A28iM3aJBJRbEQpOnUh5HOM9",
            "entityId": "d686ab8a-2d0c-4722-9ff5-bfc1020b0b55-0",
            "timestamp": 1644127126596,
            "entity": {
                "environment": {
                    "ipV4": "213.118.129.117",
                    "type": "browser",
                    "browserDetails": {
                        "viewportHeight": 969,
                        "viewportWidth": 1920,
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36"
                    }
                },
                "web": {
                    "webPageDetails": {
                        "pageViews": {
                            "value": 1
                        },
                        "name": "vangeluw-OCUC",
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC"
                    },
                    "webReferrer": {
                        "URL": "https://adobe.okta.com/"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "web"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-OCUC"
                    },
                    "identification": {
                        "core": {
                            "ecid": "12507560687324495704459439363261812234"
                        }
                    }
                },
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "2.8.0+2.9.0",
                    "environment": "browser"
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "12507560687324495704459439363261812234",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "web.webpagedetails.pageViews",
                "_id": "d686ab8a-2d0c-4722-9ff5-bfc1020b0b55-0",
                "placeContext": {
                    "localTime": "2022-02-06T06:58:46.596+01:00",
                    "localTimezoneOffset": -60
                },
                "device": {
                    "screenOrientation": "landscape",
                    "screenWidth": 1920,
                    "screenHeight": 1080
                },
                "timestamp": "2022-02-06T05:58:46.596Z"
            },
            "lastModifiedAt": "2022-02-06T05:59:48Z"
        },
        {
            "relatedEntityId": "A28iM3aJBJRbEQpOnUh5HOM9",
            "entityId": "919a46bf-a591-4c32-9201-b72250d5f5d9-0",
            "timestamp": 1644127129876,
            "entity": {
                "environment": {
                    "ipV4": "213.118.129.117",
                    "type": "browser",
                    "browserDetails": {
                        "viewportHeight": 969,
                        "viewportWidth": 1920,
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36"
                    }
                },
                "web": {
                    "webPageDetails": {
                        "pageViews": {
                            "value": 1
                        },
                        "name": "vangeluw-OCUC#",
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC#"
                    },
                    "webReferrer": {
                        "URL": "https://adobe.okta.com/"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "web"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-OCUC"
                    },
                    "identification": {
                        "core": {
                            "ecid": "12507560687324495704459439363261812234"
                        }
                    }
                },
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "2.8.0+2.9.0",
                    "environment": "browser"
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "12507560687324495704459439363261812234",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "web.webpagedetails.pageViews",
                "_id": "919a46bf-a591-4c32-9201-b72250d5f5d9-0",
                "placeContext": {
                    "localTime": "2022-02-06T06:58:49.876+01:00",
                    "localTimezoneOffset": -60
                },
                "device": {
                    "screenOrientation": "landscape",
                    "screenWidth": 1920,
                    "screenHeight": 1080
                },
                "timestamp": "2022-02-06T05:58:49.876Z"
            },
            "lastModifiedAt": "2022-02-06T05:59:48Z"
        },
        {
            "relatedEntityId": "A28iM3aJBJRbEQpOnUh5HOM9",
            "entityId": "41a80489-00d4-446c-b456-8cb19c3f309a-0",
            "timestamp": 1644130597134,
            "entity": {
                "environment": {
                    "ipV4": "213.118.129.117",
                    "type": "browser",
                    "browserDetails": {
                        "viewportHeight": 1001,
                        "viewportWidth": 1920,
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36"
                    }
                },
                "web": {
                    "webPageDetails": {
                        "pageViews": {
                            "value": 1
                        },
                        "name": "login",
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC/login"
                    },
                    "webReferrer": {
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC/login"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "web"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-OCUC"
                    },
                    "identification": {
                        "core": {
                            "ecid": "12507560687324495704459439363261812234"
                        }
                    }
                },
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "2.8.0+2.9.0",
                    "environment": "browser"
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "12507560687324495704459439363261812234",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "web.webpagedetails.pageViews",
                "_id": "41a80489-00d4-446c-b456-8cb19c3f309a-0",
                "placeContext": {
                    "localTime": "2022-02-06T07:56:37.134+01:00",
                    "localTimezoneOffset": -60
                },
                "device": {
                    "screenOrientation": "landscape",
                    "screenWidth": 1920,
                    "screenHeight": 1080
                },
                "timestamp": "2022-02-06T06:56:37.134Z"
            },
            "lastModifiedAt": "2022-02-06T06:56:38Z"
        },
        {
            "relatedEntityId": "A28jSB484ziuECF3fEoXmFlF",
            "entityId": "8ACC7B6C-2320-4865-B414-3B0CFA01F628",
            "timestamp": 1644419615000,
            "entity": {
                "environment": {
                    "ipV4": "213.118.129.117",
                    "browserDetails": {
                        "userAgent": "Mozilla/5.0 (iPhone; CPU OS 15_3 like Mac OS X; en_BE)"
                    }
                },
                "eventType": "application.login",
                "_id": "8ACC7B6C-2320-4865-B414-3B0CFA01F628",
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "mobile"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-2L6V"
                    },
                    "identification": {
                        "core": {
                            "ecid": "12019606991718502754997192487345616673",
                            "email": "woutervangeluwe+06022022-01@gmail.com"
                        }
                    }
                },
                "timestamp": "2022-02-09T15:13:35Z",
                "identityMap": {
                    "ECID": [
                        {
                            "id": "12019606991718502754997192487345616673",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                }
            },
            "lastModifiedAt": "2022-02-09T15:13:38Z"
        },
        {
            "relatedEntityId": "A28jSB484ziuECF3fEoXmFlF",
            "entityId": "54F68CE5-E9E1-4AD0-91B1-7B607A9285C4",
            "timestamp": 1644419658000,
            "entity": {
                "environment": {
                    "ipV4": "213.118.129.117",
                    "browserDetails": {
                        "userAgent": "Mozilla/5.0 (iPhone; CPU OS 15_3 like Mac OS X; en_BE)"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "mobile"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-2L6V"
                    },
                    "identification": {
                        "core": {
                            "ecid": "12019606991718502754997192487345616673"
                        }
                    }
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "12019606991718502754997192487345616673",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "commerce.productViews",
                "_id": "54F68CE5-E9E1-4AD0-91B1-7B607A9285C4",
                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "quantity": 1,
                        "productAddMethod": "Mobile",
                        "_experienceplatform": {
                            "core": {
                                "mainCategory": "Women",
                                "productURL": "product1",
                                "imageURL": "https://contentviewer.s3.amazonaws.com/helium/wh08-white_main.jpg"
                            }
                        },
                        "priceTotal": 42,
                        "name": "Cassia Funnel Sweatshirt",
                        "SKU": "product1",
                        "currencyCode": "USD"
                    }
                ],
                "timestamp": "2022-02-09T15:14:18Z"
            },
            "lastModifiedAt": "2022-02-09T15:14:21Z"
        },
        {
            "relatedEntityId": "A2-AP9zOsakzNTe9Rqwf7Wse",
            "entityId": "bfe26684-bc3b-40c5-9fe5-5aba854c3227-0",
            "timestamp": 1644420036035,
            "entity": {
                "environment": {
                    "ipV4": "193.105.139.131",
                    "type": "browser",
                    "browserDetails": {
                        "viewportHeight": 969,
                        "viewportWidth": 1920,
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36"
                    }
                },
                "web": {
                    "webPageDetails": {
                        "pageViews": {
                            "value": 1
                        },
                        "name": "vangeluw-OCUC",
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC"
                    },
                    "webReferrer": {
                        "URL": "https://adobe.okta.com/"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "web"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-OCUC"
                    },
                    "identification": {
                        "core": {
                            "ecid": "38335942889672702722192106363935964471"
                        }
                    }
                },
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "2.8.0+2.9.0",
                    "environment": "browser"
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "38335942889672702722192106363935964471",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "web.webpagedetails.pageViews",
                "_id": "bfe26684-bc3b-40c5-9fe5-5aba854c3227-0",
                "placeContext": {
                    "localTime": "2022-02-09T16:20:36.035+01:00",
                    "localTimezoneOffset": -60
                },
                "device": {
                    "screenOrientation": "landscape",
                    "screenWidth": 1920,
                    "screenHeight": 1080
                },
                "timestamp": "2022-02-09T15:20:36.035Z"
            },
            "lastModifiedAt": "2022-02-09T15:20:39Z"
        },
        {
            "relatedEntityId": "A2-AP9zOsakzNTe9Rqwf7Wse",
            "entityId": "0480c434-8fcd-4a80-b298-c561276ac989-0",
            "timestamp": 1644420037078,
            "entity": {
                "environment": {
                    "ipV4": "193.105.139.131",
                    "type": "browser",
                    "browserDetails": {
                        "viewportHeight": 969,
                        "viewportWidth": 1920,
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36"
                    }
                },
                "web": {
                    "webPageDetails": {
                        "pageViews": {
                            "value": 1
                        },
                        "name": "vangeluw-OCUC#",
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC#"
                    },
                    "webReferrer": {
                        "URL": "https://adobe.okta.com/"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "web"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-OCUC"
                    },
                    "identification": {
                        "core": {
                            "ecid": "38335942889672702722192106363935964471"
                        }
                    }
                },
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "2.8.0+2.9.0",
                    "environment": "browser"
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "38335942889672702722192106363935964471",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "web.webpagedetails.pageViews",
                "_id": "0480c434-8fcd-4a80-b298-c561276ac989-0",
                "placeContext": {
                    "localTime": "2022-02-09T16:20:37.078+01:00",
                    "localTimezoneOffset": -60
                },
                "device": {
                    "screenOrientation": "landscape",
                    "screenWidth": 1920,
                    "screenHeight": 1080
                },
                "timestamp": "2022-02-09T15:20:37.078Z"
            },
            "lastModifiedAt": "2022-02-09T15:20:39Z"
        },
        {
            "relatedEntityId": "A2-AP9zOsakzNTe9Rqwf7Wse",
            "entityId": "6b1b3983-6966-4551-a711-6b6e410fd819-0",
            "timestamp": 1644420045993,
            "entity": {
                "environment": {
                    "ipV4": "193.105.139.131",
                    "type": "browser",
                    "browserDetails": {
                        "viewportHeight": 969,
                        "viewportWidth": 1920,
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36"
                    }
                },
                "web": {
                    "webPageDetails": {
                        "pageViews": {
                            "value": 1
                        },
                        "name": "login",
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC/login"
                    },
                    "webReferrer": {
                        "URL": "https://adobe.okta.com/"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "web"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-OCUC"
                    },
                    "identification": {
                        "core": {
                            "ecid": "38335942889672702722192106363935964471"
                        }
                    }
                },
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "2.8.0+2.9.0",
                    "environment": "browser"
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "38335942889672702722192106363935964471",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "web.webpagedetails.pageViews",
                "_id": "6b1b3983-6966-4551-a711-6b6e410fd819-0",
                "placeContext": {
                    "localTime": "2022-02-09T16:20:45.993+01:00",
                    "localTimezoneOffset": -60
                },
                "device": {
                    "screenOrientation": "landscape",
                    "screenWidth": 1920,
                    "screenHeight": 1080
                },
                "timestamp": "2022-02-09T15:20:45.993Z"
            },
            "lastModifiedAt": "2022-02-09T15:20:47Z"
        },
        {
            "relatedEntityId": "A2-AP9zOsakzNTe9Rqwf7Wse",
            "entityId": "ae0f3551-7753-4467-8547-8fdbb66c2214-0",
            "timestamp": 1644420058565,
            "entity": {
                "environment": {
                    "ipV4": "193.105.139.131",
                    "type": "browser",
                    "browserDetails": {
                        "viewportHeight": 969,
                        "viewportWidth": 1920,
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36"
                    }
                },
                "web": {
                    "webPageDetails": {
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC/home"
                    },
                    "webReferrer": {
                        "URL": "https://adobe.okta.com/"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "web"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-OCUC"
                    },
                    "identification": {
                        "core": {
                            "ecid": "38335942889672702722192106363935964471",
                            "email": "woutervangeluwe+06022022-01@gmail.com"
                        }
                    }
                },
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "2.8.0+2.9.0",
                    "environment": "browser"
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "38335942889672702722192106363935964471",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "web.login",
                "_id": "ae0f3551-7753-4467-8547-8fdbb66c2214-0",
                "placeContext": {
                    "localTime": "2022-02-09T16:20:58.565+01:00",
                    "localTimezoneOffset": -60
                },
                "device": {
                    "screenOrientation": "landscape",
                    "screenWidth": 1920,
                    "screenHeight": 1080
                },
                "timestamp": "2022-02-09T15:20:58.565Z"
            },
            "lastModifiedAt": "2022-02-09T15:20:59Z"
        },
        {
            "relatedEntityId": "A2-AP9zOsakzNTe9Rqwf7Wse",
            "entityId": "5e67a9c9-b201-4e21-bd3a-4d10475f6156-0",
            "timestamp": 1644420058653,
            "entity": {
                "environment": {
                    "ipV4": "193.105.139.131",
                    "type": "browser",
                    "browserDetails": {
                        "viewportHeight": 969,
                        "viewportWidth": 1920,
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36"
                    }
                },
                "web": {
                    "webPageDetails": {
                        "pageViews": {
                            "value": 1
                        },
                        "name": "home",
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC/home"
                    },
                    "webReferrer": {
                        "URL": "https://adobe.okta.com/"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "web"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-OCUC"
                    },
                    "identification": {
                        "core": {
                            "ecid": "38335942889672702722192106363935964471"
                        }
                    }
                },
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "2.8.0+2.9.0",
                    "environment": "browser"
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "38335942889672702722192106363935964471",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "web.webpagedetails.pageViews",
                "_id": "5e67a9c9-b201-4e21-bd3a-4d10475f6156-0",
                "placeContext": {
                    "localTime": "2022-02-09T16:20:58.653+01:00",
                    "localTimezoneOffset": -60
                },
                "device": {
                    "screenOrientation": "landscape",
                    "screenWidth": 1920,
                    "screenHeight": 1080
                },
                "timestamp": "2022-02-09T15:20:58.653Z"
            },
            "lastModifiedAt": "2022-02-09T15:21:00Z"
        },
        {
            "relatedEntityId": "A2-AP9zOsakzNTe9Rqwf7Wse",
            "entityId": "33253c5a-6a7e-4858-a7d2-4e6d4a1c7901-0",
            "timestamp": 1644420061804,
            "entity": {
                "environment": {
                    "ipV4": "193.105.139.131",
                    "type": "browser",
                    "browserDetails": {
                        "viewportHeight": 969,
                        "viewportWidth": 1920,
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36"
                    }
                },
                "web": {
                    "webPageDetails": {
                        "pageViews": {
                            "value": 1
                        },
                        "name": "vangeluw-OCUC",
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC"
                    },
                    "webReferrer": {
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC/home"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "web"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-OCUC"
                    },
                    "identification": {
                        "core": {
                            "ecid": "38335942889672702722192106363935964471"
                        }
                    }
                },
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "2.8.0+2.9.0",
                    "environment": "browser"
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "38335942889672702722192106363935964471",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "web.webpagedetails.pageViews",
                "_id": "33253c5a-6a7e-4858-a7d2-4e6d4a1c7901-0",
                "placeContext": {
                    "localTime": "2022-02-09T16:21:01.804+01:00",
                    "localTimezoneOffset": -60
                },
                "device": {
                    "screenOrientation": "landscape",
                    "screenWidth": 1920,
                    "screenHeight": 1080
                },
                "timestamp": "2022-02-09T15:21:01.804Z"
            },
            "lastModifiedAt": "2022-02-09T15:21:03Z"
        },
        {
            "relatedEntityId": "A2-AP9zOsakzNTe9Rqwf7Wse",
            "entityId": "d8e81fb7-6de9-44c1-b9c6-60d93b520209-0",
            "timestamp": 1644420071737,
            "entity": {
                "environment": {
                    "ipV4": "193.105.139.131",
                    "type": "browser",
                    "browserDetails": {
                        "viewportHeight": 969,
                        "viewportWidth": 1920,
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/98.0.4758.80 Safari/537.36"
                    }
                },
                "web": {
                    "webPageDetails": {
                        "pageViews": {
                            "value": 1
                        },
                        "name": "vangeluw-OCUC",
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC"
                    },
                    "webReferrer": {
                        "URL": "https://builder.adobedemo.com/run/vangeluw-OCUC/home"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "web"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-OCUC"
                    },
                    "identification": {
                        "core": {
                            "ecid": "38335942889672702722192106363935964471"
                        }
                    }
                },
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "2.8.0+2.9.0",
                    "environment": "browser"
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "38335942889672702722192106363935964471",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "web.webpagedetails.pageViews",
                "_id": "d8e81fb7-6de9-44c1-b9c6-60d93b520209-0",
                "placeContext": {
                    "localTime": "2022-02-09T16:21:11.737+01:00",
                    "localTimezoneOffset": -60
                },
                "device": {
                    "screenOrientation": "landscape",
                    "screenWidth": 1920,
                    "screenHeight": 1080
                },
                "timestamp": "2022-02-09T15:21:11.737Z"
            },
            "lastModifiedAt": "2022-02-09T15:21:14Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

Estos son todos los datos de ExperienceEvent disponibles en Platform para este ECID.

No es necesario que utilice el ECID para solicitar datos de ExperienceEvent del perfil en tiempo real de Adobe Experience Platform; puede utilizar cualquier ID en cualquier área de nombres para solicitar estos datos.

Paso siguiente: [2.1.4 Crear un segmento: IU](./ex4.md)

[Volver al módulo 2.1](./real-time-customer-profile.md)

[Volver a todos los módulos](../../../overview.md)
