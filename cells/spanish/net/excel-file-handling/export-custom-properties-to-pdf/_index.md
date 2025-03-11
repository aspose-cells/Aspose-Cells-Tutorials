---
title: Exportar propiedades personalizadas a PDF desde Excel
linktitle: Exportar propiedades personalizadas a PDF desde Excel
second_title: API de procesamiento de Excel Aspose.Cells .NET
description: Aprenda a exportar propiedades personalizadas de Excel a PDF con Aspose.Cells para .NET en esta guía paso a paso. Agilice el uso compartido de datos.
weight: 10
url: /es/net/excel-file-handling/export-custom-properties-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar propiedades personalizadas a PDF desde Excel

## Introducción
Al trabajar con archivos de Excel, a menudo nos encontramos con la necesidad de compartir datos en un formato universalmente aceptado, como PDF. Exportar propiedades personalizadas de archivos de Excel a PDF puede ser una tarea abrumadora si no se tienen las herramientas adecuadas. Ahí es donde entra en juego Aspose.Cells para .NET, que ofrece una solución sólida para que este proceso sea sencillo y eficiente. En este artículo, le explicaremos los pasos necesarios para exportar propiedades personalizadas de un archivo de Excel a formato PDF con Aspose.Cells para .NET. Al final de esta guía, tendrá todo el conocimiento necesario para abordar esta tarea.
## Prerrequisitos
Antes de profundizar en los detalles, repasemos algunos requisitos previos que necesitarás:
1. Entorno .NET: asegúrese de tener configurado un entorno de desarrollo .NET, como Visual Studio.
2.  Aspose.Cells para .NET: Descargue e instale la última versión de Aspose.Cells para .NET. Puede encontrarla[aquí](https://releases.aspose.com/cells/net/).
3. Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a seguir los ejemplos de código más fácilmente.
## Importar paquetes
Para comenzar, primero deberá importar los paquetes necesarios a su proyecto. A continuación, le indicamos cómo hacerlo:
### Crear un nuevo proyecto
1. Abra Visual Studio.
2. Haga clic en “Crear un nuevo proyecto”.
3. Seleccione “Aplicación de consola (.NET Framework)” o “Aplicación de consola (.NET Core)” según su preferencia y haga clic en “Siguiente”.
4. Ponle un nombre a tu proyecto y haz clic en “Crear”.
### Agregue Aspose.Cells a su proyecto
Para utilizar Aspose.Cells, debes agregarlo como referencia:
1. Haga clic derecho en el proyecto en el Explorador de soluciones.
2. Seleccione “Administrar paquetes NuGet”.
3. Busque “Aspose.Cells” e instale la última versión.
Ahora que tus paquetes están importados, estás listo para comenzar a codificar.

```csharp
using System.IO;
using System.Web;
using Aspose.Cells;
using System;
```

Ahora, pasemos a la parte crucial: la guía paso a paso para exportar propiedades personalizadas de un archivo de Excel a un documento PDF. ¡Abróchese el cinturón!
## Paso 1: Configura tus directorios
Antes de comenzar a codificar, debe definir los directorios de entrada y salida. Aquí es donde leerá el archivo Excel y donde se guardará el PDF generado.
```csharp
// Directorio de entrada
string sourceDir = "Your Document Directory";
// Directorio de salida
string outputDir = "Your Document Directory";
```
 En este fragmento de código, reemplace`"Your Document Directory"` con la ruta real donde se encuentran tus archivos o donde deseas guardarlos.
## Paso 2: Cargue el archivo Excel
 A continuación, deberá cargar el archivo de Excel que contiene las propiedades personalizadas. Esto se hace mediante el comando`Workbook` clase en Aspose.Cells.
```csharp
// Cargar archivo de Excel que contiene propiedades personalizadas
Workbook workbook = new Workbook(sourceDir + "sampleWithCustProps.xlsx");
```
 Aquí, asegúrese de que`sampleWithCustProps.xlsx` es el nombre de su documento de Excel y debe residir en el directorio especificado.
## Paso 3: Crear PdfSaveOptions
 Una vez cargado el libro de trabajo, es momento de configurar las opciones para guardar el PDF. Creará una instancia de`PdfSaveOptions` y establecer las propiedades adecuadas.
```csharp
// Cree una instancia de PdfSaveOptions y pase SaveFormat al constructor
Aspose.Cells.PdfSaveOptions pdfSaveOpt = new Aspose.Cells.PdfSaveOptions();
```
Esta línea inicia las opciones de guardado de PDF que personalizarás en breve.
## Paso 4: Configurar la exportación de propiedades personalizadas
Deberá especificar cómo se deben exportar las propiedades personalizadas. En este caso, utilizaremos el`Standard` Opción para exportar.
```csharp
// Establezca la propiedad CustomPropertiesExport en PdfCustomPropertiesExport.Standard
pdfSaveOpt.CustomPropertiesExport = Aspose.Cells.Rendering.PdfCustomPropertiesExport.Standard;
```
Al configurar esta propiedad, las propiedades personalizadas de su documento de Excel se incluirán en el PDF.
## Paso 5: Guarde el libro de trabajo como PDF
Ahora que todo está configurado, es momento de guardar su libro de trabajo como un archivo PDF utilizando las opciones definidas.
```csharp
// Guarde el libro de trabajo en formato PDF mientras pasa el objeto de PdfSaveOptions
workbook.Save(outputDir + "outSampleWithCustProps.pdf", pdfSaveOpt);
```
 En esta línea,`outSampleWithCustProps.pdf` será el nombre de su nuevo archivo PDF, así que asegúrese de que sea único para evitar sobrescrituras.
## Paso 6: Confirmar el éxito
Por último, confirmemos que la operación fue exitosa imprimiendo un mensaje en la consola:
```csharp
Console.WriteLine("ExportCustomPropertiesToPDF executed successfully.");
```
Este mensaje aparecerá en tu consola para avisarte que todo salió bien.
## Conclusión
¡Y ya está! Aprendió a exportar propiedades personalizadas de un archivo de Excel a un documento PDF con Aspose.Cells para .NET. Este enfoque no solo facilita el uso compartido de datos, sino que también garantiza que los metadatos personalizados que ingresó en sus archivos de Excel permanezcan intactos y accesibles en formato PDF. Ya sea que trabaje con documentación de proyectos, informes o resúmenes de datos, este método es una valiosa incorporación a su conjunto de herramientas. No dude en explorar la documentación de Aspose.Cells[aquí](https://reference.aspose.com/cells/net/) para funcionalidades aún más potentes.
## Preguntas frecuentes
### ¿Qué son las propiedades personalizadas en Excel?
Las propiedades personalizadas son campos de metadatos que puede asociar con un libro de Excel, como el nombre del autor, el título o datos personalizados específicos para sus necesidades.
### ¿Puedo exportar propiedades personalizadas en diferentes formatos?
Sí, además de PDF, otros formatos compatibles con Aspose.Cells también permiten exportar propiedades personalizadas, según sus necesidades.
### ¿Se requiere una licencia para Aspose.Cells?
Se requiere una licencia para uso comercial, pero también puedes probar el producto de forma gratuita inicialmente. Consulta la[licencia temporal](https://purchase.aspose.com/temporary-license/) Opciones.
### ¿Dónde puedo encontrar soporte para Aspose.Cells?
 Puede encontrar soporte de la comunidad y hacer preguntas en el foro de Aspose[aquí](https://forum.aspose.com/c/cells/9).
### ¿Puedo personalizar la salida PDF guardada?
 ¡Por supuesto!`PdfSaveOptions` La clase proporciona varias propiedades que permiten una personalización detallada de la salida PDF.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
