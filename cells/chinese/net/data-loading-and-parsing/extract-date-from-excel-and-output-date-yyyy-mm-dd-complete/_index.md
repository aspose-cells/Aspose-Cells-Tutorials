---
category: general
date: 2026-03-18
description: 从 Excel 中提取日期并以 ISO 格式输出 yyyy‑mm‑dd。学习如何读取日本元号日期、进行转换，并在 C# 中显示 ISO 日期。
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: zh
og_description: 从 Excel 中提取日期并以 ISO 格式 yyyy‑mm‑dd 输出。一步一步的 C# 教程，包含完整代码和解释。
og_title: 从 Excel 提取日期 – 在 C# 中输出 yyyy‑mm‑dd 格式的日期
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: 从 Excel 提取日期并输出为 yyyy‑mm‑dd 格式 – 完整 C# 指南
url: /zh/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 Excel 提取日期 – 如何以 ISO 格式输出 yyyy‑mm‑dd 日期

是否曾需要 **extract date from Excel**，但不确定如何处理日本年号日期或获取干净的 `yyyy‑mm‑dd` 字符串？你并不孤单。在许多数据迁移项目中，源工作簿使用日本天皇历存储日期，而下游系统期望类似 `2024-04-01` 的 ISO 合规日期。  

在本指南中，我们将逐步演示一个完整且可运行的解决方案，读取单元格、解释日本年号，并 **outputs the date yyyy‑mm‑dd**。结束时，你将确切了解如何在任何 .NET 应用中 **display date ISO format**，并拥有一个可复用的代码片段，可直接放入你的项目中。

## 你需要的条件

- **.NET 6+**（或 .NET Framework 4.7.2+）。  
- **Aspose.Cells for .NET** – 该库允许我们在加载工作簿时设置自定义日历。  
- 一个 Excel 文件 (`japan-date.xlsx`)，其中的日期存储在日本年号单元格中（例如 `令和3年4月1日`）。  
- 一个常用的 IDE —— Visual Studio、Rider，甚至 VS Code 都可以。

除了 Aspose.Cells 外，不需要其他 NuGet 包，代码可在 Windows、Linux 或 macOS 上运行。

## 步骤 1：设置项目并安装 Aspose.Cells

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** 如果你在 CI 服务器上，固定包版本（`Aspose.Cells 23.12`）以确保可重复构建。

## 步骤 2：使用日本天皇历加载工作簿

当源使用非公历时，**extract date from Excel** 的关键是告诉 Aspose.Cells 在加载时使用哪个日历。我们使用 `LoadOptions.Calendar` 来实现。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**Why this matters:** 如果不使用自定义日历，Aspose.Cells 会把单元格当作普通字符串处理，年号信息会丢失。通过分配 `JapaneseEmperorCalendar`，库会在后台自动将 `令和3年4月1日` 转换为 `2021‑04‑01`。

## 步骤 3：从特定单元格检索日期

现在工作簿已经知道如何解释年号，我们可以将单元格读取为 `DateTime`。假设日期位于第一个工作表的单元格 **A1**（第 0 行，第 0 列）。

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

如果单元格为空或包含非日期值，`GetDateTime()` 会抛出异常。防御性写法如下：

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**Edge case:** 某些旧的 Excel 文件将日期存储为数字（序列号）。Aspose.Cells 会自动处理这些，但如果你预期内容混合，仍应验证单元格类型。

## 步骤 4：输出 yyyy‑mm‑dd（ISO）日期并验证

拿到 `DateTime` 后，将其格式化为 **output date yyyy‑mm‑dd** 只需一行代码：

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

对包含 `令和3年4月1日` 的文件运行程序将输出：

```
Extracted date (ISO): 2021-04-01
```

这正是许多 API 所需的 **display date iso format**。

## 完整可运行示例

将所有部分组合起来，以下是完整的、可直接复制粘贴的程序：

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **Note:** 将 `YOUR_DIRECTORY` 替换为实际包含 `japan-date.xlsx` 的文件夹。代码适用于任何工作表和任何单元格——只需调整索引。

## 处理其他日历（可选）

如果你需要 **extract date from Excel** 使用泰国佛教历或希伯来历，只需更换日历实例：

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

其余逻辑保持不变，这展示了该方法的灵活性。

## 常见陷阱及规避方法

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| `GetDateTime()` throws `InvalidCastException` | 单元格不是日期（可能是字符串） | 在调用前检查 `Cell.Type`，或对 `Cell.StringValue` 使用 `DateTime.TryParse`。 |
| Wrong year after conversion | 加载工作簿时未设置 `Calendar` | 始终在打开文件之前使用适当的日历创建 `LoadOptions`。 |
| ISO output shows time part (`2021-04-01 00:00:00`) | 使用了未指定格式的 `ToString()` | 使用 `"yyyy-MM-dd"` 格式说明符以强制 **output date yyyy‑mm‑dd**。 |
| File not found | 相对路径指向错误的文件夹 | 使用 `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` 或提供绝对路径。 |

## 生产级代码的专业提示

1. 如果需要从同一文件读取多个日期，请 **Cache the workbook** —— 打开工作簿相对耗时。  
2. 将提取逻辑 **Wrap the extraction logic** 包装成可复用的方法：

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. 将原始年号字符串（`cell.StringValue`）与 ISO 输出一起 **Log the original era string**，以便审计追踪。  
4. 使用包含不同年号（平成、令和）的若干硬编码 Excel 文件对该方法进行 **Unit test**，以确保正确性。

## 可视化概览

Below is a quick diagram illustrating the data flow—from Excel cell to ISO string.  

![从 Excel 提取日期示例，显示 Excel → LoadOptions → DateTime → ISO 字符串]  

*Alt text: “extract date from excel” 图示显示转换流程。*

## 结论

我们已经介绍了 **extract date from Excel** 所需的全部内容，处理日本年号值，并 **output date yyyy‑mm‑dd** 以符合现代 API 喜爱的 **display date iso format**。该解决方案独立完整，适用于任何支持 Aspose.Cells 的 .NET 版本，并且只需一行代码即可扩展到其他日历。

有其他日历需求吗？或者你正在从多列提取日期？随时修改 `ExtractIsoDate` 辅助方法或在下方留言。祝编码愉快，愿你的日期始终保持完美的 ISO 同步！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}