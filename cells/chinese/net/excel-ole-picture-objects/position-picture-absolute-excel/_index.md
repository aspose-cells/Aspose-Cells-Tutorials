---
"description": "通过本全面的分步教程学习如何使用 Aspose.Cells for .NET 在 Excel 中绝对定位图像。"
"linktitle": "Excel 中的位置图片（绝对）"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "Excel 中的位置图片（绝对）"
"url": "/zh/net/excel-ole-picture-objects/position-picture-absolute-excel/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel 中的位置图片（绝对）

## 介绍
您是否曾经为在 Excel 电子表格中正确定位图片而苦恼？您并不孤单！许多用户都面临这一挑战，尤其是在数据可视化需要绝对定位以获得更佳的美观度或清晰度时。不用再犹豫了；本指南将指导您使用 Aspose.Cells for .NET 在 Excel 工作表中轻松完成图片绝对定位。无论您是从事 Excel 操作的开发人员，还是希望增强报告质量的数据分析师，我们的分步教程都能帮助您简化 Excel 图像处理体验！
## 先决条件
在深入研究代码和细节之前，您需要准备一些东西：
1. Aspose.Cells 库：确保您拥有最新版本的 Aspose.Cells for .NET 库。您可以从 [发布页面](https://releases。aspose.com/cells/net/).
2. 开发环境：确保您已设置好可用的 .NET 开发环境。您可以使用 Visual Studio 或任何其他您选择的 IDE。
3. C# 基础知识：熟悉 C# 编程语言将有助于理解代码片段。
4. 图像文件：将要插入 Excel 工作表的图像文件（例如“logo.jpg”）保存在您指定的文档目录中。

## 导入包
首先，确保导入项目所需的包。你的项目文件应包含以下命名空间：
```csharp
using System.IO;
using Aspose.Cells;
```
通过导入这些命名空间，我们确保我们的程序可以利用 Aspose.Cells 提供的功能。
为了清楚起见，让我们将其分解为易于管理的步骤。
## 步骤 1：设置文档目录
在此初始步骤中，您需要定义文档所在的目录。这对于程序确定文件保存或获取位置至关重要。设置方法如下：
```csharp
string dataDir = "Your Document Directory";
```
只需更换 `"Your Document Directory"` 替换为图像文件的实际路径。这可能是这样的 `"C:\\Users\\YourUsername\\Documents\\"`。
## 步骤2：实例化工作簿对象
接下来，您需要创建一个新的实例 `Workbook` 类。此对象代表您的 Excel 文件：
```csharp
Workbook workbook = new Workbook();
```
此时，您已拥有一个可以填充数据和图像的工作簿。
## 步骤 3：添加新工作表
现在您有了工作簿，接下来需要向其中添加一个工作表。这就是添加和定位图像的神奇之处：
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
此行在您的工作簿中创建一个新的工作表并返回其索引，我们将其存储在变量中 `sheetIndex`。
## 步骤4：获取新的工作表
让我们引用新创建的工作表。使用刚刚获得的索引，我们可以访问并操作该工作表：
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
现在您可以使用 `worksheet` 对象添加内容，包括图像。
## 步骤5：添加图片
现在到了激动人心的部分！这里我们要将图片添加到工作表中。我们指定图片要锚定的行和列索引（在本例中，位于单元格“F6”，即第 5 行和第 5 列）：
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
此行代码有效地将图像锁定在相对于整个工作表的指定位置。但是，目前，它仍会随单元格一起调整大小。
## 步骤6：访问新添加的图片
为了进一步操作图片，您需要访问其属性：
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
通过这种方式，您可以访问我们刚刚添加的图像的属性！
## 步骤7：设置图片的绝对定位
要绝对定位图片（以像素为单位），您需要使用 `Left` 和 `Top` 属性。在这里，您可以控制图像的显示位置：
```csharp
picture.Left = 60;
picture.Top = 10;
```
您可以根据需要调整这两个值；它们分别代表图像的水平和垂直定位。
## 步骤8：保存Excel文件
最后，完成所有修改后，就可以保存工作簿了：
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
这将创建一个名为 `book1.out.xls` 在您之前定义的文档目录中，包含绝对放置图片的工作表。

## 结论
就这样！您已经成功使用 Aspose.Cells for .NET 将图片以绝对定位方式放置在 Excel 工作表中。这个简单的过程不仅增强了 Excel 文档的视觉呈现效果，还能确保图片始终位于您想要的位置——无论单元格大小和行高如何变化。现在，无论您是在准备报告还是创建仪表板，都可以确保图片每次都处于完美位置。
## 常见问题解答
### 什么是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一个 .NET 库，它使开发人员能够以编程方式创建、操作和转换 Excel 电子表格，而无需 Microsoft Excel。
### 我可以使用 Aspose.Cells 执行其他图像处理吗？
是的，除了定位之外，您还可以使用 Aspose.Cells 库在 Excel 电子表格中调整大小、旋转和修改图像。
### Aspose.Cells 可以免费使用吗？
Aspose.Cells 是一款商业产品，但你可以先从其网站上的免费试用版开始。 [免费试用页面](https://releases。aspose.com/).
### 如何获得 Aspose.Cells 的临时许可证？
您可以通过 [临时执照页面](https://purchase.aspose.com/temporary-license/) 由 Aspose 提供。
### 在哪里可以找到更多示例和文档？
这 [Aspose.Cells 文档](https://reference.aspose.com/cells/net/) 包含丰富的资源，包括代码示例和更详细的功能。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}