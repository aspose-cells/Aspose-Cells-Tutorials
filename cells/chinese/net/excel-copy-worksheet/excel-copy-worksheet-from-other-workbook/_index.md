---
title: Excel 从其他工作簿复制工作表
linktitle: Excel 从其他工作簿复制工作表
second_title: Aspose.Cells for .NET API 参考
description: 通过本分步指南了解如何使用 Aspose.Cells for .NET 将工作表从一个 Excel 工作簿复制到另一个 Excel 工作簿。
weight: 10
url: /zh/net/excel-copy-worksheet/excel-copy-worksheet-from-other-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 从其他工作簿复制工作表

## 介绍

您是否曾为处理多个 Excel 工作簿而苦恼，试图让数据井然有序且易于访问？如果是这样，您并不孤单！我们中的许多人都在处理不同的文件，无论是工作还是个人项目。好消息是，借助 Aspose.Cells for .NET 的帮助，您可以让生活更轻松。这个功能强大的库允许您轻松操作 Excel 文件，包括将工作表从一个工作簿复制到另一个工作簿。在本指南中，我们将引导您完成这些步骤，确保您可以简化工作流程并提高工作效率。

## 先决条件

在开始编码之前，让我们先准备好所有需要的东西。别担心，这不是火箭科学！以下是您需要的东西：

1. Visual Studio（或任何 .NET IDE）：您应该在您的机器上设置一个 .NET 开发环境。
2.  Aspose.Cells for .NET：您需要下载并安装 Aspose.Cells。如果您还没有，您可以获取[这里](https://releases.aspose.com/cells/net/).
3. 对 C# 的基本了解：对 C# 编程有一点熟悉将使这一旅程更加顺利，但如果您刚刚开始，请不要有压力！
4. .NET Framework：确保您的项目针对的是 .NET Framework 的兼容版本。
5. 系统设置：确保您可以不受任何限制地运行和测试您的应用程序。

现在一切就绪，让我们开始编码吧！

## 导入包

在开始实现功能之前，我们需要导入必要的包。这样，您就可以访问 Aspose.Cells 提供的所有功能。以下是您的分步指南：

### 添加使用语句

打开 C# 文件并在顶部添加以下使用指令：

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

该包是 Aspose 库的核心，可让您访问其所有类和方法。

现在我们已经准备好一切，让我们进入激动人心的部分——实际将工作表从一个工作簿复制到另一个工作簿！我们将把它分解为几个明确的步骤。

## 步骤 1：设置文档目录

首先，我们需要指定 Excel 文件的存储位置。定义文档目录的路径：

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";  //将其更新为您的实际目录
```
这`dataDir`变量将存储您保存最终 Excel 文件的路径。确保将“您的文档目录”替换为系统上的实际路径。

## 步骤 2：创建新工作簿并用数据填充

接下来，让我们创建第一个工作簿并向其中添加一些示例数据。操作方法如下：

```csharp
//创建新工作簿
Workbook excelWorkbook0 = new Workbook();
//获取书中的第一个工作表
Worksheet ws0 = excelWorkbook0.Worksheets[0];

//将一些数据放入标题行 (A1:A4)
for (int i = 0; i < 5; i++)
{
    ws0.Cells[i, 0].PutValue(string.Format("Header Row {0}", i));
}

//输入一些详细数据（A5:A999）
for (int i = 5; i < 1000; i++)
{
    ws0.Cells[i, 0].PutValue(string.Format("Detail Row {0}", i));
}
```
在这里，我们创建第一个工作簿并填充第一个工作表（`ws0`) 带有标题和详细信息行。此模拟数据将帮助您稍后直观地了解复制过程。

## 步骤 3：设置打印页面设置

让我们配置页面设置以在打印时重复标题行，这样我们就可以看到该功能的实际效果：

```csharp
//根据第一个工作表定义一个 pagesetup 对象
PageSetup pagesetup = ws0.PageSetup;
//每页重复前五行
pagesetup.PrintTitleRows = "$1:$5";
```
这部分定义了如何打印文档。通过设置`PrintTitleRows`，我们确保前五行会出现在每一页打印的页面上，这对于可读性非常有用。

## 步骤 4：创建第二个工作簿

现在，我们需要创建另一个工作簿，我们将第一个工作表复制到其中：

```csharp
//创建另一个工作簿
Workbook excelWorkbook1 = new Workbook();
//获取书中的第一个工作表
Worksheet ws1 = excelWorkbook1.Worksheets[0];
//命名工作表
ws1.Name = "MySheet";
```
我们创建了一个新的工作簿（`excelWorkbook1`) 并将第一个工作表重命名为“MySheet”。为工作表赋予有意义的名称以方便以后访问始终是一个好主意。

## 步骤 5：复制工作表

我们将第一个工作簿的工作表中的内容复制到第二个工作簿：

```csharp
//将第一个工作簿的第一个工作表中的数据复制到
//第二个工作簿的第一个工作表
ws1.Copy(ws0);
```
这`Copy`方法从源工作表中获取所有内容（`ws0`）并将其复制到目标工作表（`ws1`）。很简单吧？

## 步骤 6：保存新工作簿

最后，让我们保存新创建的工作簿：

```csharp
//保存 Excel 文件
excelWorkbook1.Save(dataDir + "CopyWorksheetFromWorkbookToOther_out.xls");
```
此行将把您的第二个工作簿保存在指定路径。运行代码后，别忘了检查一切是否正常！

## 结论

就这样！您已经成功学会了如何使用 Aspose.Cells for .NET 将工作表从一个工作簿复制到另一个工作簿。这是一项非常实用的技能，尤其是在处理分布在不同文件中的大量数据时。只需几行代码，您就可以更方便地组织、管理和访问您的 Excel 数据。

## 常见问题解答

### 什么是 Aspose.Cells？  
Aspose.Cells 是一个.NET 库，允许开发人员创建、操作、转换和呈现各种格式的 Excel 文件。

### 我可以免费使用 Aspose.Cells 吗？  
是的，Aspose.Cells 提供免费试用，您可以访问[这里](https://releases.aspose.com/).

### 如何获得 Aspose.Cells 的临时许可证？  
您可以通过访问申请临时许可证[此链接](https://purchase.aspose.com/temporary-license/).

### 在哪里可以找到有关 Aspose.Cells 的更多文档？  
您可以找到详细的文档[这里](https://reference.aspose.com/cells/net/).

### 是否有任何支持可供 Aspose.Cells 用户使用？  
当然！您可以通过[Aspose 论坛](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
