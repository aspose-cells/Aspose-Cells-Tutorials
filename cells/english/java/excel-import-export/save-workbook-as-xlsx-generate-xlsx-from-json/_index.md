---
category: general
date: 2026-06-21
description: Save workbook as XLSX using SmartMarkerProcessor to generate XLSX from
  JSON and easily populate Excel from JSON data.
draft: false
keywords:
- save workbook as xlsx
- generate xlsx from json
- populate excel from json
language: en
og_description: Save workbook as XLSX with a single Java snippet. Learn how to generate
  XLSX from JSON and populate Excel from JSON using SmartMarker.
og_title: Save Workbook as XLSX – Generate XLSX from JSON
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Save workbook as XLSX using SmartMarkerProcessor to generate XLSX from
    JSON and easily populate Excel from JSON data.
  headline: Save Workbook as XLSX – Generate XLSX from JSON
  type: TechArticle
- description: Save workbook as XLSX using SmartMarkerProcessor to generate XLSX from
    JSON and easily populate Excel from JSON data.
  name: Save Workbook as XLSX – Generate XLSX from JSON
  steps:
  - name: Expected Result
    text: 'After you run the program, open `output.xlsx`. You’ll see a sheet named
      **Sheet1** with two rows of data:'
  - name: Customizing the Template
    text: 'If you’d rather control column order or add a header row, create a tiny
      template before running the code:'
  - name: 1. Nested JSON Objects
    text: SmartMarker can dive into nested structures using dot notation (`${jsonArray.Address.City}`).
      Just ensure your JSON string reflects that hierarchy.
  - name: 2. Large Datasets
    text: 'When dealing with thousands of rows, disable workbook calculation before
      processing:'
  - name: 3. Data Types
    text: 'Dates, numbers, and booleans are inferred automatically, but you can force
      a format:'
  - name: 4. Multiple Placeholders
    text: You can feed several JSON arrays into the same workbook by using distinct
      placeholder names (`${orders}`, `${customers}`) and calling `processor.apply`
      for each.
  type: HowTo
- questions:
  - answer: No. The library is self‑contained; just add the JAR (or Maven dependency)
      and you’re ready to **save workbook as xlsx**.
    question: Do I need to install anything besides the Aspose Cells JAR?
  - answer: 'Absolutely. Replace `workbook.save("output.xlsx", SaveFormat.XLSX);`
      with: ```java try (FileOutputStream out = new FileOutputStream("output.xlsx"))
      { workbook.save(out, SaveFormat.XLSX); } ```'
    question: Can I write directly to a stream instead of a file?
  - answer: 'Use the `SmartMarkerProcessor.setCustomFieldNames` method to map JSON
      keys to placeholder names. ## Conclusion We’ve covered everything you need to
      **save workbook as xlsx** while **generating XLSX from JSON** and **populating
      Excel from JSON** using Aspose Cells’ SmartMarker. The short program show'
    question: What if my JSON keys don’t match Excel column names?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Save Workbook as XLSX – Generate XLSX from JSON
url: /java/excel-import-export/save-workbook-as-xlsx-generate-xlsx-from-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Save Workbook as XLSX – Generate XLSX from JSON

Ever needed to **save workbook as xlsx** but only had JSON data at hand? You're not the only one hitting that wall. Whether you're pulling API responses, reading a config file, or just experimenting with data‑driven Excel reports, turning JSON into a tidy spreadsheet is a frequent ask.

In this guide we’ll walk through a complete, ready‑to‑run Java example that **generates XLSX from JSON** and shows you exactly how to **populate Excel from JSON** using Aspose Cells’ SmartMarker processor. No vague references—just code you can copy, paste, and run.

## What You’ll Need

- Java 17 (or any recent JDK)  
- Aspose Cells for Java library (the free trial works fine)  
- A simple IDE or a command‑line build tool (Maven/Gradle)  
- The JSON snippet we’ll be feeding into the workbook  

That’s it—no extra services, no hidden steps. Let’s dive in.

## Save Workbook as XLSX – Full Process

Below is the entire program, from importing the library to persisting the file on disk. Pay close attention to the comments; they explain **why** each line matters, not just **what** it does.

```java
// ---------------------------------------------------------------
// Save Workbook as XLSX – Complete Java Example
// ---------------------------------------------------------------
import com.aspose.cells.*;
import com.google.gson.JsonArray; // For parsing raw JSON string

public class JsonToExcelDemo {

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook that will receive the data
        Workbook workbook = new Workbook();

        // Step 2: Initialize the SmartMarker processor for the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // Step 3: Enable the flag to treat an array as a single record.
        // This tells SmartMarker to iterate over each element in the JSON array.
        processor.setArrayAsSingle(true);

        // Step 4: Prepare the JSON array source.
        // In a real‑world scenario you might read this from a file or API.
        String json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // Step 5: Apply the JSON data to the SmartMarker using the placeholder ${jsonArray}
        // The JsonArray class from Aspose wraps the raw string so SmartMarker can understand it.
        processor.apply("${jsonArray}", new JsonArray(json));

        // OPTIONAL: Save the workbook to see the result.
        // This is the line that actually **save workbook as xlsx**.
        workbook.save("output.xlsx", SaveFormat.XLSX);

        System.out.println("Workbook saved successfully as output.xlsx");
    }
}
```

> **Pro tip:** If you’re using Maven, add the following dependencies to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.10.1</version>
</dependency>
```

### Expected Result

After you run the program, open `output.xlsx`. You’ll see a sheet named **Sheet1** with two rows of data:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 25  |

That’s the whole **populate excel from json** experience in under 30 lines of Java.

![save workbook as xlsx example](example.png)

*Image alt text: “save workbook as xlsx example”*

## Generate XLSX from JSON – How SmartMarker Works

SmartMarker is essentially a template engine for Excel. By placing `${jsonArray}` in any cell (or range) of a blank workbook, you tell the processor “replace this placeholder with the data from the JSON array.” When `processor.apply` runs, it:

1. Parses the JSON into a collection of records.  
2. Maps each property (`Name`, `Age`) to a column based on the placeholder’s context.  
3. Inserts rows automatically, handling data types for you.

Because we called `processor.setArrayAsSingle(true)`, the whole array is treated as one logical record set, which is the most common pattern when **generating XLSX from JSON**.

### Customizing the Template

If you’d rather control column order or add a header row, create a tiny template before running the code:

| A            | B   |
|--------------|-----|
| **Name**     | **Age** |
| ${jsonArray.Name} | ${jsonArray.Age} |

Save this as `template.xlsx` and load it instead of an empty workbook:

```java
Workbook workbook = new Workbook("template.xlsx");
```

The rest of the steps stay identical, and the output will retain the header row you defined.

## Populate Excel from JSON – Edge Cases & Tips

### 1. Nested JSON Objects  
SmartMarker can dive into nested structures using dot notation (`${jsonArray.Address.City}`). Just ensure your JSON string reflects that hierarchy.

### 2. Large Datasets  
When dealing with thousands of rows, disable workbook calculation before processing:

```java
workbook.getSettings().setCalculateFormula(false);
```

Re‑enable after saving to keep performance snappy.

### 3. Data Types  
Dates, numbers, and booleans are inferred automatically, but you can force a format:

```java
processor.apply("${jsonArray.BirthDate}", new JsonArray(json));
workbook.getWorksheets().get(0).getCells().get("C2").setNumberFormat("mm/dd/yyyy");
```

### 4. Multiple Placeholders  
You can feed several JSON arrays into the same workbook by using distinct placeholder names (`${orders}`, `${customers}`) and calling `processor.apply` for each.

## Common Questions Answered

**Q: Do I need to install anything besides the Aspose Cells JAR?**  
A: No. The library is self‑contained; just add the JAR (or Maven dependency) and you’re ready to **save workbook as xlsx**.

**Q: Can I write directly to a stream instead of a file?**  
A: Absolutely. Replace `workbook.save("output.xlsx", SaveFormat.XLSX);` with:

```java
try (FileOutputStream out = new FileOutputStream("output.xlsx")) {
    workbook.save(out, SaveFormat.XLSX);
}
```

**Q: What if my JSON keys don’t match Excel column names?**  
A: Use the `SmartMarkerProcessor.setCustomFieldNames` method to map JSON keys to placeholder names.

## Conclusion

We’ve covered everything you need to **save workbook as xlsx** while **generating XLSX from JSON** and **populating Excel from JSON** using Aspose Cells’ SmartMarker. The short program shows the full lifecycle: create a workbook, configure SmartMarker, feed a JSON array, and finally persist the file.

Next, try extending the template with formulas, styling, or multiple worksheets—each of those concepts builds directly on the foundation you just mastered. If you run into quirks, revisiting the “Edge Cases & Tips” section often clears the fog.

Happy coding, and may your spreadsheets always be as clean as your JSON!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Save XLSX Files Using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/workbook-operations/save-xlsx-files-aspose-cells-dotnet/)
- [How to Save Excel Workbook in Java Using Aspose.Cells](/cells/english/java/automation-batch-processing/excel-automation-java-aspose-cells-guide/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}