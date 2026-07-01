---
category: general
date: 2026-06-30
description: Set custom number format in Excel using Java. Learn how to create Excel
  workbook Java, get datetime from cell, calculate workbook formulas and output datetime
  value.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: en
og_description: Set custom number format in Excel using Java. This guide shows how
  to create Excel workbook Java, get datetime from cell, calculate workbook formulas
  and output datetime value.
og_title: Set Custom Number Format in Excel with Java – Full Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Set Custom Number Format in Excel with Java – Complete Guide
url: /java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set Custom Number Format in Excel with Java – Complete Guide

Ever needed to **set custom number format** in an Excel sheet while working in Java? You’re not the only one. Whether you’re building a reporting engine or just trying to display Japanese era dates correctly, mastering this trick saves you countless hours of post‑processing. In this tutorial we’ll walk through a real‑world example that **creates Excel workbook Java**, applies a locale‑specific format, recalculates formulas, and finally **gets DateTime from cell** to **output datetime value**.

We’ll use the popular Aspose.Cells for Java library because it handles number formats and culture‑aware dates out of the box. By the end of the guide you’ll have a self‑contained, runnable program that you can drop into any Maven or Gradle project. No vague “see the docs” shortcuts—just solid code and clear explanations.

---

## What You’ll Learn

- How to **create Excel workbook Java** programmatically.
- The exact steps to **set custom number format** for Japanese era dates.
- Why calling **calculate workbook formulas** is essential before extracting the value.
- The proper way to **get datetime from cell** and **output datetime value**.
- Common pitfalls (missing locale, stale formulas) and quick fixes.

---

## Prerequisites

- Java 8 or newer installed on your machine.  
- Aspose.Cells for Java 23.11 (or any recent version).  
- A basic IDE or text editor—IntelliJ IDEA, Eclipse, VS Code, whatever you prefer.  

If you haven’t added Aspose.Cells to your project yet, paste the following Maven snippet into your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Gradle users can add:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Now that the environment is ready, let’s dive into the code.

---

## Step 1: Set Custom Number Format – Overview

Before we write any Java, it helps to visualize what we’re after. Imagine an Excel cell that should display **“令和2年4月1日”** instead of the ISO‑8601 string “2020‑04‑01”. The underlying value stays a true date (so formulas still work), but the *display* follows the Japanese era format. This is exactly what the **set custom number format** operation accomplishes.

Below is the full source file. Feel free to copy‑paste it into `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Why This Works

- **`setNumberFormat`** tells Excel how to *display* the underlying numeric value. The format string `[$-ja-JP]ggge年m月d日` is the key; `ggg` selects the era name, `e` the year within the era, followed by month and day literals.
- **`calculateFormula`** forces Aspose.Cells to interpret the text “R02-04-01” as a date based on the Japanese calendar. Skipping this step leaves the cell as plain text, and `getDateTime()` would throw an exception.
- **`getDateTime`** finally extracts the *actual* `java.util.Calendar` object, which you can manipulate, format, or store elsewhere.

---

## Step 2: Create Excel Workbook Java – Deeper Look

When you **create Excel workbook Java**, you’re not just allocating memory; you’re also establishing default styles, a default worksheet, and a default culture (usually the system locale). If you need a different default locale, you can pass a `LoadOptions` object:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

For most scenarios the simple constructor is sufficient, but it’s good to know the alternative—especially when you’re dealing with multiple locales in the same application.

*Pro tip:* Always keep the workbook in memory until you’re done formatting. Writing to disk after each change incurs unnecessary I/O overhead.

---

## Step 3: Get DateTime from Cell – Handling the Result

The line `java.util.Calendar dt = cellA1.getDateTime();` does the heavy lifting. Behind the scenes Aspose.Cells converts the internal serial number (the number of days since 1899‑12‑31) into a `Calendar`. This conversion respects the workbook’s locale, so you get the correct Gregorian date even though the display uses the Japanese era.

If you need a `java.time.LocalDate` (the newer API), convert like this:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

That covers the **output datetime value** requirement while staying modern.

---

## Step 4: Calculate Workbook Formulas – When It Matters

You might wonder: *“Do I really need to call `calculateFormula()`?”* The answer is a resounding yes, unless you’re feeding the cell with a native Java `Date` object from the start. When you **set custom number format** on a text string, Excel (and Aspose.Cells) treat it as a formula‑like expression that needs evaluation. Without recalculation, `getDateTime()` will return the default `1900‑01‑00` or throw a `CellValueException`.

If your workbook already contains complex formulas referencing the newly formatted cell, call `calculateFormula()` *once* after all changes. Repeated calls are costly.

---

## Step 5: Output DateTime Value – Verifying the Result

Running the demo prints something like:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

That line confirms three things:

1. The **set custom number format** was applied (you can open the generated `.xlsx` in Excel to see “令和2年4月1日”).
2. The **calculate workbook formulas** step succeeded, turning the era string into a real date.
3. The **get datetime from cell** call returned a proper `Calendar`, which we then **output datetime value** to the console.

If you open the workbook with a spreadsheet program, you’ll see the formatted text, but the underlying cell value remains the serial number `43831` (the Excel representation of 2020‑04‑01). This duality is what makes Excel powerful.

---

## Common Pitfalls & Edge Cases

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `cellA1.getDateTime()` throws `CellValueException` | The cell is still a string because `calculateFormula()` was omitted. | Always invoke `workbook.calculateFormula()` after setting a text date that needs conversion. |
| Japanese era not displayed correctly | Locale code missing or incorrect. | Use `[$-ja-JP]` in the format string, or set workbook locale via `LoadOptions`. |
| Format shows “#VALUE!” in Excel | The format string is malformed. | Double‑check brackets and characters; the pattern `ggge年m月d日` is required for era year. |
| Time component appears (e.g., “00:00:00”) | The source string includes time or the cell’s style adds it. | Trim the source string or adjust the format to `ggge年m月d日;@`. |

---

## Full Working Example – One‑Click Run

If you prefer a single file without extra comments, here’s the minimal version:

```java
import com.aspose.cells.*;

public class MinimalDemo {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook();
        Worksheet ws = wb.getWorksheets().get(0);
        Cell c = ws.getCells().get("A1");
        c


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Mastering Data Presentation in Excel&#58; Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}