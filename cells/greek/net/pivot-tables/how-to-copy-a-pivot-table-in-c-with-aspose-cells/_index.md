---
category: general
date: 2026-09-27
description: Μάθετε πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα σε C# χρησιμοποιώντας
  το Aspose.Cells. Περιλαμβάνει την αντιγραφή γραμμών με μορφοποίηση, την αντιγραφή
  του συγκεντρωτικού πίνακα σε άλλο φύλλο και την εξαγωγή του συγκεντρωτικού πίνακα
  σε νέο βιβλίο εργασίας.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: el
lastmod: 2026-09-27
og_description: Πώς να αντιγράψετε έναν πίνακα Pivot σε C# χρησιμοποιώντας το Aspose.Cells.
  Ακολουθήστε τον οδηγό βήμα‑προς‑βήμα για να αντιγράψετε γραμμές με μορφοποίηση,
  να μετακινήσετε έναν πίνακα Pivot σε άλλο φύλλο και να τον εξάγετε σε νέο βιβλίο
  εργασίας.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Πώς να αντιγράψετε έναν πίνακα Pivot σε C# – πλήρης οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Πώς να αντιγράψετε έναν πίνακα Pivot σε C# με το Aspose.Cells
url: /el/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε έναν πίνακα Pivot σε C# με το Aspose.Cells

Αν χρειάζεστε **να αντιγράψετε έναν πίνακα pivot** από ένα φύλλο εργασίας σε άλλο, η εκμάθηση **πώς να αντιγράψετε πίνακα pivot** σε C# με το Aspose.Cells μπορεί να σας εξοικονομήσει ώρες χειροκίνητης δουλειάς. Η προσέγγιση επιτρέπει επίσης **να αντιγράψετε γραμμές με μορφοποίηση**, να διατηρήσετε το pivot cache ανέπαφο και ακόμη **να εξάγετε τον πίνακα pivot σε νέο βιβλίο εργασίας** όταν χρειάζεστε ξεχωριστό αρχείο.

Αυτό το tutorial σας οδηγεί βήμα‑βήμα μέσα από τη διαδικασία:

* δημιουργία βιβλίου εργασίας,  
* αντιγραφή της περιοχής του πίνακα pivot διατηρώντας τη μορφοποίηση,  
* τοποθέτηση των αντιγραμμένων δεδομένων σε νέο φύλλο, και  
* αποθήκευση του αποτελέσματος ως ξεχωριστό αρχείο.

Θα δείτε γιατί η ενσωματωμένη μέθοδος `CopyRows` είναι ο πιο αξιόπιστος τρόπος για **να αντιγράψετε πίνακα pivot σε άλλο φύλλο**, και θα λάβετε συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως κρυμμένες γραμμές ή εξωτερικές πηγές δεδομένων.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| .NET 6.0 ή νεότερο | Το Aspose.Cells υποστηρίζει .NET 6+ και προσφέρει την καλύτερη απόδοση. |
| Visual Studio 2022 (ή οποιοδήποτε IDE για C#) | Χρειάζεστε έναν επεξεργαστή που μπορεί να επαναφέρει τα πακέτα NuGet. |
| Aspose.Cells for .NET (πακέτο NuGet `Aspose.Cells`) | Αυτή η βιβλιοθήκη παρέχει το API `CopyRows` που χρησιμοποιείται στο παράδειγμα. |
| Ένα αρχείο Excel προέλευσης (`source.xlsx`) που περιέχει πίνακα pivot στην περιοχή `A1:G20` | Ο κώδικας αντιγράφει αυτή τη συγκεκριμένη περιοχή· προσαρμόστε την περιοχή αν ο πίνακας pivot είναι μεγαλύτερος. |

Εγκαταστήστε τη βιβλιοθήκη με το NuGet CLI ή το Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## Βήμα 1: Φόρτωση του βιβλίου εργασίας που περιέχει τον πίνακα pivot

Η πρώτη γραμμή δημιουργεί ένα αντικείμενο `Workbook` που αντιπροσωπεύει ολόκληρο το αρχείο Excel. Η φόρτωση του αρχείου μία φορά σας δίνει πρόσβαση ανάγνωσης/εγγραφής σε κάθε φύλλο εργασίας.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Γιατί είναι σημαντικό** – Χωρίς τη φόρτωση του βιβλίου εργασίας, καμία από τις επόμενες κλήσεις `CopyRows` δεν μπορεί να αναφερθεί στα δεδομένα προέλευσης ή στο pivot cache.

## Βήμα 2: Προετοιμασία των φύλλων προέλευσης και προορισμού

Χρειάζεστε ένα φύλλο προορισμού όπου θα ζει ο αντιγραμμένος πίνακας pivot. Ο κώδικας παρακάτω παίρνει το πρώτο φύλλο (όπου βρίσκεται ο αρχικός πίνακας pivot) και προσθέτει ένα νέο φύλλο με όνομα **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Pro tip:** Αν το φύλλο προορισμού υπάρχει ήδη, καλέστε πρώτα `Worksheets.RemoveAt(index)` για να αποφύγετε διπλότυπα ονόματα.

## Βήμα 3: Ορισμός της περιοχής κελιών που περιβάλλει τον πίνακα pivot

Ένα αντικείμενο `CellArea` περιγράφει τα κελιά πάνω‑αριστερά και κάτω‑δεξιά της περιοχής που θέλετε να μετακινήσετε. Στο παράδειγμα, ο πίνακας pivot καταλαμβάνει το `A1:G20`. Προσαρμόστε τις συντεταγμένες για μεγαλύτερους πίνακες.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Βήμα 4: Αντιγραφή γραμμών με μορφοποίηση και διατήρηση του pivot cache

Η μέθοδος `CopyRows` αντιγράφει **γραμμές** από το φύλλο προέλευσης στο φύλλο προορισμού. Με το `CopyOptions.CopyAll` εξασφαλίζετε ότι τιμές, μορφοποίηση, διαγράμματα και ενσωματωμένα αντικείμενα—όλα μέρη ενός πίνακα pivot—μεταφέρονται.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Γιατί το `CopyRows` λειτουργεί καλύτερα από το `Copy` για πίνακες pivot

* Το `CopyRows` σέβεται το εσωτερικό pivot cache, έτσι ο αντιγραμμένος πίνακας παραμένει λειτουργικός.  
* Διατηρεί **αντιγραφή γραμμών με μορφοποίηση** ακριβώς όπως εμφανίζονται στο αρχικό φύλλο.  
* Σε αντίθεση με ένα απλό `Copy` περιοχής, μεταφέρει επίσης κρυμμένες γραμμές και τυχόν συνδεδεμένα slicers.

## Βήμα 5: Αποθήκευση του βιβλίου εργασίας με τον αντιγραμμένο πίνακα pivot

Τέλος, γράψτε το τροποποιημένο βιβλίο εργασίας στο δίσκο. Το νέο αρχείο περιέχει το αρχικό φύλλο συν ένα φύλλο **Copy** που κρατά ένα πλήρως λειτουργικό αντίγραφο του αρχικού πίνακα pivot.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Αναμενόμενο αποτέλεσμα

Όταν ανοίξετε το `pivot_copied.xlsx`:

* Το φύλλο **Sheet1** εξακολουθεί να περιέχει τα αρχικά δεδομένα και τον πίνακα pivot.  
* Το φύλλο **Copy** εμφανίζει έναν ταυτόσημο πίνακα pivot με την ίδια διάταξη, φίλτρα και μορφοποίηση.  
* Όλοι οι τύποι και οι συνδέσεις δεδομένων παραμένουν άθικτοι επειδή το pivot cache αντιγράφηκε μαζί με τις γραμμές.

## Πώς να αντιγράψετε πίνακα pivot σε άλλο φύλλο στο ίδιο βιβλίο εργασίας

Αν χρειάζεστε τον πίνακα pivot μόνο σε διαφορετικό υπάρχον φύλλο (π.χ. “Report”), αντικαταστήστε το βήμα δημιουργίας προορισμού με μια αναφορά στο επιθυμητό φύλλο:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Αυτό το απόσπασμα δείχνει **πώς να αντιγράψετε πίνακα pivot σε άλλο φύλλο** χωρίς να δημιουργήσετε νέο φύλλο εργασίας.

## Εξαγωγή πίνακα pivot σε νέο βιβλίο εργασίας

Μερικές φορές θέλετε τον πίνακα pivot σε εντελώς ξεχωριστό αρχείο. Μετά την αντιγραφή, μπορείτε να αφαιρέσετε όλα τα φύλλα εκτός από αυτό που κρατά τον αντιγραμμένο πίνακα pivot και στη συνέχεια να αποθηκεύσετε:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Τώρα το `pivot_only.xlsx` περιέχει ένα μόνο φύλλο με τον διπλότυπο πίνακα pivot, καλύπτοντας την απαίτηση **εξαγωγής πίνακα pivot σε νέο βιβλίο εργασίας**.

## Πώς να αντιγράψετε γραμμές Excel χωρίς να χάσετε τη μορφοποίηση

Η ίδια κλήση `CopyRows` λειτουργεί για οποιαδήποτε περιοχή, όχι μόνο για πίνακες pivot. Αν χρειάζεστε **να αντιγράψετε γραμμές Excel** που περιλαμβάνουν conditional formatting, data validation ή merged cells, χρησιμοποιήστε την ίδια μέθοδο:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Επειδή το `CopyOptions.CopyAll` μεταφέρει τα πάντα, οι γραμμές προορισμού φαίνονται ακριβώς όπως οι γραμμές προέλευσης.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Συμπτωμα | Διόρθωση |
|----------|----------|----------|
| Η περιοχή προέλευσης δεν περιλαμβάνει ολόκληρο τον πίνακα pivot | Ο αντιγραμμένος πίνακας pivot εμφανίζεται κομμένος. | Επαληθεύστε ότι το `CellArea` καλύπτει όλες τις γραμμές/στήλες του πίνακα pivot. |
| Το φύλλο προορισμού περιέχει ήδη δεδομένα | Οι γραμμές που αντικαθίστανται προκαλούν απώλεια δεδομένων. | Επιλέξτε ένα καθαρό φύλλο ή ξεκινήστε την αντιγραφή σε υψηλότερο δείκτη γραμμής. |
| Ο πίνακας pivot χρησιμοποιεί εξωτερική πηγή δεδομένων | Η αντιγραφή χάνει τη σύνδεση. | Μετά την αντιγραφή, καλέστε `pivotTable.RefreshData()` για να επανασυνδέσετε. |
| Οι κρυμμένες γραμμές παραλείπονται | Κάποιες γραμμές εξαφανίζονται στην αντιγραφή. | Το `CopyRows` αντιγράφει αυτόματα κρυμμένες γραμμές· βεβαιωθείτε ότι δεν χρησιμοποιείτε `CopyOptions.CopyValuesOnly`. |

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που μπορείτε να επικολλήσετε σε ένα νέο console project. Δείχνει κάθε βήμα που συζητήθηκε παραπάνω.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Η εκτέλεση του προγράμματος** δημιουργεί το `pivot_copied.xlsx` με ένα αντίγραφο του αρχικού πίνακα pivot σε νέο φύλλο με όνομα **Copy**.

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να αντιγράψετε έναν πίνακα pivot** σε C# χρησιμοποιώντας

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}