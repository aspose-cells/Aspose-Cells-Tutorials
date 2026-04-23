---
category: general
date: 2026-02-26
description: 如何使用 C# 将 Excel 导出为制表符分隔的 txt 文件。学习将 Excel 导出为制表符、将 Excel 转换为 txt，以及在三个简单步骤中使用分隔符导出
  Excel。
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: zh
og_description: 如何使用 C# 将 Excel 导出为制表符分隔的 txt 文件。本教程展示了将 Excel 导出为制表符、将 Excel 转换为
  txt，以及使用分隔符导出 Excel。
og_title: 如何导出 Excel – 制表符分隔文本指南
tags:
- csharp
- excel
- file-conversion
title: 如何导出 Excel – 制表符分隔文本指南
url: /zh/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

keep markdown for blockquotes, lists, etc.

Also images: keep unchanged.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何导出 Excel – 完整 C# 教程

有没有想过 **如何导出 Excel** 数据到纯文本文件而不丢失格式？也许你需要一个快速的 TSV（制表符分隔值）用于数据管道，或者你正在向只能读取 `.txt` 的旧系统提供数据。无论哪种情况，你并不孤单——开发者在将数据从电子表格导出时经常会碰到这个难题。

好消息是？只需三个简单步骤，你就可以 **导出 Excel 为制表符** 分隔的文本，**将 Excel 转换为 txt**，甚至在以后改变主意时自定义分隔符。下面你会看到一个完整可运行的 C# 示例、每行代码的意义以及一些避免常见陷阱的技巧。

> **Pro tip:** 这种方法使用流行的 Aspose.Cells 库，但其概念同样适用于任何提供 `ExportTable`‑style 方法的 .NET Excel API。

## 需要的环境

- **.NET 6+**（或 .NET Framework 4.6+）。代码可以在任何近期的运行时编译。
- **Aspose.Cells for .NET**（免费试用或正式授权）。通过 NuGet 安装：`dotnet add package Aspose.Cells`。
- 一个名为 `input.xlsx` 的工作簿，放在你可控的文件夹中。
- 一点好奇心——不需要深入了解 Excel 内部实现。

如果你已经准备好这些，就直接进入解决方案吧。

## 第一步 – 加载要导出的工作簿

首先我们创建一个指向源文件的 `Workbook` 对象。该对象代表整个 Excel 文件，包括所有工作表、命名范围和格式。

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Why this matters:*  
加载工作簿后，你才能访问工作表集合（`workbook.Worksheets`）。没有这个对象，你就无法定位单元格、范围或导出设置。

> **Note:** 如果你的文件位于网络共享，前面加上 `\\` 或使用 UNC 路径——Aspose.Cells 能很好地处理。

## 第二步 – 配置导出选项（字符串值 & 制表符分隔）

接下来告诉库我们希望如何写出数据。将 `ExportAsString = true` 设置为强制每个单元格都被视为普通字符串，从而消除 Excel 区域设置导致的数字格式差异。`Delimiter = "\t"` 部分正是 **导出 Excel 为制表符** 的核心。

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Why this matters:*  
如果省略 `ExportAsString`，包含 `12345` 的单元格在某些地区可能会变成 `12,345`，从而破坏下游解析器。分隔符可以在以后换成逗号、管道符或任何字符，以实现 **导出 Excel 使用自定义分隔符** 的需求。

## 第三步 – 将特定范围导出为文本文件

最后，我们选取关心的范围（本例中为 `A1:D10`），并写入 `out.txt`。`ExportTable` 方法完成所有繁重工作：读取单元格、应用选项并将结果流式写入磁盘。

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

运行后，你会在 `out.txt` 中看到如下内容：

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

每列之间用 **制表符** 分隔，方便 `awk`、`PowerShell` 或任何支持制表符的 CSV 工具使用。

### 快速验证

在纯文本编辑器（记事本、VS Code）中打开生成的文件并确认：

1. 启用 “显示空白字符” 后列对齐。
2. 没有额外的引号或逗号出现。
3. 所有数值单元格与 Excel 中显示的完全一致（得益于 `ExportAsString`）。

如果发现异常，请检查源工作簿是否隐藏了行/列，并确保引用了正确的工作表索引。

## 常见变体与边缘情况

### 导出整个工作表

如果想 **导出 Excel 范围** 包含整张工作表，可以使用 `sheet.Cells.MaxDisplayRange`：

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### 使用不同的分隔符

将制表符换成管道符（`|`）只需改动一行代码：

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

这样即可满足 **导出 Excel 使用自定义分隔符** 的场景，而无需重写其他代码。

### 处理大文件（> 100 MB）

对于超大工作簿，使用流式导出以避免一次性加载全部内容到内存：

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### 一次性转换多个工作表

如果需要为多个工作表 **将 Excel 转换为 txt**，可以遍历它们：

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

每个工作表都会生成自己的 TSV 文件——非常适合批处理任务。

## 完整可运行示例（复制‑粘贴即用）

下面是完整程序代码，直接编译即可。只需将文件路径替换为你的实际路径。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**预期输出：** 一个名为 `out.txt` 的文件，所有列均由制表符分隔，且每个单元格的值与 Excel 中完全一致。

## 常见问答

- **这能处理 .xls 文件吗？**  
  能。Aspose.Cells 会自动检测格式，你只需将 `Workbook` 指向旧版 `.xls`，其余代码保持不变。

- **如果我的数据中包含制表符怎么办？**  
  单元格内的制表符会被保留，这可能会导致 TSV 解析器出错。此时可通过修改 `exportOptions.Delimiter` 为管道符（`|`）来规避。

- **能导出公式而不是数值吗？**  
  将 `exportOptions.ExportAsString = false` 并使用包含 `ExportFormula = true` 的 `ExportTableOptions` 重载。输出将包含原始公式文本。

- **有没有办法跳过隐藏的行？**  
  有。将 `exportOptions.ExportHiddenRows = false`（默认 `true`）即可。隐藏的行将不会出现在最终的文本文件中。

## 结论

现在，你已经掌握了一套可靠、可投入生产的方案，能够 **导出 Excel 数据为制表符分隔的文本文件**，实现 **导出 Excel 为制表符**，以及 **将 Excel 转换为 txt**，并对分隔符和范围选择拥有完整控制。借助 Aspose.Cells 的 `ExportTable` 方法，你可以避免手动构造 CSV，保持数据完整性，同时让代码保持简洁。

准备好迎接下一个挑战了吗？试试：

- 直接导出到 `MemoryStream` 用于 Web API。  
- 根据首行内容动态添加表头行。  
- 将此例程集成到监控存储桶新 Excel 上传的 Azure Function 中。

动手试一试，调整分隔符，让数据流向你需要的任何地方。祝编码愉快！

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}