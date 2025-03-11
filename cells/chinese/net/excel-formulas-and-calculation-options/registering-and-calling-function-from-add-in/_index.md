---
title: 在 Excel 中注册并调用插件函数
linktitle: 在 Excel 中注册并调用插件函数
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过我们简单的分步教程了解如何使用 Aspose.Cells for .NET 在 Excel 中注册并调用插件中的函数。
weight: 20
url: /zh/net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中注册并调用插件函数

## 介绍
您是否想通过从插件调用函数来增强您的 Excel 体验？如果是，那么您来对地方了！Excel 插件就像电子表格的仙女教母；它们神奇地扩展了功能，为您提供了一系列触手可及的新工具。使用 Aspose.Cells for .NET，注册和使用这些插件函数比以往任何时候都更容易。 
在本指南中，我将引导您完成使用 Aspose.Cells for .NET 注册和调用 Excel 插件函数的过程。我们将逐步讲解所有内容，让您立即成为专业人士！
## 先决条件
在我们深入研究编码魔法之前，让我们先介绍一下您需要准备的内容：
1. Visual Studio：确保您的机器上已安装 Visual Studio。我们将在这里编写和运行代码。
2.  Aspose.Cells 库：您需要安装 Aspose.Cells 库。您可以从他们的[下载页面](https://releases.aspose.com/cells/net/).
3. C# 基础知识：对 C# 有一点了解会大有帮助；它将帮助您无缝地跟上。
4.  Excel 插件：你应该有一个插件文件（例如`.xlam`包含您想要注册和使用的函数。
5.  Excel 加载项示例：在本教程中，我们将使用名为`TESTUDF.xlam`。因此请确保您能使用它！
现在您已准备就绪，让我们卷起袖子开始编码吧！
## 导入包
首先，您需要在 C# 文件顶部导入一些基本命名空间。以下是您需要包含的内容：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
这些命名空间将允许您访问我们将在本教程中使用的类和方法。
让我们将其分解为易于管理的步骤。在本指南结束时，您将对如何注册插件函数并在 Excel 工作簿中使用它们有深入的了解。
## 步骤 1：设置源目录和输出目录
在注册插件之前，您需要定义插件和输出文件的存放位置。
```csharp
//源目录
string sourceDir = "Your Document Directory";
//输出目录
string outputDir = "Your Document Directory";
```
代替`"Your Document Directory"`实际路径`.xlam`文件和输出文件将被保存。这就像演出开始前设置舞台一样。
## 步骤 2：创建空工作簿
接下来，您将需要创建一个空白工作簿，我们可以在其中使用附加功能。
```csharp
//创建空工作簿
Workbook workbook = new Workbook();
```
这行代码会创建一个新的工作簿，作为我们的游乐场。您可以将其视为一块崭新的画布，随时可以发挥您的创造力。
## 步骤 3：注册插件功能
现在，让我们进入正题！是时候注册您的插件功能了。操作方法如下：
```csharp
//注册启用宏的插件以及函数名称
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
此行注册名为的附加函数`TEST_UDF`发现于`TESTUDF.xlam`插件文件。`false`参数意味着插件不是以“隔离”模式加载的。 
## 步骤 4：注册附加功能（如果有）
如果您在同一个插件文件中注册了更多功能，那么您也可以注册它们！
```csharp
//在文件中注册更多函数（如果有的话）
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
在这里，您可以看到从同一个插件添加更多功能是多么容易。只需像积木一样堆叠它们即可！
## 步骤 5：访问工作表
让我们继续并访问我们将使用函数的工作表。 
```csharp
//访问第一个工作表
Worksheet worksheet = workbook.Worksheets[0];
```
我们正在访问工作簿中的第一个工作表来放置公式。这就像打开发生有趣事情的房间的门一样。
## 步骤 6：访问特定单元格
接下来，我们需要选择要用于公式的单元格。 
```csharp
//访问第一个单元格
var cell = worksheet.Cells["A1"];
```
这里我们指向单元格 A1。这就是我们要放置魔法公式的地方。你可以把它想象成在你的藏宝图上钉住一个目标！
## 步骤 7：设置公式
现在到了揭晓的时候了！让我们设置调用我们注册函数的公式。
```csharp
//设置加载项中存在的公式名称
cell.Formula = "=TEST_UDF()";
```
通过此行，我们告诉 Excel 在单元格 A1 中使用我们的函数。这就像给 Excel 下达命令并说：“嘿，这样做！”
## 步骤 8：保存工作簿
最后但同样重要的一点是，是时候保存我们的杰作了。
```csharp
//保存工作簿以输出 XLSX 格式。
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
在这里，我们将工作簿保存为 XLSX 文件。这最后一步就像将您的画作放入画框并准备展示它一样！
## 步骤9：确认执行
最后，让我们通过在控制台上打印成功消息来结束这一切。
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
这句话是我们的胜利旗帜。这是确认一切顺利的一个小小举动。
## 结论 
就这样！您不仅学会了如何使用 Aspose.Cells for .NET 注册和调用 Excel 插件中的函数，还对所涉及的每个步骤有了更深入的了解。现在生活变得轻松了一点，不是吗？那么为什么不亲自尝试一下呢？深入了解这些 Excel 插件，让您的电子表格具有全新的交互性和功能性。
## 常见问题解答
### 什么是 Excel 插件？  
Excel 插件是一种向 Excel 添加自定义特性、函数或命令的程序，允许用户扩展其功能。
### 我是否可以在不本地安装的情况下使用 Aspose.Cells ？  
不，您需要安装 Aspose.Cells 库才能在您的.NET 应用程序中使用它。
### 如何获得 Aspose.Cells 的临时许可证？  
您可以访问他们的[临时执照页面](https://purchase.aspose.com/temporary-license/)了解更多信息。
### 是否可以从单个插件调用多个函数？  
是的！您可以使用`RegisterAddInFunction`方法。
### 在哪里可以找到有关 Aspose.Cells 的更多文档？  
您可以在网站上探索其全面的文档[这里](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
