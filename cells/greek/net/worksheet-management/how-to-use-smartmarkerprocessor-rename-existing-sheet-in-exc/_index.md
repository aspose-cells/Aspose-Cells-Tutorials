---
category: general
date: 2026-05-30
description: Πώς να χρησιμοποιήσετε το SmartMarkerProcessor για να μετονομάσετε υπάρχον
  φύλλο και να αυτοματοποιήσετε τις εργασίες μετονομασίας φύλλων Excel σε λίγα απλά
  βήματα.
draft: false
keywords:
- how to use smartmarkerprocessor
- rename existing sheet
- automate excel sheet rename
language: el
og_description: Πώς να χρησιμοποιήσετε το SmartMarkerProcessor για να μετονομάσετε
  υπάρχον φύλλο και να αυτοματοποιήσετε τις εργασίες μετονομασίας φύλλων Excel σε
  έναν συνοπτικό, βήμα‑βήμα οδηγό.
og_title: Πώς να χρησιμοποιήσετε το SmartMarkerProcessor – Μετονομασία υπάρχουσας
  φύλλου στο Excel
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use SmartMarkerProcessor to rename existing sheet and automate
    Excel sheet rename tasks in a few simple steps.
  headline: How to Use SmartMarkerProcessor – Rename Existing Sheet in Excel
  type: TechArticle
- description: How to use SmartMarkerProcessor to rename existing sheet and automate
    Excel sheet rename tasks in a few simple steps.
  name: How to Use SmartMarkerProcessor – Rename Existing Sheet in Excel
  steps:
  - name: 1. Multiple Existing Detail Sheets
    text: If your template already contains **Detail**, **Detail_1**, and **Detail_2**,
      the processor will generate **Detail_3**. This behavior is deterministic, so
      you can rely on it for batch processing.
  - name: 2. Custom Prefixes or Suffixes
    text: You might want the new sheet to start with a date stamp, e.g., `"Detail_2023-09-01"`.
      Set `DetailSheetNewName = $"Detail_{DateTime.Today:yyyy-MM-dd}"`. The processor
      will still add numeric suffixes if needed.
  - name: 3. Renaming Other Sheets
    text: '`SmartMarkerOptions` also provides `HeaderSheetNewName` and `SummarySheetNewName`.
      Use them the same way to **rename existing sheet** types beyond the detail sheet.'
  - name: 4. Performance Considerations
    text: When processing large workbooks (hundreds of sheets), instantiate **one**
      `SmartMarkerProcessor` and reuse it across files. This reduces memory churn
      and speeds up the **automate excel sheet rename** workflow.
  type: HowTo
tags:
- Excel automation
- GemBox
- SmartMarker
title: Πώς να χρησιμοποιήσετε το SmartMarkerProcessor – Μετονομασία υπάρχοντος φύλλου
  στο Excel
url: /el/net/worksheet-management/how-to-use-smartmarkerprocessor-rename-existing-sheet-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το SmartMarkerProcessor – Μετονομασία υπάρχοντος φύλλου στο Excel

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το SmartMarkerProcessor** για να μετονομάσετε ένα υπάρχον φύλλο ενώ γεμίζετε δεδομένα; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν το πρότυπό τους περιέχει ήδη ένα φύλλο εργασίας “Detail” και η μηχανή SmartMarker προσπαθεί να δημιουργήσει ένα άλλο με το ίδιο όνομα. Τα καλά νέα; Με μερικές γραμμές κώδικα μπορείτε να **αυτοματοποιήσετε τη μετονομασία φύλλων Excel** χωρίς να διακόψετε τη ροή εργασίας σας.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει ακριβώς πώς να ρυθμίσετε τον επεξεργαστή, να μετονομάσετε υπάρχοντα φύλλα και να διατηρήσετε τα αρχεία Excel σας τακτοποιημένα. Χωρίς εικασίες—απλός κώδικας, εξηγήσεις του *γιατί* κάθε γραμμή είναι σημαντική, και συμβουλές για τη διαχείριση των περιπτώσεων άκρων που θα συναντήσετε.

---

## Προαπαιτούμενα

- **GemBox.Spreadsheet** (ή οποιαδήποτε βιβλιοθήκη που παρέχει το `SmartMarkerProcessor`) έκδοση 2024‑latest εγκατεστημένη μέσω NuGet.
- Ένα περιβάλλον ανάπτυξης .NET (Visual Studio, VS Code, Rider—όπως προτιμάτε).
- Ένα βασικό πρότυπο Excel (`Template.xlsx`) που περιέχει ήδη ένα φύλλο εργασίας με όνομα **Detail**.
- Μια απλή πηγή δεδομένων (π.χ., ένα `DataTable`, `List<T>`, ή ένα ανώνυμο αντικείμενο) που θέλετε να συγχωνεύσετε στο πρότυπο.

Αυτό είναι όλο. Αν λείπει κάτι από αυτά, αποκτήστε το πακέτο NuGet τώρα:

```bash
dotnet add package GemBox.Spreadsheet
```

---

![παράδειγμα χρήσης smartmarkerprocessor](/images/smartmarkerprocessor-rename.png "παράδειγμα χρήσης smartmarkerprocessor")

*Η παραπάνω εικόνα απεικονίζει το φύλλο εργασίας πριν και μετά τη λειτουργία μετονομασίας.*

---

## Βήμα 1: Ρύθμιση της παρουσίας SmartMarkerProcessor  

Το πρώτο πράγμα που χρειάζεστε είναι ένα αντικείμενο **SmartMarkerProcessor**. Σκεφτείτε το ως τη μηχανή που διαβάζει το πρότυπό σας, ψάχνει για Smart Markers (όπως `{{Name}}`) και γράφει τα δεδομένα στα κατάλληλα κελιά.

```csharp
using GemBox.Spreadsheet;
using GemBox.Spreadsheet.SmartMarkers;

// Initialize the component (license key is optional for the free version)
SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

// Load the workbook that contains the template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Create the processor instance.
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

> **Γιατί είναι σημαντικό:** Η δημιουργία μιας στιγμής του επεξεργαστή **μία φορά** και η επαναχρησιμοποίησή του σε όλη την εφαρμογή μειώνει το κόστος. Επίσης, η φόρτωση του βιβλίου εργασίας πρώτα σας δίνει πρόσβαση στη συλλογή φύλλων εργασίας, την οποία θα χρειαστούμε όταν μετονομάσουμε τα φύλλα.

---

## Βήμα 2: Διαμόρφωση των επιλογών Μετονομασίας Υπάρχοντος Φύλλου  

Τώρα έρχεται η ουσία: να πείτε στο SmartMarker πώς να συμπεριφέρεται όταν συναντά σύγκρουση ονόματος φύλλου. Η κλάση `SmartMarkerOptions` εκθέτει μια ιδιότητα που ονομάζεται `DetailSheetNewName`. Αν υπάρχει ήδη ένα φύλλο με όνομα `"Detail"`, ο επεξεργαστής θα προσθέσει αυτόματα ένα επίθημα (`_1`, `_2`, …) για να αποφύγει τη σύγκρουση.

```csharp
// Define processing options.
// The DetailSheetNewName property controls the base name for the detail sheet.
SmartMarkerOptions options = new SmartMarkerOptions
{
    // If "Detail" exists, the new sheet will become "Detail_1"
    DetailSheetNewName = "Detail"
};
```

> **Συμβουλή:** Αν προτιμάτε ένα προσαρμοσμένο επίθημα (π.χ., `"Detail-Backup"`), απλώς ορίστε `DetailSheetNewName = "Detail-Backup"`. Ο επεξεργαστής θα προσθέτει ακόμα αριθμούς όπως χρειάζεται.

> **Γιατί είναι σημαντικό:** Χωρίς αυτή την επιλογή, το SmartMarker θα έριχνε εξαίρεση ή θα αντικαθιστούσε σιωπηρά το υπάρχον φύλλο, οδηγώντας σε απώλεια δεδομένων. Η ρητή διαμόρφωση της συμπεριφοράς μετονομασίας **αυτοματοποιεί τη μετονομασία φύλλων Excel** και διατηρεί τα πρότυπά σας άθικτα.

---

## Βήμα 3: Προετοιμασία της Πηγής Δεδομένων  

Το SmartMarker μπορεί να λειτουργήσει με σχεδόν οποιαδήποτε επαναλαμβανόμενη πηγή δεδομένων. Για παράδειγμα, ας χρησιμοποιήσουμε μια απλή λίστα ανώνυμων αντικειμένων που αντιπροσωπεύουν γραμμές τιμολογίου.

```csharp
var dataSource = new[]
{
    new { Item = "Widget A", Quantity = 5, Price = 9.99 },
    new { Item = "Widget B", Quantity = 2, Price = 19.95 },
    new { Item = "Widget C", Quantity = 1, Price = 49.50 }
};
```

Αν έχετε ήδη ένα `DataTable` ή ένα `IEnumerable<T>`, απλώς συνδέστε το—δεν χρειάζεται επιπλέον μετατροπή.

---

## Βήμα 4: Εφαρμογή της επεξεργασίας SmartMarker στο πρώτο φύλλο εργασίας  

Με τον επεξεργαστή, τις επιλογές και τα δεδομένα έτοιμα, ήρθε η ώρα να εκτελέσετε τη συγχώνευση. Θα στοχεύσουμε το **πρώτο φύλλο εργασίας** (`wb.Worksheets[0]`) επειδή εκεί βρίσκεται το πρότυπό μας. Η μέθοδος `Process` δέχεται τρία ορίσματα: το φύλλο εργασίας, την πηγή δεδομένων και τις επιλογές που ορίσαμε νωρίτερα.

```csharp
// Apply SmartMarker processing.
// This will insert the data into the template and rename the detail sheet if needed.
processor.Process(wb.Worksheets[0], dataSource, options);
```

> **Τι συμβαίνει στο παρασκήνιο;**  
> 1. Το SmartMarker σαρώνει το φύλλο εργασίας για markers όπως `{{Item}}`, `{{Quantity}}`, κ.λπ.  
> 2. Δημιουργεί ένα νέο φύλλο λεπτομερειών χρησιμοποιώντας το όνομα που ορίζεται στο `DetailSheetNewName`.  
> 3. Αν υπάρχει ήδη ένα φύλλο με όνομα “Detail”, γίνεται αυτόματα “Detail_1”.  
> 4. Οι γραμμές δεδομένων γράφονται στο νέο φύλλο, διατηρώντας τη μορφοποίηση.

---

## Βήμα 5: Αποθήκευση του αποτελέσματος και επαλήθευση της μετονομασίας  

Μετά την επεξεργασία, θα θέλετε να αποθηκεύσετε το βιβλίο εργασίας στο δίσκο και να ελέγξετε διπλά ότι το φύλλο μετονομήθηκε σωστά.

```csharp
// Save the processed workbook.
wb.Save("Result.xlsx");

// Quick verification (optional console output)
Console.WriteLine("Worksheets in the resulting file:");
foreach (var sheet in wb.Worksheets)
    Console.WriteLine($"- {sheet.Name}");
```

Όταν ανοίξετε το `Result.xlsx`, θα πρέπει να δείτε ένα φύλλο με όνομα **Detail_1** (ή **Detail_2** αν το “Detail_1” υπήρχε ήδη). Οι γραμμές δεδομένων θα εμφανιστούν κάτω από τη γραμμή κεφαλίδας που τοποθετήσατε στο πρότυπο.

---

## Διαχείριση Συνηθισμένων Περιπτώσεων Άκρων  

### 1. Πολλαπλά υπάρχοντα φύλλα Detail  

Αν το πρότυπό σας περιέχει ήδη **Detail**, **Detail_1**, και **Detail_2**, ο επεξεργαστής θα δημιουργήσει **Detail_3**. Αυτή η συμπεριφορά είναι ντετερμινιστική, ώστε να μπορείτε να βασιστείτε σε αυτή για επεξεργασία σε παρτίδες.

### 2. Προσαρμοσμένα πρόθεμα ή επίθημα  

Μπορεί να θέλετε το νέο φύλλο να ξεκινά με ημερομηνία, π.χ., `"Detail_2023-09-01"`. Ορίστε `DetailSheetNewName = $"Detail_{DateTime.Today:yyyy-MM-dd}"`. Ο επεξεργαστής θα προσθέσει ακόμη αριθμητικά επιθήματα αν χρειαστεί.

### 3. Μετονομασία άλλων φύλλων  

`SmartMarkerOptions` παρέχει επίσης `HeaderSheetNewName` και `SummarySheetNewName`. Χρησιμοποιήστε τα με τον ίδιο τρόπο για **μετονομασία υπάρχοντων φύλλων** πέρα από το φύλλο λεπτομερειών.

```csharp
options.HeaderSheetNewName = "Header";
options.SummarySheetNewName = "Summary";
```

### 4. Σκέψεις απόδοσης  

Κατά την επεξεργασία μεγάλων βιβλίων εργασίας (εκατοντάδες φύλλα), δημιουργήστε **μία** `SmartMarkerProcessor` και επαναχρησιμοποιήστε την σε πολλά αρχεία. Αυτό μειώνει την κατανάλωση μνήμης και επιταχύνει τη ροή εργασίας **automate excel sheet rename**.

---

## Πλήρες λειτουργικό παράδειγμα  

Συνδυάζοντας όλα, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια εφαρμογή κονσόλας και να τρέξετε αμέσως:

```csharp
using System;
using GemBox.Spreadsheet;
using GemBox.Spreadsheet.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1. License & load template.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");
        var wb = ExcelFile.Load("Template.xlsx");

        // 2. Create processor.
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 3. Define rename options.
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // 4. Prepare data source.
        var dataSource = new[]
        {
            new { Item = "Widget A", Quantity = 5, Price = 9.99 },
            new { Item = "Widget B", Quantity = 2, Price = 19.95 },
            new { Item = "Widget C", Quantity = 1, Price = 49.50 }
        };

        // 5. Process the first worksheet.
        processor.Process(wb.Worksheets[0], dataSource, options);

        // 6. Save the result.
        wb.Save("Result.xlsx");

        // 7. Verify sheet names.
        Console.WriteLine("Worksheets after processing:");
        foreach (var sheet in wb.Worksheets)
            Console.WriteLine($"- {sheet.Name}");
    }
}
```

**Αναμενόμενη έξοδος** (κονσόλα):

```
Worksheets after processing:
- Sheet1
- Detail_1
```

Ανοίξτε το `Result.xlsx` και θα δείτε τα δεδομένα να έχουν τοποθετηθεί καθαρά κάτω από τη νέα καρτέλα **Detail_1**.

---

## Ανακεφαλαίωση  

Συζητήσαμε **πώς να χρησιμοποιήσετε το SmartMarkerProcessor** για να μετονομάσετε με ασφάλεια ένα υπάρχον φύλλο και να **αυτοματοποιήσετε πλήρως τη μετονομασία φύλλων Excel**. Τα κύρια σημεία είναι:

1. Δημιουργήστε μία μοναδική παρουσία `SmartMarkerProcessor`.  
2. Ορίστε `DetailSheetNewName` (ή άλλες επιλογές ονόματος φύλλου) για να ελέγξετε τη λογική μετονομασίας.  
3. Περάστε την πηγή δεδομένων και τις επιλογές στη μέθοδο `Process`.  
4. Αποθηκεύστε και επαληθεύστε ότι το φύλλο μετονομήθηκε όπως αναμενόταν.

Με αυτά τα βήματα, μπορείτε να ενσωματώσετε το SmartMarker σε οποιοδήποτε pipeline αναφορών—είτε δημιουργείτε τιμολόγια, αρχεία ελέγχου ή μηνιαία dashboards. Η προσέγγιση κλιμακώνεται, διαχειρίζεται τις συγκρούσεις ονομάτων με χάρη, και διατηρεί τα πρότυπα Excel επαναχρησιμοποιήσιμα.

---

## Τι ακολουθεί;  

- **Εξερευνήστε άλλες επιλογές SmartMarkerOptions**: `HeaderSheetNewName`, `SummarySheetNewName` και `InsertBlankRows` για πιο ακριβή έλεγχο.  
- **Συνδυάστε με στυλ**: Χρησιμοποιήστε το πλούσιο API μορφοποίησης του GemBox για να εφαρμόσετε χρώματα, περιγράμματα ή υπό συνθήκη μορφοποίηση μετά τη συγχώνευση.  
- **Επεξεργασία σε παρτίδες πολλαπλών βιβλίων εργασίας**: Περάστε έναν φάκελο προτύπων, επαναχρησιμοποιώντας την ίδια παρουσία επεξεργαστή για μέγιστη απόδοση.

Νιώστε ελεύθεροι να πειραματιστείτε—ίσως δημιουργήσετε ένα φύλλο “Report_2024_Q1” που προσθέτει αυτόματα αριθμό έκδοσης σε κάθε εκτέλεση. Οι δυνατότητες είναι απεριόριστες, και τώρα έχετε μια σταθερή βάση για την αυτοματοποίηση **μετονομασίας υπάρχοντος φύλλου**.

Καλή προγραμματιστική δουλειά, και εύχομαι τα αρχεία Excel σας να παραμένουν πάντα οργανωμένα!

## Τι πρέπει να μάθετε στη συνέχεια;

- [How to Merge and Rename Excel Sheets Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [How to Change Excel Sheet IDs in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/worksheet-management/change-excel-sheet-id-net-aspose-cells/)
- [How to Use Aspose.Cells for .NET to Group Rows and Columns in Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}