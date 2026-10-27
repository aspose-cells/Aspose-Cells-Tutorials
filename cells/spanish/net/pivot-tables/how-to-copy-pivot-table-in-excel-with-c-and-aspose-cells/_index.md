---
category: general
date: 2026-10-04
description: Aprende cómo copiar una tabla dinámica de un libro a otro usando C#.
  Esta guía también cubre cómo copiar filas, duplicar la tabla dinámica y copiar rangos
  de Excel de manera eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: es
lastmod: 2026-10-04
og_description: Copiar tabla dinámica en Excel usando C#. Sigue este tutorial completo
  para duplicar tablas dinámicas, copiar filas y copiar rangos de Excel con Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: Copiar tabla dinámica en Excel con C# – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cómo copiar una tabla dinámica en Excel con C# y Aspose.Cells
url: /es/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica en Excel con C# y Aspose.Cells

Si necesitas **copiar una tabla dinámica** de un libro a otro, este tutorial te muestra una solución completa y ejecutable. Verás exactamente cómo cargar un archivo de origen, definir el rango que contiene la tabla dinámica, copiar las filas (incluida la definición de la tabla dinámica) y guardar el resultado. Ya sea que estés automatizando una canalización de informes o construyendo una herramienta de migración, los pasos a continuación te permiten duplicar una tabla dinámica con solo unas pocas líneas de C#.

Copiar una tabla dinámica es más que copiar valores de celdas; la caché subyacente y la configuración de los campos deben viajar juntas. El ejemplo usa la biblioteca **Aspose.Cells** porque maneja automáticamente los metadatos de la tabla dinámica, de modo que no tienes que reconstruir la caché manualmente. Al final de esta guía podrás **cómo copiar una tabla dinámica**, **copiar rango de Excel** y **cómo copiar filas** de forma segura.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

- .NET 6.0 o posterior instalado (el código también funciona con .NET Framework 4.7+).
- Una licencia válida de Aspose.Cells for .NET o una licencia de evaluación temporal.
- Dos archivos Excel: `Source.xlsx` que contiene la tabla dinámica que deseas duplicar, y una carpeta vacía donde se escribirá `CopyWithPivot.xlsx`.
- Visual Studio 2022 (o cualquier IDE que soporte C#).

## Paso 1: Configurar el proyecto y agregar Aspose.Cells

Crea un nuevo proyecto de consola y agrega el paquete NuGet Aspose.Cells:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

El paquete proporciona las clases `Workbook`, `Worksheet` y `CellArea` que se usan en el código a continuación.

## Paso 2: Cargar el libro de origen que contiene la tabla dinámica

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Por qué es importante:** Cargar el libro crea una representación en memoria de todas las hojas, incluidas las cachés de tabla dinámica ocultas. Sin cargar el archivo, no puedes referenciar el rango de la tabla dinámica.

## Paso 3: Definir el área de celdas que cubre la tabla dinámica

Debes indicar a Aspose.Cells qué filas y columnas pertenecen a la tabla dinámica. La estructura `CellArea` te permite especificar un bloque rectangular.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Consejo:** Si no estás seguro del tamaño exacto, abre el archivo de origen en Excel, selecciona la tabla dinámica y observa el rango que se muestra en el cuadro de nombres (p. ej., `A1:K31`). Convierte las coordenadas de Excel a índices basados en cero para el código.

## Paso 4: Crear un nuevo libro de destino y obtener su primera hoja

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Por qué se requiere este paso:** El libro de destino debe existir antes de que puedas copiar filas. Aspose.Cells crea automáticamente una hoja de cálculo predeterminada, que utilizaremos como objetivo.

## Paso 5: Copiar las filas (incluida la tabla dinámica) del origen al destino

El método `CopyRows` copia tanto los valores de celda como la caché subyacente de la tabla dinámica.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **Cómo funciona:**  
> - `CopyRows` recibe la hoja de origen, la fila inicial y la cantidad de filas a copiar.  
> - También recibe la hoja de destino y la fila donde debe comenzar la copia.  
> - Como el rango de origen incluye la tabla dinámica, el método transfiere la caché, la lista de campos y el diseño de la tabla dinámica intactos. Este es el núcleo de **cómo copiar una tabla dinámica** sin perder funcionalidad.

### Caso límite: copiar una tabla dinámica que abarca varias hojas

Si los datos de origen de la tabla dinámica están en una hoja diferente a la de la propia tabla, la caché sigue la copia porque Aspose.Cells almacena la caché en el libro, no en la hoja. Sin embargo, debes asegurarte de que el libro de destino contenga el mismo rango de datos de origen; de lo contrario, la tabla mostrará errores `#REF!`. En esos casos, copia primero el rango de datos de origen y luego las filas de la tabla dinámica.

## Paso 6: Guardar el libro que ahora contiene la tabla dinámica copiada

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Ejecutar el programa genera `CopyWithPivot.xlsx` con una réplica exacta de la tabla dinámica original, incluidas todas las segmentaciones, filtros y campos calculados.

### Resultado esperado

Al abrir `CopyWithPivot.xlsx`:

- La tabla dinámica aparece en la misma posición (p. ej., A1:K31) que en `Source.xlsx`.
- Todas las etiquetas de filas y columnas, totales y formato se conservan.
- Al actualizar la tabla dinámica se muestra la misma información que la fuente, confirmando que la caché se copió correctamente.

## Cómo copiar filas sin una tabla dinámica (copiar rango de Excel)

Si solo necesitas **copiar rango de Excel** sin datos de tabla dinámica, puedes usar el mismo método `CopyRows` pero apuntar a un rango que no contenga una tabla dinámica. Por ejemplo:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

Esto demuestra **cómo copiar filas** para datos genéricos, reforzando la versatilidad de la misma API.

## Duplicar tabla dinámica en el mismo libro (enfoque alternativo)

A veces deseas **duplicar tabla dinámica** dentro del mismo libro en lugar de crear un archivo nuevo. Puedes lograrlo copiando filas a una ubicación diferente:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

Después de guardar, el libro contendrá dos tablas dinámicas idénticas, útil para comparaciones lado a lado o para crear copias de seguridad.

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| La tabla dinámica muestra `#REF!` después de copiar | El rango de datos de origen no está presente en el libro de destino | Copia primero el rango de datos de origen, o usa `CopyRows` en la hoja de datos antes de copiar la tabla dinámica |
| Se pierde el formato | Solo se copiaron valores (p. ej., usando `Copy` en lugar de `CopyRows`) | Usa siempre `CopyRows`, que preserva estilos, formato y metadatos de la tabla dinámica |
| Desplazamiento inesperado de filas | La fila de inicio en el destino no coincide con la fila de inicio en el origen | Verifica que la fila de inicio de `destWorksheet.Cells` coincida con la ubicación deseada |
| Libros grandes generan presión de memoria | `CopyRows` carga hojas completas en memoria | Procesa la copia en fragmentos o usa APIs de streaming si trabajas con más de 100 000 filas |

## Ejemplo completo y ejecutable

A continuación tienes el programa completo que puedes pegar en `Program.cs` y ejecutar de inmediato (reemplaza `YOUR_DIRECTORY` por una ruta real en tu máquina).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Ejecuta el programa con `dotnet run`. Después de la ejecución, abre `CopyWithPivot.xlsx` para verificar que la tabla dinámica aparece exactamente como en el archivo de origen.

## Conclusión

Ahora sabes **cómo copiar una tabla dinámica** de un libro de Excel a otro usando C# y Aspose.Cells. La guía cubrió todo el flujo de trabajo: cargar el archivo de origen, definir el área de la tabla dinámica, copiar filas y guardar el libro de destino. También aprendiste **cómo copiar filas**, **copiar rango de Excel** y **duplicar tabla dinámica** dentro del mismo archivo, además de los problemas habituales y consejos de mejores prácticas.

¿Listo para el siguiente paso? Prueba agregar código para actualizar programáticamente la tabla dinámica copiada, o explora exportar la tabla a PDF con Aspose.Cells. Experimenta con diferentes rangos de origen y dominarás rápidamente la automatización de Excel en .NET.

---


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copy rows excel – Preserve Pivot Table While Duplicating Rows](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}