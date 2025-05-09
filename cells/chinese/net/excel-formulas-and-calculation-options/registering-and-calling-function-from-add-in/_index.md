---
"description": "通过我们简单的分步教程，了解如何使用 Aspose.Cells for .NET 在 Excel 中注册和调用插件中的函数。"
"linktitle": "在 Excel 中注册并调用插件函数"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 Excel 中注册并调用插件函数"
"url": "/zh/net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中注册并调用插件函数

## 介绍
您是否想通过调用插件中的函数来提升您的 Excel 体验？如果是，那么您来对地方了！Excel 插件就像电子表格的精灵教母；它们神奇地扩展了功能，为您提供了一系列触手可及的新工具。有了 Aspose.Cells for .NET，注册和使用这些插件函数比以往任何时候都更加简单。 
在本指南中，我将引导您使用 Aspose.Cells for .NET 注册并调用 Excel 插件中的函数。我们将逐步讲解，让您快速上手！
## 先决条件
在我们深入研究编码魔法之前，让我们先介绍一下您需要具备哪些条件：
1. Visual Studio：请确保您的计算机上已安装 Visual Studio。我们将在这里编写和运行代码。
2. Aspose.Cells 库：您需要安装 Aspose.Cells 库。您可以从他们的 [下载页面](https://releases。aspose.com/cells/net/).
3. C# 基础知识：对 C# 有一点了解会大有帮助；它将帮助您无缝地跟进。
4. Excel 插件：你应该有一个插件文件（例如 `.xlam`包含您想要注册和使用的函数。
5. Excel 插件示例：在本教程中，我们将使用名为 `TESTUDF.xlam`。因此请确保您能随时使用它！
现在您已经做好准备，让我们卷起袖子开始编码吧！
## 导入包
首先，你需要在 C# 文件的顶部导入一些必要的命名空间。以下是你需要包含的内容：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
这些命名空间将允许您访问我们将在本教程中使用的类和方法。
让我们将其分解为易于管理的步骤。完成本指南后，您将对如何注册插件函数并在 Excel 工作簿中使用它们有深入的理解。
## 步骤 1：设置源目录和输出目录
在注册插件之前，您需要定义插件和输出文件的位置。
```csharp
// 源目录
string sourceDir = "Your Document Directory";
// 输出目录
string outputDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 实际路径 `.xlam` 文件和输出文件将被保存。这就像演出开始前的舞台布置。
## 步骤 2：创建空工作簿
接下来，您需要创建一个空白工作簿，我们可以在其中使用附加功能。
```csharp
// 创建空工作簿
Workbook workbook = new Workbook();
```
这行代码创建了一个新的工作簿，它将作为我们的游乐场。你可以把它想象成一块崭新的画布，随时可以挥洒你的创意。
## 步骤3：注册插件功能
现在，让我们进入正题！是时候注册你的插件函数了。操作方法如下：
```csharp
// 注册启用宏的插件以及函数名称
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
此行注册名为 `TEST_UDF` 发现于 `TESTUDF.xlam` 插件文件。 `false` 参数意味着插件不会以“隔离”模式加载。 
## 步骤 4：注册附加功能（如果有）
如果您在同一个插件文件中注册了更多功能，您也可以注册它们！
```csharp
// 在文件中注册更多函数（如果有）
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
在这里，您可以看到从同一个插件添加更多功能是多么容易。只需像积木一样不断堆叠它们即可！
## 步骤 5：访问工作表
让我们继续并访问我们将使用函数的工作表。 
```csharp
// 访问第一个工作表
Worksheet worksheet = workbook.Worksheets[0];
```
我们正在访问工作簿中的第一个工作表来放置公式。这就像打开了通往发生有趣事情的房间的门。
## 步骤 6：访问特定单元格
接下来，我们需要选择要用于公式的单元格。 
```csharp
// 访问第一个单元格
var cell = worksheet.Cells["A1"];
```
现在我们指向单元格 A1。这就是我们要放置魔法公式的地方。你可以把它想象成在藏宝图上钉住一个目标！
## 步骤 7：设置公式
现在是时候揭开神秘面纱了！让我们设置调用已注册函数的公式。
```csharp
// 设置加载项中存在的公式名称
cell.Formula = "=TEST_UDF()";
```
通过这行代码，我们告诉 Excel 在单元格 A1 中使用我们的函数。这就像给 Excel 下达命令，说：“嘿，执行这个！”
## 步骤 8：保存工作簿
最后但同样重要的一点是，是时候保存我们的杰作了。
```csharp
// 保存工作簿以输出 XLSX 格式。
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
在这里，我们将工作簿保存为 XLSX 文件。这最后一步就像把你的画作装裱起来，准备展示它一样！
## 步骤9：确认执行
最后，让我们通过在控制台上打印成功消息来结束这一切。
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
这句话就像我们的胜利旗帜。这句小妙语，让我们确认一切顺利。
## 结论 
就这样！您不仅学习了如何使用 Aspose.Cells for .NET 注册和调用 Excel 插件中的函数，还对每个步骤有了更深入的理解。现在是不是轻松多了？何不亲自尝试一下？深入研究这些 Excel 插件，让您的电子表格的交互性和功能性更上一层楼。
## 常见问题解答
### 什么是 Excel 插件？  
Excel 插件是一种向 Excel 添加自定义特性、功能或命令的程序，允许用户扩展其功能。
### 我可以在不本地安装的情况下使用 Aspose.Cells 吗？  
不，您需要安装 Aspose.Cells 库才能在您的 .NET 应用程序中使用它。
### 如何获得 Aspose.Cells 的临时许可证？  
您可以访问他们的 [临时执照页面](https://purchase.aspose.com/temporary-license/) 了解更多信息。
### 是否可以从单个插件调用多个功能？  
是的！您可以使用 `RegisterAddInFunction` 方法。
### 在哪里可以找到有关 Aspose.Cells 的更多文档？  
您可以在网站上浏览其全面的文档 [这里](https://reference。aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}