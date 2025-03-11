---
title: 在 Excel 中取消合并单元格
linktitle: 在 Excel 中取消合并单元格
second_title: Aspose.Cells .NET Excel 处理 API
description: 使用 Aspose.Cells for .NET 轻松取消 Excel 中合并的单元格。按照我们的分步指南创建更好的电子表格。
weight: 10
url: /zh/net/excel-merging-unmerging-cells/unmerge-merged-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中取消合并单元格

## 介绍

您是否厌倦了处理 Excel 电子表格中的合并单元格？您并不孤单！合并单元格可以成为格式化的便捷功能，但在数据操作和分析方面，它们往往会导致麻烦。但猜怎么着？取消合并这些讨厌的单元格比您想象的要容易 - 尤其是当您使用 Aspose.Cells for .NET 时。在本文中，我将逐步指导您如何取消合并单元格，确保您的数据整洁、整齐且随时可用！所以，戴上您的编码帽，让我们深入了解 Aspose.Cells 的世界。

## 先决条件

在我们开始之前，您需要准备好一些必需品：

### C# 和 .NET Framework 的基础知识
如果您熟悉 C# 编程并对 .NET 框架有基本的了解，那么您已经有一个良好的开端。如果没有，别担心！本教程设计得非常简单，因此您将在学习过程中掌握必要的概念。

### Aspose.Cells 库
确保已在 .NET 环境中安装 Aspose.Cells 库。您可以通过访问[Aspose.Cells 下载页面](https://releases.aspose.com/cells/net/).

### IDE 设置
您应该设置一个开发环境，例如 Visual Studio，您可以在其中编写和执行 C# 代码。

### 示例 Excel 文件
获取包含一些合并单元格的示例 Excel 文件 - 您将使用此文件来练习取消合并。

在满足所有这些先决条件之后，我们现在可以进入令人兴奋的部分 - 编写解决方案！

## 导入包

首先，让我们导入必要的包。使用 Aspose.Cells，您将与各种类进行交互，以有效地管理您的 Excel 文件。以下是您需要在 C# 文件顶部包含的内容：

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

通过包含此软件包，您将可以访问 Aspose.Cells 提供的所有功能。

让我们将拆分过程分解为易于管理的步骤。每个步骤都定义清晰，以便您轻松跟进。

## 步骤 1：定义目录

第一步是定义输入 Excel 文件（包含合并单元格的文件）和输出文件（未合并数据的保存文件）所在的目录。设置方法如下：

```csharp
//源目录
string sourceDir = "Your Document Directory"; 

//输出目录
string outputDir = "Your Document Directory"; 
```

确保更换`"Your Document Directory"`使用您的文件的实际路径。

## 步骤 2：创建工作簿

现在您已经设置了目录，是时候创建一个 Workbook 对象了。此对象将允许您操作 Excel 文件。您可以使用以下代码执行此操作：

```csharp
//创建工作簿
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

这行代码读取您的示例 Excel 文件并准备进行处理。 

## 步骤 3：访问工作表

每个工作簿都由工作表组成。您需要访问要取消合并单元格的特定工作表。操作方法如下：

```csharp
//创建一个工作表并获取第一张工作表
Worksheet worksheet = wbk.Worksheets[0];
```

此代码抓取第一个工作表。如果合并的单元格位于不同的工作表上，请相应地更新索引。

## 步骤 4：访问工作表中的单元格

接下来，您需要获取工作表中单元格的引用。可以使用以下方法完成此操作：

```csharp
//创建一个 Cells 对象来获取所有单元格
Cells cells = worksheet.Cells;
```

通过此行，您现在可以访问工作表上的所有单元格，并可以根据需要对其进行操作。

## 步骤 5：取消合并单元格

接下来是关键的一步——取消合并单元格！您需要指定要取消合并的合并单元格的范围。使用以下代码：

```csharp
//取消合并单元格
cells.UnMerge(5, 2, 2, 3);
```

在此示例中，`UnMerge`方法采用四个参数：起始行索引 (5)、起始列索引 (2)、要取消合并的行数 (2) 和要取消合并的列数 (3)。调整这些参数以匹配 Excel 文件中的特定合并单元格。

## 步骤 6：保存工作簿

取消合并后，您需要将更改保存到新的 Excel 文件中。操作方法如下：

```csharp
//保存文件
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

此行将未合并的数据保存在指定的输出目录中。就这么简单！

## 步骤 7：确认流程

最后，最好确认一切顺利。你可以向控制台打印一条消息，让你知道操作已成功执行：

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

就这样！您已成功使用 Aspose.Cells for .NET 取消合并 Excel 文件中的单元格。

## 结论

拆分单元格可能看起来很繁琐，尤其是在处理大型电子表格时，但使用 Aspose.Cells for .NET，这变得轻而易举！本教程将指导您完成从设置环境到执行有效拆分单元格所需的代码的所有步骤。Aspose.Cells 库提供的灵活性使您能够高效处理电子表格，使其成为使用 Excel 文件的开发人员的理想选择。因此，请深入研究并开始享受更干净、更易于管理的电子表格。

## 常见问题解答

### 什么是 Aspose.Cells？  
Aspose.Cells 是一个功能强大的库，用于在.NET 应用程序中创建、操作和转换 Excel 文档。

### 我需要许可证才能使用 Aspose.Cells 吗？  
 Aspose.Cells 提供免费试用，但需要许可证才能完全使用。您可以获得[此处为临时执照](https://purchase.aspose.com/temporary-license/).

### 我可以一次取消合并多张工作表中的单元格吗？  
是的，您可以循环遍历工作簿中的多个工作表并根据需要取消合并单元格。

### Aspose.Cells 与 .NET Core 兼容吗？  
是的，Aspose.Cells 与 .NET Core 兼容，使其适用于各种 .NET 应用程序。

### 在哪里可以找到有关 Aspose.Cells 的更多文档？  
您可以在[Aspose.Cells 参考页面](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
