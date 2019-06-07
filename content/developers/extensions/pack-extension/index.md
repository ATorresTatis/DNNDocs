---
uid: developers-pack-extension
locale: es
title: Empaquetar su extensión
dnnversion: 09.02.00
previous-topic: test-module
next-topic: install-extension
related-topics: dnn-manifest-schema,module-development,web-forms-module-development,spa-module-development,create-module,mvc-module-development,providers
links: ["[DNN Professional Training video: Skinning 5: Packaging](https://www.dnnsoftware.com/services/professional-training/training-videos-subscription/skinning-5-packaging)"]
---

# Empaquetar su extensión

Para facilitar la distribución e instalación, los componentes de una extensión (tema o módulo) se pueden agrupar en un paquete. Un paquete de extensión es simplemente un archivo zip que contiene todos los archivos requeridos por su extensión. La parte más importante del proceso es crear el Manifiesto de DNN, que proporciona la información requerida por el instalador, como las ubicaciones de destino de los archivos.

Si usa las plantillas de DNN y compila con Visual Studio, la compilación de la versión crea el archivo zip por usted.

Nota: el asistente de paquetes, al que se puede acceder a través del DNN Module Creator o la página de extensiones, actualmente no puede crear paquetes para los módulos de tipo MVC o SPA.


## Pasos

1.  Prepare sus archivos en carpetas.

    *   Archivos que comúnmente se incluyen en todos los paquetes:
        *   (Opcional) `MyLicense.txt` se muestra al usuario durante la instalación del paquete.
        *   (Opcional) `MyReleaseNotes.txt` enumera los cambios para la versión actual del paquete y también se muestra durante la instalación.
    *   Archivos incluidos en los paquetes de módulos de tipo MVC y SPA:
        *   Requeridos
            *   Vistas (.cshtml o .vbhtml) que contienen el marcado necesario para representar la interfaz de usuario del módulo.
            *   El archivo de manifiesto (.dnn) que contiene la información de definición de módulo requerida para instalar el módulo.
            *   Ensamblados (.dll) queson el código del módulo compilado y las bibliotecas de referencia de terceros. Los proyectos de WSP no tendrán un ensamblado compilado, pero aún pueden incluir bibliotecas de referencia de terceros.
            *   Scripts de SQL (.sqldataprovider) son el código requerido para crear o actualizar los objetos de la base de datos de su módulo.
        *   Opcional
            *   Los archivos de recursos (.resx) contienen cadenas de localización.
            *   Los archivos JavaScript (.js) contienen el código utilizado para la lógica del lado del cliente.
            *   Las hojas de estilo (.css) contienen los estilos personalizados que necesita su módulo.
            *   Los archivos de texto (.txt) que incluyen los archivos release.txt y license.txt que se muestran durante la instalación del módulo.

   Sugerencia: la licencia y las notas de la versión son archivos HTML, por lo que puede incluir ofertas especiales, incluida una llamada a la acción y otros detalles.

    Recuerde: incluya el número de versión de su extensión en las notas de la versión.

2.  Cree el [archivo de manifiesto de DNN](xref:dnn-manifest-schema).
3.  Comprima sus archivos, incluido el Manifiesto DNN en la carpeta raíz.
