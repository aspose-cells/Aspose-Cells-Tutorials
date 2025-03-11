---
title: 在 .NET 中以编程方式将 JSON 转换为 CSV
linktitle: 在 .NET 中以编程方式将 JSON 转换为 CSV
second_title: Aspose.Cells .NET Excel 处理 API
description: 了解如何使用 Aspose.Cells 在 .NET 中以编程方式将 JSON 转换为 CSV。按照我们的分步指南确保无缝数据转换。
weight: 15
url: /zh/net/converting-excel-files-to-other-formats/converting-json-to-csv/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以编程方式将 JSON 转换为 CSV

## 介绍
在当今的数字世界中，处理多种格式的数据已变得司空见惯，而 JSON（JavaScript 对象表示法）是数据交换中最广泛使用的格式之一。但是，当您需要将 JSON 转换为更易于分析的格式（如 CSV（逗号分隔值））时会发生什么？本教程将引导您完成使用 Aspose.Cells for .NET（一种易于使用且功能强大的电子表格操作 API）以编程方式将 JSON 转换为 CSV 的过程。 
## 先决条件
在深入研究代码之前，必须确保您拥有所有必要的组件并对我们将要使用的工具有基本的了解。让我们概述一下您需要什么：
-  Aspose.Cells for .NET：这是我们将用于将 JSON 转换为 CSV 的主要库。您可以[点击下载](https://releases.aspose.com/cells/net/).
- Visual Studio：您需要一个像 Visual Studio 这样的集成开发环境 (IDE) 来编写和执行 .NET 代码。
- .NET Framework：确保您已安装 .NET Framework。Aspose.Cells 与 .NET Core 和 .NET Framework 兼容。
- C# 基础知识：虽然本指南将分解代码的每个部分，但如果您对 C# 有一定熟悉，它将会有所帮助。
## 导入包
要在 .NET 项目中使用 Aspose.Cells，首先需要安装该库。您可以通过 NuGet 包管理器执行此操作：
1. 打开 Visual Studio。
2. 转到工具>NuGet 包管理器>管理解决方案的 NuGet 包。
3. 搜索 Aspose.Cells 并安装最新版本。
安装后，请确保在代码中包含以下命名空间：
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
现在一切都已设置好，让我们逐步分解代码，以便您了解使用 Aspose.Cells 将 JSON 文件转换为 CSV 是多么容易。
## 步骤 1：读取 JSON 文件
我们要做的第一件事是从文件中读取 JSON 数据。我们假设你已经有一个 JSON 文件（我们称之为`SampleJson.json`存储在系统目录中。
您可以使用`File.ReadAllText()`方法将 JSON 文件的内容读为字符串。
```csharp
//源目录
string sourceDir = "Your Document Directory";
//读取 JSON 文件
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

此步骤至关重要，因为您需要原始 JSON 数据来启动转换过程。通过将其读取为字符串，您可以准备由 Aspose.Cells 进行处理。
## 步骤 2：创建空工作簿
Aspose.Cells 主要在工作簿（Excel 文件）上运行。要开始导入 JSON 数据，首先需要创建一个空白工作簿来插入此数据。
```csharp
//创建空工作簿
Workbook workbook = new Workbook();
```
在这里，您将初始化一个空的工作簿，该工作簿最终将保存 CSV 格式的数据。可以将其视为在 Excel 中创建一个空白电子表格，该表格很快就会填充您的 JSON 数据。
## 步骤 3：访问工作簿中的单元格
现在我们有了一个空的工作簿，我们需要访问它的单元格。`Cells` Aspose.Cells 中的集合代表工作表中的所有单元格，您将在其中放置 JSON 数据。
```csharp
//获取单元格
Cells cells = workbook.Worksheets[0].Cells;
```
此代码片段选择第一个工作表（索引 0 处的工作表）并获取其`Cells`集合。这些单元格就像电子表格的网格，数据将添加到其中。
## 步骤 4：设置 JsonLayoutOptions
 Aspose.Cells 提供了多种自定义选项，用于导入 JSON 数据。在这里，我们定义`JsonLayoutOptions`指定 Aspose 如何处理数组、数字数据和对象标题。
```csharp
//设置 JsonLayoutOptions
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate：自动将字符串值转换为数字或日期值。
- ArrayAsTable：将 JSON 中的数组视为工作簿中的表。
- IgnoreArrayTitle 和 IgnoreObjectTitle：这些选项忽略数组和对象的标题，确保只导入原始数据。
## 步骤 5：导入 JSON 数据
设置布局选项后，就可以引入 JSON 数据了。`JsonUtility.ImportData()`方法在这里完成繁重的工作，将 JSON 数据插入到工作簿的单元格中。
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
此方法采用几个参数：
- `str`：我们在步骤1中读取的JSON字符串。
- `cells`：将放置数据的单元格集合。
- `0, 0`：这些是行和列索引，指示数据应该从哪里开始（即左上角）。
- `importOptions`：我们在步骤4中设置的布局选项。
## 步骤 6：将工作簿保存为 CSV
现在 JSON 数据已保存在工作簿中，我们可以轻松地将工作簿保存为 CSV 文件。CSV 是一种用于存储表格数据的简单、轻量级格式，非常适合数据分析。
```csharp
//输出目录
string outputDir = "Your Document Directory";
//保存工作簿
workbook.Save(outputDir + @"SampleJson_out.csv");
```
在此步骤中，我们将工作簿保存为 CSV 文件。您指定路径和文件名（`SampleJson_out.csv`) 将在其中保存 CSV。
## 步骤 7：确认流程
为了确保一切按预期工作，我们可以在控制台中打印一条确认消息。
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
简单的成功消息有助于确认过程顺利进行。
## 结论
使用 Aspose.Cells for .NET 将 JSON 转换为 CSV 是一个简单而强大的过程。只需几行代码，您就可以将复杂的 JSON 数据转换为更易于访问的 CSV 格式。无论您处理的是数组、对象还是数字数据，Aspose.Cells 都可以轻松配置转换过程以满足您的需求。
## 常见问题解答
### Aspose.Cells 可以处理大型 JSON 文件吗？
是的，Aspose.Cells 旨在高效处理大型数据集，使其适合处理大型 JSON 文件而不会出现性能问题。
### 如何自定义 CSV 输出？
您可以通过调整`JsonLayoutOptions`或者在将工作簿保存为 CSV 之前处理其格式。
### 有没有办法在转换过程中从 JSON 中排除某些数据？
是的，通过在导入之前调整 JSON 或使用自定义代码逻辑，您可以排除或过滤掉特定的数据字段。
### Aspose.Cells 除了支持 CSV 之外还支持其他文件格式吗？
当然！Aspose.Cells 支持多种格式，包括 Excel (XLS、XLSX)、PDF、HTML 等等。
### 我如何免费试用 Aspose.Cells？
你可以[点击此处下载免费试用版](https://releases.aspose.com/)购买前测试所有功能。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
