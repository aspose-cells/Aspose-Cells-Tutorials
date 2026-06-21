---
category: general
date: 2026-06-21
description: Create new workbook in Java and export Excel to XLSB. Learn how to add
  custom property Excel, save workbook as XLSB, and more.
draft: false
keywords:
- create new workbook
- create excel workbook java
- export excel to xlsb
- save workbook as xlsb
- add custom property excel
language: en
og_description: Create new workbook in Java, add custom property Excel, and export
  Excel to XLSB with a concise, runnable example.
og_title: Create New Workbook in Java – Complete Programming Guide
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create new workbook in Java and export Excel to XLSB. Learn how to
    add custom property Excel, save workbook as XLSB, and more.
  headline: Create New Workbook in Java – Step‑by‑Step Guide
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Create New Workbook in Java – Step‑by‑Step Guide
url: /java/workbook-operations/create-new-workbook-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create New Workbook in Java – Complete Programming Guide

Ever wondered how to **create new workbook** in Java without wrestling with low‑level file streams? You’re not alone. Whether you’re building a reporting engine or need to ship a project‑specific Excel file, the ability to spin up an Excel workbook programmatically is a must‑have skill.  

In this tutorial we’ll walk through the entire process: from initializing a workbook, adding a custom property Excel, to finally **export Excel to XLSB** and **save workbook as XLSB**. By the end you’ll have a ready‑to‑run code sample that you can drop into any Maven or Gradle project.

> **Pro tip:** The example uses the Aspose.Cells for Java library because it natively supports XLSB (binary) format and custom document properties. If you prefer an open‑source alternative, Apache POI can also do the job, but the API is a bit more verbose.

## What You’ll Need

- **Java Development Kit (JDK) 8+** – any recent version works.
- **Aspose.Cells for Java** (or Apache POI) – we’ll show the Maven dependency.
- A modest IDE (IntelliJ IDEA, Eclipse, VS Code) – whatever you like.
- A folder you have write permission to – the tutorial will save `output.xlsb` there.

Now that the prerequisites are out of the way, let’s dive in.

![Diagram illustrating how to create new workbook, add custom property, and export to XLSB format](/images/create-new-workbook-java.png){alt="create new workbook Java diagram"}

## Step 1: Set Up the Project and Add the Dependency

Before you can **create excel workbook java**, you need the library on your classpath.

If you’re using Maven, add this to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

For Gradle, place the following in `build.gradle`:

```groovy
implementation 'com.aspose:aspose-cells:24.10'
```

> **Why this matters:** Aspose.Cells abstracts away the binary XLSB structure, letting you focus on business logic instead of file format quirks.

## Step 2: Initialize a New Workbook (the Core of “Create New Workbook”)

Creating a fresh workbook is as simple as invoking the `Workbook` constructor. Think of this as opening a blank notebook where you’ll later write data.

```java
import com.aspose.cells.*;

public class WorkbookCreator {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook instance
        Workbook workbook = new Workbook();   // <-- create new workbook
```

The `Workbook` object represents the entire Excel file in memory. At this point it contains a single default worksheet named “Sheet1”.

## Step 3: Access the First Worksheet and Prepare It

Most real‑world scenarios start by grabbing the default sheet (or adding a new one). Here we’ll fetch the first worksheet, which is index `0`.

```java
        // Step 3: Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

You can rename the sheet, set column widths, or apply styles right after this line—everything is possible before you even think about saving.

## Step 4: Add a Custom Property Excel – Why It’s Useful

Custom document properties let you embed metadata that downstream systems can read. For example, a “ProjectId” helps a reporting service group files automatically.

```java
        // Step 4: Add a custom property (ProjectId = 12345)
        workbook.getCustomProperties().add("ProjectId", "12345"); // <-- add custom property excel
```

Under the hood, Aspose adds this to the workbook’s `CustomDocumentProperties` part, which is visible in Excel under **File → Info → Properties → Advanced Properties**.

## Step 5: Populate the Worksheet (Optional but Demonstrative)

Let’s sprinkle a couple of rows so you can see the file isn’t just empty scaffolding.

```java
        // Step 5: Write some sample data
        Cells cells = sheet.getCells();
        cells.get("A1").putValue("Hello");
        cells.get("B1").putValue("World");
        cells.get("A2").putValue("Project ID");
        cells.get("B2").putValue("12345");
```

You could, of course, pull data from a database, generate charts, or apply conditional formatting—Aspose supports all of that.

## Step 6: Export Excel to XLSB and Save Workbook as XLSB

Now comes the moment of truth: persisting the in‑memory workbook to a binary XLSB file. The `save` method takes the file path and the format type.

```java
        // Step 6: Define output path (adjust to your environment)
        String outputPath = "YOUR_DIRECTORY/output.xlsb";

        // Step 7: Save the workbook as XLSB (binary) format
        workbook.save(outputPath, SaveFormat.XLSB); // <-- export excel to xlsb
        System.out.println("Workbook saved successfully at " + outputPath);
    }
}
```

When you run this program, you’ll find `output.xlsb` in the folder you specified. Opening the file in Excel will show the data we wrote and the custom property under **File → Info**.

### Expected Output

```
Workbook saved successfully at YOUR_DIRECTORY/output.xlsb
```

And if you inspect the file in Excel, the **ProjectId** custom property will be present with the value `12345`.

## Step 7: Verify the Custom Property (Optional Debug Step)

If you want to double‑check that the property survived the round‑trip, you can reload the file and read it back:

```java
        // Optional verification
        Workbook loaded = new Workbook(outputPath);
        String projectId = loaded.getCustomProperties().get("ProjectId").getValue().toString();
        System.out.println("Loaded ProjectId: " + projectId); // Should print 12345
```

Running the verification block prints:

```
Loaded ProjectId: 12345
```

That confirms the **add custom property excel** step worked as intended.

## Common Pitfalls and How to Avoid Them

- **Missing Dependency:** If you forget the Aspose.Cells JAR, you’ll get `ClassNotFoundException`. Double‑check your `pom.xml` or `build.gradle`.
- **Write Permissions:** Attempting to save to a protected folder throws an `IOException`. Use a directory you own or adjust permissions.
- **Incorrect SaveFormat:** Using `SaveFormat.XLSX` will produce an XML‑based file, not the binary XLSB you expect. Always pass `SaveFormat.XLSB` when you need the compact format.
- **Custom Property Name Collisions:** Excel reserves some property names (e.g., `Author`). Pick unique identifiers like `ProjectId` to avoid overwriting built‑in metadata.

## Extending the Example

Now that you’ve mastered the basics, consider these next steps:

- **Add Multiple Custom Properties:** Store version numbers, timestamps, or user IDs.
- **Create Multiple Worksheets:** Use `workbook.getWorksheets().add("Data")` for a multi‑sheet report.
- **Apply Styles and Formatting:** Bold headers, set cell colors, or add data validation.
- **Stream the Workbook Directly to HTTP Response:** Perfect for web apps that generate reports on the fly.

Each of these enhancements builds on the same core concepts we covered: **create new workbook**, **add custom property excel**, **export excel to xlsb**, and **save workbook as xlsb**.

---

## Conclusion

We’ve walked through a complete, runnable example that shows how to **create new workbook** in Java, embed a custom property, and **export Excel to XLSB** using Aspose.Cells. The code is self‑contained, explains the *why* behind each line, and even includes a verification snippet to prove the custom property persisted.  

Armed with this foundation, you can now automate Excel generation for invoices, dashboards, or any data‑driven document your application needs. Want to explore open‑source alternatives? Swap Aspose for Apache POI and adjust the API calls—principles remain identical.  

Feel free to experiment: change the property name, add charts, or switch the output format to `XLSX` for a human‑readable version. If you hit a snag, the Aspose documentation and community forums are excellent resources. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}