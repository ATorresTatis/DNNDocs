---
uid: developers-mvc-modules-overview
locale: es
title: Módulos MVC
dnnversion: 09.02.00
related-topics: mvc-module-mvccontroller,mvc-module-mvcviews,mvc-module-unittest,unsupported-mvc-features
---

# Módulos MVC

## Proyecto de Módulo MVC

Después de crear un proyecto de módulo MVC a partir de una plantilla, el proyecto se verá con la siguiente estructura en Visual Studio:

 ![Visual Studio MVC project](/images/scr-mvc-project-vssolution.png)

*   Modelos, vistas, carpetas de controladores y código de ejemplo.
*   Una carpeta de componentes con el esqueleto del controlador de negocios del módulo y una clase DAL.
*   Una muestra del empaquetado de archivos con el archivo de manifiesto DNN, las notas de la versión y el texto de la licencia, además de los scripts SQL para la instalación y desinstalación
*   Proceso de empaquetado del módulo para MSBuild al compilar el archivo ejecutable en uno .zip

## Código inicial del proyecto de la plantilla

Después de crear el módulo y construir el paquete, vaya a **Host \> Extensiones** para instalar el paquete. Después de la instalación, puede agregar el módulo a una página para probar. El código inicial creado por la plantilla debe verse así:  

![Initial MVC DNN Module](/images/scr-mvc-module-template-view.png)

  
Ya sea que use la plantilla DNN 8 MVC o una plantilla MVC similar, el código generado produce una aplicación completamente funcional que le permite agregar elementos a una lista. La vista predeterminada es la lista de elementos. Cada elemento del modelo consta de un título, una descripción y el usuario que lo creo. La plantilla genera los controladores MVC, las vistas y las entidades del modelo, así como una clase de controlador de datos. Si su módulo realizará operaciones de datos CRUD (Create, Read, Update, Delete), puede personalizar este código. De lo contrario, puede eliminar lo que no necesite.
