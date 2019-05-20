---
uid: developers-extensions-overview
locale: es
title: Creación de un módulo 
dnnversion: 09.02.00
related-topics: dnn-manifest-schema,module-features,module-architecture,about-evs
links: ["[DNN Module APIs](https://www.dnnsoftware.com/dnn-api/)","[DNN 8 API Reference](https://www.dnnsoftware.com/dnn-api/)","[DNN Wiki: Module Development](https://www.dnnsoftware.com/wiki/module-development/)","[DNN Community Blog: Module Development series by Clinton Patterson](https://www.dnnsoftware.com/community-blog/cid/155064/module-development-for-non-developers-skinners-dnn-beginners--blog-series-intro/)","[Using the new Module Development Templates for DotNetNuke 7 by Chris Hammond](https://www.chrishammond.com/blog/itemid/2616/using-the-new-module-development-templates-for-dot/)"]
---

#¿Debería crear una extensión?

Antes de crear una extensión, vale la pena verificar primero si ya existe la extensión que necesita. Intente buscar en alguno de estos recursos para ver si la extensión que desea crear ya existe.

* [Tienda DNN](https://store.dnnsoftware.com/)
* [Buscar en GitHub](https://github.com/search?q=dnn)
* [Usar nvQuickPulse para encontrar una extensión](https://github.com/nvisionative/nvQuickPulse/blob/master/README.md)
* [Buscar a través del directorio DNN-Connect](https://www.dnn-connect.org/community/community-extensions)

# Tipos de Extensiones

A menudo, los desarrolladores crearán una extensión de _módulo_ para resolver un problema. Por supuesto, también puede usar su módulo para mejorar o proporcionar una interfaz de configuración para otras extensiones.

Por ejemplo, si tiene un código para ejecutar un informe personalizado de forma regular, normalmente programará una tarea para generar la información. Sin embargo, dado que el programador de tareas solo está disponible para la cuenta de _Superusuario_ (conocida como la cuenta Host), si desea permitir que otros usuarios ejecuten de forma ad hoc el reporte o que modifiquen la programación, puede crear un módulo que tenga una interfaz para exponer algunas de esas configuraciones. Luego, puede proporcionar acceso a ese módulo para usuarios y/o roles de seguridad mediante el mecanismo de permisos del módulo de DNN.

- **Biblioteca de JavaScript (JavaScript Library)**: le permite instalar un marco de JavaScript (por ejemplo, Angular o React) de una manera que permite que múltiples extensiones soliciten e incluyan el marco de forma segura sin cargarlo varias veces. También permite a los super-usuarios (host) definir globalmente desde dónde y cómo se carga la biblioteca.
- **Biblioteca (Library)**: un archivo conocido como DLL se empaqueta e instala para que esté disponible para cualquier número de propósitos. Algunas extensiones pueden usarlo como una API compartida y/o puede ser uno de los otros tipos de extensiones que se enumeran a continuación. Por ejemplo, un proveedor de URL se distribuye como una extensión de biblioteca.
- **Módulo (Module)**: este es el tipo de extensión que más se utiliza. Los administradores y/o los visitantes del sitio web pueden ver un módulo una vez que se instala y se agrega a una página, siempre que el usuario tenga los permisos necesarios. Podría ser un paquete de módulos e incluso puede incluir otros tipos de extensiones.
- **Proveedor (Provider)**: en general, un proveedor es un patrón de desarrollo donde la funcionalidad se proporciona fuera de la caja, pero la funcionalidad puede cambiarse o reemplazarse por la instalación y la especificación de un proveedor alternativo.
  - **Autenticación (Authentication)**: esta es la única forma en que puede reemplazar de manera segura el sistema de autenticación en DNN. La simple creación de un módulo no tendrá en cuenta todos los escenarios de inicio de sesión/registro, sino que también potencialmente abrirá un agujero de seguridad en su sitio web.
  - **Datos (Data)**: si no desea que DNN se conecte y utilice SQL Server, puede crear un proveedor de datos para conectarse a otro tipo de base de datos. En el pasado, los ejemplos de esto han incluido las bases de datos de MS Access y Oracle.
  - **Carpeta (Folder)**: Le permite especificar otros tipos de carpetas y/o ubicaciones para que almacenen archivos. En el front-end, nada cambia, pero cuando alguien accede o guarda una nueva carpeta, en realidad estará "apuntando" a otro lugar detrás de la escena (por ejemplo, Dropbox, compartir archivos en Azure, etc.).
  - **Registro (Logging)**: De forma predeterminada, DNN registra el acceso al el sistema de archivos y la base de datos configurada, pero es posible modificar este registro para almacenar los eventos en otra ubicación utilizando este punto de extensión.
  - **Membresía (Membership)**: DNN incluye su propio proveedor de membresía que es un contenedor del proveedor de AspNetMembership. Utilice este punto de extensión para utilizar otro proveedor. Por ejemplo, esto sería ideal para un entorno en una granja de servidores web que requiere tolerancia cero para la pérdida de datos, al almacenar de forma centralizada las cuentas de usuario en una ubicación específica fuera de DNN.
  - **Navegación (Navigation)**: hay un proveedor de navegación muy poderoso que ya está incluido en DNN, conocido como el menú DDR, pero si desea usar una alternativa, esta es la forma principal de hacerlo.
  - **Caché de salida (Output Cache)**: este proveedor le permite determinar cómo guardar e invalidar la cache. Si bien esto es lo más relevante y será mayor el impacto en escenarios de granjas de servidores web, se usa en todos los tipos de implementación de sitios web, incluidos los escenarios en la nube, como el almacenamiento en caché de Redis.
  - **Permisos (Permissions)**: Este proveedor le permite anular el modo en que funcionan las cuadrículas de permisos en DNN. Por ejemplo, así es como Evoq agrega la función de permisos más granulares.
  - **Perfil (Profile)**: Similar al de Membresía, este proveedor anula dónde y cómo se almacena la información del perfil de usuario. Para implementaciones de sitios web altamente sensibles, es posible que desee considerar el uso de ambos proveedores para almacenar y acceder a los datos del usuario en una ubicación separada.
  - **Roles (Roles)**: el proveedor de roles es similar a los proveedores de membresía y de perfil, solo que este pertenece a la información relacionada con los roles de seguridad.
  - **Tareas (Scheduling)**: hay una función de tareas programadas en DNN que regularmente ejecuta lógica/rutinas basadas en códigos en intervalos de tiempo definidos por trabajos programados individuales. Este proveedor controla cómo funciona esa característica. Un ejemplo de anulación de esta función puede ser ejecutar un programa en Windows, en lugar de hacerlo en el grupo de aplicaciones del sitio web de IIS.
  - **Almacén de datos de búsqueda (Search Data Store)**: este proveedor le permite controlar dónde se almacenan los datos del índice de búsqueda.
  - **Índice de búsqueda (Search Index)**: puede haber muchos proveedores de índice de búsqueda, lo que le permite indexar el sistema de archivos, el contenido/las páginas estáticas y varios tipos de datos juntos o individualmente. Este proveedor lo hace posible.
  - **Mapa del sitio (Sitemap)**: un mapa del sitio XML se genera automáticamente utilizando este proveedor. El proveedor predeterminado generalmente funciona bastante bien para casi cualquier sitio web, sin necesidad de cambiarlo. Donde realmente brilla este proveedor es cuando tiene un módulo que genera una gran cantidad de páginas adicionales (por ejemplo, un blog o artículos de noticias) que deben incluirse correctamente en los rastreadores de búsqueda como Google y Bing.
  - **Editor de texto (HTML) (Text (HTML) Editor)**: si desea tener editores de texto adicionales o alternativos para que los contribuyentes de contenido utilicen o incluso muestren solo en sus propios módulos, utilice este proveedor para hacerlo.
  - **URL**: este es un proveedor muy utilizado para hacer que las URL de su sitio web en DNN sean más fáciles de usar y de buscar. Este es el proveedor que usaría para hacer cosas como eliminar el número de ID de una URL en un módulo que enumera el contenido que ha generado páginas de forma dinámica (por ejemplo, un blog o artículos de noticias).

- **Trabajos programados (Scheduled Job)**: use una extensión de trabajo programado para conectar y ejecutar lógica basada en código en un intervalo de tiempo regular. Instalar esta extensión y especificarla en el programador permite que el código se ejecute en los intervalos o eventos que elija. En las granjas de servidores web, puede (y debería) incluso elegir en qué servidor se ejecutará el trabajo programado. Por ejemplo, así es como se ejecuta el índice de búsqueda.
- **Temas (Theme)**: anteriormente conocido como "máscaras", este punto de extensión es el que le permite instalar y poner a disposición los elementos visuales que hacen que las páginas individuales o todo el sitio web se vean de una manera específica. Proporciona las dependencias y los archivos necesarios para permitir a los administradores establecer un diseño global predeterminado para todo el sitio web, así como asignar/anular esa configuración en páginas específicas. Un paquete de temas a menudo contendrá uno o ambos tipos de extensión a continuación.
- **Contenedor (Container)**: mientras que un archivo de tema hace que una página web tenga una apariencia específica, un contenedor hará que un módulo se vea de una manera específica. Cada módulo en una página específica podría tener su propia apariencia (aunque no se recomienda en la mayoría de los casos).
- **Objeto de máscara (tema) (Skin (Theme) Object)**: un objeto de máscara tiene muchos de los mismos atributos y habilidades que un módulo, pero los administradores no pueden configurarlo de ninguna manera. Siempre se presentará dentro del tema, y generalmente solo se puede configurar editando el código del tema en sí. Los ejemplos de un objeto de máscara incluyen enlaces estáticos (por ejemplo, inicio de sesión, registro, declaración de privacidad, términos de uso), búsqueda, logotipo y rutas de navegación.

# Creando un módulo  

You can produce a module in different ways:

*   Create an entire module from scratch. For very simple modules, you can use the DNN Module Creator.
*   Start with module development templates, such as:
    *   [DNN 8 Templates](https://github.com/dnnsoftware/DNN.Templates/releases/)
    *   [Chris Hammond's DotNetNuke Module and Theme Development Templates](https://github.com/ChrisHammond/DNNTemplates/) ([Installation instructions](https://www.chrishammond.com/blog/itemid/2616/using-the-new-module-development-templates-for-dot/))
    *   [Matt Rutledge's generator-dnn](https://github.com/mtrutledge/generator-dnn)
    *   [Upendo Ventures' generator-upendodnn](https://github.com/UpendoVentures/generator-upendodnn)
*   Customize a pre-existing module.

    Thousands of third-party modules and themes are available from the [DNN Store](https://store.dnnsoftware.com). There are extensions for sale, including versions that include the source code, as well as some free extension.



You can also use different programming frameworks (Web Forms, MVC, SPA) and languages (C#, VB) to create your module.
