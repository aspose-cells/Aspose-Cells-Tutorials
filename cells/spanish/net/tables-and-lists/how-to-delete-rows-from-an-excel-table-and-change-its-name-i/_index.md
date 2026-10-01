---
category: general
date: 2026-10-01
description: Aprende a eliminar filas de una tabla de Excel y cambiar el nombre de
  la tabla de Excel usando C#. Guía paso a paso con código completo y buenas prácticas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: es
lastmod: 2026-10-01
og_description: Eliminar filas de una tabla de Excel y cambiar el nombre de la tabla
  de Excel en C#. Sigue este tutorial completo para cargar un libro, modificar la
  tabla y guardar el resultado.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: Eliminar filas de una tabla de Excel y cambiar su nombre en C# – guía completa
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Cómo eliminar filas de una tabla de Excel y cambiar su nombre en C#
url: /es/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo eliminar filas de una tabla de Excel y cambiar su nombre en C#

Si necesita **eliminar filas de una tabla de Excel** mientras trabaja con C#, esta guía muestra los pasos exactos requeridos. Verá cómo **cargar un libro de Excel en C#**, eliminar filas específicas de una tabla y luego **actualizar el nombre de la tabla de Excel** para que el archivo permanezca consistente.

El tutorial cubre todo lo que necesita saber: paquetes NuGet requeridos, código completo ejecutable y problemas comunes como violaciones de la estructura de la tabla. Al final del artículo podrá modificar cualquier tabla de Excel programáticamente sin intervención manual.

## Requisitos previos

Antes de comenzar, asegúrese de tener:

* .NET 6.0 SDK o posterior instalado.
* Visual Studio 2022 (o cualquier IDE de C#) configurado para desarrollo .NET.
* La biblioteca **Aspose.Cells for .NET** añadida vía NuGet (`Install-Package Aspose.Cells`).
* Un libro de Excel existente (`Table.xlsx`) que contenga al menos una hoja de cálculo con una tabla.

Estos elementos proporcionan el entorno necesario para **cargar el libro de Excel c#** y ejecutar las operaciones de manera fiable.

## Paso 1: Cargar el libro que contiene la tabla

La primera operación es abrir el archivo del libro. Aspose.Cells lee todo el libro en memoria, dándole control total sobre hojas de cálculo, tablas y datos de celdas.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Por qué es importante*: Cargar el libro es la base para cualquier manipulación de tabla posterior. El objeto `Workbook` expone la colección `Worksheets`, que usará para localizar la tabla objetivo.

## Paso 2: Acceder a la primera hoja y a su primera tabla

La mayoría de los archivos de Excel almacenan tablas en la primera hoja, pero puede ajustar el índice si es necesario. El siguiente código recupera el primer objeto `Table`.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

Si la hoja no contiene una tabla, `sheet.Tables.Count` será cero y deberá manejar ese caso. Intentar acceder a `sheet.Tables[0]` cuando no existen tablas lanza una excepción, por lo que se recomienda una cláusula de protección en código de producción.

## Paso 3: Eliminar filas de la tabla de Excel

Para **eliminar filas de una tabla de Excel**, llame a `DeleteRows(startRow, totalRows)`. El parámetro `startRow` es basado en cero relativo a la primera fila de datos de la tabla (la fila después del encabezado).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### ¿Por qué usar `DeleteRows` en lugar de eliminar filas de la hoja?

`DeleteRows` actualiza el rango interno de la tabla, preservando fórmulas, estilos y nombres definidos que pertenecen a la tabla. Eliminar directamente filas de la hoja podría romper la estructura de la tabla y generar una excepción.

**Caso límite**: Si la eliminación dejara la tabla sin filas de datos, Aspose.Cells lanza una `ArgumentException`. Prevenga esto verificando `table.RowCount` antes de la eliminación.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## Paso 4: Cambiar el nombre de la tabla de Excel

Después de eliminar filas, puede querer dar a la tabla un identificador más descriptivo. La propiedad `Name` establece el nombre definido de la tabla, que se usa en fórmulas y VBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*¿Por qué renombrar?* Un nombre de tabla claro mejora la legibilidad en fórmulas (`=SUM(SalesData2026[Amount])`) y evita colisiones de nombres cuando varias tablas comparten propósitos similares.

## Paso 5: Guardar el libro modificado (opcional)

Persista los cambios guardando en un archivo nuevo o sobrescribiendo el original. Guardar en una nueva ubicación es más seguro durante el desarrollo.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

El método `Save` escribe el libro actualizado, incluyendo el rango de tabla modificado y el nuevo nombre de tabla, en el disco.

## Ejemplo completo en funcionamiento

Unir todos los pasos produce un programa autónomo que puede ejecutar inmediatamente.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**Salida esperada** (asumiendo que el archivo y la tabla existen):

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

Ejecutar el programa actualiza el archivo de Excel exactamente como se describe: se eliminan filas, el nombre de la tabla cambia y el resultado se guarda sin edición manual.

## Preguntas frecuentes y solución de problemas

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué ocurre si la tabla abarca celdas combinadas?* | `DeleteRows` respeta los rangos combinados. Si una celda combinada cruza el límite de eliminación, Aspose.Cells ajusta automáticamente la combinación. Verifique el resultado visualmente si depende de combinaciones complejas. |
| *¿Puedo eliminar filas de una tabla que forma parte de una caché de tabla dinámica?* | Eliminar filas de una tabla origen que alimenta una tabla dinámica **no** actualiza automáticamente la caché de la tabla dinámica. Llame a `pivotTable.RefreshData()` después de modificar la tabla origen. |
| *¿Es posible eliminar filas basándose en una condición (p. ej., valor < 0)?* | Sí. Itere a través de `table.ListObjects` o `table.Rows` para localizar las filas coincidentes, luego recopile sus índices y llame a `DeleteRows` para cada rango. |
| *¿Necesito disponer del objeto `Workbook`?* | `Workbook` implementa `IDisposable`. Envuélvalo en un bloque `using` para liberar los recursos de forma determinista, especialmente al procesar archivos grandes. |
| *¿En qué se diferencia de usar EPPlus?* | EPPlus también soporta la manipulación de tablas pero usa una API diferente (`ExcelTable`). Los conceptos de cargar un libro, eliminar filas y renombrar la tabla son análogos. Elija la biblioteca que se ajuste a sus requisitos de licencia. |

## Mejores prácticas al modificar tablas de Excel en C#

* **Validar índices** – Los índices de filas de la tabla son basados en cero; los errores de off‑by‑one provocan eliminaciones inesperadas.
* **Comprobar colisiones de nombres** – Excel no permite nombres definidos duplicados; siempre verifique la unicidad antes de asignar un nuevo nombre.
* **Respaldar archivos originales** – Los scripts automatizados pueden corromper datos; mantenga una copia del libro origen.
* **Usar sentencias `using`** – Garantiza que los manejadores de archivo se liberen rápidamente:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **Probar con casos límite** – Tablas con una sola fila de datos, tablas que abarcan toda la hoja y tablas vinculadas a gráficos deben verificarse después de los cambios.

## Conclusión

Ahora sabe cómo **eliminar filas de una tabla de Excel** y **cambiar el nombre de la tabla de Excel** usando C#. La solución completa carga el libro, accede a la tabla objetivo, elimina las filas deseadas, renombra la tabla y guarda el resultado. Aplique estas técnicas para automatizar la generación de informes, la limpieza de datos o cualquier flujo de trabajo que requiera gestión programática de tablas de Excel.

A continuación, explore temas relacionados como **actualizar valores de celdas en una tabla de Excel**, **agregar nuevas filas programáticamente** y **exportar datos de tabla a CSV**. Dominar estas operaciones le dará control total sobre los archivos de Excel desde sus aplicaciones C#.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar características adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo renombrar una tabla en Excel con C# – Guía paso a paso](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Crear tabla de Excel en C# – Guía paso a paso](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Obtener la primera tabla de un libro de Excel en C# – Guía completa](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}