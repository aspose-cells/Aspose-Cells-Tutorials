---
title: 以 97-2003 格式保存 Excel 文件
linktitle: 以 97-2003 格式保存 Excel 文件
second_title: Aspose.Cells .NET Excel 处理 API
description: 了解如何使用 Aspose.Cells for .NET 以 97-2003 格式保存 Excel 文件。获得实用见解和分步指导。
weight: 10
url: /zh/net/saving-files-in-different-formats/save-excel-file-in-97-2003-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 以 97-2003 格式保存 Excel 文件

## 介绍
以编程方式创建和管理 Excel 文件可能会带来翻天覆地的变化，尤其是对于严重依赖数据处理的企业而言。Aspose.Cells 是 .NET 开发人员可用的出色工具之一。它功能多样且功能强大，可帮助您简化工作流程并使用电子表格自动执行任务。如果您希望以经典的 97-2003 格式保存 Excel 文件，那么您来对地方了！让我们开始吧。
## 先决条件
在我们深入讨论细节之前，您需要满足一些先决条件：
1. 对 .NET 的基本了解：熟悉 C# 或 VB.NET 将会非常有帮助。
2.  Aspose.Cells for .NET：确保您的项目中安装了 Aspose.Cells 库。如果尚未安装，您可以[点击下载](https://releases.aspose.com/cells/net/).
3. Visual Studio：像 Visual Studio 或任何 .NET 兼容 IDE 这样的开发环境将促进编码和调试。
4. NuGet 包管理器：用于在您的项目中最轻松地安装 Aspose.Cells。 
一旦满足了这些先决条件，我们就可以开始了！
## 导入包
要开始使用 Aspose.Cells，您首先需要将必要的命名空间导入到您的项目中。这将使您能够访问操作 Excel 文件所需的类和方法。操作方法如下：
### 打开你的项目
在 Visual Studio 中打开您的 .NET 项目。
### 安装 Aspose.Cells
如果您尚未安装 Aspose.Cells 包，您可以通过 NuGet 进行安装。 
1. 转到工具->NuGet 包管理器->管理解决方案的 NuGet 包。
2. 搜索 Aspose.Cells。
3. 单击“安装”。
### 导入命名空间
在 C# 文件的顶部，包含以下行：
```csharp
using System.IO;
using Aspose.Cells;
```
现在您就可以开始编码了！
在本节中，我们将指导您使用 Aspose.Cells 以 97-2003 格式 (.xls) 保存 Excel 文件的过程。让我们将其分解为易于遵循的步骤。
## 步骤 1：设置文档目录
首先！您需要建立保存 Excel 文件的目录。
```csharp
string dataDir = "Your Document Directory";
```
- `"Your Document Directory"` ：将此占位符字符串替换为要保存 Excel 文件的实际路径。它可能类似于`"C:\\ExcelFiles\\"`.
## 步骤 2：创建新的工作簿对象
接下来，让我们创建一个新的实例`Workbook`课堂上。这就是所有魔法发生的地方！
```csharp
Workbook workbook = new Workbook();
```
- `Workbook`：此类代表您正在处理的 Excel 文件。通过实例化它，您实际上是在创建一个新的空白工作簿。
## 步骤 3：以 97-2003 格式保存工作簿
这是您期待已久的时刻！是时候保存您的工作簿了。有两种方法可以做到这一点。
### 简单保存
使用以下代码将您的文件直接保存到指定路径。
```csharp
workbook.Save(dataDir + "output.xls");
```
### 按指定格式保存
您还可以明确指定保存格式：
```csharp
workbook.Save(dataDir + "output.xls", SaveFormat.Excel97To2003);
```
- `output.xls`：这是您要保存的文件的名称。您可以根据需要重命名它。
- `SaveFormat.Excel97To2003`：这可确保您的文件保存为 Excel 97-2003 格式。
## 结论
以上就是使用 Aspose.Cells for .NET 以经典 97-2003 格式保存 Excel 文件的简单教程。无论您是创建财务报告还是维护数据日志，这种方法都可以简化您的工作并提高工作效率。尽情探索这个强大库的功能吧！
请记住，与任何编码项目一样，尝试和尝试不同的功能将带来更多的可能性。所以不要犹豫！
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的.NET 库，使开发人员无需安装 Microsoft Excel 即可处理 Excel 文件格式。
### 如何下载 Aspose.Cells for .NET？
您可以从以下位置下载[此链接](https://releases.aspose.com/cells/net/).
### 我可以免费使用 Aspose.Cells 吗？
是的，您可以免费试用[这里](https://releases.aspose.com/).
### 我可以将 Excel 文件保存为哪些格式？
您可以将 Excel 文件保存为各种格式，如 XLS、XLSX、CSV、PDF 等。
### 我可以在哪里获得 Aspose.Cells 的支持？
访问[Aspose 支持论坛](https://forum.aspose.com/c/cells/9)寻求帮助。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
