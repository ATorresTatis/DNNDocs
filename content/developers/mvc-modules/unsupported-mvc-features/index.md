---
uid: unsupported-mvc-features
locale: es
title: Funciones MVC no compatibles
dnnversion: 09.02.00
related-topics: developers-mvc-modules-overview,mvc-module-mvccontroller,mvc-module-mvcviews,mvc-module-unittest
---

# Funciones MVC no compatibles

Algunas características de MVC no se implementaron completamente en DNN 8 debido a las diferencias entre los marcos de ASP.NET MVC y ASP.NET Web Forms.

*   Ayudantes de HTML
    *   Extensiones de formulario (BeginForm, BeginRouteForm, EndForm)
    *   Html.RouteLink
    *   Todas las Extensiones de ChildAction (por ejemplo, Html.Action, Html.RenderAction)
*   Ayudantes de URL
    *   Url.Action(string actionName, string controllerName, RouteValueDictionary routeValues, string protocol)
    *   Url.Action(string actionName, string controllerName, object routeValues, string protocol)
    *   Url.Action(string actionName, string controllerName, RouteValueDictionary routeValues, string protocol, string hostName)
    *   Url.RouteUrl
    *   Url.HttpRouteUrl
*   Tipos de retorno de acción del controlador. DNN 8 espera que las acciones devuelvan un ActionResult. Todos los demás tipos de resultados no son compatibles actualmente:
    *   ContentResult
    *   EmptyResult
    *   FileResult
    *   FileStreamResult
    *   RedirectResults
    *   RedirectToRouteResult
*   Controladores asíncronos
*   Enrutamiento por atributos
*   Bundles. DNN implementa una API de minificación y agrupación diferente para módulos MVC.

Se esperan las siguientes características en una versión futura:

*   Ayudantes de AJAX
