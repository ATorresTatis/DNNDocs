---
uid: developers-about-modules-overview
locale: es
title: About Module Development
dnnversion: 09.02.00
---

# Acerca del desarrollo de módulos

## ¿Qué es un módulo?

Una página web típica incluye elementos de página y bloques de contenido. Los elementos de la página, como el menú del sitio, el control de inicio de sesión y la barra de búsqueda, se incluyen con el tema. Los bloques de contenido son gestionados por módulos.
  
![Los módulos administran y muestran el contenido en una página.](/images/gra-module-overview.png)

El módulo es uno de los bloques de construcción básicos que extienden a DNN para permitir a los usuarios ver, crear y editar contenido. Todas las características administrativas de DNN se implementan como módulos.

> [! Sugerencia]
> El código fuente de la plataforma DNN incluye numerosos módulos de ejemplo para ayudarlo a construir sus propios módulos.

Debido a la naturaleza modular de la composición de una página en DNN, los módulos generalmente se construyen para administrar y mostrar un único tipo de contenido.

Sugerencia: considere la posibilidad de crear múltiples módulos cuando administre tipos de contenido complejos, o incluya un amplio soporte de plantillas para que los administradores puedan controlar el diseño del contenido en una página.

El desarrollo de un módulo implica seleccionar el marco de desarrollo y luego el enfoque de desarrollo.

- Marcos de desarrollo que se pueden utilizar con DNN:
  - Formularios web (Web Forms). Este marco tradicional crea módulos para DNN que utilizan controles basados en formularios web de ASP.NET.
  - MVC. Este marco (introducido en DNN 8) utiliza el marco MVC de ASP.NET.
  - SPA. Esta familia de marcos construye módulos utilizando HTML plano, JavaScript y CSS. Puede usar cualquier framework SPA.
- Puede elegir un enfoque de desarrollo manual, donde todo el módulo se construye a mano, o un enfoque más automatizado, donde la base del módulo se crea utilizando una plantilla u otra herramienta de automatización.
