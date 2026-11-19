---
category: general
date: 2026-11-19
description: Πώς να χρησιμοποιήσετε το wrapcols σε C# για την αναδίπλωση δεδομένων
  στο Excel και τον γρήγορο υπολογισμό τύπων Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- calculate excel formulas
- wrap data in excel
- save excel file c#
- load excel workbook c#
language: el
lastmod: 2026-11-19
og_description: Πώς να χρησιμοποιήσετε το wrapcols σε C# για την περιτύλιξη δεδομένων
  στο Excel. Μάθετε πώς να υπολογίζετε τύπους του Excel και να αποθηκεύετε το βιβλίο
  εργασίας προγραμματιστικά.
og_image_alt: Screenshot showing wrapped data in an Excel worksheet after applying
  WRAPCOLS
og_title: Πώς να χρησιμοποιήσετε το wrapcols σε C# – περιτύλιξη δεδομένων στο Excel
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to use wrapcols in C# to wrap data in Excel and calculate Excel
    formulas quickly.
  headline: How to use wrapcols in C# to wrap data in Excel
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Data Wrapping
title: Πώς να χρησιμοποιήσετε το wrapcols σε C# για την αναδίπλωση δεδομένων στο Excel
url: /el/net/formatting-rows-and-columns-in-excel/how-to-use-wrapcols-in-c-to-wrap-data-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το wrapcols σε C# για να αναδιπλώσετε δεδομένα στο Excel

Αν χρειάζεστε **how to use wrapcols** για να αναδιοργανώσετε μια κάθετη λίστα σε πολλές στήλες, αυτός ο οδηγός σας δείχνει τα ακριβή βήματα. Θα μάθετε επίσης πώς να **calculate Excel formulas** ώστε το αποτέλεσμα να αποθηκεύεται στο αρχείο που θα αποθηκεύσετε.

Η εργασία με το Excel από C# συχνά ξεκινά με τη φόρτωση ενός βιβλίου εργασίας, την εφαρμογή τύπων και, τέλος, τη διατήρηση των αλλαγών. Αυτός ο οδηγός καλύπτει όλα αυτά τα στάδια ενώ διατηρεί τον κώδικα εύκολο για αντιγραφή‑επικόλληση στο δικό σας έργο.

## Τι θα πετύχετε

* Φορτώστε ένα υπάρχον αρχείο `.xlsx` από το δίσκο (**load excel workbook c#**).
* Εφαρμόστε τη συνάρτηση `WRAPCOLS` σε μια περιοχή, με αποτέλεσμα να **wrap data in Excel**.
* Εξαναγκάστε τη μηχανή να αξιολογήσει τον τύπο (**calculate Excel formulas**).
* Αποθηκεύστε το τροποποιημένο βιβλίο εργασίας (**save Excel file c#**).

Η μόνη προαπαιτούμενη προϋπόθεση είναι μια αναφορά στο **Aspose.Cells for .NET** (ή οποιαδήποτε βιβλιοθήκη που υποστηρίζει τη συνάρτηση `WRAPCOLS`). Ο κώδικας λειτουργεί με .NET 6+ και Visual Studio 2022, αλλά οποιοδήποτε IDE C# αρκεί.

## Πώς να χρησιμοποιήσετε το wrapcols με το Aspose.Cells

Η συνάρτηση φύλλου εργασίας `WRAPCOLS` λαμβάνει μια μονοδιάστατη περιοχή και επιστρέφει έναν δισδιάστατο πίνακα που γεμίζει τον καθορισμένο αριθμό στηλών. Το Aspose.Cells αξιολογεί τη συνάρτηση όπως το Excel, ώστε να μπορείτε να τη χρησιμοποιήσετε άμεσα σε τύπο κελιού.

```csharp
using System;
using Aspose.Cells;          // Install-Package Aspose.Cells via NuGet

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook and get the first worksheet
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.Worksheets[0];

        // Step 2: Write the WRAPCOLS formula into a cell
        // This wraps the values from A2:A10 into 3 columns, starting at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Step 3: Force calculation so the result becomes a static range
        wb.CalculateFormula();

        // Step 4: Save the workbook so you can open it in Excel
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);

        Console.WriteLine("Workbook saved to " + outputPath);
    }
}
```

### Γιατί κάθε γραμμή έχει σημασία

* **Loading the workbook** σας παρέχει ένα ενεργό μοντέλο αντικειμένων που αντικατοπτρίζει το αρχείο Excel στο δίσκο.  
* **Assigning the formula** στο `A1` λέει στο Excel (ή στο Aspose.Cells) να αντιμετωπίσει την περιοχή ως δυναμικό πίνακα.  
* `CalculateFormula()` ενεργοποιεί τη μηχανή υπολογισμού· χωρίς αυτό, ο τύπος θα παραμείνει αμη αξιολογημένος μέχρι να ανοίξει το αρχείο στο Excel.  
* **Saving** γράφει τις υπολογισμένες τιμές πίσω σε ένα νέο αρχείο, καθιστώντας τα αναδιπλωμένα δεδομένα ορατά σε όποιον ανοίξει το βιβλίο εργασίας.

## Υπολογισμός τύπων Excel προγραμματιστικά

Η κλήση του `Workbook.CalculateFormula()` είναι ο συνιστώμενος τρόπος για **calculate Excel formulas** όταν χρειάζεστε τα αποτελέσματα άμεσα. Η μέθοδος σέβεται όλες τις ενσωματωμένες συναρτήσεις, τις προσαρμοσμένες συναρτήσεις χρήστη και τυχόν εξωτερικές αναφορές που έχουν ήδη επιλυθεί.

Αν έχετε πολλαπλά φύλλα εργασίας που εξαρτώνται το ένα από το άλλο, μπορείτε επίσης να περάσετε ένα αντικείμενο `CalculationOptions` για να ελέγξετε τα όρια επανάληψης ή να ενεργοποιήσετε τον πολυνηματικό υπολογισμό:

```csharp
var options = new CalculationOptions
{
    // Enable iterative calculation for circular references
    IterativeCalculation = true,
    MaxIterations = 100,
    // Use all available CPU cores
    EnableMultiThreadedCalculation = true
};

wb.CalculateFormula(options);
```

Αυτό το επιπλέον βήμα είναι προαιρετικό για το απλό παράδειγμα `WRAPCOLS`, αλλά γίνεται απαραίτητο σε μεγαλύτερα βιβλία εργασίας όπου η απόδοση μετρά.

## Αποθήκευση αρχείου Excel C# μετά την αναδίπλωση δεδομένων

Η κλήση του `Workbook.Save()` γράφει ολόκληρο το βιβλίο εργασίας, συμπεριλαμβανομένου του νέου υλοποιημένου πίνακα που παράγεται από το `WRAPCOLS`. Μπορείτε να επιλέξετε οποιαδήποτε από τις υποστηριζόμενες μορφές (`.xlsx`, `.xls`, `.csv`, κ.λπ.):

```csharp
// Save as a standard XLSX file (default)
wb.Save(@"YOUR_DIRECTORY\wrapped.xlsx");

// Save as CSV – only the active sheet is exported
wb.Save(@"YOUR_DIRECTORY\wrapped.csv", SaveFormat.Csv);
```

Το βήμα **save Excel file c#** εγγυάται ότι τα αναδιπλωμένα δεδομένα παραμένουν, ώστε την επόμενη φορά που κάποιος ανοίξει το αρχείο να δει έναν στατικό πίνακα αντί για τύπο.

## Φόρτωση βιβλίου εργασίας Excel C# και προετοιμασία φύλλου εργασίας

Αν το αρχείο προέλευσης δεν περιέχει ήδη τα δεδομένα που θέλετε να αναδιπλώσετε, μπορείτε να το δημιουργήσετε επί τόπου:

```csharp
// Create a new workbook with a single worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Populate column A with sample values
for (int i = 0; i < 9; i++)
{
    ws.Cells[i + 2, 0].PutValue($"Item {i + 1}");
}
```

Αυτό το απόσπασμα δείχνει **load excel workbook c#** με την έννοια ότι μπορείτε να ξεκινήσετε από ένα κενό βιβλίο εργασίας, να το γεμίσετε και στη συνέχεια να εφαρμόσετε το `WRAPCOLS`. Το ίδιο μοτίβο λειτουργεί όταν χρειάζεται να εισάγετε δεδομένα από μια βάση δεδομένων ή ένα αρχείο CSV πριν την αναδίπλωση.

## Συμβουλή: επαλήθευση του αποτελέσματος χωρίς άνοιγμα του Excel

Μετά την αποθήκευση, μπορείτε προγραμματιστικά να διαβάσετε ξανά την αναδιπλωμένη περιοχή για να επιβεβαιώσετε ότι η λειτουργία πέτυχε:

```csharp
// Reload the saved file
Workbook checkWb = new Workbook(@"YOUR_DIRECTORY\output.xlsx");
Worksheet checkWs = checkWb.Worksheets[0];

// Print the first three rows of the wrapped area
for (int row = 0; row < 3; row++)
{
    for (int col = 0; col < 3; col++)
    {
        Console.Write($"{checkWs.Cells[row, col].StringValue}\t");
    }
    Console.WriteLine();
}
```

Η κονσόλα θα πρέπει να εμφανίσει την αρχική λίστα χωρισμένη σε τρεις στήλες, επιβεβαιώνοντας ότι το **wrap data in excel** λειτούργησε όπως αναμενόταν.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

| Question | Answer |
|----------|--------|
| *Τι γίνεται αν η πηγή έχει περισσότερες γραμμές από ό,τι μπορεί να γεμίσει το `WRAPCOLS`;* | Η συνάρτηση συνεχίζει να δημιουργεί νέες γραμμές όπως απαιτείται. Ο αριθμός των στηλών παραμένει σταθερός. |
| *Μπορώ να αναδιπλώσω σε διαφορετικό αριθμό στηλών;* | Ναι—αλλάξτε το δεύτερο όρισμα, π.χ., `=WRAPCOLS(A2:A10,5)` για πέντε στήλες. |
| *Πρέπει να διαγράψω τον τύπο μετά τον υπολογισμό;* | Όχι αν καλέσετε `CalculateFormula()`. Η συνάρτηση επιστρέφει έναν στατικό πίνακα, αλλά ο τύπος παραμένει στο κελί. Αν θέλετε μόνο την τιμή, αντιγράψτε την περιοχή και επικολλήστε‑τιμές πάνω της. |
| *Θα λειτουργήσει αυτό με παλαιότερα αρχεία `.xls`;* | `WRAPCOLS` είναι μια συνάρτηση δυναμικού πίνακα που εισήχθη στο Excel 365. Παλαιότερες μορφές αρχείων που δεν υποστηρίζουν δυναμικούς πίνακες θα αποθηκεύσουν τον τύπο αλλά μπορεί να μην εμφανίσουν σωστά το αναδιπλωμένο αποτέλεσμα. Χρησιμοποιήστε `.xlsx` για αξιόπιστη συμπεριφορά. |

## Συμπέρασμα

Τώρα γνωρίζετε **how to use wrapcols** σε C# για **wrap data in Excel**, πώς να **calculate Excel formulas** εν κινήσει, και πώς να **save Excel file C#** μετά τον μετασχηματισμό. Το πλήρες παράδειγμα δείχνει τη φόρτωση ενός βιβλίου εργασίας, την εφαρμογή της συνάρτησης `WRAPCOLS`, την εξαναγκασμένη εκτίμηση και τη διατήρηση του αποτελέσματος.

### Επόμενα βήματα

* Εξερευνήστε άλλες συναρτήσεις δυναμικού πίνακα όπως `UNWRAPCOLS` ή `SEQUENCE`.
* Χρησιμοποιήστε το **Aspose.Cells** για εισαγωγή δεδομένων από βάση δεδομένων και στη συνέχεια αναδιπλώστε τα αυτόματα.
* Συνδυάστε το `WRAPCOLS` με μορφοποίηση υπό όρους για να επισημάνετε συγκεκριμένες γραμμές μετά την αναδίπλωση.

Μη διστάσετε να πειραματιστείτε με διαφορετικές πηγές περιοχών, αριθμούς στηλών και μορφές εξόδου. Αν αντιμετωπίσετε προβλήματα, η επανεξέταση του βήματος **calculate Excel formulas** ή ο έλεγχος των ρυθμίσεων υπολογισμού του βιβλίου εργασίας συνήθως τα επιλύει.

*Εικόνα: ![Screenshot of wrapped data in Excel](/images/wrapcols-example.png){.align-center alt="Στιγμιότυπο οθόνης που δείχνει τα αναδιπλωμένα δεδομένα σε ένα φύλλο εργασίας Excel μετά την εφαρμογή του WRAPCOLS"}*

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# για πίνακες Excel και αποθήκευση βιβλίου εργασίας](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-for-excel-arrays-and-workbook-savin/)
- [Πώς να δημιουργήσετε βιβλίο εργασίας Excel και να χωρίσετε δεδομένα με το WRAPCOLS σε C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}