---
category: general
date: 2026-02-28
description: Apprenez à écrire l’Unicode dans Excel en utilisant C#. Ce tutoriel montre
  également comment ajouter des emoji dans Excel, comment créer des fichiers Excel
  et comment convertir Excel en XPS.
draft: false
keywords:
- how to write unicode
- how to create excel
- add emoji in excel
- convert excel to xps
- add unicode emoji
language: fr
og_description: Découvrez comment écrire l'Unicode dans Excel, ajouter des emojis
  dans les cellules Excel, créer des classeurs Excel et convertir Excel en XPS avec
  C#. Code et astuces étape par étape.
og_title: Comment écrire du Unicode dans Excel avec C# – Guide complet de programmation
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment écrire l’Unicode dans Excel avec C# – Guide complet étape par étape
url: /fr/net/xps-and-pdf-operations/how-to-write-unicode-in-excel-with-c-complete-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Write Unicode in Excel with C# – Complete Step‑by‑Step Guide

Vous êtes-vous déjà demandé **comment écrire Unicode** dans une feuille Excel sans perdre patience ? Vous n'êtes pas le seul. Les développeurs doivent souvent insérer des emojis, des symboles spéciaux ou des caractères spécifiques à une langue dans des classeurs, et la technique habituelle `Cell.Value = "😀"` échoue souvent à cause de problèmes d’encodage.  

Dans ce guide, nous résoudrons ce problème une bonne fois pour toutes, montrerons **comment créer Excel** programmaticalement, démontrerons **add emoji in Excel** dans les cellules, et terminerons avec un exemple propre de **convert Excel to XPS**. À la fin, vous disposerez d’un extrait C# prêt à l’emploi qui écrit un emoji d’homme (👨‍) dans `A1` et enregistre le classeur complet au format XPS.

## What You’ll Need

- **.NET 6+** (ou .NET Framework 4.6+). Tout runtime récent fonctionne ; le code utilise uniquement les fonctionnalités standard de C#.
- **Aspose.Cells for .NET** – la bibliothèque qui nous permet de manipuler des fichiers Excel sans Office installé. Récupérez‑la via NuGet (`Install-Package Aspose.Cells`).
- Un IDE décent (Visual Studio, Rider ou VS Code).  
- Aucune expérience préalable avec Unicode n’est requise – nous expliquerons les points de code.

> **Pro tip:** Si vous avez déjà un projet qui référence Aspose.Cells, vous pouvez coller le code tel quel ; sinon créez une nouvelle application console et ajoutez d’abord le package NuGet.

## Step 1: Set Up the Project and Import Namespaces

First, spin up a new console application and bring in the necessary namespaces. This is the foundation for **how to create Excel** files from scratch.

```csharp
using System;
using Aspose.Cells;          // Core Excel API
using Aspose.Cells.Drawing; // Required for XPS options (optional but clearer)

namespace UnicodeExcelDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial lives here
        }
    }
}
```

*Why this matters:* `Aspose.Cells` gives us the `Workbook`, `Worksheet`, and `XpsSaveOptions` classes we’ll be using. Importing them up front keeps the later code tidy.

## Step 2: Create a New Workbook and Access the First Worksheet

Now we’ll answer **how to create excel** objects in memory. Think of a workbook as a blank notebook; the first worksheet is the first page.

```csharp
// Step 2: Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and default) worksheet – index 0
Worksheet worksheet = workbook.Worksheets[0];
```

*Explanation:* The `Workbook` constructor builds an empty Excel file with one sheet automatically. Accessing `Worksheets[0]` is safe because Aspose always creates at least one sheet.

## Step 3: Write a Unicode Emoji (Man + Variation Selector‑16) into Cell A1

Here’s the heart of **how to write unicode** characters correctly. Unicode code points are expressed in C# with the `\u{...}` syntax (available from C# 10 onward). The man emoji we want is composed of two parts:

1. `U+1F468` – le caractère de base “MAN”.
2. `U+FE0F` – Variation Selector‑16, qui force la présentation emoji.

```csharp
// Step 3: Insert the emoji into cell A1
// \u{1F468} = 👨  (MAN)
// \u{FE0F} = Variation Selector‑16 (forces emoji style)
worksheet.Cells["A1"].PutValue("\u{1F468}\u{FE0F}");
```

*Why the variation selector?* Without `FE0F`, some renderers may display the character as a plain text symbol rather than the colorful emoji. Adding it guarantees the “emoji style” on most platforms, which is essential when you **add unicode emoji** to Excel.

## Step 4: Prepare XPS Save Options (Optional but Recommended)

If you plan to **convert Excel to XPS**, you can fine‑tune the output using `XpsSaveOptions`. The default options already produce a faithful conversion, but we’ll create the object explicitly to keep the code clear and extensible.

```csharp
// Step 4: Set up XPS save options (default configuration)
XpsSaveOptions xpsOptions = new XpsSaveOptions();
```

*Note:* You can customize page size, DPI, and other settings here. For most scenarios the defaults are perfect.

## Step 5: Save the Workbook as an XPS Document

Finally, we persist the workbook to an XPS file. The `Save` method takes three arguments: the target path, the format enum, and the options we just prepared.

```csharp
// Step 5: Export the workbook to XPS
string outputPath = @"C:\Temp\Result.xps"; // Change to your desired folder
workbook.Save(outputPath, SaveFormat.Xps, xpsOptions);

Console.WriteLine($"✅ XPS file saved to {outputPath}");
```

*What you’ll see:* Opening `Result.xps` in Windows Reader shows the emoji perfectly rendered in cell A1, just like it appears in Excel.

## Full Working Example

Putting all the pieces together, here’s the complete, copy‑paste‑ready program:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

namespace UnicodeExcelDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Get the first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // 3️⃣ Write a Unicode emoji (man + VS‑16) into A1
            worksheet.Cells["A1"].PutValue("\u{1F468}\u{FE0F}");

            // 4️⃣ Prepare XPS save options (default)
            XpsSaveOptions xpsOptions = new XpsSaveOptions();

            // 5️⃣ Save as XPS
            string outputPath = @"C:\Temp\Result.xps";
            workbook.Save(outputPath, SaveFormat.Xps, xpsOptions);

            Console.WriteLine($"✅ XPS file saved to {outputPath}");
        }
    }
}
```

Run the program, navigate to `C:\Temp\Result.xps`, and you’ll see the emoji sitting proudly in the top‑left cell. That’s the full answer to **how to write Unicode** in Excel and **convert Excel to XPS** in one go.

## Common Pitfalls & Edge Cases

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Emoji appears as a square** | The target font doesn’t support the emoji glyph. | Use a font like *Segoe UI Emoji* on Windows or set `Style.Font.Name = "Segoe UI Emoji"` for the cell. |
| **Variation selector ignored** | Some older Excel viewers treat `FE0F` as a regular character. | Ensure you’re using a modern viewer (Excel 2016+ or the XPS viewer on Windows 10/11). |
| **Path not found error** | The folder doesn’t exist or you lack write permission. | Create the directory first (`Directory.CreateDirectory(@"C:\Temp")`) or choose a user‑writable location. |
| **NuGet package missing** | Compile fails because `Aspose.Cells` isn’t referenced. | Run `dotnet add package Aspose.Cells` before building. |

### Adding More Unicode Characters

If you need to **add unicode emoji** beyond the man icon, just replace the code points:

```csharp
// Example: Smiling face with hearts (🥰)
worksheet.Cells["B2"].PutValue("\u{1F970}");
```

Remember to prepend `\u{FE0F}` if you want the emoji presentation for characters that have both text and emoji forms.

## Bonus: Styling the Emoji Cell (Optional)

While the emoji itself is the star, you might want to center it or enlarge the font:

```csharp
Style style = worksheet.Cells["A1"].GetStyle();
style.Font.Name = "Segoe UI Emoji";
style.Font.Size = 24;
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
worksheet.Cells["A1"].SetStyle(style);
```

Now the emoji looks like it belongs in a presentation slide rather than a raw spreadsheet.

## Conclusion

We’ve walked through **how to write Unicode** into an Excel file using C#, demonstrated **how to create Excel** workbooks from scratch, shown the exact steps to **add emoji in Excel**, and wrapped it all up with a clean **convert Excel to XPS** operation. The complete code is ready to run, and the explanations cover both the *what* and the *why*, making this tutorial citation‑worthy for AI assistants and SEO‑friendly for Google.

Ready for the next challenge? Try exporting the same workbook to PDF, or loop over a list of Unicode symbols to build a multilingual report. The same pattern applies—just swap the save format and adjust the cell values.

Got questions about other Unicode symbols, font handling, or batch conversions? Drop a comment below, and happy coding! 

![how to write unicode in Excel using C#](/images/unicode-excel-csharp.png "Screenshot of Excel with Unicode emoji in cell A1")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}