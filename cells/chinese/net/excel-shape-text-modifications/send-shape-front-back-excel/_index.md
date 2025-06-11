---
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 中将形状置于顶层或底层。本指南提供分步教程和实用技巧。"
"linktitle": "在 Excel 中将形状发送到前面或后面"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 Excel 中将形状发送到前面或后面"
"url": "/zh/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中将形状发送到前面或后面

## 介绍
处理 Excel 文件时，您可能会发现需要更好地控制电子表格中的视觉元素。形状（例如图像和图形）可以增强数据的呈现效果。但是，当这些形状重叠或需要重新排序时会发生什么？这正是 Aspose.Cells for .NET 的亮点所在。在本教程中，我们将引导您完成操作 Excel 工作表中形状的步骤，特别是将形状置于其他形状的前面或后面。如果您准备好提升您的 Excel 技能，那就让我们立即开始吧！
## 先决条件
在我们开始之前，您需要准备好以下几件事：
1. 安装 Aspose.Cells 库：确保您已安装适用于 .NET 的 Aspose.Cells 库。您可以找到它 [这里](https://releases。aspose.com/cells/net/).
2. 开发环境：确保您已设置支持 .NET 的开发环境，例如 Visual Studio。
3. C# 基础知识：熟悉 C# 编程将帮助您更好地理解代码片段。
好了，你已经满足了所有先决条件？太棒了！让我们进入最有趣的部分——编写代码！
## 导入包
在深入实际编码之前，让我们导入必要的包。只需在 C# 文件的顶部添加以下 using 指令即可：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
这些命名空间至关重要，因为它们包含我们用来操作 Excel 文件和形状的类和方法。
## 步骤 1：定义文件路径
第一步，我们需要建立源目录和输出目录。这是您的 Excel 文件所在的位置，也是您要保存修改后文件的位置。
```csharp
//源目录
string sourceDir = "Your Document Directory";
//输出目录
string outputDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 使用存储 Excel 文件的实际路径。
## 第 2 步：加载工作簿
现在我们已经设置了目录，让我们加载包含我们想要操作的形状的工作簿（Excel 文件）。
```csharp
//加载源 Excel 文件
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
这行代码初始化了一个新的 `Workbook` 对象，将指定的 Excel 文件加载到内存中，以便我们可以对其进行操作。
## 步骤 3：访问工作表 
接下来，我们需要访问形状所在的具体工作表。在本例中，我们将使用第一个工作表。
```csharp
//访问第一个工作表
Worksheet ws = wb.Worksheets[0];
```
通过引用 `Worksheets[0]`，我们的目标是工作簿的第一个工作表。如果您的形状位于其他工作表上，请相应地调整索引。
## 步骤 4：访问形状
准备好访问工作表后，让我们获取我们感兴趣的形状。对于此示例，我们将访问第一个和第四个形状。
```csharp
//访问第一和第四个形状
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
这些线根据其索引从工作表中获取特定的形状。
## 步骤 5：打印形状的 Z 顺序位置
在移动任何形状之前，让我们打印出它们当前的 Z 轴位置。这有助于我们在进行更改之前跟踪它们的位置。
```csharp
//打印形状的 Z 顺序位置
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
通过调用 `ZOrderPosition`，我们可以看到每个形状在绘制顺序中的位置。
## 步骤 6：将第一个形状置于顶层
现在该行动了！让我们将第一个形状发送到 Z 顺序的最前面。
```csharp
//将此形状置于顶层
sh1.ToFrontOrBack(2);
```
通过 `2` 到 `ToFrontOrBack`，我们指示 Aspose.Cells 将这个形状放在前面。 
## 步骤 7：打印第二个形状的 Z 顺序位置
在我们将第二个形状发送到后面之前，让我们检查一下它的位置。
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
使用 `-2` 因为参数将形状发送到堆栈的后面，确保它不会遮挡其他形状或文本。
## 步骤 9：保存工作簿 
最后一步是保存包含新定位形状的工作簿。
```csharp
//保存输出 Excel 文件
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
此命令将修改后的工作簿保存到指定的输出目录。
## 步骤10：确认消息
最后，让我们提供一个简单的确认，让我们知道我们的任务已成功完成。
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
这就是我们教程的代码！
## 结论
使用 Aspose.Cells for .NET 在 Excel 中操作形状不仅简单易用，而且功能强大。按照本指南操作，您现在应该能够轻松地将形状置于最前面或最后面，从而更好地控制您的 Excel 演示文稿。借助这些工具，您可以提升电子表格的视觉吸引力。
## 常见问题解答
### Aspose.Cells 需要什么编程语言？  
您需要使用 C# 或任何 .NET 支持的语言来使用 Aspose.Cells。
### 我可以免费试用 Aspose.Cells 吗？  
是的，您可以免费试用 Aspose.Cells [这里](https://releases。aspose.com/).
### 我可以在 Excel 中操作哪些类型的形状？  
您可以操作各种形状，例如矩形、圆形、线条和图像。
### 我如何获得 Aspose.Cells 的支持？  
您可以访问他们的社区论坛以获取任何支持或疑问 [这里](https://forum。aspose.com/c/cells/9).
### Aspose.Cells 有临时许可证吗？  
是的，您可以申请临时驾照 [这里](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}