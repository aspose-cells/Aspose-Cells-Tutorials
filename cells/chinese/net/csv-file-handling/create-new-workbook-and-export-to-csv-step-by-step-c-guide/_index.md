---
category: general
date: 2026-04-07
description: 在 C# 中创建新工作簿并学习如何导出保留有效数字的 CSV。包括将工作簿另存为 CSV 以及导出 Excel 为 CSV 的技巧。
draft: false
keywords:
- create new workbook
- save workbook as csv
- how to export csv
- save file as csv
- export excel to csv
language: zh
og_description: 在 C# 中创建新工作簿并将其导出为 CSV，全面控制有效数字。学习将工作簿保存为 CSV 并将 Excel 导出为 CSV。
og_title: 创建新工作簿并导出为 CSV – 完整 C# 教程
tags:
- C#
- Aspose.Cells
- CSV export
- Excel automation
title: 创建新工作簿并导出为 CSV – 步骤详解 C# 指南
url: /zh/net/csv-file-handling/create-new-workbook-and-export-to-csv-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建新工作簿并导出为 CSV – 完整 C# 教程

是否曾经在 C# 中**创建新工作簿**后，想知道*如何导出 CSV*而不丢失精度？你并不是唯一遇到这种情况的人。在许多数据管道项目中，最终步骤是生成干净的 CSV 文件，而正确的格式化往往让人头疼。

在本指南中，我们将完整演示整个过程：从创建全新的工作簿、向其中写入数值、配置导出选项以保留有效数字，最后**将工作簿保存为 CSV**。完成后，你将拥有一个可直接使用的 CSV 文件，并对使用 Aspose.Cells 的*export excel to CSV*工作流有深入了解。

## 需要的环境

- **Aspose.Cells for .NET**（NuGet 包 `Aspose.Cells` – 版本 23.10 或更高）。  
- .NET 开发环境（Visual Studio、Rider 或 `dotnet` CLI）。  
- 基础的 C# 知识；不需要高级的 Excel interop 技巧。  

就这些——无需额外的 COM 引用，也不需要安装 Excel。

## 第一步：创建新的 Workbook 实例

首先，我们需要一个全新的 workbook 对象。可以把它想象成一个完全驻留在内存中的空白电子表格。

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();
```

> **为什么要这样做？** `Workbook` 类是 Aspose.Cells 中进行任何 Excel 操作的入口。以编程方式创建它意味着不依赖已有文件，从而让**save file as CSV**步骤保持简洁且可预测。

## 第二步：获取第一个工作表

每个工作簿默认至少包含一个工作表。我们将获取第一个工作表并为其设置一个友好的名称。

```csharp
// Step 2: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "Data";
```

> **小技巧：** 重命名工作表在后续使用支持工作表名称的查看器打开 CSV 时会更易辨识，尽管 CSV 本身并不存储工作表名称。

## 第三步：向单元格 A1 写入数值

现在我们在 A1 中插入一个小数位数多于最终需要保留的数字，以演示*significant digits*（有效数字）功能。

```csharp
// Step 3: Write a numeric value into cell A1
worksheet.Cells["A1"].PutValue(12345.6789);
```

> **如果需要更多数据怎么办？** 只需在其他单元格（如 `B2`、`C3` …）继续使用 `PutValue`——相同的导出设置将在**save workbook as CSV**时应用于整个工作表。

## 第四步：配置导出选项以保留有效数字

Aspose.Cells 允许你控制数字在 CSV 输出中的呈现方式。这里我们设置保留四位有效数字并启用该功能。

```csharp
// Step 4: Configure export options to use significant digits
ExportOptions exportOptions = new ExportOptions
{
    SignificantDigits = 4,      // keep only 4 significant digits
    UseSignificantDigits = true // enable the feature
};
```

> **为什么使用有效数字？** 在处理科学数据或财务报告时，你更关心精度而非单纯的小数位数。此设置确保 CSV 反映预期的准确度，这在*how to export CSV*用于下游分析时是常见需求。

## 第五步：将工作簿保存为 CSV 文件

最后，使用我们刚才定义的选项，将工作簿以 CSV 格式写入磁盘。

```csharp
// Step 5: Save the workbook as a CSV file using the configured options
string outputPath = @"C:\Temp\out.csv";
workbook.Save(outputPath, SaveFormat.Csv, exportOptions);
```

> **预期输出：** 文件 `out.csv` 将包含一行内容：

```
12350
```

可以看到 `12345.6789` 被四舍五入为 `12350`——这正是保留四位有效数字的效果。

### 保存 CSV 的快速检查清单

- **路径是否存在：** 确保目录（示例中的 `C:\Temp`）已创建，否则 `Save` 会抛出异常。  
- **文件权限：** 进程必须拥有写入权限，否则会出现 `UnauthorizedAccessException`。  
- **编码：** Aspose.Cells 默认使用 UTF‑8，适用于大多数地区。如果需要其他代码页，请在调用 `Save` 前设置 `exportOptions.Encoding`。

## 常见变体与边缘情况

### 导出多个工作表

CSV 本质上是单工作表格式。如果对包含多个工作表的工作簿调用 `Save`，Aspose.Cells 会将它们串联起来，并在每个工作表之间插入换行。若只想**save file as CSV**特定工作表，请临时隐藏其他工作表：

```csharp
// Hide all sheets except the one you want to export
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.IsVisible = false;
}
worksheet.IsVisible = true; // the sheet we prepared earlier
workbook.Save(outputPath, SaveFormat.Csv, exportOptions);
```

### 控制分隔符

默认情况下，Aspose.Cells 使用逗号（`,`）作为分隔符。如果针对欧洲地区需要分号（`;`），请调整 `CsvSaveOptions`：

```csharp
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    Separator = ';',
    ExportOptions = exportOptions
};
workbook.Save(outputPath, csvOptions);
```

### 大数据集

导出数百万行时，建议使用流式写入以避免高内存占用。Aspose.Cells 提供接受 `Stream` 的 `Workbook.Save` 重载，能够直接写入文件、网络位置或云存储。

## 完整示例代码

下面是完整的、可直接运行的程序示例。复制粘贴到控制台应用项目中，按 **F5** 运行。

```csharp
using System;
using Aspose.Cells;

namespace CsvExportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Get the first worksheet and give it a name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Insert a numeric value (more precision than we need)
            worksheet.Cells["A1"].PutValue(12345.6789);

            // 4️⃣ Set up export options – 4 significant digits
            ExportOptions exportOptions = new ExportOptions
            {
                SignificantDigits = 4,
                UseSignificantDigits = true
            };

            // 5️⃣ Define where the CSV will be saved
            string outputPath = @"C:\Temp\out.csv";

            // 6️⃣ Save as CSV using the configured options
            workbook.Save(outputPath, SaveFormat.Csv, exportOptions);

            Console.WriteLine($"CSV file created at: {outputPath}");
        }
    }
}
```

运行程序后，在记事本或 Excel 中打开 `C:\Temp\out.csv`。你应该会看到四舍五入后的值 `12350`，这表明*export excel to CSV*并保留有效数字的功能如预期工作。

## 小结

我们已经覆盖了**创建新工作簿**、填充数据、调节导出精度以及最终**save workbook as CSV**的全部步骤。关键要点如下：

- 使用 `ExportOptions` 在*how to export CSV*时控制数字格式。  
- 使用 `Save` 方法并指定 `SaveFormat.Csv` 是实现**save file as CSV**的最简方式。  
- 在高级场景下，可调整分隔符、工作表可见性或使用流式输出。

### 接下来可以尝试什么？

- **批量处理：** 循环遍历多个数据表，一次性生成多个 CSV。  
- **自定义格式：** 将 `NumberFormat` 与 `ExportOptions` 结合，实现货币或日期样式。  
- **集成：** 使用流式重载直接将 CSV 推送到 Azure Blob Storage 或 S3 存储桶。

欢迎尝试上述思路，如遇到问题请留言讨论。祝编码愉快，愿你的 CSV 导出始终保持正确的有效数字！

![C# 工作簿保存为 CSV 文件的示意图 – 创建新工作簿](/images/create-new-workbook-csv.png "创建新工作簿示意图")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}