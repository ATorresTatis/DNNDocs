---
uid: configure-messaging
locale: es
title: Configurar la mensajería para su sitio
dnnversion: 09.02.00
related-topics: update-site-info,assign-key-pages,add-metadata-to-pages,access-web-config,configure-check-for-new-version,participate-in-improvement-program,configure-html-editor,administrators-extensions-overview,administrators-connectors-overview,administrators-search-overview,administrators-vocabularies-overview
---

# Configurar la mensajería para su sitio

## Prerrequisitos

*   Una **cuenta de administrador para el sitio**. Los administradores tienen permisos completos para el sitio específico

## Pasos

1.  Vaya a **Persona Bar \> Configuración \> Configuración del sitio**.
    
    ![Persona Bar > Configuración > Configuración del sitio](/images/scr-pbar-host-Settings-E91-platform.png)
    
2.  Vaya a la pestaña **Comportamiento del sitio** y luego a la subpestaña **Mensajería**.
    
    ![Comportamiento del sitio > Mensajería](/images/scr-pbtabs-host-Settings-SiteSettings-SiteBehavior-Messaging-E90.png)
    
3.  Establezca los campos que afectan la mensajería de usuarios y los mensajes del sistema para los usuarios.          
    
    ![Configuración del sitio > Comportamiento del sitio > Mensajería](/images/scr-SiteSettings-SiteBehavior-Messaging-E90.png)
              
    > [!Nota] Los administradores y hosts/superusuarios no están restringidos por esta configuración.
    
    <ul><li>Mensajes de usuario</li></ul>

    |**Campo**|**Descripción**|
    |---|---|
    |<strong>Deshabilitar mensajes privados</strong>|Cuando está habilitado, los usuarios no podrán enviar mensajes directamente a otros usuarios o grupos.|
    |<strong>Intervalo de entrega en minutos</strong>|El número mínimo de minutos para esperar antes de permitir que el mismo usuario envíe otro mensaje. Cuando es 0, los usuarios pueden enviar otro mensaje inmediatamente después del primero|
    |<strong>Límites de destinatario</strong>|El número máximo de destinatarios permitido en un mensaje. Un rol se considera un destinatario.|       
    |<strong>Permitir archivos adjuntos</strong>|Cuando está habilitado, los usuarios pueden adjuntar archivos a sus mensajes a otros usuarios o grupos.|
    
    <ul><li>Mensajes del sistema</li></ul>
        
    |**Campo**|**Descripción**|
    |---|---|
    |<strong>Enviar correos electrónicos</strong>|Cuando está habilitado, el sistema envía un correo electrónico al usuario para cada mensaje y notificación.|
    |<strong>Incluir archivos adjuntos</strong>|Cuando está habilitado, los correos electrónicos del sistema pueden incluir archivos adjuntos.|
    
