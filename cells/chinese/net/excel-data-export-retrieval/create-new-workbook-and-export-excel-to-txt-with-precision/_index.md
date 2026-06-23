---
category: general
date: 2026-02-15
description: 创建新工作簿并在设置数值精度的同时将 Excel 导出为 TXT。学习在 C# 中设置有效数字并限制有效数字。
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: zh
og_description: 创建新工作簿并将 Excel 导出为 TXT，设置数值精度的有效数字。一步步的 C# 指南。
og_title: 创建新工作簿 – 精准导出 Excel 为 TXT
tags:
- C#
- Aspose.Cells
- Excel automation
title: 创建新工作簿并精确导出 Excel 为 TXT
url: /zh/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

them as is.

Also the block shortcodes at top and bottom remain unchanged.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建新工作簿 – 将 Excel 导出为 TXT 并精确控制数字格式

是否曾想过如何在 C# 中 **创建新工作簿** 对象并立即将其转存为纯文本文件？你并不是唯一有此需求的人。在许多数据管道场景中，我们需要 **导出 Excel 为 TXT**，同时保持数字可读，这意味着要限制小数点后出现的位数。

在本教程中，我们将完整演示整个过程：从创建全新的工作簿、配置导出以 **设置有效数字**（即限制有效数字），到最终将文件写入磁盘。完成后，你将拥有一个可直接运行的代码片段，满足你的 **数值精度** 要求——无需额外库，也不需要魔法。

> **专业提示：** 如果你已经在使用 Aspose.Cells，下面展示的类都是该库的一部分。如果你使用的是其他平台，概念仍然适用，只需替换相应的 API 调用即可。

---

## 你需要准备的内容

- .NET 6+（代码在 .NET Core 和 .NET Framework 上均可编译）  
- Aspose.Cells for .NET（免费试用版或授权版）– 通过 NuGet 安装：`dotnet add package Aspose.Cells`  
- 任意你喜欢的 IDE（Visual Studio、Rider、VS Code）  

就这些。无需额外的配置文件，也没有隐藏的步骤。

---

## 第一步：创建新工作簿

首先要 **创建新工作簿**。把 `Workbook` 类想象成一个空的 Excel 文件，等待你添加工作表、单元格和数据。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **为何重要：** 从一个干净的工作簿开始，可以避免后续可能影响精度设置的隐藏格式。

---

## 第二步：配置文本保存选项 – 设置有效数字

接下来告诉 Aspose.Cells 在写入 `.txt` 文件时希望保留多少 **有效数字**。`TxtSaveOptions` 类提供了 `SignificantDigits` 属性，正是用来完成此操作的。

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **解释：** `SignificantDigits = 5` 表示导出器会保留每个数字最重要的五位，无论小数点位于何处。这是一种在不手动格式化每个单元格的情况下 **设置数值精度** 的便捷方式。

---

## 第三步：将工作簿保存为纯文本文件

当工作簿和选项都准备好后，我们终于 **导出 Excel 为 txt**。`Save` 方法接受文件路径和我们刚配置的选项对象。

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

运行程序后会生成如下文件：

```
12346
0.00012346
3.1416
```

可以看到，每个数字都遵循了我们之前设置的 **限制有效数字** 规则。

---

## 第四步：验证结果（可选但推荐）

可以直接在任意编辑器中打开生成的 `numbers.txt`，但在 CI 流水线中，你可能希望自动化验证步骤。

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

如果控制台显示上面的三行内容，说明你已经成功 **设置有效数字**，导出工作如预期运行。

---

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| 数字出现过多小数位 | `SignificantDigits` 保持默认值 (0) | 明确将 `SignificantDigits` 设置为所需的位数 |
| 创建了空文件 | 保存前工作簿未写入任何数据 | 在调用 `Save` 之前 **先填充单元格** |
| 文件路径抛出 `UnauthorizedAccessException` | 试图写入受保护的文件夹 | 使用有写入权限的文件夹（例如 `C:\Temp` 或 `%USERPROFILE%\Documents`） |
| 对极小数字的精度不符合预期 | 有效数字计数包括小数点后的前导零 | 记住“有效数字”会忽略前导零；例如 0.000123456 使用 5 位会变为 `0.00012346` |

---

## 完整可运行示例（复制粘贴即用）

下面是完整的、独立的程序示例。将其粘贴到新的控制台项目中并运行 **Run**。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**预期的控制台输出**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

`numbers.txt` 文件将包含上面展示的三行内容。

---

## 后续步骤：深入探索

- **导出其他格式** – Aspose.Cells 还支持 CSV、HTML 和 PDF。根据需要将 `TxtSaveOptions` 替换为 `CsvSaveOptions` 或 `PdfSaveOptions`。  
- **动态精度** – 可以在运行时根据用户输入或配置文件计算 `SignificantDigits`。  
- **多工作表** – 遍历 `workbook.Worksheets`，为每个工作表导出单独的 `.txt` 文件。  
- **本地化** – 如需匹配地区设置，可通过 `CultureInfo` 控制小数分隔符（`.` 与 `,`）。  

所有这些扩展仍然基于我们本教程的核心思路：**创建新工作簿**、配置导出、并 **设置数值精度** 以满足报告需求。

---

## 小结

我们从一个全新的 **创建新工作簿** 实例出发，填充数据，并演示了如何 **导出 Excel 为 TXT**，同时 **设置有效数字** 以限制输出精度。完整示例可直接运行，且每行代码背后的 *why* 已经解释清楚，方便你在自己的项目中进行适配。

尽情实验吧——修改 `SignificantDigits` 的值、添加更多工作表，或切换输出格式。如果遇到问题，请查阅 Aspose.Cells 文档或在下方留言。祝编码愉快！

---

![创建新工作簿示例](/images/create-new-workbook.png "展示 C# IDE 中创建新工作簿代码的截图")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}