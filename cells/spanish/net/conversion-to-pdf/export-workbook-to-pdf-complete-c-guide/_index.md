---
category: general
date: 2026-02-26
description: Exportar el libro de trabajo a PDF con fuentes incrustadas y también
  exportar gráficos a PowerPoint en C#. Aprende a copiar la hoja de tabla dinámica
  y guardar el libro de trabajo como PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: es
og_description: Exporta el libro de trabajo a PDF con fuentes incrustadas y también
  exporta los gráficos a PowerPoint en C#. Sigue la guía paso a paso para copiar tablas
  dinámicas y guardarlas como PPTX.
og_title: Exportar libro de trabajo a PDF – Guía completa de C#
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Exportar libro de trabajo a PDF – Guía completa de C#
url: /es/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar libro de trabajo a PDF – Guía completa de C#

Exportar libro de trabajo a PDF es un requisito común cuando necesitas compartir informes con las partes interesadas que pueden no tener Excel instalado. En este tutorial también te mostraremos cómo **exportar gráficos a PowerPoint**, copiar una **hoja de tabla dinámica**, e incrustar fuentes para que el PDF se vea exactamente como tu diseño en pantalla.  

¿Alguna vez te has preguntado por qué algunos PDFs pierden el diseño original o por qué las diapositivas de PowerPoint terminan con formas faltantes? La respuesta suele estar en opciones ausentes durante el proceso de exportación. Al final de esta guía tendrás un único método reutilizable en C# que maneja todos esos puntos críticos—no más copiar‑pegar manual o ajustar configuraciones de exportación.

## Lo que aprenderás

- Cómo crear un libro de trabajo, agregar expresiones Smart Marker y procesarlas.  
- Cómo **copiar una hoja de tabla dinámica** sin romper la fuente de datos.  
- Cómo **exportar gráficos, formas y cuadros de texto** a una presentación de PowerPoint manteniéndolos editables.  
- Cómo **incrustar fuentes estándar** durante la exportación a PDF para una renderización consistente en cualquier máquina.  
- Cómo **guardar el libro de trabajo como PPTX** usando el enfoque `save workbook as pptx`.  

Todo esto funciona con las últimas bibliotecas Aspose.Cells y Aspose.Slides .NET (versión 23.11 al momento de escribir). Sin herramientas externas, sin scripts de post‑procesamiento—solo C# puro.

> **Pro tip:** Si ya estás usando Aspose en tu proyecto, puedes insertar los fragmentos de código tal cual; de lo contrario, agrega primero los paquetes NuGet `Aspose.Cells` y `Aspose.Slides`.

## Requisitos previos

- .NET 6.0 o posterior (el código también se ejecuta en .NET Framework 4.7.2).  
- Visual Studio 2022 (o cualquier IDE que prefieras).  
- Aspose.Cells .NET y Aspose.Slides .NET instalados vía NuGet.  
- Familiaridad básica con C# y conceptos de Excel como Smart Markers y PivotTables.

---

![Diagrama de exportar libro de trabajo a PDF](export-workbook-to-pdf.png "Flujo de trabajo de exportar libro de trabajo a PDF mostrando salidas PDF y PPTX")

## Exportar libro de trabajo a PDF – Implementación paso a paso

A continuación tienes el ejemplo completo, listo para ejecutar. Construye un libro de trabajo, inserta expresiones Smart Marker, las procesa, copia un rango de tabla dinámica y, finalmente, guarda tanto un PDF como un archivo PowerPoint.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Por qué funciona

1. **El procesamiento de Smart Marker** te permite poblar el libro de trabajo desde cualquier fuente de datos (JSON, DataTables, etc.) sin escribir bucles.  
2. **DetailSheetNewName** crea una hoja separada para cada departamento, dándote una pestaña limpia por departamento.  
3. **Copiar el rango** (`sourceRange.Copy`) duplica la tabla dinámica *incluyendo* su caché, de modo que la hoja copiada se comporta exactamente como la original.  
4. **PresentationOptions** con `ExportCharts`, `ExportShapes` y `ExportTextBoxes` indica a Aspose que renderice esos objetos como elementos nativos de PowerPoint, preservando su editabilidad.  
5. **PdfSaveOptions.EmbedStandardFonts** garantiza que el PDF se vea idéntico en máquinas que no tengan instaladas las fuentes originales.

El resultado son dos archivos—`FinalReport.pdf` y `FinalPresentation.pptx`—que pueden enviarse por correo, archivarse o mostrarse en cualquier visor sin perder fidelidad.

## Exportar gráficos a PowerPoint (Guardar libro de trabajo como PPTX)

Si tu informe contiene gráficos, probablemente querrás que sean editables en PowerPoint. La clase `PresentationOptions` es la clave. Aquí tienes un fragmento centrado que muestra solo la parte de exportación de gráficos:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**¿Qué ocurre bajo el capó?** Aspose traduce cada gráfico de Excel a un gráfico nativo de PowerPoint, preservando series, títulos de ejes y formato. Esto es mucho mejor que exportar el gráfico como una imagen estática, porque tu audiencia podrá ajustar los puntos de datos más tarde.

## Copiar hoja de tabla dinámica sin perder datos

Las tablas dinámicas suelen ser la parte más complicada de una exportación porque dependen de una caché oculta. El método simple `Copy` funciona porque Aspose copia tanto el rango visible **como** el objeto de caché subyacente.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Nota:** Si solo necesitas la tabla dinámica en una nueva hoja dentro del mismo libro de trabajo, el enfoque anterior `sourceRange.Copy` es más ligero y evita crear un libro de trabajo completamente nuevo.

## Incrustar fuentes para la exportación a PDF – Por qué es importante

Cuando abres un PDF en una máquina que no tiene las fuentes originales, el texto puede desplazarse, los saltos de línea cambiar o los caracteres desaparecer. Configurar `EmbedStandardFonts = true` indica a Aspose que incruste las fuentes más comunes (Arial, Times New Roman, etc.) directamente en el flujo del PDF.

Si utilizas fuentes personalizadas, cambia a `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Aquí tienes un ejemplo:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Ahora cada destinatario verá el mismo diseño exacto que diseñaste—sin sorpresas.

## Resumen del ejemplo completo

Uniendo todo, el programa completo (mostrado antes) realiza lo siguiente:

1. **Crea** un libro de trabajo con marcadores Smart Marker.  
2. **Procesa** los marcadores, generando una hoja de detalle con el nombre del departamento.  
3. **Copia** un rango que contiene una tabla dinámica a una nueva hoja, preservando su funcionalidad.  
4. **Exporta** el libro de trabajo a PowerPoint, manteniendo gráficos, formas y cuadros de texto editables.  
5. **Exporta** el mismo libro de trabajo a PDF mientras incrusta fuentes estándar para una renderización fiable.

Ejecuta el programa, abre los archivos generados y verás:

- **PDF**: Tablas nítidas, fuentes incrustadas y el mismo estilo visual que el origen de Excel.  
- **PowerPoint**: Gráficos editables que puedes hacer clic derecho → *Edit Data* en PowerPoint, y formas que permanecen totalmente manipulables.

---

## Preguntas frecuentes (FAQ)

**P: ¿Esto funciona con .NET Core?**  
Sí—Aspose.Cells y Aspose.Slides son multiplataforma. Solo apunta a .NET 6 o posterior y el mismo código se ejecuta en Windows, Linux o macOS.

**P: ¿Qué pasa si solo necesito exportar un subconjunto de hojas?**  
Usa `Workbook.Save` con `SaveOptions` que te permitan especificar `SheetNames`. Ejemplo: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**P: ¿Puedo encriptar el PDF?**  
Claro. Configura `PdfSaveOptions.EncryptionDetails` con una contraseña antes de llamar a `Save`.

**P: Mi tabla dinámica usa una fuente de datos externa—¿la copia romperá el vínculo?**  
La operación de copia incluye la caché, no la conexión externa. La tabla dinámica seguirá funcionando sin conexión, pero no se actualizará contra la fuente original. Si necesitas actualización en tiempo real, exporta los datos fuente junto con el libro de trabajo.

## Próximos pasos y temas relacionados

- **Dynamic Data Sources** – Aprende a alimentar JSON o un DataTable en Smart Markers para informes en tiempo real.  
- **Advanced PDF Styling** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}