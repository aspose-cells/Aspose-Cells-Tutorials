---
category: general
date: 2026-10-26
description: Μάθετε πώς να εξάγετε διαγράμματα Excel στο PowerPoint με C#. Διατηρήστε
  την επεξεργασιμότητα των σχημάτων και αποθηκεύστε ως PPTX με λίγες γραμμές κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: el
lastmod: 2026-10-26
og_description: Εξαγωγή διαγραμμάτων Excel σε PowerPoint με C#. Αυτός ο οδηγός δείχνει
  πώς να διατηρήσετε τα σχήματα επεξεργάσιμα και να αποθηκεύσετε ως PPTX χρησιμοποιώντας
  το Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Εξαγωγή διαγραμμάτων Excel σε PowerPoint με C# – βήμα‑προς‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Πώς να εξάγετε διαγράμματα Excel στο PowerPoint χρησιμοποιώντας C#
url: /el/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε διαγράμματα Excel σε PowerPoint χρησιμοποιώντας C#

Αν χρειάζεστε **εξαγωγή διαγραμμάτων Excel σε PowerPoint**, αυτός ο οδηγός σας καθοδηγεί βήμα‑βήμα μέσα από μια πλήρη, έτοιμη προς εκτέλεση λύση. Είτε δημιουργείτε έναν πίνακα αναφορών είτε αυτοματοποιείτε παρουσιάσεις, θα δείτε πώς με λίγες γραμμές κώδικα C# τα σχήματα των διαγραμμάτων παραμένουν πλήρως επεξεργάσιμα μετά τη μετατροπή.

Σε αυτό το tutorial θα μάθετε πώς να:

* Φορτώσετε ένα υπάρχον βιβλίο εργασίας Excel που περιέχει διαγράμματα.  
* (Προαιρετικά) προσαρμόσετε τις ρυθμίσεις του βιβλίου εργασίας πριν από τη μετατροπή.  
* Αποθηκεύσετε το βιβλίο εργασίας ως αρχείο PowerPoint διατηρώντας την επεξεργασιμότητα των σχημάτων.  

Όλα αυτά γίνονται με **Aspose.Cells for .NET**, μια βιβλιοθήκη που διαχειρίζεται τη μετατροπή Excel‑σε‑PowerPoint χωρίς να απαιτείται Microsoft Office στον διακομιστή.

## Τι θα χρειαστείτε

| Απαίτηση | Λόγος |
|----------|-------|
| .NET 6.0 ή νεότερο | Σύγχρονο runtime με πλήρη χαρακτηριστικά γλώσσας |
| Visual Studio 2022 (ή οποιοδήποτε IDE) | Βολικός επεξεργαστής και αποσφαλματωτής |
| **Aspose.Cells for .NET** πακέτο NuGet | Παρέχει την κλάση `Workbook` και υποστήριξη `SaveFormat.Pptx` |
| Ένα αρχείο Excel (`ChartAndShapes.xlsx`) που περιέχει τουλάχιστον ένα διάγραμμα | Πηγή των διαγραμμάτων που θέλετε να εξάγετε |

> **Συμβουλή επαγγελματία:** Χρησιμοποιήστε τη δωρεάν έκδοση **Aspose.Cells Evaluation** για να δοκιμάσετε τον κώδικα· ένα κλειδί άδειας αφαιρεί το υδατογράφημα αξιολόγησης.

```bash
dotnet add package Aspose.Cells
```

## Εξαγωγή διαγραμμάτων Excel σε PowerPoint – πλήρης ροή εργασίας

Παρακάτω βρίσκεται ο κώδικας από‑αρχή‑μέχρι‑τέλος που πραγματοποιεί την εξαγωγή ενώ **διατηρεί την επεξεργασιμότητα των σχημάτων**. Κάθε βήμα εξηγείται λεπτομερώς.

### Βήμα 1: Φόρτωση του βιβλίου εργασίας Excel

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Η φόρτωση του αρχείου διαβάζει όλα τα φύλλα, τα διαγράμματα και τα σχήματα στη μνήμη, κάτι που απαιτείται για οποιαδήποτε περαιτέρω επεξεργασία.*

### Βήμα 2: (Προαιρετικό) Προσαρμογή ρυθμίσεων βιβλίου εργασίας

Στις περισσότερες περιπτώσεις οι προεπιλεγμένες ρυθμίσεις είναι επαρκείς για καθαρή εξαγωγή. Ωστόσο, εάν χρειάζεται να αλλάξετε τη λειτουργία υπολογισμού, τη διάταξη σελίδας ή να κρύψετε ορισμένα φύλλα, μπορείτε να το κάνετε εδώ.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Γιατί είναι σημαντικό:** Η προσαρμογή των ρυθμίσεων πριν από τη μετατροπή εγγυάται ότι οι δημιουργημένες διαφάνειες αντικατοπτρίζουν ακριβώς την κατάσταση που θέλετε, ειδικά όταν τύποι ή κρυμμένα φύλλα θα μπορούσαν να επηρεάσουν τα δεδομένα του διαγράμματος.

### Βήμα 3: Αποθήκευση του βιβλίου εργασίας ως αρχείο PowerPoint

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*Η σταθερά `SaveFormat.Pptx` λέει στο Aspose.Cells να γράψει μια παρουσίαση PowerPoint. Εσωτερικά, η βιβλιοθήκη μετατρέπει κάθε διάγραμμα Excel σε σχήμα PowerPoint που παραμένει πλήρως επεξεργάσιμο στο Microsoft PowerPoint.*

### Βήμα 4: Επαλήθευση του αποτελέσματος

Ανοίξτε το `Shapes.pptx` στο PowerPoint και:

1. Επιλέξτε ένα διάγραμμα σε οποιαδήποτε διαφάνεια.  
2. Δεξί‑κλικ → **Edit Data**.  
3. Επιβεβαιώστε ότι εμφανίζεται ο πίνακας δεδομένων του διαγράμματος και μπορείτε να τροποποιήσετε τις τιμές.

Αν το διάγραμμα ανοίξει το πλαίσιο **Edit Data**, η μετατροπή πέτυχε και η **επεξεργασιμότητα των σχημάτων** διατηρήθηκε.

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="Παράδειγμα εξαγωγής διαγραμμάτων Excel σε PowerPoint"}

## Συχνά προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| Τα διαγράμματα εμφανίζονται ως στατικές εικόνες | Χρήση παλαιότερης έκδοσης Aspose.Cells που δεν υποστηρίζει εξαγωγή PPTX | Αναβαθμίστε στην πιο πρόσφατη Aspose.Cells 23.x ή νεότερη |
| Λείπουν δεδομένα στο διάγραμμα PowerPoint | Το βιβλίο εργασίας δεν έχει υπολογιστεί πλήρως πριν την εξαγωγή | Καλέστε `workbook.CalculateFormula()` πριν το `Save` |
| Τα σχήματα δεν είναι επεξεργάσιμα | Αποθήκευση με `SaveFormat.Xlsx` αντί για `SaveFormat.Pptx` | Βεβαιωθείτε ότι περνάτε `SaveFormat.Pptx` στο `Workbook.Save` |
| Εξαίρεση άδειας εκτέλεσης | Έκδοση αξιολόγησης χωρίς καταχωρημένη άδεια | Καταχωρήστε την άδειά σας με `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Ειδική περίπτωση: Εξαγωγή πολλαπλών φύλλων εργασίας με ξεχωριστά διαγράμματα

Αν το αρχείο Excel σας περιέχει πολλά φύλλα, το καθένα με το δικό του διάγραμμα, το Aspose.Cells δημιουργεί αυτόματα ξεχωριστή διαφάνεια για κάθε διάγραμμα. Μπορείτε να ελέγξετε τη σειρά των διαφανειών αναδιατάσσοντας τα φύλλα πριν από την αποθήκευση.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Συμβουλή απόδοσης: Ροή εξόδου αντί για εγγραφή σε δίσκο

Κατά τη δημιουργία αρχείων PowerPoint σε web API, αποφύγετε τα προσωρινά αρχεία γράφοντας σε ένα `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Πλήρες, εκτελέσιμο παράδειγμα

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Η κονσόλα εκτυπώνει το μήνυμα επιβεβαίωσης και το `Shapes.pptx` ανοίγει στο PowerPoint με κάθε διάγραμμα Excel να εμφανίζεται σε ξεχωριστή διαφάνεια. Επιλέγοντας ένα διάγραμμα μπορείτε να επεξεργαστείτε τα δεδομένα του, επιβεβαιώνοντας ότι η **επεξεργασιμότητα των σχημάτων** διατηρείται.

## Σύνοψη και επόμενα βήματα

Τώρα γνωρίζετε πώς να **εξάγετε διαγράμματα Excel σε PowerPoint** με C# διατηρώντας τα διαγράμματα πλήρως επεξεργάσιμα. Ο πυρήνας της λύσης είναι η μέθοδος `Workbook.Save` με `SaveFormat.Pptx`, μια δυνατότητα του **Aspose.Cells export** που αφαιρεί την πολυπλοκότητα του Open XML.

Από εδώ μπορείτε να εξερευνήσετε:

* Προσθήκη προσαρμοσμένων τίτλων ή σημειώσεων διαφάνειας χρησιμοποιώντας το API **Aspose.Slides**.  
* Μετατροπή άλλων αντικειμένων Excel (πίνακες, εικόνες) μαζί με τα διαγράμματα.  
* Αυτοματοποίηση επεξεργασίας δέσμης πολλαπλών βιβλίων εργασίας σε υπηρεσία παρασκηνίου.

Πειραματιστείτε με τις προαιρετικές ρυθμίσεις που παρουσιάστηκαν παραπάνω και ενσωματώστε αυτό το μοτίβο στις ροές αναφορών σας για γρήγορη, αξιόπιστη δημιουργία PowerPoint.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [How to Export Excel to PowerPoint with C# – Complete Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [How to Export Shapes from Excel to PowerPoint – Complete Guide](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}