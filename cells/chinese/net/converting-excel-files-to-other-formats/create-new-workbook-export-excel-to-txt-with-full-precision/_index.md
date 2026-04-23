---
category: general
date: 2026-03-18
description: 创建新工作簿并在保持数值精度的情况下将 Excel 导出为 TXT。了解如何将工作表保存为 txt 并高效地将工作表转换为 txt。
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: zh
og_description: 创建新工作簿并精确导出 Excel 为 TXT。本教程展示如何将工作表保存为 txt，以及使用 C# 将工作表转换为 txt。
og_title: 创建新工作簿 – Excel 导出为 TXT 指南
tags:
- Aspose.Cells
- C#
- Excel automation
title: 创建新工作簿 – 将 Excel 导出为 TXT（全精度）
url: /zh/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建新工作簿 – 将 Excel 导出为 TXT 并保留完整精度

是否曾经需要在 C# 中 **create new workbook** 只为将一些数据转储到纯文本文件中？也许你正在从旧系统提取报告，而下游工具只接受 `.txt` 输入。好消息是？你无需牺牲数值精度，也完全不必手动编写 CSV 字符串。

在本指南中，我们将完整演示 **export excel to txt** 的整个过程，涵盖从初始化工作簿到在 **save worksheet as txt** 时保留尾随零的所有步骤。完成后，你将拥有一段可直接运行的代码片段，可放入任何 .NET 项目中——无需额外工具。

## 你需要的准备

- **ASP.NET/.NET 6+**（代码同样适用于 .NET Framework 4.6+）  
- **Aspose.Cells for .NET** – 为 `Workbook`、`Worksheet` 和 `TxtSaveOptions` 类提供支持的库。你可以通过 `Install-Package Aspose.Cells` 从 NuGet 获取。  
- 对 C# 有基本了解（如果你熟悉 `using` 语句，就可以直接上手）。  

就是这么简单——无需 Excel interop、COM 对象，绝对不需要手动字符串拼接。

---

## 步骤 1：初始化新工作簿（Primary Keyword）

首先要做的就是 **create new workbook**。可以把工作簿想象成一块空白画布，随后你将在其上粘贴数字、文本或公式。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **为什么这很重要：** 实例化 `Workbook` 而不加载文件会得到一个全新的空白页。随后你可以以编程方式添加数据，这在没有现有 `.xlsx` 文件的 **convert worksheet to txt** 场景中尤为适用。

## 步骤 2：填充单元格 – 保留尾随零

在将数字转储为文本时，一个常见的陷阱是丢失尾随零（`123.45000` 变成 `123.45`）。如果下游系统依赖固定宽度字段，这种丢失会导致全部出错。

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **技巧提示：** `PutValue` 会自动推断数据类型。如果你需要一个看起来像数字的字符串，请改用 `PutValue("123.45000")`。

## 步骤 3：配置 TXT 保存选项 – 保留数值精度

这就是关键所在。通过切换 `PreserveNumericPrecision`，你可以指示 Aspose.Cells 写入你输入的精确值，包括任何无意义的尾随零。

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **为什么要启用它？** 当你 **save excel as txt** 时，默认行为会去除多余的小数位。将 `PreserveNumericPrecision = true` 设置为真，可确保输出与单元格显示的值完全一致，这对财务报告或科学数据至关重要。

## 步骤 4：将工作表保存为 TXT – 最终导出

现在我们真正执行 **save worksheet as txt**。你可以将路径指向任何有写入权限的位置；示例使用了名为 `output` 的相对文件夹。

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **预期输出** (`num-preserve.txt`):

```
123.45000
```

请注意，尾随零保持完整——正是你所要求的。

## 步骤 5：验证结果 – 快速检查

程序运行后，用任意文本编辑器打开 `num-preserve.txt`。你应该看到唯一一行 `123.45000`。如果看到的是 `123.45`，请再次确认 `PreserveNumericPrecision` 已设为 `true`，并且使用的是最新版本的 Aspose.Cells（v23.10+）。

## 常见变体与边缘情况

### 导出多个单元格或范围

如果需要对整个范围执行 **export excel to txt**，只需在保存前填充更多单元格：

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

默认情况下，Aspose 会将每个单元格写入新行。你也可以通过 `txtSaveOptions.Separator` 更改分隔符（制表符、逗号）。

### 使用不同编码将工作表转换为 TXT

有时下游系统需要 UTF‑8 BOM 或 ASCII。可以这样调整编码：

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### 处理大型工作簿

处理包含数十万行的大型工作表时，考虑使用流式输出：

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

## 专业技巧与注意事项

- **不要忘记在调用 `Save` 之前创建输出目录**，否则会抛出 `DirectoryNotFoundException`。  
- **留意区域设置特定的小数分隔符**。如果你的环境使用逗号（`1,23`），请将 `txtSaveOptions.DecimalSeparator = '.'` 设置为点号。  
- **版本兼容性**：`PreserveNumericPrecision` 标志在 Aspose.Cells 20.6 中引入。如果使用更旧的版本，则不存在该标志，需要在保存前将单元格格式化为文本。

![创建新工作簿示例](excel-to-txt.png "创建新工作簿")

*图片替代文字: “创建新工作簿并将 Excel 导出为 TXT，保留数值精度”*

## 回顾 – 我们覆盖的内容

- **Create new workbook** 使用 Aspose.Cells。  
- 填充包含尾随零的数字到单元格。  
- 将 `TxtSaveOptions.PreserveNumericPrecision = true` 设置为 **save excel as txt**，以防止精度丢失。  
- 将文件写入磁盘，并验证输出与原始值相匹配。  
- 这就是完整的 **convert worksheet to txt** 工作流，代码不超过 50 行 C#。

## 下一步与相关主题

既然你已经能够使用完美精度 **export excel to txt**，可以进一步探索以下内容：

- **Exporting to CSV** 使用自定义分隔符（`TxtSaveOptions.Separator`）。  
- **Saving as other plain‑text formats** 如 TSV（`SaveFormat.TabDelimited`）。  
- **Batch processing** 使用 `Directory.GetFiles` 对文件夹中的多个工作簿进行批处理。  
- **Integrating with Azure Functions** 在云端实现按需转换。  

这些都基于相同的 `Workbook` → `Worksheet` → `TxtSaveOptions` 模式，你会感到非常熟悉。

### 最后思考

如果你已经跟随完成，你现在清楚地知道如何 **create new workbook**、填充数据，并在 **save worksheet as txt** 时保留所有关心的小数位。这段代码虽小，却解决了在旧系统管道要求纯文本输入时常见的头疼问题。

试一试，微调选项，让数据以你需要的方式流动。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}