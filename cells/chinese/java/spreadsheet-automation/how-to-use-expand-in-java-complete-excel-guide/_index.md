---
category: general
date: 2026-06-21
description: 学习如何在 Java 中使用 expand 将数组展开为行，编写 Excel 公式代码，并以 Java 方式保存 Excel 文件——全部在一个教程中。
draft: false
keywords:
- how to use expand
- expand array to rows
- write excel formula code
- save excel file java
language: zh
og_description: 如何在 Java 中使用 expand 操作 Excel 数据，将数组展开为行，编写 Excel 公式代码，并以 Java 方式保存
  Excel 文件。
og_title: 如何在 Java 中使用 Expand – 完整的 Excel 指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  headline: How to Use Expand in Java – Complete Excel Guide
  type: TechArticle
- description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  name: How to Use Expand in Java – Complete Excel Guide
  steps:
  - name: Why This Works
    text: '- **`Workbook`**: Represents the entire Excel file. Creating a new one
      gives you a clean canvas; loading an existing file lets you augment a pre‑existing
      template. - **`Worksheet`**: Think of it as a single tab. We grab the first
      one because that’s where we’ll demonstrate the formula. - **`setFormul'
  - name: Real‑World Use Cases
    text: '| Scenario | How EXPAND Helps | |----------|------------------| | Generating
      a month‑long schedule from a short list of tasks | `=EXPAND(taskList,30)` |
      | Padding a matrix for a statistical model | `=EXPAND(matrix,10,10,0)` | | Creating
      placeholder rows for user input | `=EXPAND({""},20)` |'
  - name: Expected Output
    text: 'When you open `output.xlsx`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Formulas
title: 如何在 Java 中使用 Expand——完整的 Excel 指南
url: /zh/java/spreadsheet-automation/how-to-use-expand-in-java-complete-excel-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中使用 Expand – 完整 Excel 指南

有没有想过 **如何使用 expand** 来自动化 Excel？你并不是唯一的提问者——开发者们经常询问如何在不编写冗长循环的情况下将数组展开为行。好消息是，你只需要一个公式，而将该公式写入工作簿的 Java 代码出奇地简短。

在本教程中，我们将通过一个实用示例，逐步演示如何使用 expand、如何在 Java 中编写 Excel 公式代码，以及如何以 Java 方式保存 Excel 文件，以便立即查看结果。完成后，你将拥有一个可运行的程序，能够加载已有工作簿、将 `EXPAND` 函数写入单元格，并将文件写回磁盘。

## 前置条件

在开始之前，请确保你已经具备：

- 已安装 Java 17（或任意近期 JDK）。
- 用于管理依赖的 Maven 或 Gradle。
- **Aspose.Cells for Java** 库（在 Java 中操作 Excel 最简便的方式）。可以从 Maven Central 获取：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest -->
</dependency>
```

无需额外安装 Excel；该库在内部处理文件格式。如果你更喜欢 Gradle，只需相应地替换依赖块即可。

现在基础已经就绪，让我们动手实践。

## 在 Java 中使用 Expand

`EXPAND` 函数是 Excel 动态数组家族的一员。它接受一个源数组并将其展开到指定大小，默认使用 `#N/A` 填充空单元格。本例中，我们将一个简单的一维数组 `{1,2,3}` 传入，并让 Excel 将其展开为 **5 行**。

```java
// Import statements
import com.aspose.cells.*;

public class ExpandDemo {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load or create a workbook
            Workbook wb = new Workbook(); // creates a blank workbook
            // Optionally, load an existing file:
            // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Get the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // 3️⃣ Apply the EXPAND function in cell A1
            // This is where we **write excel formula code** from Java.
            ws.getCells().get("A1").setFormula("=EXPAND({1,2,3},5)");

            // 4️⃣ Save the workbook — **save excel file java** style.
            wb.save("YOUR_DIRECTORY/output.xlsx");
            System.out.println("Workbook saved successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 为什么这样可行

- **`Workbook`**：代表整个 Excel 文件。创建新工作簿相当于获得一块干净的画布；加载已有文件则可以在现有模板上进行增强。
- **`Worksheet`**：相当于单个标签页。我们取第一张工作表，因为示例公式会放在这里。
- **`setFormula`**：此方法接受任意有效的 Excel 公式字符串。本例注入 `EXPAND` 函数，告诉 Excel **将数组展开为行**（如果指定列数，也会展开为列）。
- **`save`**：将更改持久化到磁盘。这正是 **save excel file java** 的关键步骤，确保后续可以在 Excel 或其他查看器中打开文件。

运行程序，打开 `output.xlsx`，你会看到 A 列被填充为 `1, 2, 3, #N/A, #N/A`。将 `EXPAND` 的第二个参数改为 `3`，则只会得到三行——非常适合动态报表。

## 使用 EXPAND 函数将数组展开为行

如果你之前习惯手动遍历行来填充数据，`EXPAND` 函数可以替代这些冗余代码。下面简要说明其语法：

```
EXPAND(source, rows, columns, fill)
```

- **source** – 需要展开的数组。例如本例中的 `{1,2,3}`。
- **rows** – 期望的行数。本例使用 `5`。
- **columns** – 可选，默认等于源数组的列数。
- **fill** – 空单元格的填充值（默认 `#N/A`）。

### 实际使用场景

| 场景 | EXPAND 的帮助方式 |
|----------|------------------|
| 从短任务列表生成整月计划表 | `=EXPAND(taskList,30)` |
| 为统计模型填充矩阵 | `=EXPAND(matrix,10,10,0)` |
| 为用户输入创建占位行 | `=EXPAND({""},20)` |

让 Excel 完成繁重的工作，你的 Java 代码即可保持简洁，避免不必要的循环。

## 在 Java 中编写 Excel 公式代码

你可能会问：“能否动态构建公式字符串？”答案是肯定的。下面的代码片段根据变量生成 `EXPAND` 调用：

```java
int[] numbers = {4, 5, 6};
int targetRows = 7;

// Convert int array to Excel‑style literal: {4,5,6}
StringBuilder sb = new StringBuilder("{");
for (int i = 0; i < numbers.length; i++) {
    sb.append(numbers[i]);
    if (i < numbers.length - 1) sb.append(",");
}
sb.append("}");

String formula = String.format("=EXPAND(%s,%d)", sb.toString(), targetRows);
ws.getCells().get("B2").setFormula(formula);
```

可以看到我们 **write excel formula code**（编写 Excel 公式代码）是以编程方式完成的，然后将其写入单元格 `B2`。当需要根据数据库数据实时生成公式时，这种方式尤为实用——比如生成动态的 Excel 报表。

## Save Excel File Java – 持久化更改

将工作簿保存下来是整个流程的最后一步。Aspose.Cells 提供了多种保存方式：

- **`wb.save("path.xlsx")`** – 以默认的 XLSX 格式保存。
- **`wb.save("path.xls", SaveFormat.EXCEL_97_TO_2003)`** – 兼容旧版 Excel。
- **`wb.save(outputStream, SaveFormat.XLSX)`** – 将文件写入流（例如在 Web 应用中返回给前端）。

下面示例演示如何写入 `ByteArrayOutputStream`，以便从 REST 接口返回字节流：

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
wb.save(baos, SaveFormat.XLSX);
byte[] excelBytes = baos.toByteArray();
// Now you can send `excelBytes` as a response payload.
```

这正是许多企业服务采用的 **save excel file java** 模式。

## 常见坑点与专业技巧

- **公式计算时机** – Aspose.Cells 在 `save` 时 **不会** 自动计算公式。若需要得到计算结果，请在保存前调用 `wb.calculateFormula()`。
- **动态数组兼容性** – `EXPAND` 仅在 Excel 365 / 2021 及以上版本可用。使用旧版 Excel 打开会出现 `#NAME?`。若必须兼容旧客户端，请考虑手动展开。
- **区域设置问题** – 无论工作簿语言为何，都使用英文函数名 `EXPAND`；Aspose.Cells 采用英文语法。
- **大数组** – 将数千行展开会显著增大文件体积。请关注内存占用，并在必要时采用流式写入大数据集。

## 完整可运行示例

下面是完整的、可直接复制到 IDE 中运行的程序示例，包含所有导入、错误处理以及注释，帮助你快速上手。

```java
import com.aspose.cells.*;

public class ExpandDemoFull {
    public static void main(String[] args) {
        // Adjust these paths as needed
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/output.xlsx";

        try {
            // Step 1: Load an existing workbook or create a new one
            Workbook wb;
            if (new java.io.File(inputPath).exists()) {
                wb = new Workbook(inputPath);
                System.out.println("Loaded existing workbook.");
            } else {
                wb = new Workbook(); // brand‑new workbook
                System.out.println("Created a new workbook.");
            }

            // Step 2: Access the first worksheet
            Worksheet ws = wb.getWorksheets().get(0);

            // Step 3: Build a dynamic EXPAND formula (expand array to rows)
            int[] sourceArray = {1, 2, 3};
            int rowsDesired = 5;

            // Convert Java array to Excel literal syntax
            StringBuilder literal = new StringBuilder("{");
            for (int i = 0; i < sourceArray.length; i++) {
                literal.append(sourceArray[i]);
                if (i < sourceArray.length - 1) literal.append(",");
            }
            literal.append("}");

            String formula = String.format("=EXPAND(%s,%d)", literal, rowsDesired);
            ws.getCells().get("A1").setFormula(formula);
            System.out.println("Inserted formula: " + formula);

            // Optional: force calculation so the file contains values, not just formulas
            wb.calculateFormula();

            // Step 4: Save the workbook – **save excel file java** style
            wb.save(outputPath);
            System.out.println("Workbook saved to " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error occurred: " + ex.getMessage());
            ex.printStackTrace();
        }
    }
}
```

### 预期输出

打开 `output.xlsx` 后：

| A   |
|-----|
| 1   |
| 2   |
| 3   |
| #N/A |
| #N/A |

如果将 `rowsDesired` 改为 `3`，则列将在第三行后停止。`#N/A` 是 Excel 用来表示“此处无数据”的占位符——你可以通过向 `EXPAND` 传入第四个参数来替换它，例如 `=EXPAND({1,`（此处省略后续示例）。

## 接下来该学习什么？

以下教程与本指南紧密相关，进一步深化所学技术。每篇资源都提供完整的可运行代码示例以及逐步解释，帮助你掌握更多 API 功能，并在项目中探索替代实现方案。

- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [How to Delete Rows in Excel Using Aspose.Cells for Java | Guide & Tutorial](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [How to Save Excel Files in Various Formats Using Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}