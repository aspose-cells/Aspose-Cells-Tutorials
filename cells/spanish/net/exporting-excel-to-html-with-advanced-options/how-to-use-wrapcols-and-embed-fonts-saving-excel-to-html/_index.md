---
category: general
date: 2026-10-20
description: Aprenda cómo usar wrapcols en Aspose.Cells, incruste fuentes en HTML
  y guarde Excel como HTML con un ejemplo completo en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: es
lastmod: 2026-10-20
og_description: Cómo usar wrapcols en Aspose.Cells, incrustar fuentes en HTML y convertir
  un libro de trabajo a HTML con una guía clara en C# para desarrolladores.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Cómo usar wrapcols e incrustar fuentes al exportar Excel a HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Cómo usar wrapcols e incrustar fuentes al guardar Excel en HTML
url: /es/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar wrapcols e incrustar fuentes al guardar Excel como HTML

Si necesitas **cómo usar wrapcols** en una fórmula de Aspose.Cells, esta guía te muestra los pasos exactos. También aprenderás a **incrustar fuentes en HTML** y a **guardar Excel como HTML** para que la salida se vea idéntica en todos los navegadores.  

El tutorial cubre tres escenarios prácticos: usar la función `WRAPCOLS`, exportar un libro de trabajo con fuentes incrustadas y generar un informe maestro‑detalle con Smart Markers. Al final tendrás un programa C# único y ejecutable que demuestra todas estas funciones.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 (or later) installed.
* Aspose.Cells for .NET added to your project (`dotnet add package Aspose.Cells`).
* Basic familiarity with C# and Excel formulas.

No additional third‑party libraries are required; Aspose.Cells handles HTML conversion and font embedding internally.

## Paso 1: Demostrar la función **cómo usar wrapcols** en una fórmula

La función `WRAPCOLS` divide un rango unidimensional en una matriz bidimensional, llenando primero las columnas. Esto es útil cuando necesitas reorganizar datos para informes o gráficos.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Por qué esto funciona:**  
`WRAPCOLS` toma dos argumentos – el rango de origen y el número de columnas. La función llena la matriz por columnas, descartando cualquier valor excedente (el `3` en el ejemplo). El resultado aparece en la celda superior‑izquierda del rango de destino (`B1`), y puedes expandir el rango manualmente si necesitas la matriz completa.

> **Consejo profesional:** Después de establecer la fórmula, llama a `workbook.CalculateFormula()` para asegurarte de que el resultado esté actualizado antes de leer los valores de las celdas.

## Paso 2: **Convertir el libro de trabajo a HTML** y **incrustar fuentes en html**

Al exportar un archivo Excel a HTML, los navegadores suelen sustituir las fuentes por sus valores predeterminados, lo que puede romper el diseño visual. Aspose.Cells te permite incrustar las fuentes exactas usadas en el libro de trabajo directamente en el archivo HTML.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Por qué incrustar fuentes es importante:**  
Cuando `EmbedFonts` es `true`, Aspose.Cells convierte cada fuente TrueType/OpenType utilizada en una regla `@font-face` codificada en Base64 dentro del HTML generado. Esto elimina la necesidad de que la máquina cliente tenga instaladas las mismas fuentes, garantizando una representación pixel‑perfecta.

> **Caso límite:** Si el libro de trabajo de origen hace referencia a una fuente que no está instalada en el servidor, Aspose.Cells recurrirá a una fuente predeterminada y emitirá una advertencia. Asegúrate de que las fuentes requeridas estén disponibles


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Embed Fonts in HTML – Convert Excel to HTML with C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [How to Convert Excel Files to HTML Using Aspose.Cells for .NET: Hiding Overlaid Content](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}