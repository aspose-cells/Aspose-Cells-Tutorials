---
title: 获取电子表格中使用的字体列表
linktitle: 获取电子表格中使用的字体列表
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过这个简单易懂的教程学习如何使用 Aspose.Cells for .NET 从 Excel 电子表格中获取和列出字体。
weight: 10
url: /zh/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 获取电子表格中使用的字体列表

## 介绍
您是否曾经在浏览 Excel 电子表格时，对各个单元格中使用的字体感到疑惑？也许您遇到了一份旧文档，想知道选择了哪种字体？好吧，您很幸运！使用 Aspose.Cells for .NET，就像拥有一个工具箱，可以让您筛选并发现隐藏在电子表格中的字体秘密。在本指南中，我们将带您了解如何轻松检索 Excel 文件中使用的所有字体列表。系好安全带，让我们深入电子表格的世界！
## 先决条件
在我们开始编写代码之前，您需要做一些准备工作。别担心，这非常简单。以下是您需要准备的清单：
1. Visual Studio：确保您的计算机上安装了 Visual Studio 版本。我们将在这里编写代码。
2. Aspose.Cells for .NET：您需要有 Aspose.Cells 库。如果您尚未下载，可以从[地点](https://releases.aspose.com/cells/net/).
3. C# 基础知识：对 C# 编程有一点了解肯定能帮助您轻松浏览代码。
4. 示例 Excel 文件：您需要一个示例 Excel 文件，例如“sampleGetFonts.xlsx”。这是我们进行字体探索的地方。
一旦一切准备就绪，您就可以开始编码了！
## 导入包
首先，让我们导入必要的命名空间。在 .NET 中，导入包就像邀请合适的客人参加你的聚会——没有他们，事情就不会顺利进行。
导入 Aspose.Cells 的方法如下：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
通过这行简单的代码，我们将 Aspose.Cells 的核心功能引入到我们的项目中。现在，让我们继续加载工作簿。
## 步骤 1：设置文档目录
首先，在深入研究代码之前，您需要设置文档目录的路径。这是您的 Excel 文件所在的位置。 
```csharp
string dataDir = "Your Document Directory";
```
您需要将“您的文档目录”替换为您的 Excel 文件所在的实际路径。这相当于告诉程序，“嘿，这是我存放 Excel 文件的地方；快去看看吧！”
## 步骤 2：加载源工作簿
现在该加载 Excel 文件了。我们将创建一个新的`Workbook`类并传入文件的路径。 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
这是怎么回事？我们基本上打开了电子表格的大门。`Workbook`类允许我们与 Excel 文件的内容进行交互。 
## 步骤 3：获取所有字体
现在到了神奇的时刻——让我们真正地检索字体！`GetFonts()`方法就是我们的黄金门票。
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
在这里，我们要求工作簿透露其中使用的所有字体。`fnts`阵列将保存我们的宝藏。
## 步骤 4：打印字体
最后，让我们把这些字体打印出来。这将帮助我们验证我们所发现的东西。
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
此循环遍历我们的每个字体`fnts`数组，并将它们逐一输出到控制台。这就像在 Excel 文件中展示所有酷炫的排版选择一样！
## 结论
就这样！只需几行代码，您就可以使用 Aspose.Cells for .NET 成功检索并打印 Excel 电子表格中使用的字体列表。这不仅仅是字体的问题；它还涉及了解文档的细微之处、增强演示文稿以及掌握电子表格中的排版艺术。无论您是开发人员还是只是喜欢摆弄 Excel 的人，这个小代码片段都可能改变游戏规则。 
## 常见问题解答
### 我需要单独安装 Aspose.Cells 吗？
是的，您需要下载并在您的项目中引用该库。 
### 我可以将 Aspose.Cells 用于其他格式吗？
当然！Aspose.Cells 适用于多种 Excel 格式，例如 XLSX、XLS 和 CSV。
### 有免费试用吗？
是的，你可以从[下载链接](https://releases.aspose.com/).
### 我如何获得技术支持？
如果你需要帮助，[Aspose 支持论坛](https://forum.aspose.com/c/cells/9)是一项宝贵的资源。
### Aspose.Cells 与 .NET Core 兼容吗？
是的，Aspose.Cells 也与.NET Core 项目兼容。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
