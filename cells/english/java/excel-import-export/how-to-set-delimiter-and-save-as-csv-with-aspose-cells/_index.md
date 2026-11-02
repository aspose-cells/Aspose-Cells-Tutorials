---
category: general
date: 2026-08-14
description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
  export CSV strings, and recalculate formulas in Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: en
lastmod: 2026-08-14
og_description: How to set delimiter and save as CSV with Aspose.Cells, limit digits,
  export CSV strings, and recalculate formulas in Java.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: How to set delimiter and save as CSV – Aspose.Cells guide
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: How to set delimiter and save as CSV with Aspose.Cells
url: /java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to set delimiter and save as CSV with Aspose.Cells

If you need to **how to set delimiter** while exporting data from an Excel workbook, this guide shows you a complete, end‑to‑end solution using Aspose.Cells for Java. You’ll learn how to configure the CSV delimiter, limit the number of significant digits, export a CSV string, and refresh dynamic‑array formulas after loading a workbook.

The tutorial covers everything you need to run the code on your machine, including handling special calendars such as the Japanese Emperor reign. By the end, you’ll be able to generate accurate CSV files, control numeric precision, and ensure formulas are up‑to‑date.

## Prerequisites

- Java 17 or later (the code compiles with JDK 11+ as well)
- Aspose.Cells for Java 23.9 or newer – download from the [Aspose website](https://products.aspose.com/cells/java/)
- Basic familiarity with Maven or Gradle for dependency management
- An IDE (IntelliJ IDEA, Eclipse, VS Code) or a simple text editor and command line

> **Pro tip:** Use a dedicated `libs` folder or Maven Central to keep the Aspose.Cells JAR on your classpath. The examples below assume a Maven project.

## Step 1: Set up the Maven project

Create a `pom.xml` with the Aspose.Cells dependency:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

Run `mvn clean compile` to download the library and verify the build succeeds.

## Step 2: How to set delimiter and save as CSV

The primary goal is to change the default comma delimiter to a custom character (e.g., semicolon) when saving an Excel workbook as CSV. Aspose.Cells provides `CsvSaveOptions` for this purpose.

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### Why this works

- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe `'|'`, etc.) works.
- `setSignificantDigits(int)` limits numeric precision, satisfying the **how to limit digits** requirement without manually formatting each cell.

#### Expected output

The file `output.csv` will contain rows like:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Notice that numbers are rounded to five significant digits (e.g., `123.45678` → `123.46`).

## Step 3: How to limit digits when saving CSV

If you need tighter control over numeric formatting, you can also use a `CsvSaveOptions` instance to specify a custom number format string.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` follows .NET style patterns, which Aspose.Cells respects.
- Combining both `setNumberFormat` and `setSignificantDigits` gives you predictable rounding across different locales.

## Step 4: How to export CSV as a string with a custom delimiter

Sometimes you don’t want a physical file; you need the CSV data in memory (e.g., to send as an HTTP response). The `ExportTableOptions` class lets you export a range as a string.

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### When to use this

- Returning CSV from a REST endpoint (`@RestController` in Spring)
- Embedding CSV data into an email attachment without writing to disk
- Performing quick sanity checks during unit tests

## Step 5: How to recalculate formulas after loading a workbook

If your workbook contains formulas—especially **dynamic‑array formulas** introduced in recent Excel versions—you must recalculate them after loading the file. Aspose.Cells automatically refreshes dynamic‑array results, but you still need to invoke `calculateFormula()` for regular formulas.

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### Why recalculate?

- Formulas may reference external data or volatile functions (`NOW()`, `RAND()`) that need fresh values.
- Dynamic‑array formulas (e.g., `=SORT(A1:A10)`) are evaluated automatically, but calling `calculateFormula()` guarantees consistency across all sheets.

## Step 6: Full end‑to‑end example

Below is a single class that demonstrates **how to set delimiter**, **save as CSV**, **limit digits**, **export a CSV string**, **load a workbook with a special calendar**, and **recalculate formulas**. The code is ready to copy‑paste into your project.

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### Verifying the result

1. Open `output.csv` in a text editor – you should see a semicolon (`;`) separating each column.
2. Confirm that numeric columns display at most five significant digits.
3. The console output will print the CSV string generated in step 4.
4. Open `japan_updated.xlsx` in Excel – any formulas that previously displayed `#REF!` or stale values will now show the correct results.

## Common pitfalls and how to avoid them

| Issue | Cause | Fix |
|-------|-------|-----|
| CSV shows extra quotes | Cells contain commas while delimiter is also a comma | Use a different delimiter (`;` or `\t`) via `setDelimiter` |
| Numbers are rounded incorrectly | `setSignificantDigits` applied after custom number format | Apply `setNumberFormat` **before** `setSignificantDigits`


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Load and Save Excel as CSV Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [How to Load a CSV File Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [How to Load CSV Files Using Custom Parsers in Java with Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}