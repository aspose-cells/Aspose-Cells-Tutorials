---
"description": "了解如何使用 Aspose.Cells for .NET 轻松向 Excel 图表添加图片。只需几个简单的步骤即可增强您的图表和演示文稿。"
"linktitle": "将图片添加到图表"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "将图片添加到图表"
"url": "/zh/net/inserting-controls-in-charts/add-picture-to-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 将图片添加到图表

## 介绍

您是否厌倦了枯燥乏味、缺乏个性化的图表？想学习如何通过添加图片来提升 Excel 的视觉效果？好吧，您很幸运！在本教程中，我们将深入 Aspose.Cells for .NET 的世界，学习如何在 Excel 图表中添加图片。那就拿起您最爱的咖啡，开始吧！

## 先决条件

在我们深入讨论编码细节之前，您需要满足一些先决条件才能顺利进行：

- Visual Studio：您将在此编写和运行 .NET 代码。请确保您已安装它。
- Aspose.Cells for .NET：您需要此库来处理 Excel 文件。您可以 [点击此处下载](https://releases。aspose.com/cells/net/).
- 对 C# 的基本了解：虽然我会指导您完成代码，但掌握 C# 基础知识会让事情变得更清晰。

### 安装步骤

1. 安装 Aspose.Cells：您可以通过 NuGet 包管理器将 Aspose.Cells 添加到您的 Visual Studio 项目中。操作步骤：前往“工具”>“NuGet 包管理器”>“管理解决方案的 NuGet 包”，然后搜索“Aspose.Cells”。点击“安装”。
2. 设置您的项目：在 Visual Studio 中创建一个新的 C# 控制台应用程序项目。

## 导入包

一切设置完成后，下一步就是将必要的软件包导入到项目中。操作方法如下：

### 导入所需的命名空间

在 C# 代码文件的顶部，您需要导入以下命名空间：

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

这会告诉你的程序，“嘿！我要使用 Aspose.Cells 的这些很酷的功能。”

现在我们已经满足了先决条件，让我们将过程分解为几个小步骤。 

## 步骤 1：定义目录

首先，我们需要设置输入和输出文件的路径。这一步至关重要，因为我们需要知道在哪里找到现有的 Excel 文件，以及在哪里保存修改后的文件。

```csharp
//源目录
string sourceDir = "Your Document Directory/";

//输出目录
string outputDir = "Your Output Directory/";
```

代替 `Your Document Directory` 和 `Your Output Directory` 使用计算机上的实际路径。 

## 步骤 2：加载现有工作簿

现在，让我们加载现有的 Excel 文件，并将图片添加到图表中。

```csharp
// 打开现有文件。
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

此代码打开工作簿，使其可供编辑。

## 步骤3：准备图像流

在添加图片之前，我们需要读取我们想要插入图表的图像。 

```csharp
// 将图像文件放入流中。
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

确保已将图片保存在指定的目录中。

## 步骤 4：定位图表

现在，让我们指定要将图片添加到哪个图表。在此示例中，我们将目标设置为第一个工作表上的第一个图表。

```csharp
// 在第二张表中获取设计师图表。
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

您可以通过相应地更改索引来访问任何工作表。

## 步骤 5：将图片添加到图表

选择图表后，就可以添加图片了！ 

```csharp
// 向图表中添加新图片。
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

这里， `50` 和 `50` 是图像放置位置的 X 和 Y 坐标，以及 `200` 是图像的宽度和高度。

## 步骤6：自定义图片的线条格式

想给你的照片增添一些亮点吗？你可以自定义边框！操作方法如下：

```csharp
// 获取图片的lineformat类型。
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// 设置虚线样式。
lineformat.DashStyle = MsoLineDashStyle.Solid;

// 设置线条粗细。
lineformat.Weight = 4;    
```

此代码片段允许您选择边框的外观和粗细。选择与您的演示文稿相符的任何样式！

## 步骤 7：保存修改后的工作簿

经过所有这些艰苦的工作后，让我们通过执行以下代码行来保存您的修改：

```csharp
// 保存 Excel 文件。
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

现在您的图片已成功集成到图表中，并且您的输出文件已准备好供查看！

## 步骤 8：指示成功

最后，您可以添加一条简单消息来确认您的操作成功：

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## 结论

在本教程中，我们探索了如何使用 Aspose.Cells for .NET 添加图片，为您的 Excel 图表增添一抹个性。只需几个简单的步骤，就能让您的演示文稿从平淡无奇变得令人难忘。还在等什么？赶快尝试一下，让您的图表闪耀夺目！

## 常见问题解答

### 我可以在一张图表中添加多张图片吗？
是的！您可以致电 `AddPictureInChart` 方法多次添加您想要的图片数量。

### Aspose.Cells 支持哪些图像格式？
Aspose.Cells 支持多种图像格式，包括 PNG、JPEG、BMP 和 GIF。

### 我可以自定义图片的位置吗？
当然！X 和 Y 坐标 `AddPictureInChart` 方法可以实现精确定位。

### Aspose.Cells 可以免费使用吗？
Aspose.Cells 提供免费试用，但要使用完整功能，需要许可证。您可以查看定价 [这里](https://purchase。aspose.com/buy).

### 在哪里可以找到更多示例？
查看 [Aspose.Cells 文档](https://reference.aspose.com/cells/net/) 以获得更详细的示例和功能。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}