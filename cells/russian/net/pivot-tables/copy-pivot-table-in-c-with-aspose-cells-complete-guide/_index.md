---
category: general
date: 2026-08-11
description: Копировать сводную таблицу с помощью C# и Aspose.Cells. Узнайте, как
  загрузить книгу Excel, дублировать сводную таблицу и быстро сохранить её форматирование.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- duplicate pivot table excel
- move pivot table cell
- load excel workbook c#
- preserve pivot formatting
language: ru
lastmod: 2026-08-11
og_description: Копировать сводную таблицу в C# с помощью Aspose.Cells. Это руководство
  покажет, как загрузить книгу Excel, дублировать сводную таблицу и сохранить всё
  форматирование без изменений.
og_image_alt: Excel worksheet after copy pivot table operation
og_title: Копирование сводной таблицы в C# – пошаговое руководство Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  headline: Copy pivot table in C# with Aspose.Cells – complete guide
  type: TechArticle
- description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  name: Copy pivot table in C# with Aspose.Cells – complete guide
  steps:
  - name: Load Excel workbook C#
    text: Loading the workbook is the first action when you **load excel workbook
      c#**. Aspose.Cells reads the file into memory, giving you access to worksheets,
      cells, and pivot tables.
  - name: Identify and copy the pivot table range
    text: A pivot table lives inside a rectangular cell range. To **move pivot table
      cell** safely, you must copy the whole range, not just individual cells.
  - name: Save the workbook with the copied pivot table
    text: After copying, you simply save the workbook. The new file will contain both
      the original and the duplicated pivot table.
  - name: Full working example
    text: 'Putting the three steps together gives you a complete, runnable program:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Копирование сводной таблицы в C# с помощью Aspose.Cells – полное руководство
url: /ru/net/pivot-tables/copy-pivot-table-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копирование сводной таблицы в C# с Aspose.Cells – полное руководство

Если вам нужно **скопировать сводную таблицу** из одного места в другое в книге Excel с помощью C#, это руководство покажет, как это сделать. Вы увидите лаконичное решение от начала до конца, которое загружает книгу, дублирует сводную таблицу и сохраняет все детали форматирования.

Работа с Excel программно часто подразумевает работу со сложными объектами, такими как сводные таблицы. В этом руководстве вы научитесь **duplicate pivot table excel** без потери фильтров, вычисляемых полей или стилей. Единственное требование — ссылка на библиотеку Aspose.Cells, которая предоставляет полный контроль над файлами Excel из .NET.

## Prerequisites

Перед началом убедитесь, что у вас есть:

* .NET 6.0 или новее (код также работает на .NET Framework 4.7+)
* Действительная лицензия Aspose.Cells for .NET (для тестирования можно использовать бесплатную оценочную версию)
* Файл Excel (`Source.xlsx`), содержащий сводную таблицу, которую нужно скопировать
* Среда разработки, например Visual Studio 2022

## How to copy pivot table with Aspose.Cells

Основные шаги:

1. **Load Excel workbook C#** – открыть исходный файл.
2. **Select the range that contains the pivot table** – включить всю область сводной таблицы.
3. **Copy the range to a new location** – сводная таблица останется целой.
4. **Save the workbook** – новый файл будет содержать дублированную сводную таблицу.

Каждый шаг подробно объяснен ниже с полным кодом.

### Step 1: Load Excel workbook C#

Загрузка книги — первое действие, когда вы **load excel workbook c#**. Aspose.Cells читает файл в память, предоставляя доступ к листам, ячейкам и сводным таблицам.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the original pivot table
        string sourcePath = @"C:\Data\Source.xlsx";

        // Load the workbook into memory
        Workbook workbook = new Workbook(sourcePath);
```

> **Why this matters:** Loading the workbook creates a `Workbook` object that represents the entire Excel file. All subsequent operations work on this in‑memory representation, which is faster than repeatedly accessing the file system.

### Step 2: Identify and copy the pivot table range

Сводная таблица находится внутри прямоугольного диапазона ячеек. Чтобы **move pivot table cell** безопасно, необходимо копировать весь диапазон, а не отдельные ячейки.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Define the range that encloses the pivot table.
        // Adjust "A1:G20" to match your actual pivot area.
        Range sourceRange = worksheet.Cells.CreateRange("A1:G20");

        // Copy the range to a new location, e.g., starting at I1.
        // The copy operation keeps the pivot table definition and formatting.
        sourceRange.Copy(worksheet.Cells, "I1");
```

> **Why this works:** `Range.Copy` duplicates not only the cell values but also the underlying pivot cache and formatting. This is the recommended way to **duplicate pivot table excel** without rebuilding the pivot manually.

### Step 3: Save the workbook with the copied pivot table

После копирования просто сохраните книгу. Новый файл будет содержать как оригинальную, так и дублированную сводную таблицу.

```csharp
        // Path for the new workbook that will contain the copied pivot table
        string destinationPath = @"C:\Data\CopyPivot.xlsx";

        // Save the workbook; all pivot information is preserved.
        workbook.Save(destinationPath);

        Console.WriteLine("Pivot table copied successfully to " + destinationPath);
    }
}
```

> **Why you should preserve formatting:** The `preserve pivot formatting` requirement is automatically satisfied because Aspose.Cells retains style information during the copy operation. No extra styling code is needed.

### Full working example

Объединив три шага, получаем полную, готовую к запуску программу:

```csharp
using System;
using Aspose.Cells;

class CopyPivotTableDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that contains the pivot table
        string sourceFile = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourceFile);

        // 2️⃣ Identify the pivot table range and copy it
        Worksheet sheet = workbook.Worksheets[0];
        Range pivotRange = sheet.Cells.CreateRange("A1:G20"); // adjust as needed
        pivotRange.Copy(sheet.Cells, "I1"); // copies the pivot table intact

        // 3️⃣ Save the workbook with the duplicated pivot table
        string targetFile = @"C:\Data\CopyPivot.xlsx";
        workbook.Save(targetFile);

        Console.WriteLine($"Copy pivot table operation completed. File saved at: {targetFile}");
    }
}
```

**Expected result:**  
Open `CopyPivot.xlsx` in Excel. You will see the original pivot table unchanged and a second, identical pivot table starting at cell `I1`. All filters, calculated fields, and visual styles match the source.

## Common variations and edge cases

| Situation | How to handle it |
|-----------|------------------|
| **Pivot table spans a dynamic range** | Use `PivotTable.PivotTableRange` to obtain the exact address at runtime instead of hard‑coding `"A1:G20"`. |
| **You need to move the pivot table to another worksheet** | Call `sourceRange.Copy(otherWorksheet.Cells, "A1")` after creating `Worksheet otherWorksheet = workbook.Worksheets[workbook.Worksheets.Add()]`. |
| **Preserving only formatting, not data** | After copying, clear the data values with `targetRange.Clear(ClearOptions.Contents)` while leaving styles untouched. |
| **Large workbooks cause memory pressure** | Use `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` to let Aspose.Cells stream data. |
| **You want to rename the duplicated pivot table** | Access the new pivot via `sheet.PivotTables[sheet.PivotTables.Count - 1]` and set its `Name` property. |

These tips help you **move pivot table cell** positions, **duplicate pivot table excel** files, and keep the **preserve pivot formatting** requirement intact.

## Pro tips for reliable copying

* **Pro tip:** Always verify the source range includes the entire pivot cache. Missing a column can break the copied pivot.
* **Watch out for merged cells** inside the range; they may cause `Copy` to throw an exception. Unmerge before copying or adjust the range.
* **Performance tip:** If you only need to copy the pivot definition (no data), use `PivotTable.Clone` instead of copying the whole range.

## Conclusion

You now know how to **copy pivot table** programmatically in C# using Aspose.Cells while **preserve pivot formatting**, **load excel workbook c#**, and even **move pivot table cell** positions across worksheets. The complete solution loads the workbook, duplicates the pivot range, and saves a new file with both tables intact.

Next, you might explore **duplicate pivot table excel** scenarios such as copying between different workbooks, or automating report generation with multiple pivot tables. For deeper customization, check out Aspose.Cells’ PivotTable API to modify filters, calculated fields, or chart connections.

Happy coding, and feel free to experiment with the code to fit your specific Excel automation needs!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Создать новую книгу Excel – копировать и дублировать сводную таблицу](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Создать сводную таблицу в Excel с помощью Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Эффективно менять макеты сводных таблиц Excel с помощью Aspose.Cells for .NET](/cells/english/net/data-analysis/change-excel-pivot-table-layouts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}