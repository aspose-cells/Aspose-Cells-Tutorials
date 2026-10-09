---
category: general
date: 2026-03-29
description: 学习如何使用 C# 将 Excel 表导出为纯文本、将字符串写入文件，以及将 Excel 表转换为 CSV 或 TXT。包括完整代码和技巧。
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: zh
og_description: 如何在 C# 中将 Excel 表导出为文本文件。获取完整的解决方案、代码以及将 Excel 表转换并保存为 TXT 文件的最佳实践。
og_title: 如何导出 Excel 数据 – 完整的 C# 教程
tags:
- C#
- Excel
- File I/O
title: 如何导出 Excel 数据——一步一步的 C# 指南
url: /zh/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何导出 Excel 数据 – 完整 C# 指南

是否曾经想过 **如何在不手动打开电子表格的情况下导出 Excel** 数据？也许你需要将表格转存为一个简单的文本文件供旧系统使用，或者想快速生成 CSV 供数据分析管道使用。在本教程中，我们将一步步演示一个实用的端到端解决方案，**将字符串写入文件**，并准确展示 **如何将 Excel 表格** 数据转换为分隔文本格式（使用 C#）。

我们会覆盖从加载工作簿、选择目标表格、配置导出选项，到最终保存为 `.txt` 文件的全部过程。完成后，你将能够 **将表格导出为 CSV**（或任意你选择的分隔符），并了解一些 **在 C# 项目中保存 txt 文件** 的小技巧。无需外部工具——只需几个 NuGet 包和一点代码。

---

## 你需要准备的环境

- **.NET 6.0+**（如果你更喜欢经典框架，也可以使用 .NET Framework 4.7.2）
- **Syncfusion.XlsIO** NuGet 包（`ExportTableOptions` 类就在这里）
- 任意 C# IDE（Visual Studio、VS Code、Rider 都可以）
- 一个包含至少一个表格的 Excel 工作簿（示例中使用 `ws.Tables[0]`）

> 小技巧：如果还没有 Syncfusion 库，可在命令行运行  
> `dotnet add package Syncfusion.XlsIO.Net.Core`。

---

## 步骤 1 – 打开工作簿并获取第一个表格  

首先加载 Excel 文件并获取包含表格的工作表引用。这一步至关重要，因为 **convert excel table** 操作是基于 `ITable` 对象，而不是原始单元格范围。

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*为什么重要：* 使用 `using` 打开工作簿可以确保所有非托管资源被释放，避免在后续 **write string to file** 时出现文件锁定问题。

---

## 步骤 2 – 配置导出选项（纯文本、无标题、分号分隔）  

接下来告诉 Syncfusion 我们希望如何序列化表格。`ExportTableOptions` 允许你切换是否包含标题、选择分隔符，以及决定返回字符串还是字节数组。

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*为什么重要：* 将 `IncludeHeaders = false` 常常符合下游系统已经知道列顺序的预期。更改分隔符就是实现 **export table as CSV** 并使用自定义分隔符的方式。

---

## 步骤 3 – 将表格导出为字符串  

准备好选项后，调用 `ExportToString`。该方法会提取整个表格（包括所有行），并返回一个可直接写入文件的单一字符串。

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*为什么重要：* `ExportToString` 完成了将 Excel 网格转换为分隔格式的核心工作。它会遵循你设置的 `Delimiter`，从而得到干净的 **export table as csv** 结果，无需额外处理。

---

## 步骤 4 – 将导出的文本写入文件  

最后，将字符串持久化到磁盘。`File.WriteAllText` 是最简洁的 **save txt file C#** 方法；如果文件不存在会自动创建，若已存在则覆盖。

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*为什么重要：* 直接写入字符串可以避免额外的转换步骤。文件内容将类似 `Value1;Value2;Value3`，即可供任何下游解析器使用。

---

## 完整工作示例（所有步骤合并）  

下面是可直接复制粘贴的完整程序，包含错误处理和注释，便于理解。

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**预期输出**（`ExportedTable.txt` 的内容）：

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

每一行对应原始 Excel 表格中的一行，值之间用分号分隔。如果将 `Delimiter = ","`，则会得到经典的 CSV 文件。

---

## 常见问题与边缘情况  

### 我的工作簿有多个表格怎么办？  
只需将 `ws.Tables[0]` 改为相应的索引，或遍历 `ws.Tables`：

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### 如何包含列标题？  
在 `ExportTableOptions` 中将 `IncludeHeaders = true`。当下游系统需要标题行时非常有用。

### 能否动态导出到不同文件夹？  
完全可以。使用 `Path.Combine` 与 `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` 或任意用户提供的路径组合，提升灵活性。

### 大文件怎么办？  
对于超大表格，考虑流式写入而不是一次性加载整个字符串到内存：

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### 这在 .NET Core 上可用吗？  
可以——Syncfusion.XlsIO 支持 .NET 5/6/7。只需引用对应的 NuGet 包即可。

---

## 稳定导出的专业技巧  

- **在写入前验证文件路径**。缺失的目录会抛出 `DirectoryNotFoundException`。  
- **仅在表格能 comfortably fit in memory 时使用 `ExportAsString`**；否则使用 `ExportToStream` 处理超大数据集。  
- **注意文化设置**：如果数据中使用逗号作小数点，请选择分号 (`;`) 或制表符 (`\t`) 作为分隔符，以避免 CSV 解析错误。  
- **锁定版本**：Syncfusion 有时会更改 API 签名。通过在项目文件中写入 `<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />` 来固定 NuGet 版本，确保构建可复现。

---

## 结论  

本指南演示了 **如何使用 C# 将 Excel 表格导出为纯文本文件**。通过加载工作簿、配置 `ExportTableOptions`、将表格导出为字符串，最后 **将字符串写入文件**，你已经掌握了处理 **convert excel table**、**export table as csv** 与 **save txt file C#** 任务的可靠模式。

欢迎自行实验——更换分隔符、包含标题，或遍历多个表格。相同的思路同样适用于生成 CSV 报表、向旧系统提供数据，或仅仅将电子表格内容归档为轻量级文本文件。

还有其他场景想要实现吗？比如 **异步写入字符串到文件**，或在写入时即时压缩。请查看我们后续的 *C# 异步文件 I/O* 与 *使用 .NET 压缩文件* 教程，继续保持学习热情。

祝编码愉快！ 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}