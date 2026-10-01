---
category: general
date: 2026-10-01
description: Agrega un gráfico a Word con Aspose en solo minutos. Aprende a incrustar
  un gráfico de Excel en Word, exportar gráficos de Excel a Word, crear documentos
  Word con Aspose y guardar el gráfico en el documento Word.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: es
lastmod: 2026-10-01
og_description: Añade un gráfico a Word con Aspose en minutos. Esta guía muestra cómo
  incrustar un gráfico de Excel en Word, exportar el gráfico de Excel a Word, crear
  un documento Word con Aspose y guardar el gráfico en el documento Word.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Agregar gráfico a Word con Aspose – incrustar gráfico de Excel
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Cómo agregar un gráfico a Word con Aspose – incrustar gráfico de Excel
url: /es/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo agregar un gráfico a Word con Aspose – incrustar gráfico de Excel

Si necesitas **agregar un gráfico a Word** rápidamente, este tutorial te brinda una solución completa y lista para ejecutar. Verás cómo incrustar un gráfico de Excel en un archivo Word, exportar el gráfico de Excel a Word y, finalmente, **guardar el documento Word con el gráfico** con solo unas pocas líneas de C#.

Incrustar gráficos es un requisito común al generar informes, facturas o paneles de control de forma programática. Al final de esta guía podrás **crear documentos Word con Aspose** que contengan cualquier gráfico de un libro de Excel, sin necesidad de copiar y pegar manualmente.

## Requisitos previos

- .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+)
- Paquetes NuGet Aspose.Cells y Aspose.Words (instalar mediante `dotnet add package Aspose.Cells` y `dotnet add package Aspose.Words`)
- Un archivo Excel existente (`Chart.xlsx`) que contenga al menos un gráfico
- Un entorno de desarrollo como Visual Studio 2022 o VS Code

## Agregar un gráfico a Word con Aspose

A continuación se muestra el programa completo y autónomo. Cópialo en un nuevo proyecto de consola, restaura los paquetes y ejecútalo. El programa carga el libro de Excel, crea un documento Word, inserta el primer gráfico y guarda el resultado.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Por qué cada línea es importante

1. **Cargar el libro** – `Workbook` analiza el archivo Excel y te brinda acceso programático a sus hojas de cálculo y gráficos.  
2. **Crear el documento Word** – `Document` es el punto de entrada de Aspose.Words para cualquier tarea de procesamiento de Word.  
3. **DocumentBuilder** – Esta clase auxiliar te permite insertar contenido (texto, imágenes, gráficos) en la posición actual del cursor.  
4. **InsertChart** – La sobrecarga que acepta un objeto `Aspose.Cells.Chart` copia los datos, el formato y las series del gráfico directamente al archivo Word. No se requiere una conversión intermedia a imagen, preservando la calidad vectorial.  
5. **Save** – `Save` escribe el paquete .docx en disco, completando el paso de **guardar el documento Word con el gráfico**.

#### Resultado esperado

Después de ejecutar el programa, abre `Chart.docx`. Verás el mismo gráfico que estaba almacenado en `Chart.xlsx`, ubicado donde se colocó el builder (al inicio del documento). El gráfico sigue siendo totalmente editable dentro de Word (puedes cambiar su tamaño, colores o modificar la fuente de datos).

## Incrustar un gráfico de Excel en Word

Si necesitas incrustar más de un gráfico, repite la llamada a `InsertChart` para cada objeto de gráfico. Por ejemplo, para incrustar todos los gráficos de la primera hoja de cálculo:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**Consejo profesional:** Usa `builder.Writeln()` para insertar un salto de párrafo, asegurando que cada gráfico comience en una nueva línea.

## Exportar gráfico de Excel a Word – manejo de múltiples hojas de cálculo

Cuando los gráficos están distribuidos en varias hojas de cálculo, itera a través de la colección `Worksheets` del libro:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Este enfoque **exporta gráficos de Excel a Word** para cualquier diseño de libro, haciendo la solución robusta para informes complejos.

## Crear documento Word con Aspose – personalizar la apariencia

Puedes controlar el tamaño y la posición de cada gráfico insertado modificando el `Shape` devuelto por `InsertChart`:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

Ajustar `WrapType` a `Inline` asegura que el gráfico se comporte como un párrafo normal, lo cual suele ser deseable para la generación automática de documentos.

## Guardar documento Word con gráfico – mejores prácticas

- **Utiliza un nombre de archivo descriptivo** (`Report_Q1_2026.docx`) para facilitar la versionado.  
- **Libera los objetos** cuando termines, especialmente en procesos por lotes grandes:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Valida el resultado** programáticamente si generas muchos archivos:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| *¿Puedo insertar un gráfico que no sea el primero en la hoja?* | Sí. Accede a él por índice: `sheet.Charts[2]` para el tercer gráfico. |
| *¿Qué pasa si el gráfico de Excel usa una fuente de datos que no está en el libro?* | Aspose.Cells incrusta los datos directamente en el objeto del gráfico, por lo que el gráfico sigue funcionando incluso si se elimina el rango de origen. |
| *¿Necesito una licencia para Aspose?* | Una evaluación gratuita funciona, pero una versión con licencia elimina la marca de agua de evaluación y desbloquea todas las funciones. |
| *¿Será editable el gráfico en Word después de la inserción?* | El gráfico se inserta como un gráfico nativo de Word, por lo que los usuarios pueden editar series, títulos y estilos usando la interfaz de Word. |
| *¿Cómo insertar un gráfico como imagen en lugar de un gráfico nativo?* | Usa `builder.InsertImage(chart.ToImage())` para incrustar una imagen rasterizada. Esto es útil cuando deseas preservar la representación visual exacta sin la editabilidad a nivel de Word. |

## Ejemplo completo funcional (copiar‑pegar)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

Ejecutar el código genera un archivo Word (`ReportWithCharts.docx`) que contiene los resultados de **agregar gráfico a Word** para cada gráfico del libro de origen.

## Conclusión

Ahora sabes cómo **agregar un gráfico a Word** usando Aspose.Cells y Aspose.Words, cómo **incrustar un gráfico de Excel en Word**, **exportar gráficos de Excel a Word**, **crear documentos Word con Aspose**, y finalmente **guardar el documento Word con el gráfico**. El enfoque funciona tanto para escenarios de un solo gráfico como para libros complejos con muchos gráficos distribuidos en varias hojas.

Próximos pasos que podrías explorar:

- [Cómo guardar DOCX desde Excel – Guía completa para exportar gráficos a Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Crear libro de Excel con gráfico circular usando Aspose.Cells .NET - Guía completa](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Crear un gráfico de burbujas en Excel usando Aspose.Cells .NET: Guía paso a paso](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

Usa Aspose.Slides si lo necesitas

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}