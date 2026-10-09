---
category: general
date: 2026-06-17
description: Как использовать WRAPCOLS в C# для преобразования массива в матрицу,
  записи формулы массива в ячейку и загрузки существующих файлов Excel с помощью Aspose.Cells.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- write array formula
- write formula to cell
- load existing excel
language: ru
og_description: Как использовать WRAPCOLS в C# для быстрого преобразования массива
  в матрицу, записи массивной формулы в ячейку и работы с существующими файлами Excel.
og_title: Как использовать WRAPCOLS в C# — преобразовать массив в матрицу
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  headline: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  name: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  steps:
  - name: 'Optional: Write a Dynamic Array Reference'
    text: 'If you prefer to reference a range instead of a hard‑coded list, you can
      use:'
  - name: 1. What if I need a different number of rows?
    text: '`WRAPCOLS` only takes the column count; the row count is inferred. To force
      a specific row count, you can combine it with `WRAPROWS` or pad the source array
      with empty strings.'
  - name: 2. Does WRAPCOLS work with text values?
    text: 'Absolutely. Replace the numbers with quoted strings:'
  - name: 3. Can I apply formatting to the generated matrix?
    text: 'After calculation, you can style the range programmatically:'
  - name: 4. How do I handle very large arrays?
    text: Aspose.Cells can process tens of thousands of elements, but keep an eye
      on memory. If you hit limits, consider writing the data in chunks or using `Workbook.Settings.MemorySetting
      = MemorySetting.MemoryPreference;`.
  type: HowTo
tags:
- excel
- csharp
- aspose.cells
title: Как использовать WRAPCOLS в C# — преобразовать массив в матрицу в Excel
url: /ru/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать WRAPCOLS в C# – Преобразовать массив в матрицу в Excel

Когда‑нибудь задумывались **как использовать WRAPCOLS**, чтобы превратить плоский список чисел в аккуратную таблицу в Excel? Вы не одиноки. Независимо от того, создаёте ли вы инструмент отчётности или просто играете с данными, преобразование массива в матрицу может сэкономить вам кучу ручного копирования‑вставки.

В этом руководстве мы пройдём полный, исполняемый пример, который покажет, как **записать формулу массива в ячейку**, вычислить результат и даже **загрузить существующую книгу Excel**, если это необходимо. К концу вы получите готовый фрагмент кода, готовый к копированию‑вставке, работающий с последней версией Aspose.Cells для .NET.

## Что вы узнаете

- Назначение функции `WRAPCOLS` и когда она особенно полезна.  
- Как **преобразовать массив в матрицу** с помощью единственной формулы.  
- Пошаговый код для **записи формулы в ячейку** и принудительного вычисления.  
- Дополнительные приёмы для **загрузки существующего файла Excel** перед применением формулы.  
- Распространённые подводные камни и советы по расширению подхода для больших наборов данных.

Никакой внешней документации не требуется — всё, что нужно, находится здесь.

## Требования

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+).  
- Aspose.Cells для .NET установлен (`dotnet add package Aspose.Cells`).  
- Базовое понимание синтаксиса C#; если вы умеете создавать консольное приложение, вы готовы к работе.

> **Pro tip:** Если вы используете Visual Studio, включите *nullable reference types* (`<Nullable>enable</Nullable>`), чтобы заранее отлавливать потенциальные ошибки с null.

## Шаг 1: Настройка проекта и импорт пространств имён

Сначала создайте новый консольный проект (или вставьте код в существующий). Затем добавьте необходимые директивы `using`, чтобы компилятор знал, где находятся `Workbook` и `Worksheet`.

```csharp
using System;
using Aspose.Cells;   // Main library for Excel manipulation

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill in the logic in the next steps
        }
    }
}
```

> **Почему это важно:** Импорт `Aspose.Cells` даёт доступ к высокопроизводительному движку Excel, который вычисляет `WRAPCOLS` без необходимости установки Excel на машине.

## Шаг 2: Создание или загрузка книги

Вы можете начать с нуля или открыть существующий файл. Ниже показан фрагмент, демонстрирующий оба варианта; просто закомментируйте тот, который не нужен.

```csharp
// Option A – Create a brand‑new workbook
Workbook workbook = new Workbook();   // starts with a single empty worksheet

// Option B – Load an existing Excel file (useful when you have templates)
// string inputPath = @"C:\Data\input.xlsx";
// Workbook workbook = new Workbook(inputPath);
```

> **Edge case:** Если загружаемый файл защищён паролем, передайте пароль вторым аргументом: `new Workbook(path, "password")`.

## Шаг 3: Получение целевого листа

Чаще всего нужен первый лист (`Worksheets[0]`), но вы также можете обратиться к листу по имени.

```csharp
Worksheet sheet = workbook.Worksheets[0];               // by index
// Worksheet sheet = workbook.Worksheets["DataSheet"]; // by name (if it exists)
```

## Шаг 4: Запись формулы WRAPCOLS в ячейку

Это сердце руководства. `WRAPCOLS` принимает массив и количество столбцов, затем «разливает» значения по строкам. Мы разместим формулу в **A1**, чтобы матрица начиналась в левом верхнем углу.

```csharp
// Write the WRAPCOLS formula that turns {1,2,3,4,5,6} into 2 rows × 3 columns
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

> **Что происходит?**  
> - Синтаксис фигурных скобок `{1,2,3,4,5,6}` создаёт встроенную константу массива.  
> - Второй аргумент (`3`) указывает Excel создать три столбца, автоматически переходя к новой строке для оставшихся элементов.  
> - Поскольку мы используем Aspose.Cells, формула сохраняется точно так же, как вы ввели её в Excel, и движок вычислит её по требованию.

### Опционально: Записать динамическую ссылку на массив

Если вы предпочитаете ссылаться на диапазон вместо жёстко заданного списка, можно использовать:

```csharp
// Assume B1:B6 already contains numbers you want to reshape
sheet.Cells["A1"].Formula = "=WRAPCOLS(B1:B6,3)";
```

Так матрица будет автоматически обновляться при изменении исходного диапазона.

## Шаг 5: Принудительный расчёт и сохранение результата

Aspose.Cells не вычисляет формулы, пока вы явно не попросите. Вызов `Calculate()` материализует результат, превращая вывод формулы в реальные значения ячеек.

```csharp
// Force calculation so the WRAPCOLS output appears in the sheet
workbook.Calculate();

// Save the workbook – adjust the path as needed
string outputPath = @"C:\Data\output.xlsx";
workbook.Save(outputPath);
```

Когда откроете `output.xlsx` в Excel, вы увидите:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Это эффект **преобразования массива в матрицу**, который вы искали.

## Полный рабочий пример

Собрав все части вместе, получаем готовую к запуску программу:

```csharp
using System;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook (or load an existing one)
            Workbook workbook = new Workbook(); // new Workbook(@"C:\Data\input.xlsx");

            // 2️⃣ Get the first worksheet
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ Write the WRAPCOLS formula – reshape {1..6} into 2×3
            sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

            // 4️⃣ Force calculation so the matrix is materialized
            workbook.Calculate();

            // 5️⃣ Save the result
            string outputPath = @"C:\Data\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Запустите программу, откройте `output.xlsx`, и вы увидите матрицу точно как показано выше.

## Часто задаваемые вопросы и подводные камни

### 1. Что если мне нужно другое количество строк?

`WRAPCOLS` принимает только количество столбцов; количество строк определяется автоматически. Чтобы задать конкретное количество строк, можно комбинировать её с `WRAPROWS` или дополнить исходный массив пустыми строками.

```csharp
// Example: Force 3 rows, 2 columns (will add blanks if needed)
sheet.Cells["A1"].Formula = "=WRAPROWS({1,2,3,4,5,6},3)";
```

### 2. Работает ли WRAPCOLS с текстовыми значениями?

Абсолютно. Замените числа на строки в кавычках:

```csharp
sheet.Cells["A1"].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",\"Apr\",\"May\",\"Jun\"},3)";
```

### 3. Можно ли применить форматирование к полученной матрице?

После расчёта вы можете программно задать стиль диапазону:

```csharp
Range matrix = sheet.Cells.CreateRange("A1:C2");
Style style = workbook.CreateStyle();
style.Font.Color = System.Drawing.Color.Blue;
style.Font.IsBold = true;
matrix.ApplyStyle(style, new StyleFlag() { Font = true });
```

### 4. Как обрабатывать очень большие массивы?

Aspose.Cells может обработать десятки тысяч элементов, но следите за потреблением памяти. Если встретите ограничения, рассмотрите запись данных частями или используйте `Workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;`.

## Советы для продакшн‑кода

- **Кешировать ссылку на лист**, если записываете много формул в цикле; это уменьшит накладные расходы на поиск.  
- **Отключить автоматический расчёт** (`workbook.Settings.CalculateFormulaOnOpen = false;`), когда планируете пакетно записать десятки формул, а затем вызвать `Calculate()` один раз в конце.  
- **Обернуть ввод‑вывод файла в try/catch**, чтобы сразу выявлять ошибки доступа:

```csharp
try
{
    workbook.Save(outputPath);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

- **Проверять входные данные** перед построением строки формулы — особенно если конкатенируете значения, полученные от пользователя, чтобы избежать некорректных формул.

## Визуальное резюме

![Как использовать WRAPCOLS для получения матрицы результата в Excel](wrapcols-output.png "Как использовать WRAPCOLS в C# для преобразования массива в матрицу")

*На скриншоте показана матрица 2 × 3, полученная формулой WRAPCOLS.*

## Заключение

Мы рассмотрели **как использовать WRAPCOLS** в C# от начала до конца: создание или загрузку книги, запись формулы массива в ячейку, принудительный расчёт и сохранение результата. Теперь вы знаете, как **преобразовать массив в матрицу**, **записать формулу массива** и **загрузить существующие файлы Excel** — всё это несколькими строками чистого, поддерживаемого кода.

Далее вы можете изучить:


## Что стоит изучить дальше?


Следующие руководства охватывают тесно связанные темы, развивая техники, продемонстрированные в этом пособии. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как эффективно загружать файлы Excel с помощью Aspose.Cells в .NET](/cells/english/net/workbook-operations/efficient-excel-load-aspose-cells-net/)
- [Как загружать и изменять файлы Excel с помощью Aspose.Cells для .NET: Полное руководство](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [Как задать язык в файлах Excel с помощью Aspose.Cells .NET для поддержки нескольких языков](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}