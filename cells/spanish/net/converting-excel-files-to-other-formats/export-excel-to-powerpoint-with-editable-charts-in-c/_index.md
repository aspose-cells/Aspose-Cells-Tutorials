---
category: general
date: 2026-09-21
description: Exportar Excel a PowerPoint con gráficos editables usando Aspose.Cells.
  Sigue esta guía paso a paso para convertir una hoja de cálculo a PPTX manteniendo
  los gráficos editables.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: es
lastmod: 2026-09-21
og_description: Exporta Excel a PowerPoint con gráficos editables usando Aspose.Cells.
  Aprende cómo convertir una hoja de cálculo a PPTX manteniendo la editabilidad completa
  de los gráficos.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: Exportar Excel a PowerPoint con gráficos editables – tutorial de C#
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: Exportar Excel a PowerPoint con gráficos editables en C#
url: /es/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Excel a PowerPoint con gráficos editables en C#

Exportar Excel a PowerPoint con gráficos editables es un requisito común cuando necesitas reutilizar visualizaciones de hojas de cálculo en presentaciones. Esta guía te muestra cómo **exportar Excel a PowerPoint** manteniendo la editabilidad de los gráficos, usando Aspose.Cells para .NET.

Aprenderás a:

* Cargar un libro de trabajo existente que contenga gráficos y cuadros de texto.  
* Configurar las opciones de exportación PPTX para que los gráficos y formas permanezcan editables.  
* Convertir una hoja de cálculo específica a un archivo PowerPoint que pueda abrirse y editarse en Microsoft PowerPoint.

El tutorial asume que tienes conocimientos básicos de C# y una versión reciente de .NET (≥ .NET 6). No se requiere experiencia previa con Aspose.Cells.

---

## Exportar Excel a PowerPoint – visión general

La idea central detrás de **export Excel to PowerPoint** es tratar cada hoja de cálculo como una fuente de imagen que puede renderizarse en una diapositiva PPTX. Al alternar las banderas `ExportChartAsEditableText` y `ExportShapeAsEditableText`, Aspose.Cells escribe los datos subyacentes del gráfico como objetos de dibujo de PowerPoint en lugar de un mapa de bits plano. Esto hace que la diapositiva resultante sea totalmente editable—igual que un gráfico creado directamente en PowerPoint.

> **¿Por qué usar gráficos editables?**  
> Los gráficos editables permiten a los presentadores ajustar datos, colores o etiquetas sin volver al archivo original de Excel, acelerando los cambios de última hora y manteniendo fluido el flujo de trabajo de la presentación.

## Convertir una hoja de cálculo a PowerPoint (worksheet to PowerPoint)

A continuación se muestra un ejemplo completo y ejecutable que demuestra la conversión **worksheet to PowerPoint**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### Explicación de cada paso

| Paso | Qué hace el código | Por qué es importante para **export excel chart pptx** |
|------|-------------------|----------------------------------------------|
| 1️⃣   | Carga `input.xlsx` en un objeto `Aspose.Cells.Workbook`. | El libro de trabajo proporciona acceso a los gráficos que deseas exportar. |
| 2️⃣   | Establece `ExportType` a `Pptx` y habilita `ExportChartAsEditableText` y `ExportShapeAsEditableText`. | Estas banderas son la clave para **editable charts pptx** – indican a la biblioteca que escriba la geometría del gráfico como objetos de dibujo de PowerPoint en lugar de imágenes raster. |
| 3️⃣   | Llama a `ConvertToImage` en la primera hoja de cálculo, produciendo `Worksheet.pptx`. | El método realiza la operación de **export excel to powerpoint** y escribe un archivo PPTX que puede abrirse directamente en PowerPoint. |

> **Consejo profesional:** Si necesitas exportar *múltiples* hojas de cálculo, recorre `workbook.Worksheets` y llama a `ConvertToImage` para cada una, opcionalmente nombrando los archivos de salida `Sheet1.pptx`, `Sheet2.pptx`, etc.

## Habilitar gráficos editables en el PPTX (export excel chart pptx)

Cuando `ExportChartAsEditableText` se establece en `true`, Aspose.Cells escribe cada gráfico como una colección de elementos `<a:graphic>` dentro del XML del PPTX. PowerPoint entonces trata esos elementos como objetos de gráfico nativos, que puedes hacer doble clic para abrir el editor de gráficos.

**Problemas comunes**

* **Falta de licencia de Aspose.Cells** – Sin una licencia la biblioteca agrega una marca de agua al resultado. Registra una licencia al inicio de tu programa (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **Tipos de gráficos no compatibles** – Aunque la mayoría de los gráficos 2‑D (columna, línea, pastel) son totalmente editables, algunos gráficos 3‑D complejos o combinados pueden revertirse a imágenes. Prueba tus tipos de gráficos específicos si dependes de la editabilidad completa.  
* **Hojas de cálculo grandes** – Exportar hojas de cálculo muy grandes puede consumir mucha memoria. Considera usar `ExportMaxRows` o `ExportMaxColumns` en `ImageOrPrintOptions` para limitar el área que se convierte.

## Consejos para mantener los gráficos editables (editable charts pptx)

1. **Conservar los rangos de datos del gráfico** – Asegúrate de que la fuente de datos del gráfico se encuentre en la misma hoja que estás exportando. Las referencias entre hojas se convierten en valores estáticos en el PPTX.  
2. **Usar la última versión de Aspose.Cells** – Las nuevas versiones mejoran el soporte para funciones adicionales de gráficos y corrigen errores de casos límite relacionados con la exportación a PPTX.  
3. **Validar la salida** – Después de la conversión, abre el PPTX generado en PowerPoint y verifica que puedes editar el título del gráfico, las series y las etiquetas de los ejes. Si algún elemento aparece como una imagen, verifica nuevamente que `ExportChartAsEditableText` esté habilitado y que el tipo de gráfico sea compatible.  
4. **Procesamiento por lotes** – Para escenarios de automatización (p. ej., generar una presentación a partir de varios informes de Excel), envuelve la lógica de conversión en un método que acepte `Workbook`, `int worksheetIndex` y `string outputPath`. Esto aísla el flujo de trabajo de **export excel to powerpoint** y lo hace reutilizable.

## Recapitulación del ejemplo completo

Uniendo todo, aquí tienes el programa mínimo que puedes copiar‑pegar en un nuevo proyecto de consola .NET:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**Resultado esperado**

* Aparece un archivo llamado `Worksheet.pptx` en `YOUR_DIRECTORY`.  
* Al abrir el archivo en Microsoft PowerPoint se muestra una diapositiva que contiene el gráfico original y cualquier cuadro de texto.  
* Al hacer doble clic en el gráfico se abre el editor de gráficos de PowerPoint, permitiéndote cambiar los valores de las series, colores o títulos de los ejes—verificando que la función **editable charts pptx** funciona como se espera.

## Conclusión

Ahora tienes una solución completa para **export Excel to PowerPoint** que mantiene los gráficos editables. Configurando `ImageOrPrintOptions` con `ExportChartAsEditableText` y `ExportShapeAsEditableText`, el proceso de conversión produce un archivo PPTX nativo donde los gráficos se comportan como los creados directamente en PowerPoint.  

Desde aquí puedes:

* Extender el código para manejar múltiples hojas de cálculo (**worksheet to PowerPoint** para cada una).  
* Combinar la exportación con otras funciones de Aspose.Cells, como agregar títulos de diapositiva o insertar imágenes.  
* Explorar temas relacionados como **export Excel chart PPTX** con temas personalizados o automatizar todo el pipeline de generación de presentaciones.

Siéntete libre de experimentar con diferentes tipos de gráficos, agregar etiquetas de datos o integrar este flujo de trabajo en un sistema de informes más amplio. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo convertir Excel a PowerPoint usando Aspose.Cells para .NET: Guía completa](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}