---
title: "Add Text Box & Set Line Spacing in Excel Using Aspose.Cells for Java"
description: "Learn how to use Aspose.Cells for Java to add text boxes and set line spacing in Excel workbooks. Enhance your workbook presentations with styled text shapes."
date: "2025-04-08"
weight: 1
url: "/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
keywords:
- "Aspose.Cells for Java"
- "Add Text Box in Excel"
- "Set Line Spacing in Excel"
- "Excel Workbook with Styled Text"
- "Java and Aspose.Cells"

---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Add a Text Box and Set Line Spacing in Excel Using Aspose.Cells for Java

## Introduction

Creating dynamic Excel reports often requires custom text formatting, such as adding text boxes with specific line spacing. With Aspose.Cells for Java, this becomes simple and efficient. This tutorial will guide you through enhancing your workbook presentations using Aspose.Cells for Java to add styled text shapes.

By the end of this guide, you'll learn how to:
- Create a new Excel workbook and access its worksheets
- Add a text box shape to a worksheet
- Set custom line spacing inside a text shape
- Save your formatted workbook in XLSX format

Let's start by setting up your environment.

### Prerequisites

Before you begin, ensure you have the following:
- Java Development Kit (JDK) installed on your machine
- An IDE or editor for writing Java code
- Maven or Gradle build system configured to manage dependencies

A basic understanding of Java programming and familiarity with Excel file structures will be beneficial.

## Setting Up Aspose.Cells for Java

Include Aspose.Cells in your project's dependency management using Maven or Gradle:

**Maven**

Add the following dependency block to your `pom.xml` file:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

Include this in your `build.gradle` file:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Next, acquire a license for Aspose.Cells by opting for a free trial, requesting a temporary license, or purchasing a full license.

### Initializing Aspose.Cells

Once the library is included in your project, initialize it within your Java application:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Initialize an instance of Workbook (represents an Excel file)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Implementation Guide

### Create a Workbook and Access Worksheet

Start by creating a new Excel workbook and accessing its first worksheet. This is where you'll add your text box.

#### Overview

Creating a new workbook provides an empty slate to append data, shapes, and formatting as needed.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Create a new Workbook (Excel file)
        Workbook workbook = new Workbook();
        
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Add Text Box to Worksheet

Next, add a text box shape to your selected worksheet. This shape can contain any textual content you need.

#### Overview

Text boxes are versatile tools for including custom texts such as notes or instructions directly within an Excel sheet.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Create a new Workbook (Excel file)
        Workbook workbook = new Workbook();
        
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Add a text box shape to the worksheet
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Set Text in Shape

Once your text box is ready, set its content and format the text inside it.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Create a new Workbook (Excel file)
        Workbook workbook = new Workbook();
        
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Add a text box shape to the worksheet
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Set text content inside the shape
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Access Text Paragraphs in Shape

You can access individual paragraphs within a text box to apply specific formatting.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Create a new Workbook (Excel file)
        Workbook workbook = new Workbook();
        
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Add a text box shape to the worksheet
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Set text content inside the shape
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Access the second paragraph in the shape
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Set Line Spacing of Paragraph

Customizing line spacing can enhance readability. Here's how to set it:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Create a new Workbook (Excel file)
        Workbook workbook = new Workbook();
        
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Add a text box shape to the worksheet
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Set text content inside the shape
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Access the second paragraph in the shape
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Set line spacing to 20 points
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Configure space before and after the paragraph
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Save Workbook

Finally, save your workbook with the newly added and formatted text box.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Create a new Workbook (Excel file)
        Workbook workbook = new Workbook();
        
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Add a text box shape to the worksheet
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Set text content inside the shape
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Access the second paragraph in the shape
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Set line spacing to 20 points
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Configure space before and after the paragraph
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Save the workbook
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Conclusion

You've successfully learned how to add a text box and set line spacing in an Excel workbook using Aspose.Cells for Java. This enhances your ability to create dynamic, visually appealing reports.

## Keyword Recommendations
- "Aspose.Cells for Java"
- "Add Text Box in Excel"
- "Set Line Spacing in Excel"
- "Excel Workbook with Styled Text"
- "Java and Aspose.Cells"


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
