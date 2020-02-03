---
uid: about-import-export
locale: es
title: Importación y exportación
dnnversion: 09.02.00
---

# Importación y exportación

Importar / Exportar en v9.1 está diseñado para sincronizar dos sitios en diferentes instalaciones en diferentes servidores, como una instalación provisional y una instalación de producción.

Importante: antes de realizar una importación, haga una copia de seguridad de su sitio y de su base de datos. Las importaciones solo se pueden deshacer restaurando desde una copia de seguridad.

## Exportación diferencial

Puede exportar todo el sitio o seleccionar qué componentes exportar. También puede optar por realizar una exportación completa o una exportación diferencial. Una exportación diferencial incluye solo los cambios desde la última exportación; por lo tanto, el proceso es más rápido y el paquete es más pequeño.

Advertencia: las exportaciones diferenciales deben gestionarse y utilizarse con cuidado.

*   Los paquetes diferenciales deben importarse en el mismo orden en que se exportaron, para que los cambios se apliquen correctamente.
*   Eliminar un paquete de exportación diferencial invalidará los paquetes de exportación diferencial que se crearon después de este.
          
    
    ![Ilustración del escenario diferencial si se elimina la exportación diferencial media](/images/gra-import-export-example.gif)
