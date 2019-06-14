---
uid: developers-jwt-access-token
locale: es
title: JWT Access Token
dnnversion: 09.02.00
related-topics: 
---

# JWT Access Token

El token de acceso decodificado consta de tres partes separadas por puntos.

```

    header.payload.signature
            
```

Componente

Descripción

Cabecera JWT

Un objeto JSON que contiene el identificador de protocolo JWT y el esquema de firma. El encabezado se convierte en un encabezado de firma y cifrado de objetos de JavaScript (JOSE) como octetos UTF-8 y luego se codifica como una cadena Base64. Por ejemplo:

```

    {
     "typ":"JWT",
     "alg":"HS256"
    }
                        
```

Payload JWT (carga útil)

Un objeto JSON que contiene el conjunto de notificaciones JWT (información sobre el usuario) u otra información. Codificado como una cadena de base 64. El conjunto de notificaciones JWT en DNN incluye lo siguiente:

*   sid es el ID de sesión, que se ha establecido durante la vida útil del token de renovación.
*   rol es la lista de roles asignados al usuario. Se utiliza en la autorización para determinar a qué áreas del sitio puede acceder el usuario.
*   iss es el alias de portal del sitio que emitió el token.
*   exp es el tiempo de expiración del token de acceso. El token se rechazará después de este tiempo (más un pequeño período de gracia). Expresado como tiempo Unix.
*   nbf es el tiempo de "no antes (en ingles not before)". El token es rechazado antes de este tiempo. Expresado como tiempo de Unix.

Ejemplo:

```

    {
     "sid":"eecb9bf34bbb4c8eb87dbba3aa1523c6",
     "role":["Administrators","Registered Users","Subscribers"],
     "iss":"testsitece.lvh.me",
     "exp":1450834762,
     "nbf":1450830862
    }
                        
```

Firma JWT 

El hash/cifrado del encabezado y la carga útil. El método de cifrado se indica en el encabezado. Codificado como una cadena de base 64.

El nuevo token de acceso es válido por una hora.
