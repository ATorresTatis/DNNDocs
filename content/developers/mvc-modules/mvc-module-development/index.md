---
uid: mvc-module-development
locale: es
title: Desarrollo de un módulo MVC
dnnversion: 09.02.00
related-topics: create-module-using-templates,use-module-creator,providers
links: ["[Wikipedia: Model-View-Controller](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)"]
---

# Desarrollo de un módulo MVC

## Visión general

El tipo de módulo MVC integra ASP.NET MVC 5 con la plataforma DNN.

> [!Nota] Las incompatibilidades entre ASP.NET MVC y ASP.NET Web Forms causan conflictos con algunas características de Formularios Web preexistentes en la plataforma DNN. Por lo tanto, las implementaciones de DNN de algunas características de ASP.NET, como el enrutamiento MVC, son limitadas.

Los módulos MVC pueden usar cualquiera de las características de un módulo DNN estándar. Todos los tipos de módulos de DNN pueden coexistir en una sola página, y el usuario no debería poder distinguir qué marco se utilizó para construir cada módulo.

## Arquitectura de un módulo MVC

Los módulos del tipo MVC implementan el patrón modelo-vista-controlador, que separa una aplicación en tres componentes principales:

*   **Modelos/Models** que implementan la lógica del dominio y a menudo, almacenan y recuperan datos de la base de datos.
*   **Vistas/Views** que representan la interfaz de usuario (IU) del módulo. Normalmente, las vistas se crean en función de los datos proporcionados por el modelo.

    ```

        @model IEnumerable<Dnn.Modules.DnnMvcModule.Models.Item>

        <div id="Items-@Dnn.ModuleContext.ModuleId">
            @if (Model.Count() == 0)
            {
                <p>No items defined.</p>
            }
            else
            {
                <ul class="tm_tl">
                    @foreach (var item in Model)
                    {
                        <li class="tm_t">
                            <h3>@item.ItemName</h3>
                            <div class="tm_td">@item.ItemDescription</div>
                            @{
                                if (Dnn.ModuleContext.IsEditable)
                                {
                                    <div>
                                        <a href="@Url.Action("Edit", "Item", new {ctl = "Edit", itemId = item.ItemId})">@Dnn.LocalizeString("EditItem")</a>
                                        <a href="@Url.Action("Delete", "Item", new {itemId = item.ItemId})">@Dnn.LocalizeString("DeleteItem")</a>
                                    </div>
                                }
                            }
                        </li>
                    }
                </ul>
            }
        </div>

    ```

*   **Controladores/Controllers** que manejan la interacción del usuario, recuperan y actualizan el modelo, y seleccionan la vista a utilizar.

Aunque la composición de la capa de presentación es diferente, la arquitectura lógica de un módulo MVC es similar a la de un módulo de formularios web

    ![Logical architecture of an MVC module](/images/gra-module-architecture-mvc.png)

    Cuando se solicita una página DNN, el marco busca el control del módulo solicitado en la definición del módulo. En un módulo MVC, el control del módulo identifica un espacio de nombres, un controlador y una acción específicos. La salida de la acción del controlador se almacena en una cadena, que se inyecta en la página.


## Construyendo módulos MVC

Visual Studio solo admite un tipo de proyecto para proyectos MVC. Sin embargo, el tipo de proyecto de Visual Studio MVC incluye plantillas adicionales para crear nuevos controladores y vistas. Las plantillas adicionales, aceleran el desarrollo y garantizan que los controladores y las vistas sigan las convenciones estándar de MVC.

> [!Nota> Visual Studio es actualmente la única herramienta disponible para crear módulos MVC.

El marco ASP.NET MVC se basa en la convención sobre el [paradigma de configuración](https://en.wikipedia.org/wiki/Convention_over_configuration) para simplificar el desarrollo. Los módulos de DNN siguen todas las convenciones de ASP.NET MVC, así como las convenciones específicas de DNN. Las convenciones del módulo MVC incluyen:

*   Convenciones de nombres de archivos

    |**Tipo de archivo**|**Convención**|
    |---|---|
    |Controladores/Controller|El nombre debe incluir el sufijo "Controller".|
    |Vista predeterminada/Default View|El nombre debe ser el mismo que la acción asociada. Por ejemplo: La vista predeterminada para una acción del **index/índice** debe denominarse **index.cshtml.**|
    |Diseño compartido/Shared layout|El nombre debe ir prefijado con un guion bajo (_).|

*   Convenciones de ubicación de archivos

    |**Tipo de archivo**|**Convención**|
    |---|---|
    |Vista/View|La carpeta **Views** ebbe coincidir con el nombre del controlador. Por ejemplo: Una vista para el controlador  **Home** debería estar en la carpeta **Views/Home**.|
    |Diseño compartido/Shared layout|En la carpeta **Views/Shared**|
    |MVC module|En la carpeta **DesktopModules/MVC**|
    |Controladores/Controller|En la carpeta **Controllers** (opcional)|
    |Modelos/Model|En la carpeta **Models**|
    |Archivos de contenido estático (ej., hojas de estilo e imagenes)|En la carpeta **Content**|
    |Archivos de JavaScript|En la carpeta **Scripts**|

*   Otras convenciones
    *   Los campos de un formulario HTML enlazados deben tener el mismo nombre que la propiedad del modelo correspondiente

## Accediendo a las funciones de DNN

Las funciones comunes de DNN se ponen a disposición de los desarrolladores de MVC a través de las API de DNN, como:

*   **Localización**. El objeto auxiliar (helper) DNN incluye un método **LocalizeString** . Este objeto auxiliar o helper se puede usar en su vista cuando localice su módulo.
*   **Acciones del módulo**. DNN incluye los atributos **ModuleAction** y **ModuleActionItems** para identificar acciones de módulos personalizados. Estos atributos solo se pueden utilizar con los métodos de acción del controlador.
*   **Controlador de clase base**. Los controladores MVC deben heredar de la clase **DnnController**. Similar a la clase **PortalModuleBase** para los desarrolladores de módulos de Formularios Web, esta clase proporciona acceso al módulo DNN y a los objetos de contexto del portal.
