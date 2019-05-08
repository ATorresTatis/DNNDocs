---
uid: module-development
locale: es
title: Acerca del desarrollo de módulos
dnnversion: 09.02.00
related-topics: providers
---

# Acerca del desarrollo de módulos

## ¿Qué es un módulo??

Una página web típica incluye elementos de página y bloques de contenido. Los elementos de la página, como el menú del sitio, el control de inicio de sesión y la barra de búsqueda, se incluyen con el tema. Los bloques de contenido son gestionados por módulos.

  

![Modules manage and display content on the page.](/images/gra-module-overview.png)

  

El módulo es uno de los bloques de construcción básicos que extienden a DNN para permitir a los usuarios ver, crear y editar contenido. Todas las características administrativas de DNN se implementan como módulos.

> [!Sugerencia] El código fuente de  DNN incluye numerosos módulos de ejemplo para ayudarlo a construir sus propios módulos.

Debido a la naturaleza modular de la composición de las páginas en DNN, los módulos generalmente se construyen para administrar y mostrar un único tipo de contenido.

> [!Sugerencia] Considere la posibilidad de crear múltiples módulos cuando administre tipos de contenido complejos, o incluya un amplio soporte de plantillas para que los administradores puedan controlar el diseño del contenido en la página.

El desarrollo de un módulo implica seleccionar el marco de desarrollo y luego el enfoque de desarrollo.

*   Estos marcos se pueden utilizar con DNN:
    *   Web Forms. Este marco tradicional crea módulos de DNN que utilizan controles basados en formularios web de ASP.NET.
    *   MVC. Este marco (introducido en DNN 8) utiliza el marco MVC de ASP.NET.
    *   SPA. Esta familia de marcos construye módulos utilizando HTML, JavaScript y CSS. Puedes usar cualquier framework SPA.
*   Puede elegir un enfoque de desarrollo manual, donde todo el módulo se construye a mano, o un enfoque más automatizado, donde la base del módulo básico se crea utilizando una plantilla u otra herramienta de automatización.
