---
category: general
date: 2026-08-14
description: 如何使用 Aspose.Cells 设置分隔符并保存为 CSV，限制数字位数，导出 CSV 字符串，以及在 Java 中重新计算公式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: zh
lastmod: 2026-08-14
og_description: 如何使用 Aspose.Cells 设置分隔符并保存为 CSV，限制数字位数，导出 CSV 字符串，以及在 Java 中重新计算公式。
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: 如何设置分隔符并保存为 CSV – Aspose.Cells 指南
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: 如何使用 Aspose.Cells 设置分隔符并保存为 CSV
url: /zh/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何设置分隔符并使用 Aspose.Cells 保存为 CSV

如果您需要在从 Excel 工作簿导出数据时 **设置分隔符**，本指南将展示使用 Aspose.Cells for Java 的完整端到端解决方案。您将学习如何配置 CSV 分隔符、限制有效数字位数、导出 CSV 字符串，以及在加载工作簿后刷新动态数组公式。

本教程涵盖了在您的机器上运行代码所需的全部内容，包括处理诸如日本天皇年号等特殊日历。完成后，您将能够生成准确的 CSV 文件、控制数值精度，并确保公式保持最新。

## 前提条件

- Java 17 或更高（代码同样可在 JDK 11+ 上编译）
- Aspose.Cells for Java 23.9 或更高 – 从 [Aspose website](https://products.aspose.com/cells/java/) 下载
- 基本熟悉 Maven 或 Gradle 的依赖管理
- IDE（IntelliJ IDEA、Eclipse、VS Code）或简单的文本编辑器和命令行

> **专业提示：** 使用专用的 `libs` 文件夹或 Maven Central 将 Aspose.Cells JAR 保持在类路径上。下面的示例假设为 Maven 项目。

## 步骤 1：设置 Maven 项目

创建一个包含 Aspose.Cells 依赖的 `pom.xml`：

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

运行 `mvn clean compile` 下载库并验证构建成功。

## 步骤 2：设置分隔符并保存为 CSV

主要目标是在将 Excel 工作簿保存为 CSV 时，将默认的逗号分隔符更改为自定义字符（例如分号）。Aspose.Cells 提供了 `CsvSaveOptions` 来实现此目的。

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### 原理说明

- `CsvSaveOptions.setDelimiter(char)` 告诉 Aspose.Cells 使用哪个字符分隔字段。默认是逗号，但任何字符（制表符 `'\t'`、管道符 `'|'` 等）都可使用。
- `setSignificantDigits(int)` 限制数值精度，满足 **限制数字位数** 的需求，无需手动格式化每个单元格。

#### 预期输出

文件 `output.csv` 将包含如下行：

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

请注意，数字被四舍五入为五个有效数字（例如 `123.45678` → `123.46`）。

## 步骤 3：保存 CSV 时限制数字位数

如果需要更严格的数值格式控制，也可以使用 `CsvSaveOptions` 实例来指定自定义数字格式字符串。

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` 遵循 .NET 样式的模式，Aspose.Cells 会予以遵守。
- 同时使用 `setNumberFormat` 和 `setSignificantDigits` 可在不同地区实现可预测的四舍五入。

## 步骤 4：使用自定义分隔符将 CSV 导出为字符串

有时您不想生成实体文件，而是需要将 CSV 数据保存在内存中（例如作为 HTTP 响应发送）。`ExportTableOptions` 类允许您将范围导出为字符串。

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### 适用场景

- 从 REST 接口返回 CSV（Spring 中的 `@RestController`）
- 将 CSV 数据嵌入电子邮件附件而不写入磁盘
- 在单元测试期间进行快速的合理性检查

## 步骤 5：加载工作簿后重新计算公式

如果工作簿包含公式——尤其是最近 Excel 版本引入的 **动态数组公式**——则必须在加载文件后重新计算它们。Aspose.Cells 会自动刷新动态数组结果，但对于普通公式仍需调用 `calculateFormula()`。

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### 为什么需要重新计算？

- 公式可能引用外部数据或易变函数（`NOW()`、`RAND()`），需要最新的值。
- 动态数组公式（例如 `=SORT(A1:A10)`）会自动求值，但调用 `calculateFormula()` 可确保所有工作表的一致性。

## 步骤 6：完整端到端示例

下面是一个单类示例，演示 **设置分隔符**、**保存为 CSV**、**限制数字位数**、**导出 CSV 字符串**、**加载带有特殊日历的工作簿**以及 **重新计算公式**。代码可直接复制粘贴到您的项目中。

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### 验证结果

1. 在文本编辑器中打开 `output.csv` —— 您应看到每列之间使用分号 (`;`) 分隔。
2. 确认数值列最多显示五个有效数字。
3. 控制台输出将打印第 4 步生成的 CSV 字符串。
4. 在 Excel 中打开 `japan_updated.xlsx` —— 之前显示 `#REF!` 或过时值的公式现在将显示正确结果。

## 常见陷阱及避免方法

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| CSV 显示额外的引号 | 单元格包含逗号，而分隔符也是逗号 | 通过 `setDelimiter` 使用不同的分隔符（`;` 或 `\t`） |
| 数字四舍五入不正确 | `setSignificantDigits` 在自定义数字格式之后应用 | 在 `setSignificantDigits` 之前应用 `setNumberFormat` |

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源均包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.Cells for Java 加载并保存 Excel 为 CSV：完整指南](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [如何使用 Aspose.Cells for Java 加载 CSV 文件：完整指南](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [如何使用 Aspose.Cells 在 Java 中使用自定义解析器加载 CSV 文件](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}