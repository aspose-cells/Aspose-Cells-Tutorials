---
title: 以 2007 xlsb 格式保存 Excel 文件
linktitle: 以 2007 xlsb 格式保存 Excel 文件
second_title: Aspose.Cells .NET Excel 处理 API
description: 了解如何使用 Aspose.Cells for .NET 将 Excel 文件保存为 xlsb 格式！带有实际示例的分步指南等着您。
weight: 11
url: /zh/net/saving-files-in-different-formats/save-excel-file-in-2007-xlsb-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 以 2007 xlsb 格式保存 Excel 文件

## 介绍
在 .NET 中处理 Excel 文件时，有很多灵活性和功能可用，尤其是 Aspose.Cells 库。这个强大的工具允许您轻松创建、修改和保存 Excel 文件。今天，我们将探讨如何以 2007 xlsb 格式保存 Excel 文件。如果您一直在寻找一种以编程方式处理 Excel 文件而又没有典型开销的方法，那么您来对地方了！ 
## 先决条件
在我们开始之前，让我们确保您拥有无缝跟进所需的一切。您应该拥有以下内容：
1. Visual Studio：确保您的计算机上安装了 Visual Studio 版本。您将在这里编写 .NET 代码。 
2.  Aspose.Cells 库：您需要 Aspose.Cells for .NET 库。如果您尚未下载，请前往[Aspose 下载页面](https://releases.aspose.com/cells/net/)去抓住它。 
3. C# 基础知识：对 C# 和 .NET 的基础了解将帮助您更轻松地浏览代码示例。
4. .NET Framework：确保您的项目设置了 Aspose.Cells 库支持的适当 .NET 框架。
5. Excel 文档：虽然创建新工作簿是一种选择，但是如果您想操作现有文件，拥有一个起始文档可能会很有用。
## 导入包
要开始在项目中使用 Aspose.Cells 库，您需要导入必要的命名空间。这类似于在开始项目之前解压工具箱。
### 设置你的项目
1. 打开 Visual Studio：通过选择“创建新项目”开始一个新项目。 
2. 选择项目模板：根据您的喜好选择控制台应用程序或 Windows 窗体应用程序。
3. 添加 Aspose.Cells 引用：在项目资源管理器中右键单击“引用”，然后单击“添加引用”。浏览到您下载的 Aspose.Cells.dll 文件。
### 导入命名空间
添加引用后，下一步就是将命名空间包含在 C# 文件的顶部。
```csharp
using System.IO;
using Aspose.Cells;
```
这行代码允许您无限制访问 Aspose.Cells 库提供的所有类和方法。

现在，让我们分解一下以 2007 xlsb 格式保存 Excel 文件的步骤。
## 步骤 1：设置保存目录
首先，我们需要确定 Excel 文件的保存位置。

```csharp
//文档目录的路径
string dataDir = "Your Document Directory\\";
```
此行定义了文档目录的路径。请确保替换`"Your Document Directory"`使用系统中您想要保存文件的实际路径。
## 步骤 2：创建工作簿对象
接下来，我们将使用 Aspose.Cells 库创建一个新的工作簿。

```csharp
Workbook workbook = new Workbook();
```
在这里，我们创建一个新的实例`Workbook`类。这个新创建的工作簿是一个空白工作簿，您可以根据需要开始在其中填充数据。
## 步骤 3：保存工作簿
现在到了最有趣的部分——以所需的格式保存您的工作簿！
```csharp
//保存为Excel2007 xlsb格式
workbook.Save(dataDir + "output.xlsb", SaveFormat.Xlsb);
```
这行代码将您的工作簿保存为`output.xlsb`在指定目录中使用`SaveFormat.Xlsb`格式。`SaveFormat`枚举功能非常强大，它允许您指定各种格式，例如`Xlsx`, `Xls`， ETC。
## 结论
就这样，您已经成功学会了如何使用 Aspose.Cells for .NET 将 Excel 文件保存为 2007 xlsb 格式。对于需要在 .NET 应用程序中自动处理 Excel 文件的开发人员来说，这个简单而有效的功能可以带来翻天覆地的变化。

## 常见问题解答
### 什么是 Aspose.Cells 库？
Aspose.Cells 是一个功能强大的.NET 库，使开发人员能够以编程方式创建、修改和操作 Excel 文件，而无需安装 Microsoft Excel。
### 我可以免费试用 Aspose.Cells 吗？
当然可以！您可以使用[免费试用](https://releases.aspose.com/)探索图书馆的功能。
### xls 和 xlsb 格式有什么区别？
xls 格式较旧且基于二进制文件结构，而 xlsb 是一种较新的格式，它也使用二进制存储，但允许更大的文件大小和更快的处理速度。
### 我可以在哪里购买 Aspose.Cells 的许可证？
您可以直接从[Aspose 购买页面](https://purchase.aspose.com/buy).
### 我如何寻求对 Aspose.Cells 问题的支持？
如果您遇到任何问题或有疑问，请随时访问[支持论坛](https://forum.aspose.com/c/cells/9)
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
