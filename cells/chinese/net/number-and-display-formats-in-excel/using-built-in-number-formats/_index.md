---
"description": "使用 Aspose.Cells for .NET 自动设置 Excel 中的数字格式。了解如何以编程方式应用日期、百分比和货币格式。"
"linktitle": "以编程方式使用 Excel 中的内置数字格式"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "以编程方式使用 Excel 中的内置数字格式"
"url": "/zh/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 以编程方式使用 Excel 中的内置数字格式

## 介绍
在本教程中，我们将指导您如何使用 Aspose.Cells for .NET 在 Excel 中使用内置数字格式。我们将涵盖从设置环境到应用日期、百分比和货币等不同格式的所有内容。无论您是经验丰富的专业人士，还是初入 .NET 生态系统的新手，本指南都能帮助您轻松设置 Excel 单元格格式。
## 先决条件
在深入研究之前，请确保您已具备以下条件：
- 已安装 Aspose.Cells for .NET 库。您可以 [点击此处下载](https://releases。aspose.com/cells/net/).
- 具备 C# 和基本 .NET 编程的工作知识。
- 您的机器上安装了 Visual Studio 或任何 .NET IDE。
- 有效的 Aspose 许可证或 [临时执照](https://purchase。aspose.com/temporary-license/).
- 安装了.NET框架（4.0或更高版本）。
  
如果您缺少以上任何一项，请按照提供的链接进行设置。准备好了吗？让我们进入精彩的部分！
## 导入包
在开始本教程之前，请确保导入使用 Aspose.Cells for .NET 所需的命名空间：
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
导入这些文件后，您就可以以编程方式操作 Excel 文件了。现在，让我们深入了解分步指南！
## 步骤 1：创建或访问您的 Excel 工作簿
在此步骤中，您将创建一个新的工作簿。您可以将其想象为打开一个新的 Excel 文件，只不过您是通过代码来执行的！
```csharp
// 文档目录的路径。
string dataDir = "Your Document Directory";
// 如果目录尚不存在，则创建该目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// 实例化 Workbook 对象
Workbook workbook = new Workbook();
```
这里我们只是实例化了一个新的 `Workbook` 对象。它将充当您的 Excel 文件，可供数据操作。您也可以通过提供其路径来加载现有文件。
## 第 2 步：访问工作表
Excel 工作簿可以包含多个工作表。在此步骤中，我们将访问工作簿中的第一个工作表：
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
我们现在正在访问工作簿中的第一个工作表。如果需要操作其他工作表，可以使用它们的索引或名称来引用它们。
## 步骤 3：向单元格添加数据
让我们开始向特定单元格添加一些数据。首先，我们将当前系统日期插入单元格“A1”中：
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
这行代码将当前日期插入到单元格 A1 中。很酷吧？想象一下，手动操作数百个单元格——那将是一场噩梦。现在，我们继续进行格式化！
## 步骤 4：在单元格“A1”中设置日期格式
接下来，让我们将该日期格式化为更易读的格式，例如“15-Oct-24”。这正是 Aspose.Cells 的亮点所在：
1. 检索单元格的样式：
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
这里，我们抓取的是单元格 A1 的样式。可以将其理解为在进行任何调整之前，先抓取单元格的“风格”。
2.设置日期格式：
```csharp
style.Number = 15;
```
设置 `Number` 属性设置为 15 即可应用所需的日期格式。这是一个内置的数字格式代码，用于以“d-mmm-yy”格式显示日期。
3. 将样式应用于单元格：
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
这行代码将样式更改应用于单元格。现在，您将看到更加用户友好的日期格式，而不是默认的日期格式，例如“15-Oct-24”。
## 步骤 5：在单元格“A2”中添加并设置百分比格式
我们继续学习设置百分比格式。假设您想插入一个值并将其显示为百分比。在此步骤中，我们将向单元格“A2”添加一个数值，并将其格式化为百分比：
1. 插入数值：
```csharp
worksheet.Cells["A2"].PutValue(20);
```
这会将数字 20 插入到单元格 A2 中。您可能会想：“这只是一个普通的数字——我该如何将其转换为百分比呢？” 好吧，我们马上就会讲到。
2. 检索样式并设置百分比格式：
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // 格式为百分比
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
这里，我们将 2546 添加到单元格 A3。接下来，我们将设置此数字的格式，使其显示为货币。
2. 检索样式并设置货币格式：
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // 格式化为货币
worksheet.Cells["A3"].SetStyle(style);
```
设置 `Number` 属性设置为 6 时，将应用货币格式。现在，单元格 A3 中的值将显示为“2,546.00”，包含逗号和两位小数。
## 步骤 7：保存 Excel 文件
现在我们已经应用了所有的格式化魔法，是时候保存文件了：
```csharp
// 保存 Excel 文件
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
此行将 Excel 文件保存为 Excel 97-2003 格式。您可以更改 `SaveFormat` 满足您的需求。就这样，您就以编程方式创建并格式化了一个 Excel 文件！
## 结论
恭喜！您已成功学习如何使用 Aspose.Cells for .NET 将内置数字格式应用于 Excel 文件中的单元格。从日期到百分比和货币，我们涵盖了 Excel 数据处理中一些最常见的格式需求。现在，您无需手动格式化单元格，而是可以自动化整个过程，从而节省时间并减少错误。
## 常见问题解答
### 我可以使用 Aspose.Cells for .NET 应用自定义数字格式吗？
是的！除了内置格式外，Aspose.Cells 还支持自定义数字格式。您可以使用 `Custom` 财产 `Style` 班级。
### 如何将单元格格式化为具有特定符号的货币？
要应用特定的货币符号，您可以通过设置 `Style.Custom` 财产。
### 我可以格式化整行或整列吗？
当然！您可以使用 `Rows` 或者 `Columns` 收藏品 `Worksheet` 目的。
### 如何一次性格式化多个单元格？
您可以使用 `Range` 对象来选择多个单元格并一次性将样式应用于它们。
### 我需要安装 Microsoft Excel 才能使用 Aspose.Cells 吗？
不，Aspose.Cells 独立于 Microsoft Excel 运行，因此您不需要在机器上安装 Excel。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}