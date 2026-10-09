---
category: general
date: 2026-06-08
description: 使用 Java 编程创建 Excel。学习如何写入数值、设置小数位数，并使用 Aspose.Cells 保存工作簿 Excel 文件。
draft: false
keywords:
- create excel programmatically
- write numeric value
- save workbook excel
- save excel file
- how to set digits
language: zh
og_description: 在 Java 中以编程方式创建 Excel。本指南展示如何写入数值、控制数字精度以及保存 Excel 文件。
og_title: 使用编程方式创建 Excel – 完整 Java 教程
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel programmatically with Java. Learn how to write numeric
    value, set digits, and save workbook Excel file using Aspose.Cells.
  headline: Create Excel programmatically in Java – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Create a separate `ExportTableOptions` instance for each cell and assign
      it individually.
    question: What if I need more than one cell with different digit settings?
  - answer: Yes—use `Range.getExportTableOptions().set(exportOptions)` on a `Range`
      object that spans multiple cells.
    question: Can I apply the same setting to an entire range?
  - answer: No. The raw double (`12345.6789`) stays unchanged; only the visual representation
      is limited to the specified significant digits.
    question: Does this affect the underlying value?
  - answer: Aspose.Cells supports both `.xlsx` and `.xls`. Just change the file extension
      in `workbook.save()` and the library handles the conversion automatically.
    question: What about older Excel formats (`.xls`)?
  type: FAQPage
tags:
- Java
- Excel
- Aspose.Cells
title: 使用 Java 编程创建 Excel – 步骤指南
url: /zh/java/spreadsheet-automation/create-excel-programmatically-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中以编程方式创建 Excel – 完整指南

是否曾经需要**以编程方式创建 Excel**但不确定从何入手？根据我的经验，最大障碍是弄清楚如何*写入数值*并保持所需的精确度，同时还能**保存工作簿 Excel**文件而不出问题。  

在本教程中，我们将通过一个真实案例一步步演示**如何设置数字位数**、将数字写入单元格，最后**保存 Excel 文件**到磁盘——全部使用 Aspose.Cells for Java 库。没有冗余，只提供可直接复制到项目中的可运行解决方案。

## 前置条件

- Java 8 或更高（代码同样适用于 Java 11+）  
- Maven 或 Gradle 用于获取 Aspose.Cells 依赖  
- 基本了解 Java 语法（如果你能编写 `main` 方法，就可以了）  

> *专业提示：* 如果你还没有许可证，可以先使用 Aspose.Cells 的免费评估版——它在下面的示例中功能完整。

## 步骤 1：设置项目并导入 Aspose.Cells

首先，在你的 `pom.xml` 中添加 Aspose.Cells Maven 坐标。如果你更喜欢 Gradle，同样的坐标也适用。

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

依赖解析完成后，你可以在 Java 文件中导入所需的类：

```java
import com.aspose.cells.*;
```

## 步骤 2：创建新工作簿 – **以编程方式创建 Excel** 的核心

现在我们真正**以编程方式创建 Excel**。`Workbook` 对象代表整个电子表格文件。

```java
// Step 2: Instantiate a new workbook (blank Excel file)
Workbook workbook = new Workbook();
```

这行代码为你提供了一块干净的画布——可以把它想象成一个空的 Excel 文件，随时准备填充数据。

## 步骤 3：访问第一个工作表

每个工作簿默认至少包含一个工作表。获取它，以便我们开始放置数据。

```java
// Step 3: Grab the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

你也可以创建额外的工作表，但在本演示中默认工作表已经足够。

## 步骤 4：**写入数值** 并控制精度

这里就是魔法发生的地方。我们将在单元格 **A1** 中放入一个数字，然后告诉 Aspose.Cells **如何设置数字位数**——具体来说，我们希望导出文件时只显示四位有效数字。

```java
// Step 4: Put a numeric value into cell A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue(12345.6789); // raw value with many decimals
```

### 定义导出选项 – **如何设置数字位数**

Aspose.Cells 通过 `ExportTableOptions` 让你控制有效数字的位数。将其设置为 `4` 表示导出的 Excel 将显示 `1.235E+04`（或等价的四舍五入值），而底层数据保持不变。

```java
// Step 5: Create export options to keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setSignificantDigits(4);

// Apply the options to the cell
cell.getExportTableOptions().set(exportOptions);
```

> **为什么使用 `ExportTableOptions`？**  
> 它在内存中保留原始数值精度，同时强制视觉表现遵循你指定的数字位数限制——非常适合需要统一四舍五入但又不想丢失数据精度的报表。

## 步骤 5：**保存工作簿 Excel** – 拼图的最后一块

数据和格式都准备好后，是时候**保存 Excel 文件**到磁盘了。选择任意目录即可，只要确保应用程序拥有写入权限。

```java
// Step 6: Save the workbook with the configured options
String outputPath = "significant-digits.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

运行程序后会在工作目录生成 `significant-digits.xlsx`。在 Microsoft Excel 中打开，你会看到 **A1** 中的数字仅显示四位有效数字。

## 完整工作示例

把所有代码整合在一起，下面是一个可以直接编译运行的自包含类：

```java
import com.aspose.cells.*;

public class ExcelProgrammaticDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Write a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(12345.6789);

        // 4️⃣ Define export options – keep only 4 significant digits
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setSignificantDigits(4);
        cell.getExportTableOptions().set(exportOptions);

        // 5️⃣ Save the workbook (this is how we **save workbook Excel**)
        String filePath = "significant-digits.xlsx";
        workbook.save(filePath);
        System.out.println("Excel file created: " + filePath);
    }
}
```

### 预期输出

运行程序时，控制台会打印：

```
Excel file created: significant-digits.xlsx
```

打开 `significant-digits.xlsx` 可看到 **A1** 包含 `1.235E+04`（或根据 Excel 显示设置显示为 `1235`），验证了**如何设置数字位数**选项已按预期工作。

## 常见问题与边缘情况

- **如果需要在多个单元格使用不同的数字位数设置怎么办？**  
  为每个单元格创建单独的 `ExportTableOptions` 实例并分别分配。

- **可以将相同的设置应用于整个范围吗？**  
  可以——对跨多个单元格的 `Range` 对象使用 `Range.getExportTableOptions().set(exportOptions)`。

- **这会影响底层数值吗？**  
  不会。原始的 double (`12345.6789`) 保持不变，只有视觉表现被限制为指定的有效数字位数。

- **旧版 Excel 格式（`.xls`）怎么办？**  
  Aspose.Cells 同时支持 `.xlsx` 和 `.xls`。只需在 `workbook.save()` 中更改文件扩展名，库会自动处理转换。

## 下一步

既然你已经掌握了**以编程方式创建 Excel**、**写入数值**以及**保存工作簿 Excel**并精确控制数字位数的技巧，接下来可以探索：

- 添加 **样式** 和 **条件格式** 来突出重要数字。  
- 将工作簿导出为 **PDF** 或 **CSV** 以用于报表流水线。  
- 使用 **自动适应** 和 **列宽** 调整，使最终文件更加美观。  

上述主题都建立在本指南的基础之上，欢迎自行实验并扩展代码。

---

![以编程方式创建的 Excel 工作簿](https://example.com/images/create-excel-programmatically.png "以编程方式创建 Excel")

*图片说明:* 以编程方式创建 Excel – Java 示例展示了已填充的电子表格

--- 

**恭喜！** 你已经掌握了在 Java 中**以编程方式创建 Excel**的关键步骤，从插入数值到控制数字位数，再到**保存 Excel 文件**。继续玩转 API——还有整个电子表格自动化的世界等着你。祝编码愉快！

## 接下来应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 的其他功能，并在自己的项目中探索替代实现方案。每篇资源都提供完整的可运行代码示例和逐步解释。

- [如何使用 Aspose.Cells for Java 将 Excel 工作簿创建并保存为 SVG](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [如何使用 Aspose.Cells Java 将 Excel 创建并导出为 HTML | 工作簿操作指南](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [如何在 Java 中创建 Excel 文件并使用 Aspose.Cells 进行样式设置](/cells/english/java/advanced-features/excel-master-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}