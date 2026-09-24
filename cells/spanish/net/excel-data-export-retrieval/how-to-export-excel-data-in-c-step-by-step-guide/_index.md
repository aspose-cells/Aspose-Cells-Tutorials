---
category: general
date: 2026-03-21
description: Cómo exportar datos de Excel con nombres de columnas, conservar el formato
  numérico y leer filas específicas usando Aspose.Cells en C#. Aprende a leer la hoja
  de Excel y exportar filas específicas de manera eficiente.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: es
og_description: Cómo exportar datos de Excel con nombres de columna, conservar el
  formato numérico y leer filas específicas usando Aspose.Cells. Un ejemplo completo
  y ejecutable para desarrolladores C#.
og_title: Cómo exportar datos de Excel en C# – Guía completa de programación
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Cómo exportar datos de Excel en C# – Guía paso a paso
url: /es/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo exportar datos de Excel en C# – Guía completa de programación

¿Alguna vez te has preguntado **cómo exportar excel** sin perder el formato original? Tal vez intentaste un rápido copiar‑pegar y terminaste con fechas que aparecen como “44728” o sin encabezados de columna. Eso es frustrante, ¿verdad? En este tutorial verás una forma limpia, de extremo a extremo, de leer una hoja de cálculo de Excel, conservar el formato numérico, exportar con nombres de columnas y, incluso, seleccionar solo las filas que necesitas.

Usaremos la biblioteca Aspose.Cells porque te brinda un control granular sobre las opciones de exportación. Al final de esta guía tendrás un fragmento reutilizable que puedes insertar en cualquier proyecto .NET, y entenderás por qué cada opción es importante. No se requieren documentos externos; todo lo que necesitas está aquí.

---

## Lo que aprenderás

- **Leer la hoja de Excel** en memoria con Aspose.Cells.  
- **Exportar filas específicas** (p. ej., filas 0‑49) manteniendo los nombres de columna.  
- **Conservar el formato numérico** para que monedas, fechas y porcentajes permanezcan intactos.  
- Cómo **exportar con nombres de columna** e incluir comentarios de celda si los necesitas.  
- Un ejemplo completo y listo para ejecutar en C# más consejos para evitar errores comunes.

### Requisitos previos

- .NET 6.0 o superior (el código también funciona con .NET Framework 4.6+).  
- Aspose.Cells para .NET instalado vía NuGet (`Install-Package Aspose.Cells`).  
- Un archivo Excel (`input.xlsx`) colocado en una carpeta a la que puedas referenciar.

> **Consejo profesional:** Si trabajas en una canalización CI, considera obtener el paquete NuGet desde un feed privado para evitar sorpresas de licenciamiento.

---

## Paso 1 – Instalar Aspose.Cells y agregar espacios de nombres

Primero, asegúrate de que el paquete Aspose.Cells esté en tu proyecto. Abre la Consola del Administrador de paquetes y ejecuta:

```powershell
Install-Package Aspose.Cells
```

Luego agrega las directivas `using` requeridas al inicio de tu archivo C#:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Estas importaciones te dan acceso a `Workbook`, `Worksheet`, `ExportTableOptions` y `DataTable`, los componentes esenciales para **leer una hoja de Excel** y exportar datos.

---

## Paso 2 – Cargar el libro (leer el archivo Excel)

Ahora realmente **leemos la hoja de Excel**. El constructor `Workbook` recibe la ruta al archivo, y Aspose.Cells manejará tanto `.xlsx` como los formatos más antiguos `.xls`.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Por qué importa:** Cargar el libro una sola vez y reutilizar el mismo objeto `Worksheet` es mucho más eficiente que abrir el archivo repetidamente, sobre todo con hojas de cálculo grandes.

---

## Paso 3 – Configurar opciones de exportación (conservar formato numérico y nombres de columna)

Aquí le indicamos a Aspose.Cells *cómo* exportar. La clase `ExportTableOptions` permite afinar la salida. Activaremos tres banderas:

1. `ExportAsString = true` – fuerza que cada celda se convierta en cadena, lo que garantiza que los números mantengan su representación visual.  
2. `IncludeCellComments = true` – copia cualquier comentario asociado a las celdas (útil para documentación).  
3. `PreserveNumberFormat = true` – conserva el formato numérico original (símbolos de moneda, patrones de fecha, etc.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Caso límite:** Si estableces `ExportAsString` en `false` pero aún deseas mantener los formatos numéricos, podrías obtener valores numéricos crudos (p. ej., 44728 para una fecha). Mantener ambas banderas activas evita esa sorpresa.

---

## Paso 4 – Obtener la primera hoja (leer hoja de Excel)

La mayoría de los archivos simples tienen los datos que necesitas en la primera hoja, así que la obtendremos por índice. Si necesitas otra hoja, simplemente reemplaza `0` por el índice correspondiente (basado en cero) o usa `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Por qué es útil:** Acceder directamente al objeto `Worksheet` te brinda control total sobre su colección `Cells`, lo cual es esencial para **exportar filas específicas** más adelante.

---

## Paso 5 – Exportar un rango de celdas (exportar filas específicas)

Ahora, el corazón del tutorial: exportar filas 0‑49 y columnas 0‑4 (es decir, las primeras 50 filas y las primeras cinco columnas) a un `DataTable`. También pediremos a Aspose.Cells que incluya los nombres de columna como la primera fila del `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Qué hace esto

- **`startRow: 0`** – comienza en la parte superior de la hoja.  
- **`totalRows: 50`** – captura las primeras 50 filas (**exportar filas específicas**).  
- **`totalColumns: 5`** – limita la exportación a las primeras cinco columnas.  
- **`includeColumnNames: true`** – asegura que los encabezados del `DataTable` coincidan con la fila de encabezado de Excel, cumpliendo el requisito de **exportar con nombres de columna**.  
- **`exportOptions`** – aplica la configuración del Paso 3, de modo que tus valores numéricos sigan viéndose como “$1,234.56” en lugar de “1234.56”.

---

## Paso 6 – Verificar la exportación (cómo se ve el resultado)

Imprimamos las primeras filas en la consola para que veas que el formato se mantuvo.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Salida esperada (ejemplo):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Observa cómo las fechas aparecen en formato `MM/dd/yyyy` y la moneda conserva el símbolo `$`, gracias a **preservar formato numérico**.

---

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| Las fechas se convierten en números grandes | `ExportAsString` quedó en `false` | Mantén `ExportAsString = true` o convierte las celdas manualmente |
| Falta de encabezados de columna | `includeColumnNames` está en `false` | Ponlo en `true` cuando necesites **exportar con nombres de columna** |
| Los comentarios desaparecen | `IncludeCellComments` no está habilitado | Activa `IncludeCellComments` en `ExportTableOptions` |
| Se exporta la hoja equivocada | Usas `Worksheets[0]` en un archivo con varias hojas | Especifica el nombre de la hoja: `workbook.Worksheets["Data"]` |
| Excepción fuera de rango | `totalRows` supera el número real de filas | Usa `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## Bonus: Exportar toda la hoja manteniendo los formatos

Si más adelante decides que necesitas la hoja completa, simplemente reemplaza `totalRows` y `totalColumns` por las dimensiones máximas de la hoja:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Ahora tienes una rutina de **read excel worksheet** que funciona para cualquier tamaño, mientras sigue **preserving number format** y **exporting with column names**.

---

## Ejemplo completo (listo para copiar y pegar)

A continuación tienes el programa completo que puedes colocar en una aplicación de consola. Incluye todos los pasos, importaciones y una verificación simple en pantalla.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Guárdalo como `Program.cs`, ejecuta `dotnet run` y deberías ver la vista previa con formato en tu terminal.

---

## Conclusión

Acabamos de recorrer **cómo exportar excel** usando Aspose.Cells, cubriendo todo desde la carga del libro hasta la preservación del formato numérico, la exportación con nombres de columna y la limitación a filas específicas. El código es autónomo, totalmente ejecutable, e incluye salvaguardas prácticas para los casos límite más comunes.

¿Listo para el siguiente reto? Prueba exportar directamente a CSV manteniendo el formato numérico original, o inserta el `DataTable` en un contexto de Entity Framework Core para inserciones masivas en la base de datos. Ambos escenarios se basan en los mismos fundamentos que cubrimos aquí.

Si encontraste útil esta guía

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}