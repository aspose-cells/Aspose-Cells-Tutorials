---
category: general
date: 2026-07-29
description: Αντιγράψτε γραμμές από ένα φύλλο εργασίας σε άλλο και μάθετε πώς να φορτώνετε
  ένα βιβλίο εργασίας Excel προγραμματιστικά χρησιμοποιώντας το Aspose.Cells σε έναν
  οδηγό βήμα‑βήμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: el
lastmod: 2026-07-29
og_description: Αντιγράψτε γραμμές από ένα φύλλο εργασίας σε άλλο χρησιμοποιώντας
  το Aspose.Cells. Μάθετε πώς να φορτώνετε ένα βιβλίο εργασίας Excel προγραμματιστικά
  και να διατηρείτε τους πίνακες Pivot με λίγες μόνο γραμμές κώδικα C#.
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: Αντιγραφή γραμμών από ένα φύλλο εργασίας σε άλλο – Οδηγός αυτοματοποίησης
  Excel με C#
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Αντιγραφή γραμμών από ένα φύλλο εργασίας σε άλλο – Πλήρης οδηγός C#
url: /el/net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αντιγραφή γραμμών από ένα φύλλο εργασίας σε άλλο – Πλήρης Οδηγός C# 

Έχετε χρειαστεί ποτέ να **αντιγράψετε γραμμές από ένα φύλλο εργασίας σε άλλο** αλλά δεν ήσασταν σίγουροι πώς να διατηρήσετε τους τύπους και τους πίνακες Pivot ανέπαφους; Δεν είστε μόνοι. Σε πολλές αλυσίδες αναφοράς πρέπει να εξάγουμε ένα τμήμα δεδομένων από ένα κύριο φύλλο και να το τοποθετήσουμε σε ένα νέο βιβλίο εργασίας για επεξεργασία downstream. Τα καλά νέα; Με το Aspose.Cells μπορείτε να το κάνετε προγραμματιστικά, και ολόκληρη η διαδικασία απαιτεί μόνο μερικές γραμμές.

Σε αυτό το tutorial θα περάσουμε από τη φόρτωση ενός βιβλίου εργασίας Excel προγραμματιστικά, την επιλογή μιας περιοχής, και στη συνέχεια την αντιγραφή αυτών των γραμμών σε ένα ολοκαίνουργιο βιβλίο εργασίας διατηρώντας τυχόν ενσωματωμένους πίνακες Pivot. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C# — χωρίς χειροκίνητη αντιγραφή‑επικόλληση.

## Τι Θα Επιτύχετε

- **Φορτώστε βιβλίο εργασίας Excel προγραμματιστικά** χρησιμοποιώντας την κλάση `Workbook` του Aspose.Cells.  
- Ορίστε μια **περιοχή κελιών** που περιέχει τις γραμμές που θέλετε να μετακινήσετε.  
- **Αντιγράψτε γραμμές από ένα φύλλο εργασίας σε άλλο** με μία κλήση μεθόδου που διατηρεί τους πίνακες Pivot ενεργούς.  
- Αποθηκεύστε το αποτέλεσμα σε νέο αρχείο έτοιμο για διανομή ή περαιτέρω επεξεργασία.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί τόσο σε .NET Core όσο και σε .NET Framework).  
- Έγκυρη άδεια Aspose.Cells (ή προσωρινό κλειδί αξιολόγησης).  
- Δύο φακέλους στο δίσκο: ένας για το πηγαίο βιβλίο εργασίας (`Source.xlsx`) και ένας για τον προορισμό (`Destination.xlsx`).  

Αν τα έχετε, ας ξεκινήσουμε.

## Βήμα 1: Φορτώστε βιβλίο εργασίας Excel προγραμματιστικά

Πρώτα απ' όλα — πριν μπορέσετε να αντιγράψετε οτιδήποτε, πρέπει να φέρετε το πηγαίο αρχείο στη μνήμη. Το Aspose.Cells κάνει αυτό παιχνιδάκι:

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **Γιατί είναι σημαντικό:** Η προγραμματιστική φόρτωση του βιβλίου εργασίας σας δίνει πλήρη έλεγχο του περιεχομένου του αρχείου χωρίς να ανοίξετε ποτέ το Excel στον διακομιστή. Επίσης αποφεύγει τα προβλήματα COM interop και λειτουργεί σε περιβάλλοντα χωρίς UI όπως οι CI pipelines.

## Βήμα 2: Ορίστε την πηγαία περιοχή που περιέχει τις γραμμές

Στη συνέχεια, προσδιορίστε ακριβώς ποιες γραμμές θέλετε να μεταφέρετε. Το αντικείμενο `CellArea` σας επιτρέπει να ορίσετε ένα ορθογώνιο μπλοκ χρησιμοποιώντας τις διευθύνσεις του πάνω‑αριστερού και κάτω‑δεξιού κελιού:

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **Συμβουλή:** Εάν το μέγεθος των δεδομένων σας αλλάζει δυναμικά, μπορείτε να υπολογίσετε το `EndRow` με το `sourceWorksheet.Cells.MaxDataRow` ώστε πάντα να καλύπτετε ολόκληρο τον πίνακα.

## Βήμα 3: Δημιουργήστε ένα νέο βιβλίο εργασίας για τον προορισμό

Τώρα δημιουργήστε ένα κενό βιβλίο εργασίας που θα λάβει τις αντιγραμμένες γραμμές. Αυτό το βιβλίο ξεκινά με ένα μόνο φύλλο εργασίας από προεπιλογή:

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **Γιατί ένα νέο βιβλίο εργασίας;** Η καθαρή εκκίνηση εξασφαλίζει ότι δεν θα αντικαταστήσετε κατά λάθος υπάρχοντα δεδομένα και σας παρέχει ένα προβλέψιμο περιβάλλον για δοκιμές.

## Βήμα 4: Αντιγράψτε γραμμές από ένα φύλλο εργασίας σε άλλο (διατηρώντας τους πίνακες Pivot)

Αυτή είναι η καρδιά του tutorial. Η μέθοδος `CopyRows` αντιγράφει τις επιλεγμένες γραμμές και, όταν περάσετε `true` ως το τελευταίο όρισμα, αντιγράφει επίσης τυχόν πίνακες Pivot που βρίσκονται μέσα στην περιοχή:

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### Τι συμβαίνει στο παρασκήνιο;

- **Φύλλο πηγής**: `sourceWorkbook.Worksheets[0]` δείχνει στο πρώτο φύλλο του πηγαίου αρχείου.  
- **Δείκτες γραμμών**: Το Aspose.Cells χρησιμοποιεί μηδενική αρίθμηση, έτσι τα `StartRow` και `EndRow` αντιστοιχούν στις γραμμές που ορίσατε στο `sourceRange`.  
- **Γραμμή εκκίνησης προορισμού**: Ξεκινάμε στη γραμμή 0 στο νέο φύλλο, τοποθετώντας ουσιαστικά το αντιγραμμένο μπλοκ στην κορυφή.  
- **Σημαία `true`**: Αυτός είναι ο μαγικός διακόπτης που λέει στο Aspose.Cells να κλωνοποιήσει τυχόν πίνακες Pivot που βρίσκονται μέσα στις αντιγραμμένες γραμμές, διατηρώντας τη μνήμη cache και τις συνδέσεις τους.  

> **Προειδοποίηση για ειδικές περιπτώσεις:** Εάν η πηγαία περιοχή περιέχει συγχωνευμένα κελιά που εκτείνονται εκτός του ορισμένου χώρου, αυτές οι συγχωνεύσεις θα περικοπούν. Για να τις διατηρήσετε ανέπαφες, επεκτείνετε την περιοχή ώστε να καλύπτει πλήρως την συγχωνευμένη περιοχή.

## Βήμα 5: Αποθηκεύστε το βιβλίο εργασίας προορισμού

Τέλος, γράψτε το νέο αρχείο στο δίσκο. Μπορείτε να επιλέξετε οποιονδήποτε φάκελο θέλετε· απλώς βεβαιωθείτε ότι η διαδικασία έχει δικαιώματα εγγραφής:

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

Όταν ανοίξετε το `Destination.xlsx` θα δείτε τις γραμμές A1‑H20 να έχουν αντιγραφεί, συμπεριλαμβανομένων τυχόν πινάκων Pivot που ήταν αρχικά ενσωματωμένοι. Το υπόλοιπο του βιβλίου παραμένει κενό, έτοιμο να προσθέσετε περισσότερα φύλλα ή δεδομένα αργότερα.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι το πλήρες, εκτελέσιμο πρόγραμμα:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**Αναμενόμενη έξοδος** (console):

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

Ανοίξτε το αρχείο προορισμού και ελέγξτε ότι τα δεδομένα, η μορφοποίηση και οι πίνακες Pivot φαίνονται ακριβώς όπως στο πηγαίο αρχείο. Εάν παρατηρήσετε ελλιπή δεδομένα, ελέγξτε ξανά ότι το `sourceRange` καλύπτει πλήρως τις σχετικές γραμμές.

## Συχνές Ερωτήσεις & Συμβουλές

- **Μπορώ να αντιγράψω σε συγκεκριμένο φύλλο εργασίας αντί για το πρώτο;**  
  Απόλυτα. Αντικαταστήστε το `destinationWorkbook.Worksheets[0]` με `destinationWorkbook.Worksheets["TargetSheet"]` (δημιουργήστε το φύλλο πρώτα αν δεν υπάρχει).

- **Τι γίνεται αν χρειαστεί να αντιγράψω μόνο τις τιμές, όχι τους τύπους;**  
  Χρησιμοποιήστε το `CopyRows` με την υπερφόρτωση που δέχεται ένα αντικείμενο `CopyRowsOptions` και ορίστε `PasteType` σε `PasteType.Values`.

- **Πώς να διαχειριστώ μεγάλα αρχεία χωρίς να εξαντλήσω τη μνήμη;**  
  Το Aspose.Cells υποστηρίζει **streaming** μέσω `LoadOptions` με `MemorySetting.MemoryPreference`. Φορτώστε το πηγαίο βιβλίο εργασίας με μικρότερο αποτύπωμα μνήμης και η λειτουργία αντιγραφής θα παραμείνει αποδοτική.

- **Παραμένουν οι πίνακες Pivot συνδεδεμένοι με την αρχική πηγή δεδομένων;**  
  Όταν ορίσετε τη σημαία `true`, η μνήμη cache του Pivot διπλασιάζεται, έτσι οι νέοι πίνακες Pivot στο νέο βιβλίο αναφέρονται στα αντιγραμμένα δεδομένα, όχι στο αρχικό αρχείο.

## Συμπεράσματα

Τώρα ξέρετε πώς να **αντιγράψετε γραμμές από ένα φύλλο εργασίας σε άλλο** διατηρώντας τυχόν πίνακες Pivot ανέπαφους, και έχετε δει πώς να **φορτώσετε βιβλίο εργασίας Excel προγραμματιστικά** χρησιμοποιώντας το Aspose.Cells. Αυτό το πρότυπο αποτελεί ισχυρή βάση για την κατασκευή αυτοματοποιημένων αλυσίδων αναφοράς, scripts μεταφοράς δεδομένων ή οποιοδήποτε σενάριο που απαιτεί διαχωρισμό δεδομένων Excel σε πραγματικό χρόνο.

Τι ακολουθεί; Δοκιμάστε να επεκτείνετε το snippet ώστε:

- Να επαναλάβετε πάνω σε πολλαπλές πηγικές περιοχές και να τις συγκεντρώσετε σε ένα ενιαίο αρχείο προορισμού.  
- Να εφαρμόσετε conditional formatting μετά την αντιγραφή για να επισημάνετε βασικές μετρήσεις.  
- Να εξάγετε το τελικό βιβλίο εργασίας σε PDF ή CSV για downstream κατανάλωση.

Πειραματιστείτε ελεύθερα, και αν συναντήσετε κάποιο πρόβλημα, αφήστε ένα σχόλιο παρακάτω. Καλό κώδικα!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Αντιγράψετε Γραμμές στο Excel Χρησιμοποιώντας το Aspose.Cells για .NET: Ένας Οδηγός C#](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)
- [Αντιγραφή Φύλλου Εργασίας από Ένα Βιβλίο Εργασίας σε Άλλο χρησιμοποιώντας το Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [Πώς να Εξάγετε Ορατές Γραμμές Excel Χρησιμοποιώντας το Aspose.Cells για .NET: Οδηγός Βήμα‑Βήμα](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}