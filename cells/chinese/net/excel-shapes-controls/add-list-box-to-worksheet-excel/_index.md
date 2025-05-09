---
"description": "了解如何使用 Aspose.Cells for .NET 将列表框添加到 Excel 工作表。按照我们简单易懂的分步指南，让您的 Excel 工作表实现交互。"
"linktitle": "在 Excel 中将列表框添加到工作表"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 Excel 中将列表框添加到工作表"
"url": "/zh/net/excel-shapes-controls/add-list-box-to-worksheet-excel/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中将列表框添加到工作表

## 介绍
在 Excel 工作表中添加列表框等交互式元素可以显著提升数据管理和呈现效果。无论您是创建交互式表单还是自定义数据输入工具，使用列表框控制用户输入的能力都至关重要。Aspose.Cells for .NET 提供了一种在 Excel 文件中添加和管理这些控件的有效方法。在本指南中，我们将引导您完成使用 Aspose.Cells for .NET 向工作表添加列表框的过程。
## 先决条件
在深入编码之前，请确保您已准备好以下工具和资源：
- Aspose.Cells for .NET Library：您可以从 [Aspose.Cells for .NET下载页面](https://releases。aspose.com/cells/net/).
- 开发环境：任何支持.NET开发的IDE，例如Visual Studio。
- .NET Framework：确保您的项目针对的是受支持的 .NET 框架版本。
另外，考虑购买 [临时执照](https://purchase.aspose.com/temporary-license/) 如果您想不受限制地探索所有功能。
## 导入包
在开始之前，请确保已导入必要的 Aspose.Cells 命名空间。操作方法如下：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
在本教程中，我们将把添加列表框的过程分解为几个简单的步骤。请仔细遵循每个步骤，确保一切按预期运行。
## 步骤 1：设置文档目录
在创建任何 Excel 文件之前，您需要一个保存位置。设置目录的方法如下：
```csharp
// 文档目录的路径。
string dataDir = "Your Document Directory";
// 如果目录不存在，则创建目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
在此步骤中，您将定义文件的存储位置。代码会检查目录是否存在，如果不存在，则会为您创建一个。这可确保您以后不会遇到任何“文件未找到”错误。
## 步骤 2：创建新工作簿并访问第一个工作表
接下来，我们将创建一个新的工作簿并访问我们将添加列表框的第一个工作表。
```csharp
// 创建一个新的工作簿。
Workbook workbook = new Workbook();
// 获取第一张工作表。
Worksheet sheet = workbook.Worksheets[0];
```
工作簿本质上就是你的 Excel 文件。在这里，我们创建一个新的工作簿并访问第一个工作表，我们将在其中放置列表框。你可以将其想象成创建一个空白画布，用于绘制控件。
## 步骤3：输入列表框的数据
在添加列表框之前，我们需要填充列表框将引用的一些数据。
```csharp
// 获取工作表单元格集合。
Cells cells = sheet.Cells;
// 输入标签的值。
cells["B3"].PutValue("Choose Dept:");
// 将标签设置为粗体。
cells["B3"].GetStyle().Font.IsBold = true;
// 列表框的输入值。
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
这里，我们在工作表中添加了一些文本。标签“选择部门：”位于单元格 B3 中，字体设置为粗体。在 A 列中，我们插入了一些值，这些值将作为列表框的输入范围，代表不同的部门。用户在与列表框交互时将从此输入范围中进行选择。
## 步骤 4：将列表框添加到工作表
现在我们已经设置了数据，让我们添加列表框控件本身。
```csharp
// 添加一个新的列表框。
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
此代码将列表框添加到工作表中。参数定义列表框的位置和大小。列表框位于第 2 行、第 0 列，宽度为 122，高度为 100。这些坐标和大小决定了列表框在工作表中的显示位置。
## 步骤 5：设置列表框属性
接下来，我们将设置列表框的各种属性，以使其完全发挥作用。
```csharp
// 设置放置类型。
listBox.Placement = PlacementType.FreeFloating;
// 设置链接的单元格。
listBox.LinkedCell = "A1";
// 设定输入范围。
listBox.InputRange = "A2:A7";
// 设置选择类型。
listBox.SelectionType = SelectionType.Single;
// 设置具有 3-D 阴影的列表框。
listBox.Shadow = true;
```
- PlacementType.FreeFloating：此属性确保无论如何修改工作表，列表框都保持在其位置。
- LinkedCell：设置一个单元格（在本例中为 A1），其中将显示从列表框中选择的值。
- InputRange：这告诉列表框在哪里查找其选项列表（A2 到 A7，我们之前设置）。
- SelectionType.Single：这限制用户只能从列表框中选择一个项目。
- 阴影：阴影效果使列表框看起来更加立体，更具视觉吸引力。
## 步骤6：保存Excel文件
最后，让我们保存包含列表框的工作簿。
```csharp
// 保存工作簿。
workbook.Save(dataDir + "book1.out.xls");
```
这行代码将工作簿保存到我们之前设置的目录中。文件名为“book1.out.xls”，但您可以选择任何适合您项目的名称。
## 结论
就这样！您已经成功使用 Aspose.Cells for .NET 将列表框添加到 Excel 工作表中。只需几行代码，我们就创建了一个功能齐全的列表框，使工作表更具交互性和动态性。本教程将为您奠定坚实的基础，以探索 Aspose.Cells for .NET 中的其他控件和功能。继续尝试，很快您就能掌握该库的丰富功能！
## 常见问题解答
### 我可以允许列表框中的多项选择吗？  
是的，你可以更改 `SelectionType` 到 `SelectionType.Multi` 以允许多项选择。
### 我可以改变列表框的外观吗？  
当然！Aspose.Cells 允许您自定义列表框的外观，包括其大小、字体甚至颜色。
### 如果我稍后需要删除列表框怎么办？  
您可以从 `Shapes` 收集使用 `sheet。Shapes.RemoveAt(index)`.
### 我可以将列表框链接到不同的单元格吗？  
是的，只需更改 `LinkedCell` 属性到您想要显示所选值的任何其他单元格。
### 如何向列表框添加更多项目？  
只需通过在指定单元格中插入更多值来更新输入范围，列表框就会自动更新。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}