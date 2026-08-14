---
category: general
date: 2026-08-14
description: Exportar Excel a PowerPoint usando Aspose.Cells y aprender cómo calcular
  fórmulas de Excel en código. Ejemplo paso a paso en C# con código completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: es
lastmod: 2026-08-14
og_description: Exporta Excel a PowerPoint con Aspose.Cells y calcula fórmulas de
  Excel en código. Sigue esta guía completa para generar archivos PPTX editables a
  partir de libros de trabajo.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Exportar Excel a PowerPoint con Aspose.Cells – tutorial completo en C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Exportar Excel a PowerPoint con Aspose.Cells – guía completa de programación
url: /es/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Excel a PowerPoint con Aspose.Cells – guía completa de programación

Si necesitas **exportar Excel a PowerPoint** de forma programática, esta guía te muestra exactamente cómo hacerlo con Aspose.Cells para .NET. También aprenderás a **calcular fórmulas de Excel en código**, copiar tablas dinámicas sin perder sus definiciones y usar la nueva función EXPAND de Office‑365 para matrices dinámicas.

En las siguientes secciones recorreremos un ejemplo real en C#, explicaremos por qué cada línea es importante y cubriremos los problemas comunes para que puedas adaptar la solución a tus propios proyectos.

## Qué cubre este tutorial

* Cargar un libro de trabajo existente (`input.xlsx`)  
* Copiar un rango que contiene una tabla dinámica preservando su definición  
* Exportar el libro de trabajo a un archivo PowerPoint (`.pptx`) con cuadros de texto y formas editables  
* Exportar un rango de celdas como cadenas usando lógica personalizada  
* Calcular fórmulas de Excel en código, incluida la función EXPAND de Office‑365  
* Guardar el libro de trabajo final con todos los cambios aplicados  

**Requisitos previos**  
* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7.2+)  
* Aspose.Cells para .NET v25.11 o más reciente (la opción `CopyPivotTable` se introdujo en la v25.11)  
* Un conocimiento básico de C# y conceptos de Excel como rangos, tablas dinámicas y fórmulas  

> **Consejo profesional:** Instala Aspose.Cells vía NuGet (`Install-Package Aspose.Cells`) para mantener tu proyecto actualizado con las últimas funciones.

## Exportar Excel a PowerPoint con Aspose.Cells

La primera tarea importante es convertir el libro de trabajo en una presentación PowerPoint manteniendo todos los elementos visuales editables. Esto es esencial cuando deseas generar presentaciones a partir de informes financieros o paneles de control de forma automática.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Por qué funciona esto

* **`Workbook`** carga todo el archivo Excel en memoria, dándote acceso completo a la API.  
* **`CopyRange`** con `CopyPivotTable = true` garantiza que la fuente de datos, la caché y el diseño de la tabla dinámica se dupliquen exactamente—algo que versiones anteriores de Aspose.Cells no podían hacer.  
* Agregar una nueva hoja de cálculo (`Copy`) te permite mantener la hoja original sin tocar, lo cual es útil para auditorías.

## Exportar el libro de trabajo a PowerPoint con objetos editables

Ahora convertimos el libro de trabajo en un archivo PowerPoint. Al habilitar `ExportEditableObjects`, cada gráfico, forma o cuadro de texto se convierte en un objeto nativo de PowerPoint que los usuarios pueden editar directamente después de la exportación.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Explicación

* **`WorkbookDesigner`** es un asistente de alto nivel que prepara el libro de trabajo para la exportación, manejando Smart Markers, rangos nombrados y ajustes de diseño.  
* Establecer `ExportEditableObjects = true` indica a Aspose.Cells que traduzca los dibujos de Excel en formas de PowerPoint en lugar de aplanarlos en imágenes. Esto produce una presentación **totalmente editable**.

> **Caso límite:** Si tu libro de trabajo contiene gráficos complejos construidos a partir de conexiones de datos externas, asegúrate de que esas conexiones estén resueltas antes de llamar a `ExportToPptx`, de lo contrario el gráfico podría aparecer en blanco.

## Exportar un rango como cadenas usando lógica personalizada

A veces necesitas valores de cadena sin procesar para procesamiento posterior (p.ej., alimentar un analizador CSV). La clase `ExportTableOptions` te permite controlar cómo se convierte cada celda.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Por qué podrías usar esto

* **Tipo de dato uniforme:** Exportar como cadenas evita errores de incompatibilidad de tipos cuando el consumidor espera texto.  
* **Formato personalizado:** Reemplaza `value.ToString()` con cualquier formateador personalizado (p.ej., `value.ToString("yyyy-MM-dd")` para fechas).  

## Calcular fórmulas de Excel en código

Un requisito frecuente es **calcular fórmulas de Excel en código** sin abrir Excel. Aspose.Cells proporciona un motor de cálculo incorporado que funciona sin conexión y soporta las últimas funciones de Office‑365, incluida `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Cómo funciona el motor de cálculo

* La propiedad `Formula` almacena la expresión exactamente como la escribirías en Excel.  
* `CalculateFormula()` desencadena una recalculación completa del libro de trabajo, respetando las dependencias entre celdas.  
* La función `EXPAND` (disponible en Excel 365) devuelve un rango de desbordamiento basado en la celda origen (`B1`) y las filas (`5`) y columnas (`3`) especificadas.  

> **Consejo:** Si necesitas calcular solo un subconjunto del libro de trabajo, usa `Worksheet.CalculateFormula()` para limitar el alcance y mejorar el rendimiento.

## Guardar el libro de trabajo con todos los cambios aplicados

Finalmente, escribe el libro de trabajo modificado de nuevo en disco. Puedes guardarlo en cualquiera de los formatos compatibles (`.xlsx`, `.xls`, `.csv`, etc.) cambiando la extensión del archivo.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Qué verificar

* Abre `result.xlsx` en Excel para confirmar la copia de la tabla dinámica, el resultado de la fórmula `EXPAND` y cualquier cadena exportada de forma personalizada.  
* Abre `output.pptx` en PowerPoint; deberías ver una diapositiva que refleja el diseño de Excel, y todos los gráficos/cuadros de texto deberían ser editables.

## Preguntas frecuentes y solución de problemas

| Pregunta | Respuesta |
|----------|-----------|
| **¿Necesito una licencia para usar Aspose.Cells?** | Sí. Una versión de prueba funciona para evaluación, pero una licencia completa elimina las marcas de agua de evaluación y desbloquea la función `CopyPivotTable`. |
| **¿Qué pasa si el PPTX exportado muestra formas en blanco?** | Verifica que los objetos de dibujo del libro de trabajo no estén ocultos (`Visible = true`) y que cualquier enlace de imagen externo esté incrustado antes de la exportación. |
| **¿Puedo exportar varias hojas de cálculo a diapositivas PPTX separadas?** | Usa `WorkbookDesigner.ExportToPptx` en un bucle, especificando un `ExportOptions` diferente para cada hoja, o combínalas en una sola presentación añadiendo diapositivas manualmente mediante Aspose.Slides. |
| **¿`CalculateFormula` es seguro para subprocesos?** | No. Realiza los cálculos en un solo subproceso o clona el libro de trabajo por subproceso para evitar condiciones de carrera. |

## Conclusión

Ahora tienes una **solución completa de extremo a extremo para exportar Excel a PowerPoint** usando Aspose.Cells, y comprendes cómo **calcular fórmulas de Excel en código**—incluida la moderna función `EXPAND`. El tutorial cubrió la carga de un libro de trabajo, la copia de tablas dinámicas, la exportación a PowerPoint editable, la exportación personalizada de cadenas, el cálculo de fórmulas y el guardado final.

Desde aquí puedes:

* Extender la exportación para incluir múltiples diapositivas por hoja de cálculo (la palabra clave secundaria: *calculate Excel formulas in code* puede reutilizarse al generar datos de gráficos).  
* Integrar Aspose.Slides para añadir animaciones o diseños de diapositiva maestra.  
* Reemplazar el delegado simple `CustomExport` por un formato sensible a la configuración regional para proyectos internacionales.  

Siéntete libre de experimentar con diferentes rangos, explorar otras funciones de Office‑365 (p.ej., `FILTER`, `SORT`), y combinar este flujo de trabajo con la entrega automática de correos electrónicos para pipelines de informes totalmente automatizados.

---

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Automatizar la exportación de datos de Excel usando Aspose.Cells para .NET: Guía paso a paso](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Cómo exportar gráficos de Excel a PDF usando Aspose.Cells para .NET: Guía paso a paso](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Exportar celdas de Excel a imagen usando Aspose.Cells .NET: Guía paso a paso](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}