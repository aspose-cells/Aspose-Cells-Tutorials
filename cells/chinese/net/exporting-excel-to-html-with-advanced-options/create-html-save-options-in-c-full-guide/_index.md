---
category: general
date: 2026-06-08
description: 在 C# 中创建 HTML 保存选项，以嵌入所有字体并将工作簿保存为 HTML。学习如何使用一个简洁完整的示例将 Excel 工作簿导出为
  HTML。
draft: false
keywords:
- create html save options
- save workbook as html
- export excel workbook to html
- embed all fonts in html
language: zh
og_description: 在 C# 中创建 HTML 保存选项，以嵌入所有字体并将 Excel 工作簿导出为 HTML。本指南将带您完成完整的可直接运行的解决方案。
og_title: 在 C# 中创建 HTML 保存选项 – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  headline: Create HTML Save Options in C# – Full Guide
  type: TechArticle
- description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  name: Create HTML Save Options in C# – Full Guide
  steps:
  - name: Expected Output
    text: Running the program produces `EmbeddedWorkbook.html` in the execution folder.
      Open it in any modern browser and you’ll see the text **“Hello, Aspose.Cells!”**
      rendered in **Comic Sans MS**, even if your system doesn’t have that font installed.
      Inspect the HTML source and you’ll notice a `<style>` bl
  - name: What if the workbook contains many different fonts?
    text: Embedding *all* fonts can inflate the HTML size dramatically (each font
      is Base64‑encoded). If file size becomes a concern, consider setting `EmbedAllFonts
      = false` and manually embedding only the critical fonts via `htmlOptions.FontEmbeddingMode
      = FontEmbeddingMode.Custom;`.
  - name: Does this work with older Excel files (`.xls`)?
    text: Absolutely. Aspose.Cells abstracts the source format, so whether you load
      an `.xlsx`, `.xls`, or even a CSV, the **export excel workbook to html** step
      behaves the same.
  - name: Can I control the output folder dynamically?
    text: 'Sure thing—just replace the hard‑coded `outputPath` with something like:'
  - name: What about images or charts inside the workbook?
    text: '`HtmlSaveOptions` also handles images, charts, and even formulas. By default
      they’re rendered as PNGs embedded in the HTML. If you prefer external files,
      toggle `htmlOptions.ExportImagesAsBase64 = false`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel Export
- HTML Export
title: 在 C# 中创建 HTML 保存选项 – 完整指南
url: /zh/net/exporting-excel-to-html-with-advanced-options/create-html-save-options-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建 HTML 保存选项 – 完整教程

是否曾想过如何 **创建 HTML 保存选项**，使每种字体在导出的 HTML 中都保持与 Excel 中完全相同的外观？你并不孤单。许多开发者在导出的 HTML 丢失自定义字体，导致页面显得单调时会遇到困难。好消息是，只需几行 C# 代码，你就可以 **在 HTML 中嵌入所有字体** 并 **将工作簿保存为 HTML**，毫无障碍。

在本指南中，我们将使用 Aspose.Cells 完整演示 **将 Excel 工作簿导出为 HTML** 的全过程。结束时，你将拥有一个自包含、可直接运行的程序，它不仅会创建正确的选项，还会解释 *每个设置为何重要*。没有缺失的环节，没有“请查看文档”的绕路——只有清晰的端到端解决方案。

## 前置条件

在开始之前，请确保你具备以下环境：

* .NET 6.0 SDK（或任意较新的 .NET 版本）——代码在 .NET Core 和 .NET Framework 上均可运行。  
* **Aspose.Cells** NuGet 包——`dotnet add package Aspose.Cells`。  
* 对 C# 语法有基本了解——只要会写 `Console.WriteLine`，就可以上手。  

仅此而已。无需额外工具，也不需要奇怪的配置文件。

## 第一步：创建项目并加载工作簿

首先要做的就是建立一个控制台项目并准备一个工作簿。如果你已经有 Excel 文件，直接使用即可——否则示例会在运行时动态创建一个。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook or load an existing one
        Workbook wb = new Workbook(); // starts with a default sheet

        // Populate the sheet with some styled text so we can see font embedding in action
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS";   // a non‑system font to test embedding
        style.Font.Size = 14;
        cell.SetStyle(style);

        // Continue with HTML export...
```

**这样做的原因：** 加载工作簿为后续导出提供对象。我们在工作簿中加入自定义字体（`Comic Sans MS`），以便后面的 *嵌入所有字体* 设置在生成的 HTML 中能够显现效果。

## 第二步：**创建 HTML 保存选项** – 本任务的核心

接下来进入关键环节：配置 `HtmlSaveOptions`。该对象告诉 Aspose.Cells 如何生成 HTML。

```csharp
        // Step 2: Create HTML save options and embed all fonts in the output
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Setting this to true forces every used font to be base‑64 encoded
            // and placed directly inside the HTML file. No external .ttf files.
            EmbedAllFonts = true,

            // Optional but handy: keep the original Excel formatting
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };
```

**为什么 `EmbedAllFonts = true` 很重要：** 当在浏览器中打开生成的 HTML 时，自定义字体已经被嵌入文件中。这样即使目标机器没有安装该字体，页面也会与 Excel 源文件保持完全一致的外观。

## 第三步：使用配置好的选项 **将工作簿保存为 HTML**

准备好选项后，就可以 **将工作簿保存为 HTML**。该方法接受文件路径、目标格式以及我们刚才构建的选项对象。

```csharp
        // Step 3: Save the workbook as an HTML file using the configured options
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

**内部到底发生了什么？** Aspose.Cells 会逐单元格渲染，将字体定义转换为 Base64 编码，并注入到 `<style>` 块中。生成的 `EmbeddedWorkbook.html` 是一个单一的自包含文件——不再有 `.css` 或独立的字体文件。

## 完整可运行示例

将上述所有代码组合起来，得到的完整程序可直接复制到 `Program.cs` 并运行：

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a workbook
        Workbook wb = new Workbook();
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS"; // non‑standard font for testing
        style.Font.Size = 14;
        cell.SetStyle(style);

        // 2️⃣ Create HTML save options – embed all fonts
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            EmbedAllFonts = true,
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };

        // 3️⃣ Save workbook as HTML
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

### 预期输出

运行程序后，会在执行目录生成 `EmbeddedWorkbook.html`。用任意现代浏览器打开，你会看到文本 **“Hello, Aspose.Cells!”** 以 **Comic Sans MS** 渲染，即使系统未安装该字体。检查 HTML 源码，你会发现一个包含 `@font-face` 规则的 `<style>` 块，内部是一段巨大的 Base64 字符串——这就是嵌入的字体。

![创建 HTML 保存选项流程图](image.png "显示 HTML 导出流程的示意图"){: alt="创建 HTML 保存选项流程图"}

*Alt 文本包含主要关键词以提升 SEO。*

## 常见问题与边缘情况

### 工作簿中包含多种不同字体怎么办？

嵌入 *所有* 字体会显著增大 HTML 大小（每种字体都会被 Base64 编码）。如果文件体积成为顾虑，可考虑将 `EmbedAllFonts = false`，并通过 `htmlOptions.FontEmbeddingMode = FontEmbeddingMode.Custom;` 手动嵌入关键字体。

### 能否处理旧版 Excel 文件（`.xls`）？

完全可以。Aspose.Cells 会抽象源文件格式，无论是 `.xlsx`、`.xls` 甚至 CSV，**将 Excel 工作簿导出为 HTML** 的步骤表现一致。

### 能否动态控制输出文件夹？

当然可以，只需将硬编码的 `outputPath` 替换为如下代码：

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "Reports", "MyExport.html");
Directory.CreateDirectory(Path.GetDirectoryName(outputPath));
```

这样就可以在任意位置 **将工作簿保存为 HTML**。

### 工作簿中的图片或图表怎么办？

`HtmlSaveOptions` 同样支持图片、图表以及公式。默认情况下，它们会以 PNG 形式嵌入 HTML 中。如果希望生成外部文件，只需将 `htmlOptions.ExportImagesAsBase64 = false`。

## 专业小贴士

* **性能提示：** 若在循环中导出多个工作簿，复用同一个 `HtmlSaveOptions` 实例可以减少垃圾生成。  
* **测试提示：** 使用无头浏览器（如 Puppeteer）自动验证嵌入字体的渲染效果。  
* **版本检查：** `EmbedAllFonts` 标志在 Aspose.Cells 20.9 中首次引入，请确保你的 NuGet 包已更新到最新版本。

## 结论

现在，你已经掌握了如何在 C# 中 **创建 HTML 保存选项**，并 **在 HTML 中嵌入所有字体**，以及如何 **将工作簿保存为 HTML**。本完整、可直接运行的示例涵盖了 **导出 Excel 工作簿为 HTML** 的 *什么*、*为什么* 与 *如何*，为后续的批量处理或自定义样式等高级场景奠定了坚实基础。

准备好下一步了吗？尝试导出包含图表的工作簿，或实验不同的 `HtmlSaveOptions` 属性，如 `ExportImagesAsBase64` 或 `CssClassPrefix`。同样的模式——创建选项、调整标记、调用 `wb.Save`。祝编码愉快，愿你的 HTML 导出始终与原始 Excel 表格保持完全一致！

## 接下来该学习什么？

以下教程与本指南紧密相关，进一步扩展了本章节展示的技术。每篇资源均提供完整可运行的代码示例和逐步说明，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Html Save Options 为表格元素样式添加前缀](/cells/english/net/exporting-excel-to-html-with-advanced-options/prefixing-table-elements-styles/)
- [使用 Aspose.Cells for .NET 设置 Excel 转 HTML 的默认字体 | 工作簿操作指南](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [使用 Aspose.Cells for .NET 将 Excel 工作簿和工作表属性导出为 HTML](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}