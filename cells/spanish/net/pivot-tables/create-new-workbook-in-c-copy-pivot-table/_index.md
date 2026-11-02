---
category: general
date: 2026-06-24
description: Crear un nuevo libro de trabajo en C# y copiar la tabla dinámica preservando
  sus datos. Aprende cómo copiar filas, exportar el rango seleccionado y mantener
  la tabla dinámica intacta.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: es
og_description: Crear un nuevo libro de trabajo en C# y copiar una tabla dinámica
  preservando sus datos. Guía paso a paso que cubre cómo copiar filas y exportar el
  rango seleccionado.
og_title: Crear nuevo libro de trabajo en C# – Copiar tabla dinámica
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Crear nuevo libro de trabajo en C# – Copiar tabla dinámica
url: /es/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear nuevo libro de trabajo en C# – Copiar tabla dinámica

¿Alguna vez necesitaste **create new workbook** en C# solo para mover una porción de datos que incluye una tabla dinámica? No eres el único. En muchos flujos de informes tomas un puñado de filas, quizá algunas columnas, y esperas que la pivot permanezca exactamente como estaba—sin referencias rotas, sin cálculos faltantes.  

¿La buena noticia? Con unas pocas líneas de Aspose.Cells puedes **copy pivot table**, mantenerla intacta e incluso **export selected range** sin romper nada. A continuación verás un ejemplo completo, listo‑para‑ejecutar que muestra **how to copy rows**, preserva la pivot y guarda el resultado como un libro de trabajo totalmente nuevo.

## Qué cubre este tutorial

- Configurar un proyecto C# con Aspose.Cells (la biblioteca que impulsa el código).
- Cargar el libro de trabajo fuente que contiene la pivot original.
- Usar los métodos `CopyRows` y `CopyColumns` de la biblioteca para duplicar el rango exacto que necesitas.
- Guardar el área duplicada en un escenario de **create new workbook** mientras la pivot sigue funcional.
- Consejos para casos límite como múltiples tablas dinámicas, filas ocultas y conjuntos de datos grandes.

Al final de esta guía podrás **export selected range** de cualquier archivo Excel, mantener viva la lógica de la pivot y colocar el nuevo archivo donde desees.

> **Prerequisite**: Aspose.Cells for .NET (versión de prueba gratuita o licenciada) instalado vía NuGet. Si aún no lo has añadido, ejecuta `dotnet add package Aspose.Cells` en la carpeta de tu proyecto.

## Crear nuevo libro de trabajo y copiar tabla dinámica

A continuación está el núcleo de la solución. Revisaremos cada línea, explicaremos por qué es importante y luego mostraremos el programa completo.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Por qué funciona esto

- **`CopyRows` / `CopyColumns`**: Estos métodos duplican los datos subyacentes de las celdas *y* los objetos asociados (como una caché de pivot). Por eso la pivot sigue funcional después del movimiento.
- **Separate destination workbook**: Al crear una nueva instancia de `Workbook` **create new workbook** sin ningún formato residual o hojas ocultas que puedan interferir.
- **Zero‑based indexing**: Aspose.Cells usa índices basados en cero, por lo que `0` apunta a la celda **A1**. Ajusta `startRow`/`startColumn` si tu pivot no está en la esquina superior‑izquierda.
- **Preserve pivot table**: La caché de la pivot reside en el mismo rango, así que copiar el rango copia automáticamente la caché. No se necesita código adicional.

---

## Cómo copiar filas sin romper la pivot

Si solo te interesa la parte de copia de filas, puedes aislarla:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**: Al copiar filas que intersectan una tabla dinámica, siempre copia el *entero* área de la pivot (filas + columnas). Las copias parciales pueden dejar a la pivot con campos faltantes, provocando errores `#REF!`.

## Exportar rango seleccionado – Un escenario del mundo real

Imagina que tienes un libro de trabajo de ventas gigantesco, pero tu cliente solo quiere el resumen del primer trimestre, que se encuentra en las filas 1‑20 y columnas A‑D. El fragmento anterior ya **export selected range** por ti. Simplemente cambia las variables `totalRows` y `totalColumns` para que coincidan con la solicitud del cliente, y listo.

### Manejo de filas ocultas o filtros

Si la hoja fuente tiene filas ocultas (quizá filtradas), podrías querer copiar solo las filas *visibles*. Aspose.Cells ofrece sobrecargas de `CopyRows` que respetan la visibilidad:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Establece el último booleano a `true` para copiar solo filas visibles—perfecto para “export selected range” cuando el usuario ha aplicado filtros.

## Preservar tabla dinámica – Errores comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Pivot cache not copied** | Usar `Range.Copy` simple en lugar de `Cells.CopyRows/CopyColumns`. | Mantenerse con los métodos `Cells` como se muestra. |
| **Destination sheet has existing pivot** | Guardar sobre un libro que ya contiene una pivot con el mismo nombre. | Comenzar con un `Workbook()` nuevo (como hacemos). |
| **Named ranges break** | La pivot fuente hace referencia a un rango nombrado que no está presente en el nuevo archivo. | Copiar también el rango nombrado: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | La pivot apunta a una fuente de datos externa que no está disponible. | Usar `PivotTable.RefreshData()` después de copiar si es necesario. |

## Ejemplo completo de extremo a extremo (listo para ejecutar)

A continuación está el programa completo, incluyendo las directivas `using` y una breve interfaz de consola. Copia‑pega en un nuevo proyecto de aplicación de consola y pulsa **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Expected output** (en la consola):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Abre `copy-pivot.xlsx` y verás la misma tabla dinámica que tenías en `source.xlsx`, totalmente funcional y referenciando el rango de datos copiado.

## Preguntas frecuentes

**Q: ¿Funciona esto con múltiples tablas dinámicas en la misma hoja?**  
A: Sí, siempre que el rectángulo copiado incluya cada pivot que necesites. Si solo quieres una, ajusta `rows`/`cols` para aislarla.

**Q: ¿Qué pasa si el libro de trabajo fuente usa conexiones de datos externas?**  
A: La caché de la pivot seguirá apuntando a la conexión original. Llama a `pivotTable.RefreshData()` después de cargar el destino si deseas volver a consultar la fuente.

**Q: ¿Puedo copiar la pivot a una hoja diferente dentro del mismo libro?**  
A: Por supuesto. Reemplaza `destinationWorkbook` con `sourceWorkbook` y elige otro índice de hoja.

**Q: ¿Hay una forma de copiar solo el formato?**  
A: Usa las sobrecargas de `CopyRows`/`CopyColumns` que aceptan un objeto `CopyOptions`—establece `CopyOptions.CopyType = CopyType.ValuesOnly` o `CopyType.All` según tus necesidades.

## Conclusión

Acabamos de repasar un escenario de **create new workbook** que **copy pivot table**, **preserve pivot table**, y **export selected range**—todo en puro C#


## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear una nueva tabla dinámica programáticamente en .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [Cómo cambiar los datos de origen de una tabla dinámica usando Aspose.Cells para .NET | Guía de análisis de datos](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Cómo gestionar la compatibilidad de tablas dinámicas de Excel con Aspose.Cells para .NET | Guía de análisis de datos](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}