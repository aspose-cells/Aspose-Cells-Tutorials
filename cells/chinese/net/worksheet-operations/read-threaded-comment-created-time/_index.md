---
"description": "学习如何使用 Aspose.Cells for .NET 读取 Excel 中主题注释的创建时间。包含分步指南和代码示例。"
"linktitle": "读取工作表中主题评论的创建时间"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "读取工作表中主题评论的创建时间"
"url": "/zh/net/worksheet-operations/read-threaded-comment-created-time/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 读取工作表中主题评论的创建时间

## 介绍
处理 Excel 文件时，管理注释是数据协作和反馈的关键环节。如果您使用 Aspose.Cells for .NET，您会发现它在处理各种 Excel 功能（包括线程注释）方面非常强大。在本教程中，我们将重点介绍如何在工作表中读取线程注释的创建时间。无论您是经验丰富的开发人员还是刚刚入门，本指南都将逐步指导您完成整个过程。
## 先决条件
在深入研究代码之前，让我们确保您拥有开始所需的一切：
1. Aspose.Cells for .NET：确保您已安装 Aspose.Cells 库。您可以从 [Aspose 网站](https://releases。aspose.com/cells/net/).
2. Visual Studio：Visual Studio 或任何其他 .NET IDE 的工作安装，您可以在其中编写和执行 C# 代码。
3. C# 基础知识：熟悉 C# 编程将帮助您更好地理解代码片段。
4. Excel 文件：准备一个包含一些主题评论的 Excel 文件。在本例中，我们将使用名为 `ThreadedCommentsSample。xlsx`.
现在我们已经满足了先决条件，让我们导入必要的包。
## 导入包
要开始使用 Aspose.Cells，您需要导入所需的命名空间。操作方法如下：
### 导入 Aspose.Cells 命名空间
在 Visual Studio 中打开您的 C# 项目，并在代码文件顶部添加以下 using 指令：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
该命名空间允许您访问 Aspose.Cells 库提供的所有类和方法。
现在我们已经做好了准备，让我们将读取线程评论的创建时间的过程分解为可管理的步骤。
## 步骤 1：定义源目录
首先，您需要指定Excel文件所在的目录。这很重要，因为程序需要知道在哪里查找该文件。
```csharp
// 源目录
string sourceDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 替换为 Excel 文件的实际路径。例如 `"C:\\Documents\\"`。
## 第 2 步：加载工作簿
接下来，加载包含线索评论的 Excel 工作簿。操作方法如下：
```csharp
Workbook workbook = new Workbook(sourceDir + "ThreadedCommentsSample.xlsx");
```
这行代码创建一个新的 `Workbook` 通过加载指定的Excel文件来获取对象。如果找不到文件，则会抛出异常，因此请确保路径正确。
## 步骤 3：访问工作表
工作簿加载完成后，下一步是访问包含评论的特定工作表。在本例中，我们将访问第一个工作表：
```csharp
// 访问第一个工作表
Worksheet worksheet = workbook.Worksheets[0];
```
此行从工作簿中检索第一个工作表（索引 0）。如果您的评论位于其他工作表，请相应地调整索引。
## 步骤 4：获取主题评论
现在，是时候从特定单元格中检索已讨论的评论了。在此示例中，我们将从单元格 A1 获取评论：
```csharp
// 获取主题评论
ThreadedCommentCollection threadedComments = worksheet.Comments.GetThreadedComments("A1");
```
此行代码获取与单元格 A1 关联的所有主题评论。如果没有评论，则集合为空。
## 步骤 5：遍历评论
通过检索到线程评论，我们现在可以循环遍历它们并显示详细信息，包括创建时间：
```csharp
foreach (ThreadedComment comment in threadedComments)
{
    Console.WriteLine("Comment: " + comment.Notes);
    Console.WriteLine("Author: " + comment.Author.Name);
    Console.WriteLine("Created Time: " + comment.CreatedTime);
}
```
此循环遍历 `threadedComments` 收集并打印出评论文本、作者姓名和评论创建时间。
## 步骤6：确认消息
最后，执行完注释读取逻辑后，最好提供一条确认消息。这有助于调试并确保代码成功执行：
```csharp
Console.WriteLine("ReadThreadedCommentCreatedTime executed successfully.");
```
## 结论
恭喜！您已成功学习如何使用 Aspose.Cells for .NET 读取 Excel 工作表中主题注释的创建时间。此功能对于跟踪 Excel 文档中的反馈和协作非常有用。只需几行代码，您就可以提取有价值的信息，从而增强您的数据分析和报告流程。
## 常见问题解答
### 什么是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一个功能强大的库，允许开发人员在 .NET 应用程序中创建、操作和转换 Excel 文件。
### 如何下载 Aspose.Cells for .NET？
您可以从 [Aspose 网站](https://releases。aspose.com/cells/net/).
### 有免费试用吗？
是的，您可以免费试用 Aspose.Cells，请访问 [免费试用页面](https://releases。aspose.com/).
### 我可以访问其他单元格的评论吗？
当然！您可以在 `GetThreadedComments` 方法从任何单元格访问注释。
### 我可以在哪里获得 Aspose.Cells 的支持？
如需支持，您可以访问 [Aspose 论坛](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}