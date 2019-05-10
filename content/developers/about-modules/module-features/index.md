---
uid: module-features
locale: es
title: Características comunes de módulos
dnnversion: 09.02.00
related-topics: dnn-manifest-schema,module-architecture,developers-creating-modules-overview,about-evs
links: ["[DNN Module APIs](https://www.dnnsoftware.com/dnn-api/)"]
---

# Características comunes de módulos

## Temas y Contenedores

Aunque tradicionalmente no se considera parte del desarrollo de un módulo, los temas y los contenedores definen cómo se muestra un módulo en una página. Comprender la relación entre estos elementos le ayudará a construir módulos que funcionen bien con otro contenido de la página.

Los temas definen la apariencia de las páginas dentro de DNN, y los módulos deben diseñarse para funcionar con una amplia variedad de estilos. A través de la colocación de los paneles, el tema define dónde se pueden colocar los módulos en una página web.

> [!Sugerencia] Si elige definir estilos específicos para su módulo, especifique el alcance de sus estilos en un elemento raíz (generalmente un `<div>` que envuelve su HTML de marcado) dentro de su módulo. Esto asegura que sus estilos serán más específicos que los estilos definidos en el tema.

DNN envuelve un contenedor alrededor de cada módulo en la página. Además de definir la apariencia de los bloques de contenido en la página, el contenedor también proporciona elementos de IU que administran el módulo, como el título, el menú de acción y los enlaces de acción  del módulo.

## Menú de acciones

El menú de acción del módulo proporciona una funcionalidad estándar, como eliminación de módulos, impresión, importación/exportación y  ubicación del contenido. Los elementos del menú se crean dinámicamente según las características del módulo y la configuración del sitio.

![Menú de acciones](/images/scr-actionmenu-edit-icons.png)



Puede personalizar el menú de acción del módulo implementando las siguientes funciones en su módulo:

*   Proporcionar un enlace a un manifiesto de la página de ayuda para establecer el enlace a la ayuda en el menú.

*   Implemente la interfaz `IPortable` para mostrar las opciones de Importar y Exportar en el menú.

    Nota: DNN también utiliza la interfaz `IPortable` cuando se crea o utiliza una página/plantilla de portal.

*   Implemente la interfaz `ISearchable` para mostrar el enlace de Sindicación en el menú.

    Nota: Un administrador debe habilitar la función de Sindicación de contenido en la configuración del módulo.
   
*  Implemente la interfaz `IActionable` para mostrar elementos de menú personalizados.

    Nota: los elementos del menú personalizado se incluyen en el menú del icono del lápiz. Si `IActionable` no está implementado, entonces el icono del lápiz no se mostrará.


## Ajustes/Configuraciones del módulo

DNN incluye los objetos de configuración para las entidades Host, Portal, Tab, TabModule y Module. Para simplificar el desarrollo de módulos, DNN administra el almacenamiento y la recuperación de estos valores de configuraciones. Es posible que deba acceder a estos valores para determinar cuáles de las funciones de su módulo habilitar.

También puede crear configuraciones personalizadas y la IU asociada para administrar dichas configuraciones personalizadas.

![Ajustes del módulo](/images/scr-module-settings.png)



## Empaquedato

Los módulos deben estar empaquetados en un formato estándar para compartirlos con otros sitios de DNN. Los paquetes DNN son esencialmente archivos .zip que incluyen un manifiesto DNN personalizado. El manifiesto es un archivo XML con una extensión .dnn; que define cómo se instalan los componentes de su módulo.

Se pueden crear estos paquetes:

*   Manualmente,
*   Utilizando el asistente de empaquetado de módulos, que está disponible a través del Creador de módulos en la página de Extensiones

    ![Haga clic en Crear paquete para iniciar el asistente](/images/scr-module-package.png)


*   Mediante el uso de scripts de construcción que vienen con las plantillas de módulo estándar.

## Seguridad

DNN viene con un sistema de control de acceso basado en roles que proporciona control granular a nivel de sitio, nivel de página y nivel de módulo. Puede ampliar este sistema para aumentar la granularidad de la configuración de permisos en el nivel de módulo.

![Incluir permisos de módulos personalizados](/images/scr-module-permissions.png)

Los módulos también pueden llamar a las API de seguridad de DNN para verificar los permisos actuales de un usuario antes de habilitar funciones seguras.
