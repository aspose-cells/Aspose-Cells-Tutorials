---
title: 以 HTML 格式导出文档工作簿和工作表属性
linktitle: 以 HTML 格式导出文档工作簿和工作表属性
second_title: Aspose.Cells .NET Excel 处理 API
description: 了解如何使用 Aspose.Cells for .NET 将 Excel 文档、工作簿和工作表属性导出为 HTML。包含简单的分步指南。
weight: 11
url: /zh/net/exporting-excel-to-html-with-advanced-options/exporting-document-workbook-and-worksheet-properties/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 以 HTML 格式导出文档工作簿和工作表属性

## 介绍

在处理电子表格时，我们经常需要将 Excel 文件转换为不同的格式以便共享、保存或演示。一项常见任务是将工作簿和工作表属性导出为 HTML 格式。在本文中，我们将引导您了解如何使用 Aspose.Cells for .NET 完成此操作。如果您不熟悉编码或 Aspose 库，请不要担心；我们将逐步分解，让您轻松理解！

## 先决条件

在深入研究代码之前，让我们确保您拥有开始所需的一切：

1. .NET Framework：确保您的开发环境已安装 .NET Framework。Aspose.Cells 与 .NET Framework 4.8 及以上版本兼容。
   
2.  Aspose.Cells for .NET：您需要安装 Aspose.Cells。您可以从[下载页面](https://releases.aspose.com/cells/net/). 

3. IDE：像 Visual Studio 这样的合适的集成开发环境 (IDE) 将简化您的编码体验。

4. 示例 Excel 文件：出于测试目的，请确保您有一个名为`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx`在你的工作目录中。

## 导入包

现在我们已经了解了先决条件，让我们首先在 C# 项目中导入必要的包。具体操作如下：

### 创建新项目

- 打开 IDE 并创建一个新的 C# 项目。您可以选择一个控制台应用程序，它非常适合运行此类任务。

### 添加 Aspose.Cells NuGet 包

要添加 Aspose.Cells 包，请按照以下步骤操作：

- 在解决方案资源管理器中右键单击您的项目并选择“管理 NuGet 包”。
- 在 NuGet 包管理器中，搜索“Aspose.Cells”并安装它。
- 该包将提供处理 Excel 文件所需的类和方法。

### 导入命名空间

在主程序文件的顶部，确保包含以下命名空间：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

这将使我们能够访问`Workbook`和`HtmlSaveOptions`类，我们将在示例中使用这些类。

现在您已完成所有设置，让我们将整个过程分解为简单的步骤。

## 步骤 1：设置文件目录

首先，我们需要指定输入和输出文件的位置。在代码中，像这样初始化目录：

```csharp
//源目录
string sourceDir = "Your Document Directory/";  //使用您的实际路径进行更新

//输出目录
string outputDir = "Your Document Directory/";  //使用您的实际路径进行更新
```

- 源目录：这是您的输入 Excel 文件（`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx`) 被存储。
- 输出目录：这是您希望保存输出 HTML 文件的路径。

## 第 2 步：加载 Excel 文件

现在我们需要使用`Workbook`班级：

```csharp
//加载示例 Excel 文件
Workbook workbook = new Workbook(sourceDir + "sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx");
```

- 工作簿实例：`Workbook`构造函数将文件路径带到您的 Excel 文件并创建一个您可以操作的新实例。

## 步骤 3：设置 HTML 保存选项

接下来，我们指定如何将 Excel 数据保存为 HTML：

```csharp
//指定 Html 保存选项
HtmlSaveOptions options = new HtmlSaveOptions();

//防止导出文档、工作簿和工作表属性
options.ExportDocumentProperties = false;
options.ExportWorkbookProperties = false;
options.ExportWorksheetProperties = false;
```

- HtmlSaveOptions：此类帮助管理如何将 Excel 文件转换为 HTML。
- 我们设置了几个选项来`false`因为我们不想在 HTML 输出中包含工作簿和工作表属性。

## 步骤 4：将所有内容导出为 HTML

现在我们准备将工作簿保存为 HTML 格式：

```csharp
//使用 Html 保存选项将 Excel 文件导出为 Html
workbook.Save(outputDir + "outputExportDocumentWorkbookAndWorksheetPropertiesInHTML.html", options);
```

- 这`Save`方法采用两个参数：输出 HTML 文件的文件路径和我们设置的选项。运行此方法将在指定的输出目录中创建您的 HTML 文件。

## 步骤 5：控制台反馈

最后，让我们在控制台中提供一些反馈以了解该过程已成功完成：

```csharp
Console.WriteLine("ExportDocumentWorkbookAndWorksheetPropertiesInHTML executed successfully.");
```

## 结论

就这样，您已成功使用 Aspose.Cells for .NET 将工作簿和工作表属性导出到 HTML！您遵循了一个简单的过程，从设置环境到导出 Excel 数据。使用 Aspose.Cells 等库的好处在于它简化了复杂的任务，使开发人员的工作更轻松。现在，您可以使用 HTML 更广泛地共享您的电子表格，就像让全世界窥视您的工作簿而无需向他们提供整本书一样。

## 常见问题解答

### 如何安装 Aspose.Cells for .NET？  
您可以通过 NuGet 包管理器在 Visual Studio 项目中通过 NuGet 安装 Aspose.Cells 库。

### 我可以自定义 HTML 输出吗？  
是的，Aspose.Cells 提供了多种选择`HtmlSaveOptions`自定义 Excel 文件转换为 HTML 的方式。

### 有没有办法在 HTML 导出中包含文档属性？  
您可以设置`ExportDocumentProperties`, `ExportWorkbookProperties` ， 和`ExportWorksheetProperties`到`true`在`HtmlSaveOptions`如果你想包括它们的话。

### 除了 HTML 之外，我还可以将 Excel 文件导出为哪些格式？  
Aspose.Cells 支持各种格式，包括 PDF、CSV、XML 等。

### 有试用版吗？  
是的，您可以从以下网站获取 Aspose.Cells 的免费试用版[网站](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
