---
category: general
date: 2026-07-03
description: 在 Java 中使用 Aspose.Cells 导出公式，将 Excel 单元格转换为文本。学习如何高效打印 Excel 区域并获取单元格值字符串。
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: zh
og_description: 在 Java 中包含公式导出，将 Excel 单元格转换为文本。一步一步的指南，展示如何打印 Excel 区域并将单元格值检索为字符串。
og_title: 导出时包含公式 – 将 Excel 单元格转换为文本
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: 在 Java 中包含公式导出 – 将 Excel 单元格转换为文本
url: /zh/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中包含公式导出 – 将 Excel 单元格转换为文本

是否曾在从 Excel 工作簿提取数据时需要 **include formulas export**？也许您正在构建一个报告服务，需要在提供整洁的文本块的同时保留原始公式。在这种情况下，您来对地方了。本指南将教您如何使用 Aspose.Cells for Java 将 Excel 单元格转换为纯文本——*包括*任何嵌入的公式。

我们还会涉及如何 **print Excel range**、调整 **export table options**，以及最终 **get cell values string**，这些字符串您可以记录日志、通过 API 发送或存入数据库。完成后，您将拥有一个可直接运行的代码片段，并深入了解每个调用背后的原理。

## 您将获得的内容

- 一个完整的、可复制粘贴的 Java 程序，能够读取 `.xlsx` 文件，选择范围，并将其导出为格式化的字符串。
- 对 `ExportTableOptions` 类的理解，以及为何切换 `setExportAsString` 和 `setIncludeFormula` 很重要。
- 处理大型工作表、不同数据类型以及自定义输出格式的技巧。
- 常见陷阱的快速检查清单（如合并单元格、隐藏行以及地区特定的数字格式）。

### 前提条件

- Java 17 或更高（代码在旧版本也能编译，但我们将使用最新的 LTS）。
- Aspose.Cells for Java 23.10（或任何近期版本）——可从 Maven Central 获取。
- 一个示例 `input.xlsx` 放置在您可控制的文件夹中（示例中路径为硬编码，便于说明）。

如果您已经具备上述条件，下面开始吧。

## 第一步：设置项目并添加依赖

首先，创建一个 Maven 项目（如果您喜欢，也可以使用 Gradle）。在 `pom.xml` 中添加 Aspose.Cells 依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **专业提示：** 如果您使用公司代理，请确保能够访问仓库；否则构建将因 “Could not resolve dependencies” 错误而失败。

Maven 下载完成后，您即可开始编写 Java 代码。

## 第二步：加载工作簿并获取目标工作表

代码示例的第一行展示了如何打开已有的工作簿：

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

将 `YOUR_DIRECTORY` 替换为文件的绝对或相对路径。`Workbook` 构造函数会自动检测文件格式（XLS、XLSX、CSV 等），无需手动指定。

接下来，获取第一张工作表：

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

为什么是第一张工作表？在许多模板中数据位于首个标签页，但您也可以传入任意索引，甚至使用 `get("SheetName")` 按名称获取。

## 第三步：定义要导出的范围

现在进入 **convert excel cells text** 操作的核心。您通过创建 `Range` 对象来告诉 Aspose.Cells 要提取哪些单元格：

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

`"A1:C3"` 是经典的 A1 样式地址。也可以通过代码动态构建：

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

这种灵活性在范围大小动态时非常有用——例如，您可以使用 `ws.getCells().getMaxDataRow()` 读取最后使用的行。

## 第四步：配置 Export Table Options 以包含公式

这里是 **include formulas export** 的关键所在。默认情况下，Aspose.Cells 返回 *显示* 的值。如果单元格包含 `=SUM(A1:A3)`，您将得到计算后的数字，而不是公式文本。要改变此行为，请设置 `ExportTableOptions`：

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

为什么要同时设置这两个标志？`setExportAsString(true)` 告诉 API 使用默认分隔符（列使用制表符，行使用换行符）将单元格连接成字符串。`setIncludeFormula(true)` 将值来源从 “显示值” 切换为 “原始公式”。如果只想要值，请保持为 `false`。

### 可选调整

- `eto.setExportHiddenRows(true);` – 包含 Excel 中隐藏的行。
- `eto.setExportHiddenColumns(true);` – 同样适用于列。
- `eto.setExportAsHTML(true);` – 获取 HTML 而非纯文本。

随意尝试；该选项类是 **export table options** 的实验场。

## 第五步：将范围检索为格式化字符串

现在我们提取数据：

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

返回的 `txt` 大致如下（假设 A1:C3 包含值和公式的混合）：

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

请注意制表符 (`\t`) 用于分隔列，换行符 (`\n`) 用于分隔行。如果需要二维数组，可在后续对字符串进行拆分：

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## 第六步：打印结果 – 简单实现 “Print Excel Range”

最后，我们将字符串输出到控制台：

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

运行程序会打印出上面显示的确切输出。之后您可以将字符串写入日志文件、通过 HTTP 发送，或存入 NoSQL 文档。

## 完整、可直接运行的示例

将所有代码组合起来，这就是完整的程序。复制、粘贴后点击 **Run**——无需额外导入。

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### 预期输出（示例）

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

如果工作簿中的数字被格式化为日期，它们将以地区特定的格式显示（例如 `2026‑07‑03`）。若要强制使用 ISO 日期，可通过自定义 `NumberFormat` 调整 `ExportTableOptions`。

## 处理边缘情况和常见问题

### 如果范围包含合并单元格怎么办？

合并单元格的值视为左上角单元格的值。合并区域其余部分将显示为空字符串。如果需要合并区域的地址，可在导出前调用 `Cell.getMergedRange()`。

### 能否导出超大工作表（数十万行）？

可以，但需注意内存消耗。使用 `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` 让 Aspose.Cells 将数据流式写入磁盘。同时，考虑分块导出（例如每次 10 000 行），以保持字符串大小可控。

### 如何更改列分隔符？

`ExportTableOptions` 提供 `setSeparator(char separator)` 方法。若需 CSV 样式输出，可将其设为 `','`：

```java
eto.setSeparator(',');
```

### 公式是否支持外部引用？

如果公式引用了另一个工作簿，Aspose.Cells 会保留引用文本（`='[Other.xlsx]Sheet1'!A1`），除非您也加载该工作簿，否则不会计算外部值。

## 生产级代码的专业提示

- **Cache the workbook** if you’re reading the

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，构建在本指南演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能，并在项目中探索替代实现方案。

- [如何使用 Aspose.Cells Java 创建并导出 Excel 为 HTML | 工作簿操作指南](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [如何使用 Aspose.Cells 将 Excel 转换为 PDF（Java）&#58; 步骤指南](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [使用 Aspose.Cells for Java 将 Excel 工作簿导出为图像&#58; 步骤指南](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}