---
category: general
date: 2026-08-11
description: Create new workbook Aspose in Java, add a custom property Excel, then
  save workbook as XLSB with a full step‑by‑step example.
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
language: en
lastmod: 2026-08-11
og_description: Create new workbook Aspose in Java, add a custom property Excel, and
  save the workbook as XLSB with a complete, ready‑to‑run example.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Create new workbook Aspose – add custom property Excel
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
title: Create new workbook Aspose – add custom property Excel and save as XLSB
url: /java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create new workbook Aspose – add custom property Excel and save as XLSB

If you need to **create new workbook Aspose** in a Java application, this guide shows you exactly how to do it. You will learn to **add custom property Excel**, retrieve the value, and **save workbook as XLSB** without losing any metadata.

The tutorial covers everything from project setup to verification of the saved file. No external documentation is required; just follow the steps and run the code.

## Prerequisites

Before you start, make sure you have:

- Java Development Kit (JDK) 8 or higher installed.
- Maven or Gradle to manage dependencies (the example uses Maven).
- An active Aspose.Cells for Java license (or use the free evaluation mode for testing).

## Step 1: Add Aspose.Cells to your project

Add the Aspose.Cells Maven artifact to your `pom.xml`. This dependency provides the classes needed to **create new workbook Aspose** objects.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** If you prefer Gradle, replace the Maven snippet with the equivalent `implementation "com.aspose:aspose-cells:23.12"` line.

## Step 2: Create a new workbook Aspose

The first functional step is to instantiate a `Workbook` object. This object represents an Excel file in memory and is the entry point for all further operations.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Creating a new workbook Aspose gives you a clean workbook with a default worksheet, ready for customizations.

## Step 3: Add custom property Excel

Custom properties let you store arbitrary metadata inside an Excel file. Here we **add custom property Excel** named `ProjectId` with a numeric value.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

The `add` method accepts a property name and a value of any supported type (string, number, date, etc.). This metadata travels with the file wherever you copy it.

## Step 4: Retrieve and display the custom property

Reading back the property verifies that it was stored correctly. You can also use the retrieved value in your business logic.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

Casting to `int` works because we stored a numeric value. If you store a string, use `(String)` instead.

## Step 5: Save workbook as XLSB

Now you **save workbook as XLSB**. The XLSB format stores the workbook in a binary representation, which is faster to open and smaller on disk. All custom properties are preserved automatically.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Replace `"WithCustomProps.xlsb"` with an absolute path if you need the file in a specific directory. The `SaveFormat.XLSB` enum tells Aspose.Cells to write the binary format.

## Step 6: Verify the output

Run the program from your IDE or command line:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

You should see:

```
ProjectId = 12345
```

Open `WithCustomProps.xlsb` in Excel. Navigate to **File → Info → Properties → Advanced Properties → Custom**. The `ProjectId` entry with value `12345` will be listed, confirming that the **add custom property excel** step succeeded and the **save workbook as xlsb** operation retained the metadata.

## Common questions and edge cases

### What if I need to store a string property?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Retrieve it with:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### Can I add multiple custom properties at once?

Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not limit the number of custom properties, but keep the total size reasonable to avoid bloating the file.

### How does the binary format affect performance?

XLSB files load faster because they avoid XML parsing. This is especially noticeable for workbooks with many rows, formulas, or embedded images.

### What if I need to work with an existing XLSX file?

Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`. The rest of the steps (adding properties, saving as XLSB) remain identical.

## Full source code

Below is the complete, ready‑to‑run example. Copy it into a file named `CustomPropertiesXlsb.java` inside your `src/main/java` folder.

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

Running this class produces an XLSB file that contains the custom property and can be opened in any modern version of Microsoft Excel.

## Conclusion

You now know how to **create new workbook Aspose**, **add custom property Excel**, and **save workbook as XLSB** using Java. The example demonstrates the full lifecycle: initialization, metadata injection, verification, and binary serialization.

Next, explore related topics such as **setting document properties**, **working with Excel formulas**, or **converting between XLSX and XLSB**. Each of these builds on the same Aspose.Cells API you just used, so you can extend the solution without learning new libraries.

Feel free to experiment with different data types, multiple worksheets, or password protection—Aspose.Cells supports all of those scenarios out of the box. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Save Excel Workbook Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}