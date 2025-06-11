---
"description": "在本详细教程中了解如何使用 Aspose.Cells for .NET 读取 Numbers 电子表格并将其转换为 PDF。"
"linktitle": "在 .NET 中以编程方式读取数字电子表格"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 .NET 中以编程方式读取数字电子表格"
"url": "/zh/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以编程方式读取数字电子表格

## 介绍
在当今的数字世界中，数据管理是一项至关重要的技能，而电子表格则处于数据组织的最前沿。但是，如果您需要使用 .NET 处理 Numbers 电子表格（由 Apple 的 Numbers 应用程序创建的文件），该怎么办？别担心，您并不孤单！在本教程中，我们将逐步讲解如何使用 Aspose.Cells for .NET 以编程方式读取 Numbers 电子表格的过程。您将学习如何加载 Numbers 文件并将其转换为 PDF。
## 先决条件
在我们开始之前，您需要做好以下几点：
1. Aspose.Cells for .NET：请确保您已安装 Aspose.Cells 库。您可以下载 [这里](https://releases。aspose.com/cells/net/).
2. Visual Studio：建议在您的机器上安装 Visual Studio（或任何其他与 .NET 兼容的 IDE）。
3. C# 基础知识：稍微熟悉一下 C# 编程将有助于您顺利完成学习。
4. 您的文档目录：您需要一个存储 Numbers 文件的目录，以及一个保存转换后的 PDF 的位置。
一旦满足了这些先决条件，您就可以开始了！
## 导入包
首先，我们需要将必要的软件包导入到我们的 C# 项目中。这一步至关重要，因为它使我们能够利用 Aspose.Cells 库提供的功能。
1. 在 Visual Studio 中打开您的 C# 项目。
2. 添加对 Aspose.Cells 库的引用：
   - 如果您使用 NuGet，只需在包管理器控制台中运行以下命令：
```
 Install-Package Aspose.Cells
 ```
3. 在代码中导入必要的命名空间：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
现在我们已经导入了必要的包，让我们继续逐步指导如何读取 Numbers 电子表格。
## 步骤 1：指定源目录和输出目录
在此步骤中，我们将设置源 Numbers 文件所在的目录以及您想要保存输出 PDF 的位置。
```csharp
// 源目录
string sourceDir = "Your Document Directory"; // 将其更新为您的实际目录
// 输出目录
string outputDir = "Your Document Directory"; // 将其更新为您的实际目录
```
这里我们定义了两个字符串变量， `sourceDir` 和 `outputDir`，指定输入和输出文件的位置。请确保替换 `"Your Document Directory"` 使用系统上的实际路径。
## 步骤 2：设置数字格式的加载选项
接下来，我们将指定读取 Numbers 电子表格的加载选项。此步骤至关重要，因为它会告诉 Aspose 如何解释 Numbers 文件。
```csharp
// 指定加载选项；我们要加载 Numbers 电子表格
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
我们创建了一个 `LoadOptions` 对象并指定格式为 `LoadFormat.Numbers`。这告诉 Aspose.Cells 库我们正在处理 Numbers 文件。 
## 步骤 3：将 Numbers 电子表格加载到工作簿中
现在，是时候将实际的 Numbers 电子表格加载到 `Workbook` 目的。
```csharp
// 使用上述加载选项将 Numbers 电子表格加载到工作簿中
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
我们实例化一个 `Workbook` 对象，并传递 Numbers 文件的文件路径以及我们的加载选项。确保文件名（`sampleNumbersByAppleInc.numbers`) 与 Numbers 文件的实际名称相匹配。
## 步骤 4：将工作簿保存为 PDF
一旦 Numbers 文件成功加载，下一步就是将其保存为不同的格式 - 具体来说，是 PDF。
```csharp
// 将工作簿保存为 PDF 格式
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
在这里，我们称 `Save` 方法 `Workbook` 对象，指定输出文件路径和保存格式。在本例中，我们将其保存为 PDF。确保输出文件名（`outputNumbersByAppleInc.pdf`) 是唯一的，并且不会覆盖任何现有文件。
## 步骤5：确认成功
最后，让我们添加一条消息来确认我们的操作成功。
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
这行代码会在所有操作完成后在控制台打印一条成功消息。有反馈总是好的，对吧？
## 结论
就这样！您已经成功读取了 Numbers 电子表格，并使用 Aspose.Cells for .NET 将其转换为 PDF。这个强大的库让您轻松操作电子表格，让您的数据管理任务变得轻而易举。无论您是开发应用程序，还是仅仅需要更高效地处理电子表格，Aspose.Cells 都是您工具包中不可或缺的优秀工具。
## 常见问题解答
### Aspose.Cells 可以读取哪些类型的文件？  
Aspose.Cells 可以读取多种文件格式，包括 XLS、XLSX、CSV 和 Numbers 文件。 
### 我可以使用 Aspose.Cells 编辑 Numbers 文件吗？  
是的，您可以使用 Aspose.Cells 读取、操作和保存 Numbers 文件。
### Aspose.Cells 可以免费使用吗？  
Aspose.Cells 提供免费试用，但您需要购买许可证才能继续使用。查看价格 [这里](https://purchase。aspose.com/buy).
### 如果在加载 Numbers 文件时遇到错误，该怎么办？  
请确保使用正确的加载选项，并且文件路径准确无误。如需更多支持，请访问 [Aspose 支持论坛](https://forum。aspose.com/c/cells/9).
### 如何获得 Aspose.Cells 的临时许可证？  
您可以申请临时驾照 [这里](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}