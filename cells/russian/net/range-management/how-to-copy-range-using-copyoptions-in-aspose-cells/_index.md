---
category: general
date: 2026-11-19
description: Узнайте, как копировать диапазон с помощью CopyOptions в Aspose.Cells,
  сохраняя форматирование и сводные таблицы при копировании диапазона Excel с форматированием.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: ru
lastmod: 2026-11-19
og_description: Копирование диапазона с использованием CopyOptions в Aspose.Cells
  позволяет дублировать данные Excel с сохранением полного форматирования и сводных
  таблиц, обеспечивая надёжную работу с книгой.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Копирование диапазона с использованием CopyOptions в Aspose.Cells – пошаговое
  руководство
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как скопировать диапазон с использованием CopyOptions в Aspose.Cells
url: /ru/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как копировать диапазон с помощью CopyOptions в Aspose.Cells

Если вам нужно **copy range using CopyOptions** в Aspose.Cells, это руководство покажет, как точно дублировать блок ячеек, сохраняя всё форматирование и встроенные сводные таблицы. Многие разработчики сталкиваются с проблемой сохранения стиля при перемещении данных между листами, а класс `CopyOptions` решает эту задачу без дополнительных ручных шагов.

В этом руководстве вы научитесь:

* Определять области источника и назначения в рабочей книге Excel.  
* Использовать `CopyOptions` для сохранения форматирования ячеек, ширины столбцов и сводных таблиц.  
* Сохранять результат в новый файл, готовый для дальнейшей обработки.

Пример работает с любым файлом `.xlsx` и требует только библиотеки Aspose.Cells for .NET.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 или более поздняя версия.  
* Действующая лицензия Aspose.Cells for .NET (или бесплатный оценочный ключ).  
* Visual Studio 2022 или любой предпочитаемый вами IDE для C#.  

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Cells`.

## Шаг 1: Настройка проекта и импорт пространств имён

Создайте новое консольное приложение и добавьте ссылку на Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

Директива `using Aspose.Cells;` предоставляет доступ к `Workbook`, `CellArea` и `CopyOptions`.

## Шаг 2: Загрузка рабочей книги, которую нужно изменить

Загрузите рабочую книгу, которую хотите изменить:

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` представляет весь файл Excel. Замените `YOUR_DIRECTORY` на папку, содержащую ваш исходный файл.

## Шаг 3: Определение диапазонов источника и назначения

Определите диапазоны источника и назначения:

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` создает прямоугольную область на основе адресов ячеек верхнего‑левого и нижнего‑правого угла. Вы можете изменить координаты, чтобы они соответствовали размеру блока, который нужно скопировать.

## Шаг 4: Копирование диапазона с сохранением форматирования и сводных таблиц

Скопируйте диапазон, сохраняя форматирование и сводные таблицы:

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

Объект `CopyOptions` указывает Aspose.Cells, что именно сохранять. Установка `CopyPivotTables = true` является ключом к **copy range using CopyOptions**, когда ваш источник содержит сводные таблицы. Другие флаги гарантируют автоматическое выполнение **copy excel range with formatting** — дополнительный код для повторного применения стилей после копирования не требуется.

### Почему `CopyOptions` важен

* **Performance** – Библиотека выполняет одну внутреннюю операцию вместо копирования ячеек по одной.  
* **Accuracy** – Все визуальные элементы (шрифты, цвета, границы) сохраняются при перемещении, что устраняет визуальные отклонения в сгенерированных отчетах.  
* **Reliability** – Сводные таблицы остаются рабочими, поскольку их кэш и ссылки на источник дублируются.

## Шаг 5: Сохранение изменённой рабочей книги

Сохраните изменённую рабочую книгу:

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

После вызова `Save` файл `output.xlsx` будет содержать исходные данные плюс дублированный блок в месте назначения, полностью со всеми форматированиями и сводными таблицами.

## Полный исходный код для справки

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Запуск этой программы выводит:

```
Range copied successfully. Output saved to output.xlsx
```

Откройте `output.xlsx` в Excel — вы увидите блок A1:H30, дублированный в A35:H64, со всеми цветами ячеек, границами, форматами чисел и любыми сводными таблицами без изменений.

## Часто задаваемые вопросы и обработка граничных случаев

### Что делать, если область назначения перекрывает область источника?

Aspose.Cells генерирует `ArgumentException`. Чтобы избежать этого, вычислите место назначения, которое не пересекается с источником, или копируйте на другой лист:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Как копировать между разными рабочими книгами?

Создайте второй экземпляр `Workbook` для целевого файла и используйте тот же объект `CopyOptions`:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### Копирует ли `CopyOptions` также объединённые ячейки?

Да. Флаг `CopyStyle` включает информацию об объединённых ячейках. Если требуется более тонкий контроль, установите `options.CopyMergedCells = true` (доступно в более новых версиях).

### Что делать с большими диапазонами (тысячи строк)?

Операция экономична по памяти, но для очень больших файлов может потребоваться увеличить `WorkbookSettings` `MemorySetting` до `MemorySetting.MemoryPreference`.

## Профессиональные советы

* **Reuse the same `CopyOptions`** экземпляр для нескольких операций копирования — это уменьшает накладные расходы на выделение объектов.  
* **Validate ranges** перед копированием: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` помогает быстро обнаружить ошибки, связанные с опечатками.  
* **Turn off calculation** (`workbook.Settings.CalcMode = CalculationMode.Manual`) при копировании больших наборов данных для ускорения процесса, затем вызовите `workbook.CalculateFormula()` после копирования, если нужны обновлённые результаты.

## Заключение

Теперь вы знаете, как **copy range using CopyOptions** в Aspose.Cells, достигая полного **copy excel range with formatting** при сохранении сводных таблиц и других расширенных функций. Этот подход устраняет необходимость ручного повторного применения стилей и гарантирует, что ваша автоматизация Excel остаётся надёжной и поддерживаемой.

Следующие шаги, которые вы можете изучить:

* Использовать `CopyOptions` для дублирования целых листов.  
* Сочетать операцию копирования с `WorksheetCollection.AddCopy` для генерации отчётов на основе шаблонов.  
* Интегрировать код в ASP.NET Core API для выполнения преобразований Excel «на лету».

Не стесняйтесь экспериментировать с различными координатами источника/назначения и делиться результатами в комментариях!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}