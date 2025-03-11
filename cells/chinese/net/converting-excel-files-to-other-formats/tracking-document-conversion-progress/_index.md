---
title: 在 .NET 中以编程方式跟踪文档转换进度
linktitle: 在 .NET 中以编程方式跟踪文档转换进度
second_title: Aspose.Cells .NET Excel 处理 API
description: 在本详细教程中了解如何使用 Aspose.Cells for .NET 以编程方式跟踪文档转换进度。
weight: 20
url: /zh/net/converting-excel-files-to-other-formats/tracking-document-conversion-progress/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以编程方式跟踪文档转换进度

## 介绍
您是否希望使用 Aspose.Cells for .NET 增强文档转换过程？如果是这样，您来对地方了！在本教程中，我们将深入探讨如何跟踪 Excel 文档转换为 PDF 格式时的转换进度。我们不仅会指导您完成实现此目的的基本步骤，还会在此过程中提供一些有用的见解。那么，让我们开始吧！
## 先决条件
在我们深入了解跟踪文档转换的细节之前，您应该满足一些先决条件：
1. C# 基础知识：由于我们将使用 C# 进行编码，因此对该编程语言的基本了解将会很有用。
2. 已安装 Visual Studio：这将作为我们的开发环境。您可以使用任何您喜欢的版本，但最新版本始终是最佳选择。
3.  Aspose.Cells for .NET：确保您已安装 Aspose.Cells。您可以从[Aspose 网站](https://releases.aspose.com/cells/net/).
4. Excel 文件：准备好要转换的 Excel 示例文件。您可以创建一个简单的`.xlsx`文件进行跟踪。
## 导入包
现在我们已经满足了先决条件，是时候将必要的包导入到您的 C# 项目中了。操作方法如下：
### 创建新项目
1. 打开 Visual Studio 并创建一个新项目。为简单起见，选择一个控制台应用程序模板。
### 添加对 Aspose.Cells 的引用
2. 右键单击解决方案资源管理器中的引用，选择添加引用，然后导航到 Aspose.Cells 程序集（如果未自动添加）。您还可以通过在包管理器控制台中运行以下命令来使用 NuGet 包管理器：
```bash
Install-Package Aspose.Cells
```
### 导入命名空间
3. 在你的顶部`Program.cs`文件中，添加以下 using 指令：
```csharp
using Aspose.Cells.Rendering;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
现在我们的项目设置已经全部完成！

打好基础之后，让我们将跟踪文档转换的实际过程分解为易于理解的步骤。 
## 步骤 1：定义目录
首先指定源文件和输出文件所在的目录。操作方法如下：
```csharp
//源目录
string sourceDir = "Your Document Directory";
//输出目录
string outputDir = "Your Document Directory";
```
确保更换`"Your Document Directory"`与您系统上的实际路径一致。这将有助于轻松找到您的文件。
## 步骤 2：加载工作簿
接下来，您需要使用`Workbook`类。操作方法如下：
```csharp
Workbook workbook = new Workbook(sourceDir + "PagesBook1.xlsx");
```
这行代码创建一个`Workbook`对象将允许我们与指定的 Excel 文件进行交互。
## 步骤 3：设置 PDF 保存选项
现在，让我们设置 PDF 保存选项。这就是跟踪进度的魔力开始的地方。您将创建一个实例`PdfSaveOptions`并为其分配一个回调。
```csharp
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.PageSavingCallback = new TestPageSavingCallback();
```
通过分配自定义回调（`TestPageSavingCallback`），我们可以实现自己的页面转换进度跟踪逻辑。
## 步骤 4：将工作簿保存为 PDF
一切设置完毕后，就可以将工作簿保存为 PDF 了。使用`Save`方法`Workbook`像这样的类：
```csharp
workbook.Save(outputDir + "DocumentConversionProgress.pdf", pdfSaveOptions);
```
此行将触发转换过程并在处理页面时调用我们的回调方法。
## 步骤 5：实现回调类
现在让我们创建`TestPageSavingCallback`类。在这里您可以定义在保存每个页面时开始和结束时发生的情况。
```csharp
public class TestPageSavingCallback : IPageSavingCallback
{
    public void PageStartSaving(PageStartSavingArgs args)
    {
        Console.WriteLine("Start saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        //不要输出页面索引 2 之前的页面。
        if (args.PageIndex < 2)
        {
            args.IsToOutput = false;
        }
    }
    public void PageEndSaving(PageEndSavingArgs args)
    {
        Console.WriteLine("End saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        //不输出页面索引 8 之后的页面。
        if (args.PageIndex >= 8)
        {
            args.HasMorePages = false;
        }
    }
}
```
- `PageStartSaving`：此方法在页面开始保存之前调用。在这里，我们记录每个页面保存过程的开始。此外，我们可以控制是否输出页面。在本例中，索引 2 之前的页面将被跳过。
- `PageEndSaving`：保存页面后会调用此方法。它允许您记录每个页面的保存结束时间，并控制是否应处理更多页面。在此示例中，我们在页面索引 8 后停止。
## 结论
恭喜！您已成功实施了一个使用 Aspose.Cells for .NET 跟踪文档转换进度的系统。这种方法不仅可以让您监控转换过程，还可以控制要包含或排除哪些页面，从而使您的文档管理更加高效。
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的.NET 库，允许开发人员以编程方式创建、操作和转换 Excel 文件。
### 如何获得 Aspose.Cells 的免费试用版？
您可以从[Aspose 网站](https://releases.aspose.com/).
### 是否可以自定义转换过程？
是的，使用回调，您可以自定义转换过程中页面的处理方式。
### 我可以控制输出文件名吗？
当然可以！保存工作簿时，您可以为输出文件指定任意名称。
### 在哪里可以找到对 Aspose.Cells 的支持？
您可以通过访问获得支持[Aspose 论坛](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
