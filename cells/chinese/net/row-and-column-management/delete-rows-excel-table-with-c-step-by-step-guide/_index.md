---
category: general
date: 2026-02-28
description: 快速在 C# 中删除 Excel 表格的行。学习如何添加命名范围、按名称访问工作表，并避免重复名称错误。
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: zh
og_description: 使用 C# 删除 Excel 表格中的行。本教程还展示了如何添加命名范围以及如何按名称访问工作表。
og_title: 使用 C# 删除 Excel 表格中的行 – 完整指南
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: 使用 C# 删除 Excel 表格中的行 – 步骤指南
url: /zh/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 删除 Excel 表格中的行 – 完整编程教程

是否曾需要从工作簿中 **delete rows excel table**，但不确定该使用哪个 API 调用？你并不是唯一遇到这种情况的人——大多数开发者在首次尝试以编程方式裁剪表格时都会碰到同样的难题。  

在本指南中，我们将通过一个完整、可运行的示例，演示如何从 Excel 表格中删除行，同时展示 **how to add defined name**（即 *named range*）、**access worksheet by name** 的用法，以及在另一工作表上添加重复名称时为何会抛出 `InvalidOperationException`。  

阅读完本文后，你将能够：

* 使用工作表标签名称获取工作表。  
* 安全地删除该工作表上第一个表格的数据行。  
* 创建指向特定地址的命名范围。  
* 理解跨工作表重复名称的潜在问题。

无需外部文档——所有内容都在这里。

---

## 您需要的环境

* **DevExpress Spreadsheet**（或任何提供 `Workbook`、`Worksheet`、`ListObject` 和 `Names` 对象的库）。  
* 目标为 **.NET 6** 或更高版本的 .NET 项目（代码同样可以在 .NET Framework 4.8 上编译）。  
* 对 C# 有基本了解——只要会写 `foreach` 循环即可上手。

> **专业提示：** 如果你使用的是 DevExpress 免费的 Community Edition，下面使用的 API 与商业版完全相同。

---

## 第一步 – 通过名称访问工作表

首先需要定位包含要修改表格的工作表。  
很多开发者习惯性地使用 `Worksheets[0]`，但这会把代码耦合到工作表顺序，一旦有人重命名标签就会出错。

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*为什么这很重要：* 通过使用工作表的 **name** 而不是索引，可以避免在工作簿结构变化时误编辑错误的工作表。  

如果提供的名称不存在，库会抛出 `KeyNotFoundException`，你可以捕获它并显示友好的错误信息。

---

## 第二步 – 删除 Excel 表格中的行（安全方式）

有了正确的工作表后，接下来删除第一个表格中的数据行。  
常见错误是调用 `DeleteRows(1, rowCount‑1)`。自 **DevExpress 22.2** 起，该重载已被 **禁止**，会抛出 `InvalidOperationException`。库要求在表格的数据范围内删除行，而不是删除标题行。

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **如果表格为空怎么办？** `if` 判断会阻止在 `rowCount = 0` 时调用删除方法，从而避免异常。

### 可视化概览  

![删除行 Excel 表格示例](image.png "显示从 Excel 表格中删除行的截图")  

*Alt 文本：C# 代码中的 delete rows excel table 示例*

---

## 第三步 – 如何添加已定义名称（创建命名范围）

清理完表格后，你可能想在以后引用特定范围——比如用于图表或数据验证列表。这时 **add named range excel** 就派上用场了。

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

`Names.Add` 方法接受两个参数：标识符和 A1 样式的地址。  
因为我们之前已经 **access worksheet by name**，所以地址字符串可以安全地引用任意工作表，而无需担心索引变化。

---

## 第四步 – 在另一工作表上使用命名范围 – 避免重复名称错误

你可能会认为可以在不同工作表上复用相同的标识符，例如：

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

然而，Excel 的命名作用域是 **工作簿级别**，而不是按工作表。上述调用会触发 `InvalidOperationException`，并显示消息 *“A name with the same identifier already exists.”*  

### 解决办法

1. **Pick a unique name** (`MyTable_Sheet2`)。  
2. **Delete the existing name** 再重新添加（仅在确实想替换时使用）。  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## 完整、可运行的示例

将所有步骤整合在一起，下面是一个自包含的控制台应用程序示例，你可以直接放入 Visual Studio 并对 `sample.xlsx` 文件运行。

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**预期结果**

* **Sheet1** 上第一个表格的所有数据行被删除，只剩标题行。  
* 名称 **MyTable** 现在指向 `Sheet1!$A$1:$C$5`。  
* 第二个名称 **MyTable_Sheet2** 安全地引用 **Sheet2** 上的范围，且不会抛出异常。

---

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| *What if the workbook has multiple tables?* | 通过索引获取正确的 `ListObject`（`worksheet.ListObjects[1]`）或通过名称获取（`worksheet.ListObjects["MyTable"]`）。 |
| *Can I delete rows from a table that spans multiple worksheets?* | 不可以——表格只能位于单个工作表。需要对每个工作表分别执行删除逻辑。 |
| *Is there a way to delete only a subset of rows?* | 可以——使用 `table.DeleteRows(startRow, count)`，其中 `startRow` 是表格数据区域内的零基索引。 |
| *Do named ranges survive after saving?* | 当然。调用 `SaveDocument` 后，命名范围会写入工作簿的 XML 中。 |
| *How do I list all defined names in the workbook?* | 使用 `foreach (var name in workbook.Names) Console.WriteLine(name.Name);` 进行遍历。 |

---

## 结论

我们已经使用 C# 讲解了 **delete rows excel table**，演示了 **add named range excel**，并展示了正确的 **access worksheet by name** 用法，以避免恼人的重复名称异常。  

完整的解决方案就在上面的代码片段中——复制、粘贴并在自己的文件上运行即可。之后你可以扩展逻辑以处理多个表格、动态范围计算，甚至集成到 UI 中。

**接下来可以探索的方向：**

* 使用 **named range on another sheet** 为图表系列提供数据。  
* 将删除逻辑与 **ExcelDataReader** 结合，在清理前导入数据。  
* 使用 `foreach (var file in Directory.GetFiles(...))` 循环，实现对数十个工作簿的批量更新。

对 C# 中的 Excel 自动化还有其他疑问吗？留下评论，让我们继续交流。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}