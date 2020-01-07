---
uid: add-regex-pattern-for-duplicate-pages
locale: es
title: Agregar un patrón de expresiones regulares para páginas duplicadas
dnnversion: 09.02.00
related-topics: edit-regex-pattern-for-duplicate-pages,delete-regex-pattern-for-duplicate-pages
---

# Agregar un patrón de expresiones regulares para páginas duplicadas

Puede optimizar el índice de búsqueda marcando las páginas generadas como duplicadas si difieren solo en contenido dinámico. El rastreador indexa solo uno de cada conjunto de páginas que coinciden con un patrón de expresiones regulares especificado.

## Prerrequisitos

*   Una **cuenta de administrador para el sitio**. Los administradores tienen permisos completos para el sitio específico.

## Pasos

1.  Vaya a Persona Bar \> Configuración \> Configuración del sitio.
    
    ![Vaya a Persona Bar > Configuración > Configuración del sitio.](/images/scr-pbar-host-Settings-E91.png)
    
2.  Vaya a la pestaña *Búsqueda* y luego a la subficha **Rastreo**.
    
    ![Búsqueda > Rastreo](/images/scr-pbtabs-all-Settings-SiteSettings-Search-Crawling-E90.png)
    
3.  En **Duplicados**, haga clic en **Agregar patrón de expresiones regulares**.
              
    ![](/images/scr-SiteSettings-Search-Crawling-duplicates-add-regex-pattern-button-E90.png)
    
          
4.  Defina el patrón de expresiones regulares para las páginas duplicadas.         
    
    ![](/images/scr-SiteSettings-Search-Crawling-duplicates-add-regex-pattern-E90.png)
          
    
    |**Campo**|**Descripción**|
    |---|---|
    |<strong>Descripción</strong>Un nombre para la entrada del patrón de expresión regular. Por lo general, el nombre del módulo que genera el contenido dinámico en páginas que coinciden con el patrón especificado.|
    |<strong>Patrón de expresiones regulares</strong>|La expresión regular que describe las diversas URL y parámetros de URL de las páginas que se consideran duplicadas.|
    
5.  Guardar.
