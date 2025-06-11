---
"description": "在本详细教程中了解如何使用 Aspose.Cells for .NET 以编程方式跟踪文档转换进度。"
"linktitle": "在 .NET 中以编程方式跟踪文档转换进度"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 .NET 中以编程方式跟踪文档转换进度"
"url": "/zh/net/converting-excel-files-to-other-formats/tracking-document-conversion-progress/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以编程方式跟踪文档转换进度

## 介绍
您是否希望使用 Aspose.Cells for .NET 来增强文档转换流程？如果是，那么您来对地方了！在本教程中，我们将深入讲解如何跟踪 Excel 文档转换为 PDF 格式的进度。我们不仅会指导您完成实现此目标的基本步骤，还会提供一些实用技巧。那就开始吧！
## 先决条件
在我们深入探讨跟踪文档转换的细节之前，您应该满足一些先决条件：
1. C# 基础知识：由于我们将使用 C# 进行编码，因此对该编程语言的基本了解将会很有用。
2. 已安装 Visual Studio：这将作为我们的开发环境。您可以使用任何您喜欢的版本，但最新版本始终是最佳选择。
3. Aspose.Cells for .NET：确保您已安装 Aspose.Cells。您可以从 [Aspose 网站](https://releases。aspose.com/cells/net/).
4. Excel 文件：准备一个用于转换的示例 Excel 文件。您可以创建一个简单的 `.xlsx` 文件进行跟踪。
## 导入包
现在我们已经满足了先决条件，是时候将必要的包导入到你的 C# 项目中了。操作方法如下：
### 创建新项目
1. 打开 Visual Studio 并创建一个新项目。为了简单起见，选择一个“控制台应用程序”模板。
### 添加对 Aspose.Cells 的引用
2. 在解决方案资源管理器中右键单击“引用”，选择“添加引用”，然后导航到 Aspose.Cells 程序集（如果未自动添加）。您也可以通过在程序包管理器控制台中运行以下命令来使用 NuGet 程序包管理器：
```bash
Install-Package Aspose.Cells
```
### 导入命名空间
3. 在你的顶部 `Program.cs` 文件中，添加以下 using 指令：
```csharp
using Aspose.Cells.Rendering;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
现在我们的项目设置已经全部完成！

打好基础后，让我们将跟踪文档转换的实际过程分解为易于理解的步骤。 
## 步骤 1：定义目录
首先指定源文件和输出文件的存放目录。操作方法如下：
```csharp
// 源目录
string sourceDir = "Your Document Directory";
// 输出目录
string outputDir = "Your Document Directory";
```
确保更换 `"Your Document Directory"` 替换为您系统上的实际路径。这将有助于您轻松找到文件。
## 第 2 步：加载工作簿
接下来，您需要使用 `Workbook` 类。操作方法如下：
```csharp
Workbook workbook = new Workbook(sourceDir + "PagesBook1.xlsx");
```
这行代码创建了一个 `Workbook` 对象将允许我们与我们指定的 Excel 文件进行交互。
## 步骤3：设置PDF保存选项
现在，让我们设置 PDF 保存选项。这就是跟踪进度的魔力所在。您将创建一个 `PdfSaveOptions` 并为其分配一个回调。
```csharp
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.PageSavingCallback = new TestPageSavingCallback();
```
通过分配自定义回调（`TestPageSavingCallback`），我们可以实现自己的逻辑来跟踪页面转换进度。
## 步骤 4：将工作簿保存为 PDF
一切设置完成后，就可以将工作簿保存为 PDF 格式了。使用 `Save` 方法 `Workbook` 像这样的类：
```csharp
workbook.Save(outputDir + "DocumentConversionProgress.pdf", pdfSaveOptions);
```
此行将触发转换过程并在处理页面时调用我们的回调方法。
## 步骤5：实现回调类
现在让我们创建 `TestPageSavingCallback` 类。在这里您可以定义在保存每个页面时开始和结束时发生的情况。
```csharp
public class TestPageSavingCallback : IPageSavingCallback
{
    public void PageStartSaving(PageStartSavingArgs args)
    {
        Console.WriteLine("Start saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        // 不要输出页面索引 2 之前的页面。
        if (args.PageIndex < 2)
        {
            args.IsToOutput = false;
        }
    }
    public void PageEndSaving(PageEndSavingArgs args)
    {
        Console.WriteLine("End saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        // 不输出页面索引 8 之后的页面。
        if (args.PageIndex >= 8)
        {
            args.HasMorePages = false;
        }
    }
}
```
- `PageStartSaving`：此方法在页面开始保存之前调用。在这里，我们记录每个页面保存过程的开始。此外，我们可以控制是否输出该页面。在本例中，索引 2 之前的页面将被跳过。
- `PageEndSaving`：此方法在页面保存后调用。它允许您记录每个页面的保存结束时间，并控制是否应处理更多页面。在本例中，我们在页面索引 8 后停止。
## 结论
恭喜！您已成功使用 Aspose.Cells for .NET 实现了一个用于跟踪文档转换进度的系统。这种方法不仅可以让您监控转换过程，还可以控制包含或排除哪些页面，从而提高文档管理效率。
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的 .NET 库，允许开发人员以编程方式创建、操作和转换 Excel 文件。
### 如何免费试用 Aspose.Cells？
您可以从 [Aspose 网站](https://releases。aspose.com/).
### 是否可以自定义转换过程？
是的，使用回调，您可以自定义转换期间页面的处理方式。
### 我可以控制输出文件名吗？
当然！保存工作簿时，您可以为输出文件指定任意名称。
### 在哪里可以找到对 Aspose.Cells 的支持？
您可以通过访问 [Aspose 论坛](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}