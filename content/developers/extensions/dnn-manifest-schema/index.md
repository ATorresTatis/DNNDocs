---
uid: dnn-manifest-schema
locale: es
title: El archivo manifiesto de DNN
dnnversion: 09.02.00
related-topics: module-features,module-architecture,developers-creating-modules-overview,about-evs
links: ["[DNN Module APIs](https://www.dnnsoftware.com/dnn-api/)","[Top 5 DotNetNuke Manifest file Module Packaging Tips by Bruce Chapman](https://web.archive.org/web/20160610221847/http://www.ifinity.com.au/Blog/EntryId/89/Top-5-DotNetNuke-Manifest-file-Module-Packaging-Tips)","[DNN Community blog: DAL 2 — A New DotNetNuke Data Layer for a New Decade by Charles Nurse](https://www.dnnsoftware.com/community-blog/cid/142201/dal-2-a-new-dotnetnuke-data-layer-for-a-new-decade)","[DNN Wiki: Manifests](https://www.dnnsoftware.com/wiki/manifests)","[DNN Community blog: The New Extension Installer Manifest — Part 1, Introduction by Charles Nurse](https://www.dnnsoftware.com/community-blog/cid/135060/the-new-extension-installer-manifest-part-1-introduction)"]
---

# Esquema del archivo de manifiesto de DNN

El archivo de manifiesto de DNN es un archivo XML (por ejemplo, MyDNNExtension.dnn) que indica cómo deben procesarse los archivos específicos en el paquete de extensión durante la instalación.

Solo se instalarán los archivos específicamente declarados en el manifiesto. Los archivos dentro de cualquier archivo zip especificado como `component type="ResourceFile"` no tienen que ser listados individualmente. Los archivos inexistentes mencionados en el manifiesto causarán un mensaje de error.

La extensión del archivo manifiesto debe ser `.dnn`. Puedes agregar la versión DNN al final; por ejemplo, `MyDNNExtension.dnn7`.

Guarde el archivo de manifiesto en la carpeta base de su paquete e inclúyalo al comprimir los archivos de su paquete.

## Esquema

```

    <dotnetnuke type="Package" version="8.0">
        <packages>
            <package name="MyCompany.SampleModule" type="Module" version="1.0.0">
                <friendlyName>My Sample Module</friendlyName>
                <description>My Sample Module is a demonstration module.</description>
                <iconFile>MyIcon.png</iconFile>
                <owner>
                    <name>MyCompany or MyName</name>
                    <organization>MyCompany Corporation</organization>
                    <url>www.example.com</url>
                    <email>support@example.com</email>
                </owner>
                <license src="MyLicense.txt" />
                <releaseNotes src="MyReleaseNotes.txt" />
                <azureCompatible>true</azureCompatible>
                <dependencies>
                    <dependency type="coreVersion">08.00.00</dependency>
                    ...
                </dependencies>
                <components>
                    <component type="Module">
                        ...
                    </component>
                    ...
                </components>
            </package>
        </packages>
    </dotnetnuke>

```

## package

```

    <package name="MyCompany.MySampleModule" type="Module" version="1.0.0">
    ...
    </package>

```

*   El nombre debe ser único. Para garantizar la singularidad de su paquete, agregue su compañía como prefijo.
*   El vaoor de tipo `type` puede ser alguno de los siguientes:
    *   Auth_System
    *   Container
    *   CoreLanguagePack
    *   [DashboardControl](https://www.dnnsoftware.com/wiki/manifest-dashboardcontrol-component)
    *   ExtensionLanguagePack
    *   JavaScript_Library
    *   Library
    *   [Module](https://www.dnnsoftware.com/wiki/modules)
    *   [Provider](https://www.dnnsoftware.com/wiki/providers)
    *   [Skin](https://www.dnnsoftware.com/wiki/dotnetnuke-skins)
    *   SkinObject
    *   otros tipos de extensiones personalizadas
*   `version` versión contiene el número de versión de su extensión.

Cada paquete representa una extensión de DNN. Puede instalar múltiples extensiones utilizando un solo manifiesto DNN creando una sección `package` para cada extensión dentro de la etiqueta `packages`.

Los paquetes se instalan en el orden en que aparecen en el manifiesto.

Solo se muestra la información sobre el _primer paquete_ durante la instalación. Esto incluye el nombre del paquete, la descripción, el propietario, la licencia y las notas de la versión.

## friendlyName y description

```

    <friendlyName>My Sample Module</friendlyName>
    <description>My Sample Module is a demonstration module.</description>

```

El nombre y la descripción amigable se muestran durante la instalación y se usan en la página Host \> Extensions, que enumera las extensiones que están instaladas o que están disponibles en su instalación. El valor de `friendlyName` puede contener espacios y hasta 250 caracteres; El valor de `description` puede contener hasta 2000 caracteres.

## iconFile

```

    <iconFile>MyIcon.png</iconFile>

```

Opcional. El icono se muestra en la lista desplegable del Panel de control de DNN y en la página de Extensiones. Se recomienda el formato .png. Si no se especifica, se utiliza el icono predeterminado de DNN.

## owner

```

    <owner>
        <name>MyCompany or MyName</name>
        <organization>MyCompany Inc.</organization>
        <url>www.example.com</url>
        <email>support@example.com</email>
    </owner>

```

Opcional, pero se recomienda. Es la información sobre el propietario o creador de la extensión.

## license and releaseNotes

```

    <license src="MyLicense.txt" />
    <releaseNotes src="MyReleaseNotes.txt" />

```

Opcional, pero se recomienda. Estos archivos de texto se muestran durante la instalación. Se solicita al usuario que acepte o rechace la licencia. Las notas de la versión se muestran durante la instalación. El texto real también se puede incrustar dentro de la etiqueta sin el atributo `src`.

## azureCompatible

```

    <azureCompatible>true</azureCompatible>

```

Opcional. El valor predeterminado es `false`. Se establece en `true` si la extensión es compatible con Microsoft Azure.

## dependencies

```

    <dependencies>
        <dependency type="coreVersion">08.00.00</dependency>
        ...
    </dependencies>

```

Las dependencias pueden ser cualquiera de estos tipos (sin distinción de mayúsculas y minúsculas):

*   **coreVersion**. Versión mínima de DNN requerida por la extensión que se está instalando. Ejemplo:

    ```

        <dependency type="coreVersion">08.00.00</dependency>

    ```

*   **managedPackage**. El nombre y la versión mínima de un paquete requerido por la extensión que se está instalando. El paquete requerido ya debe estar listado en la tabla de Paquetes principales.

    ```

        <dependency type="managedPackage" version="1.0.0">AnotherPackageRequiredByThisComponent</dependency>

    ```

*   **package**. El nombre de un paquete requerido por la extensión que se está instalando. El paquete requerido ya debe estar listado en la tabla de Paquetes principales. Ejemplo:

    ```

        <dependency type="package">AnotherPackageRequiredByThisComponent</dependency>

    ```

*   **type**. Un tipo en la biblioteca de librerias de .NET,  de DNN o en una biblioteca de terceros. Asegura que la instalación pueda crear un objeto del tipo especificado. Ejemplo

    ```

        <dependency type="type">System.Security.Principal.GenericPrincipal</dependency>

    ```

    Consejo: [Califique completamente](https://docs.microsoft.com/en-us/dotnet/framework/reflection-and-codedom/specifying-fully-qualified-type-names) un tipo si no está en la carpeta `App_Code` para evitar conflictos con tipos con nombres similares de otras fuentes.

*   Cualquier tipo de dependencia personalizado incluido en la lista de dependencias. DNN se puede ampliar creando tipos de dependencia personalizados, que se heredan de `DotNetNuke.Services.Installer.Dependencies.DependencyBase` y se deben incluir en la lista de dependencias (Host > Listas). Ejemplo:

    ```

        <dependency type="SomeCustomDependencyType">ValueNeededBySomeCustomDependencyType</dependency>

    ```

    Nota: el tipo de dependencia personalizado ya debe estar instalado antes de que se use en otra instalación.


## components

```

    <components>
        <component type="..." />
        <component type="..." />
        ...
    </components>

```

Algunos tipos de componentes son aplicables solo al tipo de paquete del mismo nombre; Los tipos de componentes genéricos se pueden utilizar con cualquier tipo de paquete.

<table>
    <th><strong>Tipo de paquete</strong></th>
    <th><strong>Tipo de componente específico</strong></th>
    <th><strong>Tipo de componente genérico</strong></th>
    <tr>
        <td>Auth_System</td>
        <td>AuthenticationSystem</td>
        <td rowspan="11"><center><br />Assembly<br />Cleanup<br />Config<br />File<br />ResourceFile<br />Script</center></td>
    </tr>
    <tr>
        <td>Container</td>
        <td>Container</td>
    </tr>
    <tr>
        <td>CoreLanguagePack</td>
        <td>CoreLanguage</td>
    </tr>
    <tr>
        <td>DashboardControl</td>
        <td>DashboardControl</td>
    </tr>
    <tr>
        <td>ExtensionLanguagePack</td>
        <td>ExtensionLanguage</td>
    </tr>
    <tr>
        <td>JavaScript_Library</td>
        <td></td>
    </tr>
    <tr>
        <td>Library</td>
        <td></td>
    </tr>
    <tr>
        <td>Module</td>
        <td>Module</td>
    </tr>
    <tr>
        <td>Provider</td>
        <td>Provider<br />URL Provider</td>
    </tr>
    <tr>
        <td>Skin</td>
        <td>Skin</td>
    </tr>
    <tr>
        <td>SkinObject</td>
        <td>SkinObject</td>
    </tr>
</table>

*   [`Assembly`](https://www.dnnsoftware.com/wiki/manifest-assembly-component). Los ensamblados se instalarán en la carpeta principal `.\bin` de la instalación. Los ensamblados son la parte del código compilado de su extensión. Pueden ser sus propios ensamblados o ensamblados de terceros que distribuyen con su extensión.

    ```

        <component type="Assembly">
            <assemblies>
                <assembly>
                    <path / <!-- Path of the assembly to install. Relative to the \bin folder of the DNN installation. -->
                    <name / <!-- Name of the assembly to install. -->
                    <version / <!-- Version of the assembly to install. -->
                </assembly>
                <assembly action="Unregister">
                    <path / <!-- Path of the assembly to remove. Relative to the \bin folder of the DNN installation. -->
                    <name / <!-- Name of the assembly to remove. -->
                    <version / <!-- Version of the assembly to remove. -->
                </assembly>
                ...
            </assemblies>
        </component>

    ```

*   [`AuthenticationSystem`](https://www.dnnsoftware.com/wiki/manifest-authenticationsystem-component). Proveedores de autenticación utilizados por la extensión, como **Facebook** , **Google** , **Twitter** o **cuentas de Microsoft** . De forma predeterminada, DNN se autentica utilizando su propia base de datos.

    ```

        <component type="AuthenticationSystem">
            <authenticationService>
                <type>Facebook</type>
                <settingsControlSrc />
                <loginControlSrc />
                <logoffControlSrc />
            </authenticationService>
            <authenticationService />
            ...
        </component>

    ```

*   [`Cleanup`](https://www.dnnsoftware.com/wiki/cleanup-component). Lista de archivos que deben eliminarse durante la instalación o actualización del paquete.

    Se pueden listar los archivos individualmente en el manifiesto.

    ```

        <component type="Cleanup" version="07.40.00">
            <files>
                <file>
                    <path>bin</path>
                    <name>MyFile.dll</name>
                </file>
                <file />
                ...
            </files>
        </component>

    ```

    También pueden enumerar los archivos con sus rutas en un archivo de texto.

    ```

        <component type="Cleanup" version="07.40.00" fileName="ListOfFilesToDelete.txt" />

    ```

    Vea también:

    *   Tipo de componente `Config` para actualizar los archivos de configuración durante la desinstalación.
    *   Tipo de componente `Script` para los scripts del proveedor de datos que se deben desinstalar.

*   [`Config`](https://www.dnnsoftware.com/wiki/manifest-config-component). Cambios para hacer en el archivo de configuración especificado.

    ```

        <component type="Config">
            <config>
                <configFile>web.config</configFile <!-- Name of config file, including its path relative to the root of the DNN installation. -->
                <install>
                    <configuration>
                        <nodes>
                            <node path="/configuration/system.webServer/handlers" action="update" key="path" collision="overwrite">
                                ...
                            </node>
                            <node />
                            ...
                        </nodes>
                    </configuration>
                </install>
                <uninstall>
                    <configuration>
                        <nodes />
                    </configuration>
                </uninstall>
            </config>
            <config />
            ...
        </component>

    ```

    Para obtener información sobre los atributos node, consulte [Manifiesto: XML Merge](https://www.dnnsoftware.com/wiki/manifest-xml-merge).

*   [`Container`](https://www.dnnsoftware.com/wiki/manifest-container-component). Contenedores a instalar.

    ```

        <component type="Container">
            <containerFiles>
                <basePath / <!-- Target base folder for the component installation. Relative to the root of the DNN installation. -->
                <containerName />
                <containerFile>
                    <path / <!-- Target file folder. Relative to basePath. -->
                    <name />
                </containerFile>
                <containerFile />
                ...
            </containerFiles>
        </component>

    ```

*   [`DashboardControl`](https://www.dnnsoftware.com/wiki/manifest-dashboardcontrol-component). Controles que aparecerán como pestañas separadas en el panel de control de DNN (Host \> Panel de control).

    ```

        <component type="DashboardControl">
            <dashboardControl>
                <key />
                <src />
                <localResources />
                <controllerClass />
                <isEnabled />
                <viewOrder />
            </dashboardControl>
            <dashboardControl />
            ...
        </component>

    ```

*   [`File`](https://www.dnnsoftware.com/wiki/manifest-file-component).  Archivos a instalar. De forma predeterminada, solo se instalan los archivos con extensiones de archivo permitidas; sin embargo, el usuario host puede omitir esta comprobación de seguridad durante la instalación. Para ver o modificar la lista de extensiones de archivo permitidas, vaya a la instalación de su DNN y elija Host \> Configuración del host \> Otras configuraciones \> Extensiones de archivo permitidas.

    ```

        <component type="File">
            <files>
                <basePath / <!-- Target base folder for the component installation. Relative to the root of the DNN installation. -->
                <file>
                    <path / <!-- Target file folder. Relative to basePath. Also assumed to be the source file folder in the zip file, if sourceFileName is not defined. -->
                    <name />
                    <sourceFileName / <!-- The path and name of a file inside the zip file. -->
                </file>
                <file />
                ...
            </files>
        </component>

    ```

    Ejemplo: para copiar img/MyAwesomeImageFile.jpg del archivo zip a desktopmodules/mymodule/images/MyFile.jpg,,

    ```

        <basePath>desktopmodules/mymodule</basePath>
        <file>
            <path>images</path>
            <name>MyFile.jpg</name>
            <sourceFileName>img/MyAwesomeImageFile.jpg</sourceFileName>
        </file>

    ```

*   [`CoreLanguage`](https://www.dnnsoftware.com/wiki/manifest-corelanguage-component). Archivos de paquetes de idioma necesarios para localizar la plataforma de DNN para una cultura específica. Se puede instalar un paquete de idioma central durante la instalación de la plataforma DNN o en cualquier momento posterior.

    ```

        <component type="CoreLanguage">
            <languageFiles>
                <code />
                <displayName />
                <fallback / <!-- Code for the alternative language. Used if a resource is not found in the current language pack. -->
                <languageFile>
                    <path / <!-- Target file folder. Relative to the root of the DNN installation. -->
                    <name />
                </languageFile>
                <languageFile />
                ...
            </languageFiles>
        </component>

    ```

    Para obtener la lista de códigos de idioma compatibles, consulte la clase .NET [CultureInfo](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.cultureinfo) class.

*   [`ExtensionLanguage`](https://www.dnnsoftware.com/wiki/manifest-extensionlanguage-component). Archivos de paquete de idioma necesarios para localizar una extensión DNN para una cultura específica.

    ```

        <component type="ExtensionLanguage">
            <languageFiles>
                <code />
                <package / <!-- Name of another package that contains the extension that this language pack is intended for. -->
                <basePath / <!-- Target base folder for the component installation. Relative to the root of the DNN installation. -->
                <languageFile>
                    <path / <!-- Target file folder. Relative to basePath. -->
                    <name />
                </languageFile>
                <languageFile />
                ...
            </languageFiles>
        </component>

    ```

    Para obtener la lista de códigos de idioma compatibles, consulte la clase .NET [CultureInfo](https://docs.microsoft.com/en-us/dotnet/api/system.globalization.cultureinfo) class.

*   [`Module`](https://www.dnnsoftware.com/wiki/module-component). Solo se permite `type="Module"` en un componente dentro de una sección `package`. Para instalar un conjunto de módulos como una unidad, cree una sección `package` por módulo en el mismo manifiesto.

    ```

        <component type="Module">
            <desktopModule>
                <moduleName />
                <foldername />
                <businessControllerClass />
                <codeSubdirectory />
                <isAdmin />
                <isPremium />
                <supportedFeatures<!-- Requires a value for businessControllerClass. -->
                    <supportedFeature type="Portable" /<!-- The module has import/export capabilities using the IPortable interface. -->
                    <supportedFeature type="Searchable" /<!-- The module can be indexed or searched using the ISearchable interface. -->
                    <supportedFeature type="Upgradeable" /<!-- The module can be upgraded using the IUpgradeable interface. -->
                    ...
                </supportedFeatures>
                <moduleDefinition>
                    <friendlyName />
                    <defaultCacheTime />
                    <moduleControls>
                        <moduleControl>
                            <controlKey />
                            <controlSrc />
                            <supportsPartialRendering />
                            <controlTitle />
                            <controlType />
                            <iconFile />
                            <helpUrl />
                        </moduleControl>
                        <moduleControl />
                        ...
                    </moduleControls>
                    <permissions>
                        <!-- In <permission>,
                            "code" is the code for the module,
                            "key" is the code for the permission, and
                            "name" is the user-friendly name for the permission.
                        -->
                        <permission code="..." key="..." name="..." />
                        <permission code="..." key="..." name="..." />
                        ...
                    </permissions>
                </moduleDefinition>
            </desktopModule>
            <eventMessage>
                <processorType />
                <processorCommand />
                <attributes>
                    <node>value</node>
                </attributes>
            </eventMessage>
        </component>

    ```

*   [`Provider`](https://www.dnnsoftware.com/wiki/manifest-provider-component). Amplía la lista de extensiones de archivo permitidas. Estas extensiones de archivo adicionales se aplican solo a la instalación actual y no se agregan a la lista global de extensiones de archivo que se encuentran en Host \> Configuración del host \> Otras configuraciones \> Extensiones de archivo permitidas. Se permiten las siguientes extensiones de archivo: .ashx, .aspx, .ascx, .vb, .cs, .resx, .css, .js, .resources, .config, .xml, .htc, .html, .htm, .text, .vbproj, .csproj y .sln.

    ```

        <component type="Provider" />

    ```

*   [`ResourceFile`](https://www.dnnsoftware.com/wiki/manifest-resourcefile-component). Archivos zip para descomprimir durante la instalación. Puede utilizarse en lugar de `component type="File"` para simplificar el manifiesto de paquetes que contienen muchos archivos.

.

    ```

        <component type="ResourceFile">
            <resourceFiles>
                <basePath /<!-- Target folder where the contents of the zip file will be installed. Relative to the root of the DNN installation. -->
                <resourceFile>
                    <name /<!-- Name of zip file. -->
                </resourceFile>
                <resourceFile />
                ...
            </resourceFiles>
        </component>

    ```

*   [`Script`](https://www.dnnsoftware.com/wiki/script-component). Scripts de base de datos que la extensión necesita. Los siguientes scripts se manejan de manera diferente::

    *   `install.<dataprovidertype>` (e.g., `install.SqlDataProvider`) se ejecuta _antes_ de todos los demás scripts, si el paquete se está instalando por primera vez.
    *   `upgrade.<dataprovidertype>` (e.g., `upgrade.SqlDataProvider`) e ejecuta _después_ de todos los otros scripts.

    ```

        <component type="Script">
            <scripts>
                <basePath /<!-- Target base folder for the component installation. Relative to the root of the DNN installation. -->
                <script type="Install" >
                    <path /<!-- Target file folder. Relative to basePath. -->
                    <name /<!-- Must be named "<scriptversion>.<dataprovider>". Example: 01.00.00.SqlDataProvider -->
                    <version /<!-- Version of script file to be installed. -->
                </script>
                <script type="UnInstall" >
                    <path /<!-- Location of script file. Relative to basePath. -->
                    <name /<!-- Must be named "uninstall.<dataprovidertype>". Example: uninstall.SqlDataProvider -->
                    <version /<!-- Version of script file to be removed. -->
                </script>
                ...
            </scripts>
        </component>

    ```

*   [`Skin`](https://www.dnnsoftware.com/wiki/manifest-skin-component). Todos los archivos relacionados con el tema (Theme). El instalador debe analizar los archivos de temas principales en el momento de la instalación para reemplazar los nombres de carpetas relativos; por lo tanto, cada archivo ASCX, HTML o CSS debe ser declarado como un archivo `skinFile`. Otros archivos (es decir, imágenes y scripts) se pueden empaquetar utilizando el tipo de componente ``TEXT`` para simplificar la complejidad del manifiesto del tema.

    ```

        <component type="Skin">
            <skinFiles>
                <basePath /<!-- Target base folder for the component installation. Relative to the root of the DNN installation. -->
                <skinName />
                <skinFile>
                    <path /<!-- Target file folder. Relative to basePath. -->
                    <name />
                </skinFile>
                <skinFile />
                ...
            </skinFiles>
        </component>

    ```

*   [`SkinObject`](https://www.dnnsoftware.com/wiki/manifest-skinobject-component). Objetos temáticos personalizados.

    ```

        <component type="SkinObject">
            <moduleControl>
                <controlKey /<!-- Token of the skin object within square brackets []; e.g., [COPYRIGHT] -->
                <controlSrc /<!-- Target file folder for the theme object's ASCX file. -->
                <supportsPartialRendering /<!-- "true" if the theme object supports partial rendering through an MS AJAX update panel wrapper. Default: "false" -->
            </moduleControl>
        </component>

    ```

*   [`URLProvider`](https://www.dnnsoftware.com/wiki/manifest-url-provider). Proveedor de URL personalizado que se utilizará con el Sistema de gestión avanzada de URL (AUM).

    ```

        <component type="URLProvider">
            <urlProvider>
                <name />
                <type />
                <settingsControlSrc />
                <redirectAllUrls />
                <replaceAllUrls />
                <rewriteAllUrls />
                <desktopModule />
            </urlProvider>
        </component>

    ```

