---
title: 将工作簿保存为文本 CSV 格式
linktitle: 将工作簿保存为文本 CSV 格式
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过这个专为.NET 开发人员设计的全面的分步教程，了解如何使用 Aspose.Cells 轻松地将 Excel 工作簿转换为 CSV 格式。
weight: 17
url: /zh/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将工作簿保存为文本 CSV 格式

## 介绍
处理数据时，您选择的格式确实可以决定您处理数据的难易程度。处理表格数据的最常见格式之一是 CSV（逗号分隔值）。如果您是使用 Excel 文件的开发人员，并且需要将工作簿转换为 CSV 格式，Aspose.Cells for .NET 是一个很棒的库，可以简化此任务。在本教程中，我们将分解将 Excel 工作簿无缝转换为文本 CSV 格式的步骤。
## 先决条件
在深入研究之前，请确保您已准备好开始的一切：
1. C# 和 .NET 的基础知识：由于我们将用 C# 编写代码，因此熟悉该语言和 .NET 框架至关重要。
2. Aspose.Cells 库：确保您的开发环境中安装了 Aspose.Cells for .NET 库。您可以下载它[这里](https://releases.aspose.com/cells/net/).
3. Visual Studio 或任何 C# IDE：您需要一个集成开发环境 (IDE) 来编写和执行代码。Visual Studio 是一个流行的选择。
4. Excel 工作簿：准备一个包含一些数据的示例 Excel 工作簿（例如“book1.xls”）来测试转换。
## 导入包
现在我们已经满足了先决条件，该过程的第一步是导入必要的包。在 C# 项目中，您需要在代码文件顶部包含以下命名空间：
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
这些命名空间将使您能够访问处理 Excel 文件和管理内存流所需的类和方法。
## 步骤 1：定义文档目录的路径
我们流程的第一步是定义文档（Excel 工作簿）的存储位置。这很重要，因为它可以让我们的程序知道在哪里找到需要处理的文件。 
```csharp
//文档目录的路径。
string dataDir = "Your Document Directory";
```
确保更换`"Your Document Directory"`替换为“book1.xls”文件所在的实际路径。这可能是您计算机上的目录或服务器的路径。
## 第 2 步：加载源工作簿
接下来，我们需要加载将转换为 CSV 格式的 Excel 工作簿。
```csharp
//加载源工作簿
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
这`Workbook` Aspose.Cells 库中的类允许操作和访问 Excel 工作簿。通过传递文件路径，我们可以加载指定的工作簿进行处理。
## 步骤 3：初始化工作簿数据的字节数组
在开始将工作簿转换为 CSV 之前，我们需要初始化一个空字节数组，该数组最终将保存所有工作表数据。
```csharp
// 0 字节数组
byte[] workbookData = new byte[0];
```
这个字节数组将把每个工作表的数据合并为一个单一结构，我们稍后可以将其写入文件。
## 步骤 4：设置文本保存选项
现在，让我们设置如何保存文本格式的选项。您可以选择自定义分隔符或使用制表符。
```csharp
//文本保存选项。您可以使用任何类型的分隔符
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; //将制表符设置为分隔符
```
在此示例中，我们使用制表符作为分隔符。您可以替换`'\t'`任意字符，例如逗号 (`,`)，具体取决于您希望 CSV 如何格式化。
## 步骤 5：遍历每个工作表
接下来，我们将遍历工作簿中的所有工作表，并将每个工作表保存到我们的`workbookData`数组，但您必须首先选择要处理的工作表。
```csharp
//以文本格式复制工作簿数据数组内的每个工作表数据
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    //将活动工作表保存为文本格式
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
循环遍历工作簿中的每个工作表。`ActiveSheetIndex`设置为每次循环时，我们都会保存当前工作表。结果将使用`MemoryStream`.
## 步骤 6：检索工作表数据
将工作表保存到内存流后，下一步是检索此数据并将其附加到我们的`workbookData`大批。
```csharp
    //将工作表数据保存到工作表数据数组中
    ms.Position = 0; //内存流的重置位置
    byte[] sheetData = ms.ToArray(); //获取字节数组
```
`ms.Position = 0;`写入后重置读取位置。然后我们使用`ToArray()`将内存流转换为保存工作表数据的字节数组。
## 步骤 7：合并工作表数据
现在，我们将每个工作表中的数据合并到单个`workbookData`数组已预先初始化。
```csharp
    //将此工作表数据合并到工作簿数据数组中
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
我们创建一个足够大的新数组，以容纳现有工作簿数据和新工作表数据。然后，我们将现有数据和新数据复制到这个组合数组中，以供日后使用。
## 步骤 8：将整个工作簿数据保存到文件中
最后，将所有数据整合到我们的`workbookData`数组，我们可以将这个数组保存到指定的文件路径下。
```csharp
//将整个工作簿数据保存到文件中
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes`获取组合的字节数组并将其写入指定目录中名为“out.txt”的文本文件。
## 结论
就这样！您已成功使用 Aspose.Cells for .NET 将 Excel 工作簿转换为 CSV 格式。此过程不仅高效，而且可以轻松操作 Excel 数据以进行进一步分析或报告。现在您可以自动执行数据处理任务，甚至可以将此功能集成到更大的应用程序中。
## 常见问题解答
### 我可以对 CSV 文件使用不同的分隔符吗？
是的，你可以更改`opts.Separator`为您想要的任何字符，例如逗号或竖线。
### Aspose.Cells 可以免费使用吗？
 Aspose.Cells 不是免费的，但你可以免费试用[这里](https://releases.aspose.com/).
### 除了 CSV 之外，我还可以保存为哪些格式？
Aspose.Cells 允许保存为多种格式，包括XLSX、PDF等。
### 我可以使用 Aspose.Cells 处理大型 Excel 文件吗？
是的，Aspose.Cells 旨在有效处理大文件，但性能可能取决于系统资源。
### 在哪里可以找到更详细的文档？
您可以在其上找到全面的文档和示例[参考网站](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
