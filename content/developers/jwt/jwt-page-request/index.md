---
uid: developers-jwt-page-request
locale: es
title: Solicitud de página con JWT
dnnversion: 09.02.00
related-topics: 
---

# Solicitud de página con JWT

El encabezado de una solicitud posterior debe incluir el token en este formato::

```

    Authorization: Bearer [token]

```

Una solicitud GET de muestra con JWT:

```

    GET https://testsitece.lvh.me/DesktopModules/JwtAuth/API/mobile/testget HTTP/1.1
    Host: testsitece.lvh.me
    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzaWQiOiJkYmViMjlhYTMyYjg0MTMxYTA0NjY4MDAyNzAxNWEwZSIsInJvbGUiOlsiQWRtaW5pc3RyYXRvcnMiLCJSZWdpc3RlcmVkIFVzZXJzIiwiU3Vic2NyaWJlcnMiXSwiaXNzIjoidGVzdHNpdGVjZS5sdmgubWUiLCJleHAiOjE0NTA4MzU2ODMsIm5iZiI6MTQ1MDgzMTc4M30.Yf3mmBJ8nV_IozqvvLc8L34dDklU2J7z0uXn3jsICp0

```
