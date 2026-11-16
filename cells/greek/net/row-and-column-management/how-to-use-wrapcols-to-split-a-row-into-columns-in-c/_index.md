---
category: general
date: 2026-11-16
description: Μάθετε πώς να χρησιμοποιείτε το WRAPCOLS σε C# για να χωρίσετε μια γραμμή
  σε στήλες, να αυτοματοποιήσετε ένα βιβλίο εργασίας Excel, να υπολογίσετε τύπους
  και να αποθηκεύσετε το αρχείο Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split row into columns
- automate excel workbook
- excel formula calculation
- save excel file c#
language: el
lastmod: 2026-11-16
og_description: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# για να χωρίσετε μια γραμμή
  σε στήλες, να αυτοματοποιήσετε ένα βιβλίο εργασίας Excel, να εκτελέσετε υπολογισμό
  τύπων και να αποθηκεύσετε το αρχείο Excel.
og_image_alt: Screenshot showing WRAPCOLS function splitting a row into columns in
  an Excel workbook
og_title: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# – διαχωρίστε γραμμές, υπολογίστε
  τύπους και αποθηκεύστε αρχεία Excel
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  headline: How to use WRAPCOLS to split a row into columns in C#
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  name: How to use WRAPCOLS to split a row into columns in C#
  steps:
  - name: How WRAPCOLS works
    text: '* **Source range** – `A1:T1` contains the original 20 values. * **Column
      count** – `5` tells Excel to create five columns per row. * **Result** – Excel
      fills cells `A2:E5` with the wrapped data automatically.'
  - name: Expected output
    text: 'Open `WrapColsDemo.xlsx` and you’ll see:'
  - name: Next steps
    text: '* Explore other dynamic array functions such as `SEQUENCE`, `FILTER`, and
      `UNIQUE` to enrich your Excel automation toolkit. * Combine `WRAPCOLS` with
      chart generation APIs to produce ready‑to‑publish reports. * Integrate the code
      into a background service that processes CSV uploads and outputs resha'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: Πώς να χρησιμοποιήσετε το WRAPCOLS για να χωρίσετε μια γραμμή σε στήλες σε
  C#
url: /el/net/row-and-column-management/how-to-use-wrapcols-to-split-a-row-into-columns-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το WRAPCOLS για να χωρίσετε μια σειρά σε στήλες σε C#

Αν χρειάζεστε **πώς να χρησιμοποιήσετε το WRAPCOLS** σε ένα έργο C#, αυτός ο οδηγός σας δείχνει μια πλήρη, εκτελέσιμη λύση. Θα δείτε πώς να χωρίσετε μια σειρά σε στήλες, να αυτοματοποιήσετε ένα βιβλίο εργασίας Excel, να ενεργοποιήσετε τον υπολογισμό τύπων Excel και, τέλος, να αποθηκεύσετε το αρχείο Excel με τρόπο C#.

Η εργασία με το Excel προγραμματιστικά συχνά σημαίνει διαχείριση μεγάλων συνόλων δεδομένων, και η συνάρτηση `WRAPCOLS` σας επιτρέπει να μετασχηματίσετε μια μοναδική σειρά σε μια μήτρα χωρίς χειροκίνητο βρόχο. Τα παρακάτω βήματα καλύπτουν όλα όσα χρειάζεστε — από τη δημιουργία του βιβλίου εργασίας μέχρι την τελική έξοδο αρχείου — ώστε να ενσωματώσετε την τεχνική σε οποιαδήποτε εφαρμογή .NET.

## Τι καλύπτει αυτό το tutorial

* Δημιουργία νέου βιβλίου εργασίας και πρόσβαση στο πρώτο φύλλο εργασίας.  
* Συμπλήρωση μιας σειράς με διαδοχικές τιμές (1‑20).  
* Εφαρμογή του τύπου Excel `WRAPCOLS` για να χωρίσετε τη σειρά σε μπλοκ 5‑στήλων.  
* Εκτέλεση **excel formula calculation** ώστε το αποτέλεσμα να γίνει μέρος του φύλλου.  
* Χρήση του **save excel file c#** για να γράψετε το βιβλίο εργασίας στο δίσκο.  

Δεν απαιτείται εξωτερική διαμόρφωση πέρα από τη βιβλιοθήκη Aspose.Cells για .NET (ή οποιοδήποτε συμβατό API που υποστηρίζει `WRAPCOLS`). Στο τέλος του οδηγού θα έχετε ένα αρχείο με όνομα `WrapColsDemo.xlsx` που περιέχει τέσσερις σειρές πέντε στηλών η κάθε μία, προερχόμενες από τα αρχικά δεδομένα μιας μόνο σειράς.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core 3.1 και .NET Framework 4.7+).  
* Αναφορά στο **Aspose.Cells** (διαθέσιμο μέσω NuGet: `Install-Package Aspose.Cells`).  
* Βασική εξοικείωση με τη σύνταξη C# και τους τύπους Excel.  

> **Pro tip:** Αν προτιμάτε μια δωρεάν εναλλακτική, η ανοιχτή βιβλιοθήκη EPPlus υποστηρίζει επίσης προσαρμοσμένους τύπους, αλλά το `WRAPCOLS` είναι ενσωματωμένο μόνο σε βιβλιοθήκες που υλοποιούν πλήρως τη μηχανή υπολογισμού του Excel, όπως το Aspose.Cells.

## Βήμα 1: Δημιουργία νέου βιβλίου εργασίας και λήψη του πρώτου φύλλου

Η πρώτη ενέργεια είναι η δημιουργία ενός αντικειμένου `Workbook` και η λήψη του προεπιλεγμένου φύλλου εργασίας. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel στη μνήμη.

```csharp
using Aspose.Cells;

...

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                 // creates an empty workbook
Worksheet sheet = workbook.Worksheets[0];           // the first worksheet (named "Sheet1")
```

Η δημιουργία του βιβλίου εργασίας προγραμματιστικά αποτελεί τη βάση των εργασιών **automate excel workbook**. Η αναφορά `Worksheet` σας επιτρέπει να χειρίζεστε τα κελιά άμεσα.

## Βήμα 2: Συμπλήρωση της πρώτης σειράς με τιμές 1‑20

Στη συνέχεια, γεμίστε τα κελιά `A1` έως `T1` με τους αριθμούς 1 έως 20. Ένας απλός βρόχος `for` γράφει κάθε τιμή στη σωστή στήλη.

```csharp
// Step 2: Fill the first row with values 1‑20
for (int col = 0; col < 20; col++)
{
    sheet.Cells[0, col].PutValue(col + 1);   // Row 0 = first row, column index starts at 0
}
```

Γιατί να γράψετε τις τιμές προγραμματιστικά; Εγγυάται ότι η επίδειξη λειτουργεί σε οποιονδήποτε υπολογιστή χωρίς χειροκίνητη εισαγωγή δεδομένων, κάτι που είναι απαραίτητο όταν **automate excel workbook** δημιουργείται σε μαζικές διεργασίες.

## Βήμα 3: Εφαρμογή της συνάρτησης WRAPCOLS για να χωρίσετε τη σειρά σε μπλοκ 5‑στήλων

Τώρα χρησιμοποιούμε τον τύπο Excel `WRAPCOLS`. Παίρνει μια περιοχή προέλευσης και έναν αριθμό στηλών, και επιστρέφει έναν δισδιάστατο πίνακα που «τυλίγει» τα δεδομένα στην καθορισμένη ποσότητα στηλών.

```csharp
// Step 3: Use the WRAPCOLS function to split the row into 5‑column blocks
sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";
```

Η τοποθέτηση του τύπου στο κελί `A2` λέει στο Excel να ξεκινήσει το αποτέλεσμα στη δεύτερη σειρά. Το αποτέλεσμα θα είναι μια μήτρα 4 × 5 επειδή 20 στοιχεία δια του 5 στηλών δίνουν τέσσερις σειρές.

### Πώς λειτουργεί το WRAPCOLS

* **Περιοχή προέλευσης** – `A1:T1` περιέχει τις αρχικές 20 τιμές.  
* **Αριθμός στηλών** – `5` λέει στο Excel να δημιουργήσει πέντε στήλες ανά σειρά.  
* **Αποτέλεσμα** – Το Excel γεμίζει τα κελιά `A2:E5` με τα τυλιγμένα δεδομένα αυτόματα.

Αν χρειαστεί ποτέ να **split row into columns** με διαφορετικό μέγεθος μπλοκ, απλώς αλλάξτε το δεύτερο όρισμα. Για παράδειγμα, `WRAPCOLS(A1:T1,4)` θα παρήγαγε πέντε σειρές τεσσάρων στηλών η καθεμία.

## Βήμα 4: Υπολογισμός τύπων ώστε το αποτέλεσμα του WRAPCOLS να υλοποιηθεί

Ένας πρόσφατα προστιθέμενος τύπος παραμένει μη αξιολογημένος μέχρι να τρέξει η μηχανή υπολογισμού. Καλώντας το `CalculateFormula()`, εξασφαλίζετε ότι το βήμα **excel formula calculation** γράφει τις πραγματικές τιμές στο φύλλο εργασίας.

```csharp
// Step 4: Calculate formulas so the WRAPCOLS result is materialised
workbook.CalculateFormula();
```

Η εκτέλεση του υπολογισμού είναι κρίσιμη όταν αργότερα **save excel file c#**, επειδή το αποθηκευμένο αρχείο πρέπει να περιέχει τις υπολογισμένες τιμές, όχι μόνο το κείμενο του τύπου. Χωρίς αυτό το βήμα, το βιβλίο εργασίας εξόδου θα έδειχνε `#N/A` ή τον ακατέργαστο τύπο αντί για τους αναμενόμενους αριθμούς.

## Βήμα 5: Αποθήκευση του βιβλίου εργασίας στο δίσκο

Τέλος, αποθηκεύστε το βιβλίο εργασίας χρησιμοποιώντας τη μέθοδο `Save`. Μπορείτε να ορίσετε οποιοδήποτε έγκυρο μονοπάτι αρχείου· το παράδειγμα χρησιμοποιεί έναν φάκελο placeholder που πρέπει να αντικαταστήσετε με το δικό σας.

```csharp
// Step 5: Save the workbook
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "WrapColsDemo.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Η κλήση `Save` επιδεικνύει **save excel file c#** στην πιο απλή της μορφή. Το Aspose.Cells επιλέγει αυτόματα τη μορφή XLSX βάσει της επέκτασης του αρχείου. Αν χρειάζεστε παλαιότερο αρχείο `.xls`, αλλάξτε την επέκταση αναλόγως.

### Αναμενόμενη έξοδος

Ανοίξτε το `WrapColsDemo.xlsx` και θα δείτε:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 |10 |
|11 |12 |13 |14 |15 |
|16 |17 |18 |19 |20 |

Η αρχική μοναδική σειρά έχει **split row into columns** σε τέσσερις σειρές, η καθεμία με πέντε στήλες.

## Πλήρης κώδικας

Συνδυάζοντας όλα τα βήματα παίρνουμε ένα σύντομο, αυτόνομο πρόγραμμα:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 1: Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Fill first row with values 1‑20
        for (int col = 0; col < 20; col++)
        {
            sheet.Cells[0, col].PutValue(col + 1);
        }

        // Step 3: Apply WRAPCOLS to split into 5‑column blocks
        sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";

        // Step 4: Force calculation so values are materialised
        workbook.CalculateFormula();

        // Step 5: Save the workbook (change the path as needed)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "WrapColsDemo.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Αντιγράψτε τον κώδικα σε ένα νέο έργο console, επαναφέρετε το πακέτο NuGet Aspose.Cells και τρέξτε. Το πρόγραμμα δημιουργεί το αρχείο Excel στην επιφάνεια εργασίας σας σε δευτερόλεπτα.

## Συνηθισμένες παραλλαγές και περιπτώσεις άκρων

| Κατάσταση | Προσαρμογή |
|-----------|------------|
| **Διαφορετικό μέγεθος μπλοκ** | Αλλάξτε `WRAPCOLS(A1:T1,5)` σε `WRAPCOLS(A1:T1, n)` όπου `n` είναι ο επιθυμητός αριθμός στηλών. |
| **Πολλαπλές σειρές προέλευσης** | Χρησιμοποιήστε `WRAPCOLS(A1:A10,5)` για να τυλίξετε μια κάθετη περιοχή σε μήτρα 5‑στήλων. |
| **Δυναμική περιοχή προέλευσης** | Δημιουργήστε το string διεύθυνσης σε C# (`$"A1:{CellIndexToName(0, lastCol)}1"`) πριν αναθέσετε τον τύπο. |
| **Μεγάλα φύλλα εργασίας** | Καλέστε `workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` για να παραλείψετε κελιά που προκαλούν σφάλματα και να βελτιώσετε την απόδοση. |
| **Αποθήκευση ως CSV** | Αντικαταστήστε `workbook.Save(outputPath)` με `workbook.Save(outputPath, SaveFormat.Csv)`. |

Αυτές οι παραλλαγές δείχνουν ότι το ίδιο **how to use wrapcols** μοτίβο μπορεί να προσαρμοστεί σε πολλές περιπτώσεις μετασχηματισμού δεδομένων.

## Συμβουλές αντιμετώπισης προβλημάτων

* **Ο τύπος δεν αξιολογείται** – Βεβαιωθείτε ότι καλείτε `workbook.CalculateFormula()` *μετά* την ανάθεση του τύπου. Η παράλειψη αυτού του βήματος αφήνει το κελί με το ακατέργαστο κείμενο `WRAPCOLS`.  
* **Άρνηση πρόσβασης στο αρχείο** – Ελέγξτε ότι ο φάκελος προορισμού υπάρχει και ότι η διαδικασία σας έχει δικαιώματα εγγραφής. Η χρήση του `Environment.SpecialFolder.Desktop` αποφεύγει τα περισσότερα προβλήματα δικαιωμάτων.  
* **Λανθασμένος αριθμός σειρών** – Επαληθεύστε το δεύτερο όρισμα του `WRAPCOLS`. Ορίζει τον αριθμό στηλών, όχι των σειρών· οι σειρές προκύπτουν από το σύνολο των κελιών προέλευσης διαιρεμένο με αυτόν τον αριθμό στηλών.

## Συμπέρασμα

Τώρα ξέρετε **πώς να χρησιμοποιήσετε το WRAPCOLS** σε C# για να **split row into columns**, να δημιουργήσετε πλήρως **automate excel workbook**, να εκτελέσετε **excel formula calculation**, και να **save excel file c#** με έναν καθαρό κώδικα. Αυτή η τεχνική εξαλείφει τις χειροκίνητες λειτουργίες αντιγραφής‑επικόλλησης και κλιμακώνεται άψογα για μεγάλες διαδρομές μετασχηματισμού δεδομένων.

### Επόμενα βήματα

* Εξερευνήστε άλλες δυναμικές συναρτήσεις όπως `SEQUENCE`, `FILTER` και `UNIQUE` για να εμπλουτίσετε το εργαλείο αυτοματοποίησης Excel.  
* Συνδυάστε το `WRAPCOLS` με API δημιουργίας γραφημάτων για να παράγετε έτοιμες προς δημοσίευση αναφορές.  
* Ενσωματώστε τον κώδικα σε μια υπηρεσία παρασκηνίου που επεξεργάζεται ανεβάσματα CSV και εξάγει μετασχηματισμένα αρχεία Excel για downstream analytics.

Μη διστάσετε να πειραματιστείτε με διαφορετικές περιοχές προέλευσης και αριθμούς στηλών — προσαρμόστε τον τύπο, ξανατρέξτε τον υπολογισμό, και παρακολουθήστε την άμεση ενημέρωση του βιβλίου εργασίας. Καλό κώδικα!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές του παρόντος οδηγού. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}