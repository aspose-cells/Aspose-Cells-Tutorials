---
title: 在 .NET 中以编程方式在输出 HTML 中指定 HTML CrossType
linktitle: 在 .NET 中以编程方式在输出 HTML 中指定 HTML CrossType
second_title: Aspose.Cells .NET Excel 处理 API
description: 了解如何在 Aspose.Cells for .NET 中指定 HTML CrossType。按照我们的分步教程将 Excel 文件精确转换为 HTML。
weight: 17
url: /zh/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以编程方式在输出 HTML 中指定 HTML CrossType

## 介绍
在 .NET 应用程序中将 Excel 文件转换为 HTML 时，您可能会发现自己需要指定如何在输出中处理交叉引用。Aspose.Cells for .NET 中的 HtmlSaveOptions 类提供了各种设置来控制转换过程，其中一个选项是 HtmlCrossType。在本教程中，我们将介绍如何在将 Excel 文件导出为 HTML 格式时以编程方式指定 HTML 交叉类型。 
## 先决条件
在深入研究代码之前，请确保您已具备以下条件：
-  Aspose.Cells for .NET：确保您的项目中安装了 Aspose.Cells 库。您可以从[Aspose 网站](https://releases.aspose.com/cells/net/).
- Visual Studio：Visual Studio 或任何其他 .NET 开发环境的工作安装。
- C# 基础知识：熟悉 C# 编程将帮助您更好地理解示例。
- 示例 Excel 文件：准备好示例 Excel 文件以供使用。在本例中，我们将使用`sampleHtmlCrossStringType.xlsx`.
## 导入包
首先，您需要导入必要的 Aspose.Cells 命名空间。操作方法如下：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
让我们逐步分解它，以便您可以轻松地跟随并在自己的项目中实现此功能。
## 步骤 1：定义源和输出目录
首先，您需要设置源 Excel 文件的目录以及要保存输出 HTML 文件的目录。
```csharp
//源目录
string sourceDir = "Your Document Directory";
//输出目录
string outputDir = "Your Document Directory";
```
## 步骤 2：加载示例 Excel 文件
接下来，将示例 Excel 文件加载到`Workbook`对象。这就是所有魔法开始的地方。
```csharp
//加载示例 Excel 文件
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
在这里，替换`"Your Document Directory"`替换为 Excel 文件所在的实际路径。此行将 Excel 文件读入内存，以便您可以对其进行操作。
## 步骤 3：指定 HTML 保存选项
现在，我们将创建一个实例`HtmlSaveOptions`，它允许您配置如何将 Excel 文件转换为 HTML。
```csharp
//指定 HTML 交叉类型
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
在此步骤中，我们设置了`HtmlCrossStringType`到`HtmlCrossType.Default`，这是处理输出 HTML 中的交叉引用可用的选项之一。
## 步骤 4：根据需要更改十字类型
您可以指定不同的类型`HtmlCrossStringType`根据您的要求。以下是您可以使用的各种选项：
- `HtmlCrossType.Default`：默认十字类型。
- `HtmlCrossType.MSExport`：以类似 MS Excel 的行为导出 HTML。
- `HtmlCrossType.Cross`：创建交叉引用。
- `HtmlCrossType.FitToCell`：使交叉引用适合单元格尺寸。
您可以修改`HtmlCrossStringType`像这样：
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
//或者
opts.HtmlCrossStringType = HtmlCrossType.Cross;
//或者
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## 步骤 5：保存输出 HTML 文件
配置完选项后，就可以保存转换后的 HTML 文件了。使用`Save`方法`Workbook`目的：
```csharp
//输出 HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
在这里，我们根据`HtmlCrossStringType`我们已经设置了。这样，您就可以轻松识别转换中使用的是哪种交叉类型。
## 步骤6：确认执行成功
最后，确认操作是否成功始终是一个好习惯。您可以将消息打印到控制台：
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
这将让您知道该过程已完成，没有任何错误。
## 结论
就这样！您已成功使用 Aspose.Cells 在 .NET 中为 Excel 导出指定 HTML 交叉类型。当您需要在 HTML 输出中保留特定格式或引用时，此功能特别有用，可确保转换后的文档满足您的要求。
## 常见问题解答
### Aspose.Cells 中的 HtmlCrossType 是什么？  
HtmlCrossType 定义在 HTML 转换过程中如何处理 Excel 文件中的交叉引用。您可以选择 Default、MSExport、Cross 和 FitToCell 等选项。
### 我可以免费使用 Aspose.Cells 吗？  
 Aspose.Cells 提供免费试用版。你可以从他们的[网站](https://releases.aspose.com/).
### 如何在我的.NET 项目中安装 Aspose.Cells？  
您可以通过运行以下命令在 Visual Studio 中通过 NuGet 包管理器安装 Aspose.Cells：`Install-Package Aspose.Cells`.
### 在哪里可以找到 Aspose.Cells 的文档？  
您可以找到有关 Aspose.Cells 的全面文档[这里](https://reference.aspose.com/cells/net/).
### 如果保存 HTML 文件时遇到错误，该怎么办？  
确保目录路径正确，并且您对输出目录具有写入权限。如果问题仍然存在，请查看 Aspose 支持论坛以获取帮助。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
