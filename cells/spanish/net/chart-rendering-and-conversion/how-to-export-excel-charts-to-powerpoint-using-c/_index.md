---
category: general
date: 2026-10-26
description: Aprende a exportar gráficos de Excel a PowerPoint con C#. Conserva la
  editabilidad de las formas y guarda como PPTX en unas pocas líneas de código.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: es
lastmod: 2026-10-26
og_description: Exporta gráficos de Excel a PowerPoint con C#. Esta guía muestra cómo
  mantener las formas editables y guardar como PPTX usando Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Exportar gráficos de Excel a PowerPoint con C# – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Cómo exportar gráficos de Excel a PowerPoint usando C#
url: /es/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo exportar gráficos de Excel a PowerPoint usando C#

Si necesitas **exportar gráficos de Excel a PowerPoint**, esta guía te lleva paso a paso por una solución completa y lista‑para‑ejecutar. Ya sea que estés creando un panel de informes o automatizando presentaciones, verás cómo unas pocas líneas de código C# mantienen tus formas de gráfico totalmente editables después de la conversión.

En este tutorial aprenderás a:

* Cargar un libro de Excel existente que contenga gráficos.  
* (Opcionalmente) ajustar la configuración del libro antes de la conversión.  
* Guardar el libro como un archivo PowerPoint preservando la editabilidad de las formas.  

Todo esto se realiza con **Aspose.Cells for .NET**, una biblioteca que maneja la conversión de Excel a PowerPoint sin requerir Microsoft Office en el servidor.

## Lo que necesitarás

| Requisito | Razón |
|-------------|--------|
| .NET 6.0 o posterior | Entorno de ejecución moderno con todas las características del lenguaje |
| Visual Studio 2022 (o cualquier IDE) | Editor y depurador conveniente |
| **Aspose.Cells for .NET** paquete NuGet | Proporciona la clase `Workbook` y soporte `SaveFormat.Pptx` |
| Un archivo Excel (`ChartAndShapes.xlsx`) que contenga al menos un gráfico | Fuente de los gráficos que deseas exportar |

> **Consejo profesional:** Usa la versión gratuita **Aspose.Cells Evaluation** para probar el código; una clave de licencia elimina la marca de agua de evaluación.

```bash
dotnet add package Aspose.Cells
```

## Exportar gráficos de Excel a PowerPoint – flujo de trabajo completo

A continuación se muestra el código de extremo a extremo que realiza la exportación mientras **preserva la editabilidad de las formas**. Cada paso se explica en detalle.

### Paso 1: Cargar el libro de Excel

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*La clase `Workbook` representa todo el archivo Excel. Cargar el archivo lee todas las hojas de cálculo, gráficos y formas en memoria, lo cual es necesario para cualquier manipulación posterior.*

### Paso 2: (Opcional) Ajustar la configuración del libro

En la mayoría de los casos, la configuración predeterminada es suficiente para una exportación limpia. Sin embargo, si necesitas cambiar el modo de cálculo, la configuración de página o ocultar ciertas hojas, puedes hacerlo aquí.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Por qué es importante:** Ajustar la configuración antes de la conversión garantiza que las diapositivas generadas reflejen el estado exacto que deseas, especialmente cuando fórmulas u hojas ocultas podrían afectar los datos del gráfico.

### Paso 3: Guardar el libro como archivo PowerPoint

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*La constante `SaveFormat.Pptx` indica a Aspose.Cells que genere una presentación PowerPoint. Internamente, la biblioteca convierte cada gráfico de Excel en una forma de PowerPoint que sigue siendo totalmente editable en Microsoft PowerPoint.*

### Paso 4: Verificar el resultado

Abre `Shapes.pptx` en PowerPoint y:

1. Selecciona un gráfico en cualquier diapositiva.  
2. Haz clic derecho → **Edit Data**.  
3. Confirma que aparece la tabla de datos del gráfico y puedes modificar los valores.

Si el gráfico abre el panel **Edit Data**, la conversión se realizó con éxito y se preservó la **editabilidad de la forma**.

![Exportar gráficos de Excel a PowerPoint ejemplo](export-excel-charts-to-powerpoint.png){.img-fluid alt="Exportar gráficos de Excel a PowerPoint ejemplo"}

## Problemas comunes y cómo evitarlos

| Problema | Causa | Solución |
|-------|-------|-----|
| Los gráficos aparecen como imágenes estáticas | Uso de una versión antigua de Aspose.Cells que no admite la exportación PPTX | Actualiza a la última Aspose.Cells 23.x o posterior |
| Faltan datos en el gráfico de PowerPoint | El libro no está completamente calculado antes de la exportación | Llama a `workbook.CalculateFormula()` antes de `Save` |
| Las formas no son editables | Guardando con `SaveFormat.Xlsx` en lugar de `SaveFormat.Pptx` | Asegúrate de pasar `SaveFormat.Pptx` a `Workbook.Save` |
| Excepción de licencia en tiempo de ejecución | Versión de evaluación sin una licencia registrada | Registra tu licencia con `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Caso límite: Exportar varias hojas de cálculo con gráficos separados

Si tu archivo Excel contiene varias hojas de cálculo, cada una con su propio gráfico, Aspose.Cells crea automáticamente una diapositiva separada para cada gráfico. Puedes controlar el orden de las diapositivas reorganizando las hojas antes de la operación de guardado.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Consejo de rendimiento: Transmitir la salida en lugar de escribir en disco

Al generar archivos PowerPoint en una API web, evita archivos temporales escribiendo a un `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Ejemplo completo y ejecutable

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Salida esperada:** La consola muestra el mensaje de confirmación, y `Shapes.pptx` se abre en PowerPoint con cada gráfico de Excel apareciendo en su propia diapositiva. Seleccionar un gráfico te permite editar sus datos, confirmando que se mantiene la **editabilidad de la forma**.

## Recapitulación y próximos pasos

Ahora sabes cómo **exportar gráficos de Excel a PowerPoint** con C# manteniendo los gráficos totalmente editables. El núcleo de la solución es el método `Workbook.Save` con `SaveFormat.Pptx`, una característica de **Aspose.Cells export** que abstrae la compleja manipulación de Open XML.

Desde aquí podrías explorar:

* Añadir títulos o notas personalizadas a las diapositivas usando la API **Aspose.Slides**.  
* Convertir otros objetos de Excel (tablas, imágenes) junto con los gráficos.  
* Automatizar el procesamiento por lotes de varios libros en un servicio en segundo plano.

Siéntete libre de experimentar con la configuración opcional mostrada arriba, e integrar este patrón en tus flujos de informes para una generación de PowerPoint rápida y fiable.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Exportar gráfico de Excel a PowerPoint con C# – guía completa de Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [Cómo exportar Excel a PowerPoint con C# – Guía completa](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Cómo exportar formas de Excel a PowerPoint – Guía completa](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}