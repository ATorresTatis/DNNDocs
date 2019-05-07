---
uid: about-evs
locale: es
title: Acerca del Servicio de Verificación de Extensión
dnnversion: 09.02.00
related-topics: test-module,dnn-manifest-schema,module-features,module-architecture,developers-creating-modules-overview
links: ["[DNN Module APIs](https://www.dnnsoftware.com/dnn-api/)","[DNN Community Blog: Extension Verification Service (EVS) by Nathan Rover](https://www.dnnsoftware.com/community-blog/cid/147439/extension-verification-service-evs)","[DNN Community Blog: Extension Verification Service (EVS) Update by Nathan Rover](https://www.dnnsoftware.com/community-blog/cid/154576/extension-verification-service-evs-update%20from%20june%202013)"]
---

# Acerca del Servicio de Verificación de Extensión

The DNN [Extension Verification Service] (EVS) performs compatibility tests in three areas.
El [Servicio de Verificación de Extensión de DNN](https://evs.dnnsoftware.com) (EVS) realiza pruebas de compatibilidad en tres áreas.

*   **Empaquedato de módulos**. EVS verifica:
* Que exista un archivo de manifiesto .dnn válido. El SVE arroja un error, si falta una sección requerida, o una advertencia, si falta una sección opcional.
* Que todos los archivos listados en el manifiesto existan en el paquete.
* Que todos los archivos incluidos en el paquete se enumeran en el manifiesto.
*   **Capa de datos**. EVS verifica:
    *   Que los objetos de la base de datos central no fueron modificados.
* Que cualquier script SQL en el módulo sea compatible con Microsoft Azure SQL Database y pueda ejecutarse sin errores. Si se encuentran scripts SQL incompatibles con Azure, EVS genera versiones compatibles con Azure de esos scripts y los pone a disposición en un archivo zip; sin embargo, debe verificar que los scripts convertidos todavía se comportan como se espera.
* Que {databaseOwner} y {objectQualifier} se usen correctamente.
* Que el script de desinstalación elimine por completo todos los objetos agregados por el script de instalación.
*   **Ensamblados**. EVS verifica:
* Que no existan errores en el ensamblado.
* Que cada referencia de cada ensamblado apunte a un ensamblado que exista en DNN o en el caché de ensamblados global (GAC) de .NET. Si no se encuentra el ensamblado, EVS devuelve un error.


![EVS website](/images/scr-EVS.png)
