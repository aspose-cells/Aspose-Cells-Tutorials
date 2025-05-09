---
"description": "了解如何使用 Aspose.Cells 在 .NET 中设置 PDF 创建时间。按照我们的分步指南，实现 Excel 到 PDF 的无缝转换。"
"linktitle": "在 .NET 中设置 PDF 创建时间"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 .NET 中设置 PDF 创建时间"
"url": "/zh/net/xps-and-pdf-operations/setting-pdf-creation-time/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中设置 PDF 创建时间

## 介绍
在当今的数字时代，将文档转换为不同格式的能力对于许多应用程序至关重要。一个常见的需求是将 Excel 电子表格转换为 PDF 文件。这不仅可以保留格式，还能使共享和打印更加便捷。如果您是使用 .NET 的开发人员，Aspose.Cells 是一个非常棒的库，可以简化此过程。在本教程中，我们将深入探讨如何使用 Aspose.Cells for .NET 将 Excel 文件转换为 PDF 时设置 PDF 创建时间。
## 先决条件
在我们深入研究代码细节之前，让我们确保您拥有开始所需的一切。
### 你需要什么
1. Visual Studio：确保您的计算机上已安装 Visual Studio。这将是您的开发环境。
2. Aspose.Cells for .NET：从下载 Aspose.Cells 库 [网站](https://releases.aspose.com/cells/net/)。您还可以先免费试用，以测试其功能。
3. C# 基础知识：熟悉 C# 编程将帮助您更好地理解代码片段。
4. Excel 文件：准备好要转换的 Excel 文件。在本例中，我们将使用名为 `Book1。xlsx`.
现在您已经满足了先决条件，让我们进入有趣的部分 - 导入必要的包并编写代码！
## 导入包
首先，您需要在 C# 文件中导入所需的命名空间。这至关重要，因为它允许您访问 Aspose.Cells 库提供的类和方法。
### 打开你的 C# 项目
打开 Visual Studio 并创建一个新项目或打开一个现有项目，在其中实现 PDF 转换功能。
### 添加 Aspose.Cells 引用
您可以通过在解决方案资源管理器中右键单击您的项目，选择“管理 NuGet 包”，然后搜索“Aspose.Cells”，将 Aspose.Cells 库添加到您的项目中。安装该包。
### 导入命名空间
在 C# 文件的顶部，包含以下命名空间：
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
这些命名空间将允许您访问 Workbook 类和其他基本功能。

现在我们已经导入了包，让我们在设置创建时间的同时分解将 Excel 文件转换为 PDF 的过程。
## 步骤1：定义文档目录
首先，您需要指定文档的存储目录。这是 Excel 文件所在的位置，也是输出 PDF 的保存位置。
```csharp
string dataDir = "Your Document Directory"; // 指定您的文档目录
```
代替 `"Your Document Directory"` 实际路径 `Book1.xlsx` 文件所在的位置。此路径将帮助应用程序找到要处理的文件。
## 步骤2：加载Excel文件
接下来，将 Excel 文件加载到 `Workbook` 对象。这就是 Aspose.Cells 的优势所在，因为它可以让您轻松处理 Excel 文件。
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Excel 文件的路径
Workbook workbook = new Workbook(inputPath); // 加载 Excel 文件
```
这 `Workbook` 类用于加载和操作 Excel 文件。通过传递输入路径，您可以告诉应用程序要处理哪个文件。
## 步骤 3：创建 PdfSaveOptions
现在，是时候创建一个实例了 `PdfSaveOptions`。此类允许您指定将工作簿保存为 PDF 的各种选项，包括创建时间。
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // 创建 PdfSaveOptions 实例
options.CreatedTime = DateTime.Now; // 将创建时间设置为现在
```
通过设置 `options.CreatedTime` 到 `DateTime.Now`，您要确保 PDF 将反映其创建的当前日期和时间。
## 步骤 4：将工作簿保存为 PDF
最后，您将使用刚刚定义的选项将工作簿保存为 PDF 文件。
```csharp
workbook.Save(dataDir + "output.pdf", options); // 另存为 PDF
```
这行代码获取工作簿并将其以 PDF 格式保存在指定位置。 `options` 传递参数以将创建时间包含在 PDF 元数据中。

## 结论
就这样！您已成功使用 Aspose.Cells for .NET 将 Excel 文件转换为 PDF，并附带创建时间戳。当您需要跟踪文档版本或希望向收件人提供文档创建时间信息时，此功能非常有用。
如果您想了解 Aspose.Cells 的更多功能，请随时查看 [文档](https://reference。aspose.com/cells/net/).
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个强大的 .NET 库，允许开发人员创建、操作和转换 Excel 文件。
### 我可以免费使用 Aspose.Cells 吗？
是的，你可以先免费试用一下 [Aspose 网站](https://releases。aspose.com/).
### 如何设置其他 PDF 属性？
您可以使用 `PdfSaveOptions` 类，例如页面大小、压缩等等。
### 是否可以一次转换多个 Excel 文件？
是的，您可以循环遍历文件列表并对每个文件应用相同的转换过程。
### 我可以在哪里获得 Aspose.Cells 的支持？
您可以从 Aspose 社区获得支持 [支持论坛](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}