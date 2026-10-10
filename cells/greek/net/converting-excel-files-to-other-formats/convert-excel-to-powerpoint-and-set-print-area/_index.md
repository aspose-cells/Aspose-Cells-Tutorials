---
category: general
date: 2026-10-10
description: Μετατροπή Excel σε PowerPoint και ορισμός περιοχής εκτύπωσης σε C# με
  το Aspose.Cells – μάθετε πώς να εξάγετε Excel, να ορίσετε περιοχή εκτύπωσης και
  να δημιουργήσετε αρχείο PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: el
lastmod: 2026-10-10
og_description: Μετατρέψτε το Excel σε PowerPoint με το Aspose.Cells. Αυτό το σεμινάριο
  δείχνει πώς να ορίσετε την περιοχή εκτύπωσης, να εξάγετε το Excel και να δημιουργήσετε
  ένα αρχείο PPTX σε C#.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Μετατροπή Excel σε PowerPoint – πλήρης οδηγός για προγραμματιστές C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Μετατροπή Excel σε PowerPoint και ορισμός περιοχής εκτύπωσης
url: /el/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Excel σε PowerPoint και ορισμός περιοχής εκτύπωσης

Αν χρειάζεστε **convert Excel to PowerPoint**, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε σε C#. Ορίζοντας πρώτα μια περιοχή εκτύπωσης, ελέγχετε ποια κελιά εμφανίζονται σε κάθε διαφάνεια, και το τελικό αρχείο PPTX ταιριάζει με τις προσδοκίες σας για τη διάταξη. Η λύση απαντά επίσης στο “how to export Excel” και στο “how to set print area” χρησιμοποιώντας τον ίδιο κώδικα.

Σε αυτόν τον οδηγό θα:

* Φορτώστε ένα υπάρχον βιβλίο εργασίας.
* Ορίστε την περιοχή εκτύπωσης για ένα φύλλο εργασίας (το βήμα **set print area excel**).
* Διαμορφώστε τις επιλογές μετατροπής για την έξοδο PowerPoint.
* Δημιουργήστε ένα αρχείο **convert excel to pptx** με μία μόνο κλήση μεθόδου.

Όλος ο απαιτούμενος κώδικας περιλαμβάνεται, ώστε να μπορείτε να τον αντιγράψετε, να τον επικολλήσετε και να τον εκτελέσετε αμέσως.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|-------------|----------------|
| **.NET 6.0 or later** | Το παράδειγμα στοχεύει στο .NET 6+, αλλά οποιαδήποτε έκδοση .NET που υποστηρίζει C# 10 λειτουργεί. |
| **Aspose.Cells for .NET** | Αυτή η βιβλιοθήκη παρέχει `Workbook`, `ImageOrPrintOptions` και τη μέθοδο `ConvertToPdf` (χρησιμοποιείται για PPTX). Εγκαταστήστε την μέσω NuGet: `dotnet add package Aspose.Cells` |
| **An input Excel file** | Ο οδηγός χρησιμοποιεί το `input.xlsx`. Τοποθετήστε το σε έναν φάκελο που μπορείτε να αναφέρετε από τον κώδικα. |
| **Write permission to the output folder** | Το πρόγραμμα γράφει το `output.pptx`. Βεβαιωθείτε ότι ο φάκελος υπάρχει και είναι εγγράψιμος. |

> **Pro tip:** Αν εργάζεστε με πολλαπλά φύλλα εργασίας, επαναλάβετε το βήμα περιοχής εκτύπωσης για κάθε φύλλο πριν από τη μετατροπή.

## Βήμα 1: Δημιουργία νέου έργου C# console

Ανοίξτε ένα τερματικό ή παράθυρο PowerShell και εκτελέστε:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

Αυτό δημιουργεί ένα νέο έργο με όνομα **ExcelToPowerPointDemo** και προσθέτει το πακέτο Aspose.Cells, το οποίο είναι η κύρια εξάρτηση για **how to export Excel** σε άλλες μορφές.

## Βήμα 2: Γράψτε τον κώδικα μετατροπής

Αντικαταστήστε το περιεχόμενο του `Program.cs` με το πλήρες παράδειγμα παρακάτω. Ο κώδικας δείχνει **convert excel to powerpoint**, εμφανίζει **how to set print area**, και παράγει ένα αρχείο **convert excel to pptx**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Γιατί κάθε μέρος είναι σημαντικό

* **Loading the workbook** – Αυτό είναι το πρώτο βήμα σε οποιοδήποτε σενάριο **how to export Excel**. Το `Workbook` διαβάζει το αρχείο στη μνήμη, δίνοντάς σας πλήρη πρόσβαση σε φύλλα, κελιά και μορφοποίηση.
* **Setting the print area** – Αναθέτοντας το `PageSetup.PrintArea`, λέτε στο Aspose.Cells ποια κελιά να αποδώσει. Αυτό είναι ο πυρήνας του **set print area excel**· χωρίς αυτό, ολόκληρο το φύλλο θα εξαχθεί, δημιουργώντας πιθανώς τεράστιες, μη αναγνώσιμες διαφάνειες.
* **Choosing `SaveFormat.Pptx`** – Το αντικείμενο `ImageOrPrintOptions` σας επιτρέπει να αλλάξετε τις μορφές εξόδου. Ορίζοντας το `SaveFormat` σε `Pptx` ενεργοποιεί τη διαδικασία **convert excel to pptx**.
* **Calling `ConvertToPdf`** – Παρά το όνομα της μεθόδου, όταν το `SaveFormat` είναι `Pptx` η βιβλιοθήκη παράγει αρχείο PowerPoint. Αυτή είναι η προτεινόμενη μέθοδος για **convert excel to powerpoint** με μία κλήση.

## Βήμα 3: Εκτέλεση του προγράμματος

Από το φάκελο του έργου, εκτελέστε:

```bash
dotnet run
```

Αν όλα έχουν ρυθμιστεί σωστά, θα πρέπει να δείτε έξοδο κονσόλας παρόμοια με:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Ανοίξτε το `output.pptx` στο Microsoft PowerPoint ή σε οποιονδήποτε συμβατό προβολέα. Κάθε διαφάνεια αντιστοιχεί στη σελίδα εκτύπωσης του φύλλου εργασίας, περιορισμένη στην περιοχή που ορίσατε.

## Διαχείριση πολλαπλών φύλλων εργασίας

Αν το βιβλίο εργασίας σας περιέχει περισσότερα από ένα φύλλο και θέλετε κάθε φύλλο σε ξεχωριστό σετ διαφανειών, κάντε επανάληψη στη συλλογή:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

Αυτό το πρότυπο δείχνει **how to export Excel** δεδομένα φύλλο‑με‑φύλλο ενώ εξακολουθεί να **setting print area** ξεχωριστά.

## Περιπτώσεις άκρων και συμβουλές βέλτιστων πρακτικών

| Κατάσταση | Συνιστώμενη προσέγγιση |
|-----------|----------------------|
| **Very large worksheets** | Μειώστε την περιοχή εκτύπωσης ή αυξήστε το `HorizontalResolution`/`VerticalResolution` για να διατηρήσετε το μέγεθος του PPTX διαχειρίσιμο. |
| **Different page orientations** | Ορίστε `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` πριν από τη μετατροπή. |
| **Custom slide size** | Χρησιμοποιήστε `conversionOptions.OnePagePerSheet = false;` και προσαρμόστε το `conversionOptions.Width` / `conversionOptions.Height`. |
| **Missing input file** | Τυλίξτε τον κώδικα φόρτωσης σε ένα μπλοκ `try { … } catch (FileNotFoundException)` για να παρέχετε σαφές μήνυμα σφάλματος. |
| **Non‑ASCII characters** | Βεβαιωθείτε ότι το βιβλίο εργασίας αποθηκεύεται με κωδικοποίηση UTF‑8· το Aspose.Cells διαχειρίζεται αυτόματα Unicode. |

## Πλήρης κώδικας πηγής για αναφορά

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, συμπεριλαμβανομένων των δηλώσεων `using` και των σχολίων. Αποθηκεύστε το ως `Program.cs` μέσα στο έργο που δημιουργήθηκε στο **Step 1**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Αναμενόμενη έξοδος

Η εκτέλεση του προγράμματος παράγει ένα αρχείο PowerPoint (`output.pptx`) που περιέχει:

* Μία διαφάνεια ανά σελίδα εκτύπωσης του φύλλου εργασίας.
* Μόνο τα κελιά εντός **A1:G30** είναι ορατά σε κάθε διαφάνεια.
* Διατηρημένη μορφοποίηση (γραμματοσειρές, χρώματα, περιγράμματα) όπως εμφανίζονται στο Excel.

Ανοίξτε το αρχείο στο PowerPoint για να επαληθεύσετε ότι η διάταξη ταιριάζει με την ορισμένη περιοχή εκτύπωσης.

## Συμπέρασμα

Τώρα ξέρετε πώς να **convert Excel to PowerPoint** ενώ ορίζετε με ακρίβεια **set print area excel** χρησιμοποιώντας το Aspose.Cells σε C#. Ο οδηγός κάλυψε **how to export Excel**, έδειξε **how to set print area**, και παρουσίασε το πλήρες **convert excel to pptx**.

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να ορίσετε περιοχή εκτύπωσης στο Excel χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Ορισμός περιοχής εκτύπωσης στο Excel και εξαγωγή σε PowerPoint – Οδηγός βήμα‑βήμα](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Ορισμός περιοχής εκτύπωσης Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}