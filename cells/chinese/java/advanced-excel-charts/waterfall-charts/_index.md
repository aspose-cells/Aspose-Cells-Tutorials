---
date: 2026-02-16
description: 学习如何在 Java 中使用 Aspose.Cells 设置图表数据范围并创建瀑布图。一步步指南，教您添加数据系列图表、进行自定义以及导出为
  XLSX。
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: 设置图表数据范围 – Aspose.Cells for Java 瀑布图
url: /zh/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 瀑布图

## 使用 Aspose.Cells for Java 的瀑布图简介

在本教程中，您将学习如何 **set chart data range** 并使用 Aspose.Cells for Java 创建 **waterfall chart**。瀑布图是数据可视化中的重要工具，因为它们可以让您看到一系列正负值的累计效果。无论是编制财务报表、销售业绩报告，还是其他数据驱动的分析，瀑布图都能将原始数字转化为清晰、可操作的洞察。

## 快速答案
- **What is a waterfall chart?** 一个可视化图表，展示初始值如何通过一系列中间值的增加和减少，最终得到总计。  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** 免费试用可用于开发；生产环境需要商业许可证。  
- **Can I save the file as XLSX?** 是的 – 使用 `workbook.save("FileName.xlsx")`。  
- **Is it suitable for Java data visualization?** 绝对适合；Aspose.Cells 提供丰富的图表功能，无需安装 Office。

## 什么是瀑布图？

瀑布图显示对起始值的连续正负贡献，帮助您了解每个组成部分如何影响整体结果。

## 为什么使用 Aspose.Cells for Java 添加瀑布图？

- **No Microsoft Excel required** – 在任何服务器或 CI 流水线生成图表。  
- **Full control over formatting** – 颜色、数据标签和坐标轴可通过编程自定义。  
- **Supports multiple output formats** – 支持 XLSX、PDF、HTML 等多种输出格式。  
- **High performance** – 适用于大型工作簿和自动化报告。

## 前提条件

在深入代码之前，请确保已具备以下前提条件：

- Aspose.Cells for Java: 您需要安装 Aspose.Cells for Java。可从 [here](https://releases.aspose.com/cells/java/) 下载。  
- Java Development Environment: 确保系统已安装 Java。

现在，让我们一步步开始创建瀑布图。

## 如何在 Java 中设置瀑布图的图表数据范围

### 步骤 1：导入 Aspose.Cells

```java
import com.aspose.cells.*;
```

首先，需要将 Aspose.Cells 库导入到 Java 项目中。该库提供了处理 Excel 文件的广泛功能，包括图表创建。

### 步骤 2：初始化 Workbook 和 Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

创建一个新的 workbook 并向其添加 worksheet。我们将使用此 worksheet 输入数据并 **add chart to worksheet**。

### 步骤 3：输入数据

现在，让我们在 worksheet 中填充要在瀑布图中展示的数据。

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

在本示例中，类别位于 A 列，对应的数值在 B 列。您可以将这些数据替换为自己的数据集。

### 步骤 4：创建瀑布图

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

我们已在 worksheet 中添加了瀑布图，并指定了数据系列和类别数据。这是 **adds waterfall chart** 到工作表的核心步骤。请注意 `add` 方法使用的范围 `"B2:B6"` —— 这就是我们为系列 **set chart data range** 的位置。您可以使用 `Chart` 对象的属性进一步自定义图表外观（颜色、数据标签等）。

### 步骤 5：保存 Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

将 workbook 保存为文件。示例使用 XLSX 格式，但 Aspose.Cells 还允许您 **export excel pdf java**‑兼容的文件，如 PDF、CSV 等多种格式。这满足了 **save workbook xlsx** 的需求。

## 常见问题及解决方案

- **Chart appears blank** – 验证数据范围引用 (`B2:B6` 和 `A2:A6`) 是否与实际包含数值和类别的单元格匹配。  
- **Negative values not displayed correctly** – 确保系列类型设置为 `ChartType.WATERFALL`；其他图表类型对负值的处理不同。  
- **File not opening in Excel** – 确保使用的是最新版本的 Aspose.Cells（最新发布），并且文件扩展名与格式匹配（Excel 使用 `.xlsx`）。

## 常见问答

### 如何自定义我的瀑布图外观？

您可以通过修改颜色、数据标签和坐标轴标签等属性来自定义瀑布图的外观。请参阅 Aspose.Cells 文档获取详细指南。

### 我可以在同一 worksheet 中创建多个瀑布图吗？

是的，您可以在同一 worksheet 中通过使用不同的数据范围重复相同步骤来创建多个瀑布图。

### Aspose.Cells 是否兼容不同的 Java 开发环境？

是的，Aspose.Cells for Java 与多种 Java 开发环境兼容，包括 Eclipse、IntelliJ IDEA 和 NetBeans。

### 我可以向我的瀑布图添加额外的数据系列吗？

当然，您可以向瀑布图添加更多数据系列，以有效表示复杂的数据场景。这是一个如何以编程方式 **add data series chart** 的示例。

### 在哪里可以找到更多 Aspose.Cells for Java 的资源和示例？

您可以在 [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) 查看 Aspose.Cells for Java 的文档，获取深入信息和代码示例。

## 常见问题

**Q: 如何为财务瀑布图设置图表数据范围？**  
A: 在图表的 series 上使用 `add` 方法，传入包含数值的单元格范围，例如 `"B2:B6"`。

**Q: 我可以将 workbook 导出为 PDF 而不是 XLSX 吗？**  
A: 可以，调用 `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` 即可生成 **export excel pdf java**‑兼容的输出。

**Q: 如果需要创建包含更多类别的财务瀑布图怎么办？**  
A: 将数值列和类别列的数据范围都扩展，然后相应地更新 `add` 和 `setCategoryData` 调用。

**Q: 有办法自动为正负柱形设置格式吗？**  
A: 您可以遍历 `Series` 集合，根据每个数值的正负设置 `FillFormat` 的颜色。

**Q: Aspose.Cells 是否支持图表的动态数据更新？**  
A: 可以，在图表创建后修改单元格数值；保存 workbook 时图表会反映这些更改。

---

**最后更新：** 2026-02-16  
**测试环境：** Aspose.Cells for Java（最新）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}