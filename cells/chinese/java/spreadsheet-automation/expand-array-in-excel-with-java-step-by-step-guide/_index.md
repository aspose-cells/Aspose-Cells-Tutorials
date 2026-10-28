---
category: general
date: 2026-07-03
description: 学习如何使用 Java 在 Excel 中展开数组。本教程涵盖将数组展开为行、如何使用展开功能以及如何高效插入公式。
draft: false
keywords:
- expand array in excel
- expand array to rows
- how to use expand
- how to insert formula
- set formula in cell
language: zh
og_description: 使用 Java 在 Excel 中展开数组。请按照本指南学习如何使用展开、在单元格中设置公式，以及即时将数组展开到行。
og_title: 使用 Java 在 Excel 中展开数组 – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  headline: Expand Array in Excel with Java – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  name: Expand Array in Excel with Java – Step‑by‑Step Guide
  steps:
  - name: Why Use EXPAND?
    text: '`EXPAND` removes the tedious step of dragging the fill handle. It also
      works with dynamic arrays, meaning if your source array changes, the spilled
      range updates automatically. This is especially handy when generating reports
      programmatically.'
  - name: 1. Expanding a Horizontal Array to Multiple Columns
    text: 'If you need to **expand array to rows** *and* columns, just change the
      third argument:'
  - name: 2. Using a Named Range as the Source
    text: 'Instead of a literal `{1,2,3}`, you can reference a named range that may
      change at runtime:'
  - name: 3. Handling Non‑Numeric Data
    text: '`EXPAND` works with text as well. For example:'
  - name: 4. Avoiding Zero Fill with `IFERROR`
    text: 'If you’d rather see blanks instead of zeros, wrap the `EXPAND` in `IFERROR`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: 使用 Java 在 Excel 中展开数组 – 步骤指南
url: /zh/java/spreadsheet-automation/expand-array-in-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 Java 扩展数组 – 完整编程指南

是否曾想过如何在不手动拖动单元格的情况下 **在 Excel 中扩展数组**？你并不孤单。许多开发者在需要以编程方式生成动态范围时会遇到困难——尤其是当全新的 Excel `EXPAND` 函数尚未普及时。在本指南中，我们将准确展示 **如何使用 EXPAND**，将公式插入工作表，并让结果溢出到你想要的行。完成后，你将能够在一行 Java 代码中 **将数组扩展到行**。

我们将使用 Aspose.Cells for Java 库演示一个完整、可运行的示例。没有模糊的引用，只有可以直接复制、编译并运行的具体代码。在此过程中，我们会讨论每一步为何重要，涵盖诸如非连续数组等边缘情况，并提供一些官方文档中没有的专业技巧。准备好了吗？让我们开始吧。

## 前提条件

在开始之前，请确保你拥有：

* 已安装 Java 17（或任何近期的 JDK）。
* 用于管理依赖的 Maven 或 Gradle。
* 有效的 Aspose.Cells for Java 许可证（免费试用版可用于测试）。
* 对 Excel 公式的基本了解——如果你之前使用过 `VLOOKUP` 或 `SUMIF`，就可以直接上手。

如果这些对你来说陌生，请先暂停并完成相应的设置；本教程的其余部分假设这些已经就绪。

## 第一步：设置 Maven 项目并添加 Aspose.Cells

为了保持整洁，创建一个名为 `ExpandArrayDemo` 的新 Maven 项目。将 Aspose.Cells 依赖添加到你的 `pom.xml` 中：

```xml
<!-- pom.xml -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExpandArrayDemo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.12</version> <!-- Use the latest version -->
        </dependency>
    </dependencies>
</project>
```

> **专业提示：** 如果你使用 Gradle，同样的依赖写法是 `implementation 'com.aspose:aspose-cells:23.12'`。

Maven 下载完成后，你就可以编写 **在单元格中设置公式** 的 Java 代码了。

## 第二步：创建 Workbook 并访问第一个工作表

第一段代码与之前看到的代码片段相似，但我们会添加一些安全检查和注释，以便你了解每行代码背后的 *原因*。

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook – this gives us a blank Excel file.
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet (index 0). 
        //    If you ever need a different sheet, just change the index or name.
        Worksheet ws = wb.getWorksheets().get(0);

        // From here on we’ll work with ws (the active sheet).
```

*此步骤重要原因：* 实例化 `Workbook` 会分配 Aspose 用于管理单元格、公式和样式的内部结构。访问第一个工作表是最常见的入口点，尤其是在你仅进行实验时。

## 第三步：插入 EXPAND 公式 – “如何插入公式”

现在进入本教程的核心：**如何插入公式** 以扩展数组。Excel 的 `EXPAND` 函数接受三个参数——源数组、所需行数和所需列数。在我们的例子中，我们希望将 `{1,2,3}` 扩展为 **5 行** 和 **1 列**。

```java
        // 3️⃣ Put the EXPAND formula into cell A1.
        //    The formula string must be exactly as Excel would see it.
        String formula = "=EXPAND({1,2,3},5,1)";
        ws.getCells().putFormula("A1", formula);
```

请注意我们使用了 `putFormula` 而不是 `putValue`。这告诉 Aspose 将字符串视为实际的 Excel 公式，而不是普通文本。`putFormula` 方法会自动解析字符串并在内部存储公式树。

### 为什么使用 EXPAND？

`EXPAND` 消除了拖动填充柄的繁琐步骤。它还能与动态数组配合使用，这意味着如果源数组发生变化，溢出范围会自动更新。这在以编程方式生成报告时尤为便利。

## 第四步：强制计算 – 实现结果

通过 API *在单元格中设置公式* 时，工作簿不会自动重新计算。你需要触发一次计算过程，以便数组 **扩展到行**，并让数值显示在工作表中。

```java
        // 4️⃣ Recalculate the worksheet so the formula result is materialized.
        ws.getCells().calculate();
```

如果跳过此步骤，打开生成的 `.xlsx` 时 Excel 只会显示公式而不会显示溢出值，直到你按 **F9**。调用 `calculate()` 可确保工作簿开箱即用。

## 第五步：保存工作簿并验证输出

最后，将工作簿写入文件，并可选择将溢出值打印到控制台以进行验证。

```java
        // 5️⃣ Save the workbook to disk.
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // 6️⃣ (Optional) Read back the spilled values to prove it worked.
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A = index 0
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

运行程序后，你应该在控制台看到以下输出：

```
Workbook saved to ExpandArrayResult.xlsx
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

Excel 用零填充剩余行，因为源数组只有三个元素。这是 `EXPAND` 的默认行为。如果你更喜欢空白而不是零，可以将数组包装在 `IFERROR` 中或使用 `CHOOSE` 技巧——在下面的 “高级变体” 部分会有更多说明。

## 高级变体与边缘情况

### 1. 将水平数组扩展到多列

如果你需要 **将数组扩展到行** *和* 列，只需更改第三个参数：

```java
ws.getCells().putFormula("B2", "=EXPAND({1,2,3},5,3)");
```

现在范围会溢出为 5 × 3 的块，缺失的单元格会填充为零。

### 2. 使用命名范围作为源

你可以使用可能在运行时变化的命名范围来代替字面量 `{1,2,3}`：

```java
ws.getCells().putFormula("C1", "=EXPAND(MySourceRange,10,1)");
```

确保 `MySourceRange` 已存在（你可以通过 `ws.getNames().add("MySourceRange", "Sheet1!$D$1:$D$3")` 来创建它）。

### 3. 处理非数值数据

`EXPAND` 同样适用于文本。例如：

```java
ws.getCells().putFormula("D1", "=EXPAND({\"Jan\",\"Feb\",\"Mar\"},4,1)");
```

额外的行会显示为空字符串，而不是零。

### 4. 使用 `IFERROR` 避免零填充

如果你更希望看到空白而不是零，可以将 `EXPAND` 包装在 `IFERROR` 中：

```java
ws.getCells().putFormula("E1", "=IFERROR(EXPAND({1,2,3},5,1), \"\")");
```

现在第 4 行和第 5 行将真正为空。

## 常见陷阱及规避方法

| 陷阱 | 产生原因 | 解决方案 |
|---------|----------------|-----|
| **公式未重新计算** | 忘记调用 `ws.getCells().calculate()` | 在 `putFormula` 后始终调用 `calculate()`。 |
| **零值出现在应为空白的地方** | `EXPAND` 默认用零填充 | 使用 `IFERROR(..., "")` 或用 `CHOOSE` 包装。 |
| **单元格地址错误** | 使用 `"A0"` 或 `"1A"` | Excel 地址从 1 开始；Aspose 需要 `"A1"` 样式。 |
| **库版本不匹配** | 使用不支持 `EXPAND` 的旧版 Aspose.Cells | 升级到最新版本（本文撰写时为 23.12）。 |

## 完整工作示例（所有步骤合并）

下面是完整的、可直接复制粘贴的程序。将其保存为 `ExpandArrayDemo.java`，编译并运行。

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (blank Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);

        // Insert the EXPAND formula in A1 to expand {1,2,3} to 5 rows × 1 column
        ws.getCells().putFormula("A1", "=EXPAND({1,2,3},5,1)");

        // Force calculation so the array is materialized
        ws.getCells().calculate();

        // Save the workbook to disk
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // Verify the spilled values
        System.out.println("Spilled values:");
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

运行该程序会生成一个 Excel 文件，其中 **A1 单元格** 包含 `EXPAND` 公式，A 列第 1‑5 行显示 `1, 2, 3, 0, 0`。在 Excel 中打开文件即可立即看到相同结果——无需手动拖动。

## 结论

你刚刚学习了如何使用 Java **在 Excel 中扩展数组**，**如何使用 EXPAND**，以及以编程方式 **在单元格中设置公式** 并 **将数组扩展到行** 的完整步骤。借助 Aspose.Cells，你可以避免繁琐的 UI 操作，让代码完成繁重工作。无论是构建报表引擎、自动数据录入工具，还是自定义电子表格生成器，这项技术都能为你节省大量时间。

接下来怎么办？尝试将静态数组替换为来自其他工作表的动态范围，实验多列溢出，或将 `EXPAND` 与 `FILTER` 结合使用，实现强大的数据转换。可能性无限，而你已经拥有了坚实的基础。

有问题或想分享酷炫的使用案例吗？留下一个

## 接下来该学习什么？

以下教程涵盖与本指南演示的技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.Cells for Java 向 Excel 工作簿插入行](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [如何使用 Aspose.Cells for Java 在 Excel 中插入列 - 综合指南](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)
- [如何使用 Aspose.Cells for Java 在 Excel 中选择单元格范围（2023 指南）](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}