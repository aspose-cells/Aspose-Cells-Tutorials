---
"date": "2025-04-07"
"description": "学习如何使用 Aspose.Cells for Java 在 Excel 中创建和自定义图表。本指南将帮助您自动创建图表、增强数据可视化并节省时间。"
"title": "使用 Aspose.Cells Java 创建和设计 Excel 图表——综合指南"
"url": "/zh/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells Java 创建和设置 Excel 图表样式

## 介绍

在当今数据驱动的世界中，有效的信息可视化对于分析和决策至关重要。通常，我们需要以编程方式在 Excel 工作簿中创建动态图表，尤其是在处理大型数据集或自动报告系统时。本教程演示如何使用 Aspose.Cells for Java 在 Excel 中无缝创建和自定义图表。通过将 Aspose.Cells 集成到您的 Java 应用程序中，您可以自动化图表创建、增强数据呈现并节省时间。

**您将学到什么：**
- 使用 Aspose.Cells 初始化工作簿并用数据填充它。
- 使用数据标记创建和配置折线图。
- 自定义系列外观和颜色以实现更好的可视化。
- 以 Excel 格式保存包含新创建的图表的工作簿。

让我们首先讨论一下开始所需的先决条件。

## 先决条件

在使用 Aspose.Cells for Java 创建和设计图表之前，请确保您已完成以下设置：

### 所需库
将 Aspose.Cells 作为依赖项添加到您的项目中。以下是针对 Maven 和 Gradle 用户的说明：

**Maven：**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle：**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 环境设置要求
- 您的系统上安装了 Java 开发工具包 (JDK)。
- 用于编码和测试的集成开发环境 (IDE)，例如 IntelliJ IDEA 或 Eclipse。

### 知识前提
需要对 Java 编程有基本的了解，并且熟悉 Excel 工作簿和图表概念。 

### 许可证获取
Aspose.Cells 是一款商业产品，需要许可证才能使用其全部功能。您可以获取免费试用版以评估其功能，申请临时许可证以进行长期测试，或购买该产品以供长期使用。

- **免费试用：** [下载免费试用版](https://releases.aspose.com/cells/java/)
- **临时执照：** [申请临时许可证](https://purchase.aspose.com/temporary-license/)
- **购买：** [购买 Aspose.Cells](https://purchase.aspose.com/buy)

## 设置 Aspose.Cells for Java

安装必要的依赖项后，设置开发环境以使用 Aspose.Cells。首先导入库并在 Java 应用程序中初始化 Workbook 对象：

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // 初始化新的工作簿实例
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## 实施指南

在本节中，我们将把实现分解为不同的功能：工作簿初始化和数据填充、图表创建和配置、系列定制和工作簿保存。

### 功能 1：工作簿初始化和数据填充

**概述：** 此功能主要用于创建新工作簿、访问其第一个工作表以及向其中填充用于创建图表的数据。

#### 步骤 1：初始化工作簿
首先实例化一个 `Workbook` 目的：

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // 实例化工作簿
        Workbook workbook = new Workbook();
        
        // 访问第一个工作表
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### 步骤 2：设置列标题并填充数据
定义列标题并使用示例数据填充行：

```java
        // 设置列标题 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // 为系列 1 创建随机数据
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // 为系列 2 创建随机数据
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### 功能2：图表创建和配置

**概述：** 此功能演示如何向工作簿的工作表添加图表、设置其样式以及配置基本属性。

#### 步骤 3：向工作表添加图表
添加带有数据标记的折线图：

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // 实例化工作簿
        Workbook workbook = new Workbook();
        
        // 访问第一个工作表
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // 将图表添加到工作表
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // 访问和配置图表
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // 设置预定义样式
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### 特点3：系列配置和定制

**概述：** 通过自定义系列设置（例如不同的颜色和标记样式）来增强图表的视觉吸引力。

#### 步骤 4：自定义系列设置
配置系列数据、应用自定义格式并调整标记：

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // 实例化工作簿
        Workbook workbook = new Workbook();
        
        // 访问第一个工作表
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // 向图表添加系列
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // 为系列点启用多种颜色
        chart.getNSeries().setColorVaried(true);

        // 自定义第一个系列标记样式和颜色
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // 设置第一个系列的 X 和 Y 值
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // 自定义第二个系列标记样式和颜色
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // 设置第二个系列的 X 和 Y 值
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### 功能4：工作簿保存

**概述：** 最后，保存工作簿以保留您的更改并确保图表包含在 Excel 文件中。

#### 步骤 5：保存工作簿
使用新创建的图表保存您的工作簿：

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // 实例化工作簿
        Workbook workbook = new Workbook();
        
        // 访问第一个工作表并按照前面的步骤添加数据、图表配置...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // （添加数据和配置图表的实现将在这里）

        // 将工作簿保存为 Excel 文件
        workbook.save("StyledChart.xlsx");
    }
}
```

**关键词建议：**
- “Aspose.Cells for Java”
- 《用 Java 创建 Excel 图表》
- 《Java 编程实现 Excel 自动化》

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}