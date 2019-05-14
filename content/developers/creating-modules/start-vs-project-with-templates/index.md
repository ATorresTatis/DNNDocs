---
uid: start-vs-project-with-templates
locale: es
title: Iniciar un proyecto de Visual Studio con plantillas
dnnversion: 09.02.00
previous-topic: create-module-using-templates
next-topic: test-module
links: ["[Blog de la comunidad de DNN: Desarrollo de módulos para no desarrolladores, expertos en temas o principiantes de DNN - Serie de blogs por Clinton Patterson](https://www.dnnsoftware.com/community-blog/cid/155064/module-development-for-non-developers-skinners-dnn-beginners--blog-series-intro)","[Uso de las nuevas plantillas de desarrollo de módulos para DotNetNuke 7 por Chris Hammond](https://www.chrishammond.com/blog/itemid/2616/using-the-new-module-development-templates-for-dot)"]
---

# Iniciar un proyecto de Visual Studio con plantillas

## Pre-requisitos

*   [Una instalación de DNN local con permisos de host](xref:set-up-dnn)
*   Visual Studio 2015 es el IDE recomendado para desarrollar módulos DNN.

## Pasos

1.  Descargue e instale las plantillas (Chris Hammond).    

    1.  Ejecute Visual Studio como un usario administrador.
    2.  Vaya a Herramientas> Extensiones y actualizaciones.

        ![Herramientas> Extensiones y actualizaciones](/images/scr-VS2015ExtAndUpdates.png)



    3.  Vaya en el árbol a la ocpión En línea > Galería de Visual Studio y busque DotNetNuke.

        ![En línea> Galería de Visual Studio, busque DotNetNuke y descargue](/images/scr-VS2015Search4DNN.png)


    4.  Haga clic en el botón Descargar para obtener las plantillas del proyecto de DotNetNuke.

    > [!Nota] Vea las instrcciones de [Chris Hammond's](https://www.chrishammond.com/blog/itemid/2616/using-the-new-module-development-templates-for-dot) para conocer otras formas de instalación.

    Para plantillas de DNN 8

    1.  [Descargue el archivo .vsix apropiado](https://github.com/dnnsoftware/DNN.Templates/releases)

        Se incluyen dos:

        *   Dnn.Mvc.Module.vsix
        *   Dnn.Spa.Module.vsix

        ![Descargar las plantillas de DNN8 desde Github](/images/scr-VS2015DNN8Templates-11.png)

    2.  En su carpeta de descarga, haga doble clic en el archivo .vsix para instalar la plantilla en Visual Studio.
2.  Cree un nuevo proyecto de Visual Studio.
    1.  Ejecute Visual Studio como un usuario administrador.
    2.  Archivo \> Nuevo \> Proyecto
    3.  Seleccione la plantilla para el nuevo proyecto.

        Para las plantillas de Chris Hammond, vaya a Plantillas \> Visual C # o Visual Basic \> DotNetNuke.

        ![Visual Studio \> Nuevo \> Proyecto con plantillas de Chris Hammond](/images/scr-VS2015NewProjectWithTemplates-02.png)

        Para las plantillas de DNN 8, vaya a Plantillas \> Visual C # \> DNN.

        ![Visual Studio \> Nuevo \> Proyecto con plantillas DNN8](/images/scr-VS2015NewProjectWithTemplates-01.png)

    4.  Ingrese los ajustes

        *   Nombre: El nombre de su nuevo módulo.
        *   Ubicación: Una subcarpeta dentro de la carpeta `DesktopModules` en su carpeta de instalación de DNN.


        >[!Sugerencia] Utilice el nombre de su empresa o un nombre único como nombre de la subcarpeta para evitar conflictos con otros creadores de módulos en un entorno de producción.

    5.  Desmarque la opción crear directorio para solución

        Las plantillas esperan que el archivo de solución de Visual Studio (.sln) esté en la misma carpeta que el archivo de proyecto. Al marcar esta opción, el archivo de la solución se coloca en una carpeta diferente, lo que puede causar errores de compilación.

3.  Modifique el proyecto de Visual Studio para agregar la funcionalidad a su nuevo módulo.
