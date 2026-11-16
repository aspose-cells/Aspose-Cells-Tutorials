---
category: general
date: 2026-11-16
description: Aprende cómo expandir una matriz en Excel usando Aspose.Cells, funciones
  de matriz dinámicas y un reductor lambda, luego escribe el archivo de Excel desde
  C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: es
lastmod: 2026-11-16
og_description: Cómo expandir una matriz en Excel usando Aspose.Cells, funciones de
  matrices dinámicas y un reductor lambda. Sigue el ejemplo completo en C# para escribir
  el archivo de Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Cómo expandir una matriz en Excel con Aspose.Cells – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cómo expandir una matriz en Excel con Aspose.Cells
url: /es/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo expandir una matriz en Excel con Aspose.Cells

Si necesitas **cómo expandir una matriz** en una hoja de cálculo de Excel desde C#, este tutorial muestra los pasos exactos. Crearás un libro de Excel, usarás funciones de matriz dinámica como `EXPAND` y `REDUCE`, aplicarás un acumulador **lambda**, y finalmente **escribirás el archivo de Excel** en disco. El enfoque funciona con Aspose.Cells 23.10 o posterior y no requiere una instalación manual de Excel.

Al final de esta guía tendrás un `ExpandReduceDemo.xlsx` completamente funcional que demuestra el poder de las fórmulas de matriz dinámica en un contexto programático.

## Lo que necesitarás

- .NET 6.0 (o cualquier versión de .NET compatible con Aspose.Cells)
- Paquete Aspose.Cells para .NET (`dotnet add package Aspose.Cells`)
- Un editor de código o IDE (Visual Studio, VS Code, Rider, etc.)

No se requiere interop COM adicional ni instalación de Office porque Aspose.Cells maneja el formato de archivo internamente.

## Paso 1: Crear libro de Excel

La primera tarea es **crear un libro de Excel** en memoria. Aspose.Cells proporciona la clase `Workbook`, que representa un archivo XLSX completo.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Por qué es importante:** Instanciar un `Workbook` te brinda un lienzo limpio. La hoja de cálculo predeterminada ya está preparada, por lo que no necesitas agregar una manualmente a menos que quieras varias hojas.

## Paso 2: Insertar una constante de matriz vertical

El motor de matrices dinámicas de Excel puede trabajar con constantes de matriz literales. Colocaremos la matriz vertical `{1;2;3;4;5}` en la celda **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Consejo:** El punto y coma (`;`) separa filas en la constante, mientras que una coma (`,`) separaría columnas. Esto refleja la sintaxis propia de Excel.

## Paso 3: Expandir la matriz en una matriz

Ahora respondemos la pregunta principal – **cómo expandir una matriz** – usando la función `EXPAND`. La fórmula expande la matriz de una sola columna en una matriz de 5 filas × 2 columnas, comenzando en **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **¿Por qué EXPAND?** `EXPAND(source, rows, cols)` obliga al rango origen a ocupar el tamaño especificado, rellenando con celdas vacías si es necesario. Es la forma más legible de generar una matriz más grande a partir de una sola matriz.

## Paso 4: Reducir la matriz con un acumulador lambda

La función `REDUCE` itera sobre un rango y agrega valores usando una expresión **lambda**. Aquí sumamos cada valor de columna en una sola columna, colocando el resultado en **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Cómo usar lambda:** `LAMBDA(acc, val, acc+val)` recibe el acumulador actual (`acc`) y el siguiente valor de celda (`val`). Devuelve el nuevo acumulador, realizando efectivamente una suma acumulativa. Esto demuestra **cómo usar lambda** en fórmulas de Excel desde código.

## Paso 5: Calcular fórmulas para que aparezcan los resultados

Aspose.Cells no evalúa automáticamente las fórmulas cuando las estableces. Llamar a `CalculateFormula` obliga al motor a calcular cada fórmula en el libro.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Nota:** Si abres el archivo generado en Excel, los valores ya estarán visibles porque se han pre‑calculado.

## Paso 6: Escribir el archivo de Excel en disco

Finalmente, **escribe el archivo de Excel** usando el método `Save`. Elige una carpeta en la que tengas permiso de escritura.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Resultado esperado

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **La columna B** y **C** contienen la matriz 5 × 2 producida por `EXPAND`.
- **La celda D1** muestra `15`, la suma de todos los números, calculada por la fórmula `REDUCE` + **lambda**.

## Preguntas comunes y casos límite

- **¿Puedo expandir a más columnas de las que proporciona la fuente?**  
  Sí. `EXPAND` rellena las columnas faltantes con celdas en blanco. Lo mismo ocurre con filas.

- **¿Qué pasa si la matriz fuente es horizontal (`{1,2,3,4,5}`)?**  
  `EXPAND` tratará la fuente como una sola fila; aún puedes especificar filas y columnas para remodelarla.

- **¿`REDUCE` funciona con datos no numéricos?**  
  La lambda debe devolver un valor compatible con el tipo del acumulador. Para concatenar texto podrías usar `LAMBDA(acc, val, acc & val)`.

- **¿Necesito llamar a `CalculateFormula` por cada cambio?**  
  Solo cuando necesites los valores calculados antes de guardar. Excel recalculará al abrir si lo omites.

## Consejos profesionales

- **Rendimiento:** Para libros grandes, llama a `workbook.CalculateFormula` una sola vez después de establecer todas las fórmulas, en lugar de hacerlo después de cada celda.
- **Seguridad de versión:** `EXPAND` y `REDUCE` están disponibles en Excel 365 y posteriores. Aspose.Cells los implementa sin importar la versión de Excel objetivo porque el motor de cálculo está integrado.
- **Depuración de fórmulas:** Usa `sheet.Cells["B1"].Formula` para leer la cadena exacta que estableciste; esto ayuda cuando construyes fórmulas dinámicamente.

## Conclusión

Ahora sabes **cómo expandir una matriz** en Excel usando Aspose.Cells, aprovechar las **funciones de matriz dinámica**, aplicar una **lambda** con `REDUCE`, y **escribir el archivo de Excel** desde C#. Este ejemplo de extremo a extremo puede adaptarse a transformaciones de datos más complejas, como la transposición de matrices, totales acumulados o agregaciones personalizadas.

---

*Próximos pasos:*  
- Explora otras funciones dinámicas como `FILTER`, `SORT` y `UNIQUE`.  
- Combina múltiples expresiones `LAMBDA` para crear funciones definidas por el usuario reutilizables.  
- Integra la generación del libro en APIs ASP.NET Core para crear informes al vuelo.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear un libro de Excel C# con una fórmula de matriz dinámica](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [Cómo expandir una matriz en Excel y rellenar una plantilla](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [Cómo expandir una matriz en C# con Aspose.Cells – Guía paso a paso](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}