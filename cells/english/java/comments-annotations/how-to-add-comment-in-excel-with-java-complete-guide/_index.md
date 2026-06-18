---
category: general
date: 2026-06-18
description: How to add comment in Excel using Java. Learn how to use markers, generate
  Excel comment, create Excel comment, and save Excel with comments in minutes.
draft: false
keywords:
- how to add comment
- how to use markers
- generate excel comment
- create excel comment
- save excel with comments
language: en
og_description: How to add comment in Excel using Java. This tutorial shows how to
  use markers, generate Excel comment, create Excel comment, and save Excel with comments
  efficiently.
og_title: How to Add Comment in Excel with Java – Step‑by‑Step
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add comment in Excel using Java. Learn how to use markers, generate
    Excel comment, create Excel comment, and save Excel with comments in minutes.
  headline: How to Add Comment in Excel with Java – Complete Guide
  type: TechArticle
- description: How to add comment in Excel using Java. Learn how to use markers, generate
    Excel comment, create Excel comment, and save Excel with comments in minutes.
  name: How to Add Comment in Excel with Java – Complete Guide
  steps:
  - name: What’s happening here?
    text: '- `${Name}` tells Aspose to look for a field called `Name` in the data
      source. - `;Comment=Employee: ${Name}` instructs the engine to **create a comment**
      on the same cell, with the text `Employee: John Doe` (once the marker is resolved).
      - `putValue` writes the raw marker into cell **A1**; the proc'
  - name: Edge case – multiple rows
    text: 'If you need a comment per row, switch to a `List<Map<String,Object>>`:'
  - name: Why use `SmartMarkerProcessor`?
    text: '- **Performance:** It parses the sheet only once, even with thousands of
      markers. - **Flexibility:** You can attach comments, formulas, images, and even
      conditional formatting through marker options. - **Maintainability:** Your template
      stays clean—no hard‑coded values litter the sheet.'
  - name: Verifying the result
    text: 'Open `commented.xlsx` in Excel, hover over cell **A1**, and you should
      see a tooltip that reads **Employee: John Doe**. That’s the proof that you successfully
      **create Excel comment** programmatically.'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Smart Markers
title: How to Add Comment in Excel with Java – Complete Guide
url: /java/comments-annotations/how-to-add-comment-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Add Comment in Excel with Java – Complete Guide

Ever wondered **how to add comment** to an Excel sheet programmatically? Maybe you need to stamp a note on each row, or you’re automating a report that must include reviewer remarks. Whatever the case, you’re in the right spot. In this tutorial we’ll walk through the exact steps to **how to use markers**, generate an Excel comment, and finally **save Excel with comments**—all with clean, runnable Java code.

We’ll be using the Aspose.Cells for Java library, because its Smart Marker feature makes inserting comments a breeze. By the end of this guide you’ll be able to **create Excel comment** objects on the fly, customize them, and produce a workbook that looks polished enough to hand to a client.

> **Pro tip:** If you’re not already licensed for Aspose.Cells, the free trial works perfectly for learning and testing.

---

![Diagram showing how a smart marker turns into a comment in an Excel cell](/images/how-to-add-comment-java.png){: .center-image alt="how to add comment in Excel using Java"}

## How to Add Comment in Excel with Java – Overview

In a nutshell, the process looks like this:

1. **Create a workbook** and grab the target worksheet.  
2. **Define a smart marker** that tells Aspose where to drop the comment.  
3. **Prepare a data source** (a simple `Map` works for this demo).  
4. **Run the SmartMarkerProcessor** to replace the marker and inject the comment.  
5. **Save the workbook** so the comment sticks around.

Sounds simple, right? Let’s break each step down, explain *why* we do it, and explore a few edge cases you might run into.

---

## Step 1: Set Up Your Project

Before you can start coding, you need the Aspose.Cells JAR on your classpath. If you’re using Maven, add this snippet to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

If you prefer Gradle, the equivalent is:

```groovy
implementation 'com.aspose:aspose-cells:23.12'
```

> **Why this matters:** The Smart Marker API lives inside `aspose-cells`, and without it the `SmartMarkerProcessor` class simply won’t compile.

Once the library is in place, fire up your IDE (IntelliJ, Eclipse, or VS Code) and create a new Java class called `ExcelCommentDemo`.

---

## Step 2: Define a Smart Marker with a Comment

A *smart marker* is a placeholder that Aspose replaces with data at runtime. The trick for comments is to embed a `Comment` directive right inside the marker string:

```java
// Step 2: Define a smart marker with a comment that includes the employee name
String smartMarker = "${Name;Comment=Employee: ${Name}}";
worksheet.getCells().get("A1").putValue(smartMarker);
```

### What’s happening here?

- `${Name}` tells Aspose to look for a field called `Name` in the data source.
- `;Comment=Employee: ${Name}` instructs the engine to **create a comment** on the same cell, with the text `Employee: John Doe` (once the marker is resolved).
- `putValue` writes the raw marker into cell **A1**; the processor will replace it later.

> **How to use markers** effectively: Keep them short and place them in the cell where you want the comment to appear. You can also attach comments to other cells by writing the marker in a different location.

---

## Step 3: Prepare the Data Source

For this demo a single‑entry `Map` suffices, but in real‑world scenarios you might feed a `List<Map<String,Object>>` or a POJO collection.

```java
// Step 3: Prepare the data source for the smart marker
Map<String, Object> data = Collections.singletonMap("Name", "John Doe");
```

### Edge case – multiple rows

If you need a comment per row, switch to a `List<Map<String,Object>>`:

```java
List<Map<String, Object>> dataList = new ArrayList<>();
dataList.add(Collections.singletonMap("Name", "John Doe"));
dataList.add(Collections.singletonMap("Name", "Jane Smith"));
```

Then you’d write the marker in a column header and let Aspose iterate over the list automatically.

---

## Step 4: Process the Smart Marker – Generate Excel Comment

Now the magic happens. The `SmartMarkerProcessor` reads the worksheet, finds the marker, substitutes the value, and **generates the comment**.

```java
// Step 4: Process the smart marker, inserting the value and generating the comment
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.process(worksheet.getCells(), data);
```

### Why use `SmartMarkerProcessor`?

- **Performance:** It parses the sheet only once, even with thousands of markers.
- **Flexibility:** You can attach comments, formulas, images, and even conditional formatting through marker options.
- **Maintainability:** Your template stays clean—no hard‑coded values litter the sheet.

---

## Step 5: Save Excel with Comments

Finally, write the workbook to disk. The comment is now a first‑class part of the file.

```java
// Step 5: Save the workbook with the generated comment
workbook.save("YOUR_DIRECTORY/commented.xlsx");
```

Make sure `YOUR_DIRECTORY` exists, or use `Paths.get(System.getProperty("user.home"), "commented.xlsx")` for a quick test.

### Verifying the result

Open `commented.xlsx` in Excel, hover over cell **A1**, and you should see a tooltip that reads **Employee: John Doe**. That’s the proof that you successfully **create Excel comment** programmatically.

---

## Common Pitfalls and Pro Tips

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Comment not appearing** | The marker string is malformed (missing braces) | Double‑check the `${}` syntax and ensure `;Comment=` is spelled correctly |
| **Smart marker ignored** | Workbook isn’t saved after processing | Call `processor.process(...)` *before* `workbook.save()` |
| **Multiple comments on same cell** | Re‑processing the same sheet without clearing previous markers | Use `processor.clearMarkers()` or work on a fresh copy of the template |
| **Large data sets cause slowdown** | Processing each row individually | Pass a `List<Map>` to let Aspose handle bulk insertion efficiently |

> **Pro tip:** If you need rich‑text formatting inside the comment (bold, color), retrieve the `Comment` object after processing and modify its `Font` properties.

```java
Comment comment = worksheet.getComments().get(0, 0); // row 0, column 0 = A1
comment.getFont().setBold(true);
comment.getFont().setColor(Color.BLUE);
```

---

## Extending the Example – Generating Comments from a Database

Imagine you have an `employees` table and you want each employee’s name and ID to appear as a comment on their salary cell. The steps stay the same; you only change the data source:

```java
String query = "SELECT Name, Salary FROM employees";
try (Connection conn = DriverManager.getConnection(url, user, pass);
     Statement stmt = conn.createStatement();
     ResultSet rs = stmt.executeQuery(query)) {

    List<Map<String, Object>> rows = new ArrayList<>();
    while (rs.next()) {
        Map<String, Object> row = new HashMap<>();
        row.put("Name", rs.getString("Name"));
        row.put("Salary", rs.getDouble("Salary"));
        rows.add(row);
    }

    // Marker placed in B2 (Salary column)
    worksheet.getCells().get("B2").putValue("${Salary;Comment=Employee: ${Name}}");
    processor.process(worksheet.getCells(), rows);
}
```

Now each salary cell gets a comment with the corresponding employee name. This demonstrates how you can **save Excel with comments** that reflect live data.

---

## Conclusion

We’ve covered everything you need to know to **how to add comment** to an Excel workbook using Java:

- Set up Aspose.Cells and create a workbook.  
- Write a smart marker that includes a `Comment` directive.  
- Feed the marker with a data source (single value or collection).  
- Run `SmartMarkerProcessor` to **generate Excel comment** and replace the placeholder.  
- Finally, **save Excel with comments** and verify the result.

Armed with this knowledge, you can now automate report generation, annotate cells with audit trails, or simply sprinkle helpful notes throughout your spreadsheets—all without manual clicking.

What’s next? Try adding **rich‑text formatting**, attach images to comments, or combine markers with conditional formatting for a truly dynamic workbook. The sky’s the limit, and you’ve just earned a solid shortcut for your next data‑driven project.

Got questions or a cool use‑case you’d like to share? Drop a comment below, and let’s keep the conversation rolling. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Add Image to Excel Comment with Aspose.Cells for Java: A Complete Guide](/cells/english/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)
- [How to Add a Signature Line to an Image in Excel Using Java and Aspose.Cells](/cells/english/java/security-protection/add-signature-line-image-excel-java-aspose-cells/)
- [How to Add HTML‑Rich Text in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/formatting/add-html-rich-text-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}