---
uid: use-module-creator
locale: es
title: Utilizar el creador de módulos
dnnversion: 09.02.00
next-topic: create-module-using-templates
related-topics: module-module-creator,web-forms-module-development,spa-module-development,mvc-module-development
---

# Utilizar el creador de módulos

## Visión general

La funcionalidad DNN Module Creator permite a los desarrolladores crear módulos rápidamente sin utilizar un IDE, como Visual Studio. Automatiza muchas de las tareas iniciales de creación de módulos, para que los desarrolladores puedan centrarse en escribir su código. Además, DNN Module Creator se puede ampliar con plantillas personalizadas para optimizar aún más el desarrollo.

El uso de DNN Module Creator se recomienda generalmente solo para módulos simples. Para módulos más complejos, puede crear un módulo de formularios web utilizando plantillas.

## Pre-requisitos

*   [Una instalación de DNN local con permisos de host](xref:set-up-dnn).

## Pasos

1.  Crear, copiar o editar una página.
    *   [Crear una pagina](xref:obsolete)
    *   [Copiar una página](xref:obsolete)
    *   [Editar una página](xref:obsolete)

2.  Dentro de un panel, haga clic en el icono del módulo.
          
    ![Panel con iconos de contenido](/images/scr-pane-with-content-icons-module.png)
             
3.  Busque el Creador de Módulos entre los módulos instalados.         
    
    ![Búsqueda del creador de módulos](/images/scr-menuModulesList04ModuleCreator.png)         
    
4.  Arrastre el creador de módulos a cualquier panel de la página web.          
    
    ![Arrastrar a un panel](/images/scr-menuModulesModuleCreatorDrag.png)
             
5.  Rellene el formulario de creación de módulos.         
    
    ![Formulario de creación de módulos](/images/scr-ModuleCreatorForm.png)
          
    |**Campo**|**Descripción**|
    |---|---|
    |**Nombre del propietario**|Nombre de su organización. Debe contener únicamente caracteres alfanuméricos. Se utiliza para crear una carpeta para distinguir sus módulos de aquellos creados por otros creadores de módulos. También se utiliza como el espacio de nombres para su código.|
    |**Nombre del módulo**|Debe contener únicamente caracteres alfanuméricos. Se utiliza para crear el nombre descriptivo y el nombre completo del módulo. El nombre completo es \[OwnerName\].\[ModuleName\]|
    |**Idioma**|El idioma seleccionado (C#, VB o Web) determina qué plantillas estarán disponibles.|  
    |**Plantilla**|Para **C#** y **VB**, elija:<ul><li>**Script en línea**. El código está embebido. También utiliza controles de usuario.</li><li>**Razor**. Utiliza scripts de Razor para renderizar las vistas.</li><li>**Control de usuario**. El código se almacena en archivos separados. Es el formto más utilizado.</li></ul>Para **Web**, la plantilla **HTML** permite utilizar HTML, CSS y JavaScript.|
    |**Nombre del Control**|Nombre del control de módulo primario que está registrado con DNN.|
    
    El nuevo módulo reemplazará el formulario del creador del módulo en el panel.
     
    ![Módulo creado](/images/scr-ModuleCreatorModuleCreated.png)
              
6.  Personalizar el módulo.
    1.  Desde el icono con forma de engranaje, seleccione **Desarrollar**.                 
        
        ![Ajustes (icono de engranaje) \> Desarrollar](/images/scr-ModuleGearMenuDevelop.png)                  
        
    2.  En el archivo `View.ascx`, elimine todas las líneas de código, excepto la primera.                
        
        ![En View.ascx, borre todo excepto la primera línea](/images/scr-ModuleViewAscx.png)
                          
    3.  Añada el código de marcado necesario para personalizar el módulo. Luego haga clic en **Actualizar** para guardar los cambios.
                         
        ![Personalizar el módulo](/images/scr-ModuleCustomize.png)
                          
        Ejemplo:
        
        ```
         
            <h1>Hello, <%: UserInfo.DisplayName %></h1>
                                    
        ```
        
    4. Desde el menú desplegable **Seleccionar archivo** , elija el archivo `View.ascx.cs`.
                          
        ![Seleccione View.ascx.cs.](/images/scr-ModuleViewAscxCs.png)                  
        
    5.  Elimine todo el código en la región **Controladores de eventos** y haga clic en **Actualizar** para guardar los cambios.
                          
        ![Quitar los controladores de eventos](/images/scr-ModuleDeleteEventHandlers.png)
