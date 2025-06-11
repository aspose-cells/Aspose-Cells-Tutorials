---
"description": "学习如何使用 Aspose.Cells for .NET 自定义显示格式。使用本分步指南格式化日期、百分比和货币。"
"linktitle": "使用用户定义数字自定义显示格式"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "使用用户定义数字自定义显示格式"
"url": "/zh/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用用户定义数字自定义显示格式

## 介绍
使用 Excel 文件通常需要自定义单元格格式，以便以更有意义且用户友好的方式呈现数据。想象一下，您正在为报告构建一个 Excel 文件。您不仅需要原始数字，还希望日期、百分比和货币看起来更美观、更专业，对吗？这就是自定义显示格式发挥作用的地方。在本教程中，我们将深入探讨 Aspose.Cells for .NET，向您展示如何使用用户自定义设置来自定义数字的显示格式。
## 先决条件
在开始之前，请确保您已准备好本教程所需的一切。您需要准备以下材料：
- 已安装 Aspose.Cells for .NET。 [点击此处下载](https://releases。aspose.com/cells/net/).
- C# 和 .NET 框架的基本知识。
- 拥有 Aspose.Cells 的有效许可证。如果您还没有，请获取 [免费试用](https://releases.aspose.com/) 或请求 [临时执照](https://purchase。aspose.com/temporary-license/).
- 类似 Visual Studio 的 IDE。
- .NET Framework 4.0 或更高版本。
如果您缺少任何内容，请不要担心。您可以随时重新访问这些链接下载必要的文件，或向 [Aspose 支持论坛](https://forum。aspose.com/c/cells/9).
## 导入命名空间
在进入代码之前，您需要导入所需的命名空间以访问所有必要的 Aspose.Cells 功能。
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
这两个命名空间将成为本教程的核心工具。现在，让我们进入有趣的部分：
## 步骤 1：设置项目目录
首先，你需要一个地方来存储你的文件，对吧？让我们创建一个目录来保存输出的 Excel 文件。在此步骤中，我们还将确保在保存任何内容之前该目录存在。
```csharp
// 文档目录的路径。
string dataDir = "Your Document Directory";
// 如果目录尚不存在，则创建该目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- 我们正在定义一个 `dataDir` 变量来存储输出 Excel 文件的路径。
- 然后我们使用以下方法检查目录是否存在 `System。IO.Directory.Exists()`.
- 如果目录不存在，则将使用 `System。IO.Directory.CreateDirectory()`.
## 步骤 2：创建新工作簿并添加工作表
现在我们已经有了目录，让我们创建一个新的 Excel 工作簿并向其中添加一个工作表。
```csharp
// 实例化 Workbook 对象
Workbook workbook = new Workbook();
// 向 Excel 对象添加新工作表
int i = workbook.Worksheets.Add();
// 通过传递工作表索引来获取新添加工作表的引用
Worksheet worksheet = workbook.Worksheets[i];
```
- 首先，我们创建一个新的 `Workbook` 对象。可以将其视为您的 Excel 文件。
- 我们使用 `Add()` 方法并将索引存储在变量中 `i`。
- 我们使用 `workbook。Worksheets[i]`.
## 步骤3：向单元格添加日期并自定义其格式
现在，让我们将当前日期插入单元格，并将其格式化为自定义显示方式。我们将设置自定义格式，而不是默认日期格式，例如 `d-mmm-yy`。
```csharp
// 将当前系统日期添加到“A1”单元格
worksheet.Cells["A1"].PutValue(DateTime.Now);
// 获取A1单元格的样式
Style style = worksheet.Cells["A1"].GetStyle();
// 设置自定义显示格式以将日期显示为“d-mmm-yy”
style.Custom = "d-mmm-yy";
// 将样式应用于 A1 单元格
worksheet.Cells["A1"].SetStyle(style);
```
- 我们将当前系统日期添加到单元格 `A1` 使用 `PutValue(DateTime。Now)`.
- 我们检索单元格的当前样式 `A1` 使用 `GetStyle()`。
- 我们通过设置来修改单元格的样式 `style.Custom = "d-mmm-yy"`，将日期格式化为显示星期、缩写的月份和年份。
- 最后，我们将新样式应用到单元格 `SetStyle()`。
## 步骤 4：将单元格格式化为百分比
接下来，我们来处理数字。我们将向另一个单元格添加一个数值，例如 `A2`，并将其格式化为百分比。
```csharp
// 向“A2”单元格添加数值
worksheet.Cells["A2"].PutValue(20);
// 获取A2单元格的样式
style = worksheet.Cells["A2"].GetStyle();
// 设置自定义显示格式以百分比显示值
style.Custom = "0.0%";
// 将样式应用于 A2 单元格
worksheet.Cells["A2"].SetStyle(style);
```
- 我们增加价值 `20` 到单元格 `A2`。
- 我们检索单元格的样式 `A2` 并将自定义格式设置为 `0.0%` 以百分比显示该值（例如 20%）。
- 最后，我们将样式应用到单元格 `SetStyle()`。
## 步骤 5：将单元格格式化为货币
让我们添加另一个值，比如单元格 `A3`，并将其格式化为货币显示。为了使事情更有趣，我们将使用一种格式，将正值显示为英镑货币，将负值显示为美元货币。
```csharp
// 向“A3”单元格添加数值
worksheet.Cells["A3"].PutValue(2546);
// 获取A3单元格的样式
style = worksheet.Cells["A3"].GetStyle();
// 设置自定义显示格式以货币形式显示值
style.Custom = "£#,##0;[Red]$-#,##0";
// 将样式应用于 A3 单元格
worksheet.Cells["A3"].SetStyle(style);
```
- 我们增加价值 `2546` 到单元格 `A3`。
- 我们设置了自定义格式 `£#,##0;[Red]$-#,##0`，其中正值用英镑符号显示，负值用红色美元符号显示。
- 我们将样式应用到单元格 `SetStyle()`。
## 步骤 6：保存工作簿
最后一步是将工作簿保存为 Excel 文件。本教程将使用 Excel 97-2003 格式。
```csharp
// 保存 Excel 文件
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
- 这 `Save()` 方法将工作簿保存在指定的目录中。
- 我们选择 `SaveFormat.Excel97To2003` 以确保与旧版本 Excel 的兼容性。
## 结论
就是这样！我们刚刚创建了一个 Excel 文件，使用 Aspose.Cells for .NET 为特定单元格添加了自定义日期、百分比和货币格式，然后保存了文件。自定义格式使您的 Excel 文件更具可读性和专业性。别忘了探索 Aspose.Cells 中的其他格式选项，例如条件格式，以便更好地控制数据的显示方式。
## 常见问题解答
### 如何在 Aspose.Cells 中应用更复杂的格式选项？
您可以将不同的格式样式（例如字体颜色、边框和背景颜色）与自定义数字格式相结合。
### 我可以将自定义数字格式应用于单元格区域吗？
是的，Aspose.Cells 允许您使用 `Range.SetStyle()` 方法。
### 我可以使用哪些其他文件格式保存工作簿？
Aspose.Cells 支持多种格式，包括 XLSX、CSV 和 PDF。只需将 `SaveFormat` 在 `Save()` 方法。
### 我可以使用不同的格式来格式化负数吗？
当然！您可以使用自定义数字格式，用不同的颜色或符号显示负数。
### Aspose.Cells for .NET 免费吗？
Aspose.Cells 提供免费试用，但要获得完整功能，您需要有效的许可证。您可以获取 [此处为临时驾照](https://purchase。aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}