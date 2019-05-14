---
uid: create-module-using-templates
locale: es
title: Crear un módulo usando plantillas
dnnversion: 09.02.00
previous-topic: use-module-creator
next-topic: start-vs-project-with-templates
related-topics: mvc-module-development,spa-module-development,providers
links: ["[DNN API Reference](https://www.dnnsoftware.com/dnn-api/)","[DNN Wiki: Module Development](https://www.dnnsoftware.com/wiki/module-development)","[DNN Community Blog: Module Development series by Clinton Patterson](https://www.dnnsoftware.com/community-blog/cid/155064/module-development-for-non-developers-skinners-dnn-beginners--blog-series-intro)","[Using the new Module Development Templates for DotNetNuke 7 by Chris Hammond](https://www.chrishammond.com/blog/itemid/2616/using-the-new-module-development-templates-for-dot)"]
---

# Crear un módulo usando plantillas

## Pre-requisitos

*   [Una instalación de DNN local](xref:set-up-dnn) con permisos de host.
*   Visual Studio 2015 es el IDE recomendado para desarrollar módulos DNN.

## Pasos

1.  [Inicie un proyecto de Visual Studio usando plantillas DNN](xref:start-vs-project-with-templates).
2.  Modifique el proyecto de Visual Studio para agregar la funcionalidad a su nuevo módulo.
3.  Construir, depurar y empaquetar.

    ![Tipo de construcción de Visual Studio desplegable](/images/scr-VS2015DebugReleaseBuildOptions.png)

    1.  Genere en modo de depuración.

        Esta compilación genera archivos .pdb que son necesarios cuando se depura su código.
    2.  Depure, si es necesario.
    3.  Cree el archivo de [Manifiesto DNN](xref:dnn-manifest-schema).
    4.  Genere en modo de lanzamiento..

        La compilación crea un archivo zip de instalación (para que empaquete su módulo) en la carpeta `DesktopModules` de su organización/módulo/instalación.

    5.  Alternativamente, puede [empaquetar manualmente su módulo](xref:developers-pack-extension).
