---
category: general
date: 2026-09-27
description: Aprenda cómo copiar una tabla dinámica en C# usando Aspose.Cells. Incluye
  copiar filas con formato, copiar la tabla dinámica a otra hoja y exportar la tabla
  dinámica a un nuevo libro de trabajo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: es
lastmod: 2026-09-27
og_description: Cómo copiar una tabla dinámica en C# usando Aspose.Cells. Sigue la
  guía paso a paso para copiar filas con formato, mover una tabla dinámica a otra
  hoja y exportarla a un nuevo libro de trabajo.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Cómo copiar una tabla dinámica en C# – guía completa de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Cómo copiar una tabla dinámica en C# con Aspose.Cells
url: /es/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica en C# con Aspose.Cells

Si necesitas **copiar una tabla dinámica** de una hoja a otra, aprender **cómo copiar una tabla dinámica** en C# con Aspose.Cells puede ahorrarte horas de trabajo manual. El enfoque también te permite **copiar filas con formato**, mantener intacta la caché de la tabla dinámica e incluso **exportar la tabla dinámica a un nuevo libro** cuando necesitas un archivo independiente.

Este tutorial te guía a través del flujo de trabajo completo:

* crear un libro de trabajo,  
* copiar el rango de la tabla dinámica preservando el formato,  
* colocar los datos copiados en una nueva hoja, y  
* guardar el resultado como un archivo separado.

Verás por qué el método incorporado `CopyRows` es la forma más fiable de **copiar una tabla dinámica a otra hoja**, y obtendrás consejos para manejar casos límite como filas ocultas o fuentes de datos externas.

## Requisitos previos

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later | Aspose.Cells admite .NET 6+ y ofrece el mejor rendimiento. |
| Visual Studio 2022 (or any C# IDE) | Necesitas un editor que pueda restaurar paquetes NuGet. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Esta biblioteca proporciona la API `CopyRows` utilizada en el ejemplo. |
| A source Excel file (`source.xlsx`) that contains a pivot table in the range `A1:G20` | El código copia este rango específico; ajusta el rango si tu tabla dinámica es más grande. |

Instala la biblioteca con la CLI de NuGet o la consola del Administrador de paquetes:

```bash
dotnet add package Aspose.Cells
```

## Paso 1: Cargar el libro de trabajo que contiene la tabla dinámica

La primera línea crea un objeto `Workbook` que representa todo el archivo Excel. Cargar el archivo una vez te brinda acceso de lectura/escritura a cada hoja.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Por qué este paso es importante** – Sin cargar el libro de trabajo, ninguna de las llamadas posteriores a `CopyRows` puede referenciar los datos de origen o la caché de la tabla dinámica.

## Paso 2: Preparar las hojas de origen y destino

Necesitas una hoja de destino donde residirá la tabla dinámica copiada. El código a continuación obtiene la primera hoja (donde se encuentra la tabla dinámica original) y agrega una nueva hoja llamada **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Consejo profesional:** Si la hoja de destino ya existe, llama primero a `Worksheets.RemoveAt(index)` para evitar nombres duplicados.

## Paso 3: Definir el área de celdas que engloba la tabla dinámica

Un objeto `CellArea` describe las celdas superior‑izquierda e inferior‑derecha del rango que deseas mover. En este ejemplo la tabla dinámica ocupa `A1:G20`. Ajusta las coordenadas para tablas más grandes.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Paso 4: Copiar filas con formato y preservar la caché de la tabla dinámica

El método `CopyRows` copia **filas** de la hoja de origen a la hoja de destino. Al pasar `CopyOptions.CopyAll` aseguras que los valores, el formato, los gráficos y los objetos incrustados —todos los cuales forman parte de una tabla dinámica— se transfieran.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Por qué `CopyRows` funciona mejor que `Copy` para tablas dinámicas

* `CopyRows` respeta la caché interna de la tabla dinámica, por lo que la tabla dinámica copiada sigue siendo funcional.
* Preserva **copiar filas con formato** exactamente como aparecen en la hoja original.
* A diferencia de un simple `Copy` de un rango, también mueve filas ocultas y cualquier segmentador asociado.

## Paso 5: Guardar el libro de trabajo con la tabla dinámica copiada

Finalmente, escribe el libro de trabajo modificado en disco. El nuevo archivo contiene la hoja original más una hoja **Copy** que contiene un duplicado totalmente funcional de la tabla dinámica original.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Resultado esperado

Al abrir `pivot_copied.xlsx`:

* La hoja **Sheet1** sigue conteniendo los datos y la tabla dinámica originales.
* La hoja **Copy** muestra una tabla dinámica idéntica con el mismo diseño, filtros y formato.
* Todas las fórmulas y conexiones de datos permanecen intactas porque la caché de la tabla dinámica se copió junto con las filas.

## Cómo copiar una tabla dinámica a otra hoja en el mismo libro

Si solo necesitas la tabla dinámica en otra hoja existente (p.ej., “Report”), reemplaza el paso de creación de la hoja de destino con una referencia a la hoja objetivo:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Este fragmento demuestra **copiar una tabla dinámica a otra hoja** sin crear una nueva hoja de cálculo.

## Exportar tabla dinámica a un nuevo libro

A veces deseas la tabla dinámica en un archivo completamente separado. Después de la operación de copia, puedes eliminar todas las hojas excepto la que contiene la tabla dinámica copiada y luego guardar:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Ahora `pivot_only.xlsx` contiene una sola hoja con la tabla dinámica duplicada, cumpliendo el requisito de **exportar tabla dinámica a un nuevo libro**.

## Cómo copiar filas de Excel sin perder el formato

La misma llamada `CopyRows` funciona para cualquier rango, no solo para tablas dinámicas. Si necesitas **copiar filas de Excel** que incluyan formato condicional, validación de datos o celdas combinadas, usa el mismo método:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Porque `CopyOptions.CopyAll` transfiere todo, las filas de destino se ven exactamente como las filas de origen.

## Errores comunes y cómo evitarlos

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| Source range does not include the whole pivot table | La tabla dinámica copiada aparece truncada. | Verifica que el `CellArea` cubra todas las filas/columnas de la tabla dinámica. |
| Destination sheet already contains data | Las filas sobrescritas provocan pérdida de datos. | Elige una hoja nueva o comienza a copiar en un índice de fila más alto. |
| Pivot table uses an external data source | La copia pierde su conexión. | Después de copiar, llama a `pivotTable.RefreshData()` para restablecer el vínculo. |
| Hidden rows are omitted | Algunas filas desaparecen en la copia. | `CopyRows` copia automáticamente las filas ocultas; asegúrate de no estar usando `CopyOptions.CopyValuesOnly`. |

## Ejemplo completo y ejecutable

A continuación tienes un programa autónomo que puedes pegar en un nuevo proyecto de consola. Demuestra cada paso discutido arriba.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Ejecutar el programa** crea `pivot_copied.xlsx` con un duplicado de la tabla dinámica original en una nueva hoja llamada **Copy**.

## Conclusión

Ahora sabes **cómo copiar una tabla dinámica** en C# usando

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear nuevo libro – Cómo copiar una hoja con una tabla dinámica](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copiar tabla dinámica en C# – Guía completa paso a paso](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Cómo copiar un rango con tablas dinámicas en C# – Guía completa](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}