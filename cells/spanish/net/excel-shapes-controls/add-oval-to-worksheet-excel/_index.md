---
"description": "Aprende a agregar un óvalo a una hoja de cálculo de Excel con Aspose.Cells para .NET. Guía paso a paso con explicaciones detalladas del código."
"linktitle": "Agregar óvalo a la hoja de cálculo en Excel"
"second_title": "API de procesamiento de Excel Aspose.Cells .NET"
"title": "Agregar óvalo a la hoja de cálculo en Excel"
"url": "/es/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Agregar óvalo a la hoja de cálculo en Excel

## Introducción
Crear archivos de Excel impactantes e interactivos implica mucho más que solo números y fórmulas. Formas como los óvalos pueden añadir atractivo visual o aportar elementos funcionales a tus hojas de cálculo. En este tutorial, exploraremos cómo usar Aspose.Cells para .NET para añadir óvalos a una hoja de cálculo de Excel mediante programación. Tanto si buscas añadir estilo como funcionalidad, te ayudamos con una guía paso a paso que lo explica todo.
## Prerrequisitos
Antes de sumergirte en el código, hay algunas cosas que debes tener en cuenta:
1. Biblioteca Aspose.Cells para .NET: puede descargarla desde [aquí](https://releases.aspose.com/cells/net/) o instálelo usando NuGet en Visual Studio.
2. Entorno de desarrollo: AC# IDE como Visual Studio.
3. Comprensión básica de C#: debe estar familiarizado con los conceptos básicos de codificación en C#.
Además, recuerda configurar tu proyecto instalando la biblioteca Aspose.Cells para .NET. Si aún no tienes una licencia, puedes solicitar una. [licencia temporal](https://purchase.aspose.com/temporary-license/) o utiliza el [prueba gratuita](https://releases.aspose.com/) versión.
## Importar paquetes
Antes de escribir código, asegúrese de incluir los espacios de nombres necesarios. Aquí tiene el fragmento de código de C# para asegurarse de usar las bibliotecas correctas:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Paso 1: Configure su directorio
El primer paso para agregar un óvalo a una hoja de Excel es especificar dónde se guardará el archivo. Definamos la ruta del directorio y asegurémonos de que exista antes de guardar nuestro trabajo.

Crearemos una ruta de directorio y verificaremos su existencia. Si la carpeta no existe, se creará.
```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
// Crear directorio si aún no está presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Este paso es crucial ya que garantiza que su archivo se guarde en una ubicación adecuada y que no tenga problemas con la ruta del archivo más adelante.
## Paso 2: Inicializar un nuevo libro de trabajo
A continuación, necesitamos crear un nuevo libro de trabajo donde añadiremos nuestras formas ovaladas. Este libro representa un archivo de Excel y podemos añadirle contenido o formas.

En este paso, instanciamos una nueva `Workbook` objeto que servirá como nuestro contenedor de archivos Excel.
```csharp
// Crear una instancia de un nuevo libro de trabajo.
Workbook excelbook = new Workbook();
```
## Paso 3: Agrega la primera forma ovalada
Ahora viene la parte divertida: añadir un óvalo a la hoja de cálculo. Este óvalo podría representar un elemento visual, como un botón o un resaltador. Empezaremos añadiendo el primer óvalo a la primera hoja de cálculo de nuestro libro.

Aquí usamos el `Shapes.AddOval()` método para crear un óvalo en la hoja de cálculo en una fila y columna específicas.
```csharp
// Añade una forma ovalada.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
Los parámetros dentro `AddOval()` son los siguientes:
- Los dos primeros números representan la fila y la columna de la esquina superior izquierda del óvalo.
- Los siguientes dos números representan la altura y el ancho del óvalo.
## Paso 4: Establezca la ubicación y el estilo del óvalo
Una vez creado el óvalo, podemos establecer su posición, grosor de línea y estilo de trazo. `Placement` La propiedad determina cómo se comporta el óvalo cuando cambia el tamaño o mueve celdas en la hoja de cálculo.

Hacemos que el óvalo flote libremente y ajustamos su apariencia.
```csharp
// Establezca la ubicación del óvalo.
oval1.Placement = PlacementType.FreeFloating;
// Establezca el grosor de la línea.
oval1.Line.Weight = 1;
// Establece el estilo del guion del óvalo.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Esto permite que el óvalo se mueva libremente dentro de la hoja de cálculo, y su grosor de línea y estilo se configuran para lograr consistencia visual.
## Paso 5: Agrega otra forma ovalada (círculo)
¿Por qué conformarse con uno solo? En este paso, añadiremos otra forma ovalada, creando esta vez un círculo perfecto con la misma altura y anchura.

Creamos otro óvalo, lo colocamos en una ubicación diferente y nos aseguramos de que tenga forma circular estableciendo la misma altura y ancho.
```csharp
// Añade otra forma ovalada (círculo).
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Paso 6: Dale estilo al segundo óvalo
Al igual que antes, ajustaremos la ubicación, el peso y el estilo del trazo de este segundo óvalo (o círculo).

Aplicamos propiedades similares al segundo óvalo para que coincida con el estilo del primero.
```csharp
// Establezca la ubicación del óvalo.
oval2.Placement = PlacementType.FreeFloating;
// Establezca el grosor de la línea.
oval2.Line.Weight = 1;
// Establece el estilo del guion del óvalo.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Paso 7: Guardar el libro de trabajo
Finalmente, debemos guardar el libro de trabajo con los óvalos que acabamos de añadir. Guardar el archivo garantiza que se guarden todos los cambios.

Guardamos el libro de trabajo en la ruta del directorio que definimos anteriormente.
```csharp
// Guarde el archivo Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
¡Listo! Has añadido óvalos a tu hoja de cálculo de Excel y has guardado el archivo.
## Conclusión
Añadir formas como óvalos a una hoja de Excel con Aspose.Cells para .NET no solo es sencillo, sino también una forma divertida de mejorar tus hojas de cálculo con elementos visuales adicionales. Ya sea para fines de diseño o para añadir elementos interactivos, las formas pueden desempeñar un papel fundamental en la apariencia y el funcionamiento de tus archivos de Excel. Así, la próxima vez que trabajes en un proyecto que requiera hojas de Excel interactivas o visualmente atractivas, ¡sabrás exactamente cómo añadir esos óvalos perfectos!
## Preguntas frecuentes
### ¿Puedo agregar otras formas como rectángulos o líneas usando Aspose.Cells para .NET?
Sí, puedes agregar varias formas como rectángulos, líneas y flechas usando el `Shapes` colección en Aspose.Cells.
### ¿Es posible cambiar el tamaño de los óvalos después de agregarlos?
¡Claro! Puedes modificar la altura y el ancho de los óvalos después de añadirlos.
### ¿En qué formatos de archivo puedo guardar el libro de trabajo además de XLS?
Aspose.Cells admite múltiples formatos como XLSX, CSV y PDF, entre otros.
### ¿Puedo modificar el color del contorno del óvalo?
Sí, puedes cambiar el color de la línea del óvalo usando el `Line.Color` propiedad.
### ¿Es necesario tener una licencia para Aspose.Cells?
Si bien puedes probar Aspose.Cells con una versión de prueba gratuita, necesitarás una [licencia](https://purchase.aspose.com/buy) para uso a largo plazo o para acceder a funciones avanzadas.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}