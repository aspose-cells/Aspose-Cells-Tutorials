---
"description": "了解如何使用 Aspose.Cells for .NET 以编程方式在 Excel 文件中指定文档属性（如版本、作者和标题），并提供分步说明。"
"linktitle": "在 .NET 中以编程方式指定 Excel 文件的文档版本"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 .NET 中以编程方式指定 Excel 文件的文档版本"
"url": "/zh/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以编程方式指定 Excel 文件的文档版本

## 介绍
Aspose.Cells for .NET 是一个功能强大的库，允许开发人员轻松地以编程方式操作 Excel 文件。无论您是想从头创建 Excel 文件还是修改现有文件，Aspose.Cells 都提供了全面的 API 来实现您的目标。其中一项功能是指定文档属性，例如版本、作者或标题。本教程将指导您如何使用 Aspose.Cells for .NET 以编程方式指定 Excel 文件的文档版本。
## 先决条件
在深入了解细节之前，请确保您已具备学习本教程所需的一切：
1. Aspose.Cells for .NET：您可以下载最新版本 [这里](https://releases.aspose.com/cells/net/)。如果您尚未购买许可证，您可以选择 [临时执照](https://purchase.aspose.com/temporary-license/) 探索其特点。
2. .NET 开发环境：您可以使用 Visual Studio 或任何与 .NET 兼容的 IDE。
3. C# 基础知识：了解 C# 编程将使后续工作更加轻松。
## 导入包
在开始编码之前，您需要从 Aspose.Cells 库导入必要的命名空间。这将使您能够访问操作 Excel 文件所需的类和方法。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
这两个命名空间对于与工作簿及其内置文档属性进行交互至关重要。
现在，让我们分解在 Excel 文件中指定文档属性的过程，包括版本、标题和作者。
## 步骤 1：初始化工作簿对象
第一步是创建一个新的实例 `Workbook` 对象。此对象代表您将要处理的整个 Excel 文件。
```csharp
Workbook wb = new Workbook();
```
这 `Workbook` 类提供了 Excel 文件的表示。通过实例化它，我们创建一个可以操作的空白 Excel 工作簿。
## 步骤 2：访问内置文档属性
Aspose.Cells 提供内置文档属性，包括标题、作者和文档版本等字段。您可以通过 `BuiltInDocumentProperties` 收藏。
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
这 `BuiltInDocumentPropertyCollection` 类提供对内置文档属性集合的访问，例如标题、作者以及通常与文档相关的其他元数据。
## 步骤3：设置Excel文档的标题
接下来，我们将设置 Excel 文档的标题。此元数据有助于稍后识别和管理文件。
```csharp
bdpc.Title = "Aspose File Format APIs";
```
设置标题对于文档组织至关重要。这些元数据可以在文件属性中查看，并可供外部系统使用，以便更有效地对文档进行分类或识别。
## 步骤 4：指定作者
还可以指定文档的作者来反映谁创建或修改了该文件。
```csharp
bdpc.Author = "Aspose APIs Developers";
```
此步骤有助于将文档归属于其创建者，为文档管理或协作场景提供额外的元数据。
## 步骤 5：指定文档版本
本教程中我们要讨论的最关键属性之一是文档版本。此步骤允许您指定文档的版本，这在需要版本控制的环境中非常有用。
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
设置文档版本可以清楚地了解创建该文件时使用了哪个版本的文档或库。这在需要跟踪文件修订或与不同库版本兼容性的环境中尤为重要。
## 步骤6：保存Excel文件
最后，您可以保存包含所有刚刚设置属性的 Excel 文件。Aspose.Cells 允许您以多种格式保存文件，但在本例中，我们将使用 `.xlsx` 格式。
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
这 `Save` 方法用于将文件保存到您指定的目录。在这里，我们将其保存为 Excel 文件，保存在 `.xlsx` 格式。如果需要，Aspose.Cells 还支持以下格式 `.xls`， `.csv`， 和 `.pdf`，根据您的项目需求提供灵活性。
## 结论
在本教程中，我们介绍了如何使用 Aspose.Cells for .NET 在 Excel 文件中指定文档属性，尤其是文档版本。Aspose.Cells 是一款极其灵活且功能强大的工具，可让您以编程方式操作 Excel 文件，这对于任何使用电子表格的 .NET 开发人员来说都是一笔宝贵的财富。
## 常见问题解答
### 我可以使用 Aspose.Cells 修改其他内置属性吗？  
是的，您可以修改其他内置属性，例如主题、关键字和评论等。
### Aspose.Cells 支持哪些文件格式？  
Aspose.Cells 支持多种格式，包括 `.xls`， `.xlsx`， `.csv`， `.pdf`等等。
### 我需要许可证才能使用 Aspose.Cells for .NET 吗？  
您可以使用 [免费试用](https://releases.aspose.com/) 或申请 [临时执照](https://purchase.aspose.com/temporary-license/) 进行扩展测试。
### 我可以在 Web 应用程序中使用 Aspose.Cells 吗？  
是的，Aspose.Cells 既可用于桌面应用程序，也可用于 Web 应用程序。它功能强大，并且能够与 .NET Web 框架完美集成。
### 我可以在哪里获得 Aspose.Cells 的支持？  
您可以通过以下方式访问社区和支持 [Aspose.Cells 支持论坛](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}