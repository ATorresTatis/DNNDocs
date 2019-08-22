---
uid: mvc-module-project-overview
locale: es
title: Descripción del proyecto de módulo MVC
dnnversion: 09.02.00
related-topics: create-module-using-templates
---

# Descripción del proyecto de módulo MVC

## Descripción general de un proyecto de módulo MVC

Después de crear su proyecto de módulo MVC a partir de una plantilla, la siguiente estructura del proyecto será lo que vea en su proyecto de Visual Studio  

![Proyecto de Visual Studio MVC](/images/scr-mvc-project-vssolution.png)

  
*   Modelos, vistas, carpetas de controladores y código de ejemplo.
*   Carpeta de componentes con controladores de negocio del módulo y clase DAL.
*   Ejemplos de archivos de empaquetado del módulo: archivo de manifiesto DNN, notas de la versión y texto de licencia, y scripts SQL para la instalación y desinstalación
*   Proceso de empaquetado del módulo MSBuild para construir el archivo ejecutable .zip

## Código de proyecto inicial de la plantilla

Después de crear el módulo y compilar el paquete, vaya a Host \> Extensiones para instalar el paquete. Después de la instalación, puede agregar el módulo a una página para realizar pruebas. El código inicial creado por la plantilla debería verse así:

  
![Módulo inicial MVC DNN](/images/scr-mvc-module-template-view.png)
 

Ya sea que use la plantilla de DNN 8 MVC o una plantilla MVC similar, el código generado produce una aplicación totalmente funcional que le permite agregar elementos a una lista. La vista predeterminada es la lista de elementos. Cada modelo de datos o elemento consta de un título, descripción del contenido y el usuario que creo el registro. La plantilla genera los controladores MVC, las vistas y las entidades del modelo, así como una clase controladora para el acceso a los datos. Si su módulo realizará operaciones de datos CRUD (Crear, Leer, Actualizar, Eliminar), puede personalizar este código. De lo contrario, puede eliminar lo que no necesita
