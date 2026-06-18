---
category: general
date: 2026-06-17
description: Convertir hoja de cálculo a DataTable en C# rápidamente. Aprende cómo
  leer un archivo Excel en DataTable C# y exportar Excel a DataTable C# con código
  real.
draft: false
keywords:
- convert worksheet to datatable
- read excel file into datatable c#
- load excel workbook c#
- export excel to datatable c#
language: es
og_description: Convert worksheet to DataTable in C# fast. This tutorial shows how
  to read Excel file into DataTable C# and export Excel to DataTable C# with a full
  example.
og_title: Convertir hoja de cálculo a DataTable en C# – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Convert worksheet to DataTable in C# quickly. Learn how to read Excel
    file into DataTable C# and export Excel to DataTable C# with real code.
  headline: Convert Worksheet to DataTable in C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Convertir hoja de cálculo a DataTable en C# – Guía completa de programación
url: /es/net/excel-data-import-export/convert-worksheet-to-datatable-in-c-complete-programming-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir hoja de cálculo a DataTable en C# – Guía completa de programación

¿Alguna vez necesitaste **convertir hoja de cálculo a DataTable** pero no sabías qué API llamar? No eres el único—muchos desarrolladores se topan con este obstáculo al automatizar informes o al alimentar datos de Excel a una base de datos. ¿La buena noticia? Con unas pocas líneas de C# puedes leer un archivo Excel en un `DataTable` y estar listo para ejecutar consultas LINQ, inserciones masivas o lo que venga después.

En esta guía recorreremos la carga de un libro de Excel, la extracción de la primera hoja y el **export excel to DataTable C#**—sin trucos, solo código claro. Al final tendrás un método reutilizable que convierte cualquier hoja de cálculo en un `DataTable` totalmente tipado. (Y sí, también cubriremos el escenario de “read Excel file into DataTable C#” para quienes prefieren una sola línea.)

## Prerrequisitos – Lo que necesitarás

Antes de comenzar, asegúrate de tener:

- .NET 6.0 o posterior (el código también funciona en .NET Framework 4.6+)
- Una referencia a **Aspose.Cells** (o cualquier otra biblioteca que ofrezca `ExportDataTable`; el ejemplo usa Aspose porque es sencillo)
- Un archivo Excel (`.xlsx`) que quieras procesar
- Un IDE básico de C# (Visual Studio, Rider o VS Code)

Eso es todo—no se requieren paquetes NuGet adicionales más allá de la biblioteca de Excel. ¿Listo? Vamos allá.

## Paso 1: Cargar el libro de Excel C# – Obtener el archivo en memoria

Lo primero es **load excel workbook c#**. Piensa en el libro como el contenedor que alberga todas las hojas, estilos y metadatos. Abrirlo correctamente garantiza que no bloquees el archivo ni generes fugas de recursos.

```csharp
using Aspose.Cells;
using System.Data;

// Path to your input file – change as needed
string excelPath = @"C:\Data\input.xlsx";

// Load the workbook; the constructor reads the file into memory
Workbook workbook = new Workbook(excelPath);
```

> **Por qué es importante:** La clase `Workbook` abstrae el formato de archivo de bajo nivel, por lo que no tienes que analizar XML tú mismo. Además, libera el flujo subyacente cuando el objeto sale del alcance, evitando errores de archivo en uso.

### Consejo profesional
Si trabajas con hojas de cálculo enormes, considera usar `LoadOptions` para habilitar **carga optimizada en memoria**:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook workbook = new Workbook(excelPath, options);
```

## Paso 2: Acceder a la hoja deseada – Normalmente la primera

La mayoría de los scripts rápidos simplemente toman la primera hoja, pero puedes elegir cualquiera por nombre o índice. Aquí tienes el enfoque clásico de “primera hoja”, que cubre el caso de **convert worksheet to DataTable** para archivos simples.

```csharp
// Grab the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Optional: verify the sheet isn’t empty
if (sheet.Cells.MaxDataRow < 0 || sheet.Cells.MaxDataColumn < 0)
{
    throw new InvalidOperationException("The worksheet appears to be empty.");
}
```

> **Caso límite:** Si tu libro contiene hojas ocultas o necesitas una pestaña específica, reemplaza `0` por `workbook.Worksheets["MySheet"]`.

## Paso 3: Configurar opciones de exportación – Exportar como cadena para tipos predecibles

Al convertir a un `DataTable`, a menudo deseas que cada celda sea una cadena para evitar dolores de cabeza de conversión de tipos más adelante. Eso es exactamente lo que hace la bandera **export excel to datatable c#**.

```csharp
// Set up options so every cell is treated as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true   // forces string output for all cells
};
```

¿Por qué forzar cadenas? Porque las celdas de Excel pueden contener fechas, números o fórmulas. Al exportar todo como texto evitas tipos de columna incompatibles cuando luego insertas los datos en una tabla SQL.

## Paso 4: Realizar la exportación – La lógica central de Convert Worksheet to DataTable

Ahora ocurre la magia. Llamamos a `ExportDataTable` sobre el objeto `Worksheet`, indicando la fila/columna inicial, el total de filas/columnas, una bandera para incluir encabezados de columna y nuestras opciones.

```csharp
// Determine the used range
int totalRows = sheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int totalCols = sheet.Cells.MaxDataColumn + 1;   // +1 for the same reason

// Export the used range to a DataTable
DataTable dataTable = sheet.ExportDataTable(
    0,                 // start row (0‑based)
    0,                 // start column (0‑based)
    totalRows,
    totalCols,
    true,              // include column names as first row
    exportOptions);
```

### Lo que obtienes
`dataTable` ahora refleja la hoja de cálculo:

| Column1 | Column2 | Column3 |
|---------|---------|---------|
| Row1‑A  | Row1‑B  | Row1‑C  |
| Row2‑A  | Row2‑B  | Row2‑C  |
| …       | …       | …       |

Todos los valores son cadenas, lo que hace que el procesamiento posterior sea predecible.

## Paso 5: Verificar el resultado – Comprobación rápida (read excel file into datatable c#)

Una forma rápida de confirmar que la conversión tuvo éxito es volcar las primeras filas en la consola. Esto también muestra el patrón **read excel file into datatable c#** en acción.

```csharp
Console.WriteLine("First 5 rows of the imported DataTable:");
for (int i = 0; i < Math.Min(5, dataTable.Rows.Count); i++)
{
    var row = dataTable.Rows[i];
    Console.WriteLine(string.Join(" | ", row.ItemArray));
}
```

Si ves los valores separados por tuberías esperados, has **convertido la hoja de cálculo a DataTable** con éxito.

## Paso 6: Empaquetar todo – Un método auxiliar reutilizable

La mayoría de los proyectos necesitarán esta conversión en varios lugares, así que empaquetemos todo en un único método estático. Así la llamada **read excel file into datatable c#** será tan simple como una línea.

```csharp
public static DataTable WorksheetToDataTable(string filePath, int sheetIndex = 0, bool exportAsString = true)
{
    // Load the workbook
    Workbook wb = new Workbook(filePath);

    // Grab the requested sheet
    Worksheet ws = wb.Worksheets[sheetIndex];

    // Prepare export options
    ExportTableOptions opts = new ExportTableOptions
    {
        ExportAsString = exportAsString
    };

    // Determine used range
    int rows = ws.Cells.MaxDataRow + 1;
    int cols = ws.Cells.MaxDataColumn + 1;

    // Export and return
    return ws.ExportDataTable(0, 0, rows, cols, true, opts);
}
```

Ejemplo de uso:

```csharp
DataTable myTable = WorksheetToDataTable(@"C:\Data\input.xlsx");
```

Eso es todo—sin bucles extra, sin interop COM, solo datos limpios y tipados.

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Archivo bloqueado por otro proceso** | Abrir el libro sin `LoadOptions` puede mantener abierto el manejador del archivo. | Usa `LoadOptions` con `MemorySetting.MemoryPreference` o envuelve el `Workbook` en un bloque `using`. |
| **Faltan encabezados de columna** | Si la primera fila contiene datos en lugar de encabezados, `ExportDataTable` la tratará como datos. | Pasa `false` al parámetro `includeColumnNames` y agrega los nombres de columna manualmente. |
| **Tipos de datos mixtos provocan excepciones** | Cuando `ExportAsString` es `false`, las celdas numéricas se convierten en `double`, las fechas en `DateTime`. | Mantén `ExportAsString = true` a menos que necesites tipado fuerte, entonces maneja las conversiones tú mismo. |
| **Hojas muy grandes provocan OutOfMemory** | Exportar millones de filas de una vez puede agotar la memoria. | Exporta en bloques: recorre bloques de filas y concatena los `DataTable`. |

## Bonus: Exportar varias hojas a la vez

Si necesitas **export excel to datatable c#** para cada hoja, simplemente itera sobre `workbook.Worksheets`:

```csharp
var tables = new Dictionary<string, DataTable>();
foreach (Worksheet ws in workbook.Worksheets)
{
    tables[ws.Name] = ws.ExportDataTable(
        0, 0,
        ws.Cells.MaxDataRow + 1,
        ws.Cells.MaxDataColumn + 1,
        true,
        exportOptions);
}
```

Ahora `tables` contiene un `DataTable` por hoja, indexado por el nombre de la hoja—útil para importaciones por lotes.

## Conclusión

Te hemos llevado de un archivo Excel vacío a un `DataTable` completamente poblado usando un flujo conciso de **convert worksheet to DataTable**. Los pasos cubrieron la carga del libro, la selección de la hoja, la configuración de opciones de exportación y, finalmente, la extracción de los datos a un `DataTable`. Con el método auxiliar reutilizable ya puedes **read excel file into datatable c#** en cualquier parte de tu código, y también tienes un patrón para **export excel to datatable c#** en múltiples hojas.

¿Qué sigue? Prueba a alimentar el `DataTable` resultante en `BulkInsert` de Entity Framework, generar informes CSV o aplicar filtros LINQ para extraer insights. El cielo es el límite una vez que tus datos de Excel viven en memoria como una tabla adecuada.

¿Tienes preguntas o un archivo Excel complicado que no puedes descifrar? Deja un comentario abajo, ¡y feliz codificación!


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Export Excel Data to DataTable Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}