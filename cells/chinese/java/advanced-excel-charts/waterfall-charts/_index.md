---
date: 2026-09-02
description: 了解如何在 Java 中使用 Aspose.Cells 创建 excel 瀑布图，设置图表数据范围，自定义标签并导出为 XLSX。
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: 瀑布图
og_description: 使用 Aspose.Cells for Java 创建 excel 瀑布图——设置图表数据范围，添加数据标签，并在几步内导出为 XLSX。
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: 使用 Aspose.Cells for Java 创建 excel 瀑布图
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: 使用 Aspose.Cells for Java 创建 excel 瀑布图
url: /zh/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 瀑布图

## 使用 Aspose.Cells for Java 的瀑布图简介

在本教程中，您将学习如何使用 Aspose.Cells for Java **创建 Excel 瀑布图** 和 **设置图表数据范围**。瀑布图将一系列正负数字转换为清晰的可视化故事，使其非常适合财务报表、销售业绩评估以及任何需要查看各项对总计贡献的场景。

## 快速答案
- **What is a waterfall chart?** **什么是瀑布图？** 一个可视化图表，展示初始值如何通过一系列中间值的增加和减少，最终得到总计。  
- **Which library is used?** **使用哪个库？** Aspose.Cells for Java。  
- **Do I need a license?** **我需要许可证吗？** 免费试用可用于开发；生产环境需要商业许可证。  
- **Can I save the file as XLSX?** **我可以将文件保存为 XLSX 吗？** 可以 – 使用 `workbook.save("FileName.xlsx")`。  
- **Is it suitable for Java data visualization?** **它适合 Java 数据可视化吗？** 绝对适合；Aspose.Cells 提供丰富的图表功能，无需安装 Office。

## 什么是瀑布图？
瀑布图显示对起始值的连续正负贡献，帮助您了解每个组件如何影响整体结果。通过并排可视化收益和损失，复杂的财务流动一目了然。

## 为什么使用 Aspose.Cells for Java 添加瀑布图？
Aspose.Cells 让您在任何服务器、CI 管道或桌面上生成 Excel 图表，无需 Microsoft Excel。它支持 **15+ 输出格式**（XLSX、PDF、HTML、CSV 等），在不到一秒的时间内处理 **500+ 行** 的工作簿，并提供对每个图表元素的编程控制——从颜色到数据标签。

## 前提条件

在深入代码之前，请确保您已具备以下前提条件：

- Aspose.Cells for Java：您需要安装 Aspose.Cells for Java。可从 Aspose.Cells for Java 发布页面下载：[Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/)。  
- Java 开发环境：确保系统已安装 Java，并准备好构建工具（Maven/Gradle）。

现在，让我们一步步开始创建瀑布图。

## 如何在 Java 中设置瀑布图的图表数据范围
加载一个新工作簿，填充数据，添加 `Chart` 对象，定义系列范围，最后保存文件。该过程非常直接：创建工作簿，填充类别和数值单元格，创建图表，绑定数据范围，然后导出工作簿。结果是一个功能完整的瀑布图，可用于报告或仪表板。

### 步骤 1：导入 Aspose.Cells
`com.aspose.cells` 包含所有进行 Excel 操作所需的类，包括工作簿创建、工作表处理和图表生成。

### 步骤 2：初始化工作簿和工作表
**Workbook** 表示一个 Excel 文件，**Worksheet** 是该文件中的单个工作表。创建这些对象为原始数据和图表提供画布。

### 步骤 3：输入数据
列 A 保存类别标签，列 B 包含瀑布图的数值。此布局符合财务分析中常见的损益流。

### 步骤 4：创建瀑布图
**Chart** 对象用于生成可视化表示；将其类型设置为 `ChartType.WATERFALL` 即可配置为瀑布图。使用 `add` 方法为系列设置数据范围（`"B2:B6"`），并将类别轴链接到 `"A2:A6"`。

### 步骤 5：保存工作簿
保存工作簿会将图表和数据写入指定的文件格式。调用 `workbook.save("WaterfallChart.xlsx")` 生成 XLSX 文件，或更改格式参数以导出为 PDF、CSV 或 HTML。

## 常见问题及解决方案

- **Chart appears blank** **图表为空白** – 验证数据范围引用（`B2:B6` 和 `A2:A6`）是否与实际包含数值和类别的单元格匹配。  
- **Negative values not displayed correctly** **负值显示不正确** – 确保系列类型设置为 `ChartType.WATERFALL`；其他图表类型对负值的处理方式不同。  
- **File not opening in Excel** **文件无法在 Excel 中打开** – 使用最新的 Aspose.Cells 版本，并确认文件扩展名与格式匹配（Excel 使用 `.xlsx`）。

## 常见问答

### 如何自定义我的瀑布图外观？
您可以修改属性，例如 `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` 来更改柱形颜色，使用 `setShowDataLabels(true)` 启用数据标签，并通过 `getCategoryAxis().setTitle("Stage")` 调整轴标题。Aspose.Cells API 参考提供了完整的可定制选项列表。

### 我可以在同一工作表中创建多个瀑布图吗？
可以。添加第一个图表后，使用不同的数据范围和新的 `Chart` 对象重复图表创建步骤。每个图表相互独立，可放置在工作表的任意位置。

### Aspose.Cells 是否兼容不同的 Java 开发环境？
完全兼容。该库可在 Eclipse、IntelliJ IDEA、NetBeans 以及任何支持 Maven 或 Gradle 的构建系统中使用，无需额外插件。

### 我可以向我的瀑布图添加额外的数据系列吗？
可以，通过调用 `chart.getNSeries().add("C2:C6", true)` 并分别配置每个系列来添加更多系列。这使您能够并排比较多个情景。

### 在哪里可以找到更多 Aspose.Cells for Java 的资源和示例？
请访问完整文档：Aspose.Cells Java API 参考 [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/)。

## 常见问题

**Q: How do I set the chart data range for a financial waterfall chart?**  
**问：如何为财务瀑布图设置图表数据范围？**  
A: 使用图表系列的 `add` 方法，传入包含数值的单元格范围，例如 `"B2:B6"`。

**Q: Can I export the workbook to PDF instead of XLSX?**  
**问：我可以将工作簿导出为 PDF 而不是 XLSX 吗？**  
A: 可以，调用 `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` 生成 PDF 版本。

**Q: What if I need to create a waterfall chart with more categories?**  
**问：如果需要创建包含更多类别的瀑布图怎么办？**  
A: 扩展数值列和类别列的范围，然后相应更新 `add` 和 `setCategoryData` 调用。

**Q: Is there a way to automatically format positive and negative bars?**  
**问：有没有办法自动为正负柱形设置格式？**  
A: 遍历 `Series` 集合，根据每个值的正负设置 `FillFormat` 颜色；Aspose.Cells 允许以编程方式应用条件格式。

**Q: Does Aspose.Cells support dynamic data updates for charts?**  
**问：Aspose.Cells 是否支持图表的数据动态更新？**  
A: 支持。修改单元格值后，只需重新保存工作簿——图表会自动反映新数据。

---

**Last Updated:** 2026-09-02  
**Tested with:** Aspose.Cells for Java (latest)  
**Author:** Aspose  

```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## 相关教程

- [使用 Aspose.Cells for Java 自定义 Excel 图表数据标签：分步指南](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [使用 Aspose.Cells Java 为 Excel 图表添加数据标签](/cells/java/advanced-excel-charts/chart-interactivity/)
- [使用 Aspose.Cells 在 Java 中创建并导出图表：完整指南](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}