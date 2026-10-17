---
category: general
date: 2026-10-16
description: Aspose.Cells 在 Java 中使用 EXPAND 函数设置公式。学习一步一步的示例，了解如何使用 expand 实现动态范围。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells set formula
- how to use expand
- expand function example
- Java Excel automation
- dynamic range formula
language: zh
lastmod: 2026-10-16
og_description: Aspose.Cells 在 Java 中使用 EXPAND 函数设置公式。通过完整示例了解如何在 Excel 工作簿中动态展开范围。
og_image_alt: Spreadsheet screenshot showing the EXPAND formula applied to cell B2
  via Aspose.Cells
og_title: Aspose.Cells 使用 EXPAND 设置公式 – Java 教程
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: Aspose.Cells set formula in Java using the EXPAND function. Learn a
    step‑by‑step example and see how to use expand for dynamic ranges.
  headline: Aspose.Cells set formula with EXPAND function – complete Java guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel formulas
- Spreadsheet automation
title: Aspose.Cells 使用 EXPAND 函数设置公式 – 完整 Java 指南
url: /zh/java/formulas-functions/aspose-cells-set-formula-with-expand-function-complete-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells 使用 EXPAND 函数设置公式 – 完整 Java 指南

如果您需要以编程方式 **aspose cells set formula**，本教程将向您展示具体步骤。您将学习如何使用 EXPAND 函数创建一个从起始单元格向下向右各扩展五行五列的动态范围，全部使用 Java 代码实现。

在 Java 中处理 Excel 公式常常显得笨拙，但 Aspose.Cells 把复杂性抽象掉了。下面的章节我们将逐步演示一个完整、可运行的示例，解释每行代码的意义，并探讨常见的变体，例如不同的起始单元格或可变的扩展大小。

## 本教程涵盖内容

* 使用 Aspose.Cells 加载已有工作簿  
* 访问工作表及其单元格集合  
* 使用 `EXPAND` 函数 **aspose cells set formula**  
* 重新计算工作簿以使公式生效  
* 保存结果并验证输出  

无需除 Aspose.Cells 之外的外部库，代码可在任意 Java 8+ 运行时上运行。完成后，您即可将此模式迁移到其他动态公式中。

## 前置条件

* Java Development Kit (JDK) 8 或更高版本  
* Aspose.Cells for Java（从[官方站点](https://downloads.aspose.com/cells/java)下载）  
* 将输入 Excel 文件（`input.xlsx`）放置在已知目录下  
* 具备基本的 Java 语法以及 Maven/Gradle 依赖管理经验  

## 第 1 步：创建项目并添加 Aspose.Cells

如果使用 Maven，请在 `pom.xml` 中加入以下依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest version -->
</dependency>
```

Gradle 的等价写法为：

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **小贴士：** 始终使用最新的稳定版本；新版在公式计算方面有性能提升。

## 第 2 步：加载工作簿

下面第一行代码打开已有工作簿。将 `YOUR_DIRECTORY` 替换为 `input.xlsx` 所在的绝对路径。

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*为什么重要*：加载工作簿会在内存中创建一个表示，使您能够在不再次访问文件系统的情况下操作工作表、单元格和公式。

## 第 3 步：访问目标工作表和单元格集合

我们使用第一个工作表（索引 0）。`Cells` 对象可直接通过地址访问单个单元格。

```java
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
```

如果需要操作其他工作表，请更改索引或使用 `get("SheetName")`。

## 第 4 步：**aspose cells set formula** – 应用 EXPAND 函数

现在在单元格 **B2** 中设置公式。`EXPAND` 函数接受三个参数：参考单元格、要向下扩展的行数以及要向右扩展的列数。

```java
        // Apply the EXPAND function to B2, expanding 5 rows and 5 columns from A2
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");
```

### 如何使用 expand

* **参考单元格 (`A2`)** – 动态范围的起始点。  
* **行数 (`5`)** – 范围向下扩展的行数。  
* **列数 (`5`)** – 范围向右扩展的列数。

如果需要更灵活的方案，可将这些值替换为变量：

```java
int rows = 10;
int cols = 3;
cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));
```

## 第 5 步：重新计算工作簿

设置公式后，必须让 Aspose.Cells 对其求值。`calculateFormula()` 方法会处理工作簿中的所有公式。

```java
        // Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();
```

> **为什么要重新计算？**  
> 若不调用此方法，公式将保持未求值状态，输出文件中只会显示原始的 `=EXPAND(...)` 字符串，而不是展开后的数组。

## 第 6 步：保存更新后的工作簿

最后，将更改写入新文件。这样可以保留原始工作簿以便对比。

```java
        // Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

打开 `output.xlsx` 时，单元格 **B2** 将显示一个 5 × 5 的值块，这些值来自以 **A2** 为起点的区域。如果 **A2** 的值为 `1`，则块中每个单元格都会显示 `1`，因为 `EXPAND` 会在扩展范围内复制源值。

## 完整、可运行的源代码

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet and its cells collection
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Step 3: Apply the EXPAND function to cell B2, referencing A2 and expanding 5 rows and 5 columns
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");

        // Step 4: Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();

        // Step 5: Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### 预期输出

| B2 | C2 | D2 | E2 | F2 |
|----|----|----|----|----|
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |

（实际值取决于源文件中 `A2` 的内容。）

## 常见变体和边缘情况

| 场景 | 代码更改 | 原因 |
|----------|-------------|--------|
| **不同的起始单元格** | `cells.get("C3").setFormula("=EXPAND(D3,3,2)");` | 使用任意单元格作为参考，公式相对于该单元格进行扩展。 |
| **可变的扩展大小** | `int rows = 8; int cols = 4; cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));` | 运行时确定范围大小，适用于数据驱动的报表。 |
| **零大小扩展** | `=EXPAND(A2,0,0)` | 仅返回原始单元格的值；在后续可能增大尺寸的条件逻辑中很有用。 |
| **使用命名范围** | `cells.get("B2").setFormula("=EXPAND(MyRange,5,5)");` | 当工作簿中已定义 `MyRange` 时使用，保持公式可读性。 |

> **注意：** Excel 的最大数组尺寸为 16,384 列 × 1,048,576 行。超出此限制会抛出计算错误。

## 调试技巧

* **公式未求值？** 确保在每次 `setFormula` 后调用 `workbook.calculateFormula();`。  
* **出现意外值？** 检查参考单元格（示例中的 `A2`）是否包含您期望传播的数据。  
* **性能顾虑** – 大范围扩展可能消耗较多资源。如果只需要子集，请缩小行/列参数。

## 结论

现在您拥有一个完整的 **aspose cells set formula** 示例，演示了在 Java 中 **如何使用 expand**。通过加载工作簿、设置 `EXPAND` 公式、重新计算并保存，您可以在无需手动操作 Excel 的情况下生成动态范围。

接下来您可以探索：

* 使用 `FILTER`、`SEQUENCE` 等其他动态函数配合 Aspose.Cells。  
* 将此逻辑嵌入生成按需报表的 Web 服务中。  
* 通过 Aspose.Cells API 将 `EXPAND` 与条件格式相结合。

欢迎尝试不同的起始单元格、可变大小或命名范围，以适配您的具体自动化场景。如果您觉得此 **expand function example** 有帮助，请与团队分享或在 GitHub 上提交改进。祝编码愉快！


## 接下来您可以学习什么？

以下教程与本指南紧密相关，进一步深化所示技术。每篇资源均包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并探索项目中的替代实现方案。

- [精通 Aspose.Cells Java：如何在 Excel 中中断公式计算](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [使用 Aspose.Cells Java 将 Excel 表格转换为范围：一步步指南](/cells/english/java/tables-structured-references/convert-excel-tables-ranges-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 设置 Excel 文档版本](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}