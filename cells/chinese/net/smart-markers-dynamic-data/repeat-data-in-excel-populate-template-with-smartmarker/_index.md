---
category: general
date: 2026-02-21
description: 使用 SmartMarker 快速在 Excel 中重复数据——学习如何填充 Excel 模板并轻松重复行。
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: zh
og_description: 使用 SmartMarker 在 Excel 中重复数据。了解如何填充 Excel 模板、重复行以及自动化您的电子表格。
og_title: 在 Excel 中重复数据 – 使用 SmartMarker 填充模板
tags:
- excel
- csharp
- smartmarker
- automation
title: 在 Excel 中重复数据 – 使用 SmartMarker 填充模板
url: /zh/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

template workbook, and calling `Process`, you can **populate excel template**, **repeat rows in excel**, and generally **". The last line seems cut off. Keep as is.

Translate.

Then closing shortcodes.

Make sure to keep all shortcodes unchanged.

Now produce final translated markdown.

Let's craft translation.

Be careful with bold formatting **...** keep.

Also preserve code placeholders.

Proceed.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中重复数据 – 使用 SmartMarker 填充模板

是否曾经需要 **在 Excel 中重复数据**，却不知如何避免手动复制粘贴？你并不孤单。在许多报表场景中，你会有一列项目需要自动展开为多行，手工操作极易出错。

关键在于——使用 **GemBox.Spreadsheet** 库中的 SmartMarkerProcessor，你只需一行 C# 代码即可 **填充 Excel 模板**，并让行根据集合中的每个项目自动重复。本文将逐步演示完整步骤，提供完整代码，并解释每个环节的意义，让你轻松自如地在 Excel 中重复行。

## 您将学习

* 如何定义驱动重复操作的数据结构。  
* 如何将 `SmartMarkerProcessor` 与包含隐藏模板工作表的工作簿关联。  
* `${Repeat:Item}` 标记如何自动展开为多行。  
* 处理空集合或自定义格式等边缘情况的技巧。  

通过本教程，你将能够 **populate excel from data**，实现可扩展、易维护且适用于任何 .NET 项目的 Excel 填充方式。

---

## 前提条件

* .NET 6.0 或更高版本（代码使用了现代 C# 特性）。  
* **GemBox.Spreadsheet** NuGet 包（免费版支持最多 150 行）。  
* 一个基本的 Excel 模板文件（`Template.xlsx`），其中包含名为 `HiddenTemplate` 的隐藏工作表。  
* 熟悉 C# 对象和 LINQ 有助于理解，但不是必需的。

---

## 步骤 1 – 定义重复数据结构

首先，需要一个 SmartMarker 引擎能够遍历的数据源。在大多数真实项目中，这通常来自数据库、API 或 CSV 文件。为便于说明，这里使用一个匿名类型，包含名为 `Item` 的字符串数组属性。

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **为什么这很重要：** Excel 模板中的 `${Repeat:Item}` 标记会查找名为 `Item` 的属性。如果你更改了属性名称，需要相应地更新标记。这种紧耦合确保模板与代码保持同步，能够 **populate excel template** 而无需猜测列名。

### 常见变体

* **复杂对象：** 你可以提供对象列表（例如 `new[] { new { Name = "A", Qty = 10 } }`），标记将重复行，并且可以在工作表中引用 `${Item.Name}` 和 `${Item.Qty}`。  
* **空集合：** 如果 `Item` 为空，SmartMarker 会直接移除重复块，模板保持不变——非常适合可选章节。

---

## 步骤 2 – 为隐藏模板工作表创建 SmartMarkerProcessor

接下来，加载工作簿并实例化 `SmartMarkerProcessor`。将其指向包含隐藏模板工作表的工作簿；SmartMarker 会将该工作表复制为可见工作表并展开重复标记。

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **专业提示：** 如果同一文件中有多个模板，可以在调用 `processor.Process` 时指定源工作表名称。这在需要为报表的不同部分 **repeat rows in excel** 时非常有用。

### 边缘情况处理

* **缺少模板工作表：** 将加载代码放在 try/catch 中并记录明确的错误信息——可防止文件路径错误导致的静默失败。  
* **大数据集：** 对于成千上万行的情况，考虑将输出流式写入文件（`processor.Save`），而不是全部保存在内存中。

---

## 步骤 3 – 应用数据并展开 `${Repeat:Item}` 标记

现在，使用真正的魔法行来重复行。将步骤 1 中创建的对象传递给 `processor.Process`。SmartMarker 会定位每个 `${Repeat:Item}` 标记，为每个元素复制行，并用实际值替换占位符。

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### 预期结果

打开 `Result.xlsx` 后，隐藏的模板工作表已复制为一个新的可见工作表（默认名称为 `Sheet1`）。原本包含 `${Repeat:Item}` 的行现在出现了三次，单元格分别显示 **A**、**B**、**C**。

| Item |
|------|
| A    |
| B    |
| C    |

如果你添加了 `${Item.Price}` 等列，这些列会自动从数据源填充。

---

## 如何在不使用 SmartMarker 的情况下重复 Excel 行（快速对比）

| 方法                     | 代码复杂度 | 可维护性 | 性能   |
|--------------------------|------------|----------|--------|
| 手动复制‑粘贴            | 高         | 低       | 差     |
| VBA 宏                   | 中         | 中       | 好     |
| **SmartMarkerProcessor** | 低         | 高       | 优秀   |

正如表中所示，使用 SmartMarker 来 **repeat data in excel** 能实现模板设计与业务逻辑的最佳分离。它同样是语言无关的——Java、Python、JavaScript 等库中也有类似概念。

---

## 高级技巧 & 常见陷阱

### 1. 格式化重复的行

SmartMarker 会复制整行——包括单元格样式、边框和条件格式。如果需要为首行或尾行使用不同样式，可添加 `${If:Item.IsFirst}` 等额外标记，并在 Excel 中使用条件公式。

### 2. 处理大数据集

处理超过 10 000 行时，先关闭 Excel 的自动计算功能：

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

保存后再重新启用，以保持性能流畅。

### 3. 从真实数据库填充 Excel

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

随后在模板中使用 `${Repeat:Order}` 列出每个订单。该模式展示了如何直接从 Entity Framework **populate excel from data**。

### 4. 使用多个重复块

同一工作表或不同工作表上可以存在多个 `${Repeat:...}` 标记。SmartMarker 按顺序处理它们，只有当一个块依赖另一个块的输出时，顺序才会产生影响。

---

## 完整可运行示例

下面是一个独立的控制台应用程序示例，可直接粘贴到 Visual Studio 并立即运行。它演示了全部三个步骤以及文件保存。

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**预期输出：** `Result.xlsx` 包含一个工作表，其中 `${Repeat:Item}` 所在的行出现三次，分别显示 A、B、C。无需任何手动调整。

---

## 结论

现在，你已经掌握了通过 SmartMarkerProcessor 高效 **repeat data in excel** 的方法。只需定义简单的数据对象、加载模板工作簿并调用 `Process`，即可 **populate excel template**、**repeat rows in excel**，并且能够在各种 .NET 项目中轻松复用。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}