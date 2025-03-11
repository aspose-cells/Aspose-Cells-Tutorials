---
title: Establecer la fuente predeterminada para las opciones de guardado de PDF
linktitle: Establecer la fuente predeterminada para las opciones de guardado de PDF
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a configurar fuentes predeterminadas para las opciones de guardado de PDF usando Aspose.Cells para .NET, garantizando que sus documentos se vean perfectos en todo momento.
weight: 11
url: /es/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Establecer la fuente predeterminada para las opciones de guardado de PDF

## Introducción
Cuando se trata de generar informes, facturas o cualquier otro documento en formato PDF, es fundamental garantizar que el contenido tenga el aspecto adecuado. Las fuentes desempeñan un papel fundamental para mantener el atractivo visual y la legibilidad de los documentos. Sin embargo, ¿qué sucede cuando la fuente que utilizó en su archivo de Excel no está disponible en el sistema en el que está generando el PDF? Ahí es donde Aspose.Cells para .NET resulta útil. Esta potente biblioteca le permite establecer fuentes predeterminadas para sus opciones de guardado de PDF, lo que garantiza que sus documentos tengan un aspecto profesional y uniforme, sin importar dónde se abran.
## Prerrequisitos
Antes de comenzar, asegúrese de tener lo siguiente:
1. Visual Studio: necesitará un entorno de desarrollo como Visual Studio para escribir y ejecutar su código.
2.  Aspose.Cells para .NET: Puede descargar la última versión desde[Este enlace](https://releases.aspose.com/cells/net/)Alternativamente, puede instalarlo a través del Administrador de paquetes NuGet en Visual Studio.
3. Conocimientos básicos de C#: comprender los conceptos básicos de C# le ayudará a seguir los ejemplos de código.
4. Archivo de Excel de muestra: tenga listo un archivo de Excel de muestra para probar. Puede crear uno con distintas fuentes y estilos para ver cómo Aspose.Cells maneja las fuentes faltantes.
## Importar paquetes
Antes de poder usar Aspose.Cells en su proyecto, debe importar los paquetes necesarios. A continuación, le indicamos cómo hacerlo:
1. Abra su proyecto: inicie Visual Studio y abra su proyecto existente o cree uno nuevo.
2. Agregar referencias: haga clic derecho en su proyecto en el Explorador de soluciones y seleccione "Administrar paquetes NuGet".
3. Instalar Aspose.Cells: Busque "Aspose.Cells" y haga clic en el botón "Instalar".
4. Agregue directivas de uso: en la parte superior de su archivo C#, incluya los siguientes espacios de nombres:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Paso 1: Configura tus directorios
Antes de trabajar con archivos, es importante definir los directorios de origen y de salida. Esto facilitará la localización del archivo de entrada de Excel y el guardado de los archivos de salida generados.
```csharp
// Directorio de fuentes
string sourceDir = "Your Document Directory";
// Directorio de salida
string outputDir = "Your Document Directory";
```
 Reemplazar`"Your Document Directory"` con la ruta real a sus directorios.
## Paso 2: Abra el archivo Excel
 Ahora que tenemos nuestros directorios configurados, abramos el archivo de Excel con el que desea trabajar.`Workbook` La clase en Aspose.Cells se utiliza para cargar el documento de Excel.
```csharp
// Abrir un archivo de Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Asegúrese de reemplazar el nombre del archivo con su nombre de archivo real.
## Paso 3: Configurar las opciones de representación de imágenes
 continuación, debemos configurar las opciones de renderizado para convertir nuestra hoja de Excel a un formato de imagen. Crearemos una instancia de`ImageOrPrintOptions`, especificando el tipo de imagen y la fuente predeterminada.
```csharp
// Representación en formato de archivo PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 En este fragmento de código, configuramos el`CheckWorkbookDefaultFont` propiedad a`false`, lo que significa que si falta alguna fuente, se utilizará en su lugar la fuente predeterminada especificada (“Times New Roman”).
## Paso 4: Renderizar la hoja como una imagen
 Ahora, vamos a representar la primera hoja del libro de trabajo como una imagen PNG. Usaremos el`SheetRender` clase para lograr esto.
```csharp
// Convertir la primera hoja de cálculo en una imagen
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Paso 5: Cambiar el tipo de imagen y renderizar a TIFF
 Si desea convertir la misma hoja a un formato de imagen diferente, como TIFF, simplemente puede cambiar el`ImageType` propiedad y repetir el proceso de renderizado.
```csharp
// Establecer en formato TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Paso 6: Configurar las opciones para guardar PDF
 A continuación, configuremos las opciones de guardado de PDF. Crearemos una instancia de`PdfSaveOptions`establezca la fuente predeterminada y especifique que queremos verificar si hay fuentes faltantes.
```csharp
// Configurar las opciones de guardado de PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Paso 7: Guarde el libro de trabajo como PDF
Con las opciones de guardado configuradas, es momento de guardar nuestro libro de Excel como un archivo PDF. 
```csharp
// Guardar el libro de trabajo en formato PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Paso 8: Confirmar la ejecución
Por último, es una buena práctica avisar al usuario de que el proceso se ha completado correctamente. Puedes lograrlo mediante un mensaje de consola sencillo.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Conclusión
Aspose.Cells ofrece una forma flexible y sólida de manejar las manipulaciones de archivos de Excel, lo que facilita a los desarrolladores la creación de documentos visualmente atractivos que mantienen su formato. Ya sea que esté trabajando en informes, documentos financieros o cualquier otra forma de presentación de datos, tener control sobre la representación de fuentes puede mejorar significativamente la calidad de sus resultados.
## Preguntas frecuentes
### ¿Qué es Aspose.Cells?
Aspose.Cells es una potente biblioteca .NET que permite a los desarrolladores manipular archivos de Excel sin necesidad de tener instalado Microsoft Excel. Admite varios formatos de archivo y ofrece funciones avanzadas para trabajar con hojas de cálculo.
### ¿Cómo puedo establecer una fuente predeterminada para mis archivos de Excel?
 Puede establecer una fuente predeterminada utilizando el`PdfSaveOptions` Clase y especifique el nombre de fuente deseado. Esto garantiza que, incluso si falta una fuente, su documento utilizará la fuente predeterminada que especificó.
### ¿Puedo convertir archivos de Excel a formatos distintos a PDF?
¡Por supuesto! Aspose.Cells te permite convertir archivos de Excel a varios formatos, incluidas imágenes (PNG, TIFF), HTML, CSV y más.
### ¿Aspose.Cells es de uso gratuito?
Aspose.Cells es un producto comercial, pero puedes probarlo gratis con una versión de prueba limitada. Para disfrutar de todas sus funciones, tendrás que comprar una licencia.
### ¿Dónde puedo encontrar soporte para Aspose.Cells?
 Puede encontrar soporte para Aspose.Cells visitando el sitio[Foro de Aspose](https://forum.aspose.com/c/cells/9), donde podrás hacer preguntas y compartir ideas con otros usuarios y desarrolladores.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
