---
category: general
date: 2026-09-15
description: Aprende cómo incrustar fuentes en SVG y exportar gráficos de Excel a
  PowerPoint, cubriendo la conversión de XLSX a SVG y la conversión de XLSX a PPTX
  con ejemplos de código completos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: es
lastmod: 2026-09-15
og_description: Incrusta fuentes en SVG y exporta gráficos de Excel a PowerPoint con
  código C# paso a paso. Convierte XLSX a SVG y XLSX a PPTX de forma rápida y fiable.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Incrustar fuentes en SVG y exportar gráfico de Excel a PowerPoint – guía
  completa
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cómo incrustar fuentes en SVG al convertir archivos de Excel a SVG y PowerPoint
url: /es/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo incrustar fuentes en SVG al convertir archivos de Excel a SVG y PowerPoint  

Si necesita **incrustar fuentes en SVG** al convertir un libro de Excel, esta guía le muestra exactamente cómo hacerlo. También aprenderá cómo **exportar un gráfico de Excel a PowerPoint**, y cómo **convertir XLSX a SVG** y **convertir XLSX a PPTX** con gráficos editables.  

Trabajar con datos de Excel de forma programática a menudo significa que debe mover el mismo contenido visual entre diferentes formatos de archivo. Recrear manualmente un gráfico en PowerPoint o volver a aplicar fuentes en un SVG es propenso a errores y consume tiempo. Al final de este tutorial tendrá un fragmento de C# único y reutilizable que:

* Guarda un libro de trabajo como un archivo SVG con fuentes incrustadas y selectores de variación de fuentes.  
* Exporta el mismo libro de trabajo a un archivo PPTX donde el gráfico permanece editable.  

El único requisito previo es una versión reciente de **Aspose.Cells for .NET** (2024‑x o posterior) y un entorno de desarrollo .NET como Visual Studio 2022.

---

## Lo que necesitará  

* .NET 6.0 o posterior (el código también funciona en .NET Framework 4.8).  
* Paquete NuGet de Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* Un archivo Excel (`input.xlsx`) que contenga al menos un gráfico.  
* Permiso de escritura en el directorio de salida.  

---

## Incrustar fuentes en SVG al convertir XLSX a SVG  

Incrustar fuentes garantiza que el SVG se renderice correctamente en cualquier dispositivo, incluso si el sistema de destino no tiene las tipografías originales. La clase `SvgSaveOptions` proporciona dos indicadores que hacen esto posible: `EmbedFonts` y `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Por qué funciona:**  
* `EmbedFonts = true` copia los archivos de fuentes al sección `<defs>` del SVG, eliminando dependencias externas.  
* `FontVariationSelectors = true` agrega los selectores necesarios para fuentes que admiten características OpenType, preservando variaciones de glifos como ligaduras.  

**Resultado esperado:** Abra `WithFonts.svg` en cualquier navegador moderno; el texto dentro del gráfico o las celdas aparece con la tipografía exacta utilizada en Excel, incluso en máquinas que no tienen esa fuente instalada.

---

## Exportar gráfico de Excel a PowerPoint con gráficos editables  

Cuando necesita incrustar un gráfico en una diapositiva de PowerPoint pero aún permitir que el destinatario edite los datos del gráfico, `PptxSaveOptions` de Aspose.Cells ofrece el indicador `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Por qué es importante:**  
Establecer `ExportEditableChart` en `true` guarda el gráfico como un objeto de gráfico Office Open XML en lugar de una imagen estática. Cuando abra `EditableChart.pptx` en PowerPoint, puede hacer clic derecho en el gráfico → **Edit Data** y modificar la serie como lo haría con un gráfico nativo de PowerPoint.

**Pasos de verificación:**  

1. Abra `EditableChart.pptx` en PowerPoint.  
2. Localice la diapositiva que contiene el gráfico.  
3. Elija **Chart Tools → Design → Edit Data**.  
4. Confirme que aparece la cuadrícula de datos al estilo Excel y que puede cambiar los valores.

---

## Convertir XLSX a SVG – resumen completo del flujo de trabajo  

A continuación se muestra una versión compacta que combina la carga, la manipulación opcional de datos y el guardado como SVG. Úsela cuando solo necesite la salida SVG.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Llame al método de la siguiente manera:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Consejo para casos extremos:** Si su libro de trabajo contiene fuentes personalizadas que no están instaladas en el servidor, incrústelas manualmente antes de llamar a `Save`. Use `FontInfoCollection` para agregar los archivos de fuentes a `SvgSaveOptions` mediante la propiedad `CustomFonts` (disponible en versiones más recientes de Aspose.Cells).

---

## Convertir XLSX a PPTX – preservando la editabilidad del gráfico  

El siguiente método auxiliar demuestra la ruta **convert XLSX to PPTX** mientras asegura que el gráfico permanezca editable.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Uso:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Pregunta común:** *¿Qué pasa si mi libro de trabajo tiene varias hojas de cálculo con gráficos?*  
**Respuesta:** Aspose.Cells exporta la primera hoja de cálculo por defecto. Para incluir hojas adicionales, itere sobre `workbook.Worksheets`, copie cada gráfico a una nueva diapositiva y guarde cada diapositiva individualmente usando objetos `Presentation` de Aspose.Slides. Este escenario avanzado está más allá del flujo básico de “guardar libro de trabajo como SVG” y “exportar gráfico de Excel a PowerPoint”, pero los indicadores principales siguen siendo los mismos.

---

## Consejos prácticos y trampas  

* **Rendimiento:** Incrustar fuentes aumenta el tamaño del archivo SVG. Si el tamaño es un problema, establezca `EmbedFonts = false` y confíe en fuentes web‑seguras.  
* **Licencia de fuentes:** Asegúrese de tener derecho a incrustar las fuentes que usa; algunas fuentes comerciales restringen la incrustación.  
* **Compatibilidad de gráficos:** Los gráficos editables se guardan como partes `chart.xml` dentro del PPTX. Los gráficos muy complejos (p. ej., 3‑D o combinados) pueden perder algo de estilo al editarse en PowerPoint. Pruebe los tipos de gráficos más comunes que necesita.  
* **Desajustes de versión:** El indicador `ExportEditableChart` requiere Aspose.Cells 20.10 o posterior. Usar una versión anterior retrocederá silenciosamente a una imagen rasterizada.  
* **Seguridad en hilos:** Los objetos Workbook no son seguros para hilos. Cree una nueva instancia de `Workbook` por solicitud en un escenario de servicio web.  

---

## Ejemplo completo de extremo a extremo  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Ejecutar este programa produce dos archivos:

* **WithFonts.svg** – un SVG que se renderiza exactamente como la vista de Excel, con fuentes incluidas.  
* **EditableChart.pptx** – una presentación de PowerPoint donde el gráfico puede editarse directamente.

---

## Conclusión  

Ahora sabe cómo **incrustar fuentes en SVG** cuando **convierte XLSX a SVG**, y cómo **exportar un gráfico de Excel a PowerPoint** manteniendo el gráfico editable. El mismo código también muestra una forma limpia de **guardar el libro de trabajo como SVG** y **convertir XLSX a PPTX** con un esfuerzo mínimo.  

Desde aquí puede explorar temas adicionales como:

* Agregar fuentes personalizadas programáticamente (`svgOptions.CustomFonts`).  
* Procesamiento por lotes de varios libros de trabajo en un servicio en segundo plano.  
* Usar Aspose.Slides para crear archivos PPTX de varias diapositivas que combinen varios gráficos de Excel.  

¡Experimente con las opciones, adapte los fragmentos a su proyecto y disfrute de conversiones fiables de Excel a SVG/PPTX sin procesamiento manual posterior. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar características adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo convertir gráficos de Excel a SVG usando Aspose.Cells para .NET (Guía paso a paso)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convertir gráfico de Excel a SVG Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convertir gráfico de Excel a SVG Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}