---
category: general
date: 2026-08-04
description: Exporta gráficos de Excel a PowerPoint usando Aspose.Cells en C#. Sigue
  esta guía paso a paso de conversión de Excel a PowerPoint y mantén las formas editables.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: es
lastmod: 2026-08-04
og_description: Exporta gráficos de Excel a PowerPoint con Aspose.Cells en C#. Aprende
  a crear un PPTX editable, conservar los datos del gráfico y automatizar la conversión
  de Excel a PowerPoint.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Exportar gráfico de Excel a PowerPoint con C# – tutorial completo de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Exportar gráfico de Excel a PowerPoint con C# – guía completa de Aspose.Cells
url: /es/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar gráfico de Excel a PowerPoint con C# – guía completa de Aspose.Cells

Si necesita **exportar gráfico de Excel a PowerPoint**, este tutorial le muestra cómo hacerlo con Aspose.Cells y Aspose.Slides en C#. Obtendrá un PPTX totalmente editable que conserva los datos y las formas del gráfico, dejando la conversión lista para trabajos de diseño adicionales.

Exportar gráficos de Excel a PowerPoint es un requisito común al crear canalizaciones de informes automatizados, presentaciones de ventas o material de capacitación. En esta guía aprenderá los pasos exactos para realizar una **conversión de Excel a PowerPoint** que mantiene todos los elementos del gráfico editables. No se requiere copiar‑pegar manualmente, y el código funciona con .NET 6+ así como con el clásico .NET Framework.

## Requisitos previos

- Una licencia válida de Aspose.Cells (o una clave de evaluación gratuita)  
- Aspose.Slides para .NET añadido al proyecto (la biblioteca maneja la salida PPTX)  
- SDK de .NET 6 o posterior instalado  
- Un libro de Excel que contenga al menos un gráfico (para este ejemplo usamos `Shapes.xlsx`)  

Puede instalar los paquetes NuGet con los siguientes comandos:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Paso 1: Cargar el libro de Excel

La primera operación es abrir el libro que contiene el gráfico que desea exportar. La clase `Workbook` representa todo el archivo de Excel.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Por qué es importante:** Cargar el libro le brinda acceso a sus hojas de cálculo, gráficos y formato. Aspose.Cells lee el archivo sin requerir que Microsoft Office esté instalado, lo que mantiene la solución ligera y amigable para servidores.

## Paso 2: Seleccionar la hoja de cálculo y definir el área de impresión

Una hoja de cálculo puede contener muchos gráficos, pero normalmente exporta una región específica. Configurar el `PrintArea` indica a Aspose.Cells qué celdas (incluidos los gráficos) deben renderizarse.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Por qué es importante:** Al restringir la exportación a un área de impresión definida evita diapositivas en blanco innecesarias y mantiene el tamaño del archivo PPTX pequeño. El área puede ajustarse para coincidir con el rango exacto de su gráfico.

## Paso 3: Configurar opciones de exportación para un PPTX editable

Aspose.Cells utiliza la clase `ImageOrPrintOptions` para controlar el formato de salida y la editabilidad. Configurar `ImageFormat` a `ImageFormat.Pptx` crea un archivo PowerPoint, mientras que `ExportEditableShapes = true` conserva los objetos del gráfico como formas editables.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Por qué es importante:** La bandera `ExportEditableShapes` es la clave para obtener **formas editables en PowerPoint**. Sin ella, el gráfico se rasterizaría como una imagen, perdiendo la capacidad de modificar puntos de datos o estilos más adelante.

## Paso 4: Guardar la hoja de cálculo como una presentación PowerPoint

Finalmente, invoque el método `Save` en el objeto `Workbook`. El enumerado `SaveFormat.Pptx` indica a Aspose.Cells que produzca un archivo PowerPoint.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Cuando el código finalice, abra `ShapesExport.pptx` en PowerPoint. Verá una diapositiva que contiene el gráfico original de Excel como un objeto de gráfico nativo de PowerPoint. Haga doble clic en el gráfico para editar datos, cambiar colores o agregar animaciones, como si hubiera creado el gráfico directamente en PowerPoint.

### Resultado esperado

| Nombre del archivo       | Contenido en la diapositiva               |
|--------------------------|-------------------------------------------|
| `ShapesExport.pptx`      | El gráfico de `Shapes.xlsx` renderizado como un gráfico de PowerPoint editable, con etiquetas de ejes, leyendas y series de datos intactas. |

## Ejemplo completo y ejecutable

A continuación se muestra el programa completo que puede copiar, pegar y ejecutar. Incluye todas las declaraciones `using` necesarias, manejo de errores y comentarios.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Explicación de cada bloque**

| Bloque | Propósito |
|-------|-----------|
| `using` directives | Importa los espacios de nombres de Aspose.Cells y Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | Carga el archivo de Excel sin necesidad de que Office esté instalado. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Limita la exportación a la región que contiene el gráfico. |
| `ImageOrPrintOptions` | Configura la salida PPTX y habilita **la exportación PPTX de Aspose.Cells** con formas editables. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Escribe el archivo PowerPoint en disco. |
| `try / catch` | Proporciona manejo básico de errores para archivos faltantes o problemas de licencia. |

Ejecutar este programa produce una diapositiva de PowerPoint que puede abrir en Microsoft PowerPoint, Google Slides (después de la conversión) o cualquier visor compatible.

## Variaciones comunes y casos límite

### Exportar varias hojas de cálculo

Si necesita una diapositiva para cada hoja de cálculo, recorra `workbook.Worksheets` y llame a `Save` con un nombre de archivo único para cada iteración.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Controlar el diseño de la diapositiva

Aspose.Slides le permite agregar un diseño de diapositiva personalizado después de la exportación. Cree una nueva presentación, importe la diapositiva generada y luego aplique un tema maestro.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Manejar gráficos con fuentes de datos externas

Si un gráfico hace referencia a un rango de datos fuera del área de impresión definida, amplíe el `PrintArea` para incluir esas celdas. De lo contrario, el gráfico puede perder series de datos durante la exportación.

### Consideraciones de licenciamiento

Las bibliotecas Aspose funcionan en modo de evaluación con una marca de agua. Para eliminar la marca de agua, establezca la licencia antes de cualquier llamada a la API:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Haga lo mismo para Aspose.Slides si utiliza sus funciones avanzadas.

## Consejos profesionales

- **Reutilizar opciones de exportación:** Cree una única instancia de `ImageOrPrintOptions` y asígnela a cada hoja de cálculo para mantener el código DRY.  
- **Procesamiento por lotes:** Para informes a gran escala, combine esta lógica de exportación con un trabajador en segundo plano o Azure Function para generar archivos PPTX bajo demanda.  
- **Rendimiento:** Si solo necesita la imagen del gráfico (no editable), establezca `ExportEditableShapes = false`. Esto reduce el uso de memoria y acelera la conversión.  
- **Pruebas:** Verifique el PPTX generado tanto en instalaciones de PowerPoint para Windows como macOS, ya que algunas peculiaridades de renderizado difieren entre plataformas.

## Conclusión

Ahora tiene una solución completa de extremo a extremo para **exportar gráfico de Excel a PowerPoint** usando C#. El tutorial cubrió la carga del libro, la selección del área de impresión, la configuración de **la exportación PPTX de Aspose.Cells** con **formas editables en PowerPoint**, y el guardado del resultado como un archivo PPTX totalmente editable.

Desde aquí puede explorar escenarios adicionales de **conversión de Excel a PowerPoint**, como exportación por lotes, diseños de diapositivas personalizados o integrar el proceso en una API web. Experimente con diferentes tipos de gráficos, agregue imágenes o combine varias hojas de cálculo en una sola presentación para adaptar la salida a las necesidades de su negocio.

¿Listo para automatizar su flujo de trabajo de informes? Pruebe cambiar el archivo de origen, ajustar el área de impresión e integrar el código en sus servicios .NET existentes. ¡Feliz codificación!

## ¿Qué debería aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo convertir Excel a PowerPoint usando Aspose.Cells para .NET: Guía completa](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Cómo exportar gráficos de Excel a PDF usando Aspose.Cells para .NET: Guía paso a paso](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Exportar celdas de Excel a imagen usando Aspose.Cells .NET: Guía paso a paso](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}