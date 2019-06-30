---
uid: developers-setup-jwt-for-auth
locale: es
title: Configurar la autenticación JWT para su sitio
dnnversion: 09.02.00
related-topics: 
links: ["[IETF RFC 7519](https://tools.ietf.org/html/rfc7519)","[Presentación de DNN: Cómo Evoq le ayuda a crear aplicaciones web modernas por Will Morgenweck](https://www.slideshare.net/dnnsoftware/how-evoq-helps-you-build-modern-web-applications)","[jwt.io](https://jwt.io/introduction/)"]
---

# Configurar la autenticación JWT para su sitio

## Prerrequisitos

**Una cuenta host / super user account.** Las cuentas hosts tienen permisos completos para todos los sitios en una instancia de DNN.

## Pasos

1.  Instalar el controlador de autenticación DNN JWT.

    1.  Vaya a Host \> Extensiones

        ![Host > Extensions](/images/scr-menuHostCommonExtensions.png)

    2.  En la pestaña Extensiones disponibles, expanda la sección Proveedores, busque DNN JWT Auth Handler y luego haga clic / Instalar.

        ![Available Extensions > Providers > DNN JWT Auth Handler > Install](/images/scr-AvailableExtensionsProvidersJWT.png)


    En el archivo web.config, se agrega la línea JWTAuth dentro de la sección `<messageHandlers/>`.

    ```

        <authServices>
            <messageHandlers>
                <!-- other message handlers -->
                <add name="JWTAuth" type="Dnn.AuthServices.Jwt.Auth.JwtAuthMessageHandler, Dnn.AuthServices.Jwt" enabled="false" defaultInclude="false" forceSSL="true"/>
            </messageHandlers>
        </authServices>

    ```

2.  (Opcional) Habilite la autenticación JWT para todas las solicitudes de la API web.

    1.  Acceder al archivo web.config..
    2.  Busque la línea JWTAuth recién agregada dentro de la sección `<messageHandlers/>`.
    3.  Cambia los atributos `enabled` y `defaultInclude` a "true".

        ```

            <add name="JWTAuth" type="Dnn.AuthServices.Jwt.Auth.JwtAuthMessageHandler, Dnn.AuthServices.Jwt" enabled="true" defaultInclude="true" forceSSL="true" />

        ```


    > [! Consejo para desarrolladores]: para habilitar la autenticación JWT para su API web específica, agregue el siguiente atributo a la clase de controlador:

    ```

        [DnnAuthorize(AuthTypes = "JWT")]

    ```

3.  (Opcional) Habilite el uso compartido de recursos de origen cruzado (CORS) para permitir solicitudes de clientes remotos de JavaScript.

    CORS solo es necesario si se accede a la API web a través de un navegador web. CORS no es requerido por aplicaciones móviles o de escritorio nativas.

    Advertencia: habilitar CORS permite que los sitios externos accedan a su sitio, por lo tanto, lo hacen vulnerable a ataques de scripts entre sitios (XSS).

    1.  Acceda al archivo web.config.
    2.  En su archivo web.config, agregue estas líneas de control de acceso dentro de la sección `<customHeaders/>`.

        ```

            <add name="Access-Control-Allow-Origin" value="*" />
            <add name="Access-Control-Allow-Headers" value="accept, accept-language, content-type, accept, authorization, moduleid, tabid, x-dnn-moniker" />
            <add name="Access-Control-Allow-Methods" value="GET, POST, PUT, HEAD, OPTIONS" />

        ```

4.  (Opcional) Desarrolladores: habilite el registro para la depuración avanzada, las pruebas o la solución de problemas.
    1.  Acceda al archivo DotNetNuke.log4net.config.
    2.  En el archivo DotNetNuke.log4net.config, agregue las siguientes líneas después de la etiqueta de cierre `</root>`.

        ```

            <!-- The following is required to troubleshoot provider registration issues. -->
            <logger name="DotNetNuke.Web.Api.Auth">
                <level value="TRACE" />
            </logger>
            <!-- The following is required to troubleshoot failing Web API calls. -->
            <logger name="DotNetNuke.Dnn.AuthServices.Jwt">
                <level value="TRACE" />
            </logger>

        ```
