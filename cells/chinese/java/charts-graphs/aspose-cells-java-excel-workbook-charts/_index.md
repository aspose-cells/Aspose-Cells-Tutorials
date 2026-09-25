---
date: '2026-04-11'
description: 学习使用 Aspose.Cells 进行 Excel 自动化（Java）。本教程展示了如何使用 Java 创建 Excel 工作簿、填充
  Excel 数据以及保存带图表的 Excel 文件。
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: Excel 自动化 Java：使用 Aspose 创建工作簿和图表
url: /zh/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel 自动化 Java：使用 Aspose 创建工作簿和图表

## 介绍

使用 Java 自动化 Excel 任务可以节省数小时的手动工作，尤其是在需要即时生成报告、仪表板或数据驱动的图表时。**Excel automation java** 与 Aspose.Cells 为您提供干净、高性能的 API，能够处理从工作簿创建到复杂图表样式的所有工作。在本教程中，您将学习如何设置 Aspose.Cells、**create an Excel workbook java**、填充数据、添加图表、应用 3‑D 格式，最后 **save the Excel file java**。

### 快速回答
- **哪个库简化了 Java 中的 Excel 自动化？** Aspose.Cells for Java.  
- **我可以以编程方式添加 3‑D 图表吗？** 是的——API 支持 3‑D 格式化和光照效果。  
- **开发是否需要许可证？** 提供免费试用许可证；生产环境需要商业许可证。  
- **支持哪些 Java 构建工具？** Maven 和 Gradle 均得到完整支持。  
- **可以导出哪些文件格式？** XLS、XLSX、CSV、PDF 等多种格式。

## 什么是 Excel 自动化 Java？

Excel automation java 指使用 Java 代码以编程方式生成、修改和保存 Excel 工作簿的过程。它消除手动电子表格编辑，确保一致性，并能够与数据库或 Web 服务等其他系统集成。

## 为什么使用 Aspose.Cells for Java？

- **丰富的功能集** – 从简单的单元格值到复杂的图表、数据透视表和条件格式化。  
- **无 Microsoft Office 依赖** – 可在任何服务器端环境运行。  
- **高性能** – 为大数据集和多线程场景进行优化。  
- **广泛的格式支持** – 读取/写入 XLS、XLSX、ODS、CSV、PDF、HTML 等多种格式。

## 先决条件

- **Java Development Kit (JDK) 8+**  
- **用于依赖管理的 Maven 或 Gradle**  
- **Aspose.Cells for Java 25.3 或更高版本**（试用或已授权）  

## 设置 Aspose.Cells for Java

使用以下任一配置将库添加到项目中。

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### 许可证获取

从 Aspose 网站请求免费试用许可证，或购买正式许可证用于生产。将许可证文件放置在项目中并在运行时加载。

## 基本初始化和设置

解析依赖后，即可开始编写代码。

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## 分步指南

### 步骤 1：如何创建 Excel 工作簿 Java

创建一个新的工作簿实例，用于容纳所有工作表。

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### 步骤 2：添加工作表（包括图表工作表）

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### 步骤 3：如何填充 Excel 数据 Java

插入示例数据，供图表引用。

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### 步骤 4：向工作簿添加柱形图

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### 步骤 5：对图表区域应用颜色格式

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### 步骤 6：配置图例和数据系列

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### 步骤 7：对系列应用 3D 格式

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### 步骤 8：设置系列颜色以获得更好的视觉区分

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### 步骤 9：如何保存 Excel 文件 Java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## 实际应用

- **财务报告** – 使用动态图表生成季度报表。  
- **数据分析仪表板** – 构建可自动刷新的交互式仪表板。  
- **库存管理** – 将库存水平和趋势导出到 Excel，供利益相关者审阅。  
- **项目规划** – 直接从基于 Java 的调度系统创建甘特图样式的图表。

## Excel 自动化 Java 性能技巧

- **重用 Workbook 对象** 在处理多张工作表时可降低内存消耗。  
- **批量单元格更新** 使用 `Cells.importArray` 处理大数据集，而非逐个调用 `putValue`。  
- **释放资源** 保存大文件后调用 `book.dispose()`。

## 常见问题

**Q: 我可以生成 XLSX 而不是 XLS 吗？**  
A: 可以——只需在 `book.save("output.xlsx")` 中更改文件扩展名；Aspose 会自动选择正确的格式。

**Q: 开发是否需要许可证？**  
A: 免费试用许可证可用于开发和测试。生产部署需要购买许可证。

**Q: 如何添加更多图表类型？**  
A: 在调用 `charts.add(...)` 时使用 `ChartType` 枚举（例如 `ChartType.PIE`、`ChartType.LINE`）。

**Q: 如果需要保护工作簿怎么办？**  
A: 在保存之前调用 `book.getSettings().setPassword("yourPassword")`。

**Q: Aspose.Cells 是否支持宏启用文件？**  
A: 支持——您可以在 XLSM 工作簿中创建或保留 VBA 宏。

**Last Updated:** 2026-04-11  
**Tested With:** Aspose.Cells 25.3 (Java)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}