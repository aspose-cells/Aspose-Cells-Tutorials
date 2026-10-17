---
category: general
date: 2026-10-10
description: Crear un libro de Excel en C# y usar la función WRAPCOLS para dividir
  datos de una matriz en columnas. Sigue una guía completa paso a paso con código
  ejecutable.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: es
lastmod: 2026-10-10
og_description: Crear un libro de Excel en C# y aplicar la función WRAPCOLS para dividir
  datos de una matriz en columnas. Esta guía muestra el código completo y explica
  cada paso.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Crear libro de Excel y dividir datos con WRAPCOLS en C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cómo crear un libro de Excel y dividir datos con WRAPCOLS en C#
url: /es/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un libro de Excel y dividir datos con WRAPCOLS en C#

Si necesitas **create Excel workbook** programáticamente, esta guía te muestra exactamente cómo hacerlo y cómo **split array data** a través de columnas usando la función `WRAPCOLS`. Obtendrás un ejemplo completo y ejecutable que produce un archivo `.xlsx` con los datos distribuidos en tres columnas.

El tutorial cubre todo lo que necesitas: paquetes NuGet requeridos, cada línea de código, por qué la fórmula `WRAPCOLS` funciona y cómo adaptar la solución para diferentes tamaños de matriz o recuentos de columnas. Al final podrás incorporar la técnica **use wrapcols function** en cualquier proyecto C# que genere archivos Excel.

## Requisitos previos

* .NET 6.0 SDK o una versión posterior instalada  
* Un IDE de C# (Visual Studio, VS Code, Rider, etc.)  
* El paquete NuGet **Aspose.Cells for .NET** – la biblioteca que proporciona la clase `Workbook` usada en los ejemplos  

No necesitas una instalación de Office; Aspose.Cells escribe el archivo `.xlsx` directamente.

## Paso 1 – crear libro de Excel

La primera tarea es instanciar un nuevo objeto workbook y obtener una referencia a la primera hoja de cálculo. Este paso es la base para cualquier manipulación posterior.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` representa todo el archivo, mientras que `Worksheet` representa una sola hoja. Al crear el workbook en memoria evitas I/O de disco hasta que lo guardes explícitamente.

## Paso 2 – aplicar WRAPCOLS para dividir columnas de matriz

Ahora colocarás una fórmula en la celda **A1** que usa `WRAPCOLS`. La función recibe dos argumentos: la matriz origen y el número de columnas en que deseas que la matriz se envuelva.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Por qué esto funciona:** `WRAPCOLS` toma la matriz plana `{1,2,3,4,5,6}` y llena la hoja fila por fila, creando tres columnas por fila. El primer argumento puede ser cualquier literal de matriz de Excel, un rango nombrado o una fórmula de matriz dinámica. El segundo argumento (`3`) indica a Excel cuántas columnas generar antes de pasar a la siguiente fila.

### Usar la función con diferentes tipos de datos

La función `WRAPCOLS` no está limitada a números. Puedes dividir valores de texto, fechas o tipos mixtos:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Cuando la matriz origen contiene cadenas, Excel trata automáticamente el resultado como celdas de texto. Esta flexibilidad te permite **excel formula split data** para informes, paneles de control o tareas de migración de datos.

## Paso 3 – calcular fórmulas para que la hoja se rellene

Las fórmulas se almacenan como cadenas hasta que solicitas que el workbook las evalúe. Llamar a `CalculateFormula` fuerza la evaluación y escribe los resultados en las celdas.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Sin esta llamada, el archivo guardado contendría solo el texto de la fórmula, no los valores calculados. El método funciona en todo el workbook, por lo que puedes colocar fórmulas adicionales en otros lugares y todas se resolverán con una sola llamada.

## Paso 4 – guardar el workbook para ver el resultado

Finalmente, escribe el workbook en disco. Elige una carpeta en la que tengas permiso de escritura y da al archivo un nombre claro.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Cuando abras `output.xlsx` en Excel (o cualquier visor compatible), verás:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Si usaste el ejemplo de tipo mixto, las filas 3‑4 contendrían el texto y los números respectivamente.

## Variaciones avanzadas y manejo de casos límite

### Recuento de columnas variable en tiempo de ejecución

A menudo, el número de columnas que necesitas depende de la entrada del usuario. Puedes construir la cadena de fórmula dinámicamente:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Matrices grandes y rendimiento

`WRAPCOLS` puede manejar miles de elementos, pero evaluar matrices extremadamente grandes en una sola celda puede aumentar el tiempo de cálculo. Si notas una ralentización:

* Divide la matriz origen en fragmentos más pequeños y escribe cada fragmento en una celda de inicio separada.  
* Usa `WorkbookSettings` para habilitar el cálculo multihilo:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Manejo de celdas vacías

Si la matriz origen contiene cadenas vacías (`""`) o valores `NULL`, `WRAPCOLS` inserta celdas en blanco, preservando el diseño de columnas. Este comportamiento es útil cuando necesitas columnas de marcador de posición para la entrada de datos posterior.

### Uso de rangos nombrados en lugar de literales

Para mantener la facilidad de mantenimiento, define un rango nombrado que contenga los datos origen, luego haz referencia a él:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Ahora la fórmula lee datos de la propia hoja, habilitando **how to use wrapcols** en escenarios de informes dinámicos.

## Errores comunes y consejos profesionales

* **No omitas el segundo argumento.** `WRAPCOLS(array)` sin un recuento de columnas devuelve una sola columna, lo que anula el propósito de dividir los datos.  
* **Evita mezclar dimensiones de matrices.** La matriz origen debe ser unidimensional; proporcionar una matriz bidimensional (p.ej., `{ {1,2},{3,4} }`) genera un error `#VALUE!`.  
* **Guarda después del cálculo.** Si llamas a `wb.Save` antes de `CalculateFormula`, el archivo contendrá solo el texto de la fórmula.  
* **Verifica los permisos de archivo.** Al ejecutar en entornos restringidos (p.ej., ASP.NET), asegúrate de que la identidad del proceso pueda escribir en la carpeta de destino.  

## Ejemplo completo en funcionamiento

A continuación se muestra el programa completo que puedes copiar, pegar y ejecutar. Incluye todas las importaciones, manejo de errores y comentarios.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Ejecutar el programa produce `output.xlsx` con tres regiones distintas que demuestran **excel formula split data** usando la función `WRAPCOLS`.

## Conclusión

Ahora sabes cómo **create Excel workbook** archivos en C# y cómo **use wrapcols function** para **split array columns** de manera eficiente. Los pasos principales—instanciar `Workbook`, insertar la fórmula `WRAPCOLS`, calcular y guardar—forman un patrón reutilizable para cualquier tarea de automatización que requiera la distribución de datos en columnas.

A partir de aquí puedes:

* Combinar `WRAPCOLS` con otras funciones de matriz dinámica como `FILTER` o `SORT`.  
* Exportar grandes conjuntos de datos desde bases de datos y dejar que Excel gestione el diseño automáticamente.  
* Construir informes dirigidos por el usuario donde el recuento de columnas se seleccione mediante un control de UI.

¡Experimenta con diferentes fuentes de matrices, recuentos de columnas y fórmulas adicionales para ampliar esta base. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo usar WRAPCOLS en C# – Crear libro de Excel con funciones de ajuste](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Crear libro de Excel – Convertir matriz a matriz con WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Crear libro de Excel C# – Guía paso a paso](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}