---
title: 拆分工作表窗格
linktitle: 拆分工作表窗格
second_title: Aspose.Cells for .NET API 参考
description: 通过我们的分步指南学习如何在 Aspose.Cells for .NET 中拆分工作表窗格。通过本简单教程改进 Excel 文件导航。
weight: 130
url: /zh/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 拆分工作表窗格

## 介绍

您准备好使用 Aspose.Cells for .NET 拆分 Excel 工作表的窗格了吗？想象一下：您有一个巨大的 Excel 工作表，并且您厌倦了不断滚动回标题只是为了记住您正在处理的列。输入“拆分窗格”。此便捷功能允许您冻结工作表的一部分，使其更易于导航。无论您处理的是财务数据、库存管理还是海量数据集，拆分窗格都可以将您的工作效率提高十倍。 

## 先决条件

在我们开始像电子表格向导一样拆分窗格之前，让我们先正确设置。以下是您需要的内容：

-  Aspose.Cells for .NET：请确保您已下载并安装。如果尚未安装，请立即获取[这里](https://releases.aspose.com/cells/net/).
- .NET Framework：本指南假设您在 .NET 环境中工作。
- Excel 工作簿：我们将使用示例 Excel 文件来展示此功能的工作原理。
- 临时或完整许可证：Aspose.Cells 需要许可证。如果您只是尝试一下，请获取[免费临时执照](https://purchase.aspose.com/temporary-license/)以避免评估限制。

## 导入包

在深入研究代码之前，我们先导入必要的命名空间。如果不包含这些，您实际上无法在 Aspose.Cells 中执行任何操作。

```csharp
using System.IO;
using Aspose.Cells;
```

现在我们已经了解了基本知识，让我们进入令人兴奋的部分 - 拆分窗格！

## 步骤 1：实例化工作簿

这个过程的第一步是创建一个`Workbook`对象，它将代表您要修改的 Excel 文件。在本例中，我们将从目录中加载一个文件。这是您的画布，是您将在其上施展魔法的 Excel 工作表。

在拆分窗格之前，我们需要一个工作簿！这一步就像在开始阅读之前打开一本书一样重要。

```csharp
//文档目录的路径
string dataDir = "YOUR DOCUMENT DIRECTORY";

//实例化新的工作簿并打开模板文件
Workbook book = new Workbook(dataDir + "Book1.xls");
```

在上面的代码中，替换`"YOUR DOCUMENT DIRECTORY"`替换为 Excel 文件所在的实际路径。`Workbook`类将 Excel 文件加载到内存中。

## 步骤 2：设置活动单元格

加载工作簿后，就该设置活动单元格了。在 Excel 术语中，活动单元格是当前选定或处于焦点的单元格。在本教程中，我们将选择单元格`A20`在第一个工作表中。

设置活动单元格至关重要，因为窗格拆分从此活动单元格开始。这就像选择在披萨上切第一刀的位置一样——选择你的那一块！

```csharp
//设置活动单元格
book.Worksheets[0].ActiveCell = "A20";
```

这段代码使`A20`活动单元格。这一点很重要，因为拆分围绕此点进行，就像 Excel 中的导航通常围绕特定单元格一样。

## 步骤 3：拆分工作表

现在已设置了活动单元格，让我们进入有趣的部分 — 拆分工作表！这一步是神奇的事情发生的地方。您将能够将工作表分成多个窗格，以便于查看和导航。

这是整个教程的核心。通过拆分工作表，您可以创建单独的窗格，以便滚动浏览 Excel 工作表的不同部分，而不会忽略标题或其他重要区域。

```csharp
//拆分工作表窗口
book.Worksheets[0].Split();
```

随着`Split()`方法，你告诉 Aspose.Cells 在活动单元格处拆分工作表（`A20`在这种情况下）。从此时起，Excel 会在工作表中创建一个分区，将各个窗格分开，以便您独立导航。

## 步骤 4：保存工作簿

拆分窗格后，剩下的就是保存您的工作。这最后一步将确保您的更改保存在指定的输出文件中。

如果不保存，您所有的努力成果还有什么用呢？保存可确保您精美的玻璃窗完好无损，以供将来使用。

```csharp
//保存 Excel 文件
book.Save(dataDir + "output.xls");
```

在这里，`Save()`方法将包含新拆分窗格的工作簿保存到输出 Excel 文件中。您所做的更改现在可供您（或任何其他人）使用。

## 结论

就这样！您刚刚学会了如何使用 Aspose.Cells for .NET 在 Excel 工作表中拆分窗格。不再需要无休止地滚动或丢失数据。此方法使处理大型 Excel 文件变得轻松很多，而且效率更高。有了拆分窗格的功能，您现在可以在处理复杂电子表格的同时跟踪关键数据点。

## 常见问题解答

### 我可以拆分两个以上的窗格吗？  
是的，您可以通过指定不同的活动单元格并调用`Split()`方法。

### 拆分窗格和冻结窗格有什么区别？  
拆分窗格可让您独立滚动两个窗格。冻结窗格可锁定标题或特定行/列，以便滚动时它们保持可见。

### 应用后我可以消除裂缝吗？  
是的，您可以通过关闭并重新打开工作簿或以编程方式重置它来消除拆分。

### 对于不同的 Excel 文件格式（XLS、XLSX），拆分窗格的工作方式是否相同？  
是的，`Split()`方法适用于 XLS 和 XLSX 格式。

### 我可以在没有许可证的情况下使用 Aspose.Cells 吗？  
是的，但有限制。为了获得完整的体验，最好使用[暂时的](https://purchase.aspose.com/temporary-license/)或者[付费许可](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
