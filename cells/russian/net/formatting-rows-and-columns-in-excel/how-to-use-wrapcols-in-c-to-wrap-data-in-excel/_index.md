---
category: general
date: 2026-11-19
description: Как использовать wrapcols в C# для переноса данных в Excel и быстрого
  вычисления формул Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- calculate excel formulas
- wrap data in excel
- save excel file c#
- load excel workbook c#
language: ru
lastmod: 2026-11-19
og_description: Как использовать wrapcols в C# для переноса данных в Excel. Узнайте,
  как вычислять формулы Excel и сохранять книгу программно.
og_image_alt: Screenshot showing wrapped data in an Excel worksheet after applying
  WRAPCOLS
og_title: Как использовать wrapcols в C# – перенос данных в Excel
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to use wrapcols in C# to wrap data in Excel and calculate Excel
    formulas quickly.
  headline: How to use wrapcols in C# to wrap data in Excel
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Data Wrapping
title: Как использовать wrapcols в C# для переноса данных в Excel
url: /ru/net/formatting-rows-and-columns-in-excel/how-to-use-wrapcols-in-c-to-wrap-data-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать wrapcols в C# для переноса данных в Excel

Если вам нужно **how to use wrapcols** для реорганизации вертикального списка в несколько столбцов, это руководство покажет точные шаги. Вы также узнаете, как **calculate Excel formulas**, чтобы результат был сохранён в файле, который вы сохраняете.

Работа с Excel из C# обычно начинается с загрузки рабочей книги, применения формул и, наконец, сохранения изменений. Этот учебник охватывает все эти этапы, при этом код легко скопировать‑вставить в ваш проект.

## Что вы получите

К концу этого руководства вы сможете:

* Загрузить существующий файл `.xlsx` с диска (**load excel workbook c#**).
* Применить функцию `WRAPCOLS` к диапазону, эффективно **wrap data in Excel**.
* Принудительно выполнить вычисление формулы (**calculate Excel formulas**).
* Сохранить изменённую рабочую книгу (**save Excel file c#**).

Единственное требование — наличие ссылки на **Aspose.Cells for .NET** (или любую библиотеку, поддерживающую функцию `WRAPCOLS`). Код работает с .NET 6+ и Visual Studio 2022, но любой C# IDE подойдёт.

## Как использовать wrapcols с Aspose.Cells

Функция листа `WRAPCOLS` принимает одно‑мерный диапазон и возвращает двумерный массив, заполняющий указанное количество столбцов. Aspose.Cells оценивает функцию так же, как Excel, поэтому её можно использовать напрямую в формуле ячейки.

```csharp
using System;
using Aspose.Cells;          // Install-Package Aspose.Cells via NuGet

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook and get the first worksheet
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.Worksheets[0];

        // Step 2: Write the WRAPCOLS formula into a cell
        // This wraps the values from A2:A10 into 3 columns, starting at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Step 3: Force calculation so the result becomes a static range
        wb.CalculateFormula();

        // Step 4: Save the workbook so you can open it in Excel
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);

        Console.WriteLine("Workbook saved to " + outputPath);
    }
}
```

### Почему важна каждая строка

* **Loading the workbook** даёт вам живую объектную модель, отражающую файл Excel на диске.  
* **Assigning the formula** в `A1` сообщает Excel (или Aspose.Cells), что диапазон следует рассматривать как динамический массив.  
* **`CalculateFormula()`** запускает движок вычислений; без этого формула останется невычисленной до открытия файла в Excel.  
* **Saving** записывает вычисленные значения в новый файл, делая перенесённые данные видимыми для любого, кто откроет рабочую книгу.

## Программный расчёт формул Excel

Вызов `Workbook.CalculateFormula()` — рекомендованный способ **calculate Excel formulas**, когда нужны результаты сразу. Метод учитывает все встроенные функции, пользовательские функции и любые внешние ссылки, которые уже разрешены.

Если у вас несколько листов, зависящих друг от друга, вы также можете передать объект `CalculationOptions` для контроля пределов итераций или включения многопоточного расчёта:

```csharp
var options = new CalculationOptions
{
    // Enable iterative calculation for circular references
    IterativeCalculation = true,
    MaxIterations = 100,
    // Use all available CPU cores
    EnableMultiThreadedCalculation = true
};

wb.CalculateFormula(options);
```

Этот дополнительный шаг необязателен для простого примера с `WRAPCOLS`, но становится критически важным в больших книгах, где важна производительность.

## Сохранить файл Excel C# после переноса данных

Вызов `Workbook.Save()` записывает всю рабочую книгу, включая только что материализованный массив, полученный от `WRAPCOLS`. Вы можете выбрать любой из поддерживаемых форматов (`.xlsx`, `.xls`, `.csv` и т.д.):

```csharp
// Save as a standard XLSX file (default)
wb.Save(@"YOUR_DIRECTORY\wrapped.xlsx");

// Save as CSV – only the active sheet is exported
wb.Save(@"YOUR_DIRECTORY\wrapped.csv", SaveFormat.Csv);
```

Шаг **save Excel file c#** гарантирует, что перенесённые данные сохраняются, поэтому при следующем открытии файла пользователь увидит статическую таблицу, а не формулу.

## Загрузить рабочую книгу Excel C# и подготовить лист

Если ваш исходный файл ещё не содержит данных, которые нужно перенести, вы можете создать их «на лету»:

```csharp
// Create a new workbook with a single worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Populate column A with sample values
for (int i = 0; i < 9; i++)
{
    ws.Cells[i + 2, 0].PutValue($"Item {i + 1}");
}
```

Этот фрагмент демонстрирует **load excel workbook c#** в том смысле, что вы можете начать с пустой книги, заполнить её, а затем применить `WRAPCOLS`. Та же схема работает, когда нужно импортировать данные из базы данных или CSV‑файла перед переносом.

## Профессиональный совет: проверка результата без открытия Excel

После сохранения вы можете программно считать обратно перенесённую область, чтобы убедиться, что операция прошла успешно:

```csharp
// Reload the saved file
Workbook checkWb = new Workbook(@"YOUR_DIRECTORY\output.xlsx");
Worksheet checkWs = checkWb.Worksheets[0];

// Print the first three rows of the wrapped area
for (int row = 0; row < 3; row++)
{
    for (int col = 0; col < 3; col++)
    {
        Console.Write($"{checkWs.Cells[row, col].StringValue}\t");
    }
    Console.WriteLine();
}
```

Консоль должна отобразить исходный список, разбитый на три столбца, подтверждая, что **wrap data in excel** сработал как ожидалось.

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|----------|--------|
| *What if the source range has more rows than `WRAPCOLS` can fill?* | Функция продолжает создавать новые строки по мере необходимости. Количество столбцов остаётся фиксированным. |
| *Can I wrap into a different number of columns?* | Да — измените второй аргумент, например `=WRAPCOLS(A2:A10,5)` для пяти столбцов. |
| *Do I need to clear the formula after calculation?* | Нет, если вы вызываете `CalculateFormula()`. Функция возвращает статический массив, но формула остаётся в ячейке. Если нужен чисто значение, скопируйте диапазон и вставьте только значения. |
| *Will this work with older `.xls` files?* | `WRAPCOLS` — динамическая функция массива, появившаяся в Excel 365. Старые форматы, не поддерживающие динамические массивы, сохранят формулу, но могут не отобразить результат корректно. Используйте `.xlsx` для надёжного поведения. |

## Заключение

Теперь вы знаете, **how to use wrapcols** в C# для **wrap data in Excel**, как **calculate Excel formulas** «на лету», и как **save Excel file C#** после преобразования. Полный пример демонстрирует загрузку книги, применение функции `WRAPCOLS`, принудительный расчёт и сохранение результата.

### Следующие шаги

* Исследуйте другие функции динамических массивов, такие как `UNWRAPCOLS` или `SEQUENCE`.  
* Используйте **Aspose.Cells** для импорта данных из базы и последующего автоматического переноса.  
* Сочетайте `WRAPCOLS` с условным форматированием, чтобы выделять определённые строки после переноса.

Экспериментируйте с различными исходными диапазонами, количеством столбцов и форматами вывода. Если возникнут проблемы, повторный просмотр шага **calculate Excel formulas** или проверка настроек расчёта в книге обычно решают их.

--- 

*Image: ![Скриншот, показывающий перенесённые данные в Excel](/images/wrapcols-example.png){.align-center alt="Скриншот, показывающий перенесённые данные в листе Excel после применения WRAPCOLS"}*


## Что изучать дальше?


Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to use WRAPCOLS in C# for Excel arrays and workbook saving](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-for-excel-arrays-and-workbook-savin/)
- [How to create Excel workbook and split data with WRAPCOLS in C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}