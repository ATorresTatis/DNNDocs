---
uid: developers-jwt-auth-handler
locale: es
title: Controlador de autenticación JWT
dnnversion: 09.02.00
related-topics: 
links: ["[IETF RFC 7519](https://tools.ietf.org/html/rfc7519)","[DNN Presentation: How Evoq Helps You Build Modern Web Applications by Will Morgenweck](https://www.slideshare.net/dnnsoftware/how-evoq-helps-you-build-modern-web-applications)","[jwt.io](https://jwt.io/introduction/)"]
---

# Controlador de autenticación JWT

Después de instalar el controlador de autenticación JWT en DNN, el archivo web.config se actualiza con una línea similar a la siguiente:

```

    <authServices>
        <messageHandlers>
            <!-- other message handlers -->
            <add name="JWTAuth" type="Dnn.AuthServices.Jwt.Auth.JwtAuthMessageHandler, Dnn.AuthServices.Jwt" enabled="false" defaultInclude="false" forceSSL="true"/>
        </messageHandlers>
    </authServices>

```

|**Parámetro**|**Valores permitidos**|**Descripción**|
|---|---|---|
|name|string|Nombre del proveedor de autenticación. Debe ser único dentro de la sección `messageHandlers`.|
|enabled|`true` or `false`|Cuando se establece a `true` se crea una instancia del proveedor y se agrega a la cadena de proveedores cuando se inicia la aplicación. De lo contrario, el proveedor no creará una instancia.|
|defaultInclude|`true` or `false`|Cuando se establece a `true`, el controlador de API utiliza el tipo de autenticación incluido en cada solicitud de Web.API de forma predeterminada; si es false, el controlador de API utiliza el tipo de autenticación especificado en su propio atributo `DnnAuthorize`. Por ejemplo: si el atributo del controlador de API está establecido en `[DnnAuthorize(AuthTypes = "JWT")]`, entonces el controlador de API responderá solo a las solicitudes que utilicen la autenticación JWT.|
|forceSSL|`true` or `false`|Cuando se establece a `true`, se requiere el modo SSL (HTTPS) para las todas las solicitudes; de lo contrario, las solicitudes HTTP también serán aceptadas.|

> [!Importante] Para evitar el acceso no autorizado al sitio, aplique SSL para que los tokens se traten de la misma manera que las cookies en una solicitud web.
