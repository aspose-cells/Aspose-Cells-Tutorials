---
category: general
date: 2026-06-08
description: 使用 Aspose.Cells Java 从单元格获取日期时间，并学习如何在几步内将值写入 Excel 单元格。
draft: false
keywords:
- get datetime from cell
- write value to excel cell
- Aspose.Cells Java date parsing
- Japanese era calendar Excel
- Excel formula recalculation Java
language: zh
og_description: 使用 Aspose.Cells Java 从单元格获取日期时间。本教程还展示了如何高效地向 Excel 单元格写入值。
og_title: 在 Java Excel 中获取单元格的日期时间 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  headline: Get datetime from cell in Java Excel – Complete Guide
  type: TechArticle
- description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  name: Get datetime from cell in Java Excel – Complete Guide
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
title: 在 Java Excel 中从单元格获取日期时间 – 完整指南
url: /zh/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 Java Excel 单元格获取日期时间 – 完整指南

是否曾需要 **从单元格获取日期时间**，但值看起来像日本年号字符串？你并不孤单。在许多旧版电子表格中，日期会以 “Reiwa 3/04/01” 的形式存储，要把它转换为正确的 `java.time.LocalDateTime` 往往像在破译密码。

幸运的是，Aspose.Cells for Java 能帮你完成转换，同时我们还会演示如何 **向 Excel 单元格写入值**，让你在不破坏工作表逻辑的前提下实现数据的来回传递。

在本教程中，你将学习：

* 如何创建工作簿并定位到特定工作表。  
* 启用日本年号日历以进行解析的完整步骤。  
* 为什么在读取日期前必须重新计算公式。  
* 如何在不丢失格式的情况下将新值写回单元格。  

无需外部工具，也不需要魔法——只需几行普通的 Java 代码，即可在任何 Maven 项目中直接使用。

---

## 前置条件

* **Java 8+**（示例使用现代的 `java.time` API）。  
* **Aspose.Cells for Java** ≥ 23.9.0 – 通过 Maven 或 Gradle 添加依赖。  
* 对 Excel 基础概念（工作表、单元格、公式）有基本了解。  

如果缺少该库，请从官方 Aspose 仓库获取：

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## 第一步：创建新工作簿并访问第一个工作表

首先，需要一个全新的 `Workbook` 对象。可以把它想象成在内存中打开了一个新的 Excel 文件。

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

*为什么重要：*  
以编程方式创建工作簿可以让你在任何数据写入文件系统之前，完全控制设置。第一个工作表（`index 0`）将用于演示读取和写入。

---

## 第二步：向单元格 A1 写入日本年号日期字符串

现在我们 **向 Excel 单元格写入值** 到 A1。这模拟了用户手动输入 “Reiwa 3/04/01” 的真实场景。

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

*小技巧：* `putValue` 功能强大——它接受字符串、数字、日期，甚至公式。当你传入普通字符串时，Aspose 会原样存储，非常适合本示例。

---

## 第三步：启用日本年号日历以进行日期解析

默认情况下，Aspose.Cells 使用公历。要识别 “Reiwa”，我们需要切换一个设置。

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

*为什么要启用？*  
日本年号日历会把年号名称（Reiwa、Heisei、Showa）映射到对应的公历日期。如果不打开此标志，库会把字符串当作普通文本，永远得不到正确的 `DateTime` 对象。

---

## 第四步：重新计算公式，使年号字符串转换为公历日期

Aspose 并不会自动把字符串解析为日期，而是把单元格视为公式结果，需要一次计算过程。

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

当 `calculateFormula()` 执行时，引擎会识别年号模式，应用日本日历，并在内部存储转换后的公历日期。随后调用 `getDateTime()` 会返回 `java.util.Date`（也可以转换为 `java.time`）。

**预期输出**

```
2021-04-01T00:00:00.000+00:00
```

---

## 第五步：将新值写回同一单元格（或其他单元格）

假设你想用标准的 ISO‑8601 日期覆盖原始字符串。下面演示如何安全地 **向 Excel 单元格写入值**，并保持单元格样式不变。

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

*发生了什么？*  
`putValue` 会检测到 `LocalDateTime` 类型并转换为 Excel 的序列号表示。设置数字格式后，打开 Excel 时单元格会按照你期望的方式显示日期。

---

## 完整工作示例

将上述步骤整合在一起，下面是一段可以直接编译运行的 Java 类。它会创建工作簿、写入年号字符串、完成转换，最后保存文件。

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

使用 `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` 运行此程序，然后打开 **output.xlsx**。你会看到 A1 单元格显示当前日期，控制台则输出转换后的 “2021‑04‑01” 值。

---

## 处理边缘情况与常见问题

### 如果单元格已经包含真正的 Excel 日期怎么办？

如果 `cell.getType()` 返回 `CellValueType.IS_DATE_TIME`，可以跳过重新计算步骤，直接读取值：

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

### 如何处理整列的年号字符串？

遍历已使用的范围并一次性应用相同设置：

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

### 能否在之后关闭日本年号处理？

可以——只需把标志重新设为 false：

```java
settings.setUseJapaneseEraCalendar(false);
```

记得在修改设置后再次重新计算。

---

## 专业技巧与注意事项

* **性能：** 启用日本年号日历会带来极小的开销。如果只针对少量单元格使用，建议在处理完后关闭该设置。  
* **地区匹配：** 年号字符串必须严格符合 “EraName yy/MM/dd” 格式。拼写错误（例如 “Rewa”）会导致单元格保持为普通文本。  
* **保存格式：** `Workbook.save("output.xlsx")` 会生成 XLSX 文件。若需要旧的二进制格式，可使用 `"output.xls"`，但某些功能（如年号解析）可能受限。

---

## 结论

现在，你已经掌握了在源数据使用日本年号表示时 **从单元格获取日期时间** 的方法，并了解了如何以正确的格式 **向 Excel 单元格写入值**。只需通过 `setUseJapaneseEraCalendar(true)` 开启相应日历并强制公式重新计算，Aspose.Cells 就能在传统年号字符串与现代公历日期之间架起桥梁——全部只需几行 Java 代码。

接下来可以尝试将此模式扩展到其他文化日历（如泰国历、伊斯兰历），或使用相同思路批量处理大型工作簿。基本原则——启用对应日历、重新计算、再读写——在各种场景下都适用。

遇到无法破解的日期格式？在下方留言，我们一起排查。祝编码愉快！  

![获取日期时间示例](https://example.com/images/get-datetime-from-cell.png "获取日期时间示例")


## 接下来该学习什么？

以下教程与本指南所示技术紧密相关，帮助你进一步掌握 API 功能并探索在项目中的其他实现方式。

- [使用 Aspose.Cells Java 在 Excel 中配置 1904 日期系统以实现高效单元格操作](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [在 Aspose.Cells Java 中实现递归单元格计算以增强 Excel 自动化](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [使用 Aspose.Cells for Java 将 Excel 单元格名称转换为索引的逐步指南](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}