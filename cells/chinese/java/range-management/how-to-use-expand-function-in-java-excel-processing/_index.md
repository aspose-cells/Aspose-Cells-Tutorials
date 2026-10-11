---
category: general
date: 2026-10-10
description: 学习如何在 Java 中读取和写入 Excel 文件时使用 expand 函数。一步步的指南，提供完整代码和解释。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use expand function
- read and write excel file java
- Java Excel formula
- Aspose.Cells expand
- Excel dynamic range Java
language: zh
lastmod: 2026-10-10
og_description: 如何在 Java 中读取和写入 Excel 文件时使用 expand 函数。请遵循本完整教程，使用 Aspose.Cells 添加动态范围。
og_image_alt: Screenshot of Java code using the EXPAND function on an Excel worksheet
og_title: Java Excel 处理中的 expand 函数使用方法 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to use expand function while reading and writing Excel files
    in Java. Step‑by‑step guide with complete code and explanations.
  headline: How to use expand function in Java Excel processing
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Formula
title: 如何在 Java Excel 处理中使用 expand 函数
url: /zh/java/range-management/how-to-use-expand-function-in-java-excel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java Excel 处理中使用 EXPAND 函数的方式

如果您在 Java 中处理 Excel 文件时需要**how to use expand function**，本指南将准确展示如何操作。教程结束时，您将能够在 Java 项目中读取和写入 Excel 文件，并使用 `EXPAND` 公式动态扩展单元格范围。

在 Excel 电子表格中工作通常意味着处理能够适应数据规模变化的公式。`EXPAND` 函数是 Excel 最近版本中引入的，它可以按指定的行数和列数扩展引用。结合强大的 Java 库，您可以在代码库中自动化此行为，而无需离开代码环境。

在本教程中，您将：

* 加载已有工作簿（`read and write excel file java` 场景）  
* 将 `EXPAND` 公式应用到单元格  
* 重新计算公式以显示新值  
* 保存更新后的工作簿  

先决条件：

* 已安装 Java 17 或更高版本  
* 使用 Maven 或 Gradle 进行依赖管理  
* Aspose.Cells for Java（提供 `Workbook`、`Worksheet` 等类）  

> **专业提示：** Aspose.Cells 支持 `.xlsx` 和 `.xls` 格式，并且不需要在主机上安装 Microsoft Office。

## 您需要的内容

| 项目 | 原因 |
|------|--------|
| JDK 17+ | 现代语言特性和更佳性能 |
| Maven/Gradle | 简化库的引入 |
| Aspose.Cells for Java | 提供 `Workbook`、`Worksheet` 与公式引擎 |
| 一个 Excel 文件（`input.xlsx`） | 用于演示 `EXPAND` 函数的源工作簿 |

使用 Maven 将 Aspose.Cells 添加到项目中：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

或使用 Gradle：

```groovy
implementation 'com.aspose:aspose-cells:23.12'
```

## 第一步：加载工作簿（how to use expand function – 初始化）

首先打开要修改的 Excel 文件。`Workbook` 在内存中表示整个文件。

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

**为什么这很重要：** 加载工作簿后，您即可访问所有工作表、单元格以及内部公式引擎。未加载工作簿时，无法读取或写入 Excel file java 数据。

## 第二步：访问目标工作表

大多数工作簿包含多个工作表；示例使用第一个工作表（索引 0）。您也可以按名称检索工作表。

```java
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**说明：** `Worksheet` 对象公开 `Cells` 集合，您可以在其中设置公式。如果需要定位其他工作表，请将索引替换为相应的数字，或调用 `get("SheetName")`。

## 第三步：设置 EXPAND 公式（how to use expand function in practice）

现在我们将在单元格 **B1** 中写入 `EXPAND` 公式。该公式将引用 `A1` 向下扩展 **5 行**，向右扩展 **1 列**，生成范围 `A1:A6` 并向右平移一列。

```java
        // Apply the EXPAND formula to B1
        // =EXPAND(A1,5,1) expands A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");
```

**为什么这样有效：** `setFormula` 只存储公式字符串；Aspose.Cells 并不会立即求值。`EXPAND` 函数将在我们触发计算时进行求值。

## 第四步：重新计算公式（完成 expand 函数）

插入公式后，要求工作簿重新计算所有相关单元格。此步骤确保新值出现在工作表中。

```java
        // Recalculate all formulas so the EXPAND result is evaluated
        workbook.calculateFormula();
```

**幕后发生了什么：** 计算引擎解析 `EXPAND` 表达式，确定新的范围，并将得到的值数组写回工作表。如果 `A1` 包含数字，扩展后的范围将在新单元格中重复该数字。

## 第五步：保存更新后的工作簿

最后，将修改后的工作簿写回磁盘（或输出流）。这完成了 **read and write excel file java** 的完整循环。

```java
        // Save the workbook with the new formula evaluated
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

运行程序后会生成 `output.xlsx`，其中单元格 **B1** 现在包含一个溢出范围，能够将 `A1` 的值在五行一列中复制。打开文件即可在 Excel 中看到动态数组的效果。

### 预期输出

假设 `A1` 原本的数值为 `42`，则结果单元格为：

| B1 | B2 | B3 | B4 | B5 | B6 |
|----|----|----|----|----|----|
| 42 | 42 | 42 | 42 | 42 | 42 |

如果 `A1` 包含文本字符串，则相同的文本会在扩展范围内溢出。

## 常见变体和边缘情况

| 场景 | 调整 |
|----------|------------|
| **不同的起始单元格** | 将 `"B1"` 改为任意地址，例如 `"C3"` |
| **仅按列扩展** | 使用 `=EXPAND(A1,0,3)` 将范围向右扩展三列 |
| **动态行数** | 将静态的 `5` 替换为单元格引用，如 `D1`，其保存所需的行数 |
| **使用命名范围** | 将 `A1` 替换为已定义的名称，例如 `=EXPAND(MyRange,5,1)` |
| **公式错误** | 确保工作簿保存为支持动态数组的格式（`.xlsx`）。旧版 `.xls` 文件会截断溢出。 |

### 处理大型电子表格

在处理非常大的工作簿时，可使用自定义 `CalcOptions` 对象调用 `workbook.calculateFormula(CalcOptions)`，以限制内存使用或启用多线程计算。

```java
CalcOptions options = new CalcOptions();
options.setCalculateOnOpen(true); // Faster if you only need the result later
workbook.calculateFormula(options);
```

## 完整源码（可直接复制粘贴）

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Set a formula that expands the range of A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");

        // Step 4: Recalculate all formulas so the new value is evaluated
        workbook.calculateFormula();

        // Step 5: Save the workbook with the updated data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

> **注意：** 将 `YOUR_DIRECTORY` 替换为 Excel 文件的绝对或相对路径。该代码可在 Java 支持的任何平台上运行（Windows、macOS、Linux）。

## 结论

现在您已经了解了在 Java 环境中**how to use expand function**，能够动态扩展单元格引用，并通过 Aspose.Cells 完成完整的 **read and write excel file java** 工作流。加载工作簿、应用 `EXPAND` 公式、重新计算以及保存，这些步骤覆盖了 Excel 自动化的整个生命周期。

**接下来** 您可以探索：

* 将 `EXPAND` 与其他动态数组函数（如 `FILTER` 或 `SORT`）结合使用。  
* 使用相同模式从数据库或 REST API **read and write excel file java** 数据。  
* 基于扩展范围尝试条件格式化。  

欢迎将示例适配到您自己的项目中，让 `EXPAND` 函数简化所有数据规模随时间变化的场景。

--- 

*编码愉快！*


## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。每个资源都包含完整的可运行代码示例和逐步解释。

- [如何在 Java Excel 工作簿中使用 SEQUENCE – 步骤指南](/cells/english/java/formulas-functions/how-to-use-sequence-in-java-excel-workbook-step-by-step-guid/)
- [如何在 Java 中使用 WRAPCOLS – 完整的 Excel WRAPCOLS 示例](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [如何在 Excel 中使用 Reduce 与 Java – Lambda 公式指南](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}