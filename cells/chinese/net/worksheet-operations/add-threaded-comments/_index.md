---
title: 在工作表中添加主题评论
linktitle: 在工作表中添加主题评论
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过本分步教程学习如何使用 Aspose.Cells for .NET 在 Excel 工作表中添加线程注释。轻松增强协作。
weight: 10
url: /zh/net/worksheet-operations/add-threaded-comments/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在工作表中添加主题评论

## 介绍
您是否希望使用线程注释来增强您的 Excel 工作表？如果您是使用 Aspose.Cells for .NET 的开发人员，那么您很幸运！线程注释允许在 Excel 工作表中进行更有组织的讨论，从而使用户能够有效地协作。无论您是在处理需要反馈的项目还是只想注释数据，本教程都将指导您完成使用 Aspose.Cells 在 Excel 工作表中添加线程注释的过程。 
## 先决条件
在开始之前，请确保您已满足以下先决条件：
1. Visual Studio：确保您的机器上安装了 Visual Studio，因为它是 .NET 开发最常用的 IDE。
2.  Aspose.Cells for .NET：您需要安装 Aspose.Cells for .NET 库。如果您尚未安装，可以从网站下载[这里](https://releases.aspose.com/cells/net/).
3. C# 基础知识：熟悉 C# 编程至关重要，因为本教程将用 C# 编写。
4. .NET Framework：确保您的项目设置了兼容的.NET 框架版本。
## 导入包
要使用 Aspose.Cells，您需要在项目中导入所需的命名空间。操作方法如下：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
这些命名空间将使您能够访问操作 Excel 文件和管理线程注释所需的类和方法。
现在我们已经设置了先决条件并导入了必要的包，为了清楚起见，让我们将添加线程评论的过程分解为多个步骤。
## 步骤 1：创建新工作簿
首先，我们需要创建一个新的工作簿，在其中添加我们的主题评论。
```csharp
string outDir = "Your Document Directory"; //设置输出目录
Workbook workbook = new Workbook(); //创建新工作簿
```
在此步骤中，您将设置保存 Excel 文件的输出目录。`Workbook`类是在 Aspose.Cells 中创建和操作 Excel 文件的入口点。
## 第 2 步：添加评论作者
在添加评论之前，我们需要定义一个作者。此作者将与您创建的评论相关联。现在让我们添加一位作者。
```csharp
int authorIndex = workbook.Worksheets.ThreadedCommentAuthors.Add("Aspose Test", "", ""); //添加作者
ThreadedCommentAuthor author = workbook.Worksheets.ThreadedCommentAuthors[authorIndex]; //获取作者
```
在这里，我们使用`Add`方法创建新作者。您可以在参数中指定作者的姓名和其他可选详细信息（如电子邮件）。稍后添加评论时将引用此作者。
## 步骤 3：添加主题评论
现在我们已经设置了作者，是时候向工作表中的特定单元格添加线程注释了。 
```csharp
workbook.Worksheets[0].Comments.AddThreadedComment("A1", "Test Threaded Comment", author); //添加主题评论
```
在此步骤中，我们将向第一个工作表的 A1 单元格添加注释。您可以替换`"A1"`任何您想要添加评论的单元格引用。引号中的消息是评论的内容。
## 步骤 4：保存工作簿
添加主题评论后，您需要保存工作簿以使更改持久保留。
```csharp
workbook.Save(outDir + "AddThreadedComments_out.xlsx"); //保存工作簿
```
此处，工作簿将保存在指定的输出目录中，名称为`AddThreadedComments_out.xlsx`确保目录存在，否则您将遇到文件未找到错误。
## 步骤5：确认成功
最后我们向控制台输出一条消息来表明我们的操作成功了。
```csharp
Console.WriteLine("AddThreadedComments executed successfully."); //确认信息
```
此步骤是可选的，但对于调试很有用。它让您知道代码执行没有错误。
## 结论
就这样！您已成功使用 Aspose.Cells for .NET 将线程注释添加到 Excel 工作表中。当多个用户处理同一文档时，此功能可以显著增强协作并提供清晰的沟通。
主题式评论不仅能让文档中的讨论更加丰富，还能让您的注释井然有序。您可以随意尝试不同的单元格、作者和评论，看看它们在您的工作簿中如何显示。
## 常见问题解答
### Excel 中的线程注释是什么？  
主题评论是一种允许在评论本身内进行回复和讨论的评论，使得协作更加容易。
### 我可以向单个单元格添加多个评论吗？  
是的，您可以在一个单元格中添加多个线程评论，以便进行广泛的讨论。
### 我需要许可证才能使用 Aspose.Cells 吗？  
虽然您可以免费试用 Aspose.Cells，但生产使用需要许可证。您可以获取它[这里](https://purchase.aspose.com/buy).
### 如何在 Excel 中查看评论？  
添加评论后，您可以将鼠标悬停在放置评论的单元格上或通过评论窗格来查看它们。
### 在哪里可以找到有关 Aspose.Cells 的更多信息？  
您可以参考[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)了解更多信息和详细示例。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
