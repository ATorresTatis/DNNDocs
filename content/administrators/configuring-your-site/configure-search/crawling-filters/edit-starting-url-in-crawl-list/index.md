---
uid: edit-starting-url-in-crawl-list
locale: es
title: Editar una URL de inicio en la lista de rastreo
dnnversion: 09.02.00
related-topics: add-starting-url-to-crawl-list,delete-starting-url-from-crawl-list,add-directory-to-included-list,delete-directory-from-included-list,add-directory-to-excluded-list,delete-directory-from-excluded-list,add-file-extension-to-included-or-excluded-list,delete-file-extension-from-included-or-excluded-list
---

# Editar una URL de inicio en la lista de rastreo

## Prerrequisitos

*   Una **cuenta de administrador para el sitio**. Los administradores tienen permisos completos para el sitio específico.

## Pasos

1.  Vaya a **Persona Bar \> Configuración \> Configuración del sitio**.
    
    ![Persona Bar > Configuración > Configuración del sitio](/images/scr-pbar-host-Settings-E91.png)
    
2.  Vaya a la pestaña **Búsqueda** y luego a la subficha **Rastreo**.
    
    ![Búsqueda > Rastreo](/images/scr-pbtabs-all-Settings-SiteSettings-Search-Crawling-E90.png)
    
3.  En **Rutas de URL**, busque la URL para editar y haga clic en el ícono de lápiz.          
    
    ![](/images/scr-SiteSettings-Search-Crawling-url-paths-edit-E90.png)
             
4.  Configure la URL para rastrear.
             
    ![](/images/scr-SiteSettings-Search-Crawling-url-paths-edit-url-E90.png)
          
    
    |**Campo**|**Descripción**|
    |---|---|
    |<strong>URL</strong>|La URL donde debe comenzar el rastreo.|
    |<strong>URL del mapa del sitio</strong>|La URL del mapa del sitio a utilizar, si corresponde.|
    |<strong>Suplantación de roles de DNN</strong>|El rol asignado al rastreador para obtener acceso a esta ruta URL. Nota: El rol debe tener al menos un usuario asignado.|
    |<strong>Habilitar Rastreo</strong>|Si está habilitado, la URL especificada se marca para ser incluida en el siguiente rastreo. Si está deshabilitado, la <strong>URL</strong> especificada no se incluye en el siguiente rastreo; sin embargo, cualquier índice existente para esta URL todavía se usa para la búsqueda.|
    |<strong>Autenticación de Windows</strong>|Si está habilitado, el rastreador usa las credenciales especificadas para obtener acceso al sitio<ul><li><strong>Dominio de Windows</strong><li><strong>Cuenta de usuario de Windows</strong></li><li><strong>Contraseña de usuario de Windows</strong></li></ul><br />Si la cuenta de usuario y la contraseña están en blanco, se utilizan las credenciales predeterminadas de Windows del servidor local.<br />Nota: habilite esta opción si el sitio utiliza la <strong>autenticación integrada de Windows</strong>.|
    
5.  Guardar.
