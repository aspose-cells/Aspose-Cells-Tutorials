---
category: general
date: 2026-08-20
description: 学习使用 Java 将 Excel 导出为 TXT，限制小数位数，保留有效数字，并将工作簿保存为 TXT。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: zh
lastmod: 2026-08-20
og_description: 使用 Aspose.Cells 将 Excel 导出为 TXT。本指南展示了如何限制小数位数、保留有效数字，并在 Java 中将工作簿保存为
  TXT。
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: 在 Java 中将 Excel 导出为 TXT——控制小数位数和有效数字
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: 如何使用 Aspose.Cells 将 Excel 导出为 TXT 并控制小数精度
url: /zh/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 将 Excel 导出为 TXT 并控制小数位精度

如果您需要 **将 Excel 导出为 TXT** 并确保输出遵循特定的小数位数，本指南提供完整的解决方案。您将了解如何限制小数位、保留有效数字，以及使用 Aspose.Cells for Java **将工作簿保存为 TXT**。

本教程将演示创建工作簿、插入高精度数值、配置 TXT 保存选项并将文件写入磁盘的全过程。完成后，您即可生成一个文本文件，精度恰好符合要求，无需手动后处理。

## 所需环境

- Java 17（或任何受支持的 JDK）
- Aspose.Cells for Java 23.10 或更高版本
- 用于管理依赖的 IDE 或构建工具（Maven/Gradle）
- 对输出目录的写入权限

## 步骤 1：创建工作簿并访问第一个工作表

在 **将 Excel 导出为 TXT** 时，创建工作簿是第一步。`Workbook` 类代表整个 Excel 文件，`Worksheet` 让您访问单元格。

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*为什么重要*：工作簿对象保存所有数据、样式和元数据。使用全新的工作簿可以确保没有隐藏的格式干扰文本导出。

## 步骤 2：添加数值并限制小数位

插入一个拥有多位小数的数字，以演示在导出时如何 **限制小数位**。

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*为什么重要*：Excel 会存储完整精度，但在后续导出时，您可能希望截断或四舍五入该值。`limit decimal places` 设置会自动处理此需求。

## 步骤 3：配置 TXT 保存选项以保留有效数字

Aspose.Cells 提供 `TxtSaveOptions`。设置 `significantDigits` 可让导出器仅保留所需的有效数字，忽略前导零。

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*为什么重要*：**保留有效数字** 选项确保输出文件包含可预测的精度，这对期望固定宽度数值格式的下游系统至关重要。

## 步骤 4：将工作簿保存为 TXT

最后，将工作簿写入文本文件。`save` 方法会遵循您配置的选项，生成的文件将包含受限的小数表示。

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*为什么重要*：使用 **save workbook as txt** 并配合已准备好的 `TxtSaveOptions`，可确保导出文件符合前一步设定的精度约束。

### `SignificantDigits.txt` 的预期内容

```
0.00012346
```

该值在四舍五入后显示五位有效数字（`12346`），并且前导零根据 TXT 格式得以保留。

## 变体与边缘情况

| 场景 | 调整方式 |
|----------|------------|
| **不同的有效数字数量** | 调用 `txtOptions.setSignificantDigits(n)`，其中 `n` 为 1‑15。 |
| **导出范围而非整张工作表** | 在保存前使用 `txtOptions.setExportRange("A1:B10")`。 |
| **保留列分隔符** | 设置 `txtOptions.setSeparator('\t')` 以生成制表符分隔的输出。 |
| **大型工作表** | 增加 `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` 以避免 `OutOfMemoryError`。 |

## 常见陷阱与专业提示

- **不要混淆有效数字和小数位**。前导零不计入有效数字；如需固定小数位数，请使用 `setSignificantDigits` 控制有效精度，使用 `setDecimalPlaces` 控制小数点后的位数。
- **在 IDE 中运行时始终使用绝对输出路径**，以避免权限错误。
- **使用 `java.nio.file.Files.readAllLines(Paths.get(outputPath))`** 简单验证生成的文件，确保内容符合预期后再交给下游流程。

## 完整源码供参考

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

运行程序后会生成 `SignificantDigits.txt`，其中唯一一行内容为 `0.00012346`，演示了 **export excel to txt** 过程同时满足 **limit decimal places** 与 **keep significant digits** 的需求。

## 结论

现在您已经掌握了使用 Aspose.Cells for Java **将 Excel 导出为 TXT** 并控制数值精度的方法。通过配置 `TxtSaveOptions`，您可以 **限制小数位**、**保留有效数字**，并可靠地 **save workbook as txt**，无需额外的后处理。

接下来，您可以探索：

- 将多个工作表导出为独立的 TXT 文件（每个工作表 **save workbook as txt**）
- 使用 `setSeparator` 创建兼容 CSV 的输出
- 为大数据集实现批量转换自动化

欢迎尝试不同的数字位数和分隔符，以满足项目的精确需求。祝编码愉快！


## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}