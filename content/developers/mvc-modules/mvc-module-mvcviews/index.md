---
uid: mvc-module-mvcviews
locale: es
title: Vistas MVC
dnnversion: 09.02.00
related-topics: developers-mvc-modules-overview,mvc-module-mvccontroller,mvc-module-unittest,unsupported-mvc-features
---

# Vistas MVC

## The _ViewStart.cshtml

En ASP.NET MVC3 y versiones posteriores, puede definir una vista Razor llamada `ViewStart.cshtml (o _ViewStart.vbhtml para VB)` en la raíz de la carpeta `Views`. Este archivo opcional define el código de vista común que se ejecuta cuando cada vista comienza a renderizarse. Por ejemplo: El código dentro del archivo `_ViewStart.cshtml` puede establecer mediante programación cada propiedad de diseño en `Views/Shared/_Layout.cshtml` de forma predeterminada.

Ejemplo: `Views/_ViewStart.cshtml`:

```

	@{
		Layout = "~/DesktopModules/MVC/CompanyName_MyMvcModule/Views/Shared/_Layout.cshtml";
	}
			
```

Ejemplo: `Views/Shared/_Layout.cshtml`:

```

	<div id="mvcContainer-@Dnn.ActiveModule.ModuleID">
		@RenderBody()
	</div>
			
```

Los archivos anteriores, que se generan a partir de la plantilla de proyecto MVC, aseguran que todas las vistas devueltas por una acción del controlador siempre tendrán un contenedor con un identificador que incluye la identificación del módulo actual. Si elige excluir `_ViewStart.cshtml` de su proyecto, sus vistas de acción individuales simplemente se procesarán sin un ajuste común.

## Convenciones de nomenclatura para vistas

Según las convenciones de patrones MVC, las vistas residen en carpetas dentro de la carpeta Vistas. Cada controlador debe tener una carpeta `Views` con su nombre, por ejemplo el proyecto generado por la plantilla creó dos controladores MVC: `ItemController` y `SettingsController` con sus respectivos controladores: _Views/Item y Views/Settings_.

Nota: Las carpetas `View` normalmente llevan el nombre de sus controladores correspondientes, pero sin la palabra "Controller".

Del mismo modo, los archivos de vista Razor deben nombrarse de acuerdo con los nombres de los métodos de acción de su controlador asociado. Por ejmplo: Tenemos dos vistas de C# Razor en la carpeta `Views` llamados Index.cshtml y Edit.cshtml, que corresponden a los métodos de acción `ItemController.Index()` y `ItemController.Edit()`.

## Enlace de datos en la vista

Además de HTML y JavaScript, los siguientes objetos de servidor se pueden utilizar para complemenetar la vista:

*   Model El objeto modelo que se devuelve en la acción está vinculado a la vista en la declaración genérica dentro de la declaración @inherits en la parte superior de la vista.
    
    ```
    
        @inherits DotNetNuke.Web.Mvc.Framework.DnnWebViewPage<Dnn.Modules.CompanyName.MyMvcModule.Models.Item>
    					
    ```
    
    La línea anterior hará que la clase Item esté disponible para acceder en la vista Razor a través de la propiedad Model. Luego puede inyectar los atributos del modelo en el html:
    
    ```
    
        <span>@Model.ItemName</span>
    					
    ```
    
*   ViewBag Los atributos de ViewBag están disponibles en la vista Razor.
    
    ```
    
        <span class="@ViewBag.TitleClass">@Model.Name</span>
    					
    ```
    
*   HTML Helpers son clases que generan elementos HTML utilizando la clase de modelo. ASP.NET MVC incluye una clase auxiliar @HTML que construye elementos de formulario, como listas desplegables, cuadros de texto y etiquetas.
    
    ```
    
        @Html.TextBoxFor(m => m.Description)
    					
    ```
    
*   DNN Helper La propia clase de ayuda de DNN (@Dnn) proporciona objetos centrales de DNN que puede usar en su vista Razor. PortalSettings, ModuleContext, User y otros objetos proporcionan acceso a la estructura CMS subyacente de su página.
    
    ```
    
        <div id="Items-@Dnn.ModuleContext.ModuleId">
    					
    ```
    

## Navegación entre vistas

Para navegar a otra vista u otra acción del controlador, puede usar el método de acción del ayudante @Url para crear un método de acción de URL que puede colocar en una etiqueta o botón de anclaje. Por ejemplo, en la vista de índice de elemento generado por la plantilla, un hipervínculo en cada elemento puede llevar al usuario a la vista de edición del elemento individual.

```

	<a href="@Url.Action("Edit", "Item", new {ctl = "Edit", itemId = item.ItemId})">@Dnn.LocalizeString("EditItem")</a>
			
```

## Scripts del lado del cliente

Los mecanismos utilizados para registrar scripts, hojas de estilo o bibliotecas Javascript en un módulo DNN se han modificado para que funcionen con módulos MVC.

El registro de una hoja de estilo o secuencia de comandos se puede hacer con Client Resource Manager. También se permite el registro de una extensión de biblioteca de Javascript a través de Javascript Library Extension.

```

	@using DotNetNuke.Web.Client.ClientResourceManagement
	@using DotNetNuke.Framework.JavaScriptLibraries
	@{
		// Register a stylesheet
		ClientResourceManager.RegisterStyleSheet(Dnn.DnnPage, "~/DesktopModules/MVC/CompanyName_MyMvcModule/Resources/css/module.css");

		// Register a custom javascript
		ClientResourceManager.RegisterScript(Dnn.DnnPage, "~/DesktopModules/MVC/CompanyName_MyMvcModule/Resources/js/module.js", 101);

		// Register an existing Javascript Library Extension
		JavaScript.RequestRegistration("Knockout");
	}
			
```

## Localización

Uno de los métodos base en @Dnn MVC es LocalizeString(). Los archivos de recursos para Vistas están organizados en el nivel del controlador en la carpeta `App_LocalResources` en la raíz del proyecto del módulo. Por convención, ItemController debe tener un archivo de recursos llamado `App_LocalResources\Item.resx`. Si había una clave de recurso llamada "lblName.Text", puede extraer ese contenido en su vista usando el siguiente código:

```

	<label for="itemName">@Dnn.LocalizeString("lblName")</label>
			
```
