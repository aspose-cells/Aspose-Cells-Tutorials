---
title: 从工作簿中提取嵌入的 Mol 文件
linktitle: 从工作簿中提取嵌入的 Mol 文件
second_title: Aspose.Cells .NET Excel 处理 API
description: 在本详细的分步教程中了解如何使用 Aspose.Cells for .NET 从 Excel 工作簿中提取嵌入的 MOL 文件。
weight: 18
url: /zh/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从工作簿中提取嵌入的 Mol 文件

## 介绍
在管理 Excel 工作簿中的数据时，有时会遇到各种非标准格式的嵌入对象。其中一种格式是 MOL（分子结构文件），它在化学中常用于表示分子信息。如果您希望使用 Aspose.Cells for .NET 从 Excel 工作簿中提取这些 MOL 文件，那么您已经找到了正确的指南。在本文中，我们将逐步引导您完成该过程，并揭开每个部分的神秘面纱。
## 先决条件
在深入研究代码之前，必须确保您拥有必要的技能和工具。以下是您需要的内容：
1. 对 .NET 编程的基本了解：您应该熟悉 C# 和 .NET 框架。
2.  Aspose.Cells for .NET：确保您拥有 Aspose.Cells 库。您可以[点击下载](https://releases.aspose.com/cells/net/).
3. IDE：您可以使用 Visual Studio 或任何其他与 .NET 兼容的 IDE。
4. 嵌入 MOL 文件的 Excel 工作簿：对于本教程，您需要一个包含 MOL 对象的 Excel 文件。您可以创建自己的文件或使用任何示例文件。
## 导入包
首先，您需要在项目中导入必要的命名空间。这对于访问 Aspose.Cells 功能至关重要。操作方法如下：

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

这些命名空间将允许您操作工作簿、访问工作表以及处理一般文件。
现在我们已经理清了先决条件，让我们深入研究代码并了解从 Excel 工作簿中提取嵌入的 MOL 文件所涉及的每个步骤。 
## 步骤 1：设置目录
第一步是确定源文档的位置以及要将提取的 MOL 文件保存到何处。让我们设置这些目录。
```csharp
string SourceDir = "Your Document Directory"; //替换为您的目录路径
string outputDir = "Your Document Directory"; //替换为您的输出路径
```
在这里，你替换`"Your Document Directory"`替换为实际目录的路径。源目录和输出目录对于应用程序来说都是可访问的，这一点很重要。
## 步骤 2：加载工作簿
设置好目录后，下一步就是加载 Excel 工作簿。现在就开始吧。

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

我们正在创建一个实例`Workbook`类并传入我们的 Excel 文件的路径，文件名为`EmbeddedMolSample.xlsx`。此步骤初始化工作簿，允许您访问其内容。
## 步骤 3：迭代工作表
现在您的工作簿已加载，您需要循环遍历工作簿中的每个工作表。这样您就可以检查每个工作表中是否有嵌入的对象。

```csharp
var index = 1; //用于命名提取的 MOL 文件
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    //进一步的提取逻辑在这里
}
```

在这里，你使用的是`foreach`循环浏览工作表。对于每个工作表，您可以访问`OleObjects`集合，其中包含所有嵌入的对象。
## 步骤 4：提取 MOL 文件
现在到了关键部分——从 OLE 对象中提取 MOL 文件。这需要在工作表循环内再进行一次循环。

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

对于您找到的每个 OLE 对象，您都会在输出目录中创建一个新文件。`ObjectData`的财产`OleObject`保存嵌入对象的数据，您可以使用`FileStream`文件按顺序命名（`OleObject1.mol`, `OleObject2.mol`等）基于`index`多变的。
## 步骤 5：确认流程完成
最后，一旦所有 MOL 文件都被提取出来，最好通知用户该过程已成功完成。

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

这行只是向控制台打印一条消息，让您知道提取已成功。这对于用户反馈来说是一个很好的举措。
## 结论
就这样！您已成功使用 Aspose.Cells for .NET 从 Excel 工作簿中提取了嵌入的 MOL 文件。此过程集成了几个核心步骤，确保以结构化的方式处理嵌入对象。无论您从事科学研究、化学分析还是仅仅处理复杂的数据集，能够提取和操作这些文件类型都会对您管理信息的方式产生重大影响。 
## 常见问题解答
### 除了 MOL，我还可以提取 Excel 中的其他文件类型吗？
是的，您可以使用类似的技术提取各种其他嵌入的文件类型。
### Aspose.Cells 可以免费使用吗？
 Aspose.Cells 是一个商业库，但你可以[限时免费试用](https://releases.aspose.com/).
### 此方法适用于所有 Excel 版本吗？
是的，只要文件格式被 Aspose.Cells 支持。
### 我可以自动化这个提取过程吗？
当然！您可以通过将代码放入计划任务或脚本中来自动执行此过程。
### 在哪里可以找到有关 Aspose.Cells 的更多文档？
您可以查看[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)了解更多详细信息和示例。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
