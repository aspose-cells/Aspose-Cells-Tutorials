---
category: general
date: 2026-11-16
description: Узнайте, как использовать WRAPCOLS в C# для разделения строки на столбцы,
  автоматизации книги Excel, вычисления формул и сохранения файла Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split row into columns
- automate excel workbook
- excel formula calculation
- save excel file c#
language: ru
lastmod: 2026-11-16
og_description: Как использовать WRAPCOLS в C# для разделения строки на столбцы, автоматизации
  книги Excel, выполнения расчётов формул и сохранения файла Excel.
og_image_alt: Screenshot showing WRAPCOLS function splitting a row into columns in
  an Excel workbook
og_title: Как использовать WRAPCOLS в C# – разбивать строки, вычислять формулы и сохранять
  файлы Excel
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  headline: How to use WRAPCOLS to split a row into columns in C#
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  name: How to use WRAPCOLS to split a row into columns in C#
  steps:
  - name: How WRAPCOLS works
    text: '* **Source range** – `A1:T1` contains the original 20 values. * **Column
      count** – `5` tells Excel to create five columns per row. * **Result** – Excel
      fills cells `A2:E5` with the wrapped data automatically.'
  - name: Expected output
    text: 'Open `WrapColsDemo.xlsx` and you’ll see:'
  - name: Next steps
    text: '* Explore other dynamic array functions such as `SEQUENCE`, `FILTER`, and
      `UNIQUE` to enrich your Excel automation toolkit. * Combine `WRAPCOLS` with
      chart generation APIs to produce ready‑to‑publish reports. * Integrate the code
      into a background service that processes CSV uploads and outputs resha'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: Как использовать WRAPCOLS для разделения строки на столбцы в C#
url: /ru/net/row-and-column-management/how-to-use-wrapcols-to-split-a-row-into-columns-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать WRAPCOLS для разделения строки на столбцы в C#

Если вам нужно **how to use WRAPCOLS** в проекте C#, это руководство покажет полное, исполняемое решение. Вы увидите, как разделить строку на столбцы, автоматизировать книгу Excel, запустить вычисление формул Excel и, наконец, сохранить файл Excel в стиле C#.

Работа с Excel программно часто подразумевает обработку больших наборов данных, и функция `WRAPCOLS` позволяет преобразовать одну строку в матрицу без ручных циклов. Ниже приведённые шаги охватывают всё, что вам нужно — от создания книги до окончательного вывода файла — чтобы вы могли интегрировать эту технику в любое приложение .NET.

## Что покрывает это руководство

* Создание новой книги и доступ к её первому листу.  
* Заполнение строки последовательными значениями (1‑20).  
* Применение формулы Excel `WRAPCOLS` для разделения строки на блоки по 5 столбцов.  
* Выполнение **excel formula calculation**, чтобы результат стал частью листа.  
* Использование **save excel file c#** для записи книги на диск.  

Никакая внешняя конфигурация не требуется, кроме библиотеки Aspose.Cells для .NET (или любой совместимой API, поддерживающей `WRAPCOLS`). К концу руководства у вас будет файл с именем `WrapColsDemo.xlsx`, содержащий четыре строки по пять столбцов каждая, полученные из исходных данных в одной строке.

## Требования

* .NET 6.0 или новее (код также работает с .NET Core 3.1 и .NET Framework 4.7+).  
* Ссылка на **Aspose.Cells** (доступна через NuGet: `Install-Package Aspose.Cells`).  
* Базовое знакомство с синтаксисом C# и формулами Excel.  

> **Pro tip:** Если вы предпочитаете бесплатную альтернативу, библиотека с открытым исходным кодом EPPlus также поддерживает пользовательские формулы, но `WRAPCOLS` встроена только в библиотеки, реализующие полноценный движок вычислений Excel, такие как Aspose.Cells.

## Шаг 1: Создать новую книгу и получить первый лист

Первая операция — создать объект `Workbook` и получить его лист по умолчанию. Этот объект представляет весь файл Excel в памяти.

```csharp
using Aspose.Cells;

...

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                 // creates an empty workbook
Worksheet sheet = workbook.Worksheets[0];           // the first worksheet (named "Sheet1")
```

Создание книги программно является основой задач **automate excel workbook**. Ссылка `Worksheet` позволяет напрямую манипулировать ячейками.

## Шаг 2: Заполнить первую строку значениями 1‑20

Далее заполните ячейки от `A1` до `T1` числами от 1 до 20. Простой цикл `for` записывает каждое значение в соответствующий индекс столбца.

```csharp
// Step 2: Fill the first row with values 1‑20
for (int col = 0; col < 20; col++)
{
    sheet.Cells[0, col].PutValue(col + 1);   // Row 0 = first row, column index starts at 0
}
```

Зачем записывать значения программно? Это гарантирует, что демонстрация будет работать на любой машине без ручного ввода данных, что важно при генерации **automate excel workbook** в пакетных процессах.

## Шаг 3: Применить функцию WRAPCOLS для разделения строки на блоки по 5 столбцов

Теперь мы используем формулу Excel `WRAPCOLS`. Она принимает исходный диапазон и количество столбцов, затем возвращает двумерный массив, который «оборачивает» исходные данные в указанное количество столбцов.

```csharp
// Step 3: Use the WRAPCOLS function to split the row into 5‑column blocks
sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";
```

Размещение формулы в ячейке `A2` указывает Excel начать вывод со второй строки. Результатом будет матрица 4 × 5, поскольку 20 элементов, разделённые на 5 столбцов, дают четыре строки.

### Как работает WRAPCOLS

* **Source range** – `A1:T1` содержит исходные 20 значений.  
* **Column count** – `5` указывает Excel создать пять столбцов в каждой строке.  
* **Result** – Excel автоматически заполняет ячейки `A2:E5` обёрнутыми данными.  

Если вам понадобится **split row into columns** с другим размером блока, просто измените второй аргумент. Например, `WRAPCOLS(A1:T1,4)` создаст пять строк по четыре столбца каждая.

## Шаг 4: Вычислить формулы, чтобы результат WRAPCOLS материализовался

Новодобавленная формула остаётся невычисленной, пока не запустится движок вычислений. Вызвав `CalculateFormula()`, вы гарантируете, что шаг **excel formula calculation** запишет реальные значения в лист.

```csharp
// Step 4: Calculate formulas so the WRAPCOLS result is materialised
workbook.CalculateFormula();
```

Выполнение вычисления критично, когда позже вы **save excel file c#**, потому что сохранённый файл должен содержать вычисленные значения, а не только текст формулы. Без этого шага результирующая книга будет показывать `#N/A` или сырую формулу вместо ожидаемых чисел.

## Шаг 5: Сохранить книгу на диск

Наконец, сохраните книгу, используя метод `Save`. Вы можете указать любой действительный путь к файлу; в примере используется каталог‑заполнитель, который следует заменить своим.

```csharp
// Step 5: Save the workbook
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "WrapColsDemo.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Вызов `Save` демонстрирует **save excel file c#** в самой простой форме. Aspose.Cells автоматически выбирает формат XLSX на основе расширения файла. Если нужен более старый файл `.xls`, измените расширение соответственно.

### Ожидаемый результат

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 |10 |
|11 |12 |13 |14 |15 |
|16 |17 |18 |19 |20 |

Исходная одна строка была **split row into columns** на четыре строки, каждая из которых содержит пять столбцов.

## Полный исходный код

Объединение всех шагов приводит к компактной, автономной программе:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 1: Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Fill first row with values 1‑20
        for (int col = 0; col < 20; col++)
        {
            sheet.Cells[0, col].PutValue(col + 1);
        }

        // Step 3: Apply WRAPCOLS to split into 5‑column blocks
        sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";

        // Step 4: Force calculation so values are materialised
        workbook.CalculateFormula();

        // Step 5: Save the workbook (change the path as needed)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "WrapColsDemo.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Скопируйте код в новый консольный проект, восстановите пакет NuGet Aspose.Cells и запустите. Программа создаст файл Excel на вашем рабочем столе за секунды.

## Общие варианты и граничные случаи

| Ситуация | Корректировка |
|-----------|------------|
| **Different block size** | Change `WRAPCOLS(A1:T1,5)` to `WRAPCOLS(A1:T1, n)` where `n` is the desired column count. |
| **Multiple source rows** | Use `WRAPCOLS(A1:A10,5)` to wrap a vertical range into a 5‑column matrix. |
| **Dynamic source range** | Build the address string in C# (`$"A1:{CellIndexToName(0, lastCol)}1"`) before assigning the formula. |
| **Large worksheets** | Call `workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` to skip cells that cause errors and improve performance. |
| **Saving as CSV** | Replace `workbook.Save(outputPath)` with `workbook.Save(outputPath, SaveFormat.Csv)`. |

## Советы по устранению неполадок

- **Formula not evaluated** – Убедитесь, что вы вызываете `workbook.CalculateFormula()` *после* установки формулы. Пропуск этого шага оставит ячейку с сырым текстом `WRAPCOLS`.  
- **File access denied** – Проверьте, существует ли целевой каталог и имеет ли ваш процесс права записи. Использование `Environment.SpecialFolder.Desktop` избегает большинства проблем с правами.  
- **Incorrect number of rows** – Дважды проверьте второй аргумент `WRAPCOLS`. Он определяет количество столбцов, а не строк; строки вычисляются из общего количества исходных ячеек, делённого на количество столбцов.  

## Заключение

Теперь вы знаете **how to use WRAPCOLS** в C# для **split row into columns**, полностью **automate excel workbook** создание, запуск **excel formula calculation** и **save excel file c#** с единой чистой кодовой базой. Эта техника устраняет ручные операции копирования‑вставки и без труда масштабируется для больших конвейеров преобразования данных.

### Следующие шаги

- Изучите другие функции динамических массивов, такие как `SEQUENCE`, `FILTER` и `UNIQUE`, чтобы расширить ваш набор инструментов автоматизации Excel.  
- Сочетайте `WRAPCOLS` с API генерации диаграмм для создания готовых к публикации отчётов.  
- Интегрируйте код в фоновый сервис, который обрабатывает загрузки CSV и выводит преобразованные файлы Excel для последующего анализа.  

Не стесняйтесь экспериментировать с различными исходными диапазонами и количеством столбцов — изменяйте формулу, повторно запускайте вычисление и наблюдайте мгновенное обновление книги. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [как использовать wrapcols в C# – Полное руководство с Excel WRAPROWS и пересчётом формул](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Как использовать WRAPCOLS – Полное руководство по автоматизации Excel в C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)
- [Как использовать WRAPCOLS в C# – Преобразовать массив в матрицу в Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}