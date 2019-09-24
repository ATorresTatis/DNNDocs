---
uid: mvc-module-unittest
locale: es
title: Crear una prueba unitaria para un módulo MVC
dnnversion: 09.02.00
related-topics: developers-mvc-modules-overview,mvc-module-mvccontroller,mvc-module-mvcviews,unsupported-mvc-features
links: ["[Microsoft MSDN: Unit Test Basics](https://docs.microsoft.com/en-us/visualstudio/test/unit-test-basics)","[Microsoft Visual Studio: Run tests with your builds for continuous integration](https://www.visualstudio.com/en-gb/docs/test/continuous-testing/test-build)","[Moq](https://www.nuget.org/packages/Moq/)"]
---

# Crear una prueba unitaria para un módulo MVC

## Visión

Debido a que los controladores MVC son la lógica comercial central de un módulo MVC, es una buena práctica crear pruebas unitarias automatizadas para garantizar que se comporten según lo previsto. Este ejemplo ilustra cómo crear una prueba unitaria para el controlador MVC de su módulo.

> [!Nota] Este procedimiento de prueba de la unidad es aplicable solo a los módulos creados con la plantilla de módulo DNN MVC.

## Prerrequisitos

Un módulo creado con la plantilla de módulo DNN MVC en Visual Studio como un proyecto con plantillas.
*   [Moq](https://www.nuget.org/packages/Moq/), un marco de simulación para C#/.NET.

## Pasos

1.  Agregue un nuevo proyecto de prueba unitaria a la solución del módulo MVC..
    1.  En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en la solución del módulo MVC y seleccione Agregar \> Nuevo proyecto.



        ![Agregar nuevo proyecto](/images/scr-mvc-unittest-addproject.png)



    2.  En el cuadro de diálogo Agregar nuevo proyecto, seleccione Proyecto de prueba unitaria, ingrese un nombre y seleccione la carpeta local para almacenarlo.



        ![Crear proyecto de prueba unitaria](/images/scr-mvc-unittest-create.png)



2.  Agregue las referencias de ensamblados de MVC y DNN necesarias.

    Para cada conjunto que se agregará al nuevo proyecto de pruebas unitarias, haga clic con el botón derecho en el nodo Referencias del proyecto y agregue una referencia de conjunto.



    ![Referencia de proyecto](/images/scr-mvc-unittest-projref.png)



    Agregue referencias a los siguientes ensamblados, así como a otros que su módulo necesite específicamente:

    *   DotNetNuke
    *   DotNetNuke.Web.Mvc
    *   System.Web.Mvc

3.  (Opcional) Use Moq para simular un almacén de datos.

    Moq es un marco de simulación para C#/.NET, que generalmente se utiliza en pruebas unitarias para crear rápidamente objetos de dependencia que imitan objetos reales. Este proyecto utiliza Moq para simular un objeto ItemManager para ejecutar pruebas sin requerir una base de datos.

    Nota: Este paso no es necesario para la prueba de ejemplo, pero es necesario en la mayoría de los casos de prueba del mundo real.

    1.  En el Explorador de soluciones de Visual Studio, haga clic derecho en su proyecto de prueba unitaria.
    2.  Elija Administrar paquetes Nuget.
    3.  Busque Moq e instálelo.



        ![Instalación de Moq](/images/scr-mvc-unittest-moqnuget.png)




    Este ejemplo crea una clase MockStores para usar con Moq y simular una base de datos y su comportamiento.

    Cree una carpeta llamada Mocks y cree un archivo MockStores.cs dentro de la carpeta. Ingrese el siguiente código en MockStores.cs:

    ```

        using System.Collections.Generic;
        using System.Linq;
        using Dnn.Modules.CompanyName.MyMvcModule.Components;
        using Dnn.Modules.CompanyName.MyMvcModule.Models;
        using Moq;

        namespace MyMvcModuleTests.Mocks
        {
            class MockStores
            {
                public static Mock<IItemManager> MockItemManager()
                {
                    var allItems = new List<Item>();
                    var mock = new Mock<IItemManager>();

                    // void CreateItem(Item t);
                    mock.Setup(x => x.CreateItem(It.IsAny<Item>()))
                        .Callback((Item i) =>
                        {
                            allItems.Add(i);
                        });

                    // void DeleteItem(int itemId, int moduleId);
                    mock.Setup(x => x.DeleteItem(It.IsAny<int>(), It.IsAny<int>()))
                        .Callback((int id, int mid) =>
                        {
                            var remItem = allItems.FirstOrDefault(i => i.ItemId == id && i.ModuleId == mid);
                            allItems.Remove(remItem);
                        });

                    // void DeleteItem(Item t);
                    mock.Setup(x => x.DeleteItem(It.IsAny<Item>()))
                        .Callback((Item di) =>
                        {
                            var remItem = allItems.FirstOrDefault(i => i.ItemId == di.ItemId);
                            allItems.Remove(remItem);
                        });

                    // IEnumerable<Item> GetItems(int moduleId);
                    mock.Setup(x => x.GetItems(It.IsAny<int>()))
                        .Returns((int mid) => allItems.Where(x => x.ModuleId == mid));

                    // Item GetItem(int itemId, int moduleId);
                    mock.Setup(x => x.GetItem(It.IsAny<int>(), It.IsAny<int>()))
                        .Returns((int id, int mid) => allItems.FirstOrDefault(i => i.ItemId == id && i.ModuleId == mid));

                    // void UpdateItem(Item t);
                    mock.Setup(x => x.UpdateItem(It.IsAny<Item>()))
                        .Callback((Item i) =>
                        {
                            allItems.Add(i);
                        });

                    return mock;
                }
            }
        }

    ```

    El método estático MockItemManager() en la clase MockStores simula todos los métodos de una implementación IItemManager. Por lo tanto, MockStores se puede usar en el controlador como la implementación de IItemManager..

    La variable allItems es una lista genérica de objetos Item y sirve como almacén de datos.

4.  Cree la prueba unitaria.

    Consejo: Los nombres de los métodos de prueba de unidad deberían ser más descriptivos que los métodos típicos. Idealmente, el nombre del método de prueba incluye el nombre del método que se está probando, la prueba que se está realizando y el resultado esperado. Por ejemplo: `Edit_CreateNewItem_ModuleIdAssignedinModel` podría ser el nombre de un método de prueba que verifica si un método Edit() crea un nuevo elemento (si el elemento aún no existe) al verificar si el ID de módulo está asignado en el modelo de la vista.

    Este ejemplo crea una prueba unitaria para la clase ItemController.

    Puede cambiar el nombre del archivo de prueba de unidad de muestra UnitTest1.cs (incluido de forma predeterminada cuando se creó el nuevo proyecto de prueba de unidad) a ItemControllerTests.cs o crear un nuevo archivo. Luego ingrese el siguiente código en ItemControllerTests.cs:

    ```

    	using System.Web.Mvc;
    	using Dnn.Modules.CompanyName.MyMvcModule.Controllers;
    	using Dnn.Modules.CompanyName.MyMvcModule.Models;
    	using Microsoft.VisualStudio.TestTools.UnitTesting;
    	using MyMvcModuleTests.Mocks;

    	namespace MyMvcModuleTests
    	{
    		[TestClass]
    		public class ItemControllerTests
    		{
    			[TestMethod]
    			public void Edit_CreateNewItem_ModuleIdAssignedinModel()
    			{
    				// 1 - Arrange
    				int moduleId = 2;
    				var mockData = MockStores.MockItemManager();
    				var modTwoItemCntrl = new ItemController(mockData.Object, moduleId); // Create a controller for the module with moduleId=2.

    				// 2 - Act
    				var actionResult = (ViewResult)modTwoItemCntrl.Edit(); // Call the edit view with no item Id (Add New).

    				// 3 - Assert
    				var itemModel = (Item)actionResult.Model;
    				Assert.IsTrue(itemModel != null && itemModel.ModuleId == moduleId);
    			}
    		}
    	}

    ```

    Esta muestra de prueba unitaria utiliza el patrón Arrange Act Assert de una prueba unitaria:

    *   Arrange: crea una nueva instancia de ItemController con una nueva instancia de MockStores.MockItemManager y moduleId. (El siguiente paso actualiza el constructor ItemController para trabajar con esta prueba unitaria.
    *   Act: se llama al método Edit() del control sin ningún parámetro y se guarda el resultado.
    *   Assert: La prueba verifica que el valor de moduleId esté configurado en el módulo de Vista resultante antes de que se visualice la vista de agregar/editar elemento.

    Si su controlador tiene una lógica empresarial más compleja, puede automatizar la validación de la prueba unitaria.

5.  Adapte el método ItemController.Edit() para trabajar con pruebas unitarias.

    En el código que se generó usando las plantillas del módulo MVC, el ItemController no tiene capacidad de inyección de dependencia para la capa de datos. Además, algunos objetos de entorno básicos de DNN, como `PortalSettings` y `ModuleContext` no están disponibles al ejecutar pruebas unitarias. La actualización del método ItemController.Edit() corrige estas limitaciones.

    Este ejemplo agrega un constructor y una variable de clase al ItemController para inyectar la implementación / simulador IItemManager y moduleId.

    ```

        public ActionResult Edit(int itemId = -1)
        {
            // Ignore registration errors for unit tests.
            try { DotNetNuke.Framework.JavaScriptLibraries.JavaScript.RequestRegistration(CommonJs.DnnPlugins); }
            catch { }

            if (PortalSettings != null)
            {
                var userlist = UserController.GetUsers(PortalSettings.PortalId);
                var users = from user in userlist.Cast<UserInfo>().ToList()
                select new SelectListItem { Text = user.DisplayName, Value = user.UserID.ToString() };

                ViewBag.Users = users;
            }

            if (ModuleContext != null)
            {
                _moduleId = ModuleContext.ModuleId;
            }

            var item = (itemId == -1)
                ? new Item { ModuleId = _moduleId }
                : ItemManager.Instance.GetItem(itemId, _moduleId);

            return View(item);
        }

    ```

    Algunas líneas en el ItemController predeterminado no son aplicables a esta prueba de unidad de muestra, que utiliza una simulación de ItemController.

    Para ignorar esas líneas cuando se ejecuta la prueba de la unidad, el método ItemController.Edit() actualizado revisa PortalSettings y ModuleContext, que obtienen sus valores del motor de tiempo de ejecución del módulo. Durante la prueba unitaria, la simulación de ItemController omite el motor de tiempo de ejecución; por lo tanto, estas variables se configuran a `null` cuando se ejecuta la prueba unitaria.

    La variable _\_moduleId_ se pasa al constructor como parámetro itemId mediante la prueba unitaria de muestra y la instancia de ItemManager.Instance será nuestra instancia simulada porque nuestra prueba de unidad anuló la implementación en el constructor.

6.  Ejecute la prueba unitaria..

    Puede ejecutar una prueba unitaria en Visual Studio:

    *   Pruebas \> Depuración
    *   Pruebas \> Ejecutar

    La ventana Explorador de pruebas le ofrece una vista rápida de todas las pruebas, los resultados de estas y los comandos para ejecutarlas.

    ![ Explorador de pruebas unitarias](/images/scr-mvc-unittest-testexplorer.png)



    Para usuarios más avanzados, las pruebas unitarias pueden programarse para ejecutarse automáticamente como parte de su proceso de compilación.
