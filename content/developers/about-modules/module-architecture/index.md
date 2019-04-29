---
uid: module-architecture
locale: es
title: Module Architecture
dnnversion: 09.02.00
related-topics: dnn-manifest-schema,module-features,developers-creating-modules-overview,about-evs
links: ["[DNN Module APIs](https://www.dnnsoftware.com/dnn-api/)"]
---

# Arquitectura de módulos

Aunque cada módulo proporciona un conjunto diferente de características y funcionalidades, algunos elementos arquitectónicos son comunes entre los módulos. La mayoría de los módulos para DNN se desarrollan utilizando una arquitectura de n niveles. Ya sea que construya un módulo de formularios web, un módulo MVC o un módulo SPA, implementará la mayoría de estas capas en su módulo.


![Arquitectura de módulos](/images/gra-module-architecture.png)


## Capa de acceso a datos

DNN es compatible con tres marcos de datos de capa de acceso (DAL): DAL, DAL+ y DAL2. Los tres se basan en el mismo modelo de proveedor subyacente, que permite el uso de DNN con diferentes sistemas de administración de bases de datos.

Nota: DNN viene con un proveedor de base de datos de SQL Server. Otros proveedores de bases de datos de terceros están disponibles para Oracle, MySQL y MS Access; sin embargo, los proveedores de MySQL y MS Access ya no se mantienen ni son compatibles.

DAL es una implementación completamente abstracta que requiere lo siguiente:

*   Una clase de proveedor de datos abstractos que define su API de capa de datos.
*   Una implementación concreta de esta clase abstracta para cada tipo de base de datos que desee admitir (normalmente SQL Server).
*   Scripts de base de datos para crear los procedimientos almacenados, tablas y vistas requeridas por su módulo.

DAL+ agrega métodos de acceso a datos genéricos a la plataforma central para eliminar la necesidad de las clases de proveedores de datos abstractos y concretos. Puede seguir utilizando bases de datos alternativaspero debe proporcionar los scripts de base de datos necesarios.

DAL2 utiliza el Micro-ORM de nombre PetaPOCO, que elimina la necesidad de escribir procedimientos almacenados. DAL2 proporciona funciones adicionales, incluida la gestión de caché integrada, que simplifica aún más su código.

Puede usar cualquier método de acceso a datos, incluso aquellos que no están directamente soportados por DNN. También puede utilizar más de una tecnología DAL dentro de un solo módulo.

Consejo: Utilice DAL2 para la mayoría de sus consultas CRUD estándar, y use DAL+ para consultas más complejas que pueden requerir ajustes de rendimiento. Este enfoque simplifica el desarrollo y le permite enfocar sus esfuerzos.

## Capa de almacenamiento en caché

El acceso a la base de datos es una de las acciones más lentas que realiza una aplicación web. En muchos sistemas, los datos se almacenan en un formato que es diferente del formato en el que se utilizarán. Las aplicaciones a menudo realizan consultas complejas para filtrar el conjunto de datos y luego alterar el formato de los resultados antes de su uso. Si la base de datos no es local, la consulta llevará más tiempo, dependiendo de la velocidad de la red. Las consultas de la base de datos son más lentas que usar una caché en memoria.

El almacenamiento en caché es ideal para:

*   Cualquier dato que sea costoso de computar y produzca los mismos resultados durante un período de tiempo.
*   Cualquier segmento de datos que sea invariable para un subconjunto de usuarios o para una URL específica.

DNN proporciona almacenamiento en caché integrado con la API de caché.  Si utiliza las API DAL o DAL+ de DNN, implemente el patrón de almacenamiento en caché para obtener un mejor rendimiento [Cache-Aside Pattern](https://docs.microsoft.com/en-us/azure/architecture/patterns/cache-aside). Puede configurar el almacenamiento en caché incorporado de DAL2 utilizando atributos en su código.

La API de caché se puede ampliar para utilizar diferentes almacenes de caché. La abstracción proporcionada por la API de caché garantiza que los módulos funcionen sin problemas, independientemente del proveedor de almacenamiento en caché instalado por el administrador del sitio.

> [! Sugerencia] Marque las clases con el atributo [Serializable] para asegurarse de que esté almacenada correctamente por los proveedores de almacenamiento en caché fuera de proceso.

```

    [Serializable]
    public class MyInfoClass
    {
        // Property declarations...
    }

```

## Capa de logica de negocios

La mayoría de las reglas de negocios se implementan en la capa de lógica de negocios. Estas reglas pueden ser tan simples como validar datos o tan complejas como organizar flujos de trabajo a través de múltiples sistemas de back-end. Esta capa también es responsable de coordinar las llamadas a las capas de almacenamiento en caché y acceso a datos.

DNN proporciona APIs para manejar tareas comunes, como la seguridad de la aplicación, el almacenamiento de archivos, la administración de listas, el registro de eventos y la búsqueda de texto. Estas APIs son totalmente abstractas y extensibles, por lo que puede centrarse solo en las reglas de negocios que son específicas de su módulo.

## Capa de servicios

DNN proporciona un marco de servicios, que puede utilizar para definir rápidamente servicios web. El Marco de servicios proporciona acceso integrado a las entidades comunes de DNN dentro de sus métodos de servicio, de modo que el servicio pueda determinar a qué sitio se está llamando, el usuario que realiza la solicitud y el módulo encargado de procesas la solicitud. También puede proteger sus servicios web especificando qué aplicaciones y qué usuarios pueden acceder a sus puntos finales (endpoints) en el servicio.

## Capa de presentación

El componente central en la capa de presentación son los controles del módulo. Cada vista única de un módulo se registra como un control de módulo en el archivo manifiesto  de DNN. [DNN Manifest](xref:dnn-manifest-schema).

Las API de DNN facilitan el acceso a cualquier control del módulo, simplificando así la administración de la vista dentro de su módulo.

Alternativamente, los módulos pueden implementar sus propios métodos de envío de vistas para controlar cuándo se muestran vistas específicas o cómo aparece el módulo en la página.

Para los módulos de formularios web (webForms), el componente de vista principal es un control de usuario ASP.NET, denominado control de módulo en DNN. Para los módulos MVC y SPA, DNN expandió la definición de los controles del módulo para acomodar su representación de vista alternativa.
