---
category: general
date: 2026-11-19
description: Aprenda cómo copiar un rango usando CopyOptions en Aspose.Cells, preservando
  el formato y las tablas dinámicas al copiar un rango de Excel con formato.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: es
lastmod: 2026-11-19
og_description: Copiar un rango usando CopyOptions en Aspose.Cells permite duplicar
  datos de Excel con todo el formato y las tablas dinámicas preservados, lo que posibilita
  una manipulación fiable del libro de trabajo.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Copiar rango usando CopyOptions en Aspose.Cells – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cómo copiar un rango usando CopyOptions en Aspose.Cells
url: /es/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar un rango usando CopyOptions en Aspose.Cells

Si necesitas **copy range using CopyOptions** en Aspose.Cells, esta guía te muestra exactamente cómo duplicar un bloque de celdas manteniendo todo el formato y las tablas dinámicas incrustadas intactas. Muchos desarrolladores tienen dificultades para preservar el estilo al mover datos entre hojas de cálculo, y la clase `CopyOptions` resuelve ese problema sin pasos manuales adicionales.

En este tutorial aprenderás a:

* Definir áreas de origen y destino en un libro de Excel.  
* Usar `CopyOptions` para conservar el formato de celdas, el ancho de columnas y las tablas dinámicas.  
* Guardar el resultado en un nuevo archivo listo para el procesamiento posterior.

El ejemplo funciona con cualquier archivo `.xlsx` y solo requiere la biblioteca Aspose.Cells para .NET.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior instalado.  
* Una licencia válida de Aspose.Cells para .NET (o una clave de evaluación gratuita).  
* Visual Studio 2022 o cualquier IDE de C# que prefieras.  

No se necesitan paquetes NuGet adicionales más allá de `Aspose.Cells`.

## Paso 1: Configurar el proyecto e importar espacios de nombres

Crea una nueva aplicación de consola y agrega la referencia a Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

La directiva `using Aspose.Cells;` te brinda acceso a `Workbook`, `CellArea` y `CopyOptions`.

## Paso 2: Cargar el libro de trabajo que deseas modificar

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` representa todo el archivo de Excel. Reemplaza `YOUR_DIRECTORY` con la carpeta que contiene tu archivo de origen.

## Paso 3: Definir los rangos de origen y destino

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` crea un área rectangular basada en las direcciones de celda superior‑izquierda e inferior‑derecha. Puedes ajustar las coordenadas para que coincidan con el tamaño del bloque que necesitas copiar.

## Paso 4: Copiar el rango preservando el formato y las tablas dinámicas

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

El objeto `CopyOptions` indica a Aspose.Cells exactamente qué conservar. Configurar `CopyPivotTables = true` es la clave para **copy range using CopyOptions** cuando tu origen incluye tablas dinámicas. Las demás banderas garantizan que **copy excel range with formatting** se logre automáticamente—no se requiere código adicional para volver a aplicar estilos después de la copia.

### Por qué `CopyOptions` es importante

* **Performance** – La biblioteca realiza una única operación interna en lugar de copiar celdas una por una.  
* **Accuracy** – Todos los aspectos visuales (fuentes, colores, bordes) sobreviven al movimiento, lo que elimina la desviación visual en los informes generados.  
* **Reliability** – Las tablas dinámicas siguen funcionando porque su caché y referencias de origen se duplican.

## Paso 5: Guardar el libro de trabajo modificado

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Después de llamar a `Save`, el archivo `output.xlsx` contiene los datos originales más el bloque duplicado en la ubicación de destino, completo con formato y tablas dinámicas.

## Código fuente completo como referencia

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Running this program prints:

```
Range copied successfully. Output saved to output.xlsx
```

Abre `output.xlsx` en Excel – verás el bloque A1:H30 duplicado en A35:H64, con todos los colores de celda, bordes, formatos numéricos y cualquier tabla dinámica intactos.

## Preguntas comunes y manejo de casos límite

### ¿Qué pasa si el área de destino se superpone con el origen?

Aspose.Cells lanza una `ArgumentException`. Para evitarlo, calcula un destino que no intersecte el origen, o copia a una hoja de cálculo diferente:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### ¿Cómo copiar entre diferentes libros de trabajo?

Crea una segunda instancia de `Workbook` para el archivo de destino y usa el mismo objeto `CopyOptions`:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### ¿`CopyOptions` también copia celdas combinadas?

Sí. La bandera `CopyStyle` incluye la información de celdas combinadas. Si necesitas un control más fino, establece `options.CopyMergedCells = true` (disponible en versiones más recientes).

### ¿Qué pasa con rangos grandes (miles de filas)?

La operación es eficiente en memoria, pero podrías querer aumentar el `WorkbookSettings` `MemorySetting` a `MemorySetting.MemoryPreference` para archivos muy grandes.

## Consejos profesionales

* **Reuse the same `CopyOptions`** instance for multiple copy operations – reduce la sobrecarga de asignación de objetos.  
* **Validate ranges** before copying: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` ayuda a detectar errores tipográficos temprano.  
* **Turn off calculation** (`workbook.Settings.CalcMode = CalculationMode.Manual`) mientras copias conjuntos de datos grandes para acelerar el proceso, luego llama a `workbook.CalculateFormula()` después de la copia si necesitas resultados actualizados.

## Conclusión

Ahora sabes cómo **copy range using CopyOptions** en Aspose.Cells, logrando un **copy excel range with formatting** completo mientras preservas las tablas dinámicas y otras funciones avanzadas. Este enfoque elimina la reaplicación manual de estilos y asegura que tu automatización de Excel sea robusta y mantenible.

Los siguientes pasos que podrías explorar:

* Usa `CopyOptions` para duplicar hojas de cálculo completas.  
* Combina la operación de copia con `WorksheetCollection.AddCopy` para la generación de informes basados en plantillas.  
* Integra el código en una API ASP.NET Core para proporcionar transformaciones de Excel en tiempo real.

¡Siéntete libre de experimentar con diferentes coordenadas de origen/destino y comparte tus resultados en los comentarios!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}