---
category: general
date: 2026-09-11
description: Αντιγράψτε τον πίνακα Pivot και εξάγετε το Excel σε PPTX χρησιμοποιώντας
  το Aspose.Cells. Μάθετε πώς να δημιουργείτε επεξεργάσιμο PPTX και να αποθηκεύετε
  το βιβλίο εργασίας ως PPTX σε C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: el
lastmod: 2026-09-11
og_description: Αντιγράψτε τον πίνακα Pivot και εξάγετε το Excel σε PPTX σε C# χρησιμοποιώντας
  το Aspose.Cells. Δημιουργήστε επεξεργάσιμο PPTX και αποθηκεύστε το βιβλίο εργασίας
  ως PPTX με λίγες γραμμές κώδικα.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Αντιγραφή πίνακα Pivot και εξαγωγή Excel σε PPTX – πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Αντιγραφή συγκεντρωτικού πίνακα και εξαγωγή Excel σε PPTX με το Aspose.Cells
url: /el/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αντιγραφή πίνακα Pivot και εξαγωγή Excel σε PPTX με το Aspose.Cells

Αν χρειάζεστε να αντιγράψετε έναν πίνακα pivot από ένα φύλλο εργασίας σε ένα άλλο και στη συνέχεια να εξάγετε το αρχείο Excel σε μια παρουσίαση PowerPoint, αυτός ο οδηγός σας δείχνει πώς. Χρησιμοποιώντας το Aspose.Cells μπορείτε να δημιουργήσετε ένα επεξεργάσιμο PPTX και να αποθηκεύσετε το βιβλίο εργασίας ως PPTX με λίγες μόνο γραμμές κώδικα C#.

Το tutorial καλύπτει κάθε βήμα που απαιτείται για τη μετακίνηση ενός πίνακα pivot, τη διατήρηση της λειτουργικότητάς του, και την παραγωγή ενός αρχείου PPTX όπου το γράφημα και τα σχήματα παραμένουν επεξεργάσιμα. Δεν απαιτούνται εξωτερικά εργαλεία — μόνο η βιβλιοθήκη Aspose.Cells και ένα περιβάλλον ανάπτυξης .NET.

## Τι θα επιτύχετε

* **Copy pivot table** από ένα φύλλο προέλευσης σε ένα φύλλο προορισμού ενώ διατηρούνται όλες οι συνδέσεις δεδομένων.  
* **Export Excel to PPTX** ώστε η προκύπτουσα διαφάνεια να μπορεί να επεξεργαστεί στο PowerPoint.  
* **Generate editable PPTX** όπου τα γραφήματα, οι πίνακες και τα σχήματα δεν μετατρέπονται σε εικόνες.  
* **Save workbook as PPTX** χρησιμοποιώντας την ίδια κλήση API του Aspose.Cells.  

### Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+).  
* Aspose.Cells for .NET (πακέτο NuGet `Aspose.Cells`).  
* Βασική κατανόηση των εφαρμογών κονσόλας C#.  

> **Συμβουλή επαγγελματία:** Εγκαταστήστε το πακέτο NuGet μέσω του CLI για να εξασφαλίσετε ότι έχετε την πιο πρόσφατη έκδοση:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Πώς να αντιγράψετε πίνακα pivot μεταξύ φύλλων εργασίας

Η πρώτη ενέργεια είναι η μετακίνηση του πίνακα pivot διατηρώντας τον ορισμό του. Το Aspose.Cells παρέχει τη μέθοδο `CopyRange` με ένα αντικείμενο `CopyOptions` που περιλαμβάνει τη σημαία `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Γιατί λειτουργεί:**  
`CopyRange` αντιγράφει τα δεδομένα των κελιών, τη μορφοποίηση και, όταν το `CopyPivotTable` είναι true, την κρυφή μνήμη και τα μεταδεδομένα του πίνακα pivot. Η περιοχή προορισμού ξεκινά από το κελί `A1` (γραμμή 0, στήλη 0) αλλά μπορείτε να αλλάξετε τις μετατοπίσεις για να τοποθετήσετε τον πίνακα pivot αλλού.

**Κοινή περίπτωση άκρης:** Εάν το φύλλο προορισμού περιέχει ήδη έναν πίνακα pivot με το ίδιο όνομα, το Aspose.Cells θα μετονομάσει αυτόματα τον εισερχόμενο, αποτρέποντας σύγκρουση ονομάτων.

## Εξαγωγή Excel σε PPTX και δημιουργία επεξεργάσιμου PPTX

Αφού ο πίνακας pivot είναι στη θέση του, μπορείτε να εξάγετε ολόκληρο το βιβλίο εργασίας σε αρχείο PPTX. Η κλάση `ImageOrPrintOptions` σας επιτρέπει να ορίσετε `ExportImageFormat = ImageFormat.Pptx`, που λέει στο Aspose.Cells να αντιμετωπίσει το αποτέλεσμα ως παρουσίαση PowerPoint αντί για ραστερ εικόνας.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Γιατί λειτουργεί:**  
Όταν το `ExportImageFormat` ορίζεται σε `Pptx`, το Aspose.Cells μετατρέπει κάθε φύλλο εργασίας σε διαφάνεια. Τα σχήματα, τα γραφήματα και οι πίνακες pivot γράφονται ως εγγενή αντικείμενα PowerPoint, ώστε να μπορείτε να κάνετε διπλό κλικ σε αυτά στο PowerPoint και να επεξεργαστείτε τα υποκείμενα δεδομένα.

**Συμβουλή για μεγάλα βιβλία εργασίας:** Εάν χρειάζεστε μόνο ένα υποσύνολο φύλλων, ορίστε `workbook.Worksheets.RemoveAt(index)` για τα φύλλα που δεν θέλετε να εξάγετε πριν καλέσετε το `Save`. Αυτό μειώνει το μέγεθος του αρχείου PPTX.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που ενώνει τα προηγούμενα βήματα. Αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή στον υπολογιστή σας.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος εκτυπώνει:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Όταν ανοίξετε το `output.pptx` στο Microsoft PowerPoint, θα δείτε μια διαφάνεια που περιέχει τον αντιγραμμένο πίνακα pivot ως επεξεργάσιμο γράφημα. Κάνοντας διπλό κλικ στο γράφημα ανοίγει ο επεξεργαστής γραφημάτων του PowerPoint, επιτρέποντάς σας να τροποποιήσετε τις σειρές, τους άξονες και τις ετικέτες δεδομένων χωρίς να επιστρέψετε στο Excel.

## Διαχείριση τυπικών προβλημάτων

| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| Ο πίνακας pivot εμφανίζεται ως στατική εικόνα | Η σημαία `CopyPivotTable` παραλείπεται ή το `ExportImageFormat` ορίζεται σε `Png` | Βεβαιωθείτε ότι `CopyPivotTable = true` και `ExportImageFormat = ImageFormat.Pptx`. |
| Το φύλλο προορισμού εμφανίζει κενά κελιά | Η περιοχή προέλευσης δεν καλύπτει ολόκληρη την περιοχή του πίνακα pivot | Επεκτείνετε την περιοχή (π.χ., `"A1:H30"`) ώστε να περιλαμβάνει όλα τα πεδία pivot. |
| Το εξαγόμενο PPTX είναι τεράστιο | Περιλαμβάνονται περιττά φύλλα εργασίας | Αφαιρέστε τα ανεπιθύμητα φύλλα πριν καλέσετε το `Save`. |
| Το PowerPoint δεν μπορεί να επεξεργαστεί το γράφημα | Χρήση παλαιότερης έκδοσης του Aspose.Cells που δεν υποστηρίζει PPTX | Αναβαθμίστε στην πιο πρόσφατη έκδοση του Aspose.Cells (ελέγξτε τις σημειώσεις έκδοσης). |

## Επόμενα βήματα και συναφή θέματα

* **Export Excel sheet to PPTX with custom slide layouts** – εξερευνήστε το `WorksheetToPdfConverter` για πιο ακριβή έλεγχο της εμφάνισης των διαφανειών.  
* **Export Excel to PDF** – αντικαταστήστε το `ImageFormat.Pptx` με `ImageFormat.Pdf` για να δημιουργήσετε ένα PDF.  
* **Programmatically modify PPTX after export** – χρησιμοποιήστε τη βιβλιοθήκη `Aspose.Slides` για να προσθέσετε animations ή σημειώσεις ομιλητή.  

Με την κατάκτηση των **copy pivot table**, **export excel to pptx**, και **generate editable pptx**, μπορείτε να δημιουργήσετε ολοκληρωμένες pipelines αναφοράς που μεταφέρουν δεδομένα από τα υπολογιστικά φύλλα απευθείας σε παρουσιάσεις χωρίς να χάνεται η δυνατότητα επεξεργασίας.

---

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αντιγράψετε πίνακα Pivot σε C# – Μετατροπή Excel σε PPTX, Αντιγραφή περιοχής & Δημιουργία Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Δημιουργία νέου βιβλίου εργασίας Excel – Αντιγραφή & Διπλασιασμός πίνακα Pivot](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Δημιουργία πίνακα Pivot στο Excel χρησιμοποιώντας το Aspose.Cells για .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}