---
category: general
date: 2026-11-19
description: Establecer formato de moneda en Excel con C# – aprende cómo definir el
  formato numérico y el estilo de las columnas de Excel durante la importación de
  una hoja de cálculo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: es
lastmod: 2026-11-19
og_description: Establece el formato de moneda en Excel con C# y descubre cómo definir
  el formato numérico, asignar el formato de número y dar estilo a las columnas de
  Excel durante la importación de una hoja de cálculo.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Establecer formato de moneda en Excel con C# – guía completa paso a paso
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Establecer formato de moneda al importar datos a Excel usando C#
url: /es/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Establecer formato de moneda al importar datos a Excel con C#

Si necesitas **establecer el formato de moneda** en una hoja de Excel, esta guía te muestra cómo **establecer el formato numérico** y aplicar estilo a las columnas mientras realizas una **importación de hoja de cálculo**. Verás un ejemplo completo y ejecutable que asigna el formato numérico correcto a cada columna de un `DataTable` e importa los datos con el estilo deseado.

Trabajar con Excel desde C# a menudo requiere más que simplemente volcar valores sin procesar; también debes controlar cómo aparecen los números. Ya sea que estés generando facturas, informes financieros o paneles, formatear correctamente moneda, porcentajes o fechas hace que la salida sea instantáneamente legible.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 (o posterior) instalado.  
* Una referencia a **Aspose.Cells for .NET** (o cualquier biblioteca que exponga una clase `Style` con una propiedad `Number`).  
  *NuGet*: `Install-Package Aspose.Cells`.  
* Familiaridad básica con `DataTable` y colecciones de C#.  
* Un IDE como Visual Studio 2022 o VS Code.

## Paso 1: Obtener los datos que se escribirán en la hoja

Primero obtén un `DataTable` que contenga los datos sin procesar que deseas exportar. En proyectos reales esto podría provenir de una consulta a base de datos, una llamada a API o un analizador CSV.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Por qué es importante:** Importar un `DataTable` completamente poblado te permite mantener la lógica de obtención de datos separada de la lógica de generación de Excel, lo que mejora la testabilidad y mantenibilidad.

## Paso 2: Crear una matriz de estilos – una entrada por columna del DataTable

Aspose.Cells espera un `Style[]` cuya longitud coincida con el número de columnas que planeas importar. Cada elemento puede contener un formato numérico específico.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Consejo profesional:** Incluso si solo necesitas formato para un subconjunto de columnas, debes crear una instancia `Style` para cada columna; de lo contrario obtendrás una `NullReferenceException` durante la importación.

## Paso 3: Asignar formato numérico a las columnas deseadas

Los números de estilo incorporados difieren según la biblioteca. En Aspose.Cells:

* `0` → General (entero)  
* `2` → Currency (p. ej., `$#,##0.00`)  
* `3` → Date, etc.

Aquí **asignamos formato numérico** a dos columnas: la primera columna (Id) permanece como entero, mientras que la segunda columna (Amount) recibe un formato de moneda.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Cómo establecer el formato numérico:** Usar la propiedad `Number` es la forma más rápida de elegir un formato incorporado. Para monedas específicas de una localidad, considera usar una cadena de formato personalizada que incluya el símbolo de moneda apropiado.

## Paso 4: Importar el DataTable en la hoja, aplicando los estilos de columna

Ahora que la matriz de estilos está lista, importa los datos. El método `ImportDataTable` respeta los estilos que le pasaste.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Resultado esperado

Al abrir **FinancialReport.xlsx**, verás:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

*La columna **Amount** se muestra usando el formato de moneda que configuraste, mientras que **Id** permanece como entero.*

## Cómo establecer formato numérico para escenarios adicionales

### Asignar formato numérico a columnas de fecha

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Usar formatos numéricos personalizados para porcentajes

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Estilizado más allá de los formatos numéricos

También puedes establecer fuente, color de fondo o alineación en el mismo objeto `Style`:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Por qué funciona:** El objeto `Style` agrupa todas las propiedades visuales de una celda. Cuando pasas la matriz a `ImportDataTable`, cada celda hereda automáticamente el estilo definido.

## Problemas comunes y cómo evitarlos

| Problema | Síntoma | Solución |
|----------|---------|----------|
| Olvidar instanciar cada `Style` | `NullReferenceException` al importar | Recorrer la matriz y llamar a `CreateStyle()` antes de establecer propiedades. |
| Usar el índice numérico incorporado incorrecto | Formato erróneo (p. ej., fechas aparecen como enteros) | Consultar la documentación de la biblioteca para los constantes `Number` correctos. |
| No guardar el libro | Archivo de salida inexistente o vacío | Llamar a `workbook.Save(...)` después de completar la importación. |
| Desajuste de localidad para el símbolo de moneda | `$` aparece incluso en localidades no EE. UU. | Usar una cadena de formato personalizada con el símbolo apropiado (p. ej., `"€#,##0.00"`). |

## Ejemplo completo y ejecutable



## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create excel file c# – style cells and set currency format](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [How to Format Excel Columns in C# – Complete Guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}