---
date: 2025-12-06
description: 了解如何添加数据系列、创建组合图表类型、使用 Aspose.Cells for Java 将工作簿保存为 Excel 并将图表导出为 PNG。
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: 使用 Aspose.Cells 添加数据系列以创建组合图表
url: /zh/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 添加数据系列以使用 Aspose.Cells 创建组合图表

在本教程中，您将 **添加数据系列** 到 Excel 工作簿，并学习如何使用 Aspose.Cells for Java **创建组合图表** 类型。我们将逐步演示所有步骤——从设置工作簿、添加系列、定制图例，到 **保存工作簿 Excel** 文件并导出 **图表为 PNG**。完成后，您将拥有一个可直接嵌入报告或仪表板的组合图表。

## 快速答案
- **哪个库可以创建组合图表？** Aspose.Cells for Java  
- **如何添加数据系列？** 使用 `chart.getNSeries().add(...)`  
- **可以将图表导出为图片吗？** 可以，使用 `chart.toImage(...)`（PNG）  
- **工作簿可以保存为什么文件格式？** 标准 `.xlsx`（Excel）  
- **生产环境需要许可证吗？** 需要有效的 Aspose.Cells 许可证  

## 什么是 Aspose.Cells 中的 **add data series**？
添加数据系列告诉图表哪些单元格包含您想要绘制的数值。每个系列可以表示折线、柱形或其他任何图表类型，您可以将它们混合使用以构建 **组合图表**。

## 为什么要创建 **组合图表**？
组合图表允许您在同一视图中使用不同的视觉表现形式显示不同的数据集（例如，在柱形图上叠加折线系列）。这非常适合比较趋势与总量、突出相关性，或在紧凑的格式中提供更丰富的洞察。

## 前置条件
- Java Development Kit (JDK) 8 或更高版本  
- Aspose.Cells for Java 库（从下方链接下载）  
- 基本的 Java 语法和 Excel 概念了解  

## 入门指南

首先，从官方网站下载 Aspose.Cells for Java 库：

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

将 JAR 添加到项目的 classpath 后，即可开始构建图表。

### 步骤 1：导入 Aspose.Cells 类
```java
import com.aspose.cells.*;
```

### 步骤 2：创建新工作簿
```java
Workbook workbook = new Workbook();
```

### 步骤 3：访问第一个工作表
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 步骤 4：添加组合图表对象  
我们将先创建折线图，然后再添加其他系列以实现 **组合图表** 效果。
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 向图表添加数据

现在图表容器已经存在，需要为其提供数据。

### 步骤 5：定义数据范围并 **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **小贴士：** 第一个参数（`"A1:A5"`）是第一系列的范围，第二个参数（`"B1:B5"`）则创建第二系列，这两个系列将被组合在一起。

### 步骤 6：设置类别（X 轴）数据
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## 定制图表

一个好的图表能够讲述故事。让我们为它添加标题、轴标签和清晰的图例。

### 步骤 7：设置图表标题和轴标签
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 步骤 8：**Add legend chart** 并调整其位置
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## 保存与导出图表

定制完成后，您需要 **保存工作簿 Excel** 并生成图像。

### 步骤 9：将工作簿保存为 Excel 文件
```java
workbook.save("CombinedChart.xlsx");
```

### 步骤 10：导出 **chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` 方法 **生成 excel chart** 图像，可用于网页、报告或电子邮件。

## 常见问题与故障排除

| 问题 | 解决方案 |
|------|----------|
| **没有数据显示** | 确认单元格范围（`A1:A5`、`B1:B5`、`C1:C5`）在创建图表前确实包含数据。 |
| **图例覆盖图表** | 设置 `chart.getLegend().setOverlay(false)` 或将图例移动到其他位置（例如 `RIGHT`）。 |
| **生成的图像文件为空白** | 确保图表至少有一个系列，并且在所有定制完成后再调用 `chart.toImage`。 |
| **保存时抛出异常** | 检查目标目录的写权限，并确保文件未在 Excel 中打开。 |

## 常见问答

**问：如何安装 Aspose.Cells for Java？**  
答：从官方网站下载 JAR 并将其添加到项目的 classpath。下载链接为：[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)。

**问：除了折线图和柱形图，还能创建其他图表类型吗？**  
答：可以，Aspose.Cells 支持条形图、饼图、散点图、面积图等多种图表类型。请参考 API 文档获取完整列表。

**问：生产环境是否需要许可证？**  
答：生产部署需要有效的 Aspose.Cells 许可证。提供免费试用供评估使用。

**问：如何更改每个系列的颜色？**  
答：在添加系列后使用 `chart.getNSeries().get(i).setAreaColor(Color.getRed())`（或其他颜色）进行设置。

**问：在哪里可以找到更多代码示例？**  
答：完整文档和更多示例可在 Aspose 参考站点获取：[here](https://reference.aspose.com/cells/java/)。

---

**最后更新：** 2025-12-06  
**测试环境：** Aspose.Cells for Java 24.12  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
