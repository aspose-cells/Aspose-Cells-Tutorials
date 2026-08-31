---
category: general
date: 2026-02-21
description: 将 Excel 保存为 txt，精确控制有效数字。使用 C# 将 Excel 导出为 txt，轻松设置有效数字。
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: zh
og_description: 快速将 Excel 保存为 txt。学习如何使用 C# 导出 Excel 为 txt、设置有效数字并控制文本输出。
og_title: 将 Excel 保存为 txt – 在 C# 中导出保留有效数字的数值
tags:
- C#
- Aspose.Cells
- Excel automation
title: 将 Excel 保存为 txt – 完整的 C# 指南：导出带有效数字的数字
url: /zh/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 Excel 保存为 txt – 完整的 C# 指南：导出带有效数字的数字

是否曾经想要 **将 Excel 保存为 txt**，但担心数字会失去精度？你并不孤单。许多开发者在尝试将 Excel 导出为 txt 时会遇到小数位过多或被四舍五入的困扰。  

在本教程中，我们将展示一种直接的方式来 **将 Excel 导出为 txt**，并 **设置有效数字**，使输出恰好符合你的需求。完成后，你将拥有一段可直接运行的 C# 代码片段，能够将工作簿保存为文本、导出数字到 txt，并完全控制数字格式。

## 你将学到

- 如何创建新工作簿并写入数值数据。  
- 使用 `TxtSaveOptions` 正确 **设置有效数字**。  
- 如何 **将工作簿保存为文本** 并验证结果。  
- 边缘情况处理（大数、负数、地区设置问题）。  
- 进一步微调输出的快速技巧（分隔符更改、编码）。

### 前置条件

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.6+）。  
- **Aspose.Cells** NuGet 包（`Install-Package Aspose.Cells`）。  
- 对 C# 语法有基本了解——不需要深入的 Excel interop 知识。

> **专业提示：** 如果你使用 Visual Studio，请启用 *nullable reference types*（`<Nullable>enable</Nullable>`），以便提前捕获潜在的空引用错误。

---

## 步骤 1：初始化工作簿并写入数字

首先，需要一个工作簿对象。可以把它看作是 Excel 文件的内存表示。  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**为什么这很重要：**  
以编程方式创建工作簿可以避免 COM interop 的开销，且 `PutValue` 会自动检测数据类型，确保单元格被视为数字而非字符串。

---

## 步骤 2：配置 TxtSaveOptions 以控制有效数字

`TxtSaveOptions` 类是实现关键的地方。通过设置 `SignificantDigits`，你告诉 Aspose.Cells 在写文件时保留多少个有意义的数字。

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**为何需要设置它：**  
在 **导出数字到 txt** 时，通常需要一个简洁的表示（例如，仅接受特定精度的报表系统）。`SignificantDigits` 属性保证无论原始数字长度如何，都能得到一致的四舍五入结果。

---

## 步骤 3：将工作簿保存为文本文件

现在使用刚才定义的选项将工作簿写入磁盘。

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**你将看到的结果：**  
打开 `Numbers.txt`，会得到一行内容：

```
12350
```

原始的 `12345.6789` 已被四舍五入为 **四个有效数字**，正如需求所示。

---

## 步骤 4：验证输出（可选但推荐）

编写自动化测试是个好习惯。下面是一段可以在保存后立即运行的快速检查代码：

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

运行此代码块后，如果一切匹配，将会打印绿色对勾，让你确信 **save excel as txt** 操作如预期般工作。

---

## 常见变体与边缘情况

### 导出多个单元格或范围

如果需要 **导出 excel to txt** 整个范围，只需在保存前填充更多单元格：

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

相同的 `TxtSaveOptions` 将对每个值应用 4 位规则，产生：

```
12350
0.0001235
-98800
```

### 更改分隔符

某些下游系统要求制表符分隔的值。可以这样调整分隔符：

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

现在每行中的单元格将以制表符分隔。

### 处理地区特定的小数分隔符

如果你的用户使用逗号作为小数点，请设置相应的文化信息：

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

输出将遵循地区设置，将 `12350` 显示为 `12 350`（法语中的千位空格）。

---

## 完整可运行示例（复制‑粘贴即用）

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**预期的 `Numbers.txt` 内容（默认分隔符，4 个有效数字）：**

```
12350	0.0001235	-98800
```

示例中保留了默认的制表符（`\t`）作为分隔符；如果你更喜欢 CSV，可以改为逗号。

---

## 结论

现在你已经掌握了在 **保存 Excel 为 txt** 时控制有效数字的完整方法。创建工作簿、设置 `TxtSaveOptions.SignificantDigits`、保存这三个步骤，即可可靠地 **export excel to txt**。  

接下来你可以：

- 为更大数据集 **export numbers to txt**。  
- 调整分隔符、编码或文化设置，以匹配任何下游系统。  
- 在导出前结合 Aspose.Cells 的其他功能（样式、公式）使用。

试着运行一下，修改 `SignificantDigits` 为 2 或 6，观察输出如何变化。**save workbook as text** 的灵活性使其成为任何数据交换管道中的实用工具。

---

### 你可能感兴趣的相关主题

- **Export Excel to CSV** 并自定义列顺序。  
- **Read txt files back into a workbook**（使用 `Workbook.Load` 与 `LoadOptions`）。  
- **Batch processing** 多工作表并合并为一个 txt 文件。  
- **Performance tuning** 大规模导出（流式 vs. 内存）。

如果遇到问题或想分享自己的导出定制方案，欢迎留言。祝编码愉快！  

---  

*图片：生成的 `Numbers.txt` 文件截图，显示已四舍五入的数值。*  
*替代文字：“Numbers.txt 文件显示 12350、0.0001235 和 -98800，使用 4 个有效数字保存 Excel 为 txt”。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}