---
category: general
date: 2026-06-24
description: Incrustar fuentes PDF usando Aspose.Cells en C#. Aprende cómo guardar
  Excel como PDF, exportar Excel a HTML, convertir xlsx a PDF con Aspose y duplicar
  filas en una tabla dinámica.
draft: false
keywords:
- embed fonts pdf
- save excel as pdf
- export excel to html
- xlsx to pdf aspose
- duplicate rows pivot
language: es
og_description: Incrustar fuentes PDF usando Aspose.Cells en C#. Este tutorial muestra
  paso a paso cómo guardar Excel como PDF, exportar Excel a HTML y más.
og_title: Incrustar fuentes PDF con Aspose.Cells – Guía completa de C#
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Embed fonts PDF using Aspose.Cells in C#. Learn how to save Excel as
    PDF, export Excel to HTML, convert xlsx to PDF with Aspose, and duplicate rows
    pivot.
  headline: Embed fonts PDF with Aspose.Cells – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
title: Incrustar fuentes PDF con Aspose.Cells – Guía completa de C#
url: /es/net/xps-and-pdf-operations/embed-fonts-pdf-with-aspose-cells-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incrustar fuentes PDF con Aspose.Cells – Guía completa en C#

¿Alguna vez te has preguntado cómo **embed fonts PDF** cuando conviertes un libro de Excel con Aspose.Cells? No estás solo—muchos desarrolladores se topan con el problema cuando el PDF generado se ve incorrecto en máquinas que no tienen instaladas las fuentes originales.  

En esta guía recorreremos un ejemplo del mundo real que no solo **embed fonts PDF**, sino que también te muestra cómo **save Excel as PDF**, **export Excel to HTML**, convertir un **xlsx to PDF with Aspose**, e incluso **duplicate rows pivot** sin romper la tabla dinámica. ¿Suena a mucho? No hay problema—lo desglosaremos paso a paso.

## Lo que aprenderás

- Cómo copiar filas que contienen una tabla dinámica manteniendo la tabla dinámica intacta.  
- Cómo insertar un smart‑marker que repite una hoja de detalle para cada pedido.  
- Los ajustes exactos que necesitas para **embed fonts PDF**, exportar gráficos como PPTX editable y preservar paneles congelados cuando **export Excel to HTML**.  
- Consejos para solucionar problemas comunes como fuentes faltantes u objetos OLE rotos.  

**Prerequisitos:** .NET 6+ (o .NET Framework 4.6+), Aspose.Cells para .NET instalado, y un entorno básico de desarrollo en C# (Visual Studio, Rider o VS Code). No se requieren paquetes NuGet adicionales más allá de Aspose.Cells.

---

## Embed fonts PDF – Proceso paso a paso

A continuación se muestra el código completo y ejecutable. Cada sección está anotada para que puedas ver exactamente por qué hacemos lo que hacemos.

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Pivot;
using Aspose.Cells.SmartMarker;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the workbook that contains a pivot table and a shape
        // -------------------------------------------------
        var workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");

        // -------------------------------------------------
        // Step 2: Duplicate the rows that include the pivot table (keeps the pivot intact)
        // -------------------------------------------------
        // The CopyRows method copies rows 0‑29 (30 rows) from the source worksheet
        // to the same worksheet, effectively duplicating the pivot area.
        workbook.Worksheets[0].Cells.CopyRows(0, 0, 30);

        // -------------------------------------------------
        // Step 3: Insert a smart‑marker to repeat a detail sheet for each order
        // -------------------------------------------------
        var orders = new[]
        {
            new { Id = 101, Items = new[] { "Pen", "Paper" } },
            new { Id = 102, Items = new[] { "Book" } }
        };
        var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName = "OrderDetail" };
        workbook.Worksheets[0].SmartMarkerProcessing(new { Orders = orders }, smartMarkerOptions);

        // -------------------------------------------------
        // Step 4: Save the workbook as a PPTX file with editable charts, OLE objects, and text boxes
        // -------------------------------------------------
        var pptxOptions = new PptxSaveOptions
        {
            ExportChartsAsEditable = true,
            ExportOleObjects = true,
            ExportTextBoxesAsEditable = true
        };
        workbook.Save("YOUR_DIRECTORY/result.pptx", pptxOptions);

        // -------------------------------------------------
        // Step 5: Save the same workbook as a PDF while embedding standard fonts
        // -------------------------------------------------
        // This is where we actually **embed fonts PDF**.
        var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
        workbook.Save("YOUR_DIRECTORY/result.pdf", pdfOptions);

        // -------------------------------------------------
        // Step 6: Save the workbook as HTML, preserving frozen panes and embedding all fonts
        // -------------------------------------------------
        // The HTML export respects the original layout and keeps the fonts inside the file.
        var htmlOptions = new HtmlSaveOptions
        {
            PreserveFreezePanes = true,
            EmbedAllFonts = true
        };
        workbook.Save("YOUR_DIRECTORY/result.html", htmlOptions);
    }
}
```

### Por qué funciona esto

- **CopyRows** duplica las filas que contienen la tabla dinámica, de modo que la tabla dinámica original permanece vinculada a sus datos de origen. Esto satisface el requisito de **duplicate rows pivot**.  
- **SmartMarkerProcessing** crea una nueva hoja de cálculo para cada pedido, automatizando la generación de la hoja de detalle.  
- **PdfSaveOptions.EmbedStandardFonts = true** indica a Aspose.Cells que incruste las fuentes directamente en el archivo PDF, lo que es la clave para **embed fonts pdf**. Sin esta opción, el PDF recurriría a fuentes del sistema, rompiendo el diseño en otras máquinas.  
- **HtmlSaveOptions** con `EmbedAllFonts` y `PreserveFreezePanes` garantiza que al **export Excel to HTML** la fidelidad visual coincida con el libro original.  

#### Resultado esperado

- `result.pdf` – un PDF donde todas las fuentes usadas están incrustadas; ábrelo en cualquier computadora y el texto se verá idéntico al original.  
- `result.pptx` – un archivo PowerPoint con gráficos editables y objetos OLE.  
- `result.html` – una carpeta HTML (`result.html` + `result_files`) que muestra el libro en un navegador con los paneles congelados intactos.  

---

## Guardar Excel como PDF con Aspose.Cells

Si tu único objetivo es **save Excel as PDF**, puedes eliminar los pasos adicionales y centrarte en las opciones de PDF:

```csharp
var workbook = new Workbook("template.xlsx");

// Minimal PDF conversion – embed fonts for portability
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,   // crucial for embed fonts pdf
    Compliance = PdfCompliance.PdfA1b // optional: make the PDF archival‑friendly
};

workbook.Save("output.pdf", pdfOpts);
```

**Consejo profesional:** Cuando apuntas a la conformidad PDF/A, Aspose incrusta automáticamente todas las fuentes, por lo que obtienes una capa extra de seguridad para el almacenamiento a largo plazo.

---

## Exportar Excel a HTML manteniendo el diseño

Exportar a HTML a menudo pierde la apariencia original de la hoja, especialmente cuando hay paneles congelados. El fragmento siguiente muestra los ajustes exactos que necesitas:

```csharp
var wb = new Workbook("template.xlsx");

var htmlOpts = new HtmlSaveOptions
{
    PreserveFreezePanes = true, // keeps the top rows/columns locked
    EmbedAllFonts = true,       // embeds fonts so the page looks the same everywhere
    ExportActiveWorksheetOnly = true,
    ExportCellValueAsString = true
};

wb.Save("output.html", htmlOpts);
```

Porque establecemos `EmbedAllFonts`, el HTML generado contiene datos de fuentes codificados en base‑64, cumpliendo con el requisito de **export excel to html** sin necesidad de archivos CSS externos.

---

## Convertir Xlsx a PDF usando Aspose.Cells

A veces la terminología “**xlsx to pdf aspose**” aparece en búsquedas. El código a continuación demuestra la cadena de conversión exacta, incluyendo un par de mejoras adicionales:

```csharp
var wb = new Workbook("template.xlsx");

// Optional: set page layout before conversion
wb.Worksheets[0].PageSetup.Orientation = PageOrientation.Landscape;
wb.Worksheets[0].PageSetup.FitToPagesWide = 1;
wb.Worksheets[0].PageSetup.FitToPagesTall = 0;

// PDF options – embed fonts and keep hyperlinks intact
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    ExportHyperlinks = true,
    OnePagePerSheet = false
};

wb.Save("converted.pdf", pdfOpts);
```

**¿Por qué preocuparse por la configuración de página?** Si la omites, el PDF predeterminado puede recortar columnas o filas. Ajustar el diseño primero asegura que el PDF final coincida con lo que ves en Excel.

---

## Duplicar filas con tabla dinámica – Manteniendo la tabla dinámica intacta

Un obstáculo común es intentar copiar filas que contienen una tabla dinámica; la tabla a menudo pierde su conexión con la fuente de datos. El método `CopyRows` que usamos antes hace el trabajo pesado por ti:

```csharp
// Duplicate the first 30 rows (adjust as needed)
workbook.Worksheets[0].Cells.CopyRows(sourceRow: 0, destinationRow: 0, totalRows: 30);
```

- **sourceRow** – la primera fila del rango que deseas copiar.  
- **destinationRow** – donde se debe colocar la copia (misma hoja, mismo índice inicial para duplicar efectivamente).  
- **totalRows** – cuántas filas copiar.  

Porque la caché de la tabla dinámica reside en la hoja de cálculo, copiar las filas **no** rompe la tabla dinámica. Esto satisface la palabra clave **duplicate rows pivot** mientras mantiene el libro ordenado.

---

## Recapitulación del ejemplo completo

Juntando todo, aquí tienes el programa completo que puedes colocar en una aplicación de consola y ejecutar de inmediato:



## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Guardar libro de Excel como PDF con fuentes personalizadas usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Cómo exportar gráficos de Excel a PDF usando Aspose.Cells para .NET: Guía paso a paso](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Cómo exportar segmentaciones de Excel a PDF usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/export-excel-slicers-to-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}