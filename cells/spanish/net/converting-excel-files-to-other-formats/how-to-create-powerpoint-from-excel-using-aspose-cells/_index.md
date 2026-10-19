---
category: general
date: 2026-09-18
description: 'Crea PowerPoint a partir de Excel con Aspose.Cells: copia tablas dinámicas,
  exporta rangos y guarda como PPTX en unas pocas líneas de código C#.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: es
lastmod: 2026-09-18
og_description: Crea PowerPoint a partir de Excel rápidamente. Aprende cómo copiar
  tablas dinámicas, exportar rangos y guardar un libro de trabajo como PPTX usando
  Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Crear PowerPoint a partir de Excel con Aspose.Cells – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Cómo crear PowerPoint a partir de Excel usando Aspose.Cells
url: /es/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear PowerPoint a partir de Excel usando Aspose.Cells

Si necesitas crear PowerPoint a partir de Excel, esta guía te muestra una solución concisa y de extremo a extremo. Verás cómo copiar una tabla dinámica, exportar un rango seleccionado y guardar el resultado como un archivo PPTX con solo unas pocas líneas de C#.

Generar una presentación directamente a partir de los datos de una hoja de cálculo elimina el paso manual de copiar‑pegar que ralentiza los flujos de trabajo de informes. El tutorial cubre todo lo que necesitas, desde la configuración del proyecto hasta el archivo PPTX final, y funciona con la última versión de Aspose.Cells para .NET.

## Requisitos previos

* **Aspose.Cells for .NET** (versión 23.12 o más reciente). Instálalo vía NuGet: `Install-Package Aspose.Cells`.
* Un entorno de desarrollo **.NET 6+** (Visual Studio 2022 o VS Code funciona).
* Un libro de Excel (`Source.xlsx`) que contiene los datos y la tabla dinámica que deseas reutilizar.
* Permiso de escritura en la carpeta de salida.

No se requieren bibliotecas de terceros adicionales.

## Crear PowerPoint a partir de Excel – paso a paso

El proceso consta de cuatro pasos lógicos que se corresponden directamente con el ejemplo de código que verás más adelante.

### Paso 1: Cargar el libro de origen y definir el rango

Debes cargar el libro que contiene los datos de origen y la tabla dinámica. Seleccionar un rango preciso garantiza que solo se transfieran las celdas necesarias, lo que mantiene la diapositiva resultante ligera.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Por qué es importante:**  
`CreateRange` crea un objeto `Range` que puede copiarse completo. Al limitar el rango a `A1:G20`, evitas extraer celdas no relacionadas, lo que de otro modo podría inflar el archivo PowerPoint.

### Paso 2: Preparar el libro de destino

Aspose.Cells trata una diapositiva de PowerPoint como un libro cuando lo guardas en formato PPTX. Crear un libro nuevo te brinda un lienzo limpio para el rango copiado.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Consejo:** Si necesitas varias diapositivas, puedes añadir hojas de cálculo adicionales y luego guardar cada una como un archivo PPTX separado.

### Paso 3: Copiar el rango preservando la tabla dinámica

El método `CopyRange` acepta un objeto `PasteOptions`. Establecer `CopyPivotTables = true` indica a Aspose.Cells que mantenga la estructura de la tabla dinámica intacta, no solo los valores renderizados.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Cómo funciona:**  
Cuando `CopyPivotTables` es true, la hoja de destino recibe tanto los datos de origen como la caché de la tabla dinámica. Esto significa que la tabla dinámica sigue siendo completamente funcional y puede actualizarse más tarde si los datos de origen cambian.

### Paso 4: Guardar el libro como archivo PowerPoint

Finalmente, exporta el libro al formato PPTX. La bandera `SaveFormat.Pptx` indica a Aspose.Cells que escriba la hoja de cálculo como una diapositiva de PowerPoint.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Resultado:**  
`CopyWithPivot.pptx` se abre en Microsoft PowerPoint (o cualquier visor compatible) con una sola diapositiva que muestra el rango copiado, incluida una tabla dinámica en vivo que puede interactuarse en PowerPoint.

## Ejemplo completo ejecutable

A continuación se muestra el programa completo que puedes pegar en un nuevo proyecto de consola y ejecutar de inmediato.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Salida esperada:**  
Al ejecutar el programa se imprime “PowerPoint file created successfully.” y se genera un archivo llamado `CopyWithPivot.pptx`. Al abrir el archivo en PowerPoint se muestra una sola diapositiva donde el rango de Excel copiado aparece exactamente como estaba en la hoja de origen, con una tabla dinámica activa que puede actualizarse desde PowerPoint.

## Variaciones comunes y casos límite

| Situación | Qué cambiar |
|-----------|-------------|
| **Múltiples tablas dinámicas** | Define objetos `Range` separados para cada tabla y llama a `CopyRange` para cada uno, o copia toda la hoja si comparten la misma fuente de datos. |
| **Conjuntos de datos grandes** | Amplía el rango (p. ej., `"A1:Z5000"`). Considera habilitar `PasteOptions.CompressData = true` para reducir el tamaño del PPTX. |
| **Diseños de diapositiva diferentes** | Después de guardar como PPTX, abre el archivo en PowerPoint y aplica un diseño o tema personalizado; los datos siguen siendo editables. |
| **Guardar en un flujo** | Utiliza `destinationWorkbook.Save(stream, SaveFormat.Pptx)` cuando necesites devolver el PPTX a través de una API web. |
| **Preservar el formato de celdas** | Establece `PasteOptions.PasteType = PasteType.All` para mantener fuentes, colores y bordes. |

**Consejo profesional:** Siempre verifica que la carpeta de destino exista antes de llamar a `Save`. Si la carpeta falta, `Save` lanza una `DirectoryNotFoundException`.

## Conclusión

Ahora sabes cómo crear PowerPoint a partir de Excel, copiar una tabla dinámica y exportar el resultado como un archivo PPTX usando Aspose.Cells. Los pasos —cargar el libro de origen, definir un rango, copiar con `CopyPivotTables` y guardar como PPTX— cubren todo el flujo de trabajo de manera fiable y lista para producción.

A continuación, explora **cómo exportar Excel a PPTX** para múltiples hojas de cálculo, o aprende **cómo copiar rangos entre libros** cuando necesites combinar datos de varias fuentes antes de generar la presentación. Ambos temas se basan en la misma API y pueden combinarse para automatizar pipelines de informes complejos.

¡Feliz codificación y disfruta convirtiendo tus hojas de cálculo en presentaciones pulidas!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo copiar una tabla dinámica en C# – Convertir Excel a PPTX, copiar rango y crear cuadro de texto](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Crear nuevo libro – Cómo copiar una hoja de cálculo con una tabla dinámica](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Cómo crear y guardar archivos Excel con Aspose.Cells para .NET: Guía completa](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}