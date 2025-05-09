---
"description": "通过我们全面的分步教程学习如何使用 Aspose.Cells for .NET 控制 Excel 中的外部资源。"
"linktitle": "使用工作簿设置控制外部资源"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "使用工作簿设置控制外部资源"
"url": "/zh/net/workbook-settings/control-external-resources/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用工作簿设置控制外部资源

## 介绍
在数据操作和呈现领域，高效地处理外部资源至关重要。如果您正在处理 Excel 文件，并希望使用 Aspose.Cells for .NET 无缝管理外部资源，那么您来对地方了！本文将深入探讨如何在处理 Excel 工作簿时控制外部资源。完成本指南后，您将能够轻松实现自定义解决方案，从外部来源加载图像和数据。
## 先决条件
在我们深入探讨编码细节之前，您需要满足一些先决条件。请确保：
1. 拥有 Visual Studio：您需要一个 IDE 来编写和测试您的 .NET 应用程序。Visual Studio 是最推荐的选项，因为它提供广泛的支持并且易于使用。
2. 下载 Aspose.Cells for .NET：如果您还没有，请从 [下载链接](https://releases。aspose.com/cells/net/). 
3. 对 C# 的基本了解：熟悉 C# 和 .NET 框架概念将使您的流程更加顺畅。
4. 设置您的环境：确保您的项目引用了 Aspose.Cells 库。您可以通过 Visual Studio 中的 NuGet 包管理器来完成此操作。
5. 示例文件：准备一个包含外部资源（例如链接图像）的示例 Excel 文件。此文件将有助于演示我们讨论的功能。
一旦设置好这些，您就可以开始使用 Aspose.Cells 控制外部资源了。
## 导入包
要开始编码，你需要在 C# 文件中导入必要的包。你需要：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
这些命名空间提供操作 Excel 文件和处理图像所需的功能的访问。
让我们将其分解为可管理的步骤，以帮助您使用以下方式控制外部资源 `Workbook Settings`我们将逐步讲解如何创建自定义流提供程序、加载 Excel 文件以及如何将工作表渲染为图像。欢迎继续学习！
## 步骤 1：定义源和输出目录
首先，我们需要指定读取文件的目录以及保存输出的目录。设置正确的路径至关重要，以避免出现“文件未找到”的错误。
```csharp
// 源目录
static string sourceDir = "Your Document Directory";
// 输出目录
static string outputDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 使用您的文件所在的实际路径。
## 步骤2：实现IStreamProvider接口
接下来，我们将创建一个自定义类来实现 `IStreamProvider` 接口。此类将管理如何访问外部资源（如图像）。
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // 必要时清理所有资源
    }
    public void InitStream(StreamProviderOptions options)
    {
        // 打开外部资源的文件流
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
在 `InitStream` 方法中，我们打开作为外部资源的文件并将其分配给 `Stream` 属性。这允许工作簿在渲染时访问资源。
## 步骤3：加载Excel文件
现在我们已经准备好流提供程序，让我们加载包含外部资源的 Excel 工作簿。
```csharp
public static void Run()
{
    // 加载示例 Excel 文件
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // 提供 IStreamProvider 的实现
    wb.Settings.StreamProvider = new SP();
```
在此代码片段中，我们加载 Excel 文件并分配自定义 `StreamProvider` 处理外部资源的实现。
## 步骤 4：访问工作表
加载工作簿后，我们可以轻松访问所需的工作表。让我们抓取第一个。
```csharp
    // 访问第一个工作表
    Worksheet ws = wb.Worksheets[0];
```
很简单，不是吗？你可以通过指定索引来访问任何工作表。
## 步骤 5：配置图像或打印选项
现在，我们将定义输出图像的外观。我们将配置一些选项，例如确保每张纸对应一页，并指定输出图像类型。
```csharp
    // 指定图像或打印选项
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
选择 PNG 作为输出格式可确保质量保持清晰！
## 步骤 6：将工作表渲染为图像
一切设置完毕后，让我们将选定的工作表渲染为图像文件！接下来就是激动人心的部分了；你会看到你的 Excel 工作表变成了一张漂亮的图像。
```csharp
    // 通过传递所需参数创建工作表渲染
    SheetRender sr = new SheetRender(ws, opts);
    // 将整个工作表转换为 png 图像
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
这 `ToImage` 函数会完成所有繁重的工作，将工作表转换为图像。完成此步骤后，您会发现图像已保存到输出目录中。
## 结论
就这样！您现在掌握了如何在 .NET 中使用 Aspose.Cells 处理 Excel 文件时控制外部资源。这不仅增强了应用程序的功能，还使处理数据集和演示文稿变得轻而易举。按照提供的步骤，您可以轻松复制和调整此功能，以满足您项目的特定需求。
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的库，专为 C# 和 .NET 开发人员设计，无需安装 Microsoft Excel 即可创建、操作和管理 Excel 文件。
### 如何下载 Aspose.Cells for .NET？
您可以从 [Aspose 网站](https://releases。aspose.com/cells/net/).
### 有免费试用吗？
是的！您可以从他们的 [发布页面](https://releases。aspose.com/).
### Aspose.Cells 支持哪些类型的文件？
Aspose.Cells 支持各种 Excel 格式，包括 XLS、XLSX、CSV 等。
### 在哪里可以找到对 Aspose.Cells 的支持？
您可以访问 Aspose 支持论坛 [Aspose 论坛](https://forum.aspose.com/c/cells/9) 寻求帮助。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}