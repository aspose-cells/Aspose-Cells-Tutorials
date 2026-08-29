---
category: general
date: 2026-08-11
description: 在 Java 中使用 Aspose 创建新工作簿，添加自定义属性 Excel，然后将工作簿保存为 XLSB，并提供完整的逐步示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: zh
lastmod: 2026-08-11
og_description: 在 Java 中使用 Aspose 创建新工作簿，添加自定义属性 Excel，并将工作簿保存为 XLSB，提供完整的可直接运行示例。
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: 使用 Aspose 创建新工作簿 – 为 Excel 添加自定义属性
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: 创建新工作簿 Aspose – 添加自定义属性到 Excel 并保存为 XLSB
url: /zh/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建新的工作簿 Aspose – 添加自定义属性 Excel 并保存为 XLSB

如果您需要在 Java 应用程序中 **create new workbook Aspose**，本指南将准确展示如何操作。您将学习 **add custom property Excel**、检索该值，以及 **save workbook as XLSB**，且不会丢失任何元数据。

本教程涵盖从项目设置到已保存文件的验证的全部内容。无需外部文档，只需按照步骤操作并运行代码。

## 前提条件

在开始之前，请确保您拥有：

- 已安装 Java Development Kit (JDK) 8 或更高版本。
- Maven 或 Gradle 用于管理依赖（示例使用 Maven）。
- 有效的 Aspose.Cells for Java 许可证（或使用免费评估模式进行测试）。

## 步骤 1：将 Aspose.Cells 添加到项目中

将 Aspose.Cells Maven 构件添加到您的 `pom.xml` 中。此依赖提供创建 **create new workbook Aspose** 对象所需的类。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **技巧提示：** 如果您更喜欢 Gradle，请将 Maven 代码段替换为等效的 `implementation "com.aspose:aspose-cells:23.12"` 行。

## 步骤 2：创建新的工作簿 Aspose

第一步功能性操作是实例化一个 `Workbook` 对象。该对象在内存中表示一个 Excel 文件，并且是后续所有操作的入口点。

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

创建新的 workbook Aspose 为您提供一个带有默认工作表的空白工作簿，准备进行自定义。

## 步骤 3：添加自定义属性 Excel

自定义属性允许您在 Excel 文件中存储任意元数据。这里我们 **add custom property Excel** 一个名为 `ProjectId` 的属性，数值为数字类型。

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

`add` 方法接受属性名称和任意受支持类型的值（字符串、数字、日期等）。此元数据会随文件一起复制到任何位置。

## 步骤 4：检索并显示自定义属性

读取属性可以验证其是否正确存储。您也可以在业务逻辑中使用检索到的值。

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

将其强制转换为 `int` 可行，因为我们存储的是数值。如果存储的是字符串，请使用 `(String)`。

## 步骤 5：将工作簿保存为 XLSB

现在您 **save workbook as XLSB**。XLSB 格式以二进制形式存储工作簿，打开更快且磁盘占用更小。所有自定义属性会自动保留。

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

如果需要将文件保存到特定目录，请将 `"WithCustomProps.xlsb"` 替换为绝对路径。`SaveFormat.XLSB` 枚举指示 Aspose.Cells 使用二进制格式写入。

## 步骤 6：验证输出

从 IDE 或命令行运行程序：

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

您应该看到：

```
ProjectId = 12345
```

在 Excel 中打开 `WithCustomProps.xlsb`。依次进入 **File → Info → Properties → Advanced Properties → Custom**。`ProjectId` 条目值为 `12345`，这表明 **add custom property excel** 步骤成功，且 **save workbook as xlsb** 操作保留了元数据。

## 常见问题与边缘情况

### 如果需要存储字符串属性怎么办？

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

使用以下方式检索：

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### 能一次添加多个自定义属性吗？

可以。对每个名称/值对重复调用 `add`。Aspose.Cells 对自定义属性的数量没有限制，但请保持总大小在合理范围内，以免导致文件膨胀。

### 二进制格式如何影响性能？

XLSB 文件加载更快，因为它们避免了 XML 解析。对于包含大量行、公式或嵌入图像的工作簿，这一点尤为明显。

### 如果需要处理已有的 XLSX 文件怎么办？

将 `new Workbook()` 构造函数替换为 `new Workbook("ExistingFile.xlsx")`。其余步骤（添加属性、保存为 XLSB）保持不变。

## 完整源代码

以下是完整的可直接运行示例。将其复制到 `src/main/java` 文件夹下名为 `CustomPropertiesXlsb.java` 的文件中。

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

运行此类会生成包含自定义属性的 XLSB 文件，可在任何现代版本的 Microsoft Excel 中打开。

## 结论

您现在已经了解如何使用 Java **create new workbook Aspose**、**add custom property Excel**，以及 **save workbook as XLSB**。示例演示了完整的生命周期：初始化、元数据注入、验证以及二进制序列化。

接下来，探索诸如 **setting document properties**、**working with Excel formulas** 或 **converting between XLSX and XLSB** 等相关主题。它们都基于您刚才使用的 Aspose.Cells API，无需学习新库即可扩展解决方案。

欢迎尝试不同的数据类型、多工作表或密码保护——Aspose.Cells 开箱即支持所有这些场景。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [创建并保存 Excel 工作簿 Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 将 Excel 工作簿创建并保存为 SVG](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [使用 Aspose.Cells for Java 创建 Excel 工作簿并添加标签](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}