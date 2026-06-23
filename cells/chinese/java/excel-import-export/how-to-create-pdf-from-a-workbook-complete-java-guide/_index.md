---
category: general
date: 2026-03-01
description: 如何使用 Aspose.Cells for Java 创建 PDF 并将工作簿保存为 PDF，导出 Excel 为 HTML，以及使用 expand
  功能。包含逐步代码示例。
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: zh
og_description: 如何使用 Aspose.Cells for Java 将工作簿创建为 PDF。了解如何将工作簿保存为 PDF、将 Excel 导出为
  HTML，以及使用 EXPAND 函数。
og_title: 如何从工作簿创建 PDF – Java 教程
tags:
- Aspose.Cells
- Java
- PDF generation
title: 如何从工作簿创建 PDF – 完整的 Java 指南
url: /zh/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何从工作簿创建 PDF – 完整 Java 指南

是否曾想过 **how to create PDF** 直接从 Excel 工作簿创建 PDF，而无需使用第三方转换器？你并不孤单。许多开发者在需要快速 PDF 导出、HTML 预览或高级数组公式时会遇到困难——一次性完成。  

在本教程中，我们将演示一个完整的、独立的 Java 程序来实现这些功能。我们会 **save workbook as PDF**，展示如何 **export Excel to HTML** 并保持冻结行，以及演示在工作表中 **use expand function** 的用法。完成后，你将拥有一个可直接放入任何 Maven 或 Gradle 构建的可运行项目。

> **Pro tip:** 以下所有代码均适用于 Aspose.Cells 23.10（或更高版本）。如果使用的是更旧的版本，某些方法名称可能会略有不同。

---

## 前提条件

- **Java 17**（或任何 LTS 版本）已安装并配置好。
- **Aspose.Cells for Java** 库。将以下 Maven 依赖添加到你的 `pom.xml` 中：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- 你喜欢的 IDE 或文本编辑器（IntelliJ IDEA、VS Code、Eclipse …）。

没有外部 API，没有 Web 服务——仅使用纯 Java 和 Aspose.Cells SDK。

---

## 解决方案概览

我们将实现过程划分为 **七个逻辑步骤**：

1. 创建工作簿并演示 **EXPAND** 函数。  
2. 启用字体变体选择器并 **save workbook as PDF**。  
3. 将同一工作簿导出为 HTML，同时保留冻结行。  
4. 使用带 `IF` 参数的 Smart Marker 注入条件文本。  
5. 使用主从 Smart Marker 处理层级数据。  
6. 加载包含 Base‑64 编码图片的 Markdown 文件。  
7. 配置 GridJs 选项以实现对齐和边框，然后插入数据。

每个步骤都封装在单独的方法中，以保持 `main` 方法简洁，并说明 **为什么** 要这么做，而不仅仅是 **做了什么**。

---

## 第一步 – 创建工作簿并使用 EXPAND 函数

**EXPAND** 函数是 Office 365 中引入的新动态数组公式。它可以将一个范围“溢出”到更大的区域，而无需手动复制单元格。

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**为什么这很重要：**  
- `EXPAND` 会自动用空白填充结果，这在后续 **save workbook as PDF** 时非常有用——PDF 将呈现一个整齐的矩形表格。  
- 调用 `calculateFormula()` 可确保在导出之前公式引擎已计算完成。

---

## 第二步 – 启用字体变体选择器并 **Save Workbook as PDF**

如果需要支持高级排版（例如表情符号或中日韩变体选择器），必须在保存之前打开此功能。

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**关键点：** 这里回答了主要关键词 **how to create pdf**——通过在配置完设置后调用 `workbook.save(..., SaveFormat.PDF)` 实现。

---

## 第三步 – **Export Excel to HTML** 同时保留冻结行

经常有利益相关者需要快速的网页预览。Aspose.Cells 可以导出为 HTML，并通过 `setPreserveFrozenRows(true)` 保持与 Excel 相同的滚动体验。

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**为什么在意：** 冻结行是可用性提升；如果没有它们，页面向下滚动时表头行会消失。

---

## 第四步 – 带 IF‑参数的 Smart Marker

Smart Marker 让你在模板中合并数据而无需编写循环。`if` 参数直接在标记内部加入条件逻辑。

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

输出的 PDF 将显示 **“VIP Customer: Acme Corp”**，因为 `IsVIP` 为 `true`。将该标志改为 `false` 则会得到 **“Regular Customer: Acme Corp”**——无需额外代码。

---

## 第五步 – 使用层级范围的 Master‑Detail Smart Marker

当你拥有父子数据（例如订单及其明细）时，master‑detail 标记可以省去手动插入行的工作。

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**你得到的收益：** 引擎会为每个订单展开主行，并自动在其下嵌套明细行——非常适合发票或采购报告。

---

## 第六步 – 加载带嵌入 Base‑64 图片的 Markdown 文档

如果你的源数据以 Markdown 形式存在（在文档流水线中很常见），Aspose.Cells 能直接将其渲染到工作簿中。

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**边缘情况说明：** 若 Base‑64 字符串格式错误，Aspose 会跳过该图片但继续处理文档的其余部分——不会崩溃。

---

## 第七步 – 配置 GridJs 选项并插入数据

GridJs 是 Aspose 可以渲染为 HTML 的轻量级 JavaScript 表格。对数字进行对齐并添加边框可提升可读性。

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**为什么在意：** 正确的对齐和边框让生成的 HTML 看起来像一个精致的电子表格——非常适合仪表盘展示。

---

## 综合示例 – `main` 方法

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}