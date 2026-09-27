---
date: '2026-09-27'
description: 学习如何使用 Aspose.Cells 创建 Java pie chart。一步步指南，定制 Excel pie chart，设置 Maven
  依赖，并生成专业图表。
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: 使用 Aspose.Cells for Java 创建 Java pie chart。学习定制 Excel pie chart，添加
  Maven 依赖，并在几分钟内生成专业图表。
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: 使用 Aspose.Cells 创建 Java pie chart – 完整 Java 指南
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: 如何使用 Aspose.Cells 创建 Java pie chart
url: /zh/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 创建 Java 饼图

## 介绍
以编程方式创建 **pie chart** 往往像解谜一样，尤其是当你需要对颜色、图例和标题进行细粒度控制时。在本指南中，你将学习如何使用 Aspose.Cells **create pie chart java**，然后自定义 Excel 饼图以匹配你的品牌或报告风格。我们将逐步演示环境设置、数据填充、图表生成以及视觉微调——全部在你的 Java IDE 中完成。

**您将学习**
- 将 **Maven 依赖 Aspose.Cells** 添加到项目中。
- 构建工作簿，填充单元格数据，并生成 pie chart。
- 为图表应用自定义颜色、标题和图例。
- 将工作簿导出为可共享的 XLSX 文件。

在开始之前，你应熟悉基本的 Java 语法，并已安装 Maven 或 Gradle。

## 快速答案
- **哪个库可以在 Java 中创建 pie chart？** Aspose.Cells for Java。  
- **我需要许可证吗？** 免费试用可用于开发；生产环境需要付费许可证。  
- **需要哪些 Maven 坐标？** `com.aspose:aspose-cells:24.10`。  
- **我可以更改切片颜色吗？** 可以，通过每个系列的 `setAreaColor` 方法。  
- **图表可以导出为 XLSX 吗？** 当然——只需调用 `workbook.save("output.xlsx")`。

## 什么是 Excel 中的 pie chart？
pie chart 将单一数据系列可视化为圆形的比例切片，便于比较整体中的各部分。每个切片的角度对应其相对于总值的大小，从而快速洞察如市场份额、预算分配或人口比例等类别的分布。

## 为什么使用 Aspose.Cells 创建 Java pie chart？
Aspose.Cells 支持超过 50 种图表类型，并且能够在不将整个文件加载到内存的情况下处理高达一百万行的工作表。这一性能优势使你能够在普通硬件上生成大型报告，同时提供对图表外观、数据绑定和导出格式的细粒度控制，是许多开源库的优越选择。

## 前置条件
- **Java Development Kit (JDK)** 8 或更高。  
- **IDE** 如 IntelliJ IDEA 或 Eclipse。  
- **Maven** 或 **Gradle** 用于依赖管理。  
- 一个 **试用或已购买的 Aspose.Cells 许可证**。

### 所需库和依赖
将 Aspose.Cells Maven 构件添加到你的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

或使用 Gradle 等价方式：

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### 许可证获取步骤
Aspose.Cells for Java 为商业产品，但你可以先使用免费试用。访问 [购买页面](https://purchase.aspose.com/buy) 获取临时许可证密钥。

## 设置 Aspose.Cells for Java
首先，确保库已在类路径中。添加依赖后，你可以按下面的示例初始化 API。

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## 实现指南

### 创建并配置工作簿
`Workbook` 类在内存中表示整个 Excel 文件。

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### 步骤 1：实例化工作簿
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
这将创建一个全新的空工作簿，你可以立即开始填充数据。

### 访问或修改工作表单元格
`Worksheet` 表示工作簿中的单个工作表，包含单元格、行和列。  
你将把驱动 pie chart 的数据写入工作表。

#### 步骤 2：获取第一个工作表及其单元格
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
将类别名称和数值填入单元格，供图表使用。

### 创建 pie chart
`Chart` 对象可在工作表中可视化数据，支持包括 pie、column、line 等多种类型。

#### 步骤 3：向工作表添加 pie chart
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### 配置 pie chart 系列和数据
`Series` 定义图表的数据范围和格式，将工作表单元格链接到可视元素。

#### 步骤 4：为图表设置系列
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### 配置图表图例和标题外观
图表 `Legend` 显示系列名称和颜色，帮助读者识别每个切片。

#### 步骤 5：自定义图表图例和标题
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### 自定义图表系列颜色
`setAreaColor` 使用 RGB 值设置图表系列切片的填充颜色。

#### 步骤 6：更改 pie 部分颜色
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### 自动调整列宽并保存工作簿
`autoFitColumns` 自动根据单元格内容调整列宽。

#### 步骤 7：调整列宽并保存文件
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## 常见用例
- **人口统计分析：** 显示各地区的人口分布。  
- **市场份额报告：** 一目了然地可视化每个竞争者的份额。  
- **预算分配：** 突出显示资金在各部门之间的分配情况。

## 性能考虑
- 当对象不再需要时调用 `workbook.dispose()` 释放本机内存。  
- 对于海量数据集，使用 `WorkbookDesigner` 进行流式写入，而不是一次性加载全部数据。  
- 使用 Java Flight Recorder 进行性能分析，找出图表生成过程中的瓶颈。

## 常见问题

**Q: 我可以在同一个工作簿中生成多个 pie chart 吗？**  
A: 可以，对每个数据范围重复图表创建步骤；每个图表相互独立。

**Q: Aspose.Cells 支持 3‑D pie chart 吗？**  
A: 支持；在添加图表时将图表类型设为 `ChartType.PIE_3D`。

**Q: 如何为所有图表应用自定义主题？**  
A: 在创建任何图表之前，使用 `Workbook.setDefaultTheme` 方法。

**Q: 工作簿可以导出为哪些文件格式？**  
A: 超过 30 种格式，包括 XLSX、CSV、PDF 和 HTML。

**Q: 商业部署是否需要许可证？**  
A: 必须，合法许可证可去除评估水印并解锁全部功能。

## 结论
现在，你已经掌握了使用 Aspose.Cells **create pie chart java** 的完整端到端方案。按照上述步骤，你可以生成精美的 Excel 饼图，定制颜色和标题，并将其嵌入任何报告流程。进一步探索其他图表类型——柱形图、折线图、雷达图——以扩展你的数据可视化工具箱。

---

**Last Updated:** 2026-09-27  
**Tested with:** Aspose.Cells 24.10 for Java  
**Author:** Aspose

## 相关教程

- [使用 Aspose.Cells for Java 自定义 Excel 图表数据标签：一步一步指南](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [使用 Aspose.Cells Java 创建动态 Excel 图表：面向开发者的综合指南](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [使用 Aspose.Cells Java 创建并自定义 Excel 工作簿：一步一步指南](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}