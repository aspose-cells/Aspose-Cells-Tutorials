---
category: general
date: 2026-08-04
description: Определите область ячеек в Aspose.Cells и узнайте, как эффективно копировать
  сводные таблицы, копировать диапазон Excel в C# и копировать диапазон на том же
  листе.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: ru
lastmod: 2026-08-04
og_description: Определите область ячеек в Aspose.Cells и скопируйте диапазон Excel
  в C#, сохраняя сводные таблицы. Следуйте этому пошаговому руководству для надёжных
  результатов.
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: Определение области ячеек в Aspose.Cells – копирование диапазона Excel в
  C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: Определить область ячеек в Aspose.Cells и скопировать диапазон Excel в C#
url: /ru/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Определить область ячеек в Aspose.Cells и скопировать диапазон Excel на C#

Если вам нужно **define cell area** для диапазона, а затем скопировать этот диапазон на том же листе, это руководство покажет, как сделать это с помощью Aspose.Cells для .NET. Независимо от того, перемещаете ли вы отчет, основанный на сводной таблице, или дублируете блок данных, вы изучите полный процесс за несколько шагов.

Вы также узнаете **how to copy pivot** таблицы без потери их связей и увидите чистый пример **copy excel range c#**, который работает в сценарии **copy range same sheet**. Внешние инструменты не требуются — только Aspose.Cells и несколько строк C#.

## Что вам понадобится

- .NET 6.0 или новее (код также работает с .NET Framework 4.7+)
- Aspose.Cells для .NET (пакет NuGet `Aspose.Cells`)
- Excel‑книга (`input.xlsx`), содержащая сводную таблицу в диапазоне A1:J50
- Среда разработки, например Visual Studio 2022

## Шаг 1: Определить область ячеек для исходного диапазона

Первая задача — **define cell area**, представляющая блок, который вы хотите скопировать. Aspose.Cells использует структуру `CellArea`, которая хранит индексы строк и столбцов, начинающиеся с нуля.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**Почему это важно:** `CellArea` точно указывает Aspose.Cells, какие ячейки обрабатывать. Использование индексов, начинающихся с нуля, избегает ошибок «на один» при преобразовании нотации Excel A1 в код.

## Шаг 2: Определить область ячеек назначения на том же листе

Чтобы **copy range same sheet**, необходимо также указать, куда должны попасть данные. Назначение может начинаться с любой строки; здесь мы начинаем с строки 61 (индекс 60, начинающийся с нуля), чтобы оставить пустой буфер.

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**Почему это важно:** Отражая размеры источника, вы гарантируете, что скопированный блок полностью поместится без усечения.

## Шаг 3: Скопировать диапазон, сохраняя сводные таблицы

Теперь вы можете безопасно выполнить **how to copy pivot**. Класс `CopyOptions` включает флаг `CopyPivotTables`, который сохраняет определение сводной таблицы, источник данных и форматирование.

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**Почему это важно:** Если не установить `CopyPivotTables = true`, сводная таблица превратится в статический снимок, потеряв интерактивность. Эта опция копирует базовый кэш и соединения, поэтому новая сводная таблица работает точно так же, как оригинальная.

## Шаг 4: Сохранить книгу

Наконец, запишите изменения обратно на диск. Выходной файл демонстрирует, что сводная таблица была дублирована на том же листе.

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**Совет:** Используйте `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)`, если необходимо задать конкретный формат, особенно при работе со старыми версиями Excel.

## Шаг 5: Проверить скопированную сводную таблицу

Откройте `CopyWithPivot.xlsx` в Excel и проверьте следующее:

1. Диапазон A61:J110 содержит копию исходных данных.
2. Новая сводная таблица появляется в верхней части скопированного диапазона.
3. Обновление сводной таблицы отражает изменения в исходных данных, подтверждая, что **how to copy pivot** выполнено успешно.

Если сводная таблица не обновляется, убедитесь, что диапазон исходных данных в определении сводной таблицы по‑прежнему указывает на область оригинальной книги. Aspose.Cells автоматически обновляет ссылку на источник, когда `CopyPivotTables` равно true.

## Пограничные случаи и варианты

| Situation | What to change |
|-----------|----------------|
| **Копировать на другой лист** | Замените `srcWorkbook.Worksheets[0]` на индекс или имя целевого листа и соответственно скорректируйте `destinationRange`. |
| **Копировать объединённый блок ячеек** | Установите `CopyOptions.PasteType = PasteType.All`, чтобы сохранить объединённые ячейки и форматирование. |
| **Копировать только значения, без формул** | Используйте `CopyOptions.PasteType = PasteType.Values`, чтобы избежать переноса формул, ссылающихся на оригинальный лист. |
| **Большие диапазоны ( > 10 000 строк )** | Рассмотрите возможность использования `Workbook.Copy` для копирования целых листов с целью повышения производительности, затем удалите ненужные строки. |

Эти варианты демонстрируют, что та же логика **aspose.cells copy range** может быть адаптирована к множеству реальных сценариев.

## Полный рабочий пример

Ниже представлен полный готовый к запуску пример программы. Замените `YOUR_DIRECTORY` реальным путём к папке на вашем компьютере.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**Ожидаемый результат:** После выполнения программы `CopyWithPivot.xlsx` содержит исходные данные плюс идентичный блок, начинающийся с строки 61, полностью с рабочей сводной таблицей.

## Заключение

Теперь вы знаете, как **define cell area** в Aspose.Cells, **copy excel range c#** и **copy range same sheet**, сохраняя всю функциональность сводных таблиц. Эта техника устраняет ошибки ручного копирования и масштабируется для больших книг.

Далее изучайте связанные темы, такие как **how to copy pivot** между несколькими листами, или используйте **aspose.cells copy range** для дублирования целых листов с форматированием. Экспериментируйте с различными настройками `CopyOptions`, чтобы адаптировать поведение копирования под потребности вашего проекта.

Удачной разработки!

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, опирающиеся на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Excel Aspose Cells .NET Копировать диапазон данных](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET Копировать диапазон данных](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET Копировать диапазон данных](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}