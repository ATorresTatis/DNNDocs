# Documentación de la plataforma DNN

El sitio de documentación para el sistema de gestión de contenido de código abierto DNN (anteriormente DotNetNuke).

El proyecto utiliza la biblioteca `docfx` para extraer comentarios XML del código fuente de la Plataforma DNN y combinarlo con artículos escritos en Markdown para formar la documentación para DNN.

## Instalar Git
Si no lo tiene instalado, primero deberá instalar Git. Puede encontrar instrucciones sobre cómo instalar Git [aquí](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Instalar DocFX
DocFX puede instalarse en Windows a través de Chocolatey ejecutando `choco install docfx -y`

Si está en MacOS, puede instalarlo con _Homebrew_, así `brew install docfx`

O puede descargar y descomprimir`docfx.zip` desde [GitHub](https://github.com/dotnet/docfx/releases), extraerlo a una carpeta y luego configurar la ruta en `PATH` a esa carpeta para que pueda ejecutarlo desde cualquier lugar

## Configurando el Proyecto DNN Docs
Después de instalar DocFX, el siguiente paso es clonar este repositorio. 'Clonar el repositorio' simplemente creará una copia del repositorio (archivos y carpetas) en su máquina local para que pueda trabajar con ellos.

Tenga en cuenta que el siguiente comando de ejemplo clona el repositorio en la ubicación `c:\dev`. Actualice la ubicación `c:\dev` a la ubicación de su elección en su máquina.

```
c:\dev> git clone https://github.com/DNNCommunity/DNNDocs.git
```

The previous command will have created a folder called `DNNDocs` in the `c:\dev` folder. Navigate to that directory by using the cd (Change Directory) command. `cd` into the `DNNDocs` folder.
```
c:\dev> cd DNNDocs
```

Next, you'll need to fork and/or clone the [Dnn.Platform repository](https://github.com/dnnsoftware/Dnn.Platform) into a **sub-folder** of the `DNNDocs` root folder. The reason is that the project reads the XML comments in the source code and creates API documentation from that, in addition to the documentation center articles.

Please note this could take a few minutes depending on your connection speed.
```
c:\dev\dnn-docs>git clone https://github.com/dnnsoftware/Dnn.Platform.git
```

## Running the DNN Docs Project Locally
You should now be able to run the development version of the docs locally with the following command:

```
docfx --serve
```

[!NOTE]
You should run your shell in administrator mode for this to work!

The first time, the compilation process could take quite a while. You may see a couple of warning messages. Eventually, you should see a message similar to:
```
Serving "C:\dev\DNNDocs\_site" on https://localhost:8080
```

Open that page up in your browser to see the documentation.
