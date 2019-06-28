---
uid: developers-jwt-server-response
locale: es
title: Respuesta del servidor con JWT
dnnversion: 09.02.00
related-topics: 
---

# Respuesta del servidor con JWT

Cuando el servidor responde al navegador del usuario, el objeto JSON que se devuelve contiene tres propiedades.

|**Nombre de la propiedad**|**Descripción**|
|---|---|
|*displayName*|El nombre para mostrar del usuario.|
|*accessToken*|Un JWT que debe incluirse con cada solicitud posterior, a los distintos puntos finales de la API. El servidor obtiene la información del usuario del token de acceso, que es más rápido que recuperar la información de la base de datos nuevamente. El token de acceso es válido durante 60 minutos y debe renovarse utilizando el token de renovación.|
|*renewalToken*|Un JWT que se requiere para renovar el token de acceso cuando este caduque. El token de renovación deja de ser válido después de 14 días, después de que el usuario cierre la sesión o cuando el usuario cambie sus credenciales, como la contraseña de inicio de sesión del sitio web.|

Un objeto JSON de muestra enviado al navegador después de validar un usuario llamado "Administrador del sitio (Site Manager)":

```

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    Date: Wed, 23 Dec 2015 00:54:43 GMT
    Content-Length: 425

    {
     "displayName":"Site Manager",
     "accessToken":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzaWQiOiJkYmViMjlhYTMyYjg0MTMxYTA0NjY4MDAyNzAxNWEwZSIsInJvbGUiOlsiQWRtaW5pc3RyYXRvcnMiLCJSZWdpc3RlcmVkIFVzZXJzIiwiU3Vic2NyaWJlcnMiXSwiaXNzIjoidGVzdHNpdGVjZS5sdmgubWUiLCJleHAiOjE0NTA4MzU2ODMsIm5iZiI6MTQ1MDgzMTc4M30.Yf3mmBJ8nV_IozqvvLc8L34dDklU2J7z0uXn3jsICp0",
     "renewalToken":"qjjd1vmgbtWb23fPK4J9ttUQBKpgC6k1yFmnteU+9mlFxcHeC3rJlly8oGBBAIzw"
     }
                
```
