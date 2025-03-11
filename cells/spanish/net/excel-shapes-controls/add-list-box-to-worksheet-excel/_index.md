---
title: Agregar un cuadro de lista a una hoja de cálculo en Excel
linktitle: Agregar un cuadro de lista a una hoja de cálculo en Excel
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a agregar un cuadro de lista a una hoja de cálculo de Excel con Aspose.Cells para .NET. Siga nuestra sencilla guía paso a paso y haga que sus hojas de cálculo de Excel sean interactivas.
weight: 20
url: /es/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar un cuadro de lista a una hoja de cálculo en Excel

## Introducción
Agregar elementos interactivos a las hojas de cálculo de Excel, como un cuadro de lista, puede mejorar significativamente la administración y presentación de datos. Ya sea que esté creando un formulario interactivo o una herramienta de ingreso de datos personalizada, la capacidad de controlar la entrada del usuario con un cuadro de lista es invaluable. Aspose.Cells para .NET proporciona una forma eficiente de agregar y administrar estos controles en sus archivos de Excel. En esta guía, lo guiaremos a través del proceso de agregar un cuadro de lista a una hoja de cálculo utilizando Aspose.Cells para .NET.
## Prerrequisitos
Antes de comenzar a codificar, asegúrese de tener las siguientes herramientas y recursos disponibles:
-  Biblioteca Aspose.Cells para .NET: puede descargarla desde[Página de descarga de Aspose.Cells para .NET](https://releases.aspose.com/cells/net/).
- Entorno de desarrollo: cualquier IDE que admita el desarrollo .NET, como Visual Studio.
- .NET Framework: asegúrese de que su proyecto tenga como objetivo una versión compatible de .NET Framework.
 Además, considere obtener un[licencia temporal](https://purchase.aspose.com/temporary-license/) Si quieres explorar todas las funcionalidades sin limitaciones.
## Importar paquetes
Antes de comenzar, asegúrese de haber importado los espacios de nombres Aspose.Cells necesarios. A continuación, le indicamos cómo hacerlo:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
En este tutorial, desglosaremos el proceso de agregar un cuadro de lista en varios pasos simples. Siga cada paso de cerca para asegurarse de que todo funcione como se espera.
## Paso 1: Configuración del directorio de documentos
Antes de crear un archivo de Excel, necesita una ubicación para guardarlo. A continuación, se muestra cómo configurar el directorio:
```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
// Crear directorio si aún no existe.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
En este paso, definirá dónde se almacenará el archivo. El código comprueba si el directorio existe y, si no existe, crea uno para usted. Esto garantiza que no se encontrará con ningún error de "archivo no encontrado" más adelante.
## Paso 2: Cree un nuevo libro de trabajo y acceda a la primera hoja de trabajo
A continuación, crearemos un nuevo libro de trabajo y accederemos a la primera hoja de trabajo donde agregaremos nuestro cuadro de lista.
```csharp
// Crear un nuevo libro de trabajo.
Workbook workbook = new Workbook();
// Obtenga la primera hoja de trabajo.
Worksheet sheet = workbook.Worksheets[0];
```
Un libro de trabajo es básicamente un archivo de Excel. Aquí, estamos creando un nuevo libro de trabajo y accediendo a la primera hoja de cálculo, que es donde colocaremos nuestro cuadro de lista. Piense en esto como si estuviera creando un lienzo en blanco donde pintará los controles.
## Paso 3: Ingrese datos para el cuadro de lista
Antes de agregar el cuadro de lista, necesitamos completar algunos datos a los que hará referencia el cuadro de lista.
```csharp
// Obtenga la colección de celdas de la hoja de trabajo.
Cells cells = sheet.Cells;
// Introduzca un valor para la etiqueta.
cells["B3"].PutValue("Choose Dept:");
// Establezca la etiqueta en negrita.
cells["B3"].GetStyle().Font.IsBold = true;
// Valores de entrada para el cuadro de lista.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Aquí, estamos agregando algo de texto a la hoja de cálculo. La etiqueta "Elegir departamento:" se coloca en la celda B3 y su fuente está configurada en negrita. En la columna A, estamos insertando valores que servirán como rango de entrada para nuestro cuadro de lista, que representan diferentes departamentos. Este rango de entrada es lo que los usuarios elegirán al interactuar con el cuadro de lista.
## Paso 4: Agregue el cuadro de lista a la hoja de cálculo
Ahora que hemos configurado los datos, agreguemos el control del cuadro de lista.
```csharp
// Agregar un nuevo cuadro de lista.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Este código agrega el cuadro de lista a la hoja de cálculo. Los parámetros definen la posición y el tamaño del cuadro de lista. El cuadro de lista se coloca en la fila 2, columna 0 con un ancho de 122 y una altura de 100. Estas son las coordenadas y el tamaño que determinan dónde aparecerá el cuadro de lista en la hoja de cálculo.
## Paso 5: Establecer las propiedades del cuadro de lista
A continuación, configuraremos varias propiedades para el cuadro de lista para que sea completamente funcional.
```csharp
// Establecer el tipo de ubicación.
listBox.Placement = PlacementType.FreeFloating;
// Establecer la celda vinculada.
listBox.LinkedCell = "A1";
// Establecer el rango de entrada.
listBox.InputRange = "A2:A7";
// Establecer el tipo de selección.
listBox.SelectionType = SelectionType.Single;
// Establezca el cuadro de lista con sombreado 3D.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: esta propiedad garantiza que el cuadro de lista permanezca en su posición independientemente de cómo se modifique la hoja de cálculo.
- LinkedCell: Esto establece una celda (en este caso, A1) donde se mostrará el valor seleccionado del cuadro de lista.
- InputRange: Esto le indica al cuadro de lista dónde buscar su lista de opciones (A2 a A7, que configuramos anteriormente).
- SelectionType.Single: Esto restringe al usuario a seleccionar solo un elemento del cuadro de lista.
- Sombra: el efecto de sombra le da al cuadro de lista una apariencia más tridimensional, lo que lo hace visualmente atractivo.
## Paso 6: Guarde el archivo Excel
Por último, guardemos nuestro libro de trabajo con el cuadro de lista incluido.
```csharp
// Guardar el libro de trabajo.
workbook.Save(dataDir + "book1.out.xls");
```
Esta línea de código guarda el libro de trabajo en el directorio que configuramos anteriormente. El archivo se llama "book1.out.xls", pero puedes elegir cualquier nombre que se adapte a tu proyecto.
## Conclusión
¡Y ya está! Ha agregado con éxito un cuadro de lista a una hoja de cálculo de Excel con Aspose.Cells para .NET. Con solo unas pocas líneas de código, creamos un cuadro de lista completamente funcional, lo que hace que la hoja de cálculo sea más interactiva y dinámica. Este tutorial debería brindarle una base sólida para explorar otros controles y funciones en Aspose.Cells para .NET. ¡Siga experimentando y pronto dominará la amplia funcionalidad de la biblioteca!
## Preguntas frecuentes
### ¿Puedo permitir selecciones múltiples en el cuadro de lista?  
 Sí, puedes cambiar el`SelectionType` a`SelectionType.Multi` para permitir selecciones múltiples.
### ¿Puedo cambiar la apariencia del cuadro de lista?  
¡Por supuesto! Aspose.Cells te permite personalizar el aspecto del cuadro de lista, incluido el tamaño, la fuente e incluso el color.
### ¿Qué pasa si necesito eliminar el cuadro de lista más tarde?  
 Puede acceder y eliminar el cuadro de lista desde el`Shapes` colección usando`sheet.Shapes.RemoveAt(index)`.
### ¿Puedo vincular el cuadro de lista a una celda diferente?  
 Sí, simplemente cambia el`LinkedCell` propiedad a cualquier otra celda donde desee mostrar el valor seleccionado.
### ¿Cómo puedo agregar más elementos al cuadro de lista?  
Simplemente actualice el rango de entrada insertando más valores en las celdas especificadas y el cuadro de lista se actualizará automáticamente.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
