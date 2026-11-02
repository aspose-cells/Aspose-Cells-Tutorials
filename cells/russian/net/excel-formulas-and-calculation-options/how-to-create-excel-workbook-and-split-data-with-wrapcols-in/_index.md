---
category: general
date: 2026-10-10
description: Создайте рабочую книгу Excel на C# и используйте функцию WRAPCOLS для
  разбивки данных массива по столбцам. Следуйте полному пошаговому руководству с исполняемым
  кодом.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: ru
lastmod: 2026-10-10
og_description: Создайте рабочую книгу Excel на C# и примените функцию WRAPCOLS для
  разделения данных массива по столбцам. Это руководство показывает полный код и объясняет
  каждый шаг.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Создать книгу Excel и разделить данные с помощью WRAPCOLS в C#
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
title: Как создать книгу Excel и разбить данные с помощью WRAPCOLS в C#
url: /ru/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать книгу Excel и разбить данные с помощью WRAPCOLS в C#

Если вам нужно **программно создать книгу Excel**, это руководство покажет, как это сделать, а также как **разбить массив данных** по столбцам с помощью функции `WRAPCOLS`. Вы получите полностью готовый пример, который создаёт файл `.xlsx` с данными, распределёнными по трем столбцам.

В руководстве рассматриваются все необходимые детали: требуемые пакеты NuGet, каждая строка кода, почему формула `WRAPCOLS` работает, и как адаптировать решение под разные размеры массивов или количество столбцов. К концу вы сможете внедрить технику **use wrapcols function** в любой C#‑проект, генерирующий Excel‑файлы.

## Prerequisites

Перед началом убедитесь, что у вас есть:

* .NET 6.0 SDK или более поздняя версия  
* IDE для C# (Visual Studio, VS Code, Rider и т.д.)  
* NuGet‑пакет **Aspose.Cells for .NET** – библиотека, предоставляющая класс `Workbook`, используемый в примерах  

Установка Office не требуется; Aspose.Cells записывает файл `.xlsx` напрямую.

## Step 1 – create Excel workbook

Первая задача – создать объект новой книги и получить ссылку на первый лист. Этот шаг является основой для любой дальнейшей манипуляции.

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

`Workbook` представляет весь файл, а `Worksheet` – отдельный лист. Создавая книгу в памяти, вы избегаете ввода‑вывода на диск, пока явно не сохраните её.

## Step 2 – apply WRAPCOLS to split array columns

Теперь вы поместите формулу в ячейку **A1**, использующую `WRAPCOLS`. Функция принимает два аргумента: исходный массив и количество столбцов, в которые массив должен быть разбит.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Почему это работает:** `WRAPCOLS` берёт плоский массив `{1,2,3,4,5,6}` и заполняет лист построчно, создавая три столбца в каждой строке. Первый аргумент может быть любой литеральной Excel‑матрицей, именованным диапазоном или динамической формулой массива. Второй аргумент (`3`) указывает Excel, сколько столбцов генерировать перед переходом к следующей строке.

### Using the function with different data types

Функция `WRAPCOLS` не ограничивается числами. Вы можете разбивать текстовые значения, даты или смешанные типы:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Когда исходный массив содержит строки, Excel автоматически рассматривает результат как текстовые ячейки. Такая гибкость позволяет **excel formula split data** для отчётов, панелей мониторинга или задач миграции данных.

## Step 3 – calculate formulas so the worksheet is populated

Формулы хранятся как строки, пока вы не попросите книгу их вычислить. Вызов `CalculateFormula` принудительно выполняет вычисления и записывает результаты в ячейки.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Без этого вызова сохранённый файл будет содержать только текст формулы, а не вычисленные значения. Метод работает по всей книге, поэтому вы можете разместить дополнительные формулы в других местах, и они все будут рассчитаны одним вызовом.

## Step 4 – save the workbook to see the result

Наконец, запишите книгу на диск. Выберите папку, в которую у вас есть права записи, и дайте файлу понятное имя.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

При открытии `output.xlsx` в Excel (или любом совместимом просмотрщике) вы увидите:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Если вы использовали пример со смешанными типами, строки 3‑4 будут содержать соответствующий текст и числа.

## Advanced variations and edge‑case handling

### Variable column count at runtime

Часто количество требуемых столбцов зависит от ввода пользователя. Формулу можно собрать динамически:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Large arrays and performance

`WRAPCOLS` может обрабатывать тысячи элементов, но вычисление чрезвычайно больших массивов в одной ячейке может увеличить время расчёта. Если вы заметили замедление:

* Разбейте исходный массив на более мелкие части и запишите каждую часть в отдельную начальную ячейку.  
* Используйте `WorkbookSettings` для включения многопоточного расчёта:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Handling empty cells

Если исходный массив содержит пустые строки (`""`) или значения `NULL`, `WRAPCOLS` вставляет пустые ячейки, сохраняя структуру столбцов. Такое поведение полезно, когда нужны заполнители столбцов для последующего ввода данных.

### Using named ranges instead of literals

Для удобства поддержки определите именованный диапазон, содержащий исходные данные, а затем ссылайтесь на него:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Теперь формула читает данные непосредственно из листа, позволяя использовать **how to use wrapcols** в сценариях динамической отчётности.

## Common pitfalls and pro tips

* **Не опускайте второй аргумент.** `WRAPCOLS(array)` без указания количества столбцов возвращает один столбец, что сводит к нулю цель разбивки данных.  
* **Избегайте смешения размеров массивов.** Исходный массив должен быть одномерным; передача двумерного массива (например, `{ {1,2},{3,4} }`) приводит к ошибке `#VALUE!`.  
* **Сохраняйте после вычисления.** Если вызвать `wb.Save` до `CalculateFormula`, файл будет содержать только текст формулы.  
* **Проверьте права доступа к файлу.** При работе в ограниченных средах (например, ASP.NET) убедитесь, что процесс имеет право записи в целевую папку.  

## Full working example

Ниже приведена полная программа, которую можно скопировать, вставить и запустить. В ней присутствуют все импорты, обработка ошибок и комментарии.

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

Запуск программы создаёт `output.xlsx` с тремя отдельными областями, демонстрирующими **excel formula split data** с помощью функции `WRAPCOLS`.

## Conclusion

Теперь вы знаете, как **create Excel workbook** в C# и как **use wrapcols function** для эффективного **split array columns**. Основные шаги — создание `Workbook`, вставка формулы `WRAPCOLS`, вычисление и сохранение — образуют переиспользуемый шаблон для любой задачи автоматизации, требующей распределения данных по столбцам.

Дальше вы можете:

* Комбинировать `WRAPCOLS` с другими динамическими массивными функциями, такими как `FILTER` или `SORT`.  
* Экспортировать большие наборы данных из баз и позволять Excel автоматически формировать макет.  
* Создавать отчёты, где количество столбцов выбирается пользователем через элемент управления UI.

Экспериментируйте с различными источниками массивов, количеством столбцов и дополнительными формулами, чтобы расширить эту основу. Приятного кодинга!

## What Should You Learn Next?

Следующие руководства охватывают тесно связанные темы, развивая техники, продемонстрированные в этом пособии. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}