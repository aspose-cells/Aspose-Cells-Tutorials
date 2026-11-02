---
category: general
date: 2026-10-10
description: Δημιουργήστε βιβλίο εργασίας Excel σε C# και χρησιμοποιήστε τη συνάρτηση
  WRAPCOLS για να χωρίσετε τα δεδομένα του πίνακα σε στήλες. Ακολουθήστε έναν πλήρη
  οδηγό βήμα‑προς‑βήμα με εκτελέσιμο κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: el
lastmod: 2026-10-10
og_description: Δημιουργήστε βιβλίο εργασίας Excel σε C# και εφαρμόστε τη λειτουργία
  WRAPCOLS για να χωρίσετε δεδομένα πίνακα σε στήλες. Αυτός ο οδηγός παρουσιάζει τον
  πλήρη κώδικα και εξηγεί κάθε βήμα.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Δημιουργία βιβλίου εργασίας Excel και διαχωρισμός δεδομένων με WRAPCOLS
  σε C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel και να χωρίσετε δεδομένα με
  το WRAPCOLS σε C#
url: /el/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε βιβλίο εργασίας Excel και να χωρίσετε δεδομένα με WRAPCOLS σε C#

Αν χρειάζεστε να **δημιουργήσετε βιβλίο εργασίας Excel** προγραμματιστικά, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε και πώς να **χωρίσετε δεδομένα πίνακα** σε στήλες χρησιμοποιώντας τη συνάρτηση `WRAPCOLS`. Θα λάβετε ένα πλήρες, εκτελέσιμο παράδειγμα που παράγει ένα αρχείο `.xlsx` με τα δεδομένα κατανεμημένα σε τρεις στήλες.

Το tutorial καλύπτει όλα όσα χρειάζεστε: τα απαιτούμενα πακέτα NuGet, κάθε γραμμή κώδικα, γιατί λειτουργεί ο τύπος `WRAPCOLS`, και πώς να προσαρμόσετε τη λύση για διαφορετικά μεγέθη πίνακα ή αριθμούς στηλών. Στο τέλος θα μπορείτε να ενσωματώσετε την τεχνική **χρήσης της συνάρτησης wrapcols** σε οποιοδήποτε έργο C# που δημιουργεί αρχεία Excel.

## Προαπαιτούμενα

* .NET 6.0 SDK ή νεότερο εγκατεστημένο  
* Ένα IDE C# (Visual Studio, VS Code, Rider, κ.λπ.)  
* Το πακέτο NuGet **Aspose.Cells for .NET** – η βιβλιοθήκη που παρέχει την κλάση `Workbook` που χρησιμοποιείται στα παραδείγματα  

Δεν χρειάζεστε εγκατάσταση του Office· το Aspose.Cells γράφει το αρχείο `.xlsx` απευθείας.

## Βήμα 1 – δημιουργία βιβλίου εργασίας Excel

Η πρώτη εργασία είναι η δημιουργία ενός νέου αντικειμένου βιβλίου εργασίας και η λήψη αναφοράς στο πρώτο φύλλο εργασίας. Αυτό το βήμα αποτελεί τη βάση για οποιαδήποτε περαιτέρω επεξεργασία.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` αντιπροσωπεύει ολόκληρο το αρχείο, ενώ `Worksheet` αντιπροσωπεύει ένα μόνο φύλλο. Δημιουργώντας το βιβλίο εργασίας στη μνήμη αποφεύγετε τις ενέργειες I/O στο δίσκο μέχρι να το αποθηκεύσετε ρητά.

## Βήμα 2 – εφαρμογή WRAPCOLS για διαίρεση στηλών πίνακα

Τώρα θα τοποθετήσετε έναν τύπο στο κελί **A1** που χρησιμοποιεί το `WRAPCOLS`. Η συνάρτηση λαμβάνει δύο ορίσματα: τον πηγαίο πίνακα και τον αριθμό των στηλών στις οποίες θέλετε να τοποθετηθεί ο πίνακας.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Γιατί λειτουργεί:** Το `WRAPCOLS` παίρνει τον επίπεδο πίνακα `{1,2,3,4,5,6}` και γεμίζει το φύλλο εργασίας γραμμή‑με‑γραμμή, δημιουργώντας τρεις στήλες ανά γραμμή. Το πρώτο όρισμα μπορεί να είναι οποιοδήποτε λεκτικό πίνακα Excel, ένα ονομασμένο εύρος ή ένας δυναμικός τύπος πίνακα. Το δεύτερο όρισμα (`3`) λέει στο Excel πόσες στήλες να δημιουργήσει πριν προχωρήσει στην επόμενη γραμμή.

### Χρήση της συνάρτησης με διαφορετικούς τύπους δεδομένων

Η συνάρτηση `WRAPCOLS` δεν περιορίζεται μόνο σε αριθμούς. Μπορείτε να χωρίσετε τιμές κειμένου, ημερομηνίες ή μεικτούς τύπους:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Όταν ο πηγαίος πίνακας περιέχει συμβολοσειρές, το Excel αυτόματα αντιμετωπίζει το αποτέλεσμα ως κελιά κειμένου. Αυτή η ευελιξία σας επιτρέπει να **διαχωρίσετε δεδομένα με τύπο Excel** για αναφορές, πίνακες ελέγχου ή εργασίες μετεγκατάστασης δεδομένων.

## Βήμα 3 – υπολογισμός τύπων ώστε το φύλλο εργασίας να γεμίσει

Οι τύποι αποθηκεύονται ως συμβολοσειρές μέχρι να ζητήσετε από το βιβλίο εργασίας να τους αξιολογήσει. Η κλήση του `CalculateFormula` αναγκάζει την αξιολόγηση και γράφει τα αποτελέσματα στα κελιά.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Χωρίς αυτήν την κλήση το αποθηκευμένο αρχείο θα περιείχε μόνο το κείμενο του τύπου, όχι τις υπολογισμένες τιμές. Η μέθοδος λειτουργεί σε όλο το βιβλίο εργασίας, έτσι μπορείτε να τοποθετήσετε επιπλέον τύπους αλλού και όλοι θα επιλυθούν με μία κλήση.

## Βήμα 4 – αποθήκευση του βιβλίου εργασίας για να δείτε το αποτέλεσμα

Τέλος, γράψτε το βιβλίο εργασίας στο δίσκο. Επιλέξτε έναν φάκελο για τον οποίο έχετε δικαίωμα εγγραφής και δώστε στο αρχείο ένα σαφές όνομα.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Όταν ανοίξετε το `output.xlsx` στο Excel (ή σε οποιονδήποτε συμβατό προβολέα), θα δείτε:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Αν χρησιμοποιήσατε το παράδειγμα μεικτού τύπου, οι γραμμές 3‑4 θα περιέχουν το κείμενο και τους αριθμούς αντίστοιχα.

## Προχωρημένες παραλλαγές και διαχείριση ακραίων περιπτώσεων

### Μεταβλητός αριθμός στηλών κατά το χρόνο εκτέλεσης

Συχνά ο αριθμός των στηλών που χρειάζεστε εξαρτάται από την είσοδο του χρήστη. Μπορείτε να δημιουργήσετε τη συμβολοσειρά του τύπου δυναμικά:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Μεγάλοι πίνακες και απόδοση

`WRAPCOLS` μπορεί να διαχειριστεί χιλιάδες στοιχεία, αλλά η αξιολόγηση εξαιρετικά μεγάλων πινάκων σε ένα μόνο κελί μπορεί να αυξήσει το χρόνο υπολογισμού. Αν παρατηρήσετε επιβράδυνση:

* Διαχωρίστε τον πηγαίο πίνακα σε μικρότερα τμήματα και γράψτε κάθε τμήμα σε ξεχωριστό αρχικό κελί.  
* Χρησιμοποιήστε το `WorkbookSettings` για να ενεργοποιήσετε τον πολυνηματικό υπολογισμό:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Διαχείριση κενών κελιών

Αν ο πηγαίος πίνακας περιέχει κενές συμβολοσειρές (`""`) ή τιμές `NULL`, το `WRAPCOLS` εισάγει κενά κελιά, διατηρώντας τη διάταξη των στηλών. Αυτή η συμπεριφορά είναι χρήσιμη όταν χρειάζεστε στήλες κράτησης θέσης για μελλοντική εισαγωγή δεδομένων.

### Χρήση ονομασμένων περιοχών αντί για λεκτικά

Για ευκολία συντήρησης, ορίστε μια ονομασμένη περιοχή που περιέχει τα πηγαία δεδομένα, και στη συνέχεια αναφερθείτε σε αυτήν:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Τώρα ο τύπος διαβάζει δεδομένα από το ίδιο το φύλλο εργασίας, επιτρέποντας το **πώς να χρησιμοποιήσετε το wrapcols** σε δυναμικά σενάρια αναφοράς.

## Συνηθισμένα λάθη και επαγγελματικές συμβουλές

* **Μην παραλείψετε το δεύτερο όρισμα.** Το `WRAPCOLS(array)` χωρίς αριθμό στηλών επιστρέφει μία μόνο στήλη, κάτι που αναιρεί τον σκοπό του διαχωρισμού δεδομένων.  
* **Αποφύγετε το μείγμα διαστάσεων πίνακα.** Ο πηγαίος πίνακας πρέπει να είναι μονοδιάστατος· η παροχή διδιάστατου πίνακα (π.χ., `{ {1,2},{3,4} }`) προκαλεί σφάλμα `#VALUE!`.  
* **Αποθηκεύστε μετά τον υπολογισμό.** Αν καλέσετε `wb.Save` πριν το `CalculateFormula`, το αρχείο θα περιέχει μόνο το κείμενο του τύπου.  
* **Ελέγξτε τα δικαιώματα αρχείου.** Όταν εκτελείτε σε περιορισμένα περιβάλλοντα (π.χ., ASP.NET), βεβαιωθείτε ότι η ταυτότητα της διεργασίας μπορεί να γράψει στον προορισμό.

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε. Περιλαμβάνει όλες τις εισαγωγές, τον χειρισμό σφαλμάτων και τα σχόλια.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Η εκτέλεση του προγράμματος παράγει το `output.xlsx` με τρεις ξεχωριστές περιοχές που δείχνουν **διαχωρισμό δεδομένων με τύπο Excel** χρησιμοποιώντας τη συνάρτηση `WRAPCOLS`.

## Συμπέρασμα

Τώρα ξέρετε πώς να **δημιουργήσετε αρχεία βιβλίου εργασίας Excel** σε C# και πώς να **χρησιμοποιήσετε τη συνάρτηση wrapcols** για να **διαχωρίσετε στήλες πίνακα** αποδοτικά. Τα κύρια βήματα — δημιουργία του `Workbook`, εισαγωγή του τύπου `WRAPCOLS`, υπολογισμός και αποθήκευση — αποτελούν ένα επαναχρησιμοποιήσιμο πρότυπο για οποιαδήποτε εργασία αυτοματοποίησης που απαιτεί κατανομή δεδομένων σε στήλες.

Από εδώ μπορείτε:

* Συνδυάστε το `WRAPCOLS` με άλλες συναρτήσεις δυναμικού πίνακα όπως `FILTER` ή `SORT`.  
* Εξάγετε μεγάλα σύνολα δεδομένων από βάσεις και αφήστε το Excel να διαχειριστεί τη διάταξη αυτόματα.  
* Δημιουργήστε αναφορές που καθορίζονται από τον χρήστη, όπου ο αριθμός των στηλών επιλέγεται μέσω ενός στοιχείου ελέγχου UI.

Πειραματιστείτε με διαφορετικές πηγές πινάκων, αριθμούς στηλών και πρόσθετους τύπους για να επεκτείνετε αυτή τη βάση. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# – Δημιουργία βιβλίου εργασίας Excel με συναρτήσεις περιτύλιξης](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Δημιουργία βιβλίου εργασίας Excel – Μετατροπή πίνακα σε μήτρα με WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Δημιουργία βιβλίου εργασίας Excel C# – Οδηγός βήμα‑βήμα](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}