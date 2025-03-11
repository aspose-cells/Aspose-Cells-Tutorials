---
title: 仅从 Excel 文件加载可见工作表
linktitle: 仅从 Excel 文件加载可见工作表
second_title: Aspose.Cells .NET Excel 处理 API
description: 在本分步指南中了解如何使用 Aspose.Cells for .NET 从 Excel 文件中仅加载可见工作表。
weight: 12
url: /zh/net/excel-file-handling/load-visible-sheets-only/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 仅从 Excel 文件加载可见工作表

## 介绍
当您在 .NET 应用程序中处理 Excel 文件时，管理多个工作表的挑战变得显而易见，尤其是当某些工作表隐藏或与您的操作无关时。Aspose.Cells for .NET 是一个功能强大的库，可帮助您高效地操作 Excel 文件。在本文中，我们将探讨如何仅从 Excel 文件中加载可见的工作表，过滤掉任何隐藏的数据。如果您曾经因浏览 Excel 数据而感到不知所措，那么本指南适合您！
## 先决条件
在深入学习本教程之前，请确保您已准备好学习本教程所需的一切：
1. C# 的基本理解：本教程专为熟悉 C# 编程语言的开发人员而设计。
2.  Aspose.Cells for .NET：您必须下载并设置 Aspose.Cells for .NET 库。您可以[点击此处下载库](https://releases.aspose.com/cells/net/).
3. Visual Studio 或任何 IDE：您应该有一个可以在其中编写和测试 C# 代码的 IDE。
4. .NET Framework：确保您已安装运行应用程序所需的 .NET Framework。
5. 示例 Excel 文件：为了练习，请创建示例 Excel 文件或按照提供的代码进行操作。
一切准备就绪？太棒了！让我们开始吧！
## 导入包
任何使用 Aspose.Cells 的 C# 项目的第一步都是导入所需的包。这使您能够访问库提供的所有功能。操作方法如下：
1. 打开您的项目：首先在 Visual Studio 或任何其他首选 IDE 中打开您的 C# 项目。
2. 添加引用：在解决方案资源管理器中右键单击您的项目，选择“添加”，然后选择“引用”。 
3. 浏览 Aspose.Cells：找到您之前下载的 Aspose.Cells.dll 文件并将其添加到您的项目引用中。
此步骤至关重要，因为它将 Aspose.Cells 功能链接到您的项目。 
```csharp
using System.IO;
using Aspose.Cells;
using System;
```

现在您已导入了必要的包，我们将创建一个示例 Excel 工作簿。在此工作簿中，我们将有多个工作表，其中一个工作表将在本教程中隐藏。
## 步骤 1：设置您的环境
首先，让我们设置环境并指定示例文件的路径。
```csharp
//文档目录的路径。
string dataDir = "Your Document Directory";
string sampleFile = "output.xlsx";
string samplePath = dataDir + sampleFile;
```
在此代码片段中，替换`"Your Document Directory"`与您想要保存工作簿的实际路径。 
## 步骤 2：创建工作簿
接下来，让我们创建工作簿并添加一些数据。
```csharp
//创建示例工作簿
Workbook createWorkbook = new Workbook();
createWorkbook.Worksheets["Sheet1"].Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets.Add("Sheet2").Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets.Add("Sheet3").Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets["Sheet3"].IsVisible = false; //使 Sheet3 隐藏
createWorkbook.Save(samplePath);
```
以下是具体情况：
- 我们正在创建一个新的工作簿并添加三张表。
- “Sheet1”和“Sheet2”将可见，而“Sheet3”将被隐藏。
- 然后我们将工作簿保存到指定的路径。
## 步骤 3：使用加载选项加载示例工作簿
现在我们有了一个包含可见和隐藏工作表的工作簿，是时候加载它了，同时确保我们只能访问可见工作表。
```csharp
LoadOptions loadOptions = new LoadOptions();
loadOptions.LoadFilter = new CustomLoad();
```
此代码片段设置了工作簿的加载选项，我们将对其进行自定义以过滤掉隐藏的工作表。
## 步骤 4：定义自定义加载过滤器
为了仅加载可见的工作表，我们需要创建自定义加载过滤器。定义方法如下：
```csharp
class CustomLoad : LoadFilter
{
    public override void StartSheet(Worksheet sheet)
    {
        if (sheet.IsVisible)
        {
            this.LoadDataFilterOptions = LoadDataFilterOptions.All;
        }
        else
        {
            this.LoadDataFilterOptions = LoadDataFilterOptions.Structure;
        }
    }
}
```
- 这`StartSheet`方法检查每张表是否可见。
- 如果可见，它会从该表加载所有数据。
- 如果不可见，它会跳过从该表加载任何数据。
## 步骤 5：使用加载选项加载工作簿
现在让我们加载工作簿并显示可见工作表中的数据。
```csharp
Workbook loadWorkbook = new Workbook(samplePath, loadOptions);
Console.WriteLine("Sheet1: A1: {0}", loadWorkbook.Worksheets["Sheet1"].Cells["A1"].Value);
Console.WriteLine("Sheet2: A1: {0}", loadWorkbook.Worksheets["Sheet2"].Cells["A1"].Value);
```
此代码片段利用`loadOptions`仅从可见工作表导入数据并显示“Sheet1”和“Sheet2”中单元格 A1 的内容。 
## 结论
就这样！您已经成功学会了如何使用 Aspose.Cells for .NET 从 Excel 文件中仅加载可见工作表。当您知道如何限制检索的数据并仅使用所需的数据时，管理 Excel 工作表将变得轻而易举。这不仅可以提高应用程序的效率，还可以使您的代码更简洁、更易于管理。 
## 常见问题解答
### 如果需要我可以加载隐藏的工作表吗？
是的，您可以简单地调整自定义加载过滤器中的条件以包含隐藏的工作表。
### Aspose.Cells 用于什么？
Aspose.Cells 用于操作 Excel 文件，无需安装 Microsoft Excel，提供读取、写入和管理 Excel 工作表等功能。
### Aspose.Cells 有试用版吗？
是的，你可以[下载免费试用版](https://releases.aspose.com/)来测试其功能。
### 在哪里可以找到 Aspose.Cells 的文档？
这[文档](https://reference.aspose.com/cells/net/)提供有关所有功能的全面信息。
### 如何购买 Aspose.Cells？
您可以轻松地[购买 Aspose.Cells](https://purchase.aspose.com/buy)从他们的购买页面。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
