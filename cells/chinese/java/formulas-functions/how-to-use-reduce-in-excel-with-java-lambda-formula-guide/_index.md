---
category: general
date: 2026-06-08
description: 如何在 Excel 中使用 Java 的 Aspose.Cells 实现 reduce。学习 Excel 的 lambda 公式、Java
  的动态数组、如何编写 lambda，以及使用 reduce 求和的清晰分步教程。
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: zh
og_description: 如何在 Excel 中使用 Java 的 reduce。掌握 Lambda 公式、Excel 动态数组以及通过完整可运行示例使用 reduce
  求和。
og_title: 如何在 Excel 中使用 Java 的 Reduce——Lambda 公式指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: 如何在 Excel 中使用 Java 的 Reduce——Lambda 公式指南
url: /zh/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 Reduce 与 Java – Lambda 公式指南

是否曾好奇在编写 Java 代码时 **how to use reduce** 在 Excel 中该如何使用？你并不孤单。许多开发者在尝试将 Excel 的新动态数组函数与基于 Java 的自动化结合时会遇到障碍，而答案并不像最初看起来那样神秘。

在本教程中，我们将通过一个具体示例演示 **how to use reduce** 与 **lambda formula Excel** 表达式的结合，全部由 Aspose.Cells for Java 库驱动。完成后，你将能够在 Java 中生成动态数组、编写 lambda 函数，并计算 **sum with reduce**——无需手动操作电子表格。

---

## 你将构建的内容

- 完全由 Java 创建的全新工作簿。  
- 一个 **EXPAND** 动态数组，将单元格 A1:A5 填充为数字 1‑5。  
- 一个 **REDUCE** 公式，使用 **lambda formula Excel** 对这些数字求和。  
- 一个保存的 `.xlsx` 文件，可在任意电子表格程序中打开以验证结果。

无需外部宏，无需 VBA——仅使用纯 Java 代码和 Excel 的现代函数。

---

## 前置条件

- Java 17（或任何近期的 JDK）——旧版本也能工作，但会失去 `var` 语法糖。  
- Aspose.Cells for Java（免费试用版足以演示本例）。  
- 对 Java 语法和 Excel 公式有基本了解。  

如果你对 **dynamic arrays java** 还不熟悉，也别担心——本指南会解释每一步。

---

## 第一步：设置项目并导入 Aspose.Cells

首先，向你的 `pom.xml` 添加 Aspose.Cells Maven 依赖（或手动获取 JAR）。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **专业提示：** 保持依赖最新；新版在公式计算速度上有提升，这在处理 **how to use reduce** 大型工作表时尤为重要。

---

## 第二步：创建工作簿并访问第一个工作表

现在我们创建一个全新的工作簿。这是学习 **how to use reduce** 的基础，因为工作簿对象为我们提供了一个放置公式的沙盒。

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*为何重要：* `Workbook` 类抽象了整个 Excel 文件，而 `Worksheet` 代表单个标签页。稍后你会看到 **dynamic arrays java** 如何通过在 A1 放置单个公式来填充多个单元格。

---

## 第三步：使用 EXPAND 生成垂直数组

Excel 的 `EXPAND` 函数可以将值溢出到一个范围。我们将使用它在 A 列创建数字 1 到 5。

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

如果打开生成的工作簿，单元格 A1:A5 将显示 1、2、3、4、5。这正是 **dynamic arrays java** 的体现——一个公式即可填满整个范围。

---

## 第四步：编写 REDUCE Lambda 以求和数组

这一步回答核心问题：**how to use reduce** 在 Excel 中如何通过 Java 实现。`REDUCE` 函数遍历数组，并对每个元素应用你提供的 lambda。这里我们对数字求和。

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

拆解如下：

- `0` – 初始累加器值（`acc`）。  
- `A1:A5` – 由 **EXPAND** 生成的数组。  
- `LAMBDA(acc, x, acc + x)` – **lambda formula Excel**，将每个元素（`x`）加到累加器（`acc`）上。  

公式执行后，`B1` 将得到 **15**，即数字 1‑5 的 **sum with reduce**。

> **如何在 Excel 中编写 lambda**？把它视为匿名函数，前面的参数是输入，最后的表达式是返回值。在 Java 中我们只需嵌入文本，实际计算由 Excel 引擎完成。

---

## 第五步：保存工作簿

最后，将工作簿持久化到磁盘，这样你就可以在 Excel、Google Sheets 或任何支持 `.xlsx` 的查看器中打开它。

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

打开文件后你会看到：

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

**sum with reduce** 出现在 B1，证明我们已经成功演示了 **how to use reduce** 与 **lambda formula Excel** 的结合。

---

## 完整可运行示例

下面是完整的、可直接运行的 Java 程序。复制粘贴到 IDE，调整输出目录，然后点击 **Run**。

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**预期输出**（打开 `new-functions.xlsx` 时）：

- 单元格 **A1:A5** 包含 `1, 2, 3, 4, 5`。  
- 单元格 **B1** 显示 `15`，验证了 **sum with reduce**。

---

## 常见问题与边缘情况

### 如果需要水平数组而不是垂直数组怎么办？

只需在 `EXPAND` 中交换列/行参数。水平溢出到 B1:F1 的示例：

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### 能否使用 REDUCE 进行乘法而不是求和？

完全可以。只需修改 lambda 的主体：

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

此时 B1 将显示 `120`（5 ! = 120）。

### Aspose.Cells 是否支持自定义 LAMBDA 函数？

是的，你可以通过工作簿的 `Names` 集合定义具名 LAMBDA 函数，然后像调用内置公式一样使用它们。这属于更深入的内容，后续教程会讲解 **how to write lambda** 函数的持久化用法。

### 老版本 Excel 不识别 REDUCE 会怎样？

如果目标是 Excel 2019 或更早版本，公式会返回 `#NAME?`。在这种情况下


## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式。每篇资源均提供完整代码示例和逐步解释。

- [Mastering Aspose.Cells Java: How to Interrupt Formula Calculation in Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}