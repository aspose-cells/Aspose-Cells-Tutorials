---
category: general
date: 2026-10-26
description: Узнайте, как использовать WRAPCOLS в C# для разбивки диапазона на столбцы,
  применить WRAPROWS для строк и программно сохранить книгу в формате XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: ru
lastmod: 2026-10-26
og_description: Как использовать WRAPCOLS в C# для разделения данных на столбцы, использовать
  WRAPROWS для строк и сохранять книгу в формате XLSX. Следуйте полному пошаговому
  руководству.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Как использовать WRAPCOLS в C# — разбить диапазоны и сохранить в XLSX
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
title: Как использовать WRAPCOLS в C# и сохранить книгу в формате XLSX
url: /ru/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать WRAPCOLS в C# и сохранить книгу в формате XLSX

Если вам нужно **как использовать WRAPCOLS** для реорганизации данных в файле Excel, это руководство покажет полное, готовое к запуску решение. Вы увидите **пример excel wrapcols**, узнаете, как **разбить диапазон на строки** с помощью WRAPROWS, и завершите **сохранить книгу в формате XLSX** — всё выполнено **программно**.

Работа с Excel из C# часто подразумевает создание книги, применение формул и сохранение файла. Приведённый ниже код использует библиотеку Aspose.Cells, которая позволяет работать с файлами Excel без установки Microsoft Office. К концу этого руководства вы сможете **create excel workbook programmatically**, разбивать данные как по горизонтали, так и по вертикали, и создавать чистый файл `.xlsx`, готовый к дальнейшей обработке.

## Требования

* .NET 6.0 или новее (код также работает с .NET Framework 4.7+)
* Ссылка на пакет NuGet **Aspose.Cells**  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Базовые знания C# и формул Excel

## Шаг 1: Как использовать WRAPCOLS для разбивки диапазона на столбцы

Функция **WRAPCOLS** принимает одно‑мерный диапазон и распределяет его значения по указанному количеству столбцов. В этом примере мы начинаем со значений в `A1:A10` и просим WRAPCOLS создать три столбца.

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

> **Результат:** Ячейки `C1:E4` теперь содержат исходные десять элементов, распределённые по трем столбцам (в последнем столбце находятся оставшиеся элементы).

![Screenshot illustrating how to use WRAPCOLS to split a range into columns in Excel](image-url.png)

## Шаг 2: Разбить диапазон на строки с помощью WRAPROWS

В то время как **WRAPCOLS** работает по горизонтали, **WRAPROWS** делает противоположное: распределяет диапазон по заданному количеству строк. Здесь мы берём значения из `B1:B10` и размещаем их в двух строках, начиная с `F1`.

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

> **Результат:** Формула заполняет ячейки `F1:K2` десятью значениями, распределёнными по двум строкам.

## Шаг 3: Сохранить книгу в формате XLSX

После применения формул последний шаг — сохранить файл. Операция **save workbook as xlsx** записывает книгу из памяти на диск в современном формате OpenXML.

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

### Как выглядит сохранённый файл

Когда вы откроете `wrapcols_wraprows_output.xlsx` в Excel, вы увидите:

| C | D | E |
|---|---|---|
| Элемент 1 | Элемент 4 | Элемент 7 |
| Элемент 2 | Элемент 5 | Элемент 8 |
| Элемент 3 | Элемент 6 | Элемент 9 |
|        |        | Элемент 10 |

и

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Значение 1 | Значение 3 | Значение 5 | Значение 7 | Значение 9 | |
| Значение 2 | Значение 4 | Значение 6 | Значение 8 | Значение 10 | |

Формулы остаются в ячейках, поэтому любые последующие изменения исходных диапазонов автоматически отражаются.

## Шаг 4: Распространённые варианты и граничные случаи

### Изменение количества столбцов или строк

* **Больше столбцов:** Увеличьте второй аргумент функции `WRAPCOLS`.  
  Пример: `=WRAPCOLS(A1:A10,5)` создаёт пять столбцов, оставляя пустые ячейки, когда данные заканчиваются.
* **Динамическое количество столбцов:** Используйте ссылку на ячейку вместо жёстко заданного числа.  
  `=WRAPCOLS(A1:A10, G1)`, где `G1` содержит требуемое количество столбцов.

### Обработка пустых или нечисловых ячеек

WRAPCOLS и WRAPROWS по умолчанию игнорируют пустые ячейки, но сохраняют порядок непустых значений. Если необходимо сохранить пустые ячейки, оберните исходный диапазон функциями `IFERROR` или `TEXT` перед применением WRAPCOLS.

### Сохранение в другие форматы

Хотя в этом руководстве основной акцент на **save workbook as xlsx**, Aspose.Cells поддерживает множество форматов (`.xls`, `.csv`, `.pdf` и т.д.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Профессиональные советы и подводные камни

* **Pro tip:** Установите `Workbook.Settings.CalcEngineEnabled = true`, если планируете сразу после сохранения вычислять формулы.
* **Watch out for:** Большие исходные диапазоны могут создавать очень большие области разброса, что может влиять на производительность. Ограничьте размер диапазона или разбейте операцию на несколько листов.
* **Thread safety:** Объекты Aspose.Cells **не** являются потокобезопасными. Создавайте отдельный экземпляр `Workbook` для каждого потока, если обрабатываете файлы параллельно.

## Заключение

Теперь вы знаете **how to use WRAPCOLS** для разбивки вертикального диапазона на несколько столбцов, как **split range into rows** с помощью WRAPROWS и как **save workbook as XLSX** после выполнения этих преобразований. Следуя приведённым шагам, вы сможете **create excel workbook programmatically**, применять мощные формулы разброса и генерировать готовые к распространению файлы Excel без ручного вмешательства.

### Что дальше?

* Исследуйте **conditional formatting**, чтобы выделять разбросанные данные.
* Сочетайте **WRAPCOLS** с **SORT** или **FILTER** для динамических панелей.
* Используйте **charting API** Aspose.Cells для визуализации переставленных данных непосредственно из кода.

Счастливого кодинга и приятной автоматизации ваших рабочих процессов в Excel!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые расширяют техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [как использовать wrapcols в C# – Полное руководство с Excel WRAPROWS и пересчётом формул](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Как использовать WRAPCOLS в C# – Преобразовать массив в матрицу в Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [Как использовать WRAPCOLS – Полное руководство по автоматизации Excel в C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}