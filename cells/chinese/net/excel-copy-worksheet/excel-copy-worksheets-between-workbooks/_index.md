---
title: Excel 在工作簿之间复制工作表
linktitle: Excel 在工作簿之间复制工作表
second_title: Aspose.Cells for .NET API 参考
description: 了解如何使用 Aspose.Cells for .NET 在 Excel 工作簿之间复制工作表。带有代码示例的分步指南可简化您的电子表格管理。
weight: 30
url: /zh/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 在工作簿之间复制工作表

## 介绍

您是否曾经手动在 Excel 工作簿之间复制工作表？这有点像在骑独轮车时玩杂耍！但使用 Aspose.Cells for .NET，您可以简化此任务并使其像切黄油一样顺畅。无论您是管理大型数据集还是需要整合信息，在工作簿之间复制工作表都可以节省大量时间。在本教程中，我们将向您展示如何使用 Aspose.Cells for .NET 执行此操作。在本指南结束时，您将轻松完成 Excel 任务。

## 先决条件

在深入研究代码之前，让我们确保您已配备正确的工具来开始操作：

-  Aspose.Cells for .NET：您可以下载[这里](https://releases.aspose.com/cells/net/).
- Visual Studio 或任何支持.NET 框架的 IDE。
- 有效的执照或[临时执照](https://purchase.aspose.com/temporary-license/)如果您想测试 Aspose.Cells 的全部功能。
- 对 C# 和 .NET 框架有基本的了解。

您还可以查看[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)了解更多详情。

## 导入包

在开始编码之前，您需要导入必要的软件包。这就像旅行前打包行李一样——您需要合适的工具才能让旅途顺利。

```csharp
using Aspose.Cells;
```

这行简单的代码导入了 Aspose.Cells 库，它是我们即将使用的所有 Excel 魔法的门户。


现在您已完成所有设置，让我们来看看在 Excel 工作簿之间复制工作表的过程。每个步骤都分解为易于理解的步骤。因此，即使您是 Aspose.Cells 的新手，您也能够跟上进度。

## 步骤 1：设置文档目录

首先，您需要定义文件的位置。将此步骤视为为寻宝选择地图 - 它告诉代码在哪里找到并存储您的工作簿。

```csharp
//文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

在这一行中，替换`"YOUR DOCUMENT DIRECTORY"`替换为 Excel 文件的实际路径。这是加载和保存工作簿的位置。

## 第 2 步：打开第一个工作簿

接下来，您将打开第一个工作簿，其中包含要复制的工作表。想象一下打开文件夹拿一张纸。

```csharp
string InputPath = dataDir + "book1.xls";
//创建工作簿。
//打开一个文件进入第一本书。
Workbook excelWorkbook0 = new Workbook(InputPath);
```

您正在加载`book1.xls`（确保文件存在于您的目录中）放入新的`Workbook`对象被调用`excelWorkbook0`。这是包含您要复制的工作表的源工作簿。

## 步骤 3：创建第二个工作簿

现在您已经打开了第一个工作簿，是时候创建另一个空白工作簿，将复制的工作表粘贴到其中。您可以将其视为打开一个新的空白笔记本，将数据传输到其中。

```csharp
//创建另一个工作簿。
Workbook excelWorkbook1 = new Workbook();
```

这行代码创建一个名为`excelWorkbook1`。这是将工作表从第一个工作簿移出后，复制的工作表将存放在此处。

## 步骤 4：复制工作表

魔法来了！在这一步中，您实际上会将工作表从第一个工作簿复制到第二个工作簿中。这就像将笔记从一个笔记本转移到另一个笔记本一样。

```csharp
//把第一本书的第一页抄到第二本书里。
excelWorkbook1.Worksheets[0].Copy(excelWorkbook0.Worksheets[0]);
```

这里发生了什么？代码从`excelWorkbook0`并将其复制到第一张纸上`excelWorkbook1`。超级简单，对吧？

## 步骤 5：保存新工作簿

最后，您将保存包含复制的工作表的第二本工作簿。这就像将您新写的笔记保存在计算机上的新文件夹中一样。

```csharp
//保存文件。
excelWorkbook1.Save(dataDir + "CopyWorksheetsBetweenWorkbooks_out.xls");
```

这会将包含复制工作表的第二个工作簿保存到名为`CopyWorksheetsBetweenWorkbooks_out.xls`。请随意将名称更改为您喜欢的任何名称！

## 结论

就这样！您已成功使用 Aspose.Cells for .NET 将工作表从一个 Excel 工作簿复制到另一个工作簿。这是一个简单的过程，可让您免于手动复制粘贴，尤其是在处理复杂或大型电子表格时。Aspose.Cells for .NET 是一个功能强大的工具，可让您轻松操作 Excel 文件，无论您是复制工作表、合并工作簿还是执行更高级的任务。

请记住，将编码分解为更小的步骤会变得更容易。因此，下次您需要管理 Excel 文件时，您将能够像专业人士一样处理它。

## 常见问题解答

### 我可以一次复制多个工作表吗？

是的，您可以循环遍历源工作簿中的工作表并将其复制到目标工作簿。每个工作表都有自己的`Copy`方法。

### 我可以将工作表复制到已经有数据的工作簿吗？

当然可以！您可以将工作表复制到任何现有工作簿中，即使它已包含数据。只需指定正确的工作表索引即可。

### 我需要付费许可证才能使用此功能吗？

虽然您可以使用免费版 Aspose.Cells 实现基本功能，但建议您获取[临时执照](https://purchase.aspose.com/temporary-license/)或购买付费许可证以获得完整功能并避免水印等限制。

### 我可以复制带有图表和图像的工作表吗？

是的！Aspose.Cells 完全支持复制包含图表、图像和其他对象的工作表。复制过程中所有内容都将保留。

### 如何将工作表复制到新工作簿中的特定位置？

您可以使用以下方式指定复制的工作表应放置的索引：`Worksheets.AddCopy`方法，可以更好地控制工作表的去向。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
