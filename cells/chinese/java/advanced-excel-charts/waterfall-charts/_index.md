---
date: 2025-12-10
description: 了解如何使用 Aspose.Cells 在 Java 中创建瀑布图。一步步指南教您将图表添加到工作表、进行自定义，并将工作簿保存为 XLSX。
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: 如何使用 Aspose.Cells for Java 创建瀑布图
url: /zh/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 瀑布图

## 使用 Aspose.Cells for Java 的瀑布图简介

在本教程中，您将学习如何使用 Aspose.Cells for Java **创建瀑布图**。瀑布图是数据可视化中的重要工具，因为它们可以让您看到一系列正负值的累计效果。无论是编制财务报表、销售绩效报告，还是其他数据驱动的分析，瀑布图都能将原始数字转化为清晰、可操作的洞见。

## 快速答疑
- **什么是瀑布图？** 一种可视化方式，展示初始值如何通过一系列中间值的增加和减少，最终得到总计值。  
- **使用哪个库？** Aspose.Cells for Java。  
- **需要许可证吗？** 免费试用可用于开发；生产环境需要商业许可证。  
- **可以将文件保存为 XLSX 吗？** 可以 – 使用 `workbook.save("FileName.xlsx")`。  
- **适合 Java 数据可视化吗？** 绝对适合；Aspose.Cells 提供丰富的图表功能，无需安装 Office。

## 什么是瀑布图？
瀑布图显示对起始值的连续正向和负向贡献，帮助您了解每个组成部分如何影响整体结果。

## 为什么使用 Aspose.Cells for Java 添加瀑布图？
- **无需 Microsoft Excel** – 可在任何服务器或 CI 流水线生成图表。  
- **完全控制格式** – 颜色、数据标签和坐标轴均可通过代码自定义。  
- **支持多种输出格式** – XLSX、PDF、HTML 等。  
- **高性能** – 适用于大型工作簿和自动化报表。

## 前置条件

在深入代码之前，请确保已具备以下前置条件：

- Aspose.Cells for Java：您需要安装 Aspose.Cells for Java。可从 [here](https://releases.aspose.com/cells/java/) 下载。

- Java 开发环境：确保系统已安装 Java。

现在，让我们一步步开始创建瀑布图。

## 如何在 Java 中创建瀑布图

### 步骤 1：导入 Aspose.Cells

```java
import com.aspose.cells.*;
```

首先，需要将 Aspose.Cells 库导入到您的 Java 项目中。该库提供了处理 Excel 文件的广泛功能，包括图表创建。

### 步骤 2：初始化 Workbook 和 Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

创建一个新的工作簿并向其中添加工作表。我们将在此工作表中输入数据并 **向工作表添加图表**。

### 步骤 3：输入数据

现在，让我们在工作表中填充要在瀑布图中展示的数据。

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

在本示例中，类别位于 A 列，对应的数值位于 B 列。您可以将这些数据替换为自己的数据集。

### 步骤 4：创建瀑布图

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

我们已在工作表中添加了瀑布图，指定了数据系列和类别数据。这一步是 **向工作表添加瀑布图** 的核心。您可以使用 `Chart` 对象的属性进一步自定义图表外观（颜色、数据标签等）。

###骤 5：保存工作簿

```java
workbook.save("WaterfallChart.xlsx");
```

将工作簿保存为文件。示例使用 XLSX 格式，但 Aspose.Cells 也支持导出为 PDF、CSV 等多种格式。这满足了 **保存工作簿为 xlsx** 的需求。

## 常见问题及解决方案

- **图表显示为空白** – 请确认数据范围引用 (`B2:B6` 和 `A2:A6`) 与实际包含数值和类别的单元格匹配。  
- **负值未正确显示** – 确保系列类型设置为 `ChartType.WATERFALL`；其他图表类型对负值的处理方式不同。  
- **文件在 Excel 中无法打开** – 请确保使用的是最新版本的 Aspose.Cells（最新发布），并且文件扩展名与格式匹配（`.xlsx` 对应 Excel）。

## 常见问答

### 如何自定义我的瀑布图外观？

您可以通过修改颜色、数据标签和坐标轴标签等属性来自定义瀑布图外观。详细指南请参阅 Aspose.Cells 文档。

### 能在同一工作表中创建多个瀑布图吗？

可以，按照相同步骤使用不同的数据范围即可在同一工作表中创建多个瀑布图。

### Aspose.Cells 是否兼容不同的 Java 开发环境？

是的，Aspose.Cells for Java 兼容多种 Java 开发环境，包括 Eclipse、IntelliJ IDEA 和 NetBeans。

### 能向我的瀑布图添加额外的数据系列吗？

当然，您可以向瀑布图添加更多数据系列，以有效表示复杂的数据场景。

### 在哪里可以找到更多 Aspose.Cells for Java 的资源和示例？

您可以访问 Aspose.Cells for Java 的文档页面 [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) 获取深入信息和代码示例。

---

**最后更新：** 2025-12-10  
**测试环境：** Aspose.Cells for Java 24.12（最新）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}