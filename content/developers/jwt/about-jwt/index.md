---
uid: developers-about-jwt
locale: es
title: Acerca de la autenticación JWT
dnnversion: 09.02.00
links: ["[IETF RFC 7519](https://tools.ietf.org/html/rfc7519)","[Presentación de DNN: Cómo Evoq lo ayuda a crear aplicaciones web modernas por Will Morgenweck](https://www.slideshare.net/dnnsoftware/how-evoq-helps-you-build-modern-web-applications)","[jwt.io](https://jwt.io/introduction/)","[Unix time](https://en.wikipedia.org/wiki/Unix_time)"]
---

# Acerca de la autenticación JWT

## Visión general

JSON Web Token (JWT) es un formato de datos estándar abierto (IETF RFC 7519) que es compacto, autónomo y seguro. Está destinado a pasar información donde el espacio es limitado, como encabezados HTTP y consultas de URI.

*   Compacto. Debido a que el JWT está compuesto por objetos codificados de JavaScript Object Notation (JSON), es lo suficientemente compacto como para ser enviado a través de una consulta de URL, un parámetro POST o un encabezado HTTP. Los objetos JSON son más simples y más compactos que las aserciones del lenguaje de marcado de aserción de seguridad (SAML), que utilizan XML. Debido a su tamaño más pequeño, también se puede transmitir más rápido.
*   Autocontenido. El JWT puede contener toda la información requerida sobre el usuario y, por lo tanto, evita consultar la base de datos más de una vez.
*   Seguro. El JWT se puede firmar digitalmente con uno de los siguientes métodos:
    *   Algoritmo HMAC, utilizando un secreto.
    *   Algoritmo RSA, utilizando un par de claves pública/privada

JWT es ideal para aplicaciones que no pueden o no desean usar cookies, como aplicaciones móviles nativas y aplicaciones de escritorio. En una aplicación de formularios web estándar, el usuario inicia sesión en un sitio web y recibe una cookie de sesión/token que el navegador envía con cada solicitud posterior al sitio, para evitar verificar las credenciales del usuario con cada solicitud. JWT simplemente reemplaza la cookie con un token que es más pequeño y más rápido de transmitir.

## Autenticación JWT

> [!Nota] El proveedor de autenticación JWT está disponible en productos DNN; sin embargo, se debe instalar y habilitar por separado. DNN utiliza JWT solo para autenticación.



![JWT process](/images/gra-JWTprocess.png)



1.  El usuario inicia sesión con su nombre de usuario y contraseña u otras credenciales de seguridad. El navegador o la aplicación cliente envía una solicitud POST con las credenciales de usuario, que se envían a través de una conexión HTTPS.
2.  Las credenciales del usuario se comparan con la base de datos de inicio de sesión. Si son validas, el servidor crea y cifra un JWT de acceso, que se almacena en el cuerpo de la respuesta.
3.  Cuando el usuario solicita una página, el navegador o la aplicación cliente almacenan el token acceso JWT dentro de la sección `Authorization` de la solicitud.
4.  El servidor verifica la firma JWT y extrae la información del usuario de la carga útil de JWT.
5.  La página o recurso solicitado se envía al cliente.
