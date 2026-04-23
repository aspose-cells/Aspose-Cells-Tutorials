---
category: general
date: 2026-02-09
description: Limpia la interfaz de filtro en Excel con C# eliminando el botón AutoFilter.
  Aprende cómo ocultar el botón de filtro, mostrar la fila de encabezado y mantener
  tus hojas ordenadas.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: es
og_description: Interfaz de filtro limpia en Excel usando C#. Esta guía muestra cómo
  ocultar el botón de filtro, mostrar la fila de encabezado y mantener las hojas de
  cálculo limpias.
og_title: Interfaz para borrar filtros en Excel con C# – Eliminar el botón AutoFilter
tags:
- excel
- csharp
- epplus
- automation
title: Interfaz para borrar filtros en Excel con C# – Eliminar el botón AutoFilter
url: /es/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Interfaz de filtro clara en Excel con C# – Eliminar el botón AutoFilter

¿Alguna vez necesitaste **clear filter UI** en una hoja de Excel pero no estabas seguro de qué línea de código oculta esa pequeña flecha desplegable? No eres el único. El botón de filtro puede ser una molestia cuando envías un informe a los usuarios finales que nunca necesitan cambiar la vista.  

En este tutorial recorreremos un ejemplo completo y ejecutable que **removes the AutoFilter button** de una tabla, asegura que la fila de encabezado permanezca visible, y también aborda cómo *hide filter button* de forma permanente. Al final sabrás exactamente **how to remove AutoFilter** en C# y por qué cada paso es importante.

## Lo que necesitarás

- .NET 6+ (or .NET Framework 4.7.2+) – cualquier runtime reciente funciona.
- The **EPPlus** NuGet package (version 6.x or later) – nos proporciona `ExcelWorksheet`, `ExcelTable`, etc.
- Un archivo Excel sencillo con una tabla llamada **SalesTable** (siéntete libre de crear una en unos pocos clics).

Eso es todo. Sin interop COM, sin DLLs adicionales, solo un puñado de declaraciones `using` y unas pocas líneas de código.

## Interfaz de filtro clara: Eliminando el botón AutoFilter

El núcleo de la solución se encuentra en tres pequeñas sentencias. Desglosemoslas para que comprendas *por qué* son necesarias, no solo *qué* hacen.

### Paso 1 – Obtener una referencia a la tabla

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Por qué es importante: EPPlus trabaja con **tables** (`ExcelTable`), no con rangos sin formato. Al obtener el objeto de tabla obtenemos acceso a la propiedad `AutoFilter`, que controla el elemento UI que ves en la hoja. Si intentas manipular la hoja directamente, solo afectarás los valores, no el botón de filtro.

### Paso 2 – Eliminar la fila del botón AutoFilter

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Establecer `AutoFilter` a `null` indica a EPPlus que elimine la fila de filtro subyacente. Esta es la operación *clear filter UI* que la mayoría de los desarrolladores buscan cuando preguntan “**how to remove autofilter**”. Es un enfoque limpio de una sola línea que funciona en cualquier versión de Excel que EPPlus soporte.

### Paso 3 – Mantener visible la fila de encabezado

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Cuando eliminas la UI del filtro, Excel a veces puede ocultar la fila de encabezado si la bandera `ShowHeader` de la tabla es false. Al establecerla explícitamente a `true` garantizamos que los títulos de columna permanezcan en pantalla – un detalle sutil pero importante para un informe final pulido.

### Ejemplo completo y ejecutable

A continuación se muestra una aplicación de consola mínima que abre un libro de trabajo existente, ejecuta los tres pasos y guarda el resultado. Copia‑pega, pulsa **F5**, y observa cómo desaparece el botón de filtro.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Resultado esperado:** Abre *SalesReport_NoFilter.xlsx* – las flechas de filtro han desaparecido, pero los encabezados de columna permanecen. No más desorden de UI “click‑to‑filter”.

> **Consejo profesional:** Si tienes **multiple tables** y deseas ocultar el botón de filtro para todas ellas, recorre `worksheet.Tables` y aplica las mismas tres líneas dentro del bucle.

## Cómo eliminar AutoFilter en Excel usando C# – una inmersión más profunda

Podrías preguntarte, “¿Qué pasa si el libro de trabajo ya tiene un filtro aplicado? ¿Establecer `AutoFilter = null` también elimina las filas filtradas?” La respuesta es **yes**. EPPlus elimina tanto la UI como los criterios de filtro subyacentes, dejando los datos en su orden original.  

Si solo deseas *hide* el botón pero mantener el filtro activo, puedes en su lugar establecer la propiedad `AutoFilter` a un **new empty filter**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Esa variación es útil cuando deseas *hide filter button* para una apariencia pulida pero aún permitir que usuarios avanzados activen los filtros mediante VBA o la cinta de opciones.

### Caso límite: Tablas sin fila de encabezado

Algunos informes heredados usan rangos simples en lugar de tablas. En ese caso, EPPlus no expondrá un objeto `ExcelTable`, por lo que el código anterior lanzará una excepción. La solución es **convert the range to a table** primero:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Ahora has *removed autofilter excel* estilo UI incluso en un rango que comenzó sin una tabla formal.

## Mostrar la fila de encabezado después de ocultar el botón de filtro – por qué es importante

Una queja común es que después de ocultar la UI del filtro, la fila de encabezado a veces desaparece, especialmente cuando el libro de trabajo se creó originalmente con “Hide Header” activado. Al establecer explícitamente `salesTable.ShowHeader = true;` evitamos esa sorpresa.  

Si alguna vez necesitas **hide filter button** pero mantener el encabezado oculto (quizás estés generando un volcado de datos sin procesar), simplemente establece `salesTable.ShowHeader = false;` después de limpiar el filtro. El código es simétrico, lo que facilita alternar según una bandera de configuración.

## Ocultar el botón de filtro – consejos prácticos y trampas

- **Version compatibility:** EPPlus 6+ funciona solo con archivos `.xlsx`. Si trabajas con el formato antiguo `.xls`, necesitarás una biblioteca diferente (p. ej., NPOI) porque la API *clear filter UI* no está disponible.
- **Performance:** Cargar un libro de trabajo enorme solo para ocultar un botón puede ser lento. Considera usar `ExcelPackage.Load(stream, true)` para abrir en modo **read‑only**, aplicar el cambio y luego guardar.
- **Testing:** Siempre valida el archivo de salida manualmente la primera vez. Las pruebas automatizadas de UI pueden verificar que las flechas de filtro realmente hayan desaparecido (`worksheet.Tables[0].AutoFilter == null`).
- **Licensing:** EPPlus cambió a una licencia dual en la versión 5. Para proyectos comerciales necesitarás una licencia paga o cambiar a una biblioteca alternativa.

## Archivo fuente completo para copiar‑pegar

A continuación se muestra el archivo exacto que puedes colocar en un nuevo proyecto de consola. Sin dependencias ocultas, todo está auto‑contenid​o.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Ejecuta `dotnet add package EPPlus --version 6.0.8` (o la última) antes de compilar, y tendrás una hoja limpia lista para distribución.

## Conclusión

Acabamos de mostrarte **how to remove AutoFilter** y **clear filter UI** en un libro de Excel usando C#. El núcleo de tres líneas (`AutoFilter = null;`, `ShowHeader = true;`) realiza el trabajo pesado, mientras que el código auxiliar que lo rodea hace que la solución

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}