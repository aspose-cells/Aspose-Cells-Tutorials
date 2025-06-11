---
"description": "学习如何使用 Aspose.Cells for .NET 将 HTML 加载到 Excel 中时自动调整行和列。内含分步指南。"
"linktitle": "在工作簿中加载 HTML 时自动调整列和行"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在工作簿中加载 HTML 时自动调整列和行"
"url": "/zh/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在工作簿中加载 HTML 时自动调整列和行

## 介绍
您是否想过如何在使用 Aspose.Cells for .NET 将 HTML 内容加载到 Excel 工作簿时自动调整行列大小？没错，您来对地方了！在本教程中，我们将深入讲解如何将 HTML 表格加载到工作簿中，并确保行列自动调整以匹配内容。如果您处理的是频繁变化的动态数据，本指南将是您从 HTML 创建格式良好的 Excel 工作表的首选。
### 先决条件
在开始编写代码之前，您需要在系统上进行一些设置。不用担心，步骤简单明了！
1. 已安装 Visual Studio：您需要 Visual Studio 或任何其他 .NET 开发环境。
2. Aspose.Cells for .NET：您可以 [下载最新版本](https://releases.aspose.com/cells/net/) 或使用 NuGet 包管理器来安装它。
3. .NET Framework：确保您已安装 .NET Framework 4.0 或更高版本。
4. 对 C# 的基本了解：对 C# 有一些了解将使本教程对您来说更加顺利。
5. HTML 表格数据：准备一些您想要加载到 Excel 中的 HTML 内容（甚至是基本表格）。
## 导入包
首先，让我们导入必要的命名空间。以下是需要导入的内容的简单列表：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
这些包允许您处理工作簿、操作 HTML 数据并将其无缝加载到 Excel 中。
我们将这个过程分解成几个易于理解的部分，以便您轻松跟进。完成后，您将获得一个实际示例，了解如何使用 Aspose.Cells for .NET 将 HTML 加载到工作簿时自动调整行和列。
## 步骤 1：设置文档目录
为了方便保存和检索文件，我们将指定文档的存储路径。您可以将目录路径替换为您自己的文件夹位置。
```csharp
string dataDir = "Your Document Directory";
```
这行代码设置了 Excel 文件的保存目录。在处理多个项目时，妥善组织文件至关重要。想象一下，这就像你项目的文件柜！
## 步骤 2：将 HTML 数据创建为字符串
接下来，我们将定义一些基本的 HTML 内容。为了便于示例，我们将使用一个简单的 HTML 表格。您可以根据项目需求进行自定义。
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
我们在这里定义了一个非常基本的 HTML 字符串。它包含一个包含几行几列的表格。您可以根据需要添加更多行或列。就像做饭前准备食材一样！
## 步骤3：将HTML字符串加载到MemoryStream中
现在我们已经准备好 HTML 内容，下一步是使用 `MemoryStream`。这使我们能够在内存中操作 HTML 内容，而无需先将其保存到磁盘。
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
通过将 HTML 字符串转换为字节数组并将其输入到 `MemoryStream`，我们可以在内存中处理 HTML 数据。想象一下，这一步就像在锅里准备菜肴，然后放进烤箱一样！
## 步骤 4：将 MemoryStream 加载到工作簿中（不自动调整）
一旦我们将 HTML 内容放入内存中，我们就会将其加载到 Aspose `Workbook`目前，我们还没有自动调整行和列。这是我们的“之前”场景，稍后会与自动调整后的版本进行比较。
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
工作簿已加载 HTML 内容，但行和列尚未自动调整到与文本匹配的大小。这就好比烤蛋糕时忘记检查温度——虽然可以烤，但可能不够完美！
## 步骤 5：启用自动调整功能，指定 HTML 加载选项
现在，魔法来了！我们创建一个 `HtmlLoadOptions` 并启用 `AutoFitColsAndRows` 属性。这可确保在加载 HTML 内容时，列和行会进行调整以适应其中的内容。
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
通过设置此选项，我们将告诉 Aspose.Cells 自动调整行和列的大小。想象一下，这就像将烤箱设置为理想的温度，让蛋糕恰到好处地膨胀！
## 步骤 6：将 HTML 加载到工作簿中并启用自动调整
现在我们再次加载 HTML 内容，但这次使用 `AutoFitColsAndRows` 选项已启用。这将根据列宽和行高调整列宽和行高。
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
此步骤会将 HTML 内容加载到新的工作簿中，并将其保存为 Excel 文件，但现在列和行已自动调整大小！就像烤好的蛋糕一样，所有元素都大小合适。
## 结论
通过这些简单的步骤，您学会了如何使用 Aspose.Cells for .NET 将 HTML 内容加载到工作簿中，并自动调整行和列。无论内容如何变化，这都能确保您的 Excel 工作表始终保持整洁。这是一个简单而强大的功能，可以为您节省大量格式化和组织 Excel 数据的时间。
现在您已经掌握了这些知识，您可以尝试更复杂的 HTML 内容，添加样式，甚至从网页创建整个 Excel 工作簿！
## 常见问题解答
### 我可以使用此方法来加载大型 HTML 表格吗？
是的，Aspose.Cells 可以有效地处理大型 HTML 表，但为了获得最佳性能，建议使用您的数据大小进行测试。
### 自动调整后我可以手动应用特定的列宽和行高吗？
当然！即使使用自动调整功能后，您仍然可以自定义单个列和行。
### 加载 HTML 后如何设置表格样式？
加载 HTML 后，您可以使用 Aspose.Cells 的广泛样式选项应用样式。
### Aspose.Cells for .NET 是否与旧版本的 .NET Framework 兼容？
是的，Aspose.Cells for .NET 支持 .NET Framework 4.0 及更高版本。
### 我可以使用 Aspose.Cells 将 HTML 以外的其他类型的内容加载到 Excel 中吗？
是的，Aspose.Cells 支持将各种格式（如 CSV、JSON 和 XML）加载到 Excel 中。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}