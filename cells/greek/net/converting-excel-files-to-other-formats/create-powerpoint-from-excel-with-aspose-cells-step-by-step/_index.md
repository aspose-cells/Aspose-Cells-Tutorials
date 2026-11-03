---
category: general
date: 2026-10-01
description: Δημιουργήστε PowerPoint από Excel χρησιμοποιώντας το Aspose.Cells σε
  C#. Εξάγετε το Excel σε PowerPoint και μετατρέψτε γρήγορα το XLSX σε PPTX με ένα
  πλήρες παράδειγμα κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: el
lastmod: 2026-10-01
og_description: Δημιουργήστε PowerPoint από Excel χρησιμοποιώντας το Aspose.Cells
  σε C#. Μάθετε να εξάγετε το Excel σε PowerPoint και να μετατρέπετε XLSX σε PPTX
  με λίγες γραμμές κώδικα.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Δημιουργία PowerPoint από Excel με το Aspose.Cells – γρήγορος οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Δημιουργία PowerPoint από Excel με το Aspose.Cells – οδηγός βήμα‑προς‑βήμα
url: /el/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία PowerPoint από Excel με Aspose.Cells – οδηγός βήμα‑βήμα

Αν χρειάζεστε **create PowerPoint from Excel**, αυτό το tutorial σας δείχνει πώς να το κάνετε με το Aspose.Cells για .NET. Θα μάθετε να **export Excel to PowerPoint**, να μετατρέψετε ένα βιβλίο εργασίας XLSX σε παρουσίαση PPTX και να προσαρμόσετε τις προκύπτουσες διαφάνειες χωρίς να αφήσετε το C# project σας.

Ο οδηγός καλύπτει όλα όσα χρειάζεστε για να εκτελέσετε τον κώδικα σε .NET 6 ή νεότερο, συμπεριλαμβανομένης της ρύθμισης του έργου, των απαιτούμενων πακέτων NuGet και ενός πλήρους, εκτελέσιμου παραδείγματος. Στο τέλος, θα έχετε ένα αρχείο PowerPoint που περιέχει το αρχικό γράφημα Excel ακριβώς όπως εμφανίζεται στο βιβλίο εργασίας.

## Τι θα χρειαστείτε

| Προαπαιτούμενο | Αιτία |
|---|---|
| .NET 6 SDK ή νεότερο | Παρέχει το runtime για την εφαρμογή κονσόλας C# |
| Visual Studio 2022 (ή οποιοδήποτε IDE) | Διευκολύνει τη δημιουργία έργου και τον εντοπισμό σφαλμάτων |
| Aspose.Cells for .NET NuGet package | Παρέχει την κλάση `Workbook` και τα API εξαγωγής |
| Ένα αρχείο Excel (`.xlsx`) που περιέχει τουλάχιστον ένα γράφημα | Τα δεδομένα πηγής για τη διαφάνεια PowerPoint |

> **Συμβουλή:** Το Aspose.Cells λειτουργεί σε Windows, Linux και macOS, ώστε να μπορείτε να εκτελείτε τον ίδιο κώδικα σε Docker containers ή CI pipelines.

## Βήμα 1: Δημιουργήστε ένα νέο έργο κονσόλας και προσθέστε το Aspose.Cells

Ανοίξτε ένα τερματικό (ή το Visual Studio Package Manager Console) και εκτελέστε:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

Η εντολή `dotnet add package` κατεβάζει την πιο πρόσφατη σταθερή έκδοση του **Aspose.Cells**, η οποία περιλαμβάνει τη μέθοδο `ExportPptx` που χρησιμοποιείται αργότερα.

## Βήμα 2: Προσθέστε το πηγαίο βιβλίο εργασίας Excel

Τοποθετήστε το αρχείο Excel που θέλετε να μετατρέψετε στον φάκελο του έργου. Για αυτό το tutorial χρησιμοποιούμε το `ChartOle.xlsx`, το οποίο περιέχει ένα μόνο γράφημα στο πρώτο φύλλο εργασίας.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## Βήμα 3: Γράψτε τον κώδικα που **creates PowerPoint from Excel**

Ανοίξτε το `Program.cs` και αντικαταστήστε το περιεχόμενό του με τον παρακάτω κώδικα. Το παράδειγμα δείχνει τη **core export** λειτουργία και επίσης παρουσιάζει πώς να διαχειριστείτε κοινές περιπτώσεις όπως ελλιπή αρχεία και μη υποστηριζόμενους τύπους γραφημάτων.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### Γιατί λειτουργεί αυτό

* `Workbook` διαβάζει ολόκληρο το αρχείο Excel, συμπεριλαμβανομένων των ενσωματωμένων γραφημάτων, πινάκων και μορφοποίησης.  
* `ExportPptx` μετατρέπει το ενεργό φύλλο εργασίας σε μια σειρά διαφανειών PPTX. Η μέθοδος μετατρέπει αυτόματα τα γραφήματα Excel σε σχήματα PowerPoint, διατηρώντας την οπτική πιστότητα.  
* Ο κώδικας τυλίγει τη λειτουργία σε ένα μπλοκ `try/catch` για να εμφανίσει σφάλματα όπως αποτυχίες **convert XLSX to PPTX** που προκύπτουν από κατεστραμμένα αρχεία.

## Βήμα 4: Εκτελέστε το πρόγραμμα και επαληθεύστε το αποτέλεσμα

Εκτελέστε την εφαρμογή:

```bash
dotnet run
```

Θα πρέπει να δείτε το μήνυμα στην κονσόλα:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

Ανοίξτε το `Exported.pptx` στο Microsoft PowerPoint ή σε οποιονδήποτε συμβατό προβολέα. Η πρώτη διαφάνεια εμφανίζει το γράφημα ακριβώς όπως εμφανιζόταν στο `ChartOle.xlsx`. Αυτό επιβεβαιώνει ότι έχετε δημιουργήσει επιτυχώς **generated PowerPoint from Excel**.

## Βήμα 5: Προχωρημένα – εξαγωγή πολλαπλών φύλλων εργασίας ή προσαρμοσμένων διατάξεων διαφανειών

Το βασικό παράδειγμα εξάγει μόνο το πρώτο φύλλο εργασίας. Σε πραγματικές συνθήκες μπορεί να χρειαστείτε:

* **Export several worksheets** σε ξεχωριστές διαφάνειες.  
* **Control slide size** ή προσθέστε έναν placeholder τίτλου.  
* **Include hidden worksheets** στη μετατροπή.

Παρακάτω υπάρχει ένα σύντομο απόσπασμα που διατρέχει όλα τα φύλλα εργασίας και προσθέτει το καθένα ως ξεχωριστή διαφάνεια:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **Σημείωση:** Το προχωρημένο απόσπασμα απαιτεί τη βιβλιοθήκη **Aspose.Slides for .NET**. Αν χρειάζεστε μόνο τη μετατροπή ενός φύλλου, η προηγούμενη κλήση `ExportPptx` είναι επαρκής.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Αιτία | Διόρθωση |
|---|---|---|
| Κενή διαφάνεια μετά την εξαγωγή | Το φύλλο εργασίας δεν περιέχει ορατά αντικείμενα | Βεβαιωθείτε ότι υπάρχει τουλάχιστον ένα γράφημα, πίνακας ή σχήμα πριν καλέσετε το `ExportPptx`. |
| Λείπουν γραμματοσειρές στο PowerPoint | Η γραμματοσειρά δεν είναι εγκατεστημένη στον υπολογιστή όπου ανοίγεται το PPTX | Ενσωματώστε τις απαιτούμενες γραμματοσειρές στο βιβλίο εργασίας Excel ή εγκαταστήστε τις στο σύστημα-στόχο. |
| Απρόσμενη κλιμάκωση | Το μεγάλο γράφημα υπερβαίνει τις διαστάσεις της διαφάνειας | Ρυθμίστε την ιδιότητα `PageSetup.Zoom` του φύλλου εργασίας πριν την εξαγωγή. |
| `convert XLSX to PPTX` προκαλεί `NotSupportedException` | Τύπος γραφήματος που δεν υποστηρίζεται από το Aspose.Cells (π.χ., 3‑D χάρτες) | Αντικαταστήστε το γράφημα με έναν υποστηριζόμενο τύπο ή εξάγετε το φύλλο ως εικόνα πρώτα. |

Η αντιμετώπιση αυτών των περιπτώσεων εξασφαλίζει μια αξιόπιστη **export Excel to PowerPoint** ροή εργασίας σε παραγωγικά περιβάλλοντα.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create PowerPoint from Excel** χρησιμοποιώντας το Aspose.Cells για .NET. Το tutorial κάλυψε:

* Ρύθμιση έργου και εγκατάσταση NuGet  
* Φόρτωση βιβλίου εργασίας Excel και κλήση του `ExportPptx`  
* Εκτέλεση του κώδικα και επιβεβαίωση του παραγόμενου PPTX  
* Επέκταση της λύσης για διαχείριση πολλαπλών φύλλων εργασίας και προσαρμοσμένων διατάξεων  
* Πρακτικές συμβουλές για την αποφυγή κοινών προβλημάτων μετατροπής  

Με αυτή τη γνώση μπορείτε να αυτοματοποιήσετε τη δημιουργία αναφορών, να χτίσετε pipelines παρουσίασης ή να ενσωματώσετε τη μετατροπή Excel‑σε‑PowerPoint σε οποιαδήποτε εφαρμογή C#. Πειραματιστείτε με διαφορετικούς τύπους γραφημάτων, προσθέστε τίτλους διαφανειών ή συνδυάστε την εξαγωγή με το Aspose.Slides για πλήρη δημιουργία παρουσιάσεων.

--- 

*Έτοιμοι να εξερευνήσετε περισσότερα; Ρίξτε μια ματιά σε σχετικά θέματα όπως **convert Excel to PDF**, **embed Excel data in Word**, ή **use Aspose.Slides to programmatically edit PPTX files**.*

## Τι πρέπει να μάθετε στη συνέχεια;

- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}