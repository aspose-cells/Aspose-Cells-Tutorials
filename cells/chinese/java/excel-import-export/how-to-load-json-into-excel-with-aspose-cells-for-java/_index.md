---
category: general
date: 2026-10-07
description: 学习如何使用 Aspose.Cells 将 JSON 加载到 Excel 并从 JSON 生成 XLSX。此一步一步的指南还展示了如何从
  JSON 填充 Excel 并将工作簿保存为 XLSX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: zh
lastmod: 2026-10-07
og_description: 使用 Aspose.Cells for Java 将 JSON 加载到 Excel 并从 JSON 生成 XLSX。请按照本指南将
  JSON 填充到 Excel 并将工作簿保存为 XLSX。
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: 使用 Aspose.Cells 将 JSON 加载到 Excel – 完整的 Java 指南
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何使用 Aspose.Cells for Java 将 JSON 加载到 Excel
url: /zh/java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells for Java 将 JSON 加载到 Excel 中

如果您需要 **将 JSON 加载到 Excel**，本教程将向您展示一种使用 Aspose.Cells for Java 的可靠方法。您将看到如何从 JSON 生成 XLSX、从 JSON 填充 Excel，最后 **将工作簿保存为 XLSX**——全部在一个独立的程序中完成。

在电子表格中处理 JSON 很常见，尤其是当您从 Web 服务、API 或 NoSQL 存储导出数据时。阅读完本指南后，您将拥有一个可直接运行的 Java 类，它可以从 JSON 创建工作簿并将结果写入磁盘文件。

## 先决条件

在开始之前，请确保您具备以下条件：

* 已安装 Java 8 或更高版本（代码使用标准的 Java 特性）。
* Aspose.Cells for Java 库（版本 23.10 或更高）。您可以从 [Aspose 网站](https://downloads.aspose.com/cells/java) 或 Maven Central 获取。
* 一个 IDE 或者简单的文本编辑器以及用于编译和运行 Java 代码的终端。
* 对 JSON 语法和 Excel 概念有基本了解。

> **专业提示：** 如果您使用 Maven，请将以下依赖添加到 `pom.xml` 中，以避免手动管理 JAR：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## 步骤 1：设置项目并导入所需类

创建一个名为 `JsonToExcelDemo` 的新 Java 类。导入在工作簿创建、工作表处理以及 Smart Marker 处理时需要的 Aspose.Cells 类。

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*此步骤的重要性：* 导入正确的类可确保编译器能够找到 Aspose.Cells API。`Workbook` 类代表 Excel 文件，而 `SmartMarkerProcessor` 则负责 JSON 到 Excel 的转换。

## 步骤 2：定义将加载到 Excel 的 JSON 源

在本示例中，我们使用一个包含两个对象的小 JSON 数组。在实际场景中，您可以从文件、REST 接口或数据库读取 JSON。

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*此步骤的重要性：* JSON 字符串是 **从 JSON 填充 Excel** 操作的数据源。将 JSON 保存在 `String` 变量中，可轻松传递给 `SmartMarkerProcessor`。

## 步骤 3：创建新工作簿并获取第一个工作表

一个全新的工作簿为您提供干净的起点。第一个工作表（索引 0）是我们将插入 Smart Marker 的位置。

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*此步骤的重要性：* Aspose.Cells 使用 `Workbook` 对象，稍后可以将其保存为 XLSX 文件。访问第一个 `Worksheet` 使我们能够在已知的单元格地址放置标记。

## 步骤 4：插入 Smart Marker，指示 Aspose.Cells 如何处理 JSON

Smart Marker 是占位符，Aspose.Cells 会用来自源的数据替换它们。标记 `&=JSONData.ArrayAsSingle` 告诉库将整个 JSON 数组视为单个单元格的值。

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*此步骤的重要性：* 使用 `ArrayAsSingle` 可避免默认的将每个数组元素展开为单独行的行为。当您希望 JSON 文本原样显示在单元格中，或计划稍后使用公式进行拆分时，这非常有用。

## 步骤 5：使用 JSON 数据源配置 SmartMarkerProcessor

现在将 JSON 字符串绑定到逻辑名称 `JSONData`。处理器将用实际数据替换标记。

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*此步骤的重要性：* `setDataSource` 将标记中使用的名称（`JSONData`）与实际的 JSON 负载关联起来。`process()` 完成繁重的工作：解析 JSON、应用标记逻辑并将结果写入工作表。

## 步骤 6：将生成的工作簿保存为 XLSX 文件

最后，将工作簿写入磁盘。`SaveFormat.XLSX` 常量确保使用正确的 Office Open XML 格式。

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*此步骤的重要性：* 保存文件完成 **从 JSON 生成 XLSX** 工作流。生成的文件可在 Excel、LibreOffice 或任何支持 XLSX 的电子表格程序中打开。

### 完整源代码

将所有部分组合在一起，以下是完整的可运行程序，它 **从 JSON 创建工作簿**、**从 JSON 填充 Excel**，并 **将工作簿保存为 XLSX**。

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### 预期结果

打开 `JsonSingleCell.xlsx` 时，您将在单元格 **A1** 中看到与原始字符串完全相同的 JSON 数组显示：

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

如果您希望每个对象占据单独的行，请将标记替换为 `&=JSONData`（不带 `.ArrayAsSingle`）。处理器随后会将数组展开为各行，演示另一种 **从 JSON 填充 Excel** 的技术。

## 常见变体和边缘情况

| 情况 | 调整 |
|-----------|------------|
| **大型 JSON 负载（> 10 MB）** | 增加 JVM 堆大小（`-Xmx2g`），并考虑流式处理 JSON，以避免 `OutOfMemoryError`。 |
| **嵌套对象** | 在表格中使用层级标记，如 `&=JSONData.Name` 和 `&=JSONData.Age`，将每个属性映射到列。 |
| **JSON 文件而非字符串** | 使用 `java.nio.file.Files.readString(Path.of("data.json"))` 将文件读取为 `String`，并传递给 `setDataSource`。 |
| **需要保留原始 JSON 格式** | 保留 `.ArrayAsSingle` 后缀，或在 JSON 外层使用 CDATA 包裹，如果您计划稍后使用 Excel 公式解析 JSON。 |
| **多个工作表** | 创建额外的工作表（`workbook.getWorksheets().add("Sheet2")`），并在每个工作表上重复插入标记。 |

> **警告：** Smart Marker 区分大小写。确保逻辑名称（`JSONData`）在标记和 `setDataSource` 中完全一致。

## 测试解决方案

1. 编译程序：

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. 运行它：

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. 验证 `JsonSingleCell.xlsx` 是否出现在工作目录中，并且能够无错误打开。

## 接下来您应该学习什么？

以下教程涵盖与本指南演示的技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [从 JSON 创建 Excel 工作簿 – 完整 Aspose.Cells 指南](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [创建 Excel 工作簿 C# – 插入 JSON 并保存为 XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [从 JSON 保存 Excel 工作簿 – 完整指南](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}