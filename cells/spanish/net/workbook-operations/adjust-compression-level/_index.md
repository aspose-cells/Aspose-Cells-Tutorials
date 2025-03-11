---
title: Ajustar el nivel de compresión en el libro de trabajo
linktitle: Ajustar el nivel de compresión en el libro de trabajo
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a ajustar el nivel de compresión de los libros de Excel con Aspose.Cells para .NET con esta guía paso a paso. Optimice la gestión de archivos.
weight: 14
url: /es/net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajustar el nivel de compresión en el libro de trabajo

## Introducción
Cuando se trata de administrar archivos grandes de Excel, la compresión es un factor decisivo. No solo ahorra espacio de almacenamiento, sino que también hace que las transferencias de archivos sean más rápidas y eficientes. Si trabaja con Aspose.Cells para .NET, puede ajustar fácilmente el nivel de compresión de sus libros de trabajo. En esta guía, lo guiaremos a través del proceso paso a paso, asegurándonos de que comprenda cada parte del código y cómo funciona.
## Prerrequisitos
Antes de sumergirnos en el código, hay algunos requisitos previos que debes tener en cuenta:
1. Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a comprender mejor los fragmentos de código.
2.  Biblioteca Aspose.Cells: Necesita tener instalada la biblioteca Aspose.Cells. Puede descargarla desde[aquí](https://releases.aspose.com/cells/net/).
3. Visual Studio: Será necesario un entorno de desarrollo como Visual Studio para ejecutar el código.
4. .NET Framework: asegúrese de que su proyecto esté configurado con una versión compatible de .NET Framework.
## Importar paquetes
Para comenzar, debe importar los paquetes necesarios en su proyecto de C#. A continuación, le indicamos cómo hacerlo:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
 Estos paquetes son esenciales para trabajar con archivos de Excel utilizando la biblioteca Aspose.Cells.`Aspose.Cells` El espacio de nombres contiene todas las clases que necesita para manipular archivos de Excel, mientras que`Aspose.Cells.Xlsb` Proporciona las opciones para guardar archivos en formato XLSB.
Ahora, desglosemos el proceso de ajuste del nivel de compresión en un libro de trabajo en pasos manejables.
## Paso 1: Definir los directorios de origen y salida
En primer lugar, debe especificar dónde se encuentran los archivos de origen y dónde desea guardar los archivos de salida. Esto es fundamental para garantizar que su programa sepa dónde encontrar los archivos con los que necesita trabajar.
```csharp
// Directorio de fuentes
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
 Reemplazar`"Your Document Directory"` con la ruta actual a sus directorios. Esto ayudará al programa a localizar los archivos que desea comprimir.
## Paso 2: Cargue el libro de trabajo
A continuación, cargará el libro de trabajo que desea comprimir. ¡Aquí es donde comienza la magia!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
En esta línea, creamos una nueva instancia de la`Workbook` Clase y carga un archivo Excel existente. Asegúrate de que el nombre del archivo coincida con el que tienes en el directorio de origen.
## Paso 3: Configurar las opciones de guardado
Ahora es el momento de configurar las opciones de guardado. Estableceremos el tipo de compresión para el archivo de salida. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
 El`XlsbSaveOptions` La clase le permite especificar varias opciones al guardar su libro de trabajo en formato XLSB, incluidos los niveles de compresión.
## Paso 4: Medir el tiempo de compresión para el nivel 1
Comencemos con el primer nivel de compresión. Mediremos cuánto tiempo lleva guardar el libro de trabajo con este nivel de compresión.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Aquí, configuramos el tipo de compresión en Nivel 1, guardamos el libro de trabajo y luego medimos el tiempo transcurrido. Esto nos da una idea de cuánto tiempo lleva el proceso.
## Paso 5: Medir el tiempo de compresión para el nivel 6
A continuación, veamos cómo funciona la compresión de nivel 6.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Este paso es similar al anterior, pero cambiamos el nivel de compresión al Nivel 6. Notarás que el tiempo necesario puede variar según la complejidad del libro de trabajo.
## Paso 6: Medir el tiempo de compresión para el nivel 9
Por último, veamos el rendimiento con el nivel de compresión más alto.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
En este paso, establecemos el nivel de compresión en Nivel 9. Aquí es donde normalmente verá la reducción más significativa en el tamaño del archivo, pero puede demorar más tiempo en procesarse.
## Paso 7: Salida final
Después de ejecutar todos los niveles de compresión, puede generar un mensaje indicando que el proceso se ha completado exitosamente.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Esta simple línea de código confirma que su programa ha terminado de ejecutarse sin problemas.
## Conclusión
Ajustar el nivel de compresión de los libros de trabajo con Aspose.Cells para .NET es un proceso sencillo que puede generar importantes beneficios en términos de tamaño de archivo y rendimiento. Si sigue los pasos que se describen en esta guía, podrá implementar fácilmente la compresión en sus aplicaciones y mejorar la eficiencia de la administración de archivos de Excel.
## Preguntas frecuentes
### ¿Qué es Aspose.Cells?  
Aspose.Cells es una potente biblioteca para .NET que permite a los desarrolladores crear, manipular y convertir archivos de Excel sin la necesidad de Microsoft Excel.
### ¿Cómo instalo Aspose.Cells?  
 Puede descargar e instalar Aspose.Cells desde[Sitio web de Aspose](https://releases.aspose.com/cells/net/).
### ¿Qué niveles de compresión están disponibles?  
Aspose.Cells admite múltiples niveles de compresión que van desde el Nivel 1 (compresión más baja) hasta el Nivel 9 (compresión más alta).
### ¿Puedo probar Aspose.Cells gratis?  
 ¡Sí! Puedes obtener una prueba gratuita de Aspose.Cells[aquí](https://releases.aspose.com/).
### ¿Dónde puedo encontrar soporte para Aspose.Cells?  
 Para cualquier consulta o ayuda, puede visitar el foro de soporte de Aspose[aquí](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
