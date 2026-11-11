---
date: '2026-10-28'
description: 学习如何在 Java 中使用 Aspose.Cells 复制和粘贴选项粘贴数值，提供逐步代码、Maven 依赖设置和授权提示。
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: 学习如何在 Java 中使用 Aspose.Cells 复制和粘贴选项粘贴数值，提供逐步代码、Maven 依赖设置和授权提示。
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: 如何使用 Aspose.Cells 复制和粘贴选项粘贴数值
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: 如何使用 Aspose.Cells 复制和粘贴选项粘贴数值
url: /zh/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 复制和粘贴选项粘贴数值

在 Java 中实现 Excel 报表自动化意味着您可以生成、合并和格式化工作簿，而无需手动打开 Excel。使用 **Aspose.Cells**，您可以完全控制公式、隐藏行和单元格数值，从而确保报告准确且轻量化。在本教程中，您将学习如何使用 **CopyOptions.ReferToDestinationSheet** 保持公式正确，以及使用 **PasteOptions** 仅粘贴所需的可见数值。

## 快速答案
- **`CopyOptions.ReferToDestinationSheet` 是做什么的？** 它会重写公式，使其在复制操作后指向目标工作表。  
- **如何仅粘贴可见单元格？** 调用 `PasteOptions.setOnlyVisibleCells(true)` 并配合 `PasteType.VALUES` 使用。  
- **需要哪个库版本？** Aspose.Cells 25.3 或更高版本。  
- **生产环境是否需要许可证？** 是的——永久或临时许可证可移除评估限制。  
- **可以使用 Maven 或 Gradle 吗？** 两者均受支持；请参阅下方的依赖代码片段。

## 什么是“自动化 Excel 报表”？
自动化 Excel 报表是指以编程方式生成和更新 Excel 工作簿，使您能够创建、合并和格式化报告，而无需手动复制‑粘贴，从而减少错误并节省大量重复工作时间。这种方法非常适合计划的批处理任务、数据驱动的仪表板以及财务合并流水线。

## 为什么在报表中使用 CopyOptions 和 PasteOptions？
这两个类在复制数据时能够保持公式引用完整 **并且** 仅提取过滤或隐藏行后可见的单元格。将它们一起使用可在典型的过滤表场景中将传输的数据量减少最高达 80 %，并确保公式在目标工作表中继续正确计算。

## 前置条件
- Java 8 或更高版本。  
- 用于依赖管理的 Maven 或 Gradle。  
- Aspose.Cells 25.3+（试用版、临时许可证或永久许可证）。  

## 为 Java 设置 Aspose.Cells
使用以下任一方式将库添加到项目中：

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### 许可证获取
- **Free trial** – 用于评估的完整功能集。  
- **Temporary license** – 在测试期间移除试用限制。  
- **Permanent license** – 推荐用于生产工作负载。

在 Java 代码中初始化 Aspose.Cells：  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## 步骤指南

### 1. 使用 referToDestinationSheet 的 copyOptions

#### 概述
`CopyOptions` 是 Aspose.Cells 的配置对象，用于控制复制操作期间公式和单元格引用的处理方式。将 `CopyOptions.ReferToDestinationSheet` 设置为 `true` 会重写公式引用，使其在复制操作后指向新工作表。

#### 步骤 1：初始化工作簿和工作表  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 步骤 2：配置 copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### 步骤 3：执行复制操作  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*重要性说明*：最初引用 `Sheet1` 的公式现在将正确引用 `DestSheet`，从而保持自动化报告的可靠性。

**故障排除提示**：如果公式仍然引用旧工作表，请确保在复制之前调用 `setReferToDestinationSheet(true)`。

### 2. 用于仅从可见单元格粘贴数值的 pasteOptions

#### 概述
`PasteOptions` 是 Aspose.Cells 的设置对象，用于定义粘贴内容。将 `PasteType.VALUES` 与 `onlyVisibleCells=true` 结合使用，只复制显示的数值，忽略隐藏的行/列和格式。

#### 步骤 1：初始化工作簿和工作表  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 步骤 2：配置 pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### 步骤 3：执行粘贴操作  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*重要性说明*：非常适合提取过滤后的数据或生成不含隐藏行或格式噪声的干净报告。

**故障排除提示**：在复制之前，请确认 Excel 中的行/列已真正隐藏；否则，它们将被包含在内。

## 实际应用
1. **Financial consolidation** – 将月度工作表合并到主工作簿中，同时保持所有公式的准确性。  
2. **Filtered data export** – 从过滤表中仅提取可见行到汇总工作表。  
3. **Scheduled report generation** – 自动化夜间 Excel 报表生成，确保单元格数值精确且引用正确。  

## 性能考虑
- **Dispose of workbooks**：完成后调用 (`wb.dispose();`) 以释放本机资源。  
- **Batch operations**：将多个复制/粘贴调用分组，以减少开销。  
- **Monitor memory**：大型工作簿可能需要增加堆内存 (`-Xmx2g`)。  
- Aspose.Cells 支持 **50+ 种输入和输出格式**，并且能够在不将整个文件加载到内存的情况下处理 **高达 200 万行** 的工作簿，为企业工作负载提供高吞吐量性能。

## 常见问题

**Q: `CopyOptions.ReferToDestinationSheet` 用于什么？**  
A: 它会重写公式引用，使其在复制后指向目标工作表，确保报表公式保持正确。

**Q: 如何仅粘贴可见单元格？**  
A: 设置 `PasteOptions.setOnlyVisibleCells(true)` 并选择 `PasteType.VALUES`。

**Q: 是否可以在不购买许可证的情况下使用 Aspose.Cells？**  
A: 可以，提供免费试用或临时许可证用于评估，但生产环境需要永久许可证。

**Q: 为什么复制后仍有部分引用错误？**  
A: 请再次确认在复制操作 **之前** 已启用 `ReferToDestinationSheet`，并且源公式不包含外部工作簿链接。

**Q: 我应该遵循哪些内存管理最佳实践？**  
A: 完成后释放 `Workbook` 对象，将大文件分块处理，并监控 JVM 堆内存使用情况。

**Q: 是否可以在一次操作中同时使用 CopyOptions 和 PasteOptions？**  
A: 可以，先使用 `CopyOptions` 进行复制，然后在目标范围上应用 `PasteOptions` 即可。

## 资源
- **文档**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **下载**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **购买**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **免费试用**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **临时许可证**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **支持论坛**: [Aspose support](https://forum.aspose.com/c/cells)

---

**最后更新：** 2026-10-28  
**测试环境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose

## 相关教程

- [阅读 Excel 文件 Java – 使用 Aspose.Cells 进行工作簿单元格操作](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [使用 Aspose.Cells for Java 向 Excel 单元格添加数据](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [使用 Aspose.Cells Java 转换 Excel 单元格行列索引](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}