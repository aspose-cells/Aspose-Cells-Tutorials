---
category: general
date: 2026-10-26
description: Aprende a usar WRAPCOLS en C# para dividir un rango en columnas, aplicar
  WRAPROWS para filas y guardar el libro de trabajo como XLSX programáticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: es
lastmod: 2026-10-26
og_description: Cómo usar WRAPCOLS en C# para dividir los datos en columnas, usar
  WRAPROWS para filas y guardar el libro de trabajo como XLSX. Sigue la guía completa
  paso a paso.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Cómo usar WRAPCOLS en C# – dividir rangos y guardar como XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cómo usar WRAPCOLS en C# y guardar el libro de trabajo como XLSX
url: /es/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar WRAPCOLS en C# y guardar el libro de trabajo como XLSX

Si necesitas **cómo usar WRAPCOLS** para reorganizar datos en un archivo Excel, esta guía te muestra una solución completa y ejecutable. Verás un **ejemplo de excel wrapcols**, aprenderás a **dividir un rango en filas** con WRAPROWS y terminarás **guardando el libro de trabajo como XLSX**, todo hecho **programáticamente**.

Trabajar con Excel desde C# suele implicar crear un libro de trabajo, aplicar fórmulas y persistir el archivo. El código a continuación usa la biblioteca Aspose.Cells, que permite manipular archivos Excel sin necesidad de tener Microsoft Office instalado. Al final de este tutorial podrás **crear excel workbook programmatically**, dividir datos tanto horizontal como verticalmente y generar un archivo `.xlsx` listo para su procesamiento posterior.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+)
* Una referencia al paquete NuGet **Aspose.Cells**  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Familiaridad básica con C# y fórmulas de Excel

## Paso 1: Cómo usar WRAPCOLS para dividir un rango en columnas

La función **WRAPCOLS** toma un rango unidimensional y reparte sus valores en el número especificado de columnas. En este ejemplo empezamos con valores en `A1:A10` y pedimos a WRAPCOLS que cree tres columnas.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Resultado:** Las celdas `C1:E4` ahora contienen los diez elementos originales distribuidos en tres columnas (la última columna contiene los elementos restantes).

![Screenshot illustrating how to use WRAPCOLS to split a range into columns in Excel](image-url.png)

## Paso 2: Dividir rango en filas con WRAPROWS

Mientras **WRAPCOLS** funciona horizontalmente, **WRAPROWS** hace lo contrario: reparte un rango en un número determinado de filas. Aquí tomamos los valores de `B1:B10` y los organizamos en dos filas a partir de `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Resultado:** La fórmula rellena las celdas `F1:K2` con los diez valores distribuidos en dos filas.

## Paso 3: Guardar el libro de trabajo como XLSX

Después de aplicar las fórmulas, el paso final es persistir el archivo. La operación **save workbook as xlsx** escribe el libro de trabajo en memoria en el disco en el formato moderno OpenXML.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Cómo se ve el archivo guardado

Al abrir `wrapcols_wraprows_output.xlsx` en Excel verás:

| C | D | E |
|---|---|---|
| Elemento 1 | Elemento 4 | Elemento 7 |
| Elemento 2 | Elemento 5 | Elemento 8 |
| Elemento 3 | Elemento 6 | Elemento 9 |
|        |        | Elemento 10 |

y

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Valor 1 | Valor 3 | Valor 5 | Valor 7 | Valor 9 | |
| Valor 2 | Valor 4 | Valor 6 | Valor 8 | Valor 10 | |

Las fórmulas permanecen en las celdas, por lo que cualquier cambio posterior en los rangos de origen se refleja automáticamente.

## Paso 4: Variaciones comunes y casos límite

### Cambiar el número de columnas o filas

* **Más columnas:** Incrementa el segundo argumento de `WRAPCOLS`.  
  Ejemplo: `=WRAPCOLS(A1:A10,5)` crea cinco columnas, dejando celdas vacías donde se agoten los datos.
* **Conteo de columnas dinámico:** Usa una referencia de celda en lugar de un número fijo.  
  `=WRAPCOLS(A1:A10, G1)` donde `G1` contiene el número de columnas deseado.

### Manejo de celdas vacías o no numéricas

WRAPCOLS y WRAPROWS ignoran las celdas vacías por defecto, pero preservan el orden de los valores no vacíos. Si necesitas conservar los vacíos, envuelve el rango origen con funciones `IFERROR` o `TEXT` antes de aplicar WRAPCOLS.

### Guardar en otros formatos

Aunque este tutorial se centra en **save workbook as xlsx**, Aspose.Cells soporta muchos formatos (`.xls`, `.csv`, `.pdf`, etc.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Consejos profesionales y trampas

* **Consejo pro:** Establece `Workbook.Settings.CalcEngineEnabled = true` si planeas evaluar fórmulas inmediatamente después de guardar.
* **Cuidado con:** Rangos de origen muy grandes pueden generar áreas de derrame enormes, lo que afecta el rendimiento. Limita el tamaño del rango o divide la operación en varias hojas de cálculo.
* **Seguridad en hilos:** Los objetos de Aspose.Cells **no** son seguros para subprocesos. Crea una instancia de `Workbook` separada por hilo si procesas archivos en paralelo.

## Conclusión

Ahora sabes **cómo usar WRAPCOLS** para dividir un rango vertical en múltiples columnas, cómo **dividir un rango en filas** con WRAPROWS y cómo **guardar el libro de trabajo como XLSX** después de realizar estas transformaciones. Siguiendo los pasos anteriores puedes **crear excel workbook programmatically**, aplicar potentes fórmulas de derrame y generar archivos Excel listos para compartir sin intervención manual.

### ¿Qué sigue?

* Explora **formato condicional** para resaltar los datos derramados.
* Combina **WRAPCOLS** con **SORT** o **FILTER** para paneles dinámicos.
* Usa la **API de gráficos** de Aspose.Cells para visualizar los datos reorganizados directamente desde el código.

¡Feliz codificación y que disfrutes automatizando tus flujos de trabajo en Excel!


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}