---
title: 在 Excel 中将形状置于前面或后面
linktitle: 在 Excel 中将形状置于前面或后面
second_title: Aspose.Cells .NET Excel 处理 API
description: 了解如何使用 Aspose.Cells for .NET 将形状发送到 Excel 的前面或后面。本指南提供了带有提示的分步教程。
weight: 16
url: /zh/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中将形状置于前面或后面

## 介绍
处理 Excel 文件时，您可能会发现自己需要更好地控制电子表格中的视觉元素。形状（如图像和图形）可以增强数据的显示效果。但是，当这些形状重叠或需要重新排序时会发生什么？这就是 Aspose.Cells for .NET 的亮点所在。在本教程中，我们将引导您完成操作 Excel 工作表中的形状的步骤，特别是将形状发送到其他形状的前面或后面。如果您已准备好提高您的 Excel 水平，那就让我们开始吧！
## 先决条件
在开始之前，您需要准备好以下几件事：
1. 安装 Aspose.Cells 库：确保已为 .NET 安装 Aspose.Cells 库。您可以找到它[这里](https://releases.aspose.com/cells/net/).
2. 开发环境：确保您已设置支持 .NET 的开发环境，例如 Visual Studio。
3. C# 基础知识：熟悉 C# 编程将帮助您更好地理解代码片段。
好吧，您已勾选了先决条件列表中的所有框？太好了！让我们继续进行有趣的部分 - 编写一些代码！
## 导入包
在深入实际编码之前，让我们导入必要的包。只需在 C# 文件顶部添加以下 using 指令即可：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
这些命名空间至关重要，因为它们包含我们用来操作 Excel 文件和形状的类和方法。
## 步骤 1：定义文件路径
在第一步中，我们需要建立源目录和输出目录。这是您的 Excel 文件所在的位置，也是您要保存修改后的文件的位置。
```csharp
//源目录
string sourceDir = "Your Document Directory";
//输出目录
string outputDir = "Your Document Directory";
```
代替`"Your Document Directory"`使用存储 Excel 文件的实际路径。
## 步骤 2：加载工作簿
现在我们已经设置了目录，让我们加载包含要操作的形状的工作簿（Excel 文件）。
```csharp
//加载源 Excel 文件
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
这行代码初始化了一个新的`Workbook`对象，将指定的Excel文件加载到内存中，以便我们可以对其进行操作。
## 步骤 3：访问工作表 
接下来，我们需要访问形状所在的特定工作表。在本例中，我们将使用第一个工作表。
```csharp
//访问第一个工作表
Worksheet ws = wb.Worksheets[0];
```
通过引用`Worksheets[0]`，我们的目标是工作簿的第一张工作表。如果您的形状位于不同的工作表上，请相应地调整索引。
## 步骤 4：访问形状
准备好访问工作表后，让我们获取我们感兴趣的形状。对于此示例，我们将访问第一个和第四个形状。
```csharp
//访问第一和第四个形状
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
这些线根据其索引从工作表中获取特定的形状。
## 步骤 5：打印形状的 Z 顺序位置
在移动任何形状之前，让我们打印出它们当前的 Z 顺序位置。这有助于我们在进行更改之前跟踪它们的位置。
```csharp
//打印形状的 Z 顺序位置
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
通过致电`ZOrderPosition`，我们可以看到每个形状在绘制顺序中的位置。
## 步骤 6：将第一个形状置于顶层
现在该采取行动了！让我们将第一个形状发送到 Z-Order 的前面。
```csharp
//将此形状置于顶层
sh1.ToFrontOrBack(2);
```
通过`2`到`ToFrontOrBack`，我们指示 Aspose.Cells 将这个形状放在前面。 
## 步骤 7：打印第二个形状的 Z 顺序位置
在我们将第二个形状放到后面之前，让我们检查一下它的位置。
```csharp
//打印形状的 Z 顺序位置
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
这使我们在进行任何更改之前了解第四个形状的位置。
## 步骤 8：将第四个形状置于后面
最后，我们将把第四个形状发送到 Z-Order 堆栈的后面。
```csharp
//将此形状置于底层
sh4.ToFrontOrBack(-2);
```
使用`-2`因为该参数将形状发送到堆栈的后面，确保它不会遮挡其他形状或文本。
## 步骤 9：保存工作簿 
最后一步是保存包含新定位形状的工作簿。
```csharp
//保存输出 Excel 文件
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
此命令将修改后的工作簿保存到指定的输出目录。
## 步骤 10：确认信息
最后，让我们提供一个简单的确认，让我们知道我们的任务已成功完成。
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
这就是我们教程的代码！
## 结论
使用 Aspose.Cells for .NET 操作 Excel 中的形状不仅简单而且功能强大。按照本指南操作，您现在应该能够轻松地将形状发送到前面或后面，从而更好地控制 Excel 演示文稿。有了这些工具，您就可以增强电子表格的视觉吸引力了。
## 常见问题解答
### Aspose.Cells 需要什么编程语言？  
您需要使用 C# 或任何 .NET 支持的语言来使用 Aspose.Cells。
### 我可以免费试用 Aspose.Cells 吗？  
是的，您可以免费试用 Aspose.Cells[这里](https://releases.aspose.com/).
### 我可以在 Excel 中操作哪些类型的形状？  
您可以操作各种形状，例如矩形、圆形、线条和图像。
### 如何获得 Aspose.Cells 的支持？  
您可以访问他们的社区论坛以获取任何支持或疑问[这里](https://forum.aspose.com/c/cells/9).
### Aspose.Cells 有临时许可证吗？  
是的，你可以申请临时执照[这里](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
