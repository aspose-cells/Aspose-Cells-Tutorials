---
"description": "通过本指南，了解如何使用 Aspose.Cells for .NET 在 Excel 中取消行和列的分组。简化您的 Excel 数据操作。"
"linktitle": "使用 Aspose.Cells 在 Excel 中取消行和列的分组"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "使用 Aspose.Cells 在 Excel 中取消行和列的分组"
"url": "/zh/net/row-and-column-management/ungrouping-rows-and-columns/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 在 Excel 中取消行和列的分组

## 介绍
在处理 Excel 文件时，您可能会遇到需要取消行和列分组的情况。无论您是要清理电子表格还是重新格式化数据以获得更好的呈现效果，Aspose.Cells for .NET 都是一款出色的工具，可以简化此过程。在本教程中，我将指导您使用 Aspose.Cells 在 Excel 中取消行和列分组的步骤。到最后，您将对如何以编程方式处理 Excel 文件有一个扎实的理解。
## 先决条件
在深入代码之前，请确保您已完成所有设置。您需要准备以下材料：
1. Visual Studio：你的机器上应该已经安装了 Visual Studio 的可用版本。如果你还没有，可以从 [Visual Studio 的网站](https://visualstudio。microsoft.com/).
2. Aspose.Cells for .NET：您需要下载 Aspose.Cells 库。您可以从 [Aspose 发布页面](https://releases.aspose.com/cells/net/)确保您拥有必要的许可证，这些许可证可以购买或通过 [临时执照](https://purchase。aspose.com/temporary-license/).
3. C# 基础知识：对 C# 编程的基本了解将帮助您更轻松地跟上进度。
一旦一切准备就绪，我们就可以进入有趣的部分：代码！
## 导入包
首先，你需要在 C# 项目中导入必要的包。操作方法如下：
1. 在 Visual Studio 中打开您的项目。
2. 添加对 Aspose.Cells 库的引用。您可以通过右键单击项目中的“引用”，然后选择“添加引用”来完成此操作。浏览到您保存 Aspose.Cells DLL 的位置。
3. 在 C# 文件的顶部，添加以下使用指令：
```csharp
using System.IO;
using Aspose.Cells;
```
现在一切都已设置完毕，让我们逐步了解在 Excel 表中取消分组行和列的步骤。 
## 步骤1：定义文档目录
首先，您需要指定Excel文件所在的目录。您可以按如下方式设置：
```csharp
// 文档目录的路径。
string dataDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 使用计算机上保存 Excel 文件的实际路径。 
## 步骤2：创建文件流
接下来，您需要创建一个文件流来打开Excel文件。具体操作如下：
```csharp
// 创建包含要打开的 Excel 文件的文件流
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
在这里，你打开的是名为 `book1.xls`。请确保此文件存在于您指定的目录中，否则您将遇到文件未找到错误。
## 步骤 3：实例化工作簿对象
现在，让我们将 Excel 文件加载到 Workbook 对象中。这样你就可以通过编程来操作工作簿了：
```csharp
// 实例化 Workbook 对象
// 通过文件流打开Excel文件
Workbook workbook = new Workbook(fstream);
```
通过这行代码，您已成功将 Excel 文件加载到内存中并准备使用它。
## 步骤 4：访问工作表
获得工作簿后，下一步是访问要取消分组行和列的特定工作表。操作方法如下：
```csharp
// 访问 Excel 文件中的第一个工作表
Worksheet worksheet = workbook.Worksheets[0];
```
在本例中，我们访问的是第一个工作表。如果您的数据位于其他工作表，则可以相应地更改索引。
## 步骤 5：取消行分组
现在到了激动人心的部分！让我们取消组合前六行（从第 0 行到第 5 行）。使用以下代码：
```csharp
// 取消分组前六行（从 0 到 5）
worksheet.Cells.UngroupRows(0, 5);
```
此方法将删除已应用于指定行的所有分组。就这么简单！
## 步骤 6：取消列分组
与行一样，您也可以取消列的分组。以下是取消前三列（从第 0 列到第 2 列）分组的方法：
```csharp
// 取消分组前三列（从 0 到 2）
worksheet.Cells.UngroupColumns(0, 2);
```
## 步骤7：保存修改后的Excel文件
取消分组行和列后，下一步是将更改保存回 Excel 文件。您可以使用 `Save` 方法：
```csharp
// 保存修改后的 Excel 文件
workbook.Save(dataDir + "output.xls");
```
在此示例中，我们将修改后的文件保存为 `output.xls`。您可以将文件名更改为您喜欢的任何名称。
## 步骤8：关闭文件流
最后，为了释放资源，您应该关闭文件流：
```csharp
// 关闭文件流以释放所有资源
fstream.Close();
```
这是一个很好的做法，可以确保您的应用程序不会占用文件句柄超过必要的时间。
## 结论
就这样！您已经成功学会了如何使用 Aspose.Cells for .NET 取消 Excel 文件中行和列的分组。只需几行代码，您就可以以编程方式对 Excel 文件进行重大更改。无论您是要自动生成报告还是准备数据进行分析，掌握这些技巧都能为您节省大量时间。
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的库，用于在 .NET 应用程序中处理 Excel 文件，可以轻松操作、转换和创建电子表格。
### 我可以使用其他库取消 Excel 中的行和列的分组吗？
是的，.NET 中还有其他可用于 Excel 操作的库，但 Aspose.Cells 提供了广泛的功能和易用性。
### 保存后有没有办法撤消更改？
一旦保存了 Excel 文件，除非您有原始文件的备份，否则无法恢复到之前的状态。
### 如何获得 Aspose.Cells 的支持？
您可以通过访问以下方式获得支持 [Aspose 支持论坛](https://forum.aspose.com/c/cells/9)，您可以在这里提出问题并找到解决方案。
### 我可以在没有许可证的情况下使用 Aspose.Cells 吗？
是的，您可以免费使用 Aspose.Cells，但有一定的限制，您可以从 [临时执照](https://purchase.aspose.com/temporary-license/) 以实现全部功能。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}