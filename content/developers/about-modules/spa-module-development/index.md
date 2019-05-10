---
uid: spa-module-development
locale: es
title: Desarrollo de módulos SPA
dnnversion: 09.02.00
related-topics: create-module-using-templates,use-module-creator,providers
links: ["[Wikipedia: Single-Page Application](https://en.wikipedia.org/wiki/Single-page_application)","[DNN Wiki: Token Replacement API](https://www.dnnsoftware.com/wiki/ipropertyaccess)","[DNN Wiki: Standard DNN Tokens](https://www.dnnsoftware.com/wiki/tokens)"]
---

# Desarrollo de módulos SPA

## Visión general

Los marcos de aplicaciones de una sola página (SPA) son una alternativa más nueva a los marcos de desarrollo web del lado del servidor, como ASP.NET. SPA reemplaza las actualizaciones de página completa de los marcos del lado del servidor, con pequeñas actualizaciones dirigidas de elementos seleccionados de la página. Este enfoque ligero da como resultado una interfaz de usuario más rápida y con mayor capacidad de respuesta.

El tipo de módulo SPA de DNN, simplifica la creación de módulos que simulan las aplicaciones SPA tradicionales y que usan AJAX para todas las interacciones del servidor.

El marco del módulo SPA complementa otros marcos para SPA, como AngularJS, Knockout y React, al proporcionar una funcionalidad específica de DNN.

## Arquitectura de un módulo SPA

En un módulo SPA, cada archivo HTML carga el JavaScript y CSS necesarios para representar correctamente la interfaz de usuario UI. Los módulos SPA también realizan llamadas AJAX a la capa empresarial a través de la capa de servicios. Esta arquitectura es similar a la [arquitectura de aplicaciones móviles para los módulos de formularios web](xref:web-forms-module-development).

![Arquitectura lógica de un módulo SPA.](/images/gra-module-architecture-spa.png)

Cuando se solicita una página DNN, el marco busca el control del módulo solicitado en la definición del módulo. En un módulo SPA, el control del módulo identifica un archivo HTML específico. Los tokens de DNN en el archivo HTML se reemplazan con datos específicos del sitio antes de que el HTML se inyecte en la página.

## Construyendo módulos SPA

Tiene más opciones de desarrollo disponibles al construir módulos SPA en comparación con los módulos MVC. El código del lado del servidor se puede crear en Visual Studio como tipos de Proyecto de aplicación web (WAP) o Proyecto de sitio web (WAP). [Consulte Proyectos de aplicaciones web versus proyectos de sitios web en Visual Studio](https://msdn.microsoft.com/en-us/library/dd547590%28v=vs.110%29.aspx). Debido a que la capa de presentación se crea con HTML plano, JavaScript y CSS, sus componentes pueden construirse utilizando cualquier editor de código.

Puede elegir construir el módulo SPA con todo el código de capa de presentación en un proyecto y todo el código del lado del servidor en otro proyecto por separado. Este enfoque facilita el uso de diferentes herramientas de implementación que están optimizadas para el desarrollo del lado del servidor o del lado del cliente.

También, puede usar Visual Studio para crear un proyecto único que incluya componentes tanto del lado del servidor como del lado del cliente. Este enfoque aprovecha el sistema MS Build para empaquetar fácilmente su módulo como parte de su proceso de desarrollo. La plantilla de módulo DNN SPA está configurada con este enfoque.

## Acceso a las características de DNN

Los formularios Web Forms y los módulos MVC pueden acceder fácilmente a las funciones de DNN relacionadas con la representación porque ambas son tecnologías del lado del servidor. Los módulos SPA utilizan tecnología del lado del cliente y, por lo tanto, requieren un enfoque diferente para acceder a las funciones de DNN. Debido a que un módulo SPA utiliza HTML estándar, DNN proporciona tokens personalizados que pueden incluirse en el HTML para acceder a los datos y API.

Los siguientes tokens se pueden utilizar en su HTML:

*   `JavaScript` o `JS` registra un archivo JavaScript con el Administrador de recursos del cliente.
*   `CSS` registra una hoja de estilo con el Administrador de recursos del cliente..
*   `AntiForgeryToken` incluye un token anti-falsificación en la página para evitar ataques de falsificación de solicitudes entre sitios (CSRF).
*   `ModuleAction` identifica las acciones personalizadas del módulo.
*   `Resx` incluye una cadena de recursos localizada en la página.
*   `Request` incluye la cadena de consulta de solicitud de página en la página.
*   `ModuleContext` incluye una propiedad de contexto de módulo DNN en la página. Las propiedades de contexto del módulo compatibles incluyen:
    *   `ModuleId`
    *   `TabModuleId`
    *   `TabId`
    *   `PortalId`
    *   `IsSuperUser`
    *   `EditMode`
    *   `SettingName`. Puede acceder a una configuración de módulo específica utilizando el nombre de configuración, en lugar de un nombre de propiedad predefinido.
