---
"description": "使用 Aspose.Cells for .NET 轻松更新 Excel 中的 Power Query 公式项。循序渐进的指南，简化您的数据操作流程。"
"linktitle": "更新 Power Query 公式项"
"second_title": "Aspose.Cells for .NET API参考"
"title": "更新 Power Query 公式项"
"url": "/zh/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 更新 Power Query 公式项

## 介绍

如果您曾经使用过 Excel，您就会知道它的强大之处——尤其是在您开始深入研究 Power Queries 时。这些是让您轻松转换、清理和分析数据的秘诀。在 Excel 中操作 Power Query 公式的一种巧妙方法是使用 Aspose.Cells for .NET。今天，我们将逐步指导您更新 Power Query 公式项。所以，戴上您的编程帽，让我们开始吧！

## 先决条件

在深入研究代码之前，您需要设置一些内容：

1. Visual Studio：您需要一个集成开发环境 (IDE) 来编写和运行 .NET 代码。Visual Studio 是您的首选。
2. Aspose.Cells 库：确保您的项目中已安装 Aspose.Cells 库。您可以从 [地点](https://releases。aspose.com/cells/net/).
3. C# 基础知识：虽然我们将一起完成这一过程，但对 C# 有一些基础知识的了解肯定会有所帮助，尤其是在浏览不同的类和方法时。
4. 示例 Excel 文件：您需要代码片段中提到的 Excel 文件。请确保您拥有：
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework：确保您的项目针对的是 .NET Framework 的兼容版本。

现在我们已经准备好了工具包，我们可以继续进行有趣的部分：编写代码！

## 导入包

首先，你需要导入必要的命名空间。操作方法如下：

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

通过添加这些命名空间，您可以让编译器知道您打算使用 Aspose.Cells 库中的类和方法。此步骤至关重要，因为它为后续的代码奠定了基础。

让我们分解一下您提供的代码片段。本教程将引导您完成每个部分，确保您理解其中的含义。

## 步骤 1：设置工作目录

在此步骤中，我们将定义源文件和输出文件的位置。这确保 Aspose 知道在哪里查找您的 Excel 文件。

```csharp
// 工作目录
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## 第 2 步：加载工作簿

现在，让我们加载 Power Query 所在的 Excel 文件。

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
这 `Workbook` 类是进入 Excel 文件的入口点。通过传递源文件的路径，我们创建了一个允许我们操作它的实例。你可以把它想象成打开一本书——你正准备阅读（或编辑）它的内容。

## 步骤 3：访问数据混搭

接下来，我们将访问存储在工作簿的数据混搭中的 Power Query 公式。

```csharp
DataMashup mashupData = workbook.DataMashup;
```
这 `DataMashup` 类包含与您的工作簿关联的所有 Power Query 公式。我们将在这里完成繁重的工作，就像您打开工具箱进行维修一样。

## 步骤 4：循环遍历 Power Query 公式

现在我们遍历 Power Query 公式来找到我们想要更新的特定公式。

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

- 我们循环遍历每一个 `PowerQueryFormula` 在 `mashupData`。
- 在这个循环中，我们深入研究每一个 `PowerQueryFormulaItem`。
- 我们检查该项目的名称是否与“Source”匹配。如果匹配，我们将更新其值以链接到我们的新源文件。

这类似于在手册中找到正确的页面，然后进行必要的更新——这是一个简单而细致的过程。

## 步骤 5：保存更新的工作簿

完成更新后，就该保存我们的更改了。

```csharp
// 保存输出工作簿。
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
这 `Save` 方法将更新后的工作簿写入指定的输出目录。这就像将您的编辑内容封存在新版本的手册中，供其他人使用！

## 结论

恭喜！您已成功使用 Aspose.Cells for .NET 更新 Power Query 公式项。使用此方法，您可以自动修改 Excel 文件中的 Power Query 公式，从而节省宝贵的时间和精力。

## 常见问题解答

### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的库，用于在 .NET 应用程序中操作 Excel 文件，而无需安装 Microsoft Excel。

### 我需要 Microsoft Excel 来运行 Aspose.Cells 吗？
不，Aspose.Cells 使您能够以编程方式创建和编辑 Excel 文件，而无需在服务器或开发机器上安装 Excel。

### 我可以使用 Aspose.Cells 处理哪些类型的 Excel 文件？
您可以使用 Aspose.Cells 处理 .xlsx、.xls、.xlsm 和其他几种 Excel 格式。

### Aspose.Cells 有试用版吗？
是的，您可以从 [Aspose Cells发布页面](https://releases。aspose.com/).

### 我如何获得 Aspose.Cells 的支持？
您可以通过以下方式获得支持 [Aspose 论坛](https://forum.aspose.com/c/cells/9)，您可以在这里提出问题并从社区和 Aspose 团队那里找到答案。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}