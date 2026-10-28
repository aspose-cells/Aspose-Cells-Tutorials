---
date: '2026-02-22'
description: 了解如何在 Java 中使用 Aspose.Cells，通过 CopyOptions 和 PasteOptions 自动化 Excel 报表，保持公式准确并仅粘贴可见值。
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: 自动化 Excel 报表——在 Java 中使用 Aspose.Cells 精通 CopyOptions 与 PasteOptions
url: /zh/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 自动化 Excel 报表：Java 中的 CopyOptions 与 PasteOptions

您是否希望使用 Java **自动化 Excel 报表**？借助 Aspose.Cells，您可以以编程方式复制、粘贴和调整公式，使报告保持准确，并且仅传输所需的数据。在本教程中，我们将介绍两个关键功能——**CopyOptions.ReferToDestinationSheet** 和 **PasteOptions**——帮助您保留公式引用并仅从可见单元格粘贴数值。

## 快速回答
- **`CopyOptions.ReferToDestinationSheet` 的作用是什么？** 在复制数据时将公式调整为指向目标工作表。  
- **如何仅粘贴可见单元格？** 使用 `PasteType.VALUES` 并将 `PasteOptions.setOnlyVisibleCells(true)` 设置为 true。  
- **需要哪个库版本？** Aspose.Cells 25.3 或更高版本。  
- **生产环境是否需要许可证？** 是的，永久或临时许可证可解除评估限制。  
- **可以使用 Maven 或 Gradle 吗？** 两者均受支持；请参阅下面的依赖代码片段。

## 什么是“自动化 Excel 报表”？
自动化 Excel 报表是指以编程方式生成、合并和格式化 Excel 工作簿，消除手动复制‑粘贴步骤并降低错误率。Aspose.Cells 提供了丰富的 API，使 Java 开发者能够大规模操作电子表格。

## 为什么在报表中使用 CopyOptions 和 PasteOptions？
- **在工作表之间移动数据时保持公式完整性**。  
- **排除隐藏的行/列**，使报表保持简洁聚焦。  
- **提升性能**，仅复制必要的数据，而不是整个范围。

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
- **免费试用** – 完整功能集用于评估。  
- **临时许可证** – 在测试期间移除试用限制。  
- **永久许可证** – 推荐用于生产工作负载。

在 Java 代码中初始化 Aspose.Cells：  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## 步骤指南

### 1. 使用 ReferToDestinationSheet 的 CopyOptions

#### 概述
将 `CopyOptions.ReferToDestinationSheet` 设置为 `true` 会重写公式引用，使其在复制操作后指向新工作表。

#### 步骤 1：初始化 Workbook 和 Worksheet  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 步骤 2：配置 CopyOptions  
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

*重要性说明*：原本引用 `Sheet1` 的公式现在将正确引用 `DestSheet`，从而保证自动化报表的可靠性。

**故障排除提示**：如果公式仍然引用旧工作表，请确保在复制之前调用 `setReferToDestinationSheet(true)`。

### 2. 使用 PasteOptions 从可见单元格仅粘贴数值

#### 概述
`PasteOptions` 允许您定义粘贴内容。将 `PasteType.VALUES` 与 `onlyVisibleCells=true` 结合使用，可仅复制显示的数值，忽略隐藏的行/列和格式。

#### 步骤 1：初始化 Workbook 和 Worksheet  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 步骤 2：配置 PasteOptions  
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

*重要性说明*：非常适合提取过滤后的数据或生成不含隐藏行和格式噪声的清晰报表。

**故障排除提示**：在复制前请确认 Excel 中的行/列已真正隐藏；否则，它们仍会被包含。

## 实际应用
1. **财务合并** – 将月度工作表合并到主工作簿中，同时保持所有公式的准确性。  
2. **过滤数据导出** – 将过滤表中的可见行提取到汇总工作表。  
3. **定时报表生成** – 自动化夜间 Excel 报表创建，确保单元格数值精确且引用正确。

## 性能考虑
- **在完成后释放 Workbook**（`wb.dispose();`）以释放本机资源。  
- **批量操作** – 将多个复制/粘贴调用分组，以降低开销。  
- **监控内存** – 大型工作簿可能需要增加堆内存（`-Xmx2g`）。

## 常见问题

**Q1：`CopyOptions.ReferToDestinationSheet` 的用途是什么？**  
A：它会重写公式引用，使其在复制后指向目标工作表，从而确保报表公式保持正确。

**Q2：如何仅粘贴可见单元格？**  
A：设置 `PasteOptions.setOnlyVisibleCells(true)` 并选择 `PasteType.VALUES`。

**Q3：可以在不购买许可证的情况下使用 Aspose.Cells 吗？**  
A：可以，提供免费试用或临时许可证用于评估，但生产环境需要永久许可证。

**Q4：复制后为何仍有部分引用错误？**  
A：请再次确认在复制操作之前已启用 `ReferToDestinationSheet`，并且源公式不包含外部工作簿链接。

**Q5：应遵循哪些内存管理最佳实践？**  
A：完成后释放 `Workbook` 对象，分块处理大型文件，并监控 JVM 堆内存使用情况。

**Q6：可以在一次操作中同时使用 CopyOptions 和 PasteOptions 吗？**  
A：可以，先使用 `CopyOptions` 进行复制，然后在目标范围上应用 `PasteOptions`。

## 资源
- **文档**： [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **下载**： [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **购买**： [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **免费试用**： [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **临时许可证**： [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **支持论坛**： [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**最后更新：** 2026-02-22  
**测试环境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose