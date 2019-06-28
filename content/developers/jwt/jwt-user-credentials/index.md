---
uid: developers-jwt-user-credentials
locale: es
title: Credenciales de usuario de JWT
dnnversion: 09.02.00
related-topics: 
---

# Credenciales de usuario de JWT

Para DNN, las credenciales de usuario deben estar en un objeto JSON con el nombre de usuario `(key "u":)` y la contraseña `(key:"p")` 

Una solicitud POST de muestra con el nombre de usuario `sitemanager` y la contraseña `dnnhost`:

```

    POST https://testsitece.lvh.me/DesktopModules/JwtAuth/API/mobile/login HTTP/1.1
    Content-Type: application/json; charset=utf-8
    Host: testsitece.lvh.me
    Content-Length: 33

    {"u":"sitemanager","p":"dnnhost"}

```
