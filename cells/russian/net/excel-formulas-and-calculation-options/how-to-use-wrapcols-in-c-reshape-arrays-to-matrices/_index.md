---
category: general
date: 2026-05-23
description: Как использовать WRAPCOLS в C# для преобразования 1‑мерного массива в
  2‑мерную матрицу. Узнайте о функции WRAPCOLS, запишите формулу в ячейку и легко
  преобразуйте 1D в 2D.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- convert 1d to 2d
- write formula to cell
- wrap columns function
language: ru
og_description: Как использовать WRAPCOLS в C# позволяет преобразовать одномерный
  массив в двумерную матрицу с помощью одной формулы. Следуйте этому руководству,
  чтобы записать формулу в ячейку и освоить функцию wrap columns.
og_title: Как использовать WRAPCOLS в C# — преобразовать массивы в матрицы
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  headline: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  name: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  steps:
  - name: Why this matters
    text: You could try to roll your own matrix logic, but the **wrap columns function**
      already handles edge cases like uneven division and empty inputs. Adding the
      Aspose.Cells NuGet package gives us a clean API to interact with Excel formulas
      directly from C#.
  - name: The core of “how to use WRAPCOLS”
    text: 'The **WRAPCOLS** function takes two arguments: an array (or range) and
      the number of columns you want per row. In our case we’ll reshape the literal
      array `{1,2,3,4,5,6}` into **2 rows × 3 columns**.'
  - name: Expected output
    text: '``` 1 2 3 4 5 6 ```'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Как использовать WRAPCOLS в C# — преобразовать массивы в матрицы
url: /ru/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-reshape-arrays-to-matrices/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать WRAPCOLS в C# – Преобразование массивов в матрицы

Ever wondered **how to use WRAPCOLS** when you need to turn a flat list of numbers into a tidy table? You’re not alone—many developers hit a wall when they try to convert a 1‑dimensional list into a 2‑dimensional grid without writing a lot of looping code. The good news? The WRAPCOLS function (sometimes called the wrap columns function) does the heavy lifting in a single line, and you can drop it straight into an Excel workbook from C#.

In this tutorial we’ll walk through the whole process: from creating a workbook, to **write formula to cell**, to **reshape array to matrix**, and finally to **convert 1d to 2d** using the WRAPCOLS formula. By the end you’ll have a reusable snippet that works with any numeric array, and you’ll understand why the wrap columns function is often a cleaner alternative to manual array reshaping.

## Предварительные требования

* .NET 6.0 или новее (код также работает на .NET Framework 4.6+)  
* Библиотека **Aspose.Cells for .NET** (бесплатная пробная версия или лицензированная копия) – это компонент, который предоставляет нам объекты `Workbook`, `Worksheet` и `Cell`, используемые ниже.  
* Базовое понимание синтаксиса C# — продвинутые знания Excel не требуются.

Got those? Great—let’s get our hands dirty.

![Resulting 2x3 matrix after using WRAPCOLS function in C# – how to use WRAPCOLS](https://example.com/images/wrapcols-result.png "How to use WRAPCOLS – resulting 2x3 matrix")

## Шаг 1: Настройте проект и добавьте Aspose.Cells

### Почему это важно

You could try to roll your own matrix logic, but the **wrap columns function** already handles edge cases like uneven division and empty inputs. Adding the Aspose.Cells NuGet package gives us a clean API to interact with Excel formulas directly from C#.

```bash
dotnet add package Aspose.Cells
```

*Pro tip:* If you’re using Visual Studio, right‑click the project → **Manage NuGet Packages** → search for **Aspose.Cells** and install the latest stable version.

## Шаг 2: Создайте новую книгу (или загрузите существующую)

Now that the library is in place, we can spin up a workbook object. This is where the **write formula to cell** step will happen.

```csharp
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 2: Initialize a fresh workbook
        Workbook workbook = new Workbook();          // creates an empty .xls/.xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0]; // grab the first sheet
```

Here we’ve created a brand‑new workbook; you could also load an existing file with `new Workbook("path/to/file.xlsx")` if you need to embed the matrix into a pre‑formatted template.

## Шаг 3: Вставьте формулу WRAPCOLS в ячейку

### Суть «как использовать WRAPCOLS»

The **WRAPCOLS** function takes two arguments: an array (or range) and the number of columns you want per row. In our case we’ll reshape the literal array `{1,2,3,4,5,6}` into **2 rows × 3 columns**.

```csharp
        // Step 3: Write the WRAPCOLS formula into cell A1
        // The formula =WRAPCOLS({1,2,3,4,5,6},3) tells Excel to wrap every 3 items into a new row.
        worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

Notice how the formula mirrors what you’d type in Excel itself. By placing it in `Cells[0,0]` (cell **A1**) we’re **writing the formula to a cell** without any extra plumbing.

## Шаг 4: Принудительно вычислите формулу, чтобы она оценилась

Aspose.Cells doesn’t evaluate formulas automatically unless you tell it to. This step ensures the workbook actually contains the reshaped matrix.

```csharp
        // Step 4: Recalculate the workbook so the WRAPCOLS formula runs
        workbook.CalculateFormula();
```

If you skip this line, the cells will still show the formula text instead of the computed values.

## Шаг 5: Считайте результат обратно (необязательно, но удобно для проверки)

You might want to confirm that the **reshape array to matrix** operation succeeded. Here’s a quick loop that prints the resulting 2‑by‑3 grid to the console.

```csharp
        // Step 5: Output the matrix to the console for verification
        for (int row = 0; row < 2; row++)          // we expect 2 rows
        {
            for (int col = 0; col < 3; col++)      // and 3 columns per row
            {
                var value = worksheet.Cells[row, col].StringValue;
                Console.Write(value + "\t");
            }
            Console.WriteLine();
        }

        // Optional: Save the workbook to disk to see the Excel view
        workbook.Save("WrapColsResult.xlsx");
    }
}
```

### Ожидаемый вывод

```
1   2   3
4   5   6
```

The console shows the exact same layout you’d see in Excel after the WRAPCOLS formula runs. That’s the **convert 1d to 2d** transformation in action.

## Шаг 6: Обработка граничных случаев – Что если длина массива не кратна количеству столбцов?

If the source array has, say, 7 elements and you ask for 3 columns, WRAPCOLS will create the last row with the remaining element(s) and leave the remaining cells blank. Here’s a quick tweak to demonstrate:

```csharp
worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6,7},3)";
workbook.CalculateFormula();
```

Result:

```
1   2   3
4   5   6
7       
```

The **wrap columns function** gracefully pads the final row with empty cells, so you don’t need extra code to handle mismatched sizes.

## Шаг 7: Использование WRAPCOLS с динамическими данными

In real projects you’ll rarely hard‑code the array. Instead you’ll build a string representation from a C# collection:

```csharp
int[] numbers = Enumerable.Range(1, 12).ToArray(); // 1..12
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
int columns = 4; // desired columns per row

worksheet.Cells[0, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
workbook.CalculateFormula();
```

Now you’ve **converted 1d to 2d** for any length, and you still get the same clean matrix output. The formula is built at runtime, but the underlying **wrap columns function** stays the same.

## Распространённые ошибки и профессиональные советы

| Ошибка | Почему происходит | Решение |
|--------|-------------------|---------|
| Забыли вызвать `workbook.CalculateFormula()` | Aspose.Cells оставляет формулы невычисленными | Всегда вызывайте метод после установки любой формулы |
| Использование нечислового литерала массива | WRAPCOLS ожидает числа или строки, которые можно привести | Убедитесь, что литерал содержит только числа (или строки в кавычках) |
| Непреднамеренное перезаписывание существующих данных | Размещение формулы в ячейке, которая уже содержит данные | Выберите пустую ячейку (например, A1) или сначала очистите диапазон |
| Неправильное обращение к индексу листа | `Worksheets[0]` — первый лист, но вы могли добавить другие | Проверьте `worksheet = workbook.Worksheets["SheetName"];` при необходимости |

## Почему WRAPCOLS лучше ручных циклов

* **Readability** – One line of formula replaces dozens of `for` loops.  
* **Performance** – Excel’s native engine is highly optimized for array formulas.  
* **Maintainability** – Future developers can see the intent instantly: “wrap these values into columns”.  
* **Portability** – The same formula works if you export the workbook to Google Sheets or LibreOffice—no C#‑specific logic required.

## Полный рабочий пример (готовый к копированию и вставке)



## Похожие руководства

- [How to Use Aspose.Cells for .NET to Show Cell Ranges as Data Labels in Charts](/cells/english/net/charts-graphs/aspose-cells-net-chart-customization-cell-ranges-data-labels/)
- [How to Use Aspose.Cells for .NET to Group Rows and Columns in Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [How to Use Excel IF Function](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}