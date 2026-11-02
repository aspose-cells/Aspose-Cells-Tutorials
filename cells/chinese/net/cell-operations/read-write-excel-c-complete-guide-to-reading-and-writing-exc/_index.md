---
category: general
date: 2026-03-01
description: 《读写Excel C# 教程》展示了如何使用 C# 和 Aspose.Cells 通过几个简单步骤读取 Excel 单元格的值并写入日期时间到
  Excel。
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: zh
og_description: Read write Excel C# 教程解释了如何读取 Excel 单元格的值以及将日期时间写入 Excel，提供清晰的代码示例和最佳实践。
og_title: 读取和写入 Excel C# – 步骤指南
tags:
- C#
- Excel
- Aspose.Cells
title: 读写 Excel C# – Excel 单元格读取与写入完整指南
url: /zh/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 读取写入 Excel C# – 完整指南：读取和写入 Excel 单元格

是否曾尝试 **read write Excel C#**，却遇到晦涩的异常或日期不匹配？你并不孤单。许多开发者在需要从工作表中提取日本元号日期并将正确的 `DateTime` 再写回同一单元格时都会卡壳。

在本指南中，我们将逐步演示如何使用 C# 和强大的 Aspose.Cells 库 **read excel cell value** 并 **write datetime to excel**。完成后，你将拥有一个可直接放入任何 .NET 项目的独立可运行示例。

## 你将学到的内容

- 如何在 .NET 6+ 项目中安装并引用 Aspose.Cells。  
- 获取包含日本元号字符串（如 `"R3/5/12"`）的单元格的完整代码。  
- 使用 `"ja-JP"` 区域信息将该字符串解析为 `DateTime`。  
- 将得到的 `DateTime` 写回同一工作表单元格的步骤。  
- 处理空单元格或意外元号格式等边缘情况的技巧。  

不需要任何 Excel interop 经验——只要对 C# 和 .NET 有基本了解即可。让我们开始吧。

![读取写入 Excel C# 操作的截图，显示 B2 单元格在转换前后的状态](read-write-excel-csharp.png "read write excel c# example")

## 步骤 1：搭建项目 – Read Write Excel C# 基础

在编写代码之前，需要先搭建好基础环境。

1. **创建一个新的控制台应用**（或任意 .NET 项目），目标框架为 .NET 6 或更高：

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **添加 Aspose.Cells NuGet 包**。它是一个完全托管的库，无需 COM interop：

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **将 Excel 文件** (`EraDates.xlsx`) **复制到项目根目录**。该工作簿应包含名为 `"Sheet1"` 的工作表，且单元格 **B2** 的值类似 `"R3/5/12"`（即令和 3 年 5 月 12 日）。

以上即为所有准备工作。接下来我们将重点关注实际的 **read excel cell value** 与 **write datetime to excel** 逻辑。

## 步骤 2：使用 C# 读取 Excel 单元格值

项目准备就绪后，先从工作表中获取字符串。下面的代码片段演示了完整的调用链：

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**工作原理说明：** `Cell.StringValue` 始终返回显示的文本，无论底层数字格式如何。这保证我们拿到的正是用户看到的 `"R3/5/12"` 字符串。

### 常见陷阱

- **空单元格** – `StringValue` 会返回空字符串。解析前请先进行判断。  
- **意外格式** – 若单元格内容为 `"2023/05/12"`，元号解析器会抛异常；此时需要提供回退方案。

## 步骤 3：使用 C# 将 DateTime 写入 Excel

拿到元号字符串后，我们使用 `DateTime.ParseExact` 进行解析。格式 `"ggyy/MM/dd"` 告诉 .NET 期待一个日本元号（`gg`）、两位年份（`yy`）以及月份/日期。

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**为何使用 `PutValue`：** Aspose.Cells 会自动检测 .NET 类型并写入相应的 Excel 单元格类型。传入 `DateTime` 会生成真正的 Excel 日期，后续可以进行格式化或在公式中使用。

### 边缘情况与技巧

- **时区** – `DateTime` 对象不包含时区信息。如需 UTC，请调用 `DateTime.SpecifyKind`。  
- **区域回退** – 若需支持其他地区，可将解析包装在一个尝试多个 `CultureInfo` 的辅助方法中。  
- **性能** – 处理成千上万行时，复用单个 `CultureInfo` 实例，而不是在每次循环中新建。

## 步骤 4：完整可运行示例 – 综合演示

下面是完整的、可直接运行的程序。将其复制粘贴到 `Program.cs`，确保 `EraDates.xlsx` 与编译后的二进制文件同目录，然后执行 `dotnet run`。

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**预期输出**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

打开 `EraDates_Converted.xlsx` 后，单元格 **B2** 将显示普通日期（例如 `5/12/2021`），并可像其他日期值一样在 Excel 中进行计算。

## 编写健壮的 Read Write Excel C# 代码的专业技巧

- **写入前先验证** – 使用 `Cell.IsFormula` 或 `Cell.Type` 防止意外覆盖公式。  
- **批量处理** – 若需转换整列，可遍历 `ws.Cells.Columns[1]`（B 列）并应用相同逻辑。  
- **线程安全** – Aspose.Cells 对象不是线程安全的；并行时请为每个线程创建独立的 `Workbook` 实例。  
- **日志记录** – 生产脚本中请用专业日志框架（如 Serilog）替代 `Console.WriteLine`，以捕获解析失败信息。  
- **单元测试** – 编写针对已知元号字符串的单元测试，断言返回的 `DateTime` 是否正确。

## 结论

通过本教程，你已经掌握了 **read write Excel C#** 的完整流程：**read excel cell value**、解析日本元号字符串、并 **write datetime to excel**。完整示例展示了一个清晰的端到端工作流，可根据需要扩展到批量操作、不同地区或 Excel‑到‑数据库的管道。

接下来可以尝试将脚本扩展为处理整列元号日期，或探索 Aspose.Cells 丰富的格式化功能为输出单元格添加样式。你也可以尝试 EPPlus、ClosedXML 等其他库——大部分逻辑保持不变，仅 API 调用不同。

有问题或遇到棘手的 Excel 场景？欢迎在下方留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}