---
category: general
date: 2026-07-17
description: 使用 Java Lambda 函数创建 Excel 工作簿，演示 EXPAND 和 REDUCE 函数，并使用 Aspose.Cells
  计算 Excel 中的数组函数。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use lambda function java
- create excel workbook java
- use reduce function excel
- use expand function excel
- calculate array functions excel
language: zh
lastmod: 2026-07-17
og_description: 使用 Java Lambda 函数构建 Excel 工作簿，应用 EXPAND 和 REDUCE，并在 Excel 中计算数组函数——完整的逐步指南。
og_image_alt: Screenshot of use lambda function java creating Excel workbook with
  formulas
og_title: 使用 Java Lambda 函数 – 使用 Aspose.Cells 创建 Excel 工作簿
schemas:
- author: Aspose
  dateModified: '2026-07-17'
  description: Use lambda function java to create an Excel workbook, demonstrate EXPAND
    and REDUCE functions, and calculate array functions in Excel with Aspose.Cells.
  headline: Use Lambda Function Java to Create Excel Workbook Example
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
- Lambda
title: 使用 Java Lambda 函数创建 Excel 工作簿示例
url: /zh/java/workbook-operations/use-lambda-function-java-to-create-excel-workbook-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Lambda Function Java 创建 Excel 工作簿示例

想要 **use lambda function java** 来创建 Excel 工作簿吗？在本教程中，我们将通过使用 Aspose.Cells 的完整示例，展示如何在一个易于跟随的脚本中 **use expand function excel**、**use reduce function excel** 和 **calculate array functions excel**，以及构建文件。

如果你曾经盯着电子表格并想，“一定有一种编程方式可以展开这个数组或归约这些数字”，那么你来对地方了。 在本指南结束时，你将拥有一个可运行的 Java 程序，它可以创建 Excel 文件，注入 EXPAND、REDUCE、COT 和 COTH 的公式，并保存计算后的结果——同时展示 **lambda function java** 方法的强大功能。

---

## 前置条件 – 开始前你需要的东西

- **Java Development Kit (JDK) 8+** – 代码使用 lambda 表达式，请确保使用的至少是 JDK 8。  
- **Aspose.Cells for Java** – 一个商业库，可在未安装 Office 的情况下操作 Excel 文件。请从 Aspose 官网获取最新的 JAR 并将其添加到项目的类路径中。  
- 一个普通的 IDE（IntelliJ IDEA、Eclipse、VS Code）– 任意一种都可以，但带有 Maven/Gradle 支持的 IDE 能让依赖管理轻松无痛。  

无需额外安装；该库在后台处理所有繁重的工作。

---

## 步骤 1：设置项目并导入依赖

创建一个新的 Maven 项目（或如果你更喜欢 Gradle），并添加 Aspose.Cells 依赖：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

如果你不使用 Maven，只需将 `aspose-cells-24.10.jar` 放入 `libs` 文件夹并将其添加到构建路径中。

> **专业提示：** 保持依赖最新。更新的版本通常会带来性能提升和诸如 EXPAND、REDUCE 等函数的错误修复。

---

## 使用 Lambda Function Java 创建 Excel 工作簿

环境准备就绪后，让我们 **use lambda function java** 将 LAMBDA 表达式直接嵌入 Excel 公式中。Excel 中的 REDUCE 函数需要一个 lambda，而 Java 的字符串处理使其变得简单。

```java
import com.aspose.cells.*;

public class Office365FunctionsDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Create a new workbook and obtain the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 3: Demonstrate the EXPAND function – expands a seed array to a larger size
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3},5,1)");
        // Explanation: EXPAND turns the 3‑element seed into a 5‑row, 1‑column array.

        // Step 4: Demonstrate the REDUCE function – aggregates an array into a single value
        // Here we **use lambda function java** inside the Excel formula.
        sheet.getCells().get("A2").setFormula(
            "=REDUCE(0,{1,2,3,4},LAMBDA(a,b,a+b))"
        );
        // Explanation: Starting at 0, the lambda (a,b) → a+b adds each element together.

        // Step 5: Use the COT function to calculate the cotangent of π/4
        sheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 6: Use the COTH function to calculate the hyperbolic cotangent of 1
        sheet.getCells().get("A4").setFormula("=COTH(1)");

        // Step 7: Recalculate all formulas so the results are stored in the cells
        workbook.calculateFormula();

        // Step 8: Save the workbook with the evaluated results
        workbook.save("Office365Funcs.xlsx");
    }
}
```

### 为什么这样可行

- **`Workbook`** 是 **create excel workbook java** 任务的入口点。它在内存中表示整个文件。  
- **`Worksheet`** 为我们提供了一个工作表；默认工作簿已经包含一个。  
- **`setFormula`** 注入原始的 Excel 公式字符串。注意 REDUCE 行中包含 `LAMBDA(a,b,a+b)` 段落——这就是我们 **use lambda function java** 告诉 Excel 如何合并数值的地方。  
- **`calculateFormula()`** 强制 Aspose.Cells 计算每个公式，从而将结果数字直接持久化到文件中。如果不调用此方法，单元格只会包含公式文本。  

---

## 如何使用 Expand Function Excel – 动态扩展数组

**use expand function excel** 示例位于单元格 `A1`。让我们拆解公式的作用：

```excel
=EXPAND({1,2,3},5,1)
```

- `{1,2,3}` 是种子数组（三个数字）。  
- `5` 告诉 Excel 将结果扩展到五行。  
- `1` 设置列数（仅一列）。  

当工作簿在 Excel 中打开时，`A1:A5` 将显示：

| A |
|---|
| 1 |
| 2 |
| 3 |
| 0 |
| 0 |

末尾的零是填充值，因为种子数组的元素不足以填满请求的大小。

> **常见陷阱：** 忘记调用 `workbook.calculateFormula()` 会导致只能看到原始的 `=EXPAND(...)` 文本，而不是展开后的数字。

---

## 如何使用 Reduce Function Excel – 使用 Lambda 求和

**use reduce function excel** 行位于单元格 `A2`。其形式如下：

```excel
=REDUCE(0,{1,2,3,4},LAMBDA(a,b,a+b))
```

- `0` 是初始累加器值。  
- `{1,2,3,4}` 是我们想要归约的数组。  
- `LAMBDA(a,b,a+b)` 告诉 Excel 将每个元素（`b`）加到累计总和（`a`）上。  

计算后，`A2` 的值为 **10**。如果你想要乘积而不是和，只需将 `a+b` 替换为 `a*b` ——相同的 **use lambda function java** 模式仍然适用。

---

## 计算数组函数 Excel – COT 和 COTH

虽然并非严格的基于数组，COT

## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，构建在本指南展示的技术之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [如何使用 Aspose Cells – Java Excel 引擎教程](/cells/english/java/calculation-engine/)
- [使用 Aspose.Cells Java 的自定义 SUM 函数：提升你的计算](/cells/english/java/formulas-functions/custom-sum-function-excel-aspose-cells-java/)
- [如何在 Java 中使用 Aspose.Cells 实现 Excel 切片器自动化](/cells/english/java/advanced-features/excel-slicer-modifications-java-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}