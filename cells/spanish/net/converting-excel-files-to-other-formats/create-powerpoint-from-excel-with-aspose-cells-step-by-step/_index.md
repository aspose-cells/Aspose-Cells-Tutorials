---
category: general
date: 2026-10-01
description: Crear PowerPoint a partir de Excel usando Aspose.Cells en C#. Exportar
  Excel a PowerPoint y convertir XLSX a PPTX rápidamente con un ejemplo de código
  completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: es
lastmod: 2026-10-01
og_description: Crea PowerPoint a partir de Excel usando Aspose.Cells en C#. Aprende
  a exportar Excel a PowerPoint y convertir XLSX a PPTX en unas pocas líneas de código.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Crear PowerPoint desde Excel con Aspose.Cells – guía rápida
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Crear PowerPoint a partir de Excel con Aspose.Cells – guía paso a paso
url: /es/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PowerPoint a partir de Excel con Aspose.Cells – guía paso a paso

Si necesita **crear PowerPoint a partir de Excel**, este tutorial le muestra cómo hacerlo con Aspose.Cells para .NET. Aprenderá a **exportar Excel a PowerPoint**, convertir un libro de trabajo XLSX en una presentación PPTX y personalizar las diapositivas resultantes sin salir de su proyecto C#.

La guía cubre todo lo que necesita para ejecutar el código en .NET 6 o posterior, incluyendo la configuración del proyecto, los paquetes NuGet requeridos y un ejemplo completo y ejecutable. Al final, tendrá un archivo PowerPoint que contiene el gráfico original de Excel exactamente como aparece en el libro.

## Lo que necesitará

| Requisito | Razón |
|---|---|
| .NET 6 SDK or newer | Proporciona el tiempo de ejecución para la aplicación de consola C# |
| Visual Studio 2022 (or any IDE) | Permite crear proyectos y depurar fácilmente |
| Aspose.Cells for .NET NuGet package | Proporciona la clase `Workbook` y las API de exportación |
| An Excel file (`.xlsx`) that contains at least one chart | Los datos de origen para la diapositiva de PowerPoint |

> **Consejo profesional:** Aspose.Cells funciona en Windows, Linux y macOS, por lo que puede ejecutar el mismo código en contenedores Docker o pipelines de CI.

## Paso 1: Crear un nuevo proyecto de consola y agregar Aspose.Cells

Abra una terminal (o la Consola del Administrador de paquetes de Visual Studio) y ejecute:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

El comando `dotnet add package` descarga la última versión estable de **Aspose.Cells**, que incluye el método `ExportPptx` utilizado más adelante.

## Paso 2: Agregar el libro de Excel fuente

Coloque el archivo Excel que desea convertir en la carpeta del proyecto. Para este tutorial usamos `ChartOle.xlsx`, que contiene un único gráfico en la primera hoja.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## Paso 3: Escribir el código que **crea PowerPoint a partir de Excel**

Abra `Program.cs` y reemplace su contenido con el siguiente código. El ejemplo muestra la operación de **exportación central** y también cómo manejar casos límite comunes, como archivos faltantes y tipos de gráfico no compatibles.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### Por qué funciona esto

* `Workbook` lee todo el archivo Excel, incluidos los gráficos incrustados, tablas y formato.  
* `ExportPptx` convierte la hoja de cálculo activa en una presentación PPTX. El método transforma automáticamente los gráficos de Excel en formas de PowerPoint, preservando la fidelidad visual.  
* El código envuelve la operación en un bloque `try/catch` para exponer errores como fallas de **convert XLSX to PPTX** causadas por archivos corruptos.

## Paso 4: Ejecutar el programa y verificar la salida

Ejecute la aplicación:

```bash
dotnet run
```

Debería ver el mensaje en la consola:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

Abra `Exported.pptx` en Microsoft PowerPoint o cualquier visor compatible. La primera diapositiva muestra el gráfico exactamente como apareció en `ChartOle.xlsx`. Esto confirma que ha **generado PowerPoint a partir de Excel** con éxito.

## Paso 5: Avanzado – exportar varias hojas de cálculo o diseños de diapositivas personalizados

El ejemplo básico exporta solo la primera hoja. En escenarios del mundo real puede necesitar:

* **Exportar varias hojas de cálculo** en diapositivas separadas.  
* **Controlar el tamaño de la diapositiva** o agregar un marcador de posición de título.  
* **Incluir hojas de cálculo ocultas** en la conversión.  

A continuación se muestra un fragmento conciso que itera sobre todas las hojas de cálculo y agrega cada una como una diapositiva separada:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **Nota:** El fragmento avanzado requiere la biblioteca **Aspose.Slides for .NET**. Si solo necesita la conversión simple de una hoja, la llamada `ExportPptx` anterior es suficiente.

## Problemas comunes y cómo evitarlos

| Problema | Causa | Solución |
|---|---|---|
| Diapositiva en blanco después de la exportación | La hoja no contiene objetos visibles | Asegúrese de que haya al menos un gráfico, tabla o forma antes de llamar a `ExportPptx`. |
| Fuentes faltantes en el PowerPoint | Fuente no instalada en la máquina donde se abre el PPTX | Incruste las fuentes requeridas en el libro de Excel o instálelas en el sistema de destino. |
| Escalado inesperado | Gráfico grande que supera las dimensiones de la diapositiva | Ajuste la propiedad `PageSetup.Zoom` de la hoja antes de la exportación. |
| `convert XLSX to PPTX` throws `NotSupportedException` | Tipo de gráfico no compatible con Aspose.Cells (p. ej., mapas 3‑D) | Reemplace el gráfico por un tipo compatible o exporte la hoja como imagen primero. |

Abordar estos casos límite garantiza un flujo de trabajo fiable de **export Excel to PowerPoint** en entornos de producción.

## Conclusión

Ahora sabe cómo **crear PowerPoint a partir de Excel** usando Aspose.Cells para .NET. El tutorial cubrió:

* Configuración del proyecto e instalación de NuGet
* Cargar un libro de Excel e invocar `ExportPptx`
* Ejecutar el código y confirmar el PPTX generado
* Ampliar la solución para manejar múltiples hojas y diseños personalizados
* Consejos prácticos para evitar problemas comunes de conversión

Con este conocimiento puede automatizar la generación de informes, crear pipelines de presentaciones o integrar la conversión de Excel a PowerPoint en cualquier aplicación C#. Experimente con diferentes tipos de gráficos, agregue títulos a las diapositivas o combine la exportación con Aspose.Slides para crear presentaciones con todas sus funcionalidades.

--- 

*¿Listo para explorar más? Consulte temas relacionados como **convert Excel to PDF**, **embed Excel data in Word**, o **use Aspose.Slides to programmatically edit PPTX files**.*

## ¿Qué debería aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Convertir Excel a PowerPoint con Aspose Cells .NET](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convertir Excel a PowerPoint con Aspose Cells .NET](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convertir Excel a PowerPoint con Aspose Cells .NET](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}