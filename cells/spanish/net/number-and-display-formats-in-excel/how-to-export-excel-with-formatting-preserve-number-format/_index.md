---
category: general
date: 2026-03-22
description: Cómo exportar Excel con formato y preservar el formato numérico. Aprende
  a convertir un rango de Excel, obtener el resultado de una fórmula y exportar Excel
  con formato usando Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: es
og_description: Cómo exportar Excel con formato y conservar el formato numérico. Guía
  paso a paso para convertir un rango de Excel, obtener el resultado de la fórmula
  y exportar Excel con formato en C#.
og_title: Cómo exportar Excel con formato – Conservar el formato numérico
tags:
- C#
- Aspose.Cells
- Excel automation
title: Cómo exportar Excel con formato – Conservar el formato numérico
url: /es/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo exportar Excel con formato – conservar el formato numérico

¿Alguna vez te has preguntado **cómo exportar Excel** manteniendo el aspecto de cada celda exactamente como lo ves en el libro? Tal vez necesites enviar un informe a un cliente, alimentar un control de cuadrícula o simplemente almacenar los valores en una base de datos. El problema habitual es la pérdida del formato numérico o que las fórmulas se conviertan en cadenas crudas.  

En este tutorial recorreremos un ejemplo completo, listo‑para‑ejecutar en C# que **conserva el formato numérico**, **convierte un rango de Excel** a un `DataTable`, **obtiene el resultado de la fórmula**, y finalmente **exporta Excel con formato** usando Aspose.Cells. Al final tendrás un método único que puedes insertar en cualquier proyecto y llamar con una referencia a la hoja de cálculo.

> **Vista rápida:** el código crea un libro de trabajo, escribe un valor y una fórmula, indica a Aspose.Cells que exporte las celdas como cadenas formateadas, y muestra `123.456 | 246.912` – exactamente lo que esperarías ver en Excel.

---

## Lo que necesitarás

- **Aspose.Cells for .NET** (la versión de prueba gratuita funciona bien para aprender)
- .NET 6.0 o posterior (la API es la misma en .NET Framework)
- Un entorno básico de desarrollo C# (Visual Studio, VS Code, Rider… tú eliges)

No se requieren paquetes NuGet adicionales más allá de Aspose.Cells. Si aún no lo has instalado, ejecuta:

```bash
dotnet add package Aspose.Cells
```

---

## Paso 1 – Crear un libro de trabajo y escribir valores (incluyendo una fórmula)

Primero creamos un libro de trabajo nuevo y colocamos un valor numérico en **A1**. Luego añadimos una fórmula sencilla en **B1** que multiplica la primera celda por dos. Esto prepara el escenario para demostrar **obtener el resultado de la fórmula** más adelante.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Por qué es importante:**  
- `PutValue` almacena el número bruto, mientras que `PutFormula` almacena el cálculo.  
- Aspose.Cells mantiene la fórmula **activa**, de modo que cuando más tarde solicitemos el valor de la celda obtendremos realmente `246.912`, no la cadena `"=A1*2"`.

---

## Paso 2 – Indicar a Aspose.Cells que exporte los valores como cadenas formateadas

Si simplemente llamas a `ExportDataTable` con la configuración predeterminada, las celdas numéricas se devolverán como sus valores subyacentes `double`. Eso elimina los separadores de miles, símbolos de moneda o decimales personalizados que hayas configurado. La clase `ExportTableOptions` nos permite **conservar el formato numérico** y **exportar como cadena**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Punto clave:** `ExportNumberFormat = true` es la bandera que hace que **conservar el formato numérico** funcione. Sin ella verías `"123.456"` y `"246.912"` como números crudos, lo que puede verse bien en código pero no cuando pegas los datos en una UI que espera el mismo formato que Excel.

---

## Paso 3 – Imprimir los datos exportados (verificación)

Ahora que tenemos un `DataTable` lleno de cadenas formateadas, volcamos su contenido a la consola. Esto también demuestra que hemos **obtenido el resultado de la fórmula** sin evaluar la fórmula nosotros mismos.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Ejecutar el programa muestra:

```
123.456 | 246.912
```

Observa cómo la segunda columna muestra el **resultado de la fórmula**, no el texto de la fórmula. Eso es exactamente lo que necesitas cuando **exportas Excel con formato** para procesamiento posterior.

---

## Paso 4 – Convertir rangos de Excel más grandes (opcional)

El ejemplo anterior maneja una pequeña porción `A1:B1`, pero los escenarios del mundo real a menudo requieren exportar tablas completas. El mismo método funciona para cualquier bloque rectangular – solo ajusta los argumentos `firstRow`, `firstColumn`, `totalRows` y `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Consejo profesional:** Si tu hoja ya tiene una fila de encabezado, establece `includeColumnNames` en `true`. Aspose.Cells usará la primera fila del rango como nombres de columna, lo cual es útil cuando luego enlazas el `DataTable` a una cuadrícula de UI.

---

## Paso 5 – Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Los números pierden comas o símbolos de moneda** | `ExportAsString` es `false` o `ExportNumberFormat` está omitido | Establece tanto `ExportAsString = true` **como** `ExportNumberFormat = true`. |
| **Las celdas con fórmula devuelven el texto de la fórmula** | No llamaste a `CalculateFormula` antes de exportar (solo necesario si el libro no está configurado para auto‑calcular) | Activa el auto‑cálculo (`workbook.CalculateFormula()`) o confía en `ExportAsString` que fuerza la evaluación. |
| **Los encabezados aparecen como filas de datos** | `includeColumnNames` está configurado como `false` mientras tu rango incluye una fila de encabezado | Establece `includeColumnNames = true` para tratar la primera fila como nombres de columna. |
| **Los rangos grandes provocan presión de memoria** | Exportar toda la hoja de una vez carga todo en memoria | Exporta en bloques (p.ej., 500 filas a la vez) y combina los `DataTable`s si es necesario. |

---

## Paso 6 – Ejemplo completo listo para copiar y pegar

A continuación tienes el programa completo, desde las sentencias `using` hasta `Main`. Pégalo en una aplicación de consola y pulsa **F5** – verás la salida formateada al instante.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Salida esperada**

```
123.456 | 246.912

Press any key to exit...
```

Ese es todo el flujo de **cómo exportar Excel**, con el formato intacto, resultados de fórmulas evaluados y un `DataTable` limpio listo para cualquier consumidor .NET.

---

## Conclusión

Hemos cubierto todo lo que necesitas saber sobre **cómo exportar Excel** manteniendo **el formato numérico**, **convirtiendo un rango de Excel** a un `DataTable`, y **obteniendo resultados de fórmulas** sin análisis adicional. La clave es la configuración de `ExportTableOptions` – una vez que estableces `ExportAsString` y `ExportNumberFormat` en `true`, Aspose.Cells hace el trabajo pesado por ti.

A partir de aquí puedes:

- Insertar el `DataTable` en un `DataGrid` de WPF o en una vista ASP.NET MVC.  
- Escribir la tabla a un archivo CSV manteniendo la representación visual exacta.  
- Extender el enfoque a múltiples hojas o rangos dinámicos.

Siéntete libre de experimentar con diferentes formatos (moneda, porcentajes) y bloques de datos más grandes. Si encuentras alguna anomalía, vuelve a consultar la tabla de **problemas comunes**, que cubre los contratiempos más frecuentes al **exportar Excel con formato**.

¡Feliz codificación, y que tus hojas de cálculo exportadas siempre luzcan tan pulidas como los originales!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}