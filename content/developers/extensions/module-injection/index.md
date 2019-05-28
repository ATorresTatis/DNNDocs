---
uid: module-injection-filter
locale: es
title: Filtros de inyección de módulos
dnnversion: 09.02.00
related-topics: module-features,developers-creating-modules-overview
links: ["[Blog de la comunidad de DNN: descubra los filtros de inyección del módulo DNN](https://www.dnnsoftware.com/community-blog/cid/155402/discover-dnn-module-injection-filters)","[Ejemplos de filtro de inyección en GitHub](https://github.com/dnnsoftware/Dnn.InjectionFilter.Sample)"]
---

# Filtros de inyección de módulos

Los filtros de inyección de módulos son un mecanismo en DNN que le permite especificar si un módulo debe mostrarse u ocultarse. Cuando DNN muestra una página, para cada módulo de la página, pregunta a todos los Filtros de inyección si debería agregar el módulo o no. Si hay algún filtro de inyección de módulo que excluya el módulo, entonces dicho módulo no se incluirá en la página. Este es un punto de extensión de nivel bastante bajo que se puede usar para habilitar algunos escenarios que de otra manera serían difíciles de lograr.

## Cuando no usar

DNN [`StandardModuleInjectionFilter`](xref:DotNetNuke.UI.Modules.StandardModuleInjectionFilter) tse ocupa de ocultar los módulos que se eliminan, caducan o excluyen mediante permisos. La mayoría de las veces querrá usar uno de estos mecanismos, en lugar de implementar un Filtro de inyección de módulos personalizado. Por ejemplo, si está intentando mostrar u ocultar dinámicamente el contenido en una página en función de los permisos asignado a un usuario, debería usar la configuración de permisos del módulo en su lugar. Si solo desea _mostrar/ocultar_ contenido dentro de un módulo personalizado, generalmente es más apropiado colocar esa lógica dentro del módulo.

## Cuando usar

Hay una serie de escenarios que no son fáciles de manejar por ningún mecanismo existente de los que proporciona DNN. Si los criterios para ocultar/mostrar un módulo no pueden vincularse a los permisos (por ejemplo, geolocalización, valores de cookies, reglas de fecha/horas complejas, fecha de la última visita, etc.), un filtro de inyección de módulos personalizado puede ser una buena forma de implementar. Imaginemos un caso de uso como una prueba A/B <testing>, como la razón inicial para el desarrollo de dicha función. Otra razón para elegir un Filtro de inyección de módulo personalizado podría ser la necesidad de aplicar una regla uniforme para ocultar/mostrar una variedad de tipos de módulos, o módulos que su equipo no haya desarrollado (ya sea que los está integrado o sean propiedad de terceros).

Un método que puede utilizar cuando oculta módulos de forma arbitraria es aprovechar la configuración de etiquetas del módulo para indicar a los módulos que deberían estar ocultos en un determinado escenario. Por ejemplo, puede [crear dos términos](xref:add-term-to-vocabulary), _Ocultar A_ y _Ocultar B_ para excluir contenido basado en un valor de cookie en una prueba A/B. Luego, cuando esos términos se aplican como una etiqueta a un módulo, puede utilizar un Filtro de inyección de módulo personalizado para mostrar u ocultar el contenido de forma adecuada. Consulte [GitHub Injection Filter Samples](https://github.com/dnnsoftware/Dnn.InjectionFilter.Sample) para ver un punto de partida para un filtro basado en etiquetas.

## ¿Cómo agregar un filtro de inyección de módulo?

DNN simplemente incluye cualquier clase que implemente [`StandardModuleInjectionFilter`](xref:DotNetNuke.UI.Modules.IModuleInjectionFilter) en la colección de filtros para consultar si se deben mostrar. Para implementar la interfaz, una clase solo necesita implementar el método, `CanInjectModule`, que toma como entradas una instancia de `ModuleInfo` y `PortalSettings`, y devuelve Verdadero o Falso para determinar si el módulo se debe agregar o no.

```csharp
    using DotNetNuke.Collections;
    using DotNetNuke.Entities.Modules;
    using DotNetNuke.Entities.Portals;
    using DotNetNuke.UI.Modules;

    public class ExampleModuleInjectionFilter : IModuleInjectionFilter
    {
        public bool CanInjectModule(ModuleInfo module, PortalSettings portalSettings)
        {
            var hide = module.ModuleSettings.GetValueOrDefault("HideOnTuesday", false);
            return hide && DateTime.Today.DayOfWeek == DayOfWeek.Tuesday;
        }
    }
```

## ¿Cómo implementar un filtro de inyección de módulo?

Si está implementando un código personalizado (por ejemplo, un módulo personalizado), puede incluir la clase que implementa su Módulo de filtro de inyección en el ensamblado que contiene su código. Si no tiene otro código personalizado o no desea combinar el Filtro de inyección de módulos con el código existente, puede compilar la clase en su propio ensamblado y empaquetarlo por separado.  En el [archivo de manifiesto](xref:dnn-manifest-schema), escoga `Library` para el tipo de paquete, y use el componente `Assembly` para instalar el ensamblado en la carpeta `bin`.

```xml
<dotnetnuke type="Package" version="5.0">
    <packages>
        <package name="YourCompany.ExampleModuleInjectionFilter" type="Library" version="1.0.0">
            <friendlyName>Example Module Injection Filter</friendlyName>
            <description>Hides modules on Tuesdays based on a module setting.</description>
            <owner>
                <name>Your Name</name>
                <organization>YourCompany</organization>
                <url>www.example.com</url>
                <email>support@example.com</email>
            </owner>
            <license src="License.txt" />
            <releaseNotes src="ReleaseNotes.txt" />
            <azureCompatible>true</azureCompatible>
            <components>
                <component type="Assembly">
                    <assemblies>
                        <assembly>
                            <path>bin</path>
                            <name>YourCompany.ExampleModuleInjectionFilter.dll</name>
                            <version>1.0.0</version>
                        </assembly>
                    </assemblies>
                </component>
            </components>
        </package>
    </packages>
</dotnetnuke>
```
