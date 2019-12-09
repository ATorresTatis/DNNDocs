---
uid: access-web-config
locale: es
title: Modificar los archivos web.config y otros archivos .config
dnnversion: 09.02.00
related-topics: update-site-info,assign-key-pages,add-metadata-to-pages,configure-messaging,configure-check-for-new-version,participate-in-improvement-program,configure-html-editor,administrators-extensions-overview,administrators-connectors-overview,administrators-search-overview,administrators-vocabularies-overview
---

# Modificar los archivos web.config y otros archivos .config

## Pasos

1.  Vaya a **Persona Bar \> Configuración \> Administrador de configuración**.
    
    ![Persona Bar > Configuración > Administrador de configuración](/images/scr-pbar-host-Settings-E91-platform.png)
    
2.  Vaya a la pestaña **Archivos de configuración**.
    
    ![Archivos de configuración](/images/scr-pbtabs-host-Settings-ConfigManager-ConfigFiles-E90.png)
    
3.  Elija el archivo de configuración de la lista desplegable.
    
    ![lista desplegable de archivos de cofiguración > web.config](/images/scr-ConfigMgr-ConfigFiles-webconfig-E91.png)
    
> [!IMPORTANTE] Cuando modifica el archivo web.config, específicamente, debe saber que podría tener un impacto negativo en el rendimiento de su sitio web. El archivo guardado activará el reinicio del sitio web, lo que borrará toda la caché. Esto podría hacer que el sitio web parezca cargar lentamente e incluso arrojar errores temporalmente en algunos casos. Se sugiere actualizar el archivo web.config solamente durante las horas no pico en sitios web de misión crítica
