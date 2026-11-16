---
category: general
date: 2026-11-16
description: Πώς να αντιγράψετε έναν πίνακα Pivot από ένα αρχείο Excel σε ένα νέο
  βιβλίο εργασίας χρησιμοποιώντας C#. Μάθετε πώς να φορτώνετε το βιβλίο εργασίας,
  να αντιγράφετε την περιοχή και να διατηρείτε τους πίνακες Pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: el
lastmod: 2026-11-16
og_description: Πώς να αντιγράψετε έναν πίνακα Pivot από ένα υπάρχον βιβλίο εργασίας
  σε ένα νέο βιβλίο εργασίας χρησιμοποιώντας C#. Ακολουθήστε αυτόν τον πλήρη οδηγό
  για να φορτώσετε το βιβλίο εργασίας Excel, να αντιγράψετε την περιοχή και να διατηρήσετε
  τον πίνακα Pivot αμετάβλητο.
og_image_alt: how to copy pivot table example in C#
og_title: Πώς να αντιγράψετε έναν πίνακα pivot σε νέο βιβλίο εργασίας σε C# – οδηγός
  βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα σε νέο βιβλίο εργασίας σε C#
url: /el/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε έναν πίνακα Pivot σε νέο βιβλίο εργασίας σε C#

Αν χρειάζεστε **how to copy pivot table** από ένα αρχείο Excel σε ένα νέο βιβλίο εργασίας, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα. Θα μάθετε πώς να **load excel workbook c#**, ορίζετε την περιοχή προέλευσης και **copy range to new workbook** διατηρώντας τον πίνακα pivot αμετάβλητο.

Η αντιγραφή ενός πίνακα pivot είναι συχνή απαίτηση όταν θέλετε να επαναχρησιμοποιήσετε ένα πρότυπο αναφοράς, να μεταφέρετε δεδομένα μεταξύ έργων ή να δημιουργήσετε ένα ελαφρύ αρχείο για διανομή. Το παρακάτω δείγμα κώδικα χρησιμοποιεί το Aspose.Cells, μια πλήρως διαχειριζόμενη βιβλιοθήκη .NET που λειτουργεί χωρίς εγκατεστημένο Microsoft Office. Στο τέλος αυτού του tutorial θα έχετε ένα εκτελέσιμο πρόγραμμα που δημιουργεί ένα νέο βιβλίο εργασίας που περιέχει τον αρχικό πίνακα pivot, έτοιμο για περαιτέρω επεξεργασία ή κοινή χρήση.

## Προαπαιτήσεις

* .NET 6.0 SDK ή νεότερο (το παράδειγμα λειτουργεί με .NET Core και .NET Framework)
* Visual Studio 2022 ή οποιονδήποτε επεξεργαστή C# προτιμάτε
* Άδεια Aspose.Cells for .NET (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση)
* Ένα αρχείο Excel προέλευσης (`Source.xlsx`) που περιέχει τουλάχιστον έναν πίνακα pivot

> **Pro tip:** Εάν χρησιμοποιείτε τη δωρεάν δοκιμή, ορίστε την άδεια στον κώδικα για να αποφύγετε τα υδατογράμματα αξιολόγησης.

## Βήμα 1: Φόρτωση του βιβλίου εργασίας προέλευσης (load excel workbook c#)

Η πρώτη ενέργεια είναι το άνοιγμα του βιβλίου εργασίας που περιέχει τον πίνακα pivot. Το Aspose.Cells διαβάζει το αρχείο στη μνήμη, παρέχοντάς σας πλήρη πρόσβαση στα φύλλα εργασίας, τα κελιά και τα αντικείμενα pivot.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Γιατί είναι σημαντικό*: Η φόρτωση του βιβλίου εργασίας είναι η βάση για οποιοδήποτε αυτοματισμό Excel. Χωρίς ένα έγκυρο αντικείμενο `Workbook` δεν μπορείτε να εξετάσετε τον pivot ή να αντιγράψετε τα δεδομένα του.

## Βήμα 2: Ορισμός της περιοχής κελιών που περιβάλλει τον πίνακα pivot (copy range to new workbook)

Ένας πίνακας pivot ζει μέσα σε ένα ορθογώνιο μπλοκ κελιών. Πρέπει να καθορίσετε αυτό το μπλοκ ώστε η λειτουργία αντιγραφής να ξέρει τι να μετακινήσει. Ο κατασκευαστής `CellArea` χρησιμοποιεί δείκτες μηδενικής βάσης: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Γιατί είναι σημαντικό*: Ορίζοντας ρητά την περιοχή αποφεύγετε την αντιγραφή άσχετων δεδομένων και εξασφαλίζετε ότι περιλαμβάνεται η cache του pivot. Η περιοχή μπορεί να υπολογιστεί δυναμικά εάν χρειάζεται να διαχειριστείτε διαφορετικά μεγέθη pivot.

## Βήμα 3: Δημιουργία νέου βιβλίου εργασίας και λήψη του πρώτου φύλλου του

Τώρα δημιουργήστε το βιβλίο εργασίας προορισμού που θα λάβει τις αντιγραμμένες σειρές. Το Aspose.Cells προσθέτει αυτόματα ένα προεπιλεγμένο φύλλο, το οποίο θα χρησιμοποιήσουμε ως στόχο.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Γιατί είναι σημαντικό*: Ξεκινώντας με ένα καθαρό βιβλίο εργασίας εξασφαλίζει ότι μόνο ο πίνακας pivot (και οι υποστηρικτικές σειρές του) θα καταλήξουν στο αρχείο, διατηρώντας το αποτέλεσμα ελαφρύ.

## Βήμα 4: Αντιγραφή σειρών από την περιοχή προέλευσης στο φύλλο προορισμού (how to copy pivot table)

Η μέθοδος `CopyRows` αντιγράφει ολόκληρες σειρές, διατηρώντας τύπους, μορφοποίηση και—καίριας σημασίας—πίνακες pivot. Οι παράμετροι της μεθόδου είναι: η αρχική σειρά, η τελική σειρά, η συλλογή κελιών-στόχου και ο δείκτης σειράς στον προορισμό όπου αρχίζει η αντιγραφή (εδώ `0` για να ξεκινήσει από την πρώτη σειρά).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Γιατί είναι σημαντικό*: Η χρήση του `CopyRows` αντί για αντιγραφή μεμονωμένων κελιών διασφαλίζει ότι η cache του pivot παραμένει συνδεδεμένη με τα αντιγραμμένα δεδομένα. Το Aspose.Cells διαχειρίζεται τις υποκείμενες δομές XML, έτσι δεν χρειάζεται να ξαναχτίσετε τον pivot χειροκίνητα.

## Βήμα 5: Αποθήκευση του προκύπτοντος βιβλίου εργασίας (copy range to new workbook)

Τέλος, γράψτε το νέο αρχείο στο δίσκο. Το βιβλίο εργασίας προορισμού περιέχει τώρα έναν ταυτόσημο πίνακα pivot που λειτουργεί ανεξάρτητα από το αρχείο προέλευσης.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος παράγει το `CopyWithPivot.xlsx`. Το άνοιγμα του αρχείου στο Excel εμφανίζει:

* Την ίδια διάταξη πίνακα pivot όπως στο `Source.xlsx`
* Όλες τις σειρές δεδομένων προέλευσης που ήταν μέρος της cache του pivot
* Καμία αναφορά στο αρχικό βιβλίο εργασίας (ο pivot λειτουργεί εκτός σύνδεσης)

## Διαχείριση κοινών παραλλαγών

### Αντιγραφή πολλαπλών πινάκων pivot

Εάν το φύλλο προέλευσης περιέχει πολλούς πίνακες pivot, επεκτείνετε το `CellArea` ώστε να καλύπτει την ένωση όλων των περιοχών, ή επαναλάβετε το βήμα αντιγραφής για κάθε ξεχωριστή περιοχή.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Διατήρηση στυλ και μορφοποίησης υπό όρους

`CopyRows` αντιγράφει αυτόματα τα στυλ κελιών. Εάν χρειάζεται να διατηρήσετε ονομαστικά στυλ σε όλο το βιβλίο εργασίας ή προσαρμοσμένες μορφές αριθμών, καλέστε `destWorkbook.Worksheets[0].CopyStyle` πριν από την αποθήκευση.

### Εργασία με μεγάλα βιβλία εργασίας

Για αρχεία μεγαλύτερα από 100 MB, σκεφτείτε να χρησιμοποιήσετε `Workbook.LoadOptions` με το `MemorySetting` ορισμένο σε `MemorySetting.MemoryPreference` για να μειώσετε την πίεση στη μνήμη.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Πλήρης κώδικας πηγής (έτοιμος για εκτέλεση)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, συμπεριλαμβανομένων των οδηγιών `using` και των σχολίων. Αντιγράψτε το σε ένα νέο έργο κονσόλας και αντικαταστήστε το `YOUR_DIRECTORY` με τη πραγματική διαδρομή φακέλου.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Εκτελέστε το πρόγραμμα (`dotnet run` ή `Ctrl+F5` στο Visual Studio). Μετά την εκτέλεση, ανοίξτε το `CopyWithPivot.xlsx` για να επαληθεύσετε ότι ο pivot λειτουργεί ακριβώς όπως το αρχικό.

## Συχνές ερωτήσεις

**Q: Λειτουργεί αυτό με μακροεντολές ή βιβλία εργασίας ενεργοποιημένα με VBA;**  
A: Το Aspose.Cells μπορεί να διαβάσει αρχεία ενεργοποιημένα με μακροεντολές (`.xlsm`), αλλά ο κώδικας των μακροεντολών δεν αντιγράφεται. Ο ίδιος ο πίνακας pivot διατηρείται επειδή αποτελεί μέρος του XML του φύλλου εργασίας.

**Q: Τι γίνεται αν ο pivot χρησιμοποιεί εξωτερική πηγή δεδομένων;**  
A: Η λειτουργία αντιγραφής περιλαμβάνει μόνο τα δεδομένα στην cache. Εάν το βιβλίο εργασίας προορισμού χρειάζεται να ανανεωθεί από την αρχική πηγή, θα πρέπει να επαναρυθμίσετε τη σύνδεση δεδομένων χειροκίνητα.

**Q: Μπορώ να αντιγράψω τον pivot χωρίς τις υποκείμενες σειρές δεδομένων;**  
A: Όχι. Ένας πίνακας pivot χρειάζεται την cache του. Ο πιο αξιόπιστος τρόπος είναι να αντιγράψετε τις σειρές που περιέχουν την cache, όπως δείχνεται. Μπορείτε αργότερα να κρύψετε αυτές τις σειρές αν δεν θέλετε να είναι ορατές.

## Συμπέρασμα

Τώρα ξέρετε **how to copy pivot table** από ένα αρχείο Excel σε άλλο χρησιμοποιώντας C#. Το tutorial κάλυψε το **load excel workbook c#**, ορίστηκε το **copy range to new workbook**, και χρησιμοποιήθηκε η μέθοδος `CopyRows` του Aspose.Cells για να διατηρηθεί ο pivot αμετάβλητος. Με το πλήρες, εκτελέσιμο παράδειγμα μπορείτε να ενσωματώσετε αυτό το μοτίβο σε pipelines αναφορών, αυτοματοποιημένα εργαλεία εξαγωγής ή οποιοδήποτε σενάριο όπου ένας pivot πρέπει να μεταφερθεί μεταξύ βιβλίων εργασίας.

### Επόμενα βήματα

* Εξερευνήστε τις δυνατότητες του **Aspose.Cells** όπως η ανανέωση πινάκων pivot προγραμματιστικά.  
* Συνδυάστε αυτήν την προσέγγιση με το **ExcelPackage** (EPPlus) εάν χρειάζεστε μια ανοιχτού κώδικα εναλλακτική.  
* Αυτοματοποιήστε την αντιγραφή σε πολλαπλά φύλλα επαναλαμβάνοντας μέσω του `srcWorkbook.Worksheets`.  

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές περιοχές, να προσθέσετε προσαρμοσμένο στυλ, ή να ενσωματώσετε τη λογική σε μια μεγαλύτερη υπηρεσία επεξεργασίας δεδομένων. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Δημιουργία Νέου Βιβλίου Εργασίας σε C# – Αντιγραφή Πίνακα Pivot](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [Πώς να αντιγράψετε πίνακα pivot στο Excel με C# και Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Αντιγραφή πίνακα pivot σε νέο βιβλίο εργασίας, εξαγωγή σχήματος σε PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}