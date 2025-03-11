---
title: 在 Excel 中创建文本删除线效果
linktitle: 在 Excel 中创建文本删除线效果
second_title: Aspose.Cells .NET Excel 处理 API
description: 在本详细的分步教程中学习如何使用 Aspose.Cells for .NET 在 Excel 中对文本应用删除线效果。
weight: 15
url: /zh/net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中创建文本删除线效果

## 介绍
对于 Excel，视觉元素与数据本身同样重要。无论您是突出显示重要更改还是标记不再相关的项目，文本上的删除线效果都是管理电子表格中视觉表示的经典方法。在本指南中，我们将引导您完成使用 Aspose.Cells for .NET 在 Excel 中对文本实现删除线效果的过程。本教程不仅将介绍必要的先决条件，还将提供分步方法，以确保您可以轻松复制此效果。
## 先决条件
在深入学习本教程之前，请确保您已满足以下先决条件：
1. 开发环境：您应该设置一个 .NET 开发环境。这可以是 Visual Studio 或任何其他您喜欢的支持 .NET 开发的 IDE。
2. Aspose.Cells for .NET：确保您的项目中安装了 Aspose.Cells。您可以从以下链接下载：[下载 Aspose.Cells](https://releases.aspose.com/cells/net/).
3. C# 基础知识：对 C# 编程的基本了解很有帮助，因为示例将用 C# 编码。
4. .NET Framework：确保您的项目针对兼容的 .NET Framework 版本，通常是 .NET Core 或 .NET Framework 4.5 及以上版本。
## 导入包
在编写任何代码之前，您需要从 Aspose.Cells 导入所需的命名空间。这对于访问库提供的各种功能至关重要。以下是导入必要命名空间的方法：
```csharp
using System.IO;
using Aspose.Cells;
```
通过这些导入，您将可以访问本教程中将使用的 Workbook、Worksheet 和 Style 类。
现在我们已经做好了准备，让我们将流程分解为易于管理的步骤。每个步骤都附有清晰的说明，指导您在 Excel 中创建文本删除线效果。
## 步骤 1：定义文档目录
首先定义 Excel 文档的存储路径。这将是保存输出文件的位置。
```csharp
//文档目录的路径。
string dataDir = "Your Document Directory";
```
代替`"Your Document Directory"`替换为要保存 Excel 文件的实际目录路径。这将设置输出目录。
## 第 2 步：创建目录
接下来，您需要确保上一步中指定的目录存在。如果不存在，您可以通过编程方式创建它。
```csharp
//如果目录尚不存在，则创建目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
此代码检查目录是否存在，如果不存在则创建目录。这有助于避免稍后尝试保存文件时出现错误。
## 步骤 3：实例化工作簿对象
现在，是时候创建一个新的 Workbook 对象了。这是 Excel 文件的基础，您将在其中添加数据和应用格式。
```csharp
//实例化 Workbook 对象
Workbook workbook = new Workbook();
```
这`Workbook`类表示一个 Excel 文件。通过创建此类的实例，您实际上是在创建一个新的 Excel 文档。
## 步骤 4：添加新工作表
每个工作簿可以包含多个工作表。让我们继续在工作簿中创建一个新工作表。
```csharp
//向 Excel 对象添加新工作表
int i = workbook.Worksheets.Add();
```
这`Add`方法`Worksheets`集合向工作簿添加新的工作表并返回其索引。 
## 步骤 5：获取新工作表的引用
创建工作表后，您需要引用它以进行将来的操作。
```csharp
//通过传递工作表索引来获取新添加工作表的引用
Worksheet worksheet = workbook.Worksheets[i];
```
在这里，您将使用其索引 (`i`）。这将授予您操作工作表的权限。
## 步骤 6：访问单元格
您需要访问工作表中要应用删除线格式的特定单元格。在此示例中，我们使用单元格`A1`.
```csharp
//从工作表访问“A1”单元格
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
在 Excel 中，单元格通过其列和行标识符来引用（例如“A1”）。我们正在获取对单元格的引用`A1`以进行进一步的操作。
## 步骤 7：向单元格添加值
接下来，让我们在单元格中插入一些文本。我们将在单元格中写入“Hello Aspose！”`A1`.
```csharp
//向“A1”单元格添加一些值
cell.PutValue("Hello Aspose!");
```
这`PutValue`方法用于为单元格分配一个字符串值。您可以将此字符串修改为要显示的任何内容。
## 步骤 8：获取单元格的样式
现在我们的单元格中有了文本，现在是时候访问单元格的样式来应用我们想要的格式，包括删除线效果。
```csharp
//获取单元格的样式
Style style = cell.GetStyle();
```
这`GetStyle`方法检索单元格的当前样式，允许您修改字体类型、大小和效果等属性。
## 步骤 9：设置删除线效果
让我们将删除线效果应用于单元格中的文本。我们将修改单元格的字体样式。
```csharp
//出局:设置三振出局
//设置字体删除线效果
style.Font.IsStrikeout = true;
//ExEnd:设置删除线
```
通过设置`IsStrikeout`为 true，则表示您指示 Excel 在视觉上划掉所选单元格中的文本 - 就像在视觉上标记列表中的某些内容一样。
## 步骤 10：将样式应用于单元格
修改样式后，需要将其应用回单元格以反映更改。
```csharp
//将样式应用于单元格
cell.SetStyle(style);
```
这`SetStyle`方法使用新样式更新单元格，现在包括删除线格式。
## 步骤 11：保存 Excel 文件
最后，是时候将工作簿保存到指定目录了。在此示例中，我们将使用名称保存文件`book1.out.xls`.
```csharp
//保存 Excel 文件
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
这`Save`方法以 97-2003 Excel 格式将工作簿写入磁盘。您可以根据需要指定不同的格式。
## 结论
使用 Aspose.Cells for .NET 在 Excel 中为文本创建删除线效果的过程非常简单，只需一步步分解即可。通过遵循本指南，您现在掌握了使用视觉提示增强电子表格的技能，使您的数据不仅信息丰富，而且具有视觉吸引力。
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的库，用于在.NET 应用程序中管理 Excel 文件，使您能够以编程方式创建、操作和转换 Excel 文档。
### 我可以免费使用 Aspose.Cells 吗？
是的，试用期间您可以免费使用。免费试用版可从以下网址获取：[Aspose.Cells 免费试用](https://releases.aspose.com/).
### 如何购买 Aspose.Cells？
您可以通过其网站购买 Aspose.Cells 的许可证[购买 Aspose.Cells](https://purchase.aspose.com/buy).
### 是否有使用 Aspose.Cells 的示例？
是的，你可以在[Aspose.Cells 文档](https://reference.aspose.com/cells/net/).
### 我可以在哪里获得 Aspose.Cells 的支持？
您可以从以下位置获得社区支持和帮助[Aspose 论坛](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
