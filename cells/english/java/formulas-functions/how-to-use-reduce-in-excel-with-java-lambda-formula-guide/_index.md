---
category: general
date: 2026-06-08
description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
  formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
  a clear step‑by‑step tutorial.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: en
og_description: How to use reduce in Excel with Java. Master lambda formula Excel,
  dynamic arrays java, and sum with reduce using a complete, runnable example.
og_title: How to Use Reduce in Excel with Java – Lambda Formula Guide
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: How to Use Reduce in Excel with Java – Lambda Formula Guide
url: /java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use Reduce in Excel with Java – Lambda Formula Guide

Ever wondered **how to use reduce** in Excel when you’re writing Java code? You’re not alone. Many developers hit a wall trying to combine Excel’s new dynamic array functions with Java‑based automation, and the answer isn’t as cryptic as it first appears.

In this tutorial we’ll walk through a concrete example that shows **how to use reduce** together with a **lambda formula Excel** expression, all powered by the Aspose.Cells for Java library. By the end you’ll be able to generate dynamic arrays in Java, write lambda functions, and compute a **sum with reduce**—no manual spreadsheet fiddling required.

---

## What You’ll Build

- A fresh workbook created entirely from Java.  
- An **EXPAND** dynamic array that fills cells A1:A5 with the numbers 1‑5.  
- A **REDUCE** formula that sums those numbers using a **lambda formula Excel**.  
- A saved `.xlsx` file you can open in any spreadsheet program to verify the result.

No external macros, no VBA—just pure Java code and Excel’s modern functions.

---

## Prerequisites

- Java 17 (or any recent JDK) – older versions work but you’ll miss out on `var` sugar.  
- Aspose.Cells for Java (the free trial works fine for this demo).  
- Basic familiarity with Java syntax and Excel formulas.  

If you’re new to **dynamic arrays java**, don’t worry—this guide explains every piece.

---

## Step 1: Set Up Your Project and Import Aspose.Cells

First things first, add the Aspose.Cells Maven dependency to your `pom.xml` (or grab the JAR manually).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Pro tip:** Keep your dependencies up‑to‑date; newer versions improve formula evaluation speed, which matters when you’re **how to use reduce** in large sheets.

---

## Step 2: Create a Workbook and Access the First Worksheet

Now we’ll create a brand‑new workbook. This is the foundation for learning **how to use reduce** because the workbook object gives us a sandbox to drop formulas into.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Why this matters:* The `Workbook` class abstracts the entire Excel file, while `Worksheet` represents a single tab. You’ll later see how **dynamic arrays java** can fill many cells from a single formula placed in A1.

---

## Step 3: Generate a Vertical Array with EXPAND

Excel’s `EXPAND` function can spill values into a range. We’ll use it to create the numbers 1 through 5 in column A.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

If you open the resulting workbook, cells A1:A5 will read 1, 2, 3, 4, 5. This is the **dynamic arrays java** part—one formula populates a whole range.

---

## Step 4: Write a REDUCE Lambda to Sum the Array

Here’s where we answer the core question: **how to use reduce** in Excel from Java. The `REDUCE` function iterates over an array, applying a lambda you provide. In our case we’ll sum the numbers.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

Let’s break that down:

- `0` – the initial accumulator value (`acc`).  
- `A1:A5` – the array we generated with **EXPAND**.  
- `LAMBDA(acc, x, acc + x)` – the **lambda formula Excel** that adds each element (`x`) to the accumulator (`acc`).  

When the formula runs, `B1` ends up containing **15**, the **sum with reduce** of the numbers 1‑5.

> **How to write lambda** in Excel? Think of it as an anonymous function where the first arguments are the parameters, and the final expression is the return value. In Java we just embed the text; the Excel engine does the heavy lifting.

---

## Step 5: Save the Workbook

Finally, we persist the workbook to disk so you can open it in Excel, Google Sheets, or any viewer that supports `.xlsx`.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Open the file and you’ll see:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

The **sum with reduce** appears in B1, confirming that we’ve successfully demonstrated **how to use reduce** together with a **lambda formula Excel** from Java.

---

## Full Working Example

Below is the complete, ready‑to‑run Java program. Copy‑paste it into your IDE, adjust the output directory, and hit **Run**.

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**Expected output** when you open `new-functions.xlsx`:

- Cells **A1:A5** contain `1, 2, 3, 4, 5`.  
- Cell **B1** displays `15`, confirming the **sum with reduce**.

---

## Common Questions & Edge Cases

### What if I need a horizontal array instead of vertical?

Swap the column/row arguments in `EXPAND`. For a horizontal spill across B1:F1:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### Can I use REDUCE to multiply instead of sum?

Absolutely. Just change the lambda body:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

Now B1 will show `120` (5 ! = 120).

### Does Aspose.Cells support custom LAMBDA functions?

Yes, you can define named LAMBDA functions via the workbook’s `Names` collection, then call them like any built‑in formula. That’s a deeper dive for a later tutorial on **how to write lambda** functions that live beyond a single cell.

### What about older Excel versions that don’t recognize REDUCE?

If you target Excel 2019 or earlier, the engine will return `#NAME?`. In such cases


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Mastering Aspose.Cells Java: How to Interrupt Formula Calculation in Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}