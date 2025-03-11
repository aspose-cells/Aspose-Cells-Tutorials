---
title: 将 OLE 对象插入 Excel
linktitle: 将 OLE 对象插入 Excel
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过本指南中的分步说明，了解如何使用 Aspose.Cells for .NET 将 OLE 对象插入 Excel 文件。
weight: 11
url: /zh/net/excel-ole-picture-objects/insert-ole-object-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 OLE 对象插入 Excel

## 介绍
无论您嵌入的是图像、图表还是任何其他文件，使用 Aspose.Cells for .NET 都是一种简单的方法来实现这一点。在本指南中，我们将探讨将 OLE 对象插入 Excel 工作表所需的步骤。最后，您将能够使用个性化嵌入来增强您的 Excel 工作簿，从而打动您的受众或满足各种专业需求。 
## 先决条件
在深入研究代码细节之前，你需要准备一些东西：
1. Visual Studio：理想情况下，您应该在支持 .NET 的环境中工作，例如 Visual Studio。此 IDE 可让您轻松编写、测试和调试应用程序。
2. Aspose.Cells 库：您必须安装 Aspose.Cells 库。您可以通过 NuGet 包管理器获取它，也可以直接从[Aspose 网站](https://releases.aspose.com/cells/net/).
3. 示例文件：出于演示目的，请确保您有一个图像（如`logo.jpg`和 Excel 文件 (`book1.xls`) 来使用。这些将在代码中引用。
4. 对 C# 的基本了解：熟悉 C# 将帮助您理解所涉及的步骤并在必要时进行修改。
一旦一切就绪，就可以开始将 OLE 对象插入 Excel 了！
## 导入包
要使用 Aspose.Cells 操作 Excel 文件，首先需要导入所需的包。在 C# 文件的顶部添加以下命名空间：
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
通过此基本设置，您可以与工作簿、工作表以及任务所需的其他基本组件进行交互。
让我们将其分解为易于理解的步骤。
## 步骤 1：设置文档目录
第一步是确定文档的存储位置。这很简单。
```csharp
//文档目录的路径。
string dataDir = "Your Document Directory";
```
确保更换`"Your Document Directory"`使用您计划保存文件的系统上的实际目录路径。
## 步骤 2：如果目录不存在则创建目录
接下来，我们要确保这个目录存在。如果不存在，我们需要创建它。
```csharp
//如果目录尚不存在，则创建目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
这个简单的检查可以防止你的程序在以后抛出不必要的错误。
## 步骤 3：实例化新工作簿
现在，让我们创建一个新的工作簿，我们将在其中使用 OLE 对象。
```csharp
//实例化一个新的工作簿。
Workbook workbook = new Workbook();
```
这个新的工作簿将作为您计划插入的 OLE 对象的画布。
## 步骤 4：获取第一个工作表
有了工作簿后，我们需要获取第一个工作表。通常，这是您最活跃的工作地点。
```csharp
//获取第一张工作表。
Worksheet sheet = workbook.Worksheets[0];
```
简单又漂亮！我们已准备好开始向此工作表添加内容。
## 步骤 5：定义图像的路径
现在，让我们为想要嵌入到 Excel 文件中的图像设置一个路径。
```csharp
//定义一个字符串变量来存储图像路径。
string ImageUrl = dataDir + "logo.jpg";
```
确保此路径正确反映您的`logo.jpg`文件已存储。
## 步骤 6：将图像加载到字节数组中
我们需要将图像读成我们可以处理的格式。为此，我们打开文件流并将其数据读入字节数组。
```csharp
//将图片放入流中。
FileStream fs = File.OpenRead(ImageUrl);
//定义一个字节数组。
byte[] imageData = new Byte[fs.Length];
//从流中获取图片放入字节数组中。
fs.Read(imageData, 0, imageData.Length);
//关闭流。
fs.Close();
```
通过将图像读入字节数组，我们准备将其插入到 Excel 工作表中。
## 步骤 7：获取 Excel 文件路径
现在，让我们定义您的 Excel 文件位于何处。
```csharp
//获取变量中的 Excel 文件路径。
string path = dataDir + "book1.xls";
```
再次确保该路径正确且指向正确的文件。
## 步骤 8：将 Excel 文件加载到字节数组中
就像我们对图像所做的那样，我们需要将 Excel 文件本身加载到字节数组中。
```csharp
//将文件放入流中。
fs = File.OpenRead(path);
//定义一个字节数组。
byte[] objectData = new Byte[fs.Length];
//从流中存储文件。
fs.Read(objectData, 0, objectData.Length);
//关闭流。
fs.Close();
```
这为我们的 OLE 对象嵌入准备了 Excel 文件。
## 步骤 9：将 OLE 对象添加到工作表
数据准备好后，我们现在可以将 OLE 对象插入工作表。
```csharp
//将一个 OLE 对象与图像一起添加到工作表中。
sheet.OleObjects.Add(14, 3, 200, 220, imageData);
//设置嵌入的 OLE 对象数据。
sheet.OleObjects[0].ObjectData = objectData;
```
此行在 Excel 文档中创建一个嵌入对象。参数`(14, 3, 200, 220)`指定嵌入对象的位置和大小。根据您的具体用例调整这些值。
## 步骤 10：保存 Excel 文件
最后，是时候将您的更改保存到 Excel 文件了。
```csharp
//保存 Excel 文件
workbook.Save(dataDir + "output.out.xls");
```
此行保存插入了 OLE 对象的工作簿。请务必使用有意义的名称！
## 结论
使用 Aspose.Cells for .NET 将 OLE 对象插入 Excel 文件不仅有益，而且一旦将其分解为可管理的步骤，就会变得非常简单。这个强大的工具可让您增强 Excel 文档，使其具有交互性和视觉吸引力。无论您是希望自动化报告的开发人员，还是热衷于有效呈现数据的分析师，掌握 OLE 嵌入都是您工具包中的关键资产。
## 常见问题解答
### 什么是 OLE 对象？
OLE 对象是可以嵌入文档的文件，允许不同的应用程序相互集成。示例包括图像、Word 文档和演示文稿。
### 我可以免费使用 Aspose.Cells 吗？
您可以免费下载试用版，试用 Aspose.Cells 的版本[网站](https://releases.aspose.com/).
### 我可以与 OLE 对象一起使用哪些文件格式？
根据您的应用程序，您可以使用各种格式，包括图像（JPEG、PNG）、Word 文档、PDF 等。
### Aspose.Cells 是否支持所有平台？
Aspose.Cells for .NET 主要针对 .NET 平台而设计。但是，其功能在不同的 Windows、Mac 或云环境中可能会有所不同。
### 如果我遇到问题，如何获得帮助？
您可以通过以下方式获得支持[Aspose 论坛](https://forum.aspose.com/c/cells/9)开发人员分享见解和解决方案的地方。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
