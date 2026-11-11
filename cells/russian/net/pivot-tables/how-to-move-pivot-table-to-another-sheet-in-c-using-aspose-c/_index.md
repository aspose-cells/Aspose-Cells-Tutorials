---
category: general
date: 2026-10-26
description: переместить сводную таблицу на другой лист в C# с пошаговым руководством,
  которое также показывает, как эффективно загружать книгу Excel в C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- move pivot table to another sheet
- load excel workbook c#
- copy rows with pivot table
- Aspose.Cells pivot table
- C# Excel automation
language: ru
lastmod: 2026-10-26
og_description: переместить сводную таблицу на другой лист в C# с помощью Aspose.Cells.
  Следуйте этому краткому руководству, чтобы загрузить Excel‑книгу в C# и безопасно
  копировать сводные таблицы.
og_image_alt: Screenshot of a pivot table moved to another sheet using C#
og_title: Переместить сводную таблицу на другой лист в C# — полное руководство по
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: move pivot table to another sheet in C# with a step‑by‑step guide that
    also shows how to load Excel workbook C# efficiently
  headline: How to move pivot table to another sheet in C# using Aspose.Cells
  type: TechArticle
- description: move pivot table to another sheet in C# with a step‑by‑step guide that
    also shows how to load Excel workbook C# efficiently
  name: How to move pivot table to another sheet in C# using Aspose.Cells
  steps:
  - name: Expected result
    text: '* The file **CopyPivot.xlsx** contains a new worksheet **PivotCopy**. *
      The pivot table appears exactly as it did on the original sheet, preserving
      filters, row/column fields, and data source connections. * All original data
      remains in the source worksheet, so you have effectively **moved pivot tabl'
  - name: Multiple pivot tables on the same sheet
    text: 'If the source sheet hosts several pivots, repeat steps 3–5 for each `PivotTable`
      object:'
  - name: Copying to an existing sheet with data
    text: 'When the destination sheet already contains data, calculate the next free
      row:'
  - name: Preserving formatting
    text: '`CopyRows` copies cell values, formulas, and formatting by default. If
      you need to exclude formatting, use the overload that accepts a `CopyOptions`
      object and set `CopyOptions.CopyStyle = false`.'
  - name: What to explore next
    text: '* **Load Excel workbook C#** and modify formulas programmatically – see
      the Aspose.Cells documentation on `Formula` objects. * **Export pivot tables
      to PDF** using `Workbook.Save` with `SaveFormat.Pdf`. * **Create pivot tables
      from scratch** with the `PivotTable` API for dynamic report generation.'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Как переместить сводную таблицу на другой лист в C# с использованием Aspose.Cells
url: /ru/net/pivot-tables/how-to-move-pivot-table-to-another-sheet-in-c-using-aspose-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как переместить сводную таблицу на другой лист в C# с использованием Aspose.Cells

Если вам нужно **переместить сводную таблицу на другой лист** в файле .xlsx, это руководство покажет вам точные шаги. Вы также узнаете, как **загрузить Excel workbook C#** с помощью Aspose.Cells, скопировать связанную сводную таблицу и сохранить результат, не теряя соединений данных.

В руководстве рассматривается всё, что необходимо для реализации, готовой к продакшну: требуемые пакеты NuGet, полный исходный код, объяснения, почему каждый вызов API важен, и советы по обработке распространённых граничных случаев, таких как несколько сводных таблиц или листы назначения, которые уже существуют.

## Требования

* .NET 6.0 или более поздняя версия установленa  
* Visual Studio 2022 (или любой IDE, поддерживающий .NET)  
* NuGet‑пакет Aspose.Cells for .NET (`Aspose.Cells`) – библиотека, предоставляющая классы `Workbook`, `Worksheet` и `CellArea`, используемые в примере  

Установленный Microsoft Office не требуется; Aspose.Cells работает напрямую с форматом файла.

## Шаг 1: Загрузить Excel workbook в C#

Первая операция — чтение исходного файла с диска. Загрузка workbook создаёт в памяти представление каждой листа, ячейки и кэша сводных таблиц.

```csharp
using Aspose.Cells;

namespace PivotTableMover
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            var sourcePath = @"C:\Data\Source.xlsx";
            Workbook sourceWorkbook = new Workbook(sourcePath);
            // Continue with pivot table handling...
        }
    }
}
```

*Почему этот шаг важен* – `Workbook` разбирает пакет XLSX, заполняет коллекцию `Worksheets` и подготавливает объекты кэша сводных таблиц, чтобы к ним можно было обратиться позже. Без загрузки workbook дальнейшее манипулирование невозможно.

## Шаг 2: Определить лист, содержащий сводную таблицу

Обычно первая лист содержит сводную таблицу, но можно искать по имени или проверяя коллекцию `PivotTables`. Для наглядности в этом примере используется первый лист.

```csharp
// Get the first worksheet that contains the pivot table
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
```

Если workbook содержит несколько листов со сводными таблицами, пройдитесь по `sourceWorkbook.Worksheets` и проверьте `sheet.PivotTables.Count`, чтобы выбрать нужный.

## Шаг 3: Определить диапазон ячеек, охватывающий сводную таблицу

Aspose.Cells требует структуру `CellArea` для указания прямоугольного блока, который нужно скопировать. Диапазон должен включать всю сводную таблицу, включая строки заголовков и любые вычисляемые столбцы.

```csharp
// Define the area covering the pivot table (adjust rows/columns as needed)
CellArea pivotRange = new CellArea
{
    StartRow = 0,          // zero‑based index, first row of the pivot
    StartColumn = 0,       // first column of the pivot
    EndRow = 30,           // last row of the pivot (inclusive)
    EndColumn = 10         // last column of the pivot (inclusive)
};
```

*Почему этот шаг важен* – Метод `CopyRows` работает с диапазоном строк, но передавая `CellArea`, вы гарантируете, что включены все ячейки, принадлежащие сводной таблице. Если диапазон слишком мал, сводная таблица теряет исходные данные; если слишком велик, копируются лишние ячейки.

## Шаг 4: Создать (или выбрать) лист назначения

Вы можете переместить сводную таблицу на существующий лист или создать новый. В примере создаётся новый лист с именем **"PivotCopy"** и копируемые строки размещаются, начиная с строки 0.

```csharp
// Create a new worksheet for the copied pivot table
Worksheet destSheet = sourceWorkbook.Worksheets[sourceWorkbook.Worksheets.Add()];
destSheet.Name = "PivotCopy";
```

Если вы предпочитаете переместить сводную таблицу на существующий лист, замените код создания ссылкой на этот лист:

```csharp
// Worksheet destSheet = sourceWorkbook.Worksheets["ExistingSheetName"];
```

## Шаг 5: Скопировать строки — включая связанную сводную таблицу — на лист назначения

Метод `CopyRows` принимает флаг (`true`), который указывает Aspose.Cells копировать любые сводные таблицы, связанные со строками. Этот флаг необходим; без него определение сводной таблицы будет потеряно.

```csharp
// Copy rows from sourceSheet to destSheet, preserving pivot tables
sourceSheet.CopyRows(
    sourceRowIndex: 0,          // start row in source sheet
    totalRows: 40,              // number of rows to copy (covers the pivot range)
    sourceArea: pivotRange,     // the cell area that defines the pivot
    copyAssociatedPivotTables: true, // preserve pivot tables
    destinationSheet: destSheet,
    destinationRowIndex: 0);    // start row in the destination sheet
```

*Почему этот шаг важен* – Параметр `copyAssociatedPivotTables` гарантирует, что кэш сводных таблиц и настройки полей перемещаются вместе с копируемыми строками. Лист назначения получает полностью функционирующую сводную таблицу, указывающую на тот же источник данных, что и оригинал.

## Шаг 6: Сохранить изменённый workbook

После операции копирования сохраните workbook в новый файл. Оставление оригинального файла нетронутым делает процесс безопасным для автоматизированных конвейеров.

```csharp
// Save the workbook with the moved pivot table
var outputPath = @"C:\Data\CopyPivot.xlsx";
sourceWorkbook.Save(outputPath);
```

Когда вы откроете **CopyPivot.xlsx**, вы увидите лист "PivotCopy", содержащий точную копию оригинальной сводной таблицы, готовую для дальнейшего анализа или распространения.

## Полный рабочий пример

Объединение всех шагов приводит к самостоятельному консольному приложению:

```csharp
using Aspose.Cells;

namespace PivotTableMover
{
    class Program
    {
        static void Main()
        {
            // 1. Load the source workbook
            var sourcePath = @"C:\Data\Source.xlsx";
            Workbook sourceWorkbook = new Workbook(sourcePath);

            // 2. Locate the worksheet with the pivot table
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

            // 3. Define the range that includes the pivot table
            CellArea pivotRange = new CellArea
            {
                StartRow = 0,
                StartColumn = 0,
                EndRow = 30,
                EndColumn = 10
            };

            // 4. Create a destination worksheet
            Worksheet destSheet = sourceWorkbook.Worksheets[sourceWorkbook.Worksheets.Add()];
            destSheet.Name = "PivotCopy";

            // 5. Copy rows and associated pivot tables
            sourceSheet.CopyRows(
                sourceRowIndex: 0,
                totalRows: 40,
                sourceArea: pivotRange,
                copyAssociatedPivotTables: true,
                destinationSheet: destSheet,
                destinationRowIndex: 0);

            // 6. Save the result
            var outputPath = @"C:\Data\CopyPivot.xlsx";
            sourceWorkbook.Save(outputPath);
        }
    }
}
```

### Ожидаемый результат

* Файл **CopyPivot.xlsx** содержит новый лист **PivotCopy**.  
* Сводная таблица выглядит точно так же, как на оригинальном листе, сохраняя фильтры, поля строк/столбцов и соединения с источником данных.  
* Все оригинальные данные остаются в листе‑источнике, поэтому вы фактически **переместили сводную таблицу на другой лист** без потери любой функциональности.

## Обработка распространённых вариантов

### Несколько сводных таблиц на одном листе
Если лист‑источник содержит несколько сводных таблиц, повторите шаги 3–5 для каждого объекта `PivotTable`:

```csharp
foreach (PivotTable pt in sourceSheet.PivotTables)
{
    // Determine the exact area of each pivot table
    CellArea ptArea = pt.TableRange;
    // Copy each pivot individually
    sourceSheet.CopyRows(0, ptArea.EndRow - ptArea.StartRow + 1,
        ptArea, true, destSheet, destSheet.Cells.MaxDataRow + 1);
}
```

### Копирование на существующий лист с данными
Если лист назначения уже содержит данные, вычислите следующую свободную строку:

```csharp
int destStartRow = destSheet.Cells.MaxDataRow + 1;
sourceSheet.CopyRows(0, 40, pivotRange, true, destSheet, destStartRow);
```

### Сохранение форматирования
`CopyRows` по умолчанию копирует значения ячеек, формулы и форматирование. Если необходимо исключить форматирование, используйте перегрузку, принимающую объект `CopyOptions`, и установите `CopyOptions.CopyStyle = false`.

## Профессиональные советы

* **Validate the pivot range** – перед копированием проверьте, что `pivotRange.EndRow` и `EndColumn` соответствуют `pt.TableRange`. Несоответствующие диапазоны могут обрезать сводную таблицу или дублировать лишние строки.  
* **Refresh the pivot cache** после перемещения сводной таблицы, если исходные данные изменились. Вызовите `pt.RefreshData()` у сводной таблицы назначения, чтобы гарантировать актуальность вычислений.  
* **Avoid hard‑coded paths** в продакшн‑коде. Используйте `Path.Combine` и файлы конфигурации, чтобы сделать решение переносимым между средами.

## Заключение

Теперь у вас есть полный, готовый к продакшну метод **переместить сводную таблицу на другой лист** в C#. Руководство показало, как **загрузить Excel workbook C#**, определить точный диапазон сводной таблицы, скопировать строки, сохранив определение сводной таблицы, и сохранить обновлённый файл. С этими строительными блоками вы можете автоматизировать сложные задачи отчётности в Excel, интегрировать работу со сводными таблицами в веб‑сервисы или создавать пользовательские конвейеры анализа данных.

### Что изучать дальше

* **Load Excel workbook C#** и программно изменять формулы — см. документацию Aspose.Cells по объектам `Formula`.  
* **Export pivot tables to PDF** с помощью `Workbook.Save` и `SaveFormat.Pdf`.  
* **Create pivot tables from scratch** с использованием API `PivotTable` для динамической генерации отчётов.  

Не стесняйтесь экспериментировать с разными исходными файлами, несколькими сводными таблицами или пользовательскими макетами назначения. Один и тот же шаблон работает независимо от размера или сложности workbook. Приятного кодинга!

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Копировать сводную таблицу на другой лист — Полное руководство C#](/cells/english/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/)
- [Как скопировать сводную таблицу в Excel с помощью C# и Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Создать сводную таблицу в Excel с использованием Aspose.Cells для .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}