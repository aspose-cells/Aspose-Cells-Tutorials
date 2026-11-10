---
category: general
date: 2026-10-26
description: Establecer el área de impresión y exportar una hoja de Excel a PNG en
  C#. Aprende las opciones de exportación de imágenes, cómo exportar a PNG y obtener
  una imagen imprimible de un libro de trabajo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: es
lastmod: 2026-10-26
og_description: Establece el área de impresión y exporta una hoja de Excel a PNG en
  C#. Este tutorial paso a paso cubre las opciones de exportación de imágenes y cómo
  exportar PNG desde un libro de trabajo.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Establecer el área de impresión y exportar la hoja de Excel a PNG – Guía
  de C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Establecer el área de impresión y exportar la hoja de Excel a PNG en C#
url: /es/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Establecer el área de impresión y exportar una hoja de Excel a PNG en C#

Si necesita **establecer el área de impresión** antes de exportar una hoja de Excel a PNG, esta guía le muestra cómo. Verá un ejemplo completo en C# que configura las opciones de exportación de imagen, ajusta el área de impresión de la hoja de cálculo y guarda el resultado como una imagen.

Exportar una hoja de Excel a PNG es un requisito frecuente cuando desea incrustar una captura de la hoja en un informe, correo electrónico o página web. El código a continuación funciona con cualquier libro que contenga una tabla dinámica, pero la técnica también se aplica a rangos de datos normales. No se requieren herramientas externas, solo la biblioteca Aspose.Cells para .NET.

## Prerrequisitos

- .NET 6.0 o posterior (el ejemplo está dirigido a .NET 6, pero cualquier versión reciente de .NET funciona)
- Aspose.Cells para .NET (instalar vía NuGet: `Install-Package Aspose.Cells`)
- Familiaridad básica con C# y conceptos de Excel como hojas de cálculo y áreas de impresión

## Paso 1: Configurar las opciones de exportación de imagen

Lo primero que hace es crear una instancia de `ImageOrPrintOptions`. Este objeto indica a Aspose.Cells cómo renderizar la hoja como una imagen.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Por qué es importante:** `ImageOrPrintOptions` controla el formato de salida, la resolución y otros detalles de renderizado. Usar PNG garantiza calidad sin pérdidas, lo que es ideal para informes que requieren texto y gráficos nítidos.

## Paso 2: Cargar el libro de trabajo y acceder a la hoja de cálculo objetivo

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Por qué es importante:** Debe trabajar con un objeto `Worksheet` específico porque el área de impresión es una configuración a nivel de hoja.

## Paso 3: Identificar el rango que desea imprimir

En muchos escenarios los datos que le interesan están dentro de una tabla dinámica. El siguiente código extrae el rango de datos de la primera tabla dinámica de la hoja.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Si su hoja no contiene una tabla dinámica, puede reemplazar `pivotDataRange` con cualquier `CellArea` que cree manualmente, por ejemplo:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Paso 4: **Establecer el área de impresión** para que coincida con el rango seleccionado

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Por qué es importante:** El área de impresión indica a Excel (y a Aspose.Cells) qué celdas incluir al renderizar la hoja como imagen. Al alinear el área de impresión con el rango de datos de la tabla dinámica, evita márgenes en blanco y asegura que el PNG exportado contenga solo los datos relevantes.

## Paso 5: Exportar la hoja de cálculo a una imagen PNG

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Por qué es importante:** `worksheet.ToImage` respeta el área de impresión establecida previamente, por lo que el archivo PNG contiene exactamente las celdas que definió. Asignar la imagen a una forma de picture le permite incrustarla nuevamente en el libro si lo necesita, mientras que guardarla en disco le brinda un archivo independiente.

## Ejemplo completo en funcionamiento

Unir todos los pasos produce un programa autocontenido que puede ejecutar de inmediato.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Resultado esperado

Al ejecutar el programa se crea `C:\Temp\WorksheetExport.png`. Al abrir el archivo se muestra una imagen PNG nítida que contiene solo las celdas definidas por el **área de impresión establecida** (los datos de la tabla dinámica en este ejemplo). La imagen puede insertarse en documentos Word, diapositivas PowerPoint o páginas web sin pasos de conversión adicionales.

## Manejo de múltiples hojas de cálculo o tablas dinámicas

- **Múltiples hojas:** Recorrer `wb.Worksheets` y repetir los pasos 3‑5 para cada hoja que necesite exportar.
- **Múltiples tablas dinámicas:** Seleccionar el `PivotTables[index]` apropiado o iterar sobre `worksheet.PivotTables` para exportar cada tabla individualmente.
- **Sin tabla dinámica:** Crear un `CellArea` manualmente (ver el comentario en el Paso 3) y asignarlo a `PrintArea`.

## Consejos prácticos (E‑E‑A‑T)

- **Consejo profesional:** Establezca `HorizontalResolution` y `VerticalResolution` a 300 DPI para PNG listos para impresión; valores más bajos reducen el tamaño del archivo para uso web.
- **Cuidado con las formas de picture vacías:** Si la hoja no tiene formas de picture, añada una antes de asignar la imagen:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Rendimiento:** Reutilizar una única instancia de `ImageOrPrintOptions` para varias hojas evita asignaciones innecesarias.
- **Compatibilidad:** Aspose.Cells 23.9+ soporta completamente .NET 6 y versiones posteriores; versiones anteriores pueden requerir ajustes en los nombres de la API.

## Conclusión

Ahora sabe cómo **establecer el área de impresión** y exportar una hoja de Excel a PNG.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [How to export Excel to PNG – full step‑by‑step guide](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [How to export excel range as image with C# and Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sheet to png – Export a Pivot Table as PNG in C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}