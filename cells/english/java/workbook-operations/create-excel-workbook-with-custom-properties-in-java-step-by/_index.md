---
category: general
date: 2026-08-04
description: Create Excel workbook in Java and learn how to add custom property like
  author. Follow this complete tutorial to set properties and save as XLSB.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add custom property
- how to add author
- how to set property
- add author excel
language: en
lastmod: 2026-08-04
og_description: Create Excel workbook in Java, then learn how to add author and other
  custom properties. This guide shows the exact code and explains each step.
og_image_alt: Screenshot of a Java IDE displaying code that creates an Excel workbook
  and adds a custom author property
og_title: Create Excel workbook with custom properties – Java tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create Excel workbook in Java and learn how to add custom property
    like author. Follow this complete tutorial to set properties and save as XLSB.
  headline: Create Excel workbook with custom properties in Java – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- Java
- Aspose.Cells
- Custom Properties
- Workbook
title: Create Excel workbook with custom properties in Java – step‑by‑step guide
url: /java/workbook-operations/create-excel-workbook-with-custom-properties-in-java-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook with custom properties in Java – step‑by‑step guide

If you need to **create Excel workbook** programmatically, this tutorial shows you exactly how. You’ll see how to add a custom property such as an author, save the file as an XLSB workbook, and verify that the property persists.  

Working with Excel files from Java often requires more than just data – metadata like author, project name, or version can be crucial for downstream processes. In this guide you’ll learn to **add custom property**, understand **how to set property** values, and discover the best way to **how to add author** information to an Excel workbook.

## Prerequisites

Before you start, make sure you have:

* Java 17 or later installed  
* Maven or Gradle for dependency management  
* An Aspose.Cells for Java license (the free evaluation works for testing)  

These requirements ensure the code runs without additional setup.

## Step 1: Set up the Aspose.Cells dependency

Add the Aspose.Cells library to your project. With Maven, include:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

If you prefer Gradle:

```groovy
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** Keep the library up‑to‑date; newer versions add support for additional Excel formats and improve performance.

## Step 2: Create Excel workbook

The first logical block is to **create excel workbook**. This object represents the entire file and gives you access to worksheets, styles, and properties.

```java
import com.aspose.cells.*;

public class CustomPropertyDemo {

    public static void main(String[] args) throws Exception {
        // Step 2‑1: Initialize a new workbook (this creates a default worksheet)
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        Worksheet sheet = workbook.getWorksheets().get(0);
        sheet.setName("Report");
```

Creating the workbook is the foundation; without it you cannot add any custom metadata. The `Workbook` class also provides a `getCustomProperties()` collection that stores key‑value pairs.

## Step 3: Add custom property – how to add author

Now we address **how to add author** to the workbook. The author is just a custom property named `"Author"`.

```java
        // Step 3‑1: Access the custom properties collection
        CustomDocumentPropertyCollection props = workbook.getWorksheets().getCustomProperties();

        // Step 3‑2: Add the "Author" property with the value "Alice"
        props.add("Author", "Alice");

        // Verify that the property was added (helps during debugging)
        System.out.println("Added property: Author = " + props.get("Author").getValue());
```

The method `add(String name, Object value)` is the standard way to **add custom property**. You can store strings, numbers, dates, or boolean values. The above line demonstrates **how to set property** for a simple text value.

### How to add author Excel – alternative approaches

* **Using built‑in document properties:** Aspose.Cells also supports built‑in properties like `Author`.  
  ```java
  workbook.getBuiltInDocumentProperties().setAuthor("Alice");
  ```
* **Multiple authors:** If you need a list, store a delimited string or use a custom JSON payload.  
  ```java
  props.add("Authors", "Alice;Bob;Charlie");
  ```

Both approaches are valid; the custom property route gives you full control over naming and data type.

## Step 4: Save the workbook as XLSB

Saving the file in binary format (XLSB) preserves the custom property while keeping the file size small.

```java
        // Step 4‑1: Define the output path
        String outputPath = "output/CustomProp.xlsb";

        // Step 4‑2: Save using the XLSB format
        workbook.save(outputPath, SaveFormat.XLSB);

        System.out.println("Workbook saved to " + outputPath);
    }
}
```

When you open `CustomProp.xlsb` in Excel and inspect **File → Info → Properties**, you’ll see the **Author** entry you added. This confirms that the **add author excel** operation succeeded.

## How to read a custom property (verification)

Sometimes you need to read back the value to verify or display it in your UI.

```java
        // Load the workbook we just saved
        Workbook loaded = new Workbook(outputPath);

        // Retrieve the custom property
        CustomDocumentProperty authorProp = loaded.getWorksheets().getCustomProperties().get("Author");
        if (authorProp != null) {
            System.out.println("Loaded Author: " + authorProp.getValue());
        } else {
            System.out.println("Author property not found.");
        }
```

This snippet shows **how to set property** and then read it, proving that the metadata survived the save/load cycle.

## Common pitfalls and edge cases

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| **Property name collision** | Adding a property with a name that already exists replaces the old value. | Check `containsKey(name)` before `add`, or use `props.get(name).setValue(newValue)`. |
| **Unsupported data type** | Passing an object that Aspose.Cells cannot serialize (e.g., custom class). | Convert the value to a supported type (`String`, `Integer`, `Date`, `Boolean`). |
| **Saving to a read‑only folder** | `IOException` on `workbook.save`. | Ensure the target directory exists and the process has write permissions. |
| **Using older Aspose.Cells version** | Some formats like XLSB were added in later releases. | Upgrade to the latest version (as shown in the dependency block). |

Handling these scenarios makes your solution robust for production environments.

## Full, runnable example

Below is the complete program that you can copy, paste, and run after adding the Maven/Gradle dependency.

```java
import com.aspose.cells.*;

public class CustomPropertyDemo {

    public static void main(String[] args) throws Exception {
        // 1. Create a new workbook (create excel workbook)
        Workbook workbook = new Workbook();

        // 2. Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        worksheet.setName("Report");

        // 3. Add a custom property – how to add author
        CustomDocumentPropertyCollection customProps = workbook.getWorksheets().getCustomProperties();
        customProps.add("Author", "Alice");               // add custom property
        System.out.println("Added property: Author = " + customProps.get("Author").getValue());

        // 4. Save as XLSB (preserves the custom property)
        String outputPath = "output/CustomProp.xlsb";
        workbook.save(outputPath, SaveFormat.XLSB);
        System.out.println("Workbook saved to " + outputPath);

        // 5. Load the workbook again to verify the property (how to set property)
        Workbook loaded = new Workbook(outputPath);
        CustomDocumentProperty author = loaded.getWorksheets().getCustomProperties().get("Author");
        if (author != null) {
            System.out.println("Loaded Author: " + author.getValue());
        } else {
            System.out.println("Author property not found.");
        }
    }
}
```

**Expected output**

```
Added property: Author = Alice
Workbook saved to output/CustomProp.xlsb
Loaded Author: Alice
```

When you open `CustomProp.xlsb` in Microsoft Excel, the **Author** custom property appears under **File → Info → Properties**.

## Conclusion

You now know how to **create Excel workbook** in Java, **add custom property**, and specifically **how to add author** metadata. The guide covered the full workflow—from dependency setup, through property creation, to saving and verification—so you can integrate this pattern into any reporting or automation project.

**Next steps**

* Explore **how to set property** for dates, numbers, or boolean flags.  
* Use the same technique to store a document version or a unique identifier (`add custom property` “DocId”).  
* Combine custom properties with **Aspose.Cells built‑in properties** for richer metadata.  

Feel free to experiment with different property names, multiple worksheets, and other file formats like XLSX or CSV. Adding metadata early in your pipeline makes downstream processing, auditing, and user experience far smoother. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Add Worksheets in Excel Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/worksheet-management/add-spreadsheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}