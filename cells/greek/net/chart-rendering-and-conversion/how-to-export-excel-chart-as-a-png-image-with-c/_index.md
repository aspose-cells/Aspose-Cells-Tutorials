---
category: general
date: 2026-11-19
description: Πώς να εξάγετε ένα γράφημα Excel ως εικόνα PNG χρησιμοποιώντας το Aspose.Cells.
  Μάθετε πώς να αποθηκεύσετε την εικόνα του γραφήματος Excel και να ορίσετε τη μορφή
  PNG σε λίγα μόνο βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: el
lastmod: 2026-11-19
og_description: Πώς να εξάγετε ένα γράφημα Excel ως εικόνα PNG με το Aspose.Cells.
  Ακολουθήστε αυτόν τον οδηγό βήμα‑βήμα για να αποθηκεύσετε την εικόνα του γραφήματος
  Excel και να ορίσετε τη μορφή PNG αποδοτικά.
og_image_alt: How to export Excel chart as a PNG image
og_title: Πώς να εξάγετε ένα γράφημα Excel ως εικόνα PNG – γρήγορος οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Πώς να εξάγετε ένα γράφημα Excel ως εικόνα PNG με C#
url: /el/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε διάγραμμα Excel ως εικόνα PNG με C#

Αν χρειάζεστε **how to export Excel chart** σε μια φορητή εικόνα, αυτός ο οδηγός δείχνει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Χρησιμοποιώντας το Aspose.Cells μπορείτε να **save Excel chart image** σε μορφή PNG με μόνο τρεις γραμμές κώδικα, και το tutorial εξηγεί επίσης πώς να **set image format png** και **save Excel picture file** με ασφάλεια.

Θα ολοκληρώσετε αυτό το άρθρο με ένα εκτελέσιμο πρόγραμμα που φορτώνει ένα βιβλίο εργασίας, αποδίδει το πρώτο διάγραμμα και γράφει ένα αρχείο `pivot.png` στο δίσκο. Χωρίς πρόσθετα εργαλεία, χωρίς χειροκίνητη αντιγραφή‑επικόλληση—απλός κώδικας C# που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

## Προαπαιτούμενα

* .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
* Visual Studio 2022 ή οποιονδήποτε επεξεργαστή C#
* Άδεια Aspose.Cells for .NET (ή προσωρινό κλειδί αξιολόγησης)
* Αρχείο Excel (`pivot.xlsx`) που περιέχει τουλάχιστον ένα διάγραμμα στο πρώτο φύλλο εργασίας

Αυτά τα στοιχεία είναι οι μόνες εξωτερικές εξαρτήσεις· το tutorial δεν απαιτεί εγκατεστημένο Office στο μηχάνημα.

## Βήμα 1: Εγκατάσταση Aspose.Cells

Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.Cells
```

Το πακέτο προσθέτει το namespace `Aspose.Cells`, το οποίο παρέχει τις κλάσεις `Workbook`, `ImageOrPrintOptions` και άλλες που απαιτούνται για **save Excel chart image**.

## Βήμα 2: Δημιουργία ελάχιστου προγράμματος κονσόλας

Δημιουργήστε μια νέα εφαρμογή κονσόλας (`dotnet new console -n ExportChartDemo`) και αντικαταστήστε το αυτόματα δημιουργημένο `Program.cs` με τον παρακάτω κώδικα. Το πρόγραμμα δείχνει **how to export Excel chart** και περιλαμβάνει σχόλια που εξηγούν κάθε απόφαση.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Γιατί κάθε μέρος είναι σημαντικό

* **Loading the workbook** – `Workbook` αναλύει το αρχείο `.xlsx` χωρίς να χρειάζεται εγκατεστημένο Microsoft Excel.
* **ImageOrPrintOptions** – Αυτό το αντικείμενο ελέγχει τη μορφή εξόδου. Η ρύθμιση `ImageFormat = ImageFormat.Png` **sets image format png**, η οποία είναι χωρίς απώλειες και ευρέως υποστηριζόμενη.
* **RenderToImage** – Η μέθοδος `RenderToImage` μετατρέπει το διάγραμμα (ένα αντικείμενο `Picture`) σε αρχείο εικόνας. Η μέθοδος διαχειρίζεται επίσης την κλιμάκωση, DPI και διαφάνεια αυτόματα.
* **Error handling** – Ο έλεγχος για `sheet.Pictures.Count == 0` αποτρέπει μια εξαίρεση χρόνου εκτέλεσης εάν το φύλλο εργασίας δεν έχει διαγράμματα, μια κοινή περίπτωση όταν οι χρήστες δείχνουν στο λάθος φύλλο.

## Βήμα 3: Εκτέλεση του προγράμματος και επαλήθευση του αποτελέσματος

1. Δομήστε το έργο: `dotnet build`.
2. Εκτελέστε το: `dotnet run --project ExportChartDemo`.

Αν όλα είναι ρυθμισμένα σωστά, θα δείτε:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Ανοίξτε το `pivot.png` με οποιονδήποτε προβολέα εικόνων. Θα πρέπει να δείτε την ακριβή οπτική αναπαράσταση του διαγράμματος Excel, επιβεβαιώνοντας ότι έχετε αποθηκεύσει με επιτυχία **saved Excel picture file**.

### Αναμενόμενο αποτέλεσμα

Παρακάτω είναι ένα παράδειγμα του πώς μπορεί να φαίνεται το εξαγόμενο PNG

![Διάγραμμα Excel που εξήχθη αποθηκευμένο ως εικόνα PNG](images/exported-chart.png){: .center alt="Πώς να εξάγετε διάγραμμα Excel ως εικόνα PNG"}

## Βήμα 4: Προχωρημένες επιλογές – εξαγωγή πολλαπλών διαγραμμάτων

Εάν το βιβλίο εργασίας σας περιέχει περισσότερα από ένα διάγραμμα, μπορείτε να κάνετε βρόχο στη συλλογή `Pictures`:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Αυτό το μοτίβο σας επιτρέπει να **save Excel chart image** για κάθε διάγραμμα στο φύλλο, κάτι που είναι χρήσιμο για pipelines αναφοράς.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|---------|--------------|-----|
| `ArgumentOutOfRangeException` on `Pictures[0]` | Το φύλλο εργασίας δεν έχει διάγραμμα ή το διάγραμμα βρίσκεται σε διαφορετικό φύλλο. | Επαληθεύστε το δείκτη φύλλου (`Worksheets[0]`) και βεβαιωθείτε ότι το διάγραμμα υπάρχει. Χρησιμοποιήστε `Worksheets["SheetName"]` αν χρειάζεται. |
| Η εξαγόμενη εικόνα είναι θολή | Το DPI είναι ορισμένο πολύ χαμηλό (προεπιλογή 96). | Αυξήστε το `HorizontalResolution` και το `VerticalResolution` στο `ImageOrPrintOptions`. |
| Το αρχείο PNG είναι κενό ή κατεστραμμένο | Λείπει άδεια, προκαλώντας περιορισμούς αξιολόγησης. | Εφαρμόστε μια έγκυρη άδεια Aspose.Cells πριν φορτώσετε το βιβλίο εργασίας (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| Σφάλματα διαδρομής αρχείου (`FileNotFoundException`) | Λανθασμένος placeholder `YOUR_DIRECTORY`. | Χρησιμοποιήστε απόλυτες διαδρομές ή `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

Η αντιμετώπιση αυτών των προβλημάτων εξασφαλίζει μια ομαλή εμπειρία **save excel picture file**.

## Συμβουλή επαγγελματία: Εξαγωγή απευθείας σε ροή μνήμης

Μερικές φορές χρειάζεστε την εικόνα στη μνήμη (π.χ., για ανέβασμα σε web API) αντί για εγγραφή στο δίσκο:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

Η ίδια λογική **set image format png** εφαρμόζεται· απλώς αντικαθιστάτε τη διαδρομή αρχείου με μια ροή.

## Συμπέρασμα

Τώρα ξέρετε **how to export Excel chart** ως αρχείο PNG χρησιμοποιώντας το Aspose.Cells για .NET. Το tutorial κάλυψε:

* Εγκατάσταση της βιβλιοθήκης
* Φόρτωση βιβλίου εργασίας
* **Setting image format png**
* **Saving Excel chart image** στο δίσκο
* Διαχείριση πολλαπλών διαγραμμάτων και κοινών σφαλμάτων

Με αυτή τη βάση μπορείτε να ενσωματώσετε την εξαγωγή διαγραμμάτων σε αυτοματοποιημένες αναφορές, web services ή εφαρμογές επιφάνειας εργασίας. Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **save excel picture file** ως JPEG (`ImageFormat.Jpeg`) ή μετατροπή διαγραμμάτων σε PDF για εκτυπώσιμες αναφορές.

Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή διαγράμματος πίτας Excel σε εικόνα χρησιμοποιώντας Aspose.Cells .NET&#58; Οδηγός βήμα‑βήμα](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Εξαγωγή διαγράμματος ως PNG – Πλήρης οδηγός για μετατροπή Excel σε HTML με Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Εξαγωγή κελιών Excel σε εικόνα χρησιμοποιώντας Aspose.Cells .NET&#58; Οδηγός βήμα‑βήμα](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}