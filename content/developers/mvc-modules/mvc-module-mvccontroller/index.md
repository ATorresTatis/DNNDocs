---
uid: mvc-module-mvccontroller
locale: es
title: MVC Controller
dnnversion: 09.02.00
related-topics: create-module-using-templates,developers-mvc-modules-overview,mvc-module-mvcviews,mvc-module-unittest,unsupported-mvc-features
---

# Controlador MVC

## Visión general

En un módulo de formularios web, el módulo está controlado por archivos `.ascx` que representan controles de usuario y se muestran en la página. Sin embargo, en un módulo MVC, el módulo está controlado por métodos de acción del controlador MVC que devuelven una vista MVC, para que se representa en la página

## Métodos de acción

Para representar un control de módulo MVC, DNN usa la definición de fuente de control del módulo. Si su proyecto se creó a partir de la plantilla DNN MVC, el manifiesto define una vista predeterminada con el siguiente código fuente:

```

    <moduleControl>
        <controlKey />
        <controlSrc>Dnn.Modules.CompanyName.MyMvcModule.Controllers/Item/Index.mvc</controlSrc>
        ...
    </moduleControl>
			
```

> [!Nota]: El valor de controlSrc no es una ruta de archivo. En un módulo de MVC, las fuentes de control se especifican utilizando el formato: `{Controller Namespace}/{Controller Name}Controller/{Action Method Name}.mvc`

El fuente del control anterior busca el método Index() en la clase Dnn.Modules.CompanyName.MyMvcModule.Controllers.ItemController, que hereda de la clase base abstracta DotNetNuke.Web.Mvc.Framework.Controllers.DnnController.

Ejemplo: en el siguiente código, el método de acción solicita a la capa de datos (ItemManager) la lista de todos los objetos de elementos para esa instancia de módulo

```

    public class ItemController : DnnController
    {
        public ActionResult Index()
        {
            var items = ItemManager.Instance.GetItems(ModuleContext.ModuleId);
            return View(items);
        }
    }
                
```

La lista resultante son los datos del Modelo, que se devuelven y luego se pasan al componente de vista.

## Menú de acción del módulo
 
![Menú de acción del módulo](/images/scr-actionmenu-edit-icons.png)

  
El menú de acción del módulo se puede personalizar para su módulo MVC agregando un atributo  DotNetNuke.Web.Mvc.Framework.ActionFilters.ModuleActionAttribute al método de acción de la vista predeterminada.

El siguiente extracto de código se encuentra sobre en el método ItemController.Index() en el ejemplo proporcionado por el proyecto de plantilla MVC.

```

    [ModuleAction(ControlKey = "Edit", TitleKey = "AddItem")]
    public ActionResult Index()
    {
        ...
    }
			
```

Las propiedades de ModuleActionAttribute incluyen:

*   ControlKey. El nombre de la clave del control de vista del módulo, que se utiliza para especificar la acción del controlador que se invoca cuando el usuario hace clic en el elemento del menú.
*   Icon. La imagen que se utilizará como el icono junto al texto del elemento del menú. El valor predeterminado es el ícono de lápiz.
*   SecurityAccessLevel. El nivel de acceso requerido para acceder al elemento del menú. Alguno de los valores enumerados en DotNetNuke.Security.SecurityAccessLevel.
*   Title. El texto del elemento del menú.
*   TitleKey. La clave del elemento del menú. Si obtiene el texto de un archivo de recursos, use esto en lugar del atributo Title. En el ejemplo anterior, esperaría un recurso con el identificador `AddItem.Text` en el archivo Item.resx.

## Devolver el resultado de la acción

El objetivo principal de los métodos de acción del controlador MVC es representar una vista con los datos del modelo. El tipo de retorno de los métodos de acción es del tipo abstracto System.Web.Mvc.ActionResult, que tiene muchos subtipos posibles, incluidos los dos tipos de retorno que se usan más comúnmente para un módulo DNN MVC: ViewResult y RedirectToRouteResult.

ViewResult devuelve una vista renderizada que lleva el nombre del método de acción. RedirectToRouteResult redirige a otra acción del controlador, del mismo modo, que DnnController.RedirectToDefaultRoute() generalmente se llama para redirigir a la vista de módulo predeterminada.

Nota: Vea [Características MVC no compatibles](xref:unsupported-mvc-features) para obtener una lista de los tipos de ActionResult no compatibles.

## Pasar datos a la vista

Las dos construcciones que generalmente se utilizan para pasar datos a la vista son el Model y ViewBag.

*   Model
    
    El modelo es un "objeto CLR antiguo simple" (POCO). Al usar la capa de datos de su módulo, es común usar una clase de entidad DAL2 como su modelo. Desde el código generado por la plantilla, el ItemManager es una clase de repositorio de datos DAL2 que llena una lista IEnumerable de objetos Item. La lista se pasa a la Vista, donde el código Razor genera el código HTML.
    
    ```
    
        public ActionResult Index()
        {
            var items = ItemManager.Instance.GetItems(ModuleContext.ModuleId);
            return View(items);
        }
    					
    ```
    
*   ViewBag
    
    Las vistas MVC se crean para representar un modelo específico. Ocasionalmente, pasar datos adicionales a la vista fuera del alcance del modelo puede ser útil; por ejemplo, al pasar la ruta relativa del módulo para evitar codificar una hoja de estilo en la vista. Debido a que ViewBag permite propiedades dinámicas, puede definir una nueva propiedad dinámica (por ejemplo, ModulePath) para el método de acción y usar esa propiedad en su vista.
    
    Ejemplo: ItemController.cs
    
    ```
    
        public ActionResult Index()
        {
            var items = ItemManager.Instance.GetItems(ModuleContext.ModuleId);
            ViewBag.ModulePath = $"~/DesktopModules/MVC/{ModuleContext.Configuration.DesktopModule.FolderName}";
            return View(items);
        }
    					
    ```
    
    Ejemplo: Index.cshtml
    
    ```
    
        @{
            ClientResourceManager.RegisterStyleSheet(Dnn.DnnPage, ViewBag.ModulePath + "/Resources/bootstrap/css/bootstrap.min.css");
        }
    					
    ```
