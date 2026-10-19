---
category: general
date: 2026-10-04
description: Μάθετε πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα από ένα βιβλίο εργασίας
  σε άλλο χρησιμοποιώντας C#. Αυτός ο οδηγός καλύπτει επίσης πώς να αντιγράψετε γραμμές,
  να δημιουργήσετε αντίγραφο του συγκεντρωτικού πίνακα και να αντιγράψετε αποτελεσματικά
  ένα εύρος Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: el
lastmod: 2026-10-04
og_description: Αντιγραφή πίνακα Pivot στο Excel με C#. Ακολουθήστε αυτόν τον πλήρη
  οδηγό για να δημιουργήσετε αντίγραφα πινάκων Pivot, να αντιγράψετε γραμμές και να
  αντιγράψετε περιοχή Excel με το Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: Αντιγραφή συγκεντρωτικού πίνακα στο Excel με C# – βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να αντιγράψετε έναν πίνακα Pivot στο Excel με C# και Aspose.Cells
url: /el/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε έναν πίνακα Pivot στο Excel με C# και Aspose.Cells

Εάν χρειάζεται να **αντιγράψετε έναν πίνακα pivot** από ένα βιβλίο εργασίας σε άλλο, αυτό το tutorial σας δείχνει μια πλήρη, εκτελέσιμη λύση. Θα δείτε ακριβώς πώς να φορτώσετε ένα αρχείο πηγής, να ορίσετε την περιοχή που περιέχει το pivot, να αντιγράψετε τις γραμμές (συμπεριλαμβανομένου του ορισμού του pivot) και να αποθηκεύσετε το αποτέλεσμα. Είτε αυτοματοποιείτε μια διαδικασία αναφοράς είτε δημιουργείτε ένα εργαλείο μετεγκατάστασης, τα παρακάτω βήματα σας επιτρέπουν να διπλασιάσετε έναν πίνακα pivot με μόνο λίγες γραμμές C#.

Η αντιγραφή ενός πίνακα pivot είναι περισσότερο από την αντιγραφή τιμών κελιών· η υποκείμενη cache και οι ρυθμίσεις πεδίων πρέπει να μεταφερθούν μαζί. Το παράδειγμα χρησιμοποιεί τη βιβλιοθήκη **Aspose.Cells** επειδή διαχειρίζεται αυτόματα τα μεταδεδομένα του pivot, ώστε να μην χρειάζεται να επαναδημιουργήσετε τη cache χειροκίνητα. Στο τέλος αυτού του οδηγού θα μπορείτε να **αντιγράψετε pivot**, **αντιγράψετε περιοχή Excel** και **αντιγράψετε γραμμές** με ασφάλεια.

## Προαπαιτήσεις

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 ή νεότερη έκδοση εγκατεστημένη (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).
- Ένα έγκυρο license του Aspose.Cells for .NET ή προσωρινή άδεια αξιολόγησης.
- Δύο αρχεία Excel: `Source.xlsx` που περιέχει τον πίνακα pivot που θέλετε να διπλασιάσετε, και έναν κενό φάκελο όπου θα γραφτεί το `CopyWithPivot.xlsx`.
- Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει C#).

## Βήμα 1: Ρύθμιση του έργου και προσθήκη του Aspose.Cells

Δημιουργήστε ένα νέο project console και προσθέστε το πακέτο NuGet Aspose.Cells:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

Το πακέτο παρέχει τις κλάσεις `Workbook`, `Worksheet` και `CellArea` που χρησιμοποιούνται στον παρακάτω κώδικα.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας πηγής που περιέχει τον πίνακα pivot

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του βιβλίου εργασίας δημιουργεί μια αναπαράσταση στη μνήμη όλων των φύλλων, συμπεριλαμβανομένων τυχόν κρυφών caches pivot. Χωρίς τη φόρτωση του αρχείου, δεν μπορείτε να αναφερθείτε στην περιοχή του pivot.

## Βήμα 3: Ορισμός της περιοχής κελιών που καλύπτει τον πίνακα pivot

Πρέπει να πείτε στο Aspose.Cells ποιες γραμμές και στήλες ανήκουν στο pivot. Η δομή `CellArea` σας επιτρέπει να ορίσετε ένα ορθογώνιο μπλοκ.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Συμβουλή:** Εάν δεν είστε σίγουροι για το ακριβές μέγεθος, ανοίξτε το αρχείο πηγής στο Excel, επιλέξτε το pivot και σημειώστε την περιοχή που εμφανίζεται στο Name Box (π.χ., `A1:K31`). Μετατρέψτε τις συντεταγμένες του Excel σε δείκτες μηδενικής βάσης για τον κώδικα.

## Βήμα 4: Δημιουργία νέου βιβλίου εργασίας προορισμού και λήψη του πρώτου φύλλου του

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Γιατί απαιτείται αυτό το βήμα:** Το βιβλίο εργασίας προορισμού πρέπει να υπάρχει πριν μπορέσετε να αντιγράψετε γραμμές. Το Aspose.Cells δημιουργεί αυτόματα ένα προεπιλεγμένο φύλλο, το οποίο θα χρησιμοποιήσουμε ως στόχο.

## Βήμα 5: Αντιγραφή των γραμμών (συμπεριλαμβανομένου του πίνακα pivot) από την πηγή στον προορισμό

Η μέθοδος `CopyRows` αντιγράφει τόσο τις τιμές κελιών όσο και τη σχετική cache του pivot.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **Πώς λειτουργεί:**  
> - Η `CopyRows` λαμβάνει το φύλλο πηγής, τη γραμμή έναρξης και τον αριθμό γραμμών προς αντιγραφή.  
> - Λαμβάνει επίσης το φύλλο προορισμού και τη γραμμή όπου πρέπει να ξεκινήσει η αντιγραφή.  
> - Επειδή η περιοχή πηγής περιλαμβάνει τον πίνακα pivot, η μέθοδος μεταφέρει τη cache, τη λίστα πεδίων και τη διάταξη του pivot αμετάβλητα. Αυτό αποτελεί τον πυρήνα του **πώς να αντιγράψετε pivot** χωρίς απώλεια λειτουργικότητας.

### Ακραία περίπτωση: αντιγραφή pivot που εκτείνεται σε πολλά φύλλα

Εάν τα δεδομένα πηγής του pivot βρίσκονται σε διαφορετικό φύλλο από το ίδιο το pivot, η cache ακολουθεί την αντιγραφή επειδή το Aspose.Cells αποθηκεύει τη cache στο βιβλίο εργασίας, όχι στο φύλλο. Ωστόσο, πρέπει να διασφαλίσετε ότι το βιβλίο εργασίας προορισμού περιέχει την ίδια περιοχή δεδομένων πηγής· διαφορετικά το pivot θα εμφανίσει σφάλματα `#REF!`. Σε τέτοιες περιπτώσεις, αντιγράψτε πρώτα την περιοχή δεδομένων πηγής και μετά τις γραμμές του pivot.

## Βήμα 6: Αποθήκευση του βιβλίου εργασίας που τώρα περιέχει τον αντιγραμμένο πίνακα pivot

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Η εκτέλεση του προγράμματος παράγει το `CopyWithPivot.xlsx` με ακριβή αντίγραφο του αρχικού πίνακα pivot, συμπεριλαμβανομένων όλων των slicers, φίλτρων και υπολογιζόμενων πεδίων.

### Αναμενόμενο αποτέλεσμα

Κατά το άνοιγμα του `CopyWithPivot.xlsx`:

- Ο πίνακας pivot εμφανίζεται στην ίδια θέση (π.χ., A1:K31) όπως στο `Source.xlsx`.
- Όλες οι ετικέτες γραμμών και στηλών, τα σύνολα και η μορφοποίηση διατηρούνται.
- Η ανανέωση του pivot εμφανίζει τα ίδια δεδομένα με την πηγή, επιβεβαιώνοντας ότι η cache αντιγράφηκε σωστά.

## Πώς να αντιγράψετε γραμμές χωρίς pivot (αντιγραφή περιοχής Excel)

Εάν χρειάζεται μόνο να **αντιγράψετε περιοχή Excel** χωρίς δεδομένα pivot, μπορείτε να χρησιμοποιήσετε την ίδια μέθοδο `CopyRows` αλλά να στοχεύσετε μια περιοχή που δεν περιέχει pivot. Για παράδειγμα:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

Αυτό δείχνει **πώς να αντιγράψετε γραμμές** για γενικά δεδομένα, ενισχύοντας την ευελιξία του ίδιου API.

## Διπλασιασμός πίνακα pivot στο ίδιο βιβλίο εργασίας (εναλλακτική προσέγγιση)

Μερικές φορές θέλετε να **διπλασιάσετε έναν πίνακα pivot** μέσα στο ίδιο βιβλίο εργασίας αντί να δημιουργήσετε νέο αρχείο. Μπορείτε να το πετύχετε αντιγράφοντας γραμμές σε διαφορετική θέση:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

Μετά την αποθήκευση, το βιβλίο εργασίας θα περιέχει δύο ταυτόσημα pivots—χρήσιμο για σύγκριση πλευρά-προς-πλευρά ή δημιουργία αντιγράφων ασφαλείας.

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Ο πίνακας pivot εμφανίζει `#REF!` μετά την αντιγραφή | Η περιοχή δεδομένων πηγής δεν υπάρχει στο βιβλίο εργασίας προορισμού | Αντιγράψτε πρώτα την περιοχή δεδομένων πηγής ή χρησιμοποιήστε το `CopyRows` στο φύλλο δεδομένων πηγής πριν αντιγράψετε το pivot |
| Απώλεια μορφοποίησης | Αντιγράφηκαν μόνο τιμές (π.χ., χρήση `Copy` αντί για `CopyRows`) | Χρησιμοποιείτε πάντα το `CopyRows` που διατηρεί το στυλ, τη μορφοποίηση και τα μεταδεδομένα του pivot |
| Απροσδόκητη μετατόπιση γραμμής | Η αρχική γραμμή προορισμού δεν ταιριάζει με την αρχική γραμμή πηγής | Επαληθεύστε ότι η αρχική γραμμή `destWorksheet.Cells` ταιριάζει με την επιθυμητή θέση |
| Μεγάλα βιβλία εργασίας προκαλούν πίεση μνήμης | `CopyRows` φορτώνει ολόκληρα φύλλα στη μνήμη | Επεξεργαστείτε την αντιγραφή σε τμήματα ή χρησιμοποιήστε streaming APIs εάν εργάζεστε με >100.000 γραμμές |

## Πλήρες, εκτελέσιμο παράδειγμα

Ακολουθεί το πλήρες πρόγραμμα που μπορείτε να επικολλήσετε στο `Program.cs` και να τρέξετε αμέσως (αντικαταστήστε το `YOUR_DIRECTORY` με πραγματική διαδρομή στο σύστημά σας).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Τρέξτε το πρόγραμμα με `dotnet run`. Μετά την εκτέλεση, ανοίξτε το `CopyWithPivot.xlsx` για να επαληθεύσετε ότι ο πίνακας pivot εμφανίζεται ακριβώς όπως στο αρχικό αρχείο.

## Συμπέρασμα

Τώρα ξέρετε πώς να **αντιγράψετε έναν πίνακα pivot** από ένα βιβλίο εργασίας Excel σε άλλο χρησιμοποιώντας C# και Aspose.Cells. Ο οδηγός κάλυψε τη πλήρη ροή εργασίας—από τη φόρτωση του αρχείου πηγής, τον ορισμό της περιοχής κελιών του pivot, την αντιγραφή γραμμών και την αποθήκευση του βιβλίου εργασίας προορισμού. Επιπλέον, μάθατε **πώς να αντιγράψετε γραμμές**, **πώς να αντιγράψετε περιοχή Excel** και **πώς να διπλασιάσετε πίνακα pivot** στο ίδιο αρχείο, καθώς και κοινά προβλήματα και συμβουλές βέλτιστων πρακτικών.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να προσθέσετε κώδικα για προγραμματιστική ανανέωση του αντιγραμμένου pivot ή εξερευνήστε την εξαγωγή του pivot σε PDF με Aspose.Cells. Πειραματιστείτε με διαφορετικές περιοχές πηγής και θα κυριαρχήσετε γρήγορα στην αυτοματοποίηση του Excel στο .NET.

---


## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αντιγραφή Πίνακα Pivot σε C# – Πλήρης Οδηγός Βήμα‑βήμα](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Δημιουργία Νέου Βιβλίου Excel – Αντιγραφή & Διπλασιασμός Πίνακα Pivot](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Αντιγραφή γραμμών Excel – Διατήρηση Πίνακα Pivot κατά τη Διπλασίαση Γραμμών](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}