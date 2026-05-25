---
category: general
date: 2026-03-21
description: Exportar tabla de datos de Excel a un DataTable con encabezados, limitar
  los decimales y exportar las primeras 100 filas usando Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: es
og_description: Aprende cómo exportar una tabla de datos de Excel a un DataTable,
  mantener los encabezados, limitar los decimales y obtener las primeras 100 filas
  en C#.
og_title: Exportar tabla de datos de Excel en C# – Guía paso a paso
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Exportar tabla de datos de Excel en C# – Guía completa
url: /es/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar tabla de datos de Excel – Guía completa en C#

¿Necesitas **exportar tabla de datos de excel** desde un libro de trabajo a un `DataTable` de .NET? Estás en el lugar correcto—esta guía te muestra exactamente cómo hacerlo, mantener los encabezados de columna, limitar los decimales y extraer solo las primeras 100 filas.  

Si alguna vez has mirado una hoja de cálculo y pensado, “¿Cómo llevo esto a mi aplicación sin perder el formato?” no estás solo. En los próximos minutos convertiremos ese “qué‑pasaría” en una solución concreta, lista para copiar y pegar, que funciona con Aspose.Cells, una biblioteca popular para la manipulación de Excel.

## Lo que aprenderás

- Cómo **exportar excel a datatable** usando el método `ExportDataTable`.  
- Cómo mantener los nombres originales de columna (`export excel with headers`).  
- Cómo **limitar los decimales en excel** mediante la configuración de `ExportTableOptions`.  
- Cómo obtener de forma segura solo las primeras 100 filas (`export first 100 rows`).  

Sin scripts externos, sin cadenas mágicas—solo C# puro que puedes insertar en cualquier proyecto .NET.

## Requisitos previos

| Requisito | Por qué es importante |
|-------------|----------------|
| .NET 6 o posterior (o .NET Framework 4.7+) | Aspose.Cells es compatible con ambos, pero los entornos más recientes te ofrecen APIs listas para async. |
| Paquete NuGet Aspose.Cells para .NET | Proporciona `Workbook`, `ExportTableOptions` y el asistente `ExportDataTable`. |
| Un archivo Excel de ejemplo (p.ej., `Numbers.xlsx`) | La fuente de los datos que exportarás. |
| Conocimientos básicos de C# | Seguirás los fragmentos de código, pero no se requiere nada avanzado. |

Si alguno de estos te resulta desconocido, obtén el paquete NuGet con `dotnet add package Aspose.Cells` y crea un pequeño archivo Excel con algunos números—tus datos de prueba.

![ejemplo de exportar tabla de datos de excel](excel-data-table.png "Captura de pantalla de una hoja de Excel que será exportada a un DataTable")

## Paso 1: Cargar el Libro de trabajo (export excel data table)

Lo primero que necesitas es una instancia de `Workbook` que apunte a tu archivo Excel. Piensa en ello como abrir un libro antes de poder leer sus capítulos.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Por qué es importante:** Cargar el libro de trabajo te da acceso a sus hojas, celdas y estilos. Si la ruta del archivo es incorrecta, Aspose lanzará una `FileNotFoundException`, así que verifica la ubicación.

## Paso 2: Configurar opciones de exportación – limit decimal places excel

Por defecto, Aspose exporta cada valor numérico con precisión completa. A menudo solo necesitas un puñado de dígitos significativos, especialmente al alimentar los datos a una cuadrícula UI o a una API que espera números redondeados.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Consejo profesional:** Si necesitas una estrategia de redondeo diferente (p.ej., siempre redondear hacia arriba), puedes post‑procesar el `DataTable` después de la exportación. La configuración `SignificantDigits` es la forma más rápida de **limit decimal places excel** sin escribir bucles adicionales.

## Paso 3: Exportar el rango deseado (export first 100 rows)

Ahora indicamos a Aspose qué bloque de celdas queremos extraer a un `DataTable`. En este tutorial tomamos las primeras 100 filas y las primeras 10 columnas, pero puedes ajustar esos números según tu caso.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Caso límite:** Si la hoja contiene menos de 100 filas, Aspose simplemente exportará lo que exista sin lanzar un error. Sin embargo, podrías querer protegerte contra un rango inesperadamente pequeño:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Paso 4: Verificar el resultado – Volcado rápido en consola

Ver los datos en tu depurador es agradable, pero imprimir algunas filas en la consola confirma que el **export excel to datatable** realmente funcionó y que los decimales están recortados.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Salida esperada

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Observa cómo las columnas numéricas ahora muestran solo cuatro dígitos significativos, coincidiendo con la configuración `SignificantDigits = 4` que aplicamos antes.

## Paso 5: Envolver todo – Un ejemplo completo y ejecutable

A continuación tienes el programa completo que puedes copiar‑pegar en una aplicación de consola. Incluye manejo de errores, la protección opcional del recuento de filas y el método auxiliar para imprimir.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Ejecuta el programa y verás las primeras 100 filas de tu hoja, redondeadas adecuadamente, con los nombres de columna intactos.

## Preguntas frecuentes y trucos

| Pregunta | Respuesta |
|----------|-----------|
| **¿Qué pasa si mi hoja tiene celdas combinadas?** | `ExportDataTable` aplana las celdas combinadas tomando el valor de la celda superior‑izquierda. Si necesitas un manejo personalizado, descombina primero o lee los objetos `Cell` sin procesar. |
| **¿Puedo exportar a un `DataSet` en su lugar?** | Sí—usa `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}