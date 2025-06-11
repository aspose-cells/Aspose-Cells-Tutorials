---
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 中按比例定位图像。让您的电子表格更具视觉吸引力。"
"linktitle": "Excel 中的位置图片（比例）"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "Excel 中的位置图片（比例）"
"url": "/zh/net/excel-ole-picture-objects/position-picture-proportional-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel 中的位置图片（比例）

## 介绍
您是否厌倦了那些像素化的图片，它们似乎总是无法完美地融入您的 Excel 电子表格？想象一下：您有一个漂亮的徽标，需要在 Excel 表格中突出显示，但它最终被挤压、拉伸或放置不当。没有人希望出现这种情况！好吧，坐稳了，因为今天您将学习如何使用 Aspose.Cells 库在 Excel 中按比例定位图像。这个强大的库使操作 Excel 文件变得轻而易举，无论是用于报告、数据分析，还是仅仅修饰您的演示文稿。让我们深入了解如何完美对齐图片！
## 先决条件
在我们深入实际编码之前，您需要在机器上设置一些东西：
1. Visual Studio：确保您已安装 Visual Studio，因为它将为您的 .NET 项目提供便捷的环境。
2. Aspose.Cells 库：您需要 Aspose.Cells 库。您可以免费试用，也可以从 [Aspose 网站](https://purchase。aspose.com/buy).
3. C# 基础知识：稍微熟悉一下 C# 编程将有助于理解我们将要讨论的示例。
4. 图像文件：准备好要插入 Excel 表的图像（如您的徽标）。
现在您已准备好一切，让我们开始编码吧！
## 导入包
要在您的项目中开始使用 Aspose.Cells，您需要导入特定的命名空间。操作方法如下：
### 创建新项目
在 Visual Studio 中，创建一个新项目：
- 打开 Visual Studio。
- 点击“创建新项目”。
- 根据您的喜好选择“类库（.NET Framework）”或“控制台应用程序”。
### 安装 Aspose.Cells
您可以通过 NuGet 将 Aspose.Cells 包添加到您的项目中。具体操作如下：
- 在解决方案资源管理器中右键单击您的项目。
- 选择“管理 NuGet 包”。
- 搜索“Aspose.Cells”并单击“安装”。
### 添加使用指令
在代码文件的顶部，包含以下指令：
```csharp
using System.IO;
using Aspose.Cells;
```
这些指令将允许您访问操作 Excel 文件所需的类。
现在，让我们将其分解为详细的步骤，以便在 Excel 中按比例成功定位图像。
## 步骤 1：设置目录
首先，请确保你有一个专门用于存放文档的文件夹。如果文件夹不存在，请按照以下步骤创建：
```csharp
string dataDir = "Your Document Directory";
// 如果目录尚不存在，则创建该目录。
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
此代码片段会创建一个新目录（如果不存在）来存储您的 Excel 文件。只需替换 `"Your Document Directory"` 使用您想要保存文件的实际路径。
## 步骤 2：实例化工作簿
接下来，让我们创建一个新的工作簿：
```csharp
Workbook workbook = new Workbook();
```
此行初始化一个新的工作簿对象，为您提供一个空白画布以供工作。
## 步骤 3：添加新工作表
现在我们已经设置了工作簿，让我们向其中添加一个新工作表：
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
这将添加一个新的工作表并返回该工作表的索引，我们可以稍后使用该索引来操作它。
## 步骤 4：访问新工作表
要操作新添加的工作表，您需要访问它：
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
现在， `worksheet` 将允许我们向该特定工作表添加内容和图像。
## 步骤5：插入图片
现在到了激动人心的部分！让我们添加你美丽的图像。替换 `"logo.jpg"` 使用您的图像文件的名称：
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
此行将图像添加到单元格 F6（因为行和列都是零索引， `5` 指第六个单元格）。
## 步骤6：访问添加的图片
插入图像后，您可以像这样访问它：
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
这使您可以操纵图片属性。
## 步骤 7：按比例定位图片
现在，让我们按比例定位图片：
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
这里， `UpperDeltaX` 和 `UpperDeltaY` 调整图像相对于单元格尺寸的位置。您可以调整这些值，使图像达到合适的尺寸。
## 步骤 8：保存更改
最后，保存工作簿以保留所有更改：
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
此行将您的工作簿保存为 `book1.out.xls` 在指定的目录中。
## 结论
就这样！您已经学会了如何使用 Aspose.Cells for .NET 在 Excel 中按比例放置图片。这不仅仅是插入图片，更重要的是让它们在电子表格中看起来更完美。请记住：放置得当的图片可以显著提升数据呈现效果。
尽情尝试不同的图像和布局，并立即探索 Aspose.Cells 提供的丰富功能。您的 Excel 表格即将焕然一新！
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个强大的 .NET 库，用户无需安装 Microsoft Excel 即可创建、操作和转换 Excel 文件。
### 我可以免费使用 Aspose.Cells 吗？
是的，Aspose.Cells 提供免费试用版，您可以下载 [这里](https://releases。aspose.com/).
### 在哪里可以找到该文档？
您可以访问综合 [文档](https://reference.aspose.com/cells/net/) 适用于 Aspose.Cells。
### Aspose.Cells 支持所有图像格式吗？
Aspose.Cells 支持各种格式，包括 JPEG、PNG、BMP、GIF 和 TIFF。
### 我如何获得 Aspose.Cells 的支持？
如有任何疑问，欢迎访问 [支持论坛](https://forum.aspose.com/c/cells/9) 您可以在那里提出问题。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}