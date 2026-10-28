---
category: general
date: 2026-09-18
description: Aprende a expandir una matriz en Excel usando la función EXPAND, a rellenar
  una plantilla de Excel y a crear una hoja de cálculo de Excel con un rango dinámico
  mediante C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: es
lastmod: 2026-09-18
og_description: Cómo expandir una matriz en Excel con la función EXPAND, rellenar
  una plantilla de Excel y crear una solución de rango dinámico en Excel utilizando
  código C#.
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: Cómo expandir una matriz en Excel y rellenar una plantilla
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Cómo expandir una matriz en Excel y rellenar una plantilla
url: /es/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo expandir una matriz en Excel y rellenar una plantilla

Si necesitas **cómo expandir una matriz** en Excel mientras rellenas una plantilla pre‑diseñada, esta guía te muestra una solución completa, de extremo a extremo. Usando la función `EXPAND` junto con los Smart Markers de Aspose.Cells, puedes convertir una única referencia de celda en un rango de 5 × 5 y reemplazar automáticamente marcadores como `{IsActive}` con datos en tiempo real.

Verás cómo **populate excel template**, crear un **dynamic range excel**, y usar correctamente **use expand function** en un proyecto C#. Al final del tutorial tendrás un programa ejecutable que carga un archivo `.xlsx`, expande una fórmula de matriz, aplica Smart Markers y guarda el resultado.

## Requisitos previos

* .NET 6.0 o posterior (el código también funciona con .NET Core 3.1+)
* Aspose.Cells para .NET (paquete NuGet `Aspose.Cells`)
* Un libro de Excel que contenga una celda de fórmula de marcador de posición (p. ej., `B2`) y un Smart Marker como `{IsActive}`
* Familiaridad básica con C# y fórmulas de Excel

> **Consejo profesional:** La función `EXPAND` está disponible solo en Excel para Microsoft 365 y Excel 2021+. Las versiones anteriores devolverán un error `#NAME?`.

## Paso 1: Cómo expandir una matriz con la función EXPAND

El primer paso es cargar el libro de trabajo y escribir una fórmula `EXPAND` que convierta una única celda de origen en una matriz más grande.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

Por qué es importante: `EXPAND` elimina la necesidad de copiar manualmente fórmulas a través de filas y columnas. Cuando la celda de origen (`A2`) cambia, todo el bloque de 5 × 5 se actualiza automáticamente, proporcionándote un **dynamic range excel** que reacciona a los cambios de datos.

## Paso 2: Rellenar la plantilla de Excel usando Smart Markers

Los Smart Markers te permiten incrustar marcadores de posición dentro de la plantilla que son reemplazados con valores de un objeto C#. Esta es la forma más cómoda de **populate excel template** sin escribir código celda por celda.

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

La llamada `SmartMarkersProcessor().Apply` escanea toda la hoja, encuentra `{IsActive}` y inyecta el valor booleano. La fórmula entonces evalúa a `"Active"` o `"Inactive"` automáticamente.

## Paso 3: Verificar el rango expandido y el resultado rellenado

Después de aplicar tanto la fórmula `EXPAND` como los Smart Markers, puedes leer programáticamente algunas celdas para asegurarte de que todo funcionó como se esperaba.

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

Ejecutar el programa debería imprimir el valor original de `A2` (o el resultado de la matriz) y ya sea **Active** o **Inactive** dependiendo de la bandera `IsActive`.

## Paso 4: Guardar el libro de trabajo – la salida final

Finalmente, escribe el libro de trabajo modificado en disco. Este paso demuestra el flujo completo desde la carga, expansión, rellenado, hasta la persistencia del archivo.

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

El `output.xlsx` guardado ahora contiene una matriz de 5 × 5 generada por la fórmula `EXPAND` y una celda que refleja el valor de `{IsActive}`. Abre el archivo en Excel para ver el rango dinámico en acción.

## Casos límite y mejores prácticas

| Situación                              | Recomendación                                                                 |
|----------------------------------------|--------------------------------------------------------------------------------|
| La versión de Excel no admite `EXPAND`| Recurre a las fórmulas clásicas `=OFFSET` o `=INDEX`, o actualiza a Office 365. |
| Necesidad de expandir a un tamaño variable      | Usa `ROWS(source)` y `COLUMNS(source)` dentro de `EXPAND` para verdadera dinamismo.   |
| Múltiples Smart Markers en la misma hoja| Llama a `SmartMarkersProcessor().Apply` una vez con un objeto de datos compuesto.      |
| Libros de trabajo grandes ( > 10 000 filas)       | Desactiva el cálculo mientras escribes fórmulas (`workbook.Settings.CheckFormula = false`). |

## Ejemplo completo funcionando

A continuación se muestra el programa completo y autónomo que puedes copiar y pegar en un nuevo proyecto de consola.

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**Salida esperada al ejecutar el programa** (suponiendo que `A2` contenga el número `42`):

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

Al abrir `output.xlsx` se muestra un bloque de 5 × 5 lleno con los valores derivados de `A2` y una celda que muestra **Active**.

## Conclusión

Ahora sabes **how to expand array** en Excel usando la función `EXPAND`, cómo **populate excel template** con Smart Markers, y cómo crear un **dynamic range excel** que se adapta automáticamente a los datos de origen. El ejemplo también muestra la forma correcta de **use expand function** y la **expand array formula** en un escenario real de automatización C#.

A continuación, considera ampliar la solución:

* Reemplaza las dimensiones fijas `5,5` por `ROWS(A2:A10), COLUMNS(A2:E2)` para rangos verdaderamente variables.
* Combina varios Smart Markers para generar informes completos (p. ej., listas de empleados, tablas de ventas).
* Explora la API de estilo de Aspose.Cells para formatear automáticamente el bloque expandido.

¡Siéntete libre de experimentar con diferentes matrices de origen, nombres de marcadores y diseños de libros de trabajo! ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Exportar datos a Excel: rellenar una plantilla a partir de una matriz en C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [Cómo crear una matriz en Excel con C# – Guía paso a paso](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Procesar datos usando la función de matriz en Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}