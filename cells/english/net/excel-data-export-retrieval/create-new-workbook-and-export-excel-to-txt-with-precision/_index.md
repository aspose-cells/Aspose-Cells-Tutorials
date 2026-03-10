---
category: general
date: 2026-02-15
description: Create new workbook and export Excel to TXT while setting numeric precision.
  Learn to set significant digits and limit significant digits in C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: en
og_description: Create new workbook and export Excel to TXT, setting significant digits
  for numeric precision. A step‑by‑step C# guide.
og_title: Create New Workbook – Export Excel to TXT with Precision
tags:
- C#
- Aspose.Cells
- Excel automation
title: Create New Workbook and Export Excel to TXT with Precision
url: /net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create New Workbook – Export Excel to TXT with Precise Numeric Formatting

Ever wondered how to **create new workbook** objects in C# and instantly dump them to a plain‑text file? You're not the only one. In many data‑pipeline scenarios we need to **export Excel to TXT** while keeping numbers readable, which means limiting the number of digits that appear after the decimal point.  

In this tutorial we’ll walk through the whole process: from spinning up a fresh workbook, to configuring the export so it **sets significant digits** (aka limiting significant digits), and finally writing the file to disk. By the end you’ll have a ready‑to‑run snippet that respects your **numeric precision** requirements—no extra libraries, no magic.

> **Pro tip:** If you’re already using Aspose.Cells, the classes shown below are part of that library. If you’re on a different platform, the concepts still apply; just swap the API calls.

---

## What You’ll Need

- .NET 6+ (the code compiles on .NET Core and .NET Framework alike)  
- Aspose.Cells for .NET (free trial or licensed version) – install via NuGet: `dotnet add package Aspose.Cells`  
- Any IDE you like (Visual Studio, Rider, VS Code)  

That’s it. No extra configuration files, no hidden steps.

---

## Step 1: Create a New Workbook

The very first thing is to **create new workbook**. Think of the `Workbook` class as an empty Excel file waiting for sheets, cells, and data.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Why this matters:** By starting with a clean workbook you avoid any hidden formatting that could interfere with the precision settings later on.

---

## Step 2: Configure Text Save Options – Set Significant Digits

Now we tell Aspose.Cells how many **significant digits** we want when we write to a `.txt` file. The `TxtSaveOptions` class exposes a `SignificantDigits` property that does exactly that.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Explanation:** `SignificantDigits = 5` means the exporter will keep the most important five digits of any number, regardless of where the decimal point sits. It’s a handy way to **set numeric precision** without manually formatting each cell.

---

## Step 3: Save the Workbook as a Plain‑Text File

With the workbook and options ready, we finally **export Excel to txt**. The `Save` method takes the file path and the options object we just configured.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Running the program produces a file that looks like this:

```
12346
0.00012346
3.1416
```

Notice how each number respects the **limit significant digits** rule we set earlier.

---

## Step 4: Verify the Result (Optional but Recommended)

It’s easy to open the generated `numbers.txt` in any editor, but you might want to automate the verification step, especially in CI pipelines.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

If the console shows the three lines above, you’ve successfully **set significant digits** and the export works as intended.

---

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Numbers appear with too many decimal places | `SignificantDigits` was left at the default (0) | Explicitly set `SignificantDigits` to the desired count |
| Empty file is created | Workbook never received any data before saving | Populate cells **before** calling `Save` |
| File path throws `UnauthorizedAccessException` | Trying to write to a protected folder | Use a folder you have write permissions for (e.g., `C:\Temp` or `%USERPROFILE%\Documents`) |
| Precision seems off for very small numbers | Significant digits count includes leading zeros after the decimal | Remember that “significant” ignores leading zeros; 0.000123456 with 5 digits becomes `0.00012346` |

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete, self‑contained program. Paste it into a new console project and hit **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Expected console output**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

And the `numbers.txt` file will contain the three lines shown above.

---

## Next Steps: Going Beyond the Basics

- **Export other formats** – Aspose.Cells also supports CSV, HTML, and PDF. Swap `TxtSaveOptions` for `CsvSaveOptions` or `PdfSaveOptions` as needed.  
- **Dynamic precision** – you can compute `SignificantDigits` at runtime based on user input or configuration files.  
- **Multiple worksheets** – iterate over `workbook.Worksheets` and export each one to its own `.txt` file.  
- **Localization** – control the decimal separator (`.` vs `,`) via `CultureInfo` if you need to match regional settings.  

All of these extensions still rely on the core idea we covered: **create new workbook**, configure the export, and **set numeric precision** to match your reporting requirements.

---

## Summary

We’ve taken a fresh **create new workbook** instance, filled it with data, and demonstrated how to **export Excel to TXT** while **setting significant digits** to limit the output precision. The full example runs out‑of‑the‑box, and the explanation covered the *why* behind each line so you can adapt it to your own projects.

Feel free to experiment—change the `SignificantDigits` value, add more sheets, or switch the output format. If you hit a snag, check the Aspose.Cells documentation or drop a comment below. Happy coding!

---

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}