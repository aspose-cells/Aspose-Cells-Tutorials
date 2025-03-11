---
title: 写入保护 Excel 工作簿时指定作者
linktitle: 写入保护 Excel 工作簿时指定作者
second_title: Aspose.Cells for .NET API 参考
description: 在本分步指南中了解如何使用 Aspose.Cells for .NET 指定作者并对您的 Excel 工作簿进行写保护。
weight: 30
url: /zh/net/excel-security/specify-author-while-write-protecting-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 写入保护 Excel 工作簿时指定作者

## 介绍

当谈到在 .NET 应用程序中处理 Excel 文件时，Aspose.Cells 是许多开发人员的首选解决方案。其丰富的功能集使您可以轻松生成、操作和保护 Excel 文件。开发人员面临的一个常见要求是写入 Excel 工作簿，同时确保它受到保护以防止未经授权的编辑。此外，在共享文档时，指定作者对于跟踪目的非常有用。在本指南中，我们将深入探讨如何使用 Aspose.Cells for .NET 在对 Excel 工作簿进行写保护时指定作者。

## 先决条件

在我们深入实施细节之前，必须打下坚实的基础。以下是开始实施所需的先决条件：

1. Visual Studio：您需要安装 Visual Studio。您将在这里编写和编译 .NET 代码。
2. .NET Framework：确保您已安装 .NET Framework。Aspose.Cells 支持多个版本，因此请选择适合您的应用程序的版本。
3.  Aspose.Cells 库：您需要有 Aspose.Cells 库。您可以从[官方下载页面](https://releases.aspose.com/cells/net/).
4. 对 C# 的基本了解：熟悉 C# 将帮助您轻松完成编码过程。

## 导入包

为了充分利用 Aspose.Cells 提供的功能，我们首先导入必要的包。通过添加以下 using 指令来开始您的 C# 文件：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

此指令将允许您访问 Aspose.Cells 库中包含的类和方法。现在我们已经导入了包，让我们继续进行有趣的部分 - 编写代码！

## 步骤 1：设置目录

在启动工作簿之前，最好先设置源文件所在的路径以及要保存输出的位置。操作方法如下：

```csharp
//源目录
string sourceDir = "YOUR SOURCE DIRECTORY";

//输出目录
string outputDir = "YOUR OUTPUT DIRECTORY";
```

确保更换`"YOUR SOURCE DIRECTORY"`和`"YOUR OUTPUT DIRECTORY"`在您的机器上具有实际路径。将其视为在开始制作杰作之前创建一个整洁的工作空间！

## 步骤 2：创建空工作簿

现在我们已经设置了目录，下一步是创建一个空的工作簿。这实际上是您写入数据的画布。

```csharp
//创建空工作簿。
Workbook wb = new Workbook();
```

就像艺术家从一张空白画布开始一样，您也从一个空白的工作簿开始，稍后您可以在其中添加数据或格式。

## 步骤 3：对工作簿进行写保护

写保护是一个至关重要的方面，特别是如果你想确保数据的完整性时。你可以用密码来做到这一点。

```csharp
//用密码写保护工作簿。
wb.Settings.WriteProtection.Password = "YOUR_PASSWORD";
```

在这一行中，替换`"YOUR_PASSWORD"`选择一个强密码。此密码就像一扇锁着的门 — — 只有拥有钥匙（密码）的人才能进入。

## 步骤 4：指定作者

现在我们将指定工作簿的作者。这对于问责制特别有用，并允许其他人查看谁创建或修改了文件。

```csharp
//在写保护工作簿时指定作者。
wb.Settings.WriteProtection.Author = "YOUR_AUTHOR";
```

确保更换`"YOUR_AUTHOR"`以及您想要与文档关联的名称。将其视为签署您的艺术品 - 它让人们知道该感谢谁创作了这件作品！

## 步骤 5：保存工作簿

最后一步是将工作簿保存为所需的格式。在本例中，我们将其保存为 XLSX 文件。 

```csharp
//将工作簿保存为 XLSX 格式。
wb.Save(outputDir + "outputSpecifyAuthorWhileWriteProtectingWorkbook.xlsx");
```

在这里，输出文件将保存在你指定的输出目录中，名称为`outputSpecifyAuthorWhileWriteProtectingWorkbook.xlsx`。这是您的辛勤工作最终得到回报的地方，您可以与其他人分享您的工作簿，并且知道它受到了很好的保护！

## 结论

就这样！您已经学会了如何创建 Excel 工作簿、使用密码设置写保护、指定作者以及使用 Aspose.Cells for .NET 无缝保存。这些功能组合不仅可以保护您的数据，还可以保持其完整性并提供适当的归属。

## 常见问题解答

### 我可以自定义写保护密码吗？  
是的，您可以根据需要自定义密码。只需替换`YOUR_PASSWORD`使用您想要的密码。

### Aspose.Cells 可以免费使用吗？  
Aspose.Cells 是一个付费库，但您可以免费试用一段时间。请访问[免费试用链接](https://releases.aspose.com/)开始吧。

### 如何购买 Aspose.Cells 库？  
您可以通过以下方式购买 Aspose.Cells[购买页面](https://purchase.aspose.com/buy).

### 我可以在 Web 应用程序中使用这种方法吗？  
当然！Aspose.Cells 可以在使用 .NET 的桌面和 Web 应用程序中无缝运行。

### 如果我需要支持该怎么办？  
对于问题和疑难解答，Aspose 社区非常有帮助。您可以访问他们的[支持论坛](https://forum.aspose.com/c/cells/9)寻求帮助。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
