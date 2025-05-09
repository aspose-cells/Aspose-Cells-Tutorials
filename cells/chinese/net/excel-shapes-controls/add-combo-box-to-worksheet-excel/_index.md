---
"description": "学习如何使用 Aspose.Cells for .NET 以编程方式将组合框添加到 Excel 工作表。本分步指南将引导您了解每个细节。"
"linktitle": "在 Excel 中将组合框添加到工作表"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 Excel 中将组合框添加到工作表"
"url": "/zh/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中将组合框添加到工作表

## 介绍
创建交互式 Excel 电子表格可以极大地提升用户体验，尤其是在添加组合框等表单元素时。组合框允许用户从预定义列表中选择选项，从而简化数据输入并提高效率。使用 Aspose.Cells for .NET，您可以以编程方式在 Excel 工作表中创建组合框，而无需直接使用 Excel。这个强大的库允许开发人员以各种方式操作 Excel 文件，包括自动化表单控件。
在本教程中，我们将指导您使用 Aspose.Cells for .NET 在 Excel 工作表中添加组合框。如果您正在尝试构建动态且用户友好的电子表格，本指南将帮助您入门。
## 先决条件
在深入研究代码之前，请确保您拥有所需的一切：
- Aspose.Cells for .NET：从下载并安装 Aspose.Cells for .NET 库 [下载页面](https://releases。aspose.com/cells/net/).
- .NET Framework：确保您的计算机上已安装 .NET Framework。Aspose.Cells 支持的任何版本均可使用。
- 开发环境：使用 Visual Studio 等 IDE 来管理您的项目并编写代码。
- Aspose 许可证：在评估模式下，您无需许可证即可使用，但要使用完整版本，则需要申请许可证。获取 [临时执照](https://purchase.aspose.com/temporary-license/) 如果需要的话。
## 导入包
首先，您需要将所需的命名空间导入到项目中。您需要的内容如下：
```csharp
using System.IO;
using Aspose.Cells;
```
这些对于与 Excel 文件交互以及操作工作簿中的组合框等表单元素至关重要。
为了便于理解，我们将添加组合框的过程分解为多个简单的步骤。
## 步骤 1：设置文档目录
第一步是创建一个用于保存 Excel 文件的目录。如果文件夹尚不存在，可以创建一个。
```csharp
// 文档目录的路径。
string dataDir = "Your Document Directory";
// 如果目录尚不存在，则创建该目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir：指定输出文件的保存位置。
- System.IO.Directory.Exists：检查目录是否已存在。
- System.IO.Directory.CreateDirectory：如果目录缺失，则创建目录。
## 步骤 2：创建新工作簿
现在，创建一个新的 Excel 工作簿，您将在其中添加组合框。

```csharp
// 创建一个新的工作簿。
Workbook workbook = new Workbook();
```

- 工作簿workbook：初始化Workbook类的一个新实例，代表一个Excel文件。
## 步骤 3：获取工作表和单元格
接下来，从工作簿访问第一个工作表并检索将输入数据的单元格集合。

```csharp
// 获取第一张工作表。
Worksheet sheet = workbook.Worksheets[0];
// 获取工作表单元格集合。
Cells cells = sheet.Cells;
```

- 工作表 sheet：从工作簿中获取第一个工作表。
- Cells cells：从工作表中获取单元格集合。
## 步骤 4：组合框的输入值
现在，我们需要在单元格中输入一些值。这些值将作为组合框的选项。

```csharp
// 输入一个值。
cells["B3"].PutValue("Employee:");
// 将其设置为粗体。
cells["B3"].GetStyle().Font.IsBold = true;
// 输入一些表示组合框输入范围的值。
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- cells["B3"].PutValue：将标签“Employee”放置在单元格 B3 中。
- Font.IsBold = true：将文本设置为粗体以使其突出显示。
- 输入范围：在单元格 A2 至 A7 中输入多个员工 ID。这些 ID 将显示在组合框下拉列表中。
## 步骤 5：将组合框添加到工作表
下一步是将组合框控件添加到工作表。此组合框将允许用户从您之前输入的员工 ID 中选择一个。

```csharp
// 添加一个新的组合框。
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox：向工作表添加一个新的组合框。数字 (2, 0, 2, 0, 22, 100) 代表组合框的位置和尺寸。
## 步骤 6：将组合框链接到单元格并设置输入范围
为了使组合框发挥作用，我们需要将其链接到特定的单元格并定义它将从中提取选项的单元格范围。

```csharp
// 设置链接的单元格。
comboBox.LinkedCell = "A1";
// 设定输入范围。
comboBox.InputRange = "A2:A7";
```

- LinkedCell：将组合框的选定内容链接到单元格 A1。组合框中选定的值将显示在此单元格中。
- InputRange：定义包含将填充组合框选项的值的单元格范围（A2：A7）。
## 步骤 7：自定义组合框外观
您可以通过指定下拉线的数量并启用 3D 阴影来进一步自定义组合框，以获得更好的美感。

```csharp
// 设置组合框列表部分显示的列表行数。
comboBox.DropDownLines = 5;
// 使用 3-D 阴影设置组合框。
comboBox.Shadow = true;
```

- DropDownLines：控制组合框下拉菜单中一次可见的选项数。
- 阴影：为组合框添加 3D 阴影效果。
## 步骤 8：自动调整列并保存工作簿
最后，让我们自动调整列以获得整洁的布局并保存工作簿。

```csharp
// 自动调整列
sheet.AutoFitColumns();
// 保存文件。
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns：自动调整列宽以适合内容。
- 保存：将工作簿作为 Excel 文件保存在指定目录中。

## 结论
使用 Aspose.Cells for .NET 向 Excel 工作表添加组合框非常简单，可以显著提高数据输入的灵活性。通过以编程方式创建表单控件，您可以轻松构建交互式电子表格。本教程向您展示了如何使用 Aspose.Cells 添加组合框、将其链接到单元格以及配置其输入范围。
Aspose.Cells 提供了丰富的 Excel 文件操作功能，是希望自动化电子表格任务的开发人员的理想之选。 [免费试用](https://releases。aspose.com/).
## 常见问题解答
### 我可以在没有安装 Excel 的情况下使用 Aspose.Cells 吗？
是的，Aspose.Cells 独立于 Excel 工作，不需要安装 Excel。
### 如何在 Aspose.Cells 中申请许可证？
您可以通过以下方式申请许可证 [这里](https://purchase.aspose.com/buy) 并调用 `License.SetLicense()` 在你的代码中。
### Aspose.Cells 支持保存哪些文件格式？
Aspose.Cells 支持以多种格式保存文件，如 XLSX、XLS、CSV、PDF 等。
### 我可以添加的组合框数量有限制吗？
不，没有严格的限制；您可以根据项目需要添加任意数量的组合框。
### 如何获得 Aspose.Cells 的支持？
您可以从 [Aspose 论坛](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}