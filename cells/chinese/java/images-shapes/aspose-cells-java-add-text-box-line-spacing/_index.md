---
"date": "2025-04-08"
"description": "学习如何使用 Aspose.Cells for Java 在 Excel 工作簿中添加文本框并设置行距。使用样式化的文本形状增强您的工作簿演示效果。"
"title": "使用 Aspose.Cells for Java 在 Excel 中添加文本框并设置行距"
"url": "/zh/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells for Java 在 Excel 中添加文本框并设置行距

## 介绍

创建动态 Excel 报表通常需要自定义文本格式，例如添加具有特定行距的文本框。使用 Aspose.Cells for Java，这一切变得简单高效。本教程将指导您使用 Aspose.Cells for Java 添加样式化的文本形状，从而增强工作簿的演示文稿。

在本指南结束时，您将学习如何：
- 创建新的 Excel 工作簿并访问其工作表
- 向工作表添加文本框形状
- 设置文本形状内的自定义行距
- 将格式化的工作簿保存为 XLSX 格式

让我们从设置您的环境开始。

### 先决条件

开始之前，请确保您已准备好以下内容：
- 您的机器上安装了 Java 开发工具包 (JDK)
- 用于编写 Java 代码的 IDE 或编辑器
- 配置 Maven 或 Gradle 构建系统来管理依赖项

对 Java 编程有基本的了解并熟悉 Excel 文件结构将会很有帮助。

## 设置 Aspose.Cells for Java

使用 Maven 或 Gradle 将 Aspose.Cells 纳入项目的依赖管理中：

**Maven**

将以下依赖块添加到您的 `pom.xml` 文件：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

将其包含在您的 `build.gradle` 文件：

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

接下来，通过选择免费试用、申请临时许可证或购买完整许可证来获取 Aspose.Cells 的许可证。

### 初始化 Aspose.Cells

一旦该库包含在您的项目中，请在您的 Java 应用程序中对其进行初始化：

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // 初始化 Workbook 实例（代表一个 Excel 文件）
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## 实施指南

### 创建工作簿和 Access 工作表

首先创建一个新的 Excel 工作簿并访问其第一个工作表。您将在这里添加文本框。

#### 概述

创建新工作簿可提供一个空白区域，以便根据需要添加数据、形状和格式。

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // 创建新工作簿（Excel 文件）
        Workbook workbook = new Workbook();
        
        // 访问第一个工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### 将文本框添加到工作表

接下来，在选定的工作表中添加一个文本框形状。此形状可以包含您需要的任何文本内容。

#### 概述

文本框是一种多功能工具，可直接在 Excel 工作表中包含自定义文本（例如注释或说明）。

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // 创建新工作簿（Excel 文件）
        Workbook workbook = new Workbook();
        
        // 访问第一个工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 向工作表添加文本框形状
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### 在形状中设置文本

文本框准备好后，设置其内容并格式化其中的文本。

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // 创建新工作簿（Excel 文件）
        Workbook workbook = new Workbook();
        
        // 访问第一个工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 向工作表添加文本框形状
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 设置形状内的文本内容
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### 访问形状中的文本段落

您可以访问文本框中的各个段落以应用特定的格式。

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // 创建新工作簿（Excel 文件）
        Workbook workbook = new Workbook();
        
        // 访问第一个工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 向工作表添加文本框形状
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 设置形状内的文本内容
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 访问形状中的第二段
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### 设置段落行距

自定义行距可以增强可读性。设置方法如下：

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // 创建新工作簿（Excel 文件）
        Workbook workbook = new Workbook();
        
        // 访问第一个工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 向工作表添加文本框形状
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 设置形状内的文本内容
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 访问形状中的第二段
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // 将行距设置为 20 点
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // 配置段落前后的间距
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### 保存工作簿

最后，使用新添加和格式化的文本框保存您的工作簿。

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // 创建新工作簿（Excel 文件）
        Workbook workbook = new Workbook();
        
        // 访问第一个工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 向工作表添加文本框形状
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 设置形状内的文本内容
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 访问形状中的第二段
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // 将行距设置为 20 点
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // 配置段落前后的间距
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // 保存工作簿
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## 结论

您已成功学习了如何使用 Aspose.Cells for Java 在 Excel 工作簿中添加文本框并设置行距。这将提升您创建动态、美观的报表的能力。

## 关键词推荐
- “Aspose.Cells for Java”
- “在 Excel 中添加文本框”
- “在 Excel 中设置行距”
- “带有样式文本的 Excel 工作簿”
- “Java 和 Aspose.Cells”


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}