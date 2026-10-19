---
category: general
date: 2026-06-27
description: 在将 Excel 转换为 HTML 时，将字体嵌入 HTML。了解如何使用简洁的 Java 代码将工作簿保存为带嵌入字体的 HTML。
draft: false
keywords:
- embed fonts in html
- convert excel to html
- save workbook as html
- Java Excel to HTML conversion
- Aspose.Cells HTML export
language: zh
og_description: 在将 Excel 转换为 HTML 时将字体嵌入 HTML。本指南展示如何使用 Java 将工作簿保存为嵌入字体的 HTML。
og_title: 在HTML中嵌入字体 – 将Excel转换为HTML并保存工作簿
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  headline: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  type: TechArticle
- description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  name: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  steps:
  - name: Right‑click the page → “View Page Source”.
    text: Right‑click the page → “View Page Source”.
  - name: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
    text: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
  - name: Load or create the workbook.
    text: Load or create the workbook.
  - name: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
    text: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
  - name: Call `Workbook.save` with those options.
    text: Call `Workbook.save` with those options.
  type: HowTo
tags:
- Java
- Aspose.Cells
- HTML
- Excel
title: 在HTML中嵌入字体 – 将Excel转换为HTML并保存工作簿
url: /zh/java/excel-import-export/embed-fonts-in-html-convert-excel-to-html-save-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在HTML中嵌入字体 – 将Excel转换为HTML并保存工作簿

是否曾在 *将 Excel 转换为 HTML* 时需要 **在 HTML 中嵌入字体**？也许你正在构建一个报表门户，默认的网页字体根本不够用。好消息是，你不必妥协于平淡、通用的外观——Aspose.Cells 让你可以将电子表格中使用的确切字体直接打包到生成的 HTML 文件中。

在本教程中，我们将演示一个完整、可直接运行的 Java 示例，**将工作簿保存为 HTML** 并嵌入字体，解释为何需要这样做，并指出可能遇到的一些陷阱。完成后，你将拥有一个自包含的 HTML 页面，外观与原始 Excel 表完全一致，没有缺失的字形，也没有外部 CSS 的烦恼。

## 你将学到的内容

- 如何在 Java 中加载已有的 Excel 工作簿（或从头创建一个）。  
- 如何配置 `HtmlSaveOptions` 将工作簿的字体直接嵌入到 HTML 输出中。  
- 如何调用 `Workbook.save` 将文件写为 **带嵌入字体的 HTML**。  
- 处理大字体文件、自定义字体目录以及排查常见问题的技巧。

> **先决条件：** 你的类路径中需要 Aspose.Cells for Java（最新版本），并且运行环境为 Java 8+。不需要其他第三方库。

---

## 第 1 步：设置项目并导入所需类

在编写代码之前，先确保开发环境已就绪。如果使用 Maven，请在 `pom.xml` 中添加 Aspose.Cells 依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the newest version available -->
</dependency>
```

如果更喜欢 Gradle，则对应写法为：

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

> **专业提示：** 保持库的最新版本。新版本通常会改进字体处理并减小嵌入数据的体积。

现在，导入我们需要的类：

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.HtmlSaveOptions;
import com.aspose.cells.SaveFormat;
import java.io.File;
```

这些导入让我们能够访问工作簿模型、HTML 导出选项以及一些实用工具类。

---

## 第 2 步：加载（或创建）Excel 工作簿

你可以加载已有的 `.xlsx` 文件，也可以即时创建工作簿。这里假设项目的 `resources` 文件夹中有一个名为 `Sample.xlsx` 的文件。

```java
// Load an existing workbook
String inputPath = "resources/Sample.xlsx";
Workbook wb = new Workbook(inputPath);
```

如果没有源文件，也可以快速生成一个工作簿：

```java
// Create a workbook from scratch (optional)
Workbook wb = new Workbook();               // creates a new empty workbook
wb.getWorksheets().get(0).getCells().putValue("A1", "Hello, world!");
```

> **为什么重要：** 当嵌入字体时，Aspose.Cells 会提取工作簿中使用的精确字体定义。如果工作簿包含自定义字体，这些字体会随 HTML 一起携带，从而保证视觉一致性。

---

## 第 3 步：配置 HtmlSaveOptions 以嵌入字体

这是本教程的核心。默认情况下，`HtmlSaveOptions` 会生成引用系统字体的 CSS。要改变这种行为，只需启用 `setEmbedFonts(true)` 标志。

```java
// Step 1: Create HTML save options
HtmlSaveOptions htmlOpts = new HtmlSaveOptions(SaveFormat.HTML);

// Step 2: Enable embedding of fonts in the HTML output
htmlOpts.setEmbedFonts(true);

// (Optional) Reduce the size of embedded fonts by subsetting only used glyphs
htmlOpts.setSubsetFonts(true);
```

### 选项说明

| 选项 | 默认值 | 更改后的效果 |
|--------|---------|---------------------|
| `setEmbedFonts(true)` | `false` | 将完整的字体文件（通常以 Base64 编码的 data URI 形式）嵌入生成的 HTML 中。 |
| `setSubsetFonts(true)` | `false` | 将嵌入的字体仅限于实际使用的字符，从而显著缩小文件大小。 |
| `setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_ALL)` | `EMBED_ALL` | 如果受到许可限制，您可以选择仅嵌入特定字体。 |

> **边缘情况：** 如果工作簿使用的字体未在服务器上安装，Aspose.Cells 会回退到默认系统字体。为避免意外，请确保所有自定义字体已放置在 Java 运行时的字体目录中，或通过 `FontConfig` 手动注册。

---

## 第 4 步：将工作簿保存为带嵌入字体的 HTML

选项配置完毕后，只需调用 `save`。输出将是一个单独的 `.html` 文件，里面既包含工作簿数据，又直接在标记中编码了字体文件。

```java
// Step 3: Save the workbook as an HTML file with embedded fonts
String outputDir = "output";
new File(outputDir).mkdirs(); // Ensure the folder exists

String outputPath = outputDir + File.separator + "page.html";
wb.save(outputPath, htmlOpts);

System.out.println("HTML file with embedded fonts created at: " + outputPath);
```

在任何现代浏览器中打开 `page.html` 时，页面会以与你在 Excel 中看到的完全相同的排版渲染——没有外部字体文件，也没有缺失字符。

---

## 第 5 步：验证结果并了解输出内容

在浏览器（Chrome、Firefox、Edge 任意）中打开生成的 HTML 文件。你应该能忠实地看到工作表的渲染效果。为再次确认字体已真正嵌入：

1. 右键单击页面 → “查看页面源代码”。  
2. 搜索 `@font-face`。你会发现一条 CSS 规则，其中包含 `src: url(data:font/ttf;base64,…)` 行——这就是 Base64 编码的字体数据。  

如果看到上述内容，**在 HTML 中嵌入字体** 的步骤就成功了。

### 常见问题

- **“为什么 HTML 文件比预期的大？”**  
  嵌入完整字体文件会增加数百 KB。使用 `setSubsetFonts(true)` 可以缩小体积，或者只转换所需的工作表。

- **“我能只嵌入特定的字体吗？”**  
  可以。设置 `htmlOpts.setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_SPECIFIED)`，随后通过 `htmlOpts.getSpecifiedFontNames().add("MyCustomFont")` 指定字体名称。

- **“如果字体受许可证限制，无法嵌入怎么办？”**  
  关闭该标志 (`setEmbedFonts(false)`) 并通过 CSS 提供网页安全的回退字体，或在拥有授权的 CDN 上托管该字体。

---

## 第 6 步：处理大型工作簿的性能建议

对小型电子表格来说，嵌入字体效果很好，但如果工作簿包含 dozens of custom fonts，HTML 大小会急剧膨胀。以下是一些面向性能的建议：

- **子集化字体**（如前所示），只保留实际使用的字形。  
- **仅导出所需工作表**，使用 `htmlOpts.setExportActiveWorksheetOnly(true)`。  
- **生成后压缩 HTML**（例如服务器端 gzip），以降低网络延迟。  
- **缓存生成的 HTML**，如果同一 Excel 文件被频繁请求。

---

## 第 7 步：后续步骤 – 超越基础导出

掌握了 **在 HTML 中嵌入字体** 后，你可能想进一步探索相关功能：

- **将 Excel 转换为带图片的 HTML** (`htmlOpts.setExportImagesAsBase64(true)`)。  
- **生成 PDF 而非 HTML** (`wb.save("output.pdf", SaveFormat.PDF)`)。  
- **创建响应式 HTML**，通过调整 `htmlOpts.setExportActiveWorksheetOnly` 和 `htmlOpts.setExportGridLines` 实现。  

所有这些功能的使用模式相同：配置一个 `*SaveOptions` 对象，打开相应的标志，然后调用 `Workbook.save`。

---

## 结论

你刚刚学习了如何在使用 Aspose.Cells for Java 将 **Excel 转换为 HTML** 并 **保存工作簿为 HTML** 的过程中 **嵌入字体**。关键步骤如下：

1. 加载或创建工作簿。  
2. 创建 `HtmlSaveOptions` 并启用 `setEmbedFonts(true)`。  
3. 使用这些选项调用 `Workbook.save`。

最终得到的是一个单一的、可移植的 HTML 文件，外观与原始电子表格完全一致——没有缺失的字体、没有额外的 CSS 文件，也不依赖客户端已安装的字体。

欢迎尝试字体子集化、选择性嵌入，甚至将其与服务器端缓存结合，以应对高并发场景。如果遇到异常（如文件意外过大或缺字形），请回顾本节中提到的可选设置并进行相应调整。

祝编码愉快，尽情享受现在可以直接从 Java 应用程序提供的像素级完美 HTML 吧！

## 接下来你可以学习什么？

以下教程与本指南的技术紧密相连，帮助你进一步掌握 API 的其他功能，并在项目中探索替代实现方案。每篇资源都包含完整的可运行代码示例和逐步解释。

- [使用 Aspose.Cells 将 Excel 转换为 HTML（Java）：分步指南](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [使用 Aspose.Cells for Java 导出 Excel 为 HTML：完整指南](/cells/english/java/workbook-operations/export-excel-to-html-aspose-cells-java/)
- [使用 IStreamProvider 与 Aspose.Cells for Java 导出 Excel 为 HTML：综合指南](/cells/english/java/workbook-operations/export-excel-html-streamprovider-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}