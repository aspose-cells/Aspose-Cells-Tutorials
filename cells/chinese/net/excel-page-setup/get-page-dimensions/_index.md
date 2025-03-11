---
title: 获取页面尺寸
linktitle: 获取页面尺寸
second_title: Aspose.Cells for .NET API 参考
description: 在本分步指南中了解如何使用 Aspose.Cells for .NET 获取页面尺寸。非常适合使用 Excel 文件的开发人员。
weight: 40
url: /zh/net/excel-page-setup/get-page-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 获取页面尺寸

## 介绍

在处理 .NET 应用程序中的电子表格时，Aspose.Cells 库脱颖而出，成为一款功能强大的工具，可让开发人员轻松操作 Excel 文件。但是，如何使用这个功能强大的库获取各种纸张尺寸的页面尺寸？在本教程中，我们将逐步介绍该过程，确保您不仅了解 Aspose.Cells 的工作原理，而且还能熟练地在项目中使用它。 

## 先决条件 

在我们进入编码部分之前，你需要做好几件事才能有效地跟进：

### Visual Studio
确保你的机器上安装了 Visual Studio。这是你编写和执行 .NET 代码的地方。

### Aspose.Cells 库
您需要下载 Aspose.Cells 库并在项目中引用。您可以从以下位置获取它：
- 下载链接：[用于.NET的Aspose.Cells](https://releases.aspose.com/cells/net/)

### C# 基础知识
如果您对 C# 有基本的了解，这将大有裨益。本教程将采用易于理解的基本编程概念。

准备好了吗？让我们开始吧！

## 导入包

我们旅程的第一步是将必要的 Aspose.Cells 包导入我们的 C# 项目。具体操作如下：

### 创建新项目

打开 Visual Studio 并创建一个新的 C# 控制台应用程序项目。你可以随意命名，我们来使用`GetPageDimensions`.

### 添加引用

要使用 Aspose.Cells，您需要添加对库的引用：
- 在解决方案资源管理器中右键单击您的项目。
- 选择“管理 NuGet 包”。
- 搜索“Aspose.Cells”并安装。

### 添加使用指令

在你的顶部`Program.cs`文件中，插入此 using 指令来访问 Aspose.Cells 功能：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

现在我们已经导入了必要的软件包，一切已经顺利！ 

现在让我们通过每个步骤来探索如何检索各种纸张尺寸的尺寸。 

## 步骤 1：创建工作簿类的实例

您需要做的第一件事是从 Aspose.Cells 创建 Workbook 类的实例。此类代表一个 Excel 文件。

```csharp
Workbook book = new Workbook();
```

在这里，我们只需创建一个新的工作簿来保存我们的电子表格数据和配置。

## 第 2 步：访问第一个工作表

创建工作簿实例后，您需要访问第一个工作表。每个工作簿可以包含多个工作表，但在本演示中，我们将只使用第一个工作表。

```csharp
Worksheet sheet = book.Worksheets[0];
```

此行获取第一个工作表，使我们能够设置纸张尺寸并检索其各自的尺寸。

## 步骤 3：将纸张尺寸设置为 A2 并检索尺寸

现在是时候设置纸张尺寸并获取尺寸了！我们从 A2 纸张尺寸开始。

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

此代码将纸张尺寸设置为 A2，并立即输出宽度和高度。Aspose.Cells 的美妙之处在于它的简单性！

## 步骤 4：对其他纸张尺寸重复上述步骤

您需要对其他纸张尺寸（如 A3、A4 和 Letter）重复此过程。操作方法如下：

对于 A3：

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

对于 A4：

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

信件：

```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```

## 步骤 5：输出结论

最后，您需要确认整个操作已成功完成。您可以简单地将此状态记录到控制台：

```csharp
Console.WriteLine("GetPageDimensions executed successfully.\r\n");
```

## 结论

恭喜！您现在已经成功学会了如何使用 Aspose.Cells for .NET 检索不同纸张尺寸的页面尺寸。无论您是开发报告工具、自动电子表格还是数据分析功能，能够提取各种格式的页面尺寸都是非常有价值的。 

## 常见问题解答

### 什么是 Aspose.Cells？
Aspose.Cells 是一个.NET 库，用于创建、操作和转换 Excel 文件，而无需 Microsoft Excel。

### 我需要安装 Microsoft Excel 才能使用 Aspose.Cells 吗？
不是，Aspose.Cells 是一个独立库，不需要安装 Excel。

### 在哪里可以找到更多 Aspose.Cells 的示例？
您可以在这里查看文档：[Aspose.Cells 文档](https://reference.aspose.com/cells/net/).

### Aspose.Cells 有免费试用版吗？
是的！您可以从以下位置获取免费试用版：[Aspose.Cells 免费试用](https://releases.aspose.com/).

### 如何获得 Aspose.Cells 的支持？
您可以通过访问 Aspose 支持论坛获得帮助：[Aspose.Cells 支持](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
