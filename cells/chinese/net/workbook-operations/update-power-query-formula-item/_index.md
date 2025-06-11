---
"description": "通过本全面的分步指南了解如何使用 Aspose.Cells for .NET 更新 Excel 中的 Power Query 公式。"
"linktitle": "更新工作簿中的 Power Query 公式项"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "更新工作簿中的 Power Query 公式项"
"url": "/zh/net/workbook-operations/update-power-query-formula-item/"
"weight": 27
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 更新工作簿中的 Power Query 公式项

## 介绍
对于任何数据分析师或 Excel 爱好者来说，了解如何在 Excel 中使用 Power Query 高效管理数据都至关重要。如果您曾经需要更新 Power Query 工作簿中的公式项，那么您来对地方了。本指南旨在帮助您学习如何使用 Aspose.Cells for .NET 无缝更新 Excel 工作簿中的 Power Query 公式。只需几个简单的步骤，您就能操作和简化数据，确保您的工作簿保持动态和集中化。
## 先决条件
在开始深入研究示例代码和步骤之前，让我们先了解一下您需要什么：
1. 对 C# 和 .NET 的基本了解：熟悉 C# 中的编程概念将会很有帮助，因为我们将编写一些代码。
2. 安装 Aspose.Cells for .NET：您需要将 Aspose.Cells 库集成到您的 .NET 项目中。您可以下载 [这里](https://releases。aspose.com/cells/net/).
3. 准备好修改的 Excel 文件：确保您拥有一个包含要更新的 Power Query 的 Excel 文件。您需要一个示例工作簿，例如 `SamplePowerQueryFormula.xlsx` 供您使用。
## 导入包
首先，请确保您的 C# 文件中包含以下命名空间：
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
这将允许您访问 Aspose.Cells 库提供的功能，特别是处理工作簿和 Power Query 数据。
## 步骤 1：设置工作目录
首先，您需要定义源文件和输出文件的位置。 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
在此步骤中，您将指定目录路径。替换 `"Your Document Directory"` 替换为 Excel 文件的实际保存路径。这会告诉程序在哪里查找源文件以及在哪里保存更新后的文件。
## 第 2 步：加载工作簿
现在您已经设置了工作目录，下一步是将 Excel 文件加载到程序中。
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
在这里，您可以创建一个 `Workbook` 加载指定 Excel 文件的对象。 `Workbook` 该类是 Aspose.Cells 库的一部分，对于您在该 Excel 文件上执行的任何操作都至关重要。
## 步骤 3：访问 Power Query 数据
工作簿加载完成后，就可以访问其中存储的 Power Query 公式了。
```csharp
DataMashup mashupData = workbook.DataMashup;
```
在这一行中， `DataMashup` 属性有助于访问工作簿中的 Power Query 数据结构。此属性使您能够与 Excel 文件中包含的 Power Query 数据的各个方面进行交互。
## 步骤 4：循环遍历 Power Query 公式
在可以访问 Power Query 数据的情况下，下一步是遍历现有的每个公式。
```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```
奇迹就在这里发生。我们循环遍历每一个 `PowerQueryFormula` 然后通过每一个 `PowerQueryFormulaItem`。 这 `if` 语句查找名为“Source”的公式项，并将其值更新为您希望 Power Query 引用的源文件的路径。这使您可以动态更改 Power Query 从中提取数据的文件。
## 步骤 5：保存更新的工作簿
更新必要的公式项后，最后一步是保存工作簿。
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
此行将修改后的工作簿保存到新文件中，从而保留原始文件，同时允许您使用更新的版本。
## 步骤6：确认消息
最后，检查代码是否正确执行是一种很好的做法。
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
这个简单的消息将在控制台中向您确认您的操作已成功，为该过程提供令人放心的结束。
## 结论
就这样！使用 Aspose.Cells for .NET 更新 Excel 中的 Power Query 公式项只需几个简单的步骤即可完成。按照本指南，您可以高效地管理 Excel 数据连接，并确保工作簿运行顺畅。无论您是经验丰富的专业人士，还是数据处理新手，Aspose.Cells 都能为您提供强大的方法来自动化和增强 Excel 工作流程。 
## 常见问题解答
### 我可以将 Aspose.Cells 与任何版本的 .NET 一起使用吗？
Aspose.Cells 与多个版本的 .NET 兼容，包括 .NET Framework 和 .NET Core。
### Aspose.Cells 可以免费使用吗？
Aspose.Cells 提供免费试用，但如需持续使用，则需要许可证。您可以获取临时许可证 [这里](https://purchase。aspose.com/temporary-license/).
### 如果我现有的 Excel 文件没有 Power Query 怎么办？
所描述的过程重点是更新 Power Query 项目，因此如果您的文件缺少它们，则需要先合并 Power Queries。
### 在哪里可以找到有关 Aspose.Cells 的更多信息？
查看文档，获取全面的指导和示例。访问 [文档](https://reference。aspose.com/cells/net/).
### 如何报告 Aspose.Cells 的错误或问题？
您可以访问其支持的论坛以获取有关您遇到的任何问题的帮助。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}