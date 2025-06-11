---
"description": "学习如何使用 Aspose.Cells for .NET 从 Excel 中的齿轮状 SmartArt 元素中提取文本。包含分步指南和代码示例。"
"linktitle": "在 Excel 中从齿轮类型 Smart Art 中提取文本"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 Excel 中从齿轮类型 Smart Art 中提取文本"
"url": "/zh/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中从齿轮类型 Smart Art 中提取文本

## 介绍
使用 Excel 时，您可能会遇到 SmartArt 图形，它们能以视觉上引人入胜的方式传达您的信息。在这些图形中，齿轮状 SmartArt 图形因其层次分明、方向清晰的流程而备受青睐，常用于项目管理或系统建模。但是，如果您需要以编程方式从这些形状中提取文本，该怎么办？Aspose.Cells for .NET 就派上用场了！在这篇博文中，我们将逐步指导您如何使用 Aspose.Cells for .NET 从 Excel 中的齿轮状 SmartArt 形状中提取文本。
## 先决条件
在深入探讨之前，您需要满足一些基本前提条件。不用担心，这很简单，我会指导您完成。
### .NET 环境
确保您的计算机上已设置 .NET 开发环境。这可以是 Visual Studio，也可以是任何支持 .NET 开发的 IDE。
### Aspose.Cells for .NET
接下来，您需要安装 Aspose.Cells 库。这是一个强大的工具，可以帮助您无缝操作 Excel 文件。您可以从 [Aspose 发布页面](https://releases.aspose.com/cells/net/)。如果您想先探索一下，可以利用 [免费试用](https://releases。aspose.com/).
### C# 基础知识
学习本教程只需具备 C# 编程的基本知识即可。如果您是新手，不用担心——我会尽可能地设计步骤，方便初学者学习。
### 示例 Excel 文件
在本教程中，您还需要一个包含齿轮形状 SmartArt 图形的示例 Excel 文件。您可以轻松创建一个，也可以在线查找模板。只需确保 SmartArt 图形至少包含一个齿轮形状即可。
## 导入包
要开始编码，您需要导入必要的软件包。操作方法如下：
### 创建新项目
1. 打开您的 .NET IDE。
2. 创建一个新项目。例如，在 .NET 选项下选择“控制台应用程序”。
3. 为您的项目命名并设置所需的框架。 
### 添加引用
要使用 Aspose.Cells，您需要将库引用添加到您的项目中：
1. 在解决方案资源管理器中右键单击您的项目名称。
2. 选择“管理 NuGet 包”。
3. 搜索“Aspose.Cells”并安装它。
一旦安装完毕，您就可以开始编码了！
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
现在，让我们逐步分解用于提取文本的代码。
## 步骤 1：设置源目录
首先定义 Excel 文件所在的目录：
```csharp
// 源目录
string sourceDir = "Your Document Directory";
```
确保更换 `"Your Document Directory"` 使用您的 Excel 文件的实际路径。
## 步骤 2：加载 Excel 工作簿
接下来，我们将加载 Excel 工作簿。以下是访问其内容的方法：
```csharp
// 加载包含齿轮类型智能艺术形状的示例 Excel 文件。
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
此部分将加载您的示例 Excel 工作簿。
## 步骤 3：访问第一个工作表
现在我们已经加载了工作簿，让我们访问 SmartArt 存在的第一个工作表：
```csharp
// 访问第一个工作表。
Worksheet ws = wb.Worksheets[0];
```
这将检索第一个工作表以供进一步操作。
## 步骤 4：访问第一个形状
接下来，我们需要访问工作表中的第一个形状。通过这样做，我们可以浏览我们的SmartArt图形：
```csharp
// 访问第一个形状。
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
在这里，我们关注第一个形状，我们假设它是我们需要的 SmartArt。
## 步骤 5：获取群组形状
一旦我们有了形状，就可以得到 SmartArt 表示的结果了：
```csharp
// 以群组形状的形式获取齿轮型智能艺术形状的结果。
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
这将以分组形状的形式检索我们的齿轮类型 SmartArt。
## 步骤 6：提取单个形状
现在，让我们提取组成 SmartArt 的各个形状：
```csharp
// 获取由组形状组成的单个形状的列表。
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
该数组将保存我们需要循环的所有单个形状。
## 步骤 7：提取并打印文本
最后，我们可以循环遍历形状数组并从任何齿轮形状中提取文本：
```csharp
// 提取齿轮类型形状的文本并将其打印在控制台上。
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
在这个循环中，我们检查形状的类型，如果是齿轮类型，则打印文本。
## 步骤8：执行确认
最后，您可能希望在过程成功完成后添加一条确认消息：
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
这样，您的提取就完成了，您应该在控制台中看到您的文本输出！
## 结论
恭喜！您刚刚学习了如何使用 Aspose.Cells for .NET 从 Excel 中的齿轮状 SmartArt 图形中提取文本。这项便捷的技术为自动化依赖可视化数据呈现的报告或文档打开了大门。无论您是经验丰富的开发人员还是刚刚入门，控制和提取 SmartArt 中的信息都可以简化您的工作流程并提高效率。别忘了探索详细信息 [Aspose.Cells文档](https://reference.aspose.com/cells/net/) 以获得进一步的功能。
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个 .NET 库，允许开发人员轻松创建和操作 Excel 文件。
### 我可以将 Aspose.Cells 与其他语言一起使用吗？
是的！Aspose.Cells 支持多种编程语言，包括 Java 和 Python。
### 我需要购买 Aspose.Cells for .NET 吗？
Aspose.Cells 提供免费试用，但如需长期使用，则需要购买。您可以找到购买选项 [这里](https://purchase。aspose.com/buy).
### 是否为 Aspose.Cells 用户提供支持？
当然！你可以在 [Aspose.Cells论坛](https://forum。aspose.com/c/cells/9).
### 我可以使用此方法提取其他 SmartArt 类型吗？
是的，只需稍加修改，您就可以通过更改代码中的条件从各种 SmartArt 形状中提取文本。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}