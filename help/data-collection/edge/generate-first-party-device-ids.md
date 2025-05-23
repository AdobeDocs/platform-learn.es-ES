---
title: Generar ID de dispositivos de origen
description: Obtenga información sobre cómo generar ID de dispositivos de origen
feature: Web SDK
level: Experienced
jira: KT-9728
thumbnail: KT-9728.jpeg
exl-id: 2e3c1f71-e224-4631-b680-a05ecd4c01e7
source-git-commit: fd60f7ad338c81f5b32e7951d5a00b49c5aa1756
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# Generar ID de dispositivos de origen

Las aplicaciones de Adobe Experience Cloud han generado tradicionalmente cookies para almacenar los ID de dispositivo mediante diferentes tecnologías, entre las que se incluyen:

1. Cookies de terceros
1. Cookies de origen configuradas por un servidor de Adobe mediante la configuración CNAME de un nombre de dominio
1. Cookies de origen configuradas por JavaScript

Los cambios recientes en el explorador restringen la duración de estos tipos de cookies. Las cookies de origen son más efectivas cuando se establecen mediante un servidor propiedad del cliente que utiliza un registro A/AAAA DNS, en lugar de un CNAME DNS. La [funcionalidad de ID de dispositivo de origen (FPID)](https://experienceleague.adobe.com/es/docs/experience-platform/web-sdk/identity/first-party-device-ids) permite a los clientes que implementan el SDK web de Adobe Experience Platform usar ID de dispositivo en cookies de servidores que usan registros A/AAAA de DNS. Estos ID se pueden enviar al Adobe de y se pueden usar como semillas para generar ID de Experience Cloud (ECID), que sigue siendo el identificador principal en las aplicaciones de Adobe Experience Cloud.

A continuación se muestra un ejemplo rápido de cómo funciona la funcionalidad:

![ID de dispositivos de origen (FPID) e ID de Experience Cloud (ECID)](../assets/kt-9728.png)

1. Un explorador del usuario final solicita una página web del servidor web o CDN de un cliente.
1. El cliente genera un ID de dispositivo (FPID) en su servidor web o CDN (el servidor web debe estar vinculado al registro A/AAAA de DNS del nombre de dominio).
1. El cliente establece una cookie de origen para almacenar el FPID en el explorador del usuario final.
1. La implementación del SDK web de Adobe Experience Platform del cliente realiza una solicitud al Edge Network de la plataforma y:
   1. Incluye el FPID en el mapa de identidad.
   1. Configura un CNAME para sus solicitudes de SDK web y su secuencia de datos con el nombre de su cookie FPID.
1. El Edge Network Experience Platform recibe el FPID y lo utiliza para generar un ID de Experience Cloud (ECID).
1. La respuesta del SDK web de Platform devuelve el ECID al explorador del usuario final.
1. Si el SDK web de Platform `idMigrationEnabled=true` usa JavaScript para almacenar el ECID como cookie `AMCV_` en el explorador del usuario final.
1. En caso de que la cookie `AMCV_` caduque, el proceso se repetirá. Siempre que esté disponible el mismo ID de dispositivo de origen, se crea una nueva cookie `AMCV_` con el mismo valor de ECID que antes.

>[!NOTE]
>
>No es necesario establecer `idMigrationEnabled` en `true` para usar FPID. Sin embargo, con `idMigrationEnabled=false` es posible que no vea una cookie `AMCV_` y tendrá que buscar el valor ECID en la respuesta de red.


Para este tutorial, se utiliza un ejemplo específico utilizando el lenguaje de script PHP para mostrar cómo:

* Generación de un UUIDv4
* Escribir el valor de UUIDv4 en una cookie
* Incluir el valor de la cookie en el mapa de identidad
* Validar la generación de ECID

Puede encontrar más documentación relacionada con los ID de dispositivos de origen en la documentación del producto.

## Generación de un UUIDv4

PHP no tiene una biblioteca nativa para la generación de UUID, por lo que estos ejemplos de código son más extensos de lo que probablemente se requeriría si se utilizara otro lenguaje de programación. Se eligió PHP para este ejemplo porque es un lenguaje ampliamente compatible del lado del servidor.


Cuando se llama a la siguiente función, genera un UUID aleatorio versión 4:

```
<?php
    
    function guidv4($data)
    {
        $data = $data ?? random_bytes(16);

        $data[6] = chr(ord($data[6]) & 0x0f | 0x40); // set version to 0100
        $data[8] = chr(ord($data[8]) & 0x3f | 0x80); // set bits 6-7 to 10

        return vsprintf('%s%s-%s-%s-%s-%s%s%s', str_split(bin2hex($data), 4));
    }

?>
```

## Escribir el valor de UUIDv4 en una cookie

El siguiente código realiza una solicitud a la función anterior para generar un UUID. A continuación, establece los indicadores de cookies que ha decidido su organización. Si ya se ha generado una cookie, se amplía la caducidad.

```
<?php

    if(!isset($_COOKIE['FPID'])) {
        $cookie_value = guidv4(openssl_random_pseudo_bytes(16));        
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
        $_COOKIE[$cookie_name] = $cookie_value;
    }
    else {
        $cookie_value = $_COOKIE[$cookie_name];
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
    }

?>
```

>[!NOTE]
>
>La cookie que contiene el ID del dispositivo de origen puede tener cualquier nombre.

## Incluir el valor de la cookie en el mapa de identidad

El paso final es usar PHP para repetir el valor de la cookie en el mapa de identidad.


```
{
    "identityMap": {
        "FPID": [
                    {
                        "id": "<? echo $_COOKIE[$cookie_name] ?>",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
        }
}
```

>[!IMPORTANT]
>
>El símbolo del área de nombres de identidad usado en el mapa de identidad debe llamarse `FPID`.
>
> `FPID` es un área de nombres de identidad reservada que no está visible en las listas de interfaz de áreas de nombres de identidad.


## Validar generación de ECID

Valide la implementación confirmando que se genera el mismo ECID a partir del ID del dispositivo de origen:

1. Genere una cookie FPID.
1. Envíe una solicitud al Edge Network de Platform mediante el SDK web de Platform.
1. Se genera una cookie con el formato `AMCV_<IMSORGID@AdobeOrg>`. Esta cookie contiene el ECID.
1. Anote el valor de la cookie que se genera y luego elimine todas las cookies del sitio, excepto la cookie `FPID`.
1. Envíe otra solicitud al Edge Network de Platform.
1. Confirme que el valor de la cookie `AMCV_<IMSORGID@AdobeOrg>` sea el mismo valor `ECID` que el de la cookie `AMCV_` que se eliminó. Si el valor de la cookie es el mismo para un FPID determinado, el proceso de inicialización del ECID se realizó correctamente.

Para obtener más información acerca de esta característica, consulte [la documentación](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html?lang=es).
