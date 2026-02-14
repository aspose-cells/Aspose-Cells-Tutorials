---
date: 2026-02-14
description: 学习如何使用 Aspose.Cells for Java 将图表导出为 PNG、添加数据系列、合并折线柱状图、将工作簿保存为 XLSX 并添加图例。
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: 将图表导出为 PNG 并为组合图添加数据系列
url: /zh/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

Tested With:" translate.

"Author:" translate.

Close shortcodes.

Now produce final content.

Be careful to keep markdown syntax.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 将图表导出为 PNG 并为组合图添加数据系列

在本教程中，您将 **添加数据系列** 到 Excel 工作簿，**组合折线图和柱形图** 元素，并学习如何使用 Aspose.Cells for Java **将图表导出为 PNG**。我们将逐步演示——从设置工作簿、向工作表添加图表、定制图例，到 **将工作簿另存为 xlsx** 并生成图表的 PNG 图像。完成后，您将拥有一个可直接嵌入报告或仪表盘的组合图表。

## 快速答案
- **哪个库可以创建组合图表？** Aspose.Cells for Java  
- **如何添加数据系列？** 使用 `chart.getNSeries().add(...)`  
- **如何将图表导出为 png？** 调用 `chart.toImage("file.png", ImageFormat.getPng())`  
- **工作簿可以保存为何种文件格式？** 标准 `.xlsx`（将工作簿另存为 xlsx）  
- **生产环境是否需要许可证？** 需要有效的 Aspose.Cells 许可证  

## 什么是 Aspose.Cells 中的 **export chart to PNG**？
将图表导出为 PNG 会生成 Excel 图表的光栅图像，可在网页、报告或电子邮件中显示，而无需 Excel 应用程序。

## 为什么要创建 **combined line column chart**？
组合图表允许您在同一视图中使用不同的可视化方式展示不同的数据集（例如，在柱形图上叠加折线系列）。这非常适合比较趋势与总量、突出相关性，或在紧凑的格式中提供更丰富的洞察。

## 前置条件
- Java Development Kit (JDK) 8 或更高  
- Aspose.Cells for Java 库（从下面的链接下载）  
- 对 Java 语法和 Excel 概念有基本了解  

## 入门指南

首先，从官方网站下载 Aspose.Cells for Java 库：

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

将 JAR 添加到项目的类路径后，即可开始构建图表。

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

### 步骤 4：向工作表添加组合图表对象  
我们将先创建折线图，然后再添加柱形系列，以实现 **combined line column chart** 效果。
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 向图表添加数据

现在图表容器已经存在，需要为其提供数据。

### 步骤 5：定义数据范围并 **添加数据系列**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **小贴士：** 第一个参数（`"A1:A5"`）是第一系列的范围，第二个参数（`"B1:B5"`）则创建第二系列，随后会与第一系列组合。

### 步骤 6：设置类别（X 轴）数据
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## 定制图表

一个好的图表能够讲述故事。让我们为其添加标题、坐标轴标签和清晰的图例。

### 步骤 7：**设置图表坐标轴标签** 和标题
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 步骤 8：**添加图例** 并调整其位置
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## 保存与导出图表

定制完成后，您需要 **将工作簿另存为 xlsx** 并生成图像。

### 步骤 9：将工作簿保存为 Excel 文件（xlsx）
```java
workbook.save("CombinedChart.xlsx");
```

### 步骤 10：**将图表导出为 PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` 方法 **生成 Excel 图表** 图像，可用于网页、报告或电子邮件。

## 常见问题与故障排除

| 问题 | 解决方案 |
|-------|----------|
| **未显示数据** | 确认单元格范围（`A1:A5`、`B1:B5`、`C1:C5`）在创建图表前已包含数据。 |
| **图例与图表重叠** | 设置 `chart.getLegend().setOverlay(false)` 或将图例移动到其他位置（例如 `RIGHT`）。 |
| **生成的图像为空白** | 确保图表至少有一个系列，并在所有定制完成后调用 `chart.toImage`。 |
| **保存时抛出异常** | 检查目标目录的写入权限，并确保文件未在 Excel 中打开。 |

## 常见问答

**Q: 如何安装 Aspose.Cells for Java？**  
A: 从官方网站下载 JAR 并将其添加到项目的类路径。下载链接为：[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)。

**Q: 除了折线图和柱形图，我还能创建其他图表类型吗？**  
A: 可以，Aspose.Cells 支持条形图、饼图、散点图、面积图等多种图表类型。请参阅 API 文档获取完整列表。

**Q: 生产环境是否需要许可证？**  
A: 生产部署必须使用有效的 Aspose.Cells 许可证。可获取免费试用版进行评估。

**Q: 如何更改每个系列的颜色？**  
A: 在添加系列后使用 `chart.getNSeries().get(i).setAreaColor(Color.getRed())`（或类似方法）进行设置。

**Q: 在哪里可以找到更多代码示例？**  
A: 完整文档和更多示例可在 Aspose 参考站点获取：[here](https://reference.aspose.com/cells/java/)。

---

**最后更新：** 2026-02-14  
**测试环境：** Aspose.Cells for Java 最新版本  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}