---
date: '2026-04-11'
description: 学习如何显示 Aspose Cells 版本、在 Java 中加载 Excel 工作簿，以及使用 Aspose.Cells 处理图表枚举。请参照一步一步的示例。
keywords:
- display aspose cells version
- load excel workbook java
- excel chart manipulation
title: 在 Java 中显示 Aspose Cells 版本和图表枚举处理
url: /zh/java/charts-graphs/aspose-cells-java-excel-charts-enum-handling-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 显示 Aspose Cells 版本及图表枚举处理（Java）

## 简介

如果您需要 **display Aspose Cells version**，在 Java 中加载 Excel 工作簿，并处理图表枚举，那么您来对地方了。在本教程中，我们将逐步演示将 Aspose.Cells for Java 集成到项目中的具体步骤，提取图表数据，并将基于整数的枚举转换为可读字符串。完成后，您将拥有一个可靠的、可直接投入代码库的生产就绪解决方案。

**您将学习的内容**
- 如何显示 Aspose.Cells 版本。
- 如何 **load Excel workbook Java** 并访问图表数据。
- 如何将整数枚举值转换为对应的字符串。
- 如何检索图表点的 X 和 Y 值类型。

让我们开始吧！

## 快速回答

- **如何检查 Aspose.Cells 版本？** 调用 `CellsHelper.getVersion()` 并打印结果。  
- **哪个 Maven 坐标添加 Aspose.Cells？** `com.aspose:aspose-cells:25.3`。  
- **我可以在 Java 中加载 Excel 工作簿吗？** 可以——使用 `new Workbook(filePath)`。  
- **枚举值是如何转换的？** 存储一个 `HashMap<Integer, String>` 并通过整数键查找。  
- **哪个方法打印 X/Y 值类型？** `pnt.getXValueType()` 和 `pnt.getYValueType()`。

## 什么是 “display Aspose Cells version”？

该短语指检索库的运行时版本字符串。了解确切的版本有助于调试、确保兼容性，并确认您的许可证已应用于目标发布版本。

## 为什么要显示版本并在 Java 中加载 Excel 工作簿？

- **调试** – 确认正确的库已在类路径上。  
- **合规** – 便于验证您使用的是已授权的版本。  
- **自动化** – 使脚本能够适应不同的库版本，而无需手动更改。

## 先决条件

### 必需的库和依赖项

- **Aspose.Cells for Java** – 用于 Excel 操作的核心库。  
- **Java Development Kit (JDK)** – 8 版或更高版本。

### 环境设置

- 您选择的 IDE（IntelliJ IDEA、Eclipse、NetBeans）。  
- 构建工具：Maven **或** Gradle（如下说明）。

### 所需知识

- 基础的 Java 编程。  
- 熟悉 Excel 概念（工作表、图表）有帮助，但不是必需的。

## 设置 Aspose.Cells for Java

### 使用 Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### 使用 Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 获取许可证的步骤
- **免费试用**：从 [Aspose's Release Page](https://releases.aspose.com/cells/java/) 下载。  
- **临时许可证**：在 [Aspose's Temporary License Page](https://purchase.aspose.com/temporary-license/) 获取短期许可证。  
- **购买**：对于长期项目，可通过 [Aspose Purchase Page](https://purchase.aspose.com/buy) 购买许可证。

### 基本初始化和设置
```java
import com.aspose.cells.*;

public class InitializeAsposeCells {
    public static void main(String[] args) {
        // Set the license if available
        License license = new License();
        try {
            license.setLicense("Path_to_License_File");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Print Aspose.Cells version to confirm setup
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

## 实现指南

### 如何显示 Aspose Cells 版本
**概述** – 快速在运行时验证库版本。

#### 步骤 1：导入所需的包
```java
import com.aspose.cells.*;
```

#### 步骤 2：创建类和主方法
```java
public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        // This prints the Aspose.Cells version
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

**说明**
- `CellsHelper.getVersion()` 返回您应用程序使用的 Aspose.Cells DLL 的确切版本字符串。

### 如何将整数枚举转换为字符串枚举
**概述** – 将数值枚举值（例如 `CellValueType.IS_NUMERIC`）转换为可读文本。

#### 步骤 1：设置用于转换的 HashMap
```java
import java.util.HashMap;

HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### 步骤 2：转换并打印枚举值
```java
public class EnumConversion {
    public static void main(String[] args) {
        int exampleEnumValue = CellValueType.IS_NUMERIC;
        System.out.println("Converted Enum Value: " + cvTypes.get(exampleEnumValue));
    }
}
```

**说明**
- `cvTypes` 映射将数值常量与人类可读的标签之间的差距弥合。

### 如何在 Java 中加载 Excel 工作簿并访问图表数据
**概述** – 打开现有工作簿，定位图表，并确保其数据是最新的。

#### 步骤 1：导入必要的包
```java
import com.aspose.cells.*;
```

#### 步骤 2：加载工作簿并访问工作表
```java
public class LoadExcelAndAccessChart {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();
    }
}
```

**说明**
- `new Workbook(filePath)` 将文件加载到内存中。  
- `ch.calculate()` 强制图表重新计算任何公式，以确保读取的数据是最新的。

### 如何检索并打印图表点的 X 和 Y 值类型
**概述** – 提取特定点的 X 和 Y 值的数据类型。

#### 步骤 1：设置枚举转换 HashMap（复用前面的）
```java
HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### 步骤 2：访问图表点并打印值类型
```java
public class RetrieveChartPointTypes {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();

        ChartPoint pnt = ch.getNSeries().get(0).getPoints().get(0);

        System.out.println("X Value Type: " + cvTypes.get(pnt.getXValueType()));
        System.out.println("Y Value Type: " + cvTypes.get(pnt.getYValueType()));
    }
}
```

**说明**
- `pnt.getXValueType()` / `pnt.getYValueType()` 返回整数常量，指示该值是数值、字符串、日期等。  
- `cvTypes` 映射将这些整数转换为可读文本。

## 实际应用

1. **财务报告** – 自动生成带有已验证数据类型的图表，以用于审计追踪。  
2. **数据可视化仪表板** – 将图表点提取到自定义 UI 组件中。  
3. **自动化测试** – 验证图表系列包含预期的数据类型。  
4. **商业智能** – 将图表元数据输入下游分析管道。  
5. **自定义报告工具** – 构建需要精确枚举处理的定制报告引擎。

## 性能考虑因素

- **仅加载所需工作表** – 处理大文件时，使用 `Workbook.getWorksheets().get(index)` 而不是加载所有工作表。  
- **及时释放对象** – 处理完后将工作簿引用设为 `null`，以帮助垃圾回收。  
- **批量处理文件** – 在处理大量工作簿时，分批处理以保持内存使用可预测。

## 常见问题与解决方案

- **未找到许可证** – 确保许可证文件路径正确且文件已包含在构建输出中。  
- **图表未计算** – 在读取点值之前始终调用 `chart.calculate()`。  
- **枚举映射不正确** – 验证已将所有相关的 `CellValueType` 常量添加到 `HashMap` 中。

## 常见问答

**问：我可以在 Aspose.Cells 24.x 上使用此代码吗？**  
答：可以，版本检索、工作簿加载和图表点访问的 API 在最近的版本中保持稳定。

**问：如果我的图表包含日期值怎么办？**  
答：将 `CellValueType.IS_DATE_TIME` 添加到 `cvTypes` 映射中，并映射为 `"IsDateTime"`。

**问：试用是否需要许可证？**  
答：完整功能需要试用许可证；如果没有许可证，生成的文件会出现水印。

**问：如何处理多个工作表？**  
答：遍历 `wb.getWorksheets()`，并处理遇到的每个 `Chart` 对象。

**问：有没有办法将图表数据导出为 CSV？**  
答：有——通过 `chart.getNSeries().get(i).getValues()` 提取系列值，并使用标准的 Java I/O 写入。

---

**最后更新:** 2026-04-11  
**已测试版本:** Aspose.Cells 25.3 for Java  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}