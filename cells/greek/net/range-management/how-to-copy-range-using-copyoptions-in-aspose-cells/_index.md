---
category: general
date: 2026-11-19
description: Μάθετε πώς να αντιγράψετε μια περιοχή χρησιμοποιώντας το CopyOptions
  στο Aspose.Cells, διατηρώντας τη μορφοποίηση και τους πίνακες Pivot κατά την αντιγραφή
  μιας περιοχής Excel με μορφοποίηση.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: el
lastmod: 2026-11-19
og_description: Η αντιγραφή περιοχής χρησιμοποιώντας το CopyOptions στο Aspose.Cells
  σας επιτρέπει να αντιγράψετε δεδομένα Excel με πλήρη μορφοποίηση και διατηρημένους
  πίνακες Pivot, εξασφαλίζοντας αξιόπιστη διαχείριση του βιβλίου εργασίας.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Αντιγραφή περιοχής χρησιμοποιώντας το CopyOptions στο Aspose.Cells – οδηγός
  βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να αντιγράψετε περιοχή χρησιμοποιώντας το CopyOptions στο Aspose.Cells
url: /el/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε περιοχή χρησιμοποιώντας CopyOptions στο Aspose.Cells

Εάν χρειάζεστε **αντιγραφή περιοχής χρησιμοποιώντας CopyOptions** στο Aspose.Cells, αυτός ο οδηγός σας δείχνει ακριβώς πώς να αντιγράψετε ένα μπλοκ κελιών διατηρώντας όλη τη μορφοποίηση και τους ενσωματωμένους πίνακες Pivot. Πολλοί προγραμματιστές αντιμετωπίζουν δυσκολίες στη διατήρηση του στυλ όταν μετακινούν δεδομένα μεταξύ φύλλων εργασίας, και η κλάση `CopyOptions` λύνει αυτό το πρόβλημα χωρίς επιπλέον χειροκίνητα βήματα.

Σε αυτό το tutorial θα μάθετε να:

* Ορίζετε περιοχές προέλευσης και προορισμού σε ένα βιβλίο εργασίας Excel.  
* Χρησιμοποιείτε το `CopyOptions` για να διατηρήσετε τη μορφοποίηση των κελιών, το πλάτος των στηλών και τους πίνακες Pivot.  
* Αποθηκεύετε το αποτέλεσμα σε νέο αρχείο έτοιμο για επεξεργασία downstream.

Το παράδειγμα λειτουργεί με οποιοδήποτε αρχείο `.xlsx` και απαιτεί μόνο τη βιβλιοθήκη Aspose.Cells for .NET.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερη έκδοση εγκατεστημένη.  
* Ένα έγκυρο license του Aspose.Cells for .NET (ή ένα δωρεάν κλειδί αξιολόγησης).  
* Visual Studio 2022 ή οποιοδήποτε IDE C# προτιμάτε.  

Δεν απαιτούνται επιπλέον πακέτα NuGet εκτός από το `Aspose.Cells`.

## Βήμα 1: Ρύθμιση του έργου και εισαγωγή namespaces

Δημιουργήστε μια νέα εφαρμογή console και προσθέστε την αναφορά Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

Η οδηγία `using Aspose.Cells;` σας δίνει πρόσβαση στα `Workbook`, `CellArea` και `CopyOptions`.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας που θέλετε να τροποποιήσετε

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Το `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel. Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το αρχείο προέλευσης.

## Βήμα 3: Ορισμός των περιοχών προέλευσης και προορισμού

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

Η μέθοδος `CellArea.CreateCellArea` δημιουργεί μια ορθογώνια περιοχή βάσει των διευθύνσεων του πάνω‑αριστερού και κάτω‑δεξιού κελιού. Μπορείτε να προσαρμόσετε τις συντεταγμένες ώστε να ταιριάζουν στο μέγεθος του μπλοκ που θέλετε να αντιγράψετε.

## Βήμα 4: Αντιγραφή της περιοχής διατηρώντας τη μορφοποίηση και τους πίνακες Pivot

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

Το αντικείμενο `CopyOptions` λέει στο Aspose.Cells ακριβώς τι πρέπει να διατηρήσει. Ορίζοντας `CopyPivotTables = true` είναι το κλειδί για **αντιγραφή περιοχής χρησιμοποιώντας CopyOptions** όταν η πηγή περιλαμβάνει πίνακες Pivot. Οι υπόλοιπες σημαίες εξασφαλίζουν ότι **copy excel range with formatting** επιτυγχάνεται αυτόματα—δεν απαιτείται επιπλέον κώδικας για επανεφαρμογή στυλ μετά την αντιγραφή.

### Γιατί είναι σημαντικό το `CopyOptions`

* **Απόδοση** – Η βιβλιοθήκη εκτελεί μια εσωτερική λειτουργία αντί να αντιγράφει τα κελιά ένα‑προς‑ένα.  
* **Ακρίβεια** – Όλες οι οπτικές πτυχές (γραμματοσειρές, χρώματα, περιγράμματα) παραμένουν, εξαλείφοντας την οπτική απόκλιση σε παραγόμενες αναφορές.  
* **Αξιοπιστία** – Οι πίνακες Pivot παραμένουν λειτουργικοί επειδή η κρυφή μνήμη και οι αναφορές προέλευσης αντιγράφονται.

## Βήμα 5: Αποθήκευση του τροποποιημένου βιβλίου εργασίας

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Μετά την κλήση του `Save`, το αρχείο `output.xlsx` περιέχει τα αρχικά δεδομένα συν το αντιγραμμένο μπλοκ στην τοποθεσία προορισμού, πλήρως μορφοποιημένο και με τους πίνακες Pivot.

## Πλήρης κώδικας πηγής για αναφορά

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Η εκτέλεση αυτού του προγράμματος εμφανίζει:

```
Range copied successfully. Output saved to output.xlsx
```

Ανοίξτε το `output.xlsx` στο Excel – θα δείτε το μπλοκ A1:H30 αντιγραμμένο στο A35:H64, με όλα τα χρώματα κελιών, περιγράμματα, μορφές αριθμών και τυχόν πίνακες Pivot αμετάβλητα.

## Συχνές ερωτήσεις και διαχείριση ειδικών περιπτώσεων

### Τι γίνεται αν η περιοχή προορισμού επικαλύπτεται με την πηγή;

Το Aspose.Cells ρίχνει `ArgumentException`. Για να το αποφύγετε, υπολογίστε έναν προορισμό που δεν τέμνει την πηγή ή αντιγράψτε σε διαφορετικό φύλλο εργασίας:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Πώς να αντιγράψετε μεταξύ διαφορετικών βιβλίων εργασίας;

Δημιουργήστε μια δεύτερη παρουσία `Workbook` για το αρχείο προορισμού και χρησιμοποιήστε το ίδιο αντικείμενο `CopyOptions`:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### Αντιγράφει το `CopyOptions` επίσης συγχωνευμένα κελιά;

Ναι. Η σημαία `CopyStyle` περιλαμβάνει πληροφορίες συγχωνευμένων κελιών. Αν χρειάζεστε πιο λεπτομερή έλεγχο, ορίστε `options.CopyMergedCells = true` (διαθέσιμο σε νεότερες εκδόσεις).

### Τι γίνεται με μεγάλες περιοχές (χιλιάδες γραμμές);

Η λειτουργία είναι αποδοτική σε μνήμη, αλλά μπορεί να θέλετε να αυξήσετε το `WorkbookSettings` `MemorySetting` σε `MemorySetting.MemoryPreference` για πολύ μεγάλα αρχεία.

## Pro tips

* **Επαναχρησιμοποίηση του ίδιου αντικειμένου `CopyOptions`** για πολλαπλές αντιγραφές – μειώνει το κόστος δημιουργίας αντικειμένων.  
* **Επικύρωση περιοχών** πριν από την αντιγραφή: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` βοηθά στον εντοπισμό λαθών πληκτρολόγησης νωρίς.  
* **Απενεργοποίηση υπολογισμών** (`workbook.Settings.CalcMode = CalculationMode.Manual`) κατά την αντιγραφή μεγάλων συνόλων δεδομένων για ταχύτερη εκτέλεση, και μετά την αντιγραφή καλέστε `workbook.CalculateFormula()` αν χρειάζεστε ενημερωμένα αποτελέσματα.

## Συμπέρασμα

Τώρα ξέρετε πώς να **αντιγράψετε περιοχή χρησιμοποιώντας CopyOptions** στο Aspose.Cells, επιτυγχάνοντας πλήρη **copy excel range with formatting** ενώ διατηρείτε πίνακες Pivot και άλλες προχωρημένες λειτουργίες. Αυτή η προσέγγιση εξαλείφει την ανάγκη χειροκίνητης επαναεφαρμογής στυλ και διασφαλίζει ότι η αυτοματοποίηση Excel παραμένει αξιόπιστη και συντηρήσιμη.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

* Χρησιμοποιήστε το `CopyOptions` για αντιγραφή ολόκληρων φύλλων εργασίας.  
* Συνδυάστε την ενέργεια αντιγραφής με `WorksheetCollection.AddCopy` για δημιουργία αναφορών βάσει προτύπων.  
* Ενσωματώστε τον κώδικα σε ένα ASP.NET Core API για παροχή μετασχηματισμών Excel σε πραγματικό χρόνο.

Μη διστάσετε να πειραματιστείτε με διαφορετικές συντεταγμένες πηγής/προορισμού και να μοιραστείτε τα αποτελέσματά σας στα σχόλια!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}