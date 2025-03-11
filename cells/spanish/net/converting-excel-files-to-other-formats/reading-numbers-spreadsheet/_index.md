---
title: Hoja de cálculo para leer números mediante programación en .NET
linktitle: Hoja de cálculo para leer números mediante programación en .NET
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a leer hojas de cálculo de Numbers y convertirlas a PDF usando Aspose.Cells para .NET en este tutorial detallado.
weight: 18
url: /es/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoja de cálculo para leer números mediante programación en .NET

## Introducción
En el mundo digital actual, la gestión de datos es una habilidad vital y las hojas de cálculo están a la vanguardia de la organización de datos. Pero, ¿qué sucede si necesita trabajar con una hoja de cálculo de Numbers (esos archivos creados por la aplicación Numbers de Apple) mediante .NET? No se preocupe, ¡no está solo! En este tutorial, le explicaremos el proceso de lectura de una hoja de cálculo de Numbers mediante programación con Aspose.Cells para .NET. Aprenderá a cargar un archivo de Numbers y convertirlo a PDF.
## Prerrequisitos
Antes de comenzar, hay algunas cosas que debes tener en cuenta:
1. Aspose.Cells para .NET: Asegúrate de tener instalada la biblioteca Aspose.Cells. Puedes descargarla[aquí](https://releases.aspose.com/cells/net/).
2. Visual Studio: se recomienda tener Visual Studio (o cualquier otro IDE compatible con .NET) instalado en su máquina.
3. Conocimientos básicos de C#: un poco de familiaridad con la programación en C# le ayudará a seguir el proceso sin problemas.
4. Su directorio de documentos: necesitará un directorio donde esté almacenado su archivo Numbers, junto con una ubicación para guardar el PDF convertido.
Una vez que hayas cubierto estos requisitos previos, ¡estarás listo para comenzar!
## Importar paquetes
Para comenzar, debemos importar los paquetes necesarios a nuestro proyecto de C#. Este es un paso crucial porque nos permite aprovechar las funcionalidades que ofrece la biblioteca Aspose.Cells.
1. Abra su proyecto C# en Visual Studio.
2. Agregue una referencia a la biblioteca Aspose.Cells:
   - Si está utilizando NuGet, simplemente ejecute el siguiente comando en la consola del administrador de paquetes:
```
 Install-Package Aspose.Cells
 ```
3. Importa los espacios de nombres necesarios en tu código:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ahora que hemos importado los paquetes necesarios, pasemos a la guía paso a paso para leer una hoja de cálculo de Numbers.
## Paso 1: Especifique los directorios de origen y salida
En este paso, configuraremos los directorios donde se encuentra el archivo Numbers de origen y donde desea guardar el PDF de salida.
```csharp
// Directorio de fuentes
string sourceDir = "Your Document Directory"; // Actualice esto a su directorio actual
// Directorio de salida
string outputDir = "Your Document Directory"; // Actualice esto a su directorio actual
```
 Aquí, estamos definiendo dos variables de cadena,`sourceDir` y`outputDir` , para especificar las ubicaciones de los archivos de entrada y salida. Asegúrese de reemplazar`"Your Document Directory"` con las rutas reales de su sistema.
## Paso 2: Configurar las opciones de carga para el formato de números
A continuación, especificaremos las opciones de carga para leer una hoja de cálculo de Numbers. Este paso es esencial, ya que le indica a Aspose cómo interpretar el archivo de Numbers.
```csharp
// Especifique las opciones de carga; queremos cargar la hoja de cálculo de Numbers
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
 Creamos una`LoadOptions` objeto y especifique el formato como`LoadFormat.Numbers`Esto le dice a la biblioteca Aspose.Cells que estamos trabajando con un archivo Numbers. 
## Paso 3: Cargue la hoja de cálculo de números en un libro de trabajo
Ahora, es el momento de cargar la hoja de cálculo de Numbers real en un`Workbook` objeto.
```csharp
// Cargue la hoja de cálculo de Numbers en el libro de trabajo con las opciones de carga anteriores
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
 Instanciábamos una`Workbook` objeto y pasar la ruta del archivo Numbers junto con nuestras opciones de carga. Asegúrese de que el nombre del archivo (`sampleNumbersByAppleInc.numbers`) coincide con el nombre real de su archivo Numbers.
## Paso 4: Guarde el libro de trabajo como PDF
Una vez que el archivo Numbers se haya cargado correctamente, el siguiente paso es guardarlo en un formato diferente, específicamente, PDF.
```csharp
// Guardar el libro de trabajo en formato PDF
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
 Aquí, llamamos al`Save` método en el`Workbook` objeto, especificando la ruta del archivo de salida y el formato en el que queremos guardarlo. En este caso, lo guardaremos como PDF. Asegúrese de que el nombre del archivo de salida (`outputNumbersByAppleInc.pdf`) es único y no sobrescribe ningún archivo existente.
## Paso 5: Confirmar el éxito
Por último, agreguemos un mensaje para confirmar que nuestra operación fue exitosa.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Esta línea de código imprimirá un mensaje de éxito en la consola una vez que todo esté listo. Siempre es bueno recibir comentarios, ¿no?
## Conclusión
¡Y ya está! Ha leído correctamente una hoja de cálculo de Numbers y la ha convertido a PDF con Aspose.Cells para .NET. Esta potente biblioteca le permite manipular hojas de cálculo sin esfuerzo, lo que hace que sus tareas de gestión de datos sean muy sencillas. Ya sea que esté desarrollando aplicaciones o simplemente necesite manejar hojas de cálculo de manera más eficiente, Aspose.Cells es una herramienta fantástica para tener en su kit de herramientas.
## Preguntas frecuentes
### ¿Qué tipos de archivos puede leer Aspose.Cells?  
Aspose.Cells puede leer una variedad de formatos de archivos, incluidos archivos XLS, XLSX, CSV y Numbers. 
### ¿Puedo editar archivos Numbers usando Aspose.Cells?  
Sí, puedes leer, manipular y guardar archivos Numbers con Aspose.Cells.
### ¿Aspose.Cells es de uso gratuito?  
 Aspose.Cells ofrece una prueba gratuita, pero necesitará una licencia para un uso prolongado. Consulte los precios[aquí](https://purchase.aspose.com/buy).
### ¿Qué hago si encuentro un error al cargar un archivo de Numbers?  
 Asegúrese de que está utilizando las opciones de carga correctas y de que la ruta del archivo sea precisa. Para obtener más ayuda, visite el sitio web[Foro de soporte de Aspose](https://forum.aspose.com/c/cells/9).
### ¿Cómo puedo obtener una licencia temporal para Aspose.Cells?  
 Puede solicitar una licencia temporal[aquí](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
