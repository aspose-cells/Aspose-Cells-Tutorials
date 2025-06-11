---
"description": "学习如何使用 Aspose.Cells for .NET 在 Excel 单元格中添加注释。为初学者提供增强 Excel 功能的分步指南。"
"linktitle": "在 Excel 中向单元格或形状添加注释"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 Excel 中向单元格或形状添加注释"
"url": "/zh/net/excel-comment-annotation/add-comments-to-cells-or-shapes-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中向单元格或形状添加注释

## 介绍
您是否想通过向单元格或形状添加注释来增强您的 Excel 文档？那么您来对地方了！本文将指导您使用 Aspose.Cells for .NET 高效地向 Excel 文件添加注释。无论您是想提供反馈、注释，还是仅仅是一个友好的提示，我们都会逐步讲解，以便您轻松上手。那就拿起您的虚拟工具箱，开始吧！
## 先决条件
在开始向 Excel 工作表添加注释之前，请确保您已准备好所需的一切。以下是您应该准备的内容：
- 已安装 Visual Studio：您需要一个 IDE 来编写和编译 .NET 应用程序。Visual Studio 是许多开发人员的热门选择。
- Aspose.Cells 软件包：确保您已安装 Aspose.Cells 库。它是一个强大的 Excel 文件处理工具。您可以从 [发布页面](https://releases。aspose.com/cells/net/).
- C# 基础知识：对 C# 编程的基本了解将会很有帮助，因为所有示例都将使用这种编程语言。
- Aspose.Cells 许可证：如需扩展功能，请考虑购买许可证，但您也可以从 [免费试用](https://releases.aspose.com/)，但这有其局限性。
## 导入包
要开始使用 Aspose.Cells，首先需要在 C# 项目中导入必要的软件包。操作方法如下：
### 打开你的项目
在 Visual Studio 中打开现有项目，或者如果从头开始，则创建一个新项目。
### 安装 Aspose.Cells
您可以通过 NuGet 轻松安装 Aspose.Cells 软件包。具体操作如下：
1. 在解决方案资源管理器中右键单击您的项目。
2. 选择“管理 NuGet 包”。
3. 搜索“Aspose.Cells”并安装最新版本。
### 添加 Using 语句
在代码文件的顶部，包含以下 using 指令：
```csharp
using System.IO;
using Aspose.Cells;
```
现在，您已准备好使用 Aspose.Cells 操作 Excel 文件。 

先决条件搞清楚了，我们来看看本指南的重点：如何在 Excel 文件中的单元格或形状中添加注释。我们将一步步讲解。
## 步骤1：设置文档目录
在开始操作工作簿之前，我们需要定义文档的存储位置。以下是如何设置文档目录。
```csharp
// 文档目录的路径。
string dataDir = "Your Document Directory";
// 如果目录尚不存在，则创建该目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
这里，我们检查目录是否存在。如果不存在，就创建它。这就像在开始布置家具之前，先确认你有一个家！
## 步骤2：实例化工作簿对象
现在我们需要创建一个新的 Workbook 实例，我们将在其中实现所有的魔法。
```csharp
// 实例化 Workbook 对象
Workbook workbook = new Workbook();
```
将工作簿视为您的空白画布，您可以在其中绘制您的 Excel 杰作。 
## 步骤 3：添加新工作表
一个 Excel 文件可以包含多个工作表。让我们在工作簿中添加一个新的工作表。
```csharp
// 向 Workbook 对象添加新工作表
int sheetIndex = workbook.Worksheets.Add();
```
每位伟大的艺术家都需要一张空白画布。现在，我们来添一张！
## 步骤 4：访问新工作表
接下来，获取新工作表的引用以开始进行更改。
```csharp
// 通过传递工作表索引来获取新添加工作表的引用
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
这一步至关重要，因为它允许您直接使用刚刚添加的新工作表，就像访问您的工作台一样。
## 步骤5：向单元格 F5 添加注释
现在，让我们进入激动人心的部分——为特定单元格添加注释。在本例中，我们将对单元格“F5”进行注释。
```csharp
// 向“F5”单元格添加注释
int commentIndex = worksheet.Comments.Add("F5");
```
可以把它想象成在工作的特定部分贴一张便签。它可以帮助你记住你的想法！
## 步骤6：访问新添加的评论
为了定制我们的评论，我们需要在添加评论后立即访问它。
```csharp
// 访问新添加的评论
Comment comment = worksheet.Comments[commentIndex];
```
在此步骤中，我们将检索便签，以便我们可以在上面写下我们的想法。
## 步骤 7：设置注释
现在，是时候记下我们的笔记了。让我们在评论中添加一些文字。
```csharp
// 设置注释
comment.Note = "Hello Aspose!";
```
想象一下在便签上写字。你正在把你的想法变成文字！
## 步骤8：保存Excel文件
最后，同样重要的是，我们需要保存我们的辛苦工作。这将保存包含我们评论的工作簿！
```csharp
// 保存 Excel 文件
workbook.Save(dataDir + "book1.out.xls");
```
这一步就像写完一个精彩的故事后合上书一样——您要确保它被保存下来！
## 结论
就这样！您已经成功使用 Aspose.Cells for .NET 在 Excel 文件中的单元格中添加了注释。注释对于协作项目或简单地为自己添加提醒非常有用。现在您已经完成了整个过程，准备好将您的 Excel 技能提升到一个新的水平。
## 常见问题解答
### 我可以使用 Aspose.Cells 为形状添加注释吗？
是的！您可以像添加单元格注释一样，为形状添加注释。
### Aspose.Cells 支持哪些文件格式？
Aspose.Cells 支持各种格式，包括 XLS、XLSX、CSV 等。
### Aspose.Cells 可以免费使用吗？
Aspose.Cells 提供免费试用，但要使用全部功能，您可能需要购买许可证。
### 在哪里可以找到对 Aspose.Cells 的支持？
您可以通过访问 [Aspose 论坛](https://forum。aspose.com/c/cells/9).
### 如何获得 Aspose.Cells 的临时许可证？
临时驾照可从 [Aspose 许可证页面](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}