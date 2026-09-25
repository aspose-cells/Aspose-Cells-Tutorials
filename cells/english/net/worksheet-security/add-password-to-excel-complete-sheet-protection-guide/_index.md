---
category: general
date: 2026-03-27
description: Add password to Excel and secure your data with excel sheet protection
  options, allowing select unlocked cells while you save protected workbook easily.
draft: false
keywords:
- add password to excel
- excel sheet protection options
- allow select unlocked cells
- save protected workbook
- enable sheet protection
language: en
og_description: Add password to Excel and protect your sheets with built‑in options,
  allowing select unlocked cells and saving a protected workbook in minutes.
og_title: Add password to Excel – Complete Sheet Protection Guide
tags:
- Aspose.Cells
- C#
- Excel security
title: Add password to Excel – Complete Sheet Protection Guide
url: /net/worksheet-security/add-password-to-excel-complete-sheet-protection-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add password to Excel – Complete Sheet Protection Guide

Ever wondered how to **add password to Excel** files without pulling your hair out? You’re not the only one—many developers hit a wall when they need to lock down sensitive data in spreadsheets. The good news? With a few lines of C# and Aspose.Cells you can enable sheet protection, pick the exact excel sheet protection options you need, and even allow select unlocked cells for a smoother user experience.

In this tutorial we’ll walk through the whole process: from creating a workbook, writing confidential values, to applying a SHA‑256 password, tweaking protection settings, and finally **save protected workbook** to disk. By the end you’ll know exactly how to add a password to Excel, why each option matters, and how to adapt the code for your own projects.

## Prerequisites

- .NET 6 or later (the code works with .NET Core and .NET Framework alike)
- Aspose.Cells for .NET installed via NuGet (`dotnet add package Aspose.Cells`)
- A basic understanding of C# syntax (no advanced tricks required)

If any of those sound unfamiliar, pause here and install the package—once you’re set, we can dive right in.

## Step 1 – Create a New Workbook (Enable Sheet Protection)

Before we can **add password to Excel**, we need a workbook object to work with. This step also sets the stage for later protection tweaks.

```csharp
using Aspose.Cells;

class ProtectSheetDemo
{
    static void Main()
    {
        // Create a fresh workbook – think of it as a blank Excel file
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

*Why this matters:* Instantiating a `Workbook` gives you a clean slate. If you were opening an existing file, you’d call `new Workbook("path.xlsx")` instead. The `Worksheet` reference is where we’ll write data and later apply protection.

## Step 2 – Write Sensitive Data (What We’ll Protect)

Now we’ll insert something the user definitely shouldn’t edit—maybe a password, a financial figure, or personal ID.

```csharp
        // Write confidential text into cell A1
        worksheet.Cells["A1"].PutValue("Sensitive Information");
```

*Pro tip:* If you need to lock only part of the sheet, you can mark specific cells as unlocked later. By default, all cells become locked when protection is turned on, so we’ll handle that in the next step.

## Step 3 – Enable Sheet Protection & Add a SHA‑256 Password

Here’s the heart of the tutorial: we finally **add password to Excel** by turning on protection and assigning a strong hash.

```csharp
        // Access the protection object for the worksheet
        WorksheetProtection protection = worksheet.Protection;

        // Turn on protection – this is the “enable sheet protection” flag
        protection.IsProtected = true;

        // Set a SHA‑256 hashed password (much stronger than plain text)
        protection.SetPassword("MyStrongPwd!", PasswordType.SHA256);
```

*Why use SHA‑256?* Plain‑text passwords can be cracked with brute‑force tools, whereas a SHA‑256 hash adds a cryptographic layer that Aspose.Cells handles for you. If you prefer the older Excel‑compatible hash, replace `PasswordType.SHA256` with `PasswordType.Standard`.

## Step 4 – Fine‑Tune Excel Sheet Protection Options

Now that the sheet is locked, we decide **excel sheet protection options** such as whether users can select locked cells, edit objects, or, crucial for many workflows, **allow select unlocked cells**.

```csharp
        // Allow users to click on unlocked cells (useful for data entry)
        protection.AllowSelectUnlockedCells = true;

        // Disallow editing of embedded objects like charts or shapes
        protection.AllowEditObject = false;

        // You can also restrict formatting, inserting rows, etc.
        // protection.AllowFormatCells = false;
        // protection.AllowInsertRows = false;
```

*Explanation:*  
- `AllowSelectUnlockedCells` lets end‑users navigate the sheet without triggering a “sheet protected” warning. This is handy when you expose a form‑like area.  
- `AllowEditObject = false` blocks changes to charts, pictures, or other embedded objects, tightening security.  
- Additional flags exist for granular control—feel free to enable what your scenario demands.

## Step 5 – Save the Protected Workbook (Save Protected Workbook)

The final act is to persist the file. This is where we **save protected workbook** to disk, and you’ll see the password protection in action when you open it in Excel.

```csharp
        // Persist the workbook with all protection settings applied
        workbook.Save("ProtectedSheet.xlsx");

        // Optional: let the console know we’re done
        System.Console.WriteLine("Workbook saved as ProtectedSheet.xlsx with password protection.");
    }
}
```

When you double‑click `ProtectedSheet.xlsx`, Excel will prompt for the password you set (`MyStrongPwd!`). If you try to edit a locked cell, you’ll be blocked; however, you can still select unlocked cells thanks to the earlier option.

### Expected Result

- **File:** `ProtectedSheet.xlsx` appears in your project’s output folder.  
- **Behavior:** Opening the file asks for the password. After entering it, cell A1 remains read‑only, while any unlocked cells (if you marked any) can be edited.  
- **Verification:** Try editing A1—Excel should refuse. Try clicking an unlocked cell (if you created one); it should be selectable without error.

## Common Variations & Edge Cases

| Scenario | What to Change | Why |
|----------|----------------|-----|
| **Different password algorithm** | Use `PasswordType.Standard` | For compatibility with older Excel versions that don’t support SHA‑256. |
| **Protecting an existing workbook** | Load via `new Workbook("Existing.xlsx")` | Allows you to add protection to a file you already have. |
| **Locking only a range** | Set `worksheet.Cells["B2:C5"].Style.Locked = false;` before protection | Unlocks a specific range while the rest stays locked. |
| **Allowing users to format cells** | `protection.AllowFormatCells = true;` | Useful for dashboards where users can change colors but not data. |
| **Saving to a stream (e.g., web response)** | `workbook.Save(stream, SaveFormat.Xlsx);` | Ideal for ASP.NET APIs that return the file directly to the browser. |

*Watch out for:* forgetting to set `IsProtected = true`—the password alone won’t lock the sheet. Also, always test with a real Excel client because some protection flags behave slightly differently across Office versions.

## Full Working Example (Copy‑Paste Ready)

Below is the complete program you can drop into a console app. No missing pieces.

```csharp
using Aspose.Cells;

class ProtectSheetDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write some sensitive information into a cell
        worksheet.Cells["A1"].PutValue("Sensitive Information");

        // Optional: Unlock a range for user input (e.g., B1:C5)
        worksheet.Cells["B1:C5"].Style.Locked = false;

        // Step 3: Enable sheet protection and set a SHA‑256 hashed password
        WorksheetProtection protection = worksheet.Protection;
        protection.IsProtected = true;                     // enable sheet protection
        protection.SetPassword("MyStrongPwd!", PasswordType.SHA256);

        // Step 4: Restrict actions – allow selecting unlocked cells only
        protection.AllowSelectUnlockedCells = true;
        protection.AllowEditObject = false;               // disallow editing objects
        // Additional options you might need:
        // protection.AllowFormatCells = false;
        // protection.AllowInsertRows = false;

        // Step 5: Save the protected workbook to a file
        workbook.Save("ProtectedSheet.xlsx");

        System.Console.WriteLine("Workbook saved as ProtectedSheet.xlsx with password protection.");
    }
}
```

Run the program, open the generated file, and you’ll see the protection in action.

## Visual Reference

![Add password to Excel sheet protection screenshot](https://example.com/images/add-password-to-excel.png "add password to excel")

*Alt text includes the primary keyword for SEO.*

## Recap & Next Steps

We’ve just shown you **how to add password to Excel** using Aspose.Cells, covered essential **excel sheet protection options**, demonstrated the **allow select unlocked cells** flag, and saved a **protected workbook** that respects those settings. In a nutshell, the flow is:

1. Create or load a workbook.  
2. Write the data you want to protect.  
3. Turn on protection, set a strong password, and tweak options.  
4. Save the workbook.

Now that you have the basics, consider these follow‑up ideas:

- **Programmatic password prompts:** expose the password via a secure UI instead of hard‑coding.  
- **Batch protection:** loop through multiple worksheets and apply the same settings.  
- **Integrate with ASP.NET Core:** return the protected file as a download response.  

Feel free to experiment—maybe you’ll lock down an entire reporting suite or just a single confidential sheet. Either way, you now have the toolkit to protect Excel data the right way.

---

*Happy coding! If this guide helped you add password to Excel, let us know in the comments or share your own tweaks. The more we learn together, the more secure our spreadsheets become.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}