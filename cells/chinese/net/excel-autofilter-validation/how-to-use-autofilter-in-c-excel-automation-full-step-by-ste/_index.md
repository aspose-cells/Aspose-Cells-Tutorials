---
category: general
date: 2026-05-30
description: 如何在 C# Excel 自动化中使用 AutoFilter。学习如何创建 Excel 工作簿、按值筛选行，并简化您的电子表格任务。
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: zh
og_description: 如何在 C# Excel 自动化中使用 AutoFilter。掌握创建 Excel 工作簿、按值过滤行以及轻松自动化电子表格的技巧。
og_title: 如何在 C# Excel 自动化中使用 AutoFilter – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: 如何在 C# Excel 自动化中使用 AutoFilter – 完整分步指南
url: /zh/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# Excel 自动化中使用 AutoFilter – 完整指南

有没有想过在使用 C# 代码生成 Excel 文件时**如何使用 AutoFilter**？你并不孤单——许多开发者在需要隐藏不符合特定条件的行时都会遇到这个难题。  

在本教程中，我们将通过一个具体且可运行的示例，**创建 Excel 工作簿**、添加表格，然后**按列 B 的值过滤行**。完成后，你将拥有一段干净、可复用的代码片段，能够直接嵌入任何需要 Excel 自动化的 C# 项目中。

## 你将学到

- 使用 Aspose.Cells（或 Microsoft.Office.Interop）库搭建 C# 项目。  
- **以编程方式创建 Excel 工作簿**并添加样式化表格。  
- 应用 **AutoFilter** 只显示 **列 B** 等于特定字符串的行。  
- 完全移除过滤，恢复完整数据集。  
- 处理缺失列或多重过滤条件等边缘情况的技巧。

无需任何 Excel‑VBA 经验；只要具备基本的 C# 与 NuGet 包使用知识即可。

---

## 前置条件

| 需求 | 重要原因 |
|------|----------|
| .NET 6.0 或更高（或 .NET Framework 4.7+） | 现代运行时提供更好的性能和更简便的包管理。 |
| 通过 NuGet 安装 Aspose.Cells for .NET（或 Microsoft.Office.Interop.Excel） | 此库提供我们在代码中使用的 `Workbook`、`Worksheet` 和 `Table` 对象。 |
| 代码编辑器（Visual Studio、VS Code、Rider 等） | 你需要编译并运行示例。 |
| 基本的 C# 知识 | 本教程解释每行代码的*原因*，而不仅仅是*作用*。 |

你可以使用以下方式安装 Aspose.Cells：

```bash
dotnet add package Aspose.Cells
```

---

## 如何在 C# 中使用 Aspose.Cells 的 AutoFilter

下面是完整的、独立的程序示例。将其保存为 `Program.cs` 于控制台项目中并运行——你将在输出文件夹中得到 `FilteredWorkbook.xlsx`。

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### 代码工作原理

1. **创建工作簿** – `new Workbook()` 会生成一个空文件；`Worksheets[0]` 获取默认工作表。  
2. **填充示例数据** – 我们写入一小段数据，以便直观看到过滤效果。  
3. **添加表格** – `ListObjects.Add` 将范围转换为 Excel 表格，表格会自动支持过滤和样式。  
4. **应用 AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` 表示：“仅显示第二列（B）等于 *Apple* 的行”。  
5. **保存文件** – 会生成两个文件：一个带过滤，一个移除过滤，以证明 `RemoveAutoFilter()` 正常工作。

> **专业提示：** 如果需要按多个条件过滤（例如 “Apple” *或* “Banana”），使用重载 `Filter(int columnIndex, string criteria1, string criteria2)` 或传入字符串数组。

---

## 按值过滤行 – 常见变体

虽然上例侧重于 **过滤列 B**，你可能想过滤其他列或使用数值条件。下面是快速参考表：

| 期望的过滤条件 | 代码片段 |
|----------------|----------|
| 列 C 文本匹配 | `table.AutoFilter.Filter(2, "Cherry");` |
| 列 C 中大于 10 的数字 | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| 列 B 中的多个值 | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**边缘情况：** 如果列标题拼写错误或列索引超出范围，Aspose.Cells 会抛出 `ArgumentException`。在应用过滤前，可通过检查 `table.ListColumns.Count` 来防止此类错误。

---

## 移除 AutoFilter – 何时重置

有时需要重新展示完整数据集（例如用户清空搜索框后）。只需一行代码 `table.RemoveAutoFilter()` 即可完成。如果使用 Microsoft.Office.Interop，则调用 `worksheet.AutoFilterMode = false;`。

---

## 完整示例回顾

下面再次提供**完整程序**，已去除注释，适合希望快速浏览的读者：

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

运行后会生成两个文件：

- **FilteredWorkbook.xlsx** – 仅显示 *Apple* 行。  
- **UnfilteredWorkbook.xlsx** – 恢复原始数据。

---

## 常见问题

**Q: 这能用于旧的 .xls 文件吗？**  
A: 能。Aspose.Cells 只需更改文件扩展名或使用 `SaveOptions` 即可保存为 `.xls` 或 `.xlsx`。

**Q: 如果需要在工作簿已经保存后再过滤怎么办？**  
A: 使用 `new Workbook("path.xlsx")` 加载文件，应用过滤后再次 `Save`。

**Q: 能对不是表格的范围应用过滤吗？**  
A: 完全可以。使用 `worksheet.AutoFilter.Range = "A1:C5";` 然后 `worksheet.AutoFilter.ApplyFilter();`。不过表格自带样式和更便捷的列引用。

---

## 图片 – 可视化确认

![显示在使用 C# 创建的 Excel 工作簿中对列 B 应用 AutoFilter 的截图](/images/autofilter-column-b.png "AutoFilter on column B")

*(该图片展示了仅保留包含 “Apple” 的行的过滤视图。)*

---

## 结论

我们已经完整演示了在 **C# 驱动的 Excel 自动化** 场景中**如何使用 AutoFilter**——从**创建 Excel 工作簿**、**按列 B 的值过滤行**，到**在不需要时移除过滤**。初始化、添加表格、应用过滤、清理的核心步骤，可在任何需要 **excel automation c#** 的项目中复用。

准备好迎接下一个挑战了吗？可以尝试：

- 为过滤后的行添加条件格式以突出显示。  
- 将过滤后的数据导出为 CSV 供下游处理。  
- 组合多个过滤条件（例如 “Apple” *且* 数量 > 8）。

动手实验，发现问题并解决它们——

## 接下来该学习什么？

- [如何在 .NET 中使用 Aspose.Cells 实现 Excel AutoFilter（数据分析指南）](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [如何在 Aspose.Cells .NET 中使用 Autofilter Not Contains 进行 Excel 数据分析](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 实现 Excel Autofilter ‘EndsWith’](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}