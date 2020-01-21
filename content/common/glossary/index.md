---
uid: glossary
locale: es
title: Glossary
dnnversion: 09.02.00
links: ["[DNN Wiki: DNN Glossary](https://www.dnnsoftware.com/wiki/dotnetnuke-glossary)","[DNN Wiki: Globalization Glossary](https://www.dnnsoftware.com/wiki/international-glossary)"]
---

# Glosario

**menú de acción (action menú)**

El conjunto de menús que proporciona acceso a la funcionalidad de un módulo. Disponible solo si la página está en modo Edición. Los menús pueden incluir el menú de edición (icono de lápiz), el menú de Administración (icono de engranaje) y el menú para mover (icono de cuatro flechas). La plataforma DNN proporciona acciones que son comunes a todos los módulos; sin embargo, un módulo puede agregar acciones adicionales. Si la instancia del módulo es independiente, las acciones realizadas a través del menú de acción del módulo afectan solo a esa instancia de módulo específica en esa página web específica. Si se hace referencia a la misma instancia de módulo en varias páginas, los cambios realizados en la instancia de módulo desde cualquiera de esas páginas se reflejan en todas esas páginas..

**Administración avanzada de URL (Advanced URL Management)**

La última implementación de Friendly URL Rewriter. Incluye herramientas adicionales que brindan a los administradores de DNN un mayor control sobre el formato de las URL dentro de DNN.

**Contenedor (container)**

Un conjunto de componentes relacionados que definen la apariencia de un módulo. Por el contrario, una máscara o un tema define la apariencia de una página web o sitio web completo.

**Cultura (culture)**

El código RFC 4646 para el idioma y la región. Ejemplo: en-US para inglés (US) y fr-FR para francés (Francia).

**Propietario de la base de datos (databaseOwner)**

Un token utilizado en los scripts de la base de datos para referirse al esquema de la base de datos de SQL Server que se utiliza durante la instalación de DNN. Valor predeterminado: `dbo`.

**Compromiso (engagement)**

Una puntuación que mide qué tan involucrado está el miembro con el resto de la comunidad.

**Puntos de experiencia (Experience Points)**

Un puntaje acumulativo ilimitado de por vida basado en las actividades del usuario en el sitio.

**Extensión (extensión)**

Una combinación de temas, módulos u otros componentes que reemplazan o extienden características específicas de la Plataforma DNN.

**URL amigable (friendly URL)**

Una URL que oculta una ruta codificada. Ejemplo: https://www.example.com/myanswerpage podría resolverse en https://www.example.com/default.aspx?tabid=42 . DNN proporciona tres modos de URL amigables::

*   **Advanced** proporciona URLs amigables para los humanos y para búsquedas.
*   **HumanFriendly** usa URL simples para nombres de páginas y valores de tabid en URLs más complicadas. Soporta el redireccionamiento con algunas limitaciones.
*   **SearchFriendly** incluye patrones de  `tabid` en las URLs.

**Influencia (influence)**

Una puntuación que mide el efecto positivo o negativo del miembro en la comunidad.

**Manifiesto (manifest)**

Un archivo XML (por ejemplo, MyExtension.dnn) que especifica cómo instalar una extensión. El manifiesto contiene información sobre el tipo de extensión y los diversos componentes que conforman la extensión.

**Módulo (module)**

Una extensión DNN que proporciona contenido o alguna funcionalidad en una página. Ejemplo: un módulo podría producir contenido dinámico que se muestra en un panel en la página.

**Calificador (objectQualifier)**

Una cadena personalizada utilizada como prefijo para nombres de objetos SQL relacionados con DNN, como tablas y procedimientos almacenados. Esto le permite identificar los objetos DNN en una base de datos que admite otras aplicaciones además de DNN. Valor predeterminado: en blanco.

**Paquete (package)**

Un archivo zip que contiene todos los archivos necesarios para instalar una extensión en un sitio web basado en DNN. Además, una sección del esquema de del archivo DNN de manifestó, que especifica cómo se instalan los componentes principales de la extensión.

**Página (page)**

Un objeto DNN que incluye todos los componentes de una página web, como los scripts y los componentes de la interfaz de usuario.

**Panel (pane)**

Un área de plantilla de diseño que contiene un módulo. Los diseñadores de temas determinan los nombres y las posiciones de los paneles. Los administradores y editores de páginas web seleccionan el panel para cada módulo agregado a la página web. Cuando se ve la página web, el panel puede mostrar contenido, dependiendo de la funcionalidad del módulo.

**Portal (portal)**
Portal es un término que se utilizó originalmente en versiones anteriores de DNN y desde entonces se ha reemplazado por "sitio" o "sitio web". Esencialmente, un portal es un único sitio web en su instancia de DNN, y DNN puede tener uno o varios portales/sitios en una sola instancia de DNN. Aún verá el término `portal` y `portals` utilizados en la API y en la base de datos de DNN.

**Alias de portal (portal alias)**

Una URL que se refiere a un sitio web específico en una instalación de DNN. Ejemplos: https://www.example.com(alias del portal principal), https://www.example.com/pathname (alias de portal secundario). Cada sitio web puede tener uno o más alias de portal.

**Premium (premium)**

Una configuración de módulo que indica que el uso del módulo puede restringirse por razones de seguridad. Ejemplo: los módulos que exponen información confidencial del usuario y los módulos que administran el acceso de seguridad al sitio deben ser premium.

**Proveedor (provider)**

Un tipo de extensión de DNN que proporciona una implementación alternativa de una funcionalidad específica de la plataforma DNN. Ejemplos: proveedores de autenticación, proveedores de datos y proveedores de navegación. En la mayoría de los casos, incluso si hay varias implementaciones disponibles en una instalación de DNN, solo una implementación de cada tipo de proveedor está activa en cualquier momento.

**Puntos de reputación (Reputation Points)**

Un conjunto de puntos basado en cómo los miembros del sitio perciben la confiabilidad de un usuario.

**Sitio (site)**

Un sitio web específico en una instalación de DNN, que puede alojar múltiples sitios web que comparten archivos y recursos.

**Superusuario (superuser)**

La cuenta administrativa más privilegiada con acceso completo a todos los sitios web dentro de la instalación de DNN y a todas las aplicaciones instaladas.

**Tab (tab)**

Este es un término que puede ver usado y simplemente describe una instancia de una página/página web en DNN. "Página" y "Pestaña" son términos intercambiables desde la perspectiva del usuario final. Todavía lo verá con el nombre `tab` o `tabs` en la API de DNN y en objetos de la base de datos

**Objeto del tema (theme object)**

Un tipo de extensión DNN utilizada en temas para proporcionar funcionalidad adicional para elementos comunes de IU en una página web. Ejemplos: barra de menú, aviso de copyright, enlaces de inicio de sesión o de registro, enlaces de privacidad, enlaces de términos del servicio y cuadros de búsqueda. Los objetos temáticos son configurados por el diseñador del tema

> [!Consejo] [10 Pound Gorilla](https://www.10poundgorilla.com/) y su herramienta [DNN-Skinning-Tool](https://10poundgorilla.com/DNN-Skinning-Tool) funciona como referencia y como una herramienta que permite personalizar el código para los objetos del tema de DNN, en función de los valores de atributo que especifique.

**Tema (theme)**

Un conjunto de componentes relacionados que definen el aspecto de una página web o sitio web. Estos componentes incluyen:

*   una o más plantillas de diseño, y
*   un CSS opcional para cada una de las plantillas, o un CSS maestro opcional para todo el sitio web.

Por el contrario, un contenedor y cualquier CSS asociado definen la apariencia de un módulo en un solo panel de una página.

**Token (token)**

En una plantilla de contenido HTML, un marcador de posición para los datos que se inyectarán en la salida HTML. Ejemplo: `[User:UserName]` se reemplaza con el nombre de usuario real.

En una plantilla de diseño de HTML, una palabra que representa el código estándar DNN para un objeto del tema. Por ejemplo: \[NAV\], \[COPYRIGHT\], \[LOGIN\], \[PRIVACY\], \[TERMS\], y \[SEARCH\].

En una plantilla de visualización, una palabra que representa un campo en el tipo de contenido asociado con el visualizador. Ejemplo: si se nombra `Meeting Timeslot` el campo de tipo de contenido, el token del campo sería `{{meetingTimeslot}}`.
