---
uid: web-forms-module-development
locale: es
title: Desarrollo de módulos de formularios web
dnnversion: 09.02.00
related-topics: use-module-creator,providers
links: ["[Module Development: DNN Video Library](https://www.dnnsoftware.com/videos/)"]
---

# Desarrollo de módulos de formularios web

## Arquitectura de módulos de formularios web

Los módulos de Web Forms siguen el patrón arquitectónico del módulo DNN estándar y utilizan un modelo de renderizado tradicional del lado del servidor. Cuando se solicita una página, DNN creará una instancia del control del módulo relevante como se encuentre definida en la configuración del módulo. El control de módulo se hereda de una clase de código subyacente que contiene la lógica de presentación y que realiza llamadas adicionales a los métodos de negocios apropiados en la capa de lógica de negocios.

![Arquitectura lógica de un módulo de formularios web.](/images/gra-module-architecture-wf.png)

Puede incluir puntos finales (endpoints) de servicios web para permitir el acceso de las aplicaciones móviles, si es necesario. Cuando se accede al módulo desde una aplicación móvil, la capa de presentación se mueve al dispositivo móvil y la capa de servicios se convierte en el punto final (endpoint) del lado del servidor que llama a los métodos comerciales apropiados.

![Acceso al módulo de formularios web a través de un servicio web](/images/gra-module-architecture-mobile.png)


## Construyendo Módulos de Formularios Web

En Visual Studio, los módulos se pueden crear como uno de estos tipos de proyectos:

*   Web Site Project (WSP)
*   Web Application Project (WAP)

Los módulos creados utilizando el tipo de proyecto WSP incluyen el código fuente como parte del paquete del módulo. El código fuente se compila en tiempo de ejecución, lo que le permite modificar fácilmente el código directamente en el servidor. Si bien este enfoque proporciona flexibilidad para realizar actualizaciones, también reduce el rendimiento de inicio y puede complicar las actualizaciones de los módulos.

> Importante: El tipo de proyecto WSP no se recomienda para el desarrollo de módulos comerciales, ya que requiere la distribución del código fuente con su módulo.

Los proyectos WSP no tienen un archivo de proyecto (.csproj o .vbproj). En su lugar, se basan en archivos que forman parte de un sitio web completo. Al crear un módulo WSP, todos los controles de usuario, los archivos de código subyacente asociados y otros archivos relacionados se colocan en una carpeta de proyecto en la carpeta `DesktopModules`. Todos los archivos de código no asociados con un control de usuario deben colocarse en la carpeta `App_Code` en la raíz del sitio web. Este modelo de código inconexo complica el desarrollo y el empaquetado del módulo.

Los módulos creados utilizando el tipo de proyecto WAP se compilan en el momento del desarrollo y no requieren que incluya el código fuente en su módulo. Los proyectos WAP tienen un archivo de proyecto y se crean como proyectos independientes.

> Nota: Microsoft recomienda el tipo de proyecto WAP para el desarrollo de ASP.NET. (Consulte [Proyectos de aplicaciones web versus proyectos de sitios web en Visual Studio](https://docs.microsoft.com/en-us/previous-versions/aspnet/dd547590(v=vs.110))).

Aunque se recomienda Visual Studio para el desarrollo de módulos, puede crear módulos utilizando editores de texto estándar o la funcionalidad de DNN Module Creator que viene incluida. Sin embargo, estas herramientas no proporcionan soporte para el compilador .NET; por lo tanto, son más adecuados para desarrollar módulos basados en WSP.

Puede organizar sus archivos de proyecto de Web Forms de la forma que desee. Muchos desarrolladores de módulos organizan archivos de proyectos basados en la arquitectura lógica.

## Empaquetar módulos de formularios web

Los módulos creados con el tipo de proyecto WAP pueden aprovechar los scripts de MS Build para agrupar automáticamente los archivos del módulo y el manifiesto del módulo. Los módulos basados en WSP se pueden empaquetar utilizando el asistente de paquetes que está disponible en DNN.

Independientemente del tipo de proyecto, los paquetes de módulos de Web Forms incluyen los siguientes archivos:

*   Requeridos
    * Los controles de usuario `(.ascx)` que contienen el marcado necesario para representar la interfaz de usuario UI del módulo.
    * Los archivos de código `(.cs o .vb)` que contienen la lógica empresarial, lógica de almacenamiento en caché y/o el código de acceso a datos (solo se incluyen para los tipos de proyectos WSP).
    * El archivo de manifiesto `(.dnn)` que contiene la información de definición de módulo requerida para su instalación.
    * Los archivos `(.dll)` que son el código del módulo compilado y las bibliotecas de referencia de terceros. Los proyectos WSP no tendrán un ensamblado compilado para el módulo, pero podrían incluir referencias a bibliotecas de terceros.
    * Los scripts SQL `(.sqldataprovider)` que son el código requerido para crear o actualizar los objetos de la base de datos de su módulo.
*   Opcionales
    * Los archivos de recursos `(.resx)` que contienen cadenas de localización.
    * Los archivos JavaScript `(.js)` que contienen el código utilizado para la lógica del lado del cliente.
    * Las hojas de estilo `(.css)` que contienen los estilos personalizados de presentación que necesita su módulo.
    * Los archivos de texto `(.txt)` que incluyen los archivos release.txt y license.txt que se muestran durante la instalación del módulo.

La funcionalidad de DNN Module Creator coloca automáticamente los archivos en las carpetas apropiadas (`App_Code` y `DesktopModules`) y puede usarse para empaquetar el módulo una vez está completado.
