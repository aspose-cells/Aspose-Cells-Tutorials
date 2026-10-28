---
category: general
date: 2026-09-11
description: Copiar tabla dinámica y exportar Excel a PPTX usando Aspose.Cells. Aprende
  a generar PPTX editable y guardar el libro de trabajo como PPTX en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: es
lastmod: 2026-09-11
og_description: Copiar tabla dinámica y exportar Excel a PPTX en C# usando Aspose.Cells.
  Generar PPTX editable y guardar el libro como PPTX con unas pocas líneas de código.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Copiar tabla dinámica y exportar Excel a PPTX – guía completa de C#
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Copiar tabla dinámica y exportar Excel a PPTX con Aspose.Cells
url: /es/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar tabla dinámica y exportar Excel a PPTX con Aspose.Cells

Si necesitas copiar una tabla dinámica de una hoja a otra y luego exportar el archivo Excel a una presentación PowerPoint, esta guía te muestra cómo hacerlo. Con Aspose.Cells puedes generar un PPTX editable y guardar el libro como PPTX en solo unas pocas líneas de código C#.

El tutorial cubre cada paso necesario para mover una tabla dinámica, preservar su funcionalidad y producir un archivo PPTX donde el gráfico y las formas siguen siendo editables. No se requieren herramientas externas, solo la biblioteca Aspose.Cells y un entorno de desarrollo .NET.

## Lo que lograrás

* **Copiar tabla dinámica** de una hoja origen a una hoja destino manteniendo todas las conexiones de datos intactas.  
* **Exportar Excel a PPTX** para que la diapositiva resultante pueda editarse en PowerPoint.  
* **Generar PPTX editable** donde los gráficos, tablas y formas no se aplanan en imágenes.  
* **Guardar el libro como PPTX** usando la misma llamada API de Aspose.Cells.  

### Requisitos previos

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.6+).  
* Aspose.Cells para .NET (paquete NuGet `Aspose.Cells`).  
* Conocimientos básicos de aplicaciones de consola en C#.  

> **Consejo:** Instala el paquete NuGet vía CLI para garantizar que tienes la última versión:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Cómo copiar tabla dinámica entre hojas de cálculo

La primera operación es mover la tabla dinámica mientras se preserva su definición. Aspose.Cells proporciona un método `CopyRange` con un objeto `CopyOptions` que incluye la bandera `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Por qué funciona:**  
`CopyRange` copia datos de celdas, formato y, cuando `CopyPivotTable` es verdadero, la caché y los metadatos de la tabla dinámica. El rango de destino comienza en la celda `A1` (fila 0, columna 0) pero puedes cambiar los desplazamientos para colocar la tabla dinámica en otro lugar.

**Caso límite común:** Si la hoja destino ya contiene una tabla dinámica con el mismo nombre, Aspose.Cells renombrará automáticamente la que se está importando, evitando un conflicto de nombres.

## Exportar Excel a PPTX y generar PPTX editable

Una vez que la tabla dinámica está en su lugar, puedes exportar todo el libro a un archivo PPTX. La clase `ImageOrPrintOptions` permite especificar `ExportImageFormat = ImageFormat.Pptx`, lo que indica a Aspose.Cells que trate la salida como una presentación PowerPoint en lugar de una imagen rasterizada.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Por qué funciona:**  
Cuando `ExportImageFormat` se establece en `Pptx`, Aspose.Cells traduce cada hoja de cálculo en una diapositiva. Las formas, gráficos y tablas dinámicas se escriben como objetos nativos de PowerPoint, de modo que puedes hacer doble clic en ellos en PowerPoint y editar los datos subyacentes.

**Consejo para libros grandes:** Si solo necesitas un subconjunto de hojas, usa `workbook.Worksheets.RemoveAt(index)` para eliminar las hojas que no deseas exportar antes de llamar a `Save`. Esto reduce el tamaño del archivo PPTX.

## Ejemplo completo y ejecutable

A continuación se muestra el programa completo que une los pasos anteriores. Reemplaza `YOUR_DIRECTORY` con la ruta real en tu máquina.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Salida esperada

Al ejecutar el programa se imprime:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Cuando abras `output.pptx` en Microsoft PowerPoint, verás una diapositiva que contiene la tabla dinámica copiada como un gráfico editable. Al hacer doble clic en el gráfico se abre el editor de gráficos de PowerPoint, permitiéndote modificar series, ejes y etiquetas de datos sin volver a Excel.

## Manejo de problemas típicos

| Problema | Causa | Solución |
|----------|-------|----------|
| La tabla dinámica aparece como una imagen estática | Falta la bandera `CopyPivotTable` o `ExportImageFormat` configurado a `Png` | Asegúrate de que `CopyPivotTable = true` y `ExportImageFormat = ImageFormat.Pptx`. |
| La hoja destino muestra celdas en blanco | El rango de origen no cubre toda el área de la tabla dinámica | Amplía el rango (p. ej., `"A1:H30"`) para incluir todos los campos de la tabla dinámica. |
| El PPTX exportado es muy grande | Se incluyen hojas de cálculo innecesarias | Elimina las hojas no deseadas antes de llamar a `Save`. |
| PowerPoint no puede editar el gráfico | Se está usando una versión antigua de Aspose.Cells que no soporta PPTX | Actualiza a la última versión de Aspose.Cells (consulta las notas de la versión). |

## Próximos pasos y temas relacionados

* **Exportar hoja de Excel a PPTX con diseños de diapositiva personalizados** – explora `WorksheetToPdfConverter` para un control más fino sobre la apariencia de la diapositiva.  
* **Exportar Excel a PDF** – reemplaza `ImageFormat.Pptx` por `ImageFormat.Pdf` para generar un PDF en su lugar.  
* **Modificar programáticamente el PPTX después de la exportación** – usa la biblioteca `Aspose.Slides` para añadir animaciones o notas del presentador.  

Al dominar **copiar tabla dinámica**, **exportar excel a pptx** y **generar pptx editable**, puedes crear pipelines de informes de extremo a extremo que trasladan datos de hojas de cálculo directamente a presentaciones sin perder la capacidad de edición.

---


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}