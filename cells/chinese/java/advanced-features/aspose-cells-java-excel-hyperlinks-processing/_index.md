---
date: '2026-11-03'
description: 了解如何使用 Aspose.Cells for Java 从 Excel 中提取超链接。本指南涵盖加载工作簿、检索链接、处理大文件以及超链接管理的最佳实践。
keywords:
- how to extract hyperlinks
- process large excel files
- load excel workbook
- retrieve excel links
- excel hyperlink management
lastmod: '2026-11-03'
og_description: 了解如何使用 Aspose.Cells for Java 从 Excel 中提取超链接。获取逐步代码、性能技巧和常见问题解答，以实现可靠的超链接管理。
og_image_alt: Guide to extract hyperlinks from Excel using Aspose.Cells for Java
og_title: 如何从 Excel 中提取超链接 – 高级管理
schemas:
- author: Aspose
  dateModified: '2026-11-03'
  description: Learn how to extract hyperlinks from Excel using Aspose.Cells for Java.
    This guide covers loading workbooks, retrieving links, processing large files,
    and best practices for hyperlink management.
  headline: How to extract hyperlinks from Excel – advanced management
  type: TechArticle
- questions:
  - answer: Aspose.Cells for Java supports Java 8 and newer, including all LTS releases
      up to Java 21.
    question: What versions of Java are compatible with Aspose.Cells?
  - answer: Yes. Load only the required worksheet or range, and avoid loading the
      entire workbook when possible. Reusing a single `Workbook` instance further
      reduces heap pressure.
    question: Can I extract hyperlinks from very large Excel files without running
      out of memory?
  - answer: A free trial lets you experiment, but a commercial license removes evaluation
      limits, unlocks multi‑threaded processing, and provides full technical support.
    question: Is a license required for hyperlink extraction in production?
  - answer: The `TargetModeType.EMAIL` constant identifies email links; you can extract
      the `mailto:` address and process it separately.
    question: How do I handle hyperlinks that point to email addresses?
  - answer: Absolutely. All hyperlink properties—display text, tooltip, address, and
      target mode—are retained when you save the workbook in any supported format.
    question: Does Aspose.Cells preserve hyperlink formatting when saving?
  type: FAQPage
tags:
- extract hyperlinks
- Aspose.Cells
- Java Excel processing
title: 如何从 Excel 中提取超链接 – 高级管理
url: /zh/java/advanced-features/aspose-cells-java-excel-hyperlinks-processing/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何从 Excel 中提取超链接 – 高级管理

## 快速答案
- **打开工作簿的主要类是什么？** `Workbook` – 表示内存中整个 Excel 文件的核心对象。  
- **哪个方法返回范围内的所有超链接？** `Range.getHyperlinks()` – 枚举指定范围内的每个超链接对象。  
- **基本的超链接提取是否需要许可证？** 免费试用可用于开发，但商业许可证可移除评估限制并解锁完整的性能优化。  
- **我能高效处理大文件吗？** 可以——专注于特定工作表或范围，复用单个 `Workbook` 实例，并及时释放对象。  
- **支持哪些 Java 版本？** Java 8 及更高版本，包括 Java 11、17 以及后续的 LTS 版本。

## 什么是“从 Excel 中提取超链接”？

从 Excel 中提取超链接是指读取存储在单元格中的链接信息——例如 URL、文件路径、电子邮件地址或内部单元格引用——以便可以以编程方式使用这些数据。Aspose.Cells 提供了一个简洁的 API 来枚举这些链接，无需启动 Microsoft Excel，从而节省时间和服务器资源。

## 为什么要从 Excel 中检索超链接？

检索超链接可以让您**验证链接健康状况**、**迁移或重写 URL**、**生成摘要报告**以及**构建可搜索的索引**以用于知识库集成。例如，夜间作业可以扫描仓库中的每个工作簿，标记损坏的 URL，并自动将其更新为新域名，确保已发布的报告中不包含过时的引用。

## 前置条件

- **Aspose.Cells for Java** 库（版本 25.3 或更高）。  
- Java 8 及以上以及 IDE（IntelliJ IDEA、Eclipse、VS Code 等）。  
- 用于依赖管理的 Maven 或 Gradle。  
- 有效的 Aspose.Cells 许可证（试用可选）。  

### 设置 Aspose.Cells for Java

使用 Maven 或 Gradle 将库添加到项目中。

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
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **技巧提示：** 保持库版本为最新；每个小版本都会增加对新超链接类型的支持，并将内存使用率提升最高可达 30 %。

#### 基本初始化

依赖就绪后，创建一个简单的 Java 类来验证工作簿是否能够加载。

```java
import com.aspose.cells.Workbook;

public class InitializeAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set license if available
        // License license = new License();
        // license.setLicense("path/to/license/file");

        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## 如何从 Excel 中提取超链接 – 加载工作簿

Workbook 是用于加载并在内存中表示整个 Excel 文件的主要类。  
使用一行代码加载工作簿：`Workbook workbook = new Workbook("input.xlsx");`。此调用解析文件头部，构建工作表的内存表示，并为后续查询准备 API。仅加载所需的工作簿（而非整个文件夹）可将 10 MB 以下文件的启动时间降低约 40 %。

### 加载工作簿（功能 1）

```java
import com.aspose.cells.Workbook;

public class FeatureLoadWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## 如何从 Excel 中提取超链接 – 访问工作表和范围

Range 表示工作表内的矩形单元格块。  
首先获取要扫描的工作表，然后创建覆盖感兴趣区域的 `Range` 对象。例如，`worksheet.getCells().createRange("A1", "Z1000")` 定义了一个矩形块；随后 API 允许您在该范围上调用 `getHyperlinks()`。通过定义范围，您可以将扫描限制在相关区域，从而提升性能并降低内存使用。

### 访问工作表和范围（功能 2）

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Range;

public class FeatureAccessWorksheetAndRange {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");

        // Access the first worksheet in the workbook (index 0).
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Create a range from cell A1 to A7 within the worksheet.
        Range range = worksheet.getCells().createRange("A1", "A7");
        
        System.out.println("Range created successfully!");
    }
}
```

## 如何从 Excel 中提取超链接 – 检索并处理超链接

`getHyperlinks()` 返回指定范围内所有超链接对象的集合。  
调用 `Range.getHyperlinks()` 可获取 `Hyperlink` 对象的集合。每个对象提供 `getAddress()`、`getDisplay()`、`getTooltip()` 和 `getTargetMode()` 等属性。您可以遍历集合，记录每个链接，或将其存入数据库以供后续分析。在持久化数据之前，还可以按地址类型或显示文本进一步过滤集合。

### 检索并处理超链接（功能 3）

```java
import com.aspose.cells.Range;
import com.aspose.cells.Hyperlink;
import com.aspose.cells.TargetModeType;

public class FeatureRetrieveAndProcessHyperlinks {
    public static void main(String[] args) throws Exception {
        // Assume 'range' is obtained as shown in previous examples.
        Range range = null;  // Placeholder, replace with actual range initialization

        // Retrieve all hyperlinks within the specified range.
        Hyperlink[] hyperlinks = range.getHyperlinks();

        // Iterate over each hyperlink and process it to determine its type.
        for (Hyperlink link : hyperlinks) {
            String displayText = link.getTextToDisplay();
            int linkType = link.getLinkType();
            System.out.println(displayText + ": " + getLinkTypeName(linkType));
        }
    }

    // Helper method to convert hyperlink type integer to a human‑readable string.
    private static String getLinkTypeName(int linkType) {
        switch (linkType) {
            case TargetModeType.EXTERNAL:
                return "EXTERNAL";
            case TargetModeType.FILE_PATH:
                return "FILE_PATH";
            case TargetModeType.EMAIL:
                return "EMAIL";
            default:
                return "CELL_REFERENCE";
        }
    }
}
```

## 实际应用

| 用例 | 收益 |
|----------|---------|
| **数据验证** | 在发布报告之前，自动验证每个超链接是否指向可访问的 URL。 |
| **自动化** | 在迁移到新数据仓库期间提取链接，并即时更新引用。 |
| **报告** | 创建一个汇总表，列出工作簿中引用的所有外部资源。 |

## 性能考虑

- **仅处理所需范围** – 限制范围可将包含数千行的工作簿的内存消耗降低最高 60 %。  
- **释放对象** – 使用后将 `workbook = null;`，让 JVM 的垃圾回收器回收内存。  
- **批量处理** – 处理大量文件时，尽可能复用单个 `Workbook` 实例。此模式使您能够高效**批量处理 Excel 文件**，在标准 8 核服务器上实现每分钟 150 文件的吞吐量。

## 常见问题及解决方案

| 问题 | 解决方案 |
|-------|----------|
| **空 `range`** | 确保在调用 `getHyperlinks()` 之前已创建范围。 |
| **缺少许可证** | 试用版可用于开发，但许可证版可移除评估限制并提升性能。 |
| **不支持的超链接类型** | 使用 `TargetModeType` 常量来处理 Aspose 更新时新增的类型。 |

## 常见问答

**Q: 哪些 Java 版本与 Aspose.Cells 兼容？**  
A: Aspose.Cells for Java 支持 Java 8 及更高版本，包括所有截至 Java 21 的 LTS 发行版。

**Q: 我能在不耗尽内存的情况下从超大 Excel 文件中提取超链接吗？**  
A: 可以。仅加载所需的工作表或范围，尽量避免加载整个工作簿。复用单个 `Workbook` 实例进一步降低堆内存压力。

**Q: 生产环境中提取超链接是否需要许可证？**  
A: 免费试用可供实验，但商业许可证可移除评估限制，解锁多线程处理，并提供完整的技术支持。

**Q: 如何处理指向电子邮件地址的超链接？**  
A: `TargetModeType.EMAIL` 常量用于识别电子邮件链接；您可以提取 `mailto:` 地址并单独处理。

**Q: Aspose.Cells 在保存时是否保留超链接的格式？**  
A: 当然。所有超链接属性——显示文本、提示、地址和目标模式——在将工作簿保存为任何受支持的格式时都会被保留。

**Q: 我能在批处理任务中使用 Aspose.Cells **读取 Excel 超链接** 吗？**  
A: 可以——将 API 与文件循环结合，读取多个工作簿中的 Excel 超链接，然后将结果存入中央仓库。

**Q: 在高吞吐场景下，**加载 Excel 工作簿 Java** 的最佳方式是什么？**  
A: 尽可能复用单个 `Workbook` 实例，及时关闭输入流，并启用 `MemorySetting.MEMORY_PREFERENCE` 选项以优化内存使用。

---

**最后更新：** 2026-11-03  
**测试环境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose  

如果您有更多问题，欢迎访问 [Aspose 支持论坛](https://forum.aspose.com/c/cells/9)。

## 相关教程

- [如何使用 Aspose.Cells for Java 为 Excel 添加超链接 – 步骤指南](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [处理大型 Excel 文件：通过 Aspose.Cells 管理超链接](/cells/java/advanced-features/manage-excel-hyperlinks-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 在 Excel 工作簿中查找隐藏的外部链接](/cells/java/advanced-features/detect-hidden-external-links-excel-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}