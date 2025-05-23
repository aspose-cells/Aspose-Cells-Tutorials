---
"description": "Aprenda a especificar HTML CrossType en Aspose.Cells para .NET. Siga nuestro tutorial paso a paso para convertir archivos de Excel a HTML con precisión."
"linktitle": "Especificación de HTML CrossType en la salida HTML mediante programación en .NET"
"second_title": "API de procesamiento de Excel Aspose.Cells .NET"
"title": "Especificación de HTML CrossType en la salida HTML mediante programación en .NET"
"url": "/es/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Especificación de HTML CrossType en la salida HTML mediante programación en .NET

## Introducción
Al convertir archivos de Excel a HTML en aplicaciones .NET, es posible que necesite especificar cómo se gestionan las referencias cruzadas en la salida. La clase HtmlSaveOptions de Aspose.Cells para .NET ofrece varias opciones para controlar el proceso de conversión, y una de ellas es HtmlCrossType. En este tutorial, explicaremos cómo especificar programáticamente el tipo de referencia cruzada de HTML al exportar archivos de Excel a formato HTML. 
## Prerrequisitos
Antes de sumergirse en el código, asegúrese de tener lo siguiente:
- Aspose.Cells para .NET: Asegúrese de tener la biblioteca Aspose.Cells instalada en su proyecto. Puede descargarla desde [Sitio web de Aspose](https://releases.aspose.com/cells/net/).
- Visual Studio: una instalación funcional de Visual Studio o cualquier otro entorno de desarrollo .NET.
- Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a comprender mejor los ejemplos.
- Archivo de Excel de muestra: Tenga listo un archivo de Excel de muestra para trabajar con él. Para este ejemplo, usaremos `sampleHtmlCrossStringType.xlsx`.
## Importar paquetes
Para empezar, deberá importar los espacios de nombres Aspose.Cells necesarios. A continuación, le explicamos cómo hacerlo:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Vamos a desglosarlo paso a paso para que le resulte fácil seguirlo e implementar esta funcionalidad en sus propios proyectos.
## Paso 1: Defina sus directorios de origen y salida
Primero, debe configurar los directorios para el archivo Excel de origen y dónde desea guardar el archivo HTML de salida.
```csharp
// Directorio de origen
string sourceDir = "Your Document Directory";
// Directorio de salida
string outputDir = "Your Document Directory";
```
## Paso 2: Cargue el archivo Excel de muestra
A continuación, cargue el archivo Excel de muestra en un `Workbook` objeto. Aquí es donde comienza toda la magia.
```csharp
// Cargue el archivo Excel de muestra
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
Aquí, reemplace `"Your Document Directory"` Con la ruta real donde se encuentra su archivo de Excel. Esta línea lee el archivo de Excel en memoria para que pueda manipularlo.
## Paso 3: Especificar las opciones de guardado de HTML
Ahora, crearemos una instancia de `HtmlSaveOptions`, que le permite configurar cómo se convertirá el archivo Excel a HTML.
```csharp
// Especificar tipo cruzado de HTML
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
En este paso, hemos establecido el `HtmlCrossStringType` a `HtmlCrossType.Default`, que es una de las opciones disponibles para manejar referencias cruzadas en el HTML de salida.
## Paso 4: Cambie el tipo de cruz según sea necesario
Puede especificar diferentes tipos para `HtmlCrossStringType` Según sus necesidades. Estas son las distintas opciones que puede utilizar:
- `HtmlCrossType.Default`:El tipo de cruz predeterminado.
- `HtmlCrossType.MSExport`:Exporta el HTML con un comportamiento similar a MS Excel.
- `HtmlCrossType.Cross`:Crea referencias cruzadas.
- `HtmlCrossType.FitToCell`:Ajusta las referencias cruzadas a las dimensiones de la celda.
Puedes modificar el `HtmlCrossStringType` como esto:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExpot;
// o 
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// or
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Paso 5: Guardar el archivo HTML de salida
Una vez configuradas las opciones, es hora de guardar el archivo HTML convertido. Utilice el `Save` método en tu `Workbook` objeto:
```csharp
// Salida HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
Aquí, nombramos el archivo de salida en función de `HtmlCrossStringType` Hemos configurado. De esta manera, podrá identificar fácilmente qué tipo de cruz se utilizó en la conversión.
## Paso 6: Confirmar la ejecución exitosa
Por último, siempre es recomendable confirmar que la operación se realizó correctamente. Puede imprimir un mensaje en la consola:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Esto le permitirá saber que el proceso se ha completado sin ningún error.
## Conclusión
¡Listo! Has especificado correctamente el tipo de HTML para tu exportación de Excel en .NET usando Aspose.Cells. Esta función es especialmente útil cuando necesitas mantener un formato o referencias específicas en tu salida HTML, garantizando así que los documentos convertidos cumplan con tus requisitos.
## Preguntas frecuentes
### ¿Qué es HtmlCrossType en Aspose.Cells?  
HtmlCrossType define cómo se gestionan las referencias cruzadas en el archivo de Excel durante la conversión a HTML. Puede elegir opciones como Predeterminado, MSExport, Cruzado y Ajustar a celda.
### ¿Puedo utilizar Aspose.Cells gratis?  
Aspose.Cells ofrece una versión de prueba gratuita. Puedes descargarla desde su sitio web. [sitio web](https://releases.aspose.com/).
### ¿Cómo instalo Aspose.Cells en mi proyecto .NET?  
Puede instalar Aspose.Cells a través del Administrador de paquetes NuGet en Visual Studio ejecutando el comando: `Install-Package Aspose.Cells`.
### ¿Dónde puedo encontrar la documentación de Aspose.Cells?  
Puede encontrar documentación completa en Aspose.Cells [aquí](https://reference.aspose.com/cells/net/).
### ¿Qué debo hacer si encuentro un error al guardar el archivo HTML?  
Asegúrese de que las rutas de directorio sean correctas y de tener permisos de escritura en el directorio de salida. Si el problema persiste, consulte el foro de soporte de Aspose para obtener ayuda.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}