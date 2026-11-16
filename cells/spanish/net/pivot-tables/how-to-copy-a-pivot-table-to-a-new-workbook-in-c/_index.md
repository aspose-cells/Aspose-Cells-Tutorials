---
category: general
date: 2026-11-16
description: Cómo copiar una tabla dinámica de un archivo de Excel a un nuevo libro
  de trabajo usando C#. Aprende a cargar el libro, copiar el rango y preservar las
  tablas dinámicas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: es
lastmod: 2026-11-16
og_description: Cómo copiar una tabla dinámica de un libro de trabajo existente a
  uno nuevo usando C#. Sigue esta guía completa para cargar el libro de Excel, copiar
  el rango y mantener la tabla dinámica intacta.
og_image_alt: how to copy pivot table example in C#
og_title: Cómo copiar una tabla dinámica a un nuevo libro de trabajo en C# – guía
  paso a paso
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Cómo copiar una tabla dinámica a un nuevo libro de trabajo en C#
url: /es/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica a un nuevo libro de trabajo en C#

Si necesitas **how to copy pivot table** de un archivo Excel a un nuevo libro de trabajo, esta guía te muestra los pasos exactos. Aprenderás cómo **load excel workbook c#**, definir el rango de origen y **copy range to new workbook** manteniendo la tabla dinámica intacta.

Copiar una tabla dinámica es un requisito común cuando deseas reutilizar una plantilla de informe, migrar datos entre proyectos o generar un archivo ligero para distribución. El ejemplo de código a continuación usa Aspose.Cells, una biblioteca .NET totalmente administrada que funciona sin Microsoft Office instalado. Al final de este tutorial tendrás un programa ejecutable que crea un nuevo libro de trabajo que contiene la tabla dinámica original, listo para procesamiento adicional o para compartir.

## Requisitos previos

* .NET 6.0 SDK o posterior (el ejemplo funciona con .NET Core y .NET Framework)
* Visual Studio 2022 o cualquier editor de C# que prefieras
* Una licencia de Aspose.Cells para .NET (la prueba gratuita funciona para evaluación)
* Un archivo Excel de origen (`Source.xlsx`) que contiene al menos una tabla dinámica

> **Consejo profesional:** Si estás usando la prueba gratuita, establece la licencia en el código para evitar marcas de agua de evaluación.

## Paso 1: Cargar el libro de trabajo de origen (load excel workbook c#)

La primera acción es abrir el libro de trabajo que contiene la tabla dinámica. Aspose.Cells lee el archivo en memoria, dándote acceso completo a hojas de cálculo, celdas y objetos de tabla dinámica.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Por qué es importante*: Cargar el libro de trabajo es la base para cualquier automatización de Excel. Sin un objeto `Workbook` válido no puedes inspeccionar la tabla dinámica ni copiar sus datos.

## Paso 2: Definir el área de celdas que rodea la tabla dinámica (copy range to new workbook)

Una tabla dinámica vive dentro de un bloque rectangular de celdas. Debes especificar ese bloque para que la operación de copia sepa qué mover. El constructor `CellArea` usa índices basados en cero: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Por qué es importante*: Al establecer explícitamente el rango evitas copiar datos no relacionados y aseguras que la caché de la tabla dinámica se incluya. El rango puede calcularse dinámicamente si necesitas manejar tamaños de tabla dinámica variables.

## Paso 3: Crear un nuevo libro de trabajo y obtener su primera hoja de cálculo

Ahora crea el libro de trabajo de destino que recibirá las filas copiadas. Aspose.Cells agrega automáticamente una hoja de cálculo predeterminada, que usaremos como objetivo.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Por qué es importante*: Comenzar con un libro de trabajo limpio garantiza que solo la tabla dinámica (y sus filas de soporte) terminen en el archivo, manteniendo la salida ligera.

## Paso 4: Copiar filas del rango de origen a la hoja de destino (how to copy pivot table)

El método `CopyRows` copia filas completas, preservando fórmulas, formato y—crucialmente—tablas dinámicas. Los parámetros del método son: fila de inicio, fila final, colección de celdas de destino y el índice de fila en el destino donde comienza la copia (aquí `0` para iniciar en la primera fila).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Por qué es importante*: Usar `CopyRows` en lugar de copiar celdas individuales asegura que la caché de la tabla dinámica permanezca vinculada a los datos copiados. Aspose.Cells maneja las estructuras XML subyacentes, por lo que no necesitas reconstruir la tabla dinámica manualmente.

## Paso 5: Guardar el libro de trabajo resultante (copy range to new workbook)

Finalmente, escribe el nuevo archivo en disco. El libro de trabajo de destino ahora contiene una tabla dinámica idéntica que funciona de forma independiente del archivo de origen.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Resultado esperado

Ejecutar el programa produce `CopyWithPivot.xlsx`. Al abrir el archivo en Excel se muestra:

* El mismo diseño de tabla dinámica que en `Source.xlsx`
* Todas las filas de datos de origen que formaban parte de la caché de la tabla dinámica
* Sin referencias al libro de trabajo original (la tabla dinámica funciona sin conexión)

## Manejo de variaciones comunes

### Copiar múltiples tablas dinámicas

Si tu hoja de origen contiene varias tablas dinámicas, amplía el `CellArea` para cubrir la unión de todos los rangos, o repite el paso de copia para cada área distinta.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Preservar estilos y formato condicional

`CopyRows` copia los estilos de celda automáticamente. Si necesitas preservar estilos nombrados a nivel de libro o formatos numéricos personalizados, llama a `destWorkbook.Worksheets[0].CopyStyle` antes de guardar.

### Trabajar con libros de trabajo grandes

Para archivos mayores de 100 MB, considera usar `Workbook.LoadOptions` con `MemorySetting` configurado a `MemorySetting.MemoryPreference` para reducir la presión de memoria.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Código fuente completo (listo para ejecutar)

A continuación se muestra el programa completo, incluyendo directivas `using` y comentarios. Cópialo en un nuevo proyecto de consola y reemplaza `YOUR_DIRECTORY` con la ruta real de la carpeta.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Ejecuta el programa (`dotnet run` o `Ctrl+F5` en Visual Studio). Después de la ejecución, abre `CopyWithPivot.xlsx` para verificar que la tabla dinámica se comporte exactamente como la original.

## Preguntas frecuentes

**Q: ¿Funciona esto con libros de trabajo con macros o habilitados para VBA?**  
A: Aspose.Cells puede leer archivos habilitados para macros (`.xlsm`), pero el código de macro no se copia. La tabla dinámica en sí se conserva porque forma parte del XML de la hoja de cálculo.

**Q: ¿Qué pasa si la tabla dinámica usa una fuente de datos externa?**  
A: La operación de copia incluye solo los datos en caché. Si el libro de trabajo de destino necesita actualizarse desde la fuente original, tendrás que volver a configurar la conexión de datos manualmente.

**Q: ¿Puedo copiar la tabla dinámica sin las filas de datos subyacentes?**  
A: No. Una tabla dinámica necesita su caché. La forma más fiable es copiar las filas que contienen la caché, como se muestra. Luego puedes ocultar esas filas si no deseas que sean visibles.

## Conclusión

Ahora sabes **how to copy pivot table** de un archivo Excel a otro usando C#. El tutorial cubrió **load excel workbook c#**, definió el **copy range to new workbook**, y utilizó el método `CopyRows` de Aspose.Cells para mantener la tabla dinámica intacta. Con el ejemplo completo y ejecutable puedes integrar este patrón en pipelines de informes, herramientas de exportación automatizadas o cualquier escenario donde una tabla dinámica deba trasladarse entre libros de trabajo.

### Próximos pasos

* Explora las características de **Aspose.Cells** como la actualización de tablas dinámicas programáticamente.  
* Combina este enfoque con **ExcelPackage** (EPPlus) si necesitas una alternativa de código abierto.  
* Automatiza la copia entre múltiples hojas iterando sobre `srcWorkbook.Worksheets`.  

Siéntete libre de experimentar con diferentes rangos, agregar estilos personalizados o incrustar la lógica en un servicio de procesamiento de datos más grande. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear nuevo libro de trabajo en C# – Copiar tabla dinámica](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [Cómo copiar tabla dinámica en Excel con C# y Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Copiar tabla dinámica a nuevo libro de trabajo, exportar forma a PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}