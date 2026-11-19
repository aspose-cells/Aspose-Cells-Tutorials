---
category: general
date: 2026-11-19
description: Establezca el formato numérico de la celda en C# y aprenda cómo aplicar
  el formato de fecha de Excel para fechas de era japonesa, lo que permite una conversión
  fiable de fechas de Excel en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: es
lastmod: 2026-11-19
og_description: Establezca el formato numérico de la celda en C# y aplique el formato
  de fecha de Excel a fechas de la era japonesa. Siga esta guía completa para una
  conversión precisa de fechas de Excel en C#.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Establecer el formato numérico de la celda y convertir fechas japonesas
  en C# – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Establecer el formato numérico de la celda y convertir fechas japonesas en
  C#
url: /es/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Establecer formato numérico de celda y convertir fechas japonesas en C#

## Lo que aprenderás

* Cómo crear un libro de trabajo y acceder a su primera hoja.  
* Cómo **establecer formato numérico de celda** para que Excel trate el valor como una fecha.  
* Cómo **aplicar formato de fecha de Excel** que reconozca cadenas de era japonesa.  
* Cómo activar la **conversión de fecha de Excel en C#** recalculando fórmulas.  
* Salida esperada y consejos de solución de problemas para casos límite.

**Prerequisitos**

* .NET 6 o posterior (el código también funciona con .NET Framework 4.6+).  
* Aspose.Cells para .NET 2024 o más reciente – instalar vía NuGet: `dotnet add package Aspose.Cells`.  
* Familiaridad básica con C# y el manejo de fechas en Excel.

> **Consejo profesional:** Aspose.Cells funciona sin que Microsoft Office esté instalado, lo que lo hace ideal para automatización del lado del servidor.

## Establecer formato numérico de celda con Aspose.Cells en C#

El primer paso es indicar a Excel que la celda contiene una fecha. Excel almacena las fechas como números de serie, por lo que debemos aplicar un formato numérico de fecha incorporado (ID 14) a la celda objetivo.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Por qué esto funciona

* `Style.Number = 14` corresponde al formato *Fecha corta* de Excel (`mm/dd/yyyy` por defecto).  
* Cuando la celda contiene una cadena de era japonesa como `R3/04/01`, el analizador interno de Aspose.Cells reconoce la era y la convierte al número de serie gregoriano correspondiente durante `CalculateFormula()`.  
* Después del cálculo, `StringValue` devuelve la fecha gregoriana formateada.

## Aplicar formato de fecha de Excel para fechas de era japonesa

Si deseas que la celda muestre la era japonesa en lugar de la fecha gregoriana, puedes usar un formato numérico personalizado que incluya el código de era. Esto demuestra la capacidad de **aplicar formato de fecha de Excel**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` fuerza la configuración regional japonesa.  
* `ggg` representa el nombre de la era (p. ej., `R` para Reiwa).  
* Agregar caracteres literales (`年`, `月`, `日`) crea un diseño de fecha japonés familiar.

### Cuándo usar un formato personalizado

* Informes dirigidos a audiencias japonesas.  
* Cuando necesitas conservar la información original de la era para documentos legales.  
* En paneles donde se muestran tanto fechas gregorianas como de era lado a lado.

## Conversión de fecha de Excel en C# – manejo de eras japonesas

El proceso de **c# excel date conversion** se puede dividir en tres partes lógicas:

1. **Analizar la cadena de era** – Aspose.Cells reconoce automáticamente `R` (Reiwa), `H` (Heisei), `S` (Showa), etc.  
2. **Convertir a un número de serie** – Excel almacena fechas como días desde 1899‑12‑30.  
3. **Formatear el número de serie** – ya sea con un formato incorporado (ID 14) o un formato japonés personalizado.

### Ejemplo completo de extremo a extremo

A continuación se muestra un programa autocontenido que demuestra tanto la salida gregoriana como la de era en una sola ejecución.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Salida esperada en la consola**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Casos límite y errores comunes

| Situación                              | Qué observar                                   | Solución / Recomendación                                   |
|----------------------------------------|------------------------------------------------|------------------------------------------------------------|
| Cadena de era vacía o malformada       | `PutValue` almacena el texto literal; la conversión falla | Validar la entrada con una expresión regular antes de escribir a la celda. |
| Desajuste de configuración regional    | El formato personalizado muestra dígitos occidentales en lugar de caracteres japoneses | Asegúrate de que el formato `Custom` incluya `[$-ja-JP]` o establece `Workbook.Settings.CultureInfo` a `ja-JP`. |
| El libro contiene fórmulas que hacen referencia a la celda de fecha | La recalculación puede sobrescribir los resultados de la fórmula | Llama a `CalculateFormula` **después** de todos los pasos de formato, o usa `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` si necesitas omitir errores. |
| Uso de versiones antiguas de Aspose.Cells | El soporte de era japonesa se añadió en 2022 Q3 | Actualiza al paquete NuGet más reciente. |

## Probando la solución

1. **Ejecuta el programa** desde Visual Studio o `dotnet run`.  
2. Verifica que la consola imprima la fecha gregoriana `2021‑04‑01` y la cadena de era `R3年04月01日`.  
3. Abre el libro generado (si añades `wb.Save("Demo.xlsx");`) en Microsoft Excel para ver el mismo formato aplicado a las celdas.

### Consejo de automatización

Si necesitas procesar un gran rango de fechas de era (p. ej., la columna A contiene muchas fechas japonesas), envuelve la lógica de conversión en un bucle:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Este enfoque mantiene la operación de **establecer formato numérico de celda** rápida y eficiente en memoria.

## Conclusión

Ahora sabes cómo **establecer formato numérico de celda** en C# usando Aspose.Cells, cómo **aplicar formato de fecha de Excel** para cadenas de era japonesa, y cómo realizar una **conversión de fecha de Excel en C#** confiable de era a fechas gregorianas. El código completo y ejecutable muestra ambas salidas y resalta casos límite comunes.  

**Próximos pasos**

* Explorar otros IDs de formato incorporados


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [establecer formato de fecha de Excel en C# – Guía completa paso a paso](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Cómo aplicar formato numérico en Excel con Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [Cómo aplicar un formato numérico personalizado en Excel en C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}