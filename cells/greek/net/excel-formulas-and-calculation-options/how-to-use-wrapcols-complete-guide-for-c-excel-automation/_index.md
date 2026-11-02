---
category: general
date: 2026-07-13
description: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# για να μετατρέψετε έναν πίνακα
  σε στήλες, να εφαρμόσετε τύπο πίνακα στο Excel και να δημιουργήσετε πρόγραμματικά
  ένα βιβλίο εργασίας Excel — όλα με σαφή βήματα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert array to columns
- apply array formula excel
- create excel workbook programmatically
- evaluate excel formula c#
language: el
lastmod: 2026-07-13
og_description: Η χρήση του WRAPCOLS σε C# σας επιτρέπει να μετατρέψετε γρήγορα έναν
  πίνακα σε στήλες, να εφαρμόσετε έναν τύπο πίνακα σε στυλ Excel και να αξιολογήσετε
  το αποτέλεσμα προγραμματιστικά.
og_image_alt: Screenshot showing how to use WRAPCOLS formula in a C# generated Excel
  sheet
og_title: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# – Γρήγορη δημιουργία βιβλίου εργασίας
  Excel
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  headline: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  type: TechArticle
- description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  name: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  steps:
  - name: What if I need more than two columns?
    text: 'Just change the second argument of WRAPCOLS. For example, `=WRAPCOLS({1,2,3,4,5,6},3)`
      would produce three columns:'
  - name: Can I feed a dynamic range instead of a hard‑coded array?
    text: 'Absolutely. You can build the array string programmatically:'
  - name: What about error handling?
    text: 'If the formula is malformed, `Calculate()` will throw a `CellsException`.
      Wrap the calculation in a try/catch block and log the error:'
  - name: Does this work with older Excel versions?
    text: WRAPCOLS was introduced in Excel 365/2021. When you save the file as an
      older `.xls` format, the formula may be lost. Stick to `.xlsx` if you need the
      function to survive outside the C# engine.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Πώς να χρησιμοποιήσετε το WRAPCOLS – Πλήρης οδηγός για αυτοματοποίηση Excel
  με C#
url: /el/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το WRAPCOLS – Πλήρης Οδηγός για Αυτοματοποίηση Excel με C#

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το WRAPCOLS** όταν χρειάζεται να μετατρέψετε μια επίπεδη λίστα σε έναν τακτοποιημένο πίνακα μέσα σε ένα αρχείο Excel που δημιουργείται από C#; Δεν είστε ο μόνος. Είτε δημιουργείτε μια μηχανή αναφορών, εξάγετε αποτελέσματα έρευνας, είτε απλώς παίζετε με δεδομένα, η λειτουργία WRAPCOLS μπορεί άμεσα να αναδιαμορφώσει έναν πίνακα σε αριθμό στηλών που καθορίζετε.  

Σε αυτό το σεμινάριο θα περάσουμε από όλη τη διαδικασία: από **τη δημιουργία ενός Excel workbook προγραμματιστικά** μέχρι **την εφαρμογή ενός array formula σε στυλ Excel**, και τελικά **την αξιολόγηση του τύπου με C#**. Στο τέλος θα μπορείτε να **μετατρέψετε έναν πίνακα σε στήλες** με μία μόνο γραμμή κώδικα, χωρίς χειροκίνητες κινήσεις κελιού‑κατά‑κελί.

> **Τι θα πάρετε:** ένα εκτελέσιμο δείγμα κώδικα, εξήγηση κάθε βήματος, συμβουλές για κοινά προβλήματα και προτάσεις για επέκταση της λύσης.

---

## Απαιτούμενα

- .NET 6.0+ (ή οποιοδήποτε πρόσφατο .NET runtime)
- Ένα IDE για C# (Visual Studio, Rider ή VS Code)
- Η βιβλιοθήκη **Aspose.Cells for .NET** (η δωρεάν δοκιμή λειτουργεί) – είναι ο πιο εύκολος τρόπος για να χειριστείτε αρχεία Excel χωρίς να χρειάζεται εγκατεστημένο Excel.
- Βασική εξοικείωση με τη σύνταξη C# και τους τύπους Excel.

Αν προτιμάτε διαφορετική βιβλιοθήκη (π.χ., EPPlus ή ClosedXML), οι βασικές ιδέες παραμένουν ίδιες—απλώς αντικαταστήστε τις κλήσεις API.

## Βήμα 1: Ρυθμίστε το Έργο σας και Προσθέστε τη Βιβλιοθήκη Excel

Πρώτα απ' όλα, δημιουργήστε μια νέα εφαρμογή console και προσθέστε το Aspose.Cells μέσω NuGet:

```bash
dotnet new console -n WrapColsDemo
cd WrapColsDemo
dotnet add package Aspose.Cells
```

> **Συμβουλή:** Χρησιμοποιήστε τη σημαία `--version` για να κλειδώσετε σε μια γνωστή σταθερή έκδοση, π.χ., `Aspose.Cells 24.9`.

Τώρα ανοίξτε το `Program.cs`. Θα ξεκινήσουμε προσθέτοντας τα απαιτούμενα namespaces:

```csharp
using System;
using Aspose.Cells;   // Main API for workbook manipulation
```

Η αναφορά στη βιβλιοθήκη εξασφαλίζει ότι μπορούμε να **δημιουργήσουμε ένα Excel workbook προγραμματιστικά** και να δουλέψουμε με τύπους.

## Βήμα 2: Δημιουργήστε ένα Νέο Workbook και το Στόχο Κελιού

Στη συνέχεια, δημιουργήστε ένα νέο workbook και επιλέξτε το κελί όπου θα βρίσκεται ο τύπος WRAPCOLS. Σε όρους Excel, το κελί **A1** είναι γραμμή 0, στήλη 0.

```csharp
// Step 2.1: Create a new workbook (blank Excel file)
Workbook workbook = new Workbook();

// Step 2.2: Grab the first worksheet (default)
Worksheet sheet = workbook.Worksheets[0];

// Step 2.3: Define the target cell (A1)
Cell targetCell = sheet.Cells[0, 0];
```

Γιατί το κάνουμε αυτό; Το αντικείμενο `Workbook` είναι ο container για όλα τα φύλλα, τα στυλ και τους υπολογισμούς. Αναφέροντας ρητά το κελί, διατηρούμε τον κώδικα σαφή και αποφεύγουμε τα «μαγικά νούμερα» αργότερα.

## Βήμα 3: Εισάγετε τον WRAPCOLS Array Formula

Τώρα έρχεται η καρδιά του σεμιναρίου—**πώς να χρησιμοποιήσετε το WRAPCOLS**. Η συνάρτηση παίρνει έναν πίνακα και έναν αριθμό στηλών, και επιστρέφει μια δισδιάστατη περιοχή. Σε σύνταξη Excel φαίνεται έτσι:

```
=WRAPCOLS({1,2,3,4}, 2)
```

Αυτό λέει στο Excel να οργανώσει τους αριθμούς 1‑4 σε **2 στήλες**, με αποτέλεσμα:

| A | B |
|---|---|
| 1 | 3 |
| 2 | 4 |

Για να ενσωματώσετε αυτόν τον τύπο από C#:

```csharp
// Step 3: Apply the WRAPCOLS array formula to A1
targetCell.Formula = "=WRAPCOLS({1,2,3,4},2)";
```

Παρατηρήστε ότι χρησιμοποιούμε ένα **string** που αντικατοπτρίζει αυτό που θα πληκτρολογούσατε στη γραμμή τύπων του Excel. Αυτό είναι το βήμα **apply array formula excel**, και το Aspose.Cells το αντιμετωπίζει αυτόματα ως τύπο πίνακα επειδή το WRAPCOLS επιστρέφει μια περιοχή.

## Βήμα 4: Εξαναγκάστε τον Υπολογισμό ώστε ο Τύπος να Αξιολογηθεί

Το Excel συνήθως επαναϋπολογίζει αργά—μόνο όταν ανοίγετε το αρχείο. Επειδή θέλουμε να διαβάσουμε το αποτέλεσμα αμέσως, πρέπει να ενεργοποιήσουμε έναν υπολογισμό:

```csharp
// Step 4: Calculate the workbook so the WRAPCOLS formula resolves
workbook.Calculate();
```

Η κλήση του `Calculate()` είναι η ενέργεια **evaluate excel formula c#** που εξαναγκάζει τη μηχανή να υπολογίσει κάθε τύπο, συμπεριλαμβανομένου του WRAPCOLS array. Χωρίς αυτήν την κλήση, το `targetCell.Value` θα ήταν ακόμα `null`.

## Βήμα 5: Ανακτήστε και Επαληθεύστε το Αποτέλεσμα

Τώρα που το workbook έχει υπολογιστεί, μπορούμε να πάρουμε τις τιμές από τα κελιά που κατέλαβε ο πίνακας. Το πάνω‑αριστερό κελί (A1) περιέχει το πρώτο στοιχείο, ενώ τα διπλανά κελιά περιέχουν τα υπόλοιπα. Ας διαβάσουμε ολόκληρο το μπλοκ 2 × 2:

```csharp
// Step 5: Read the evaluated values from the resulting range
object[,] result = targetCell.GetArrayValue() as object[,];

// Simple sanity check: print the 2x2 matrix to console
if (result != null)
{
    for (int r = 0; r < result.GetLength(0); r++)
    {
        for (int c = 0; c < result.GetLength(1); c++)
        {
            Console.Write($"{result[r, c]}\t");
        }
        Console.WriteLine();
    }
}
else
{
    Console.WriteLine("No array result was returned.");
}
```

Όταν εκτελέσετε το πρόγραμμα, η κονσόλα θα πρέπει να εμφανίσει:

```
1   3
2   4
```

Αυτή η έξοδος επιβεβαιώνει ότι μετατρέψαμε επιτυχώς **array to columns** χρησιμοποιώντας το WRAPCOLS.

## Βήμα 6: Αποθηκεύστε το Workbook (Προαιρετικό αλλά Χρήσιμο)

Αν θέλετε να ανοίξετε το αρχείο στο Excel και να δείτε τον τύπο ζωντανά, απλώς αποθηκεύστε το:

```csharp
// Step 6: Persist the workbook to disk (optional)
workbook.Save("WrapColsDemo.xlsx");
Console.WriteLine("Workbook saved as WrapColsDemo.xlsx");
```

Ανοίγοντας το αρχείο θα δείτε τον τύπο WRAPCOLS στο A1 και την γεμισμένη περιοχή 2‑στηλών κάτω από αυτό. Αυτό το βήμα είναι χρήσιμο για εντοπισμό σφαλμάτων ή για παράδοση του αρχείου στους τελικούς χρήστες.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν χρειάζομαι περισσότερες από δύο στήλες;

Απλώς αλλάξτε το δεύτερο όρισμα του WRAPCOLS. Για παράδειγμα, `=WRAPCOLS({1,2,3,4,5,6},3)` θα παράγει τρεις στήλες:

| A | B | C |
|---|---|---|
| 1 | 3 | 5 |
| 2 | 4 | 6 |

Ενημερώστε τη γραμμή C# αναλόγως:

```csharp
targetCell.Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

### Μπορώ να τροφοδοτήσω μια δυναμική περιοχή αντί για σκληροκωδικοποιημένο πίνακα;

Απόλυτα. Μπορείτε να δημιουργήσετε το string του πίνακα προγραμματιστικά:

```csharp
int[] numbers = Enumerable.Range(1, 10).ToArray();
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";
```

Με αυτόν τον τρόπο μπορείτε να **apply array formula excel** εν κινήσει, ιδανικό για αναφορές με μεταβλητό μέγεθος δεδομένων.

### Πώς να χειριστείτε τα σφάλματα;

Αν ο τύπος είναι εσφαλμένος, το `Calculate()` θα ρίξει ένα `CellsException`. Τυλίξτε τον υπολογισμό σε μπλοκ try/catch και καταγράψτε το σφάλμα:

```csharp
try
{
    workbook.Calculate();
}
catch (CellsException ex)
{
    Console.Error.WriteLine($"Formula evaluation failed: {ex.Message}");
}
```

### Λειτουργεί αυτό με παλαιότερες εκδόσεις του Excel;

Το WRAPCOLS εισήχθη στο Excel 365/2021. Όταν αποθηκεύετε το αρχείο σε παλαιότερη μορφή `.xls`, ο τύπος μπορεί να χαθεί. Παραμείνετε στο `.xlsx` αν χρειάζεστε τη λειτουργία να παραμείνει εκτός της μηχανής C#.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα μαζί, εδώ είναι το πλήρες, έτοιμο για αντιγραφή πρόγραμμα:

```csharp
using System;
using System.Linq;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            Cell targetCell = sheet.Cells[0, 0];

            // 2️⃣ Build a dynamic array (optional)
            int[] numbers = Enumerable.Range(1, 8).ToArray(); // {1,2,3,4,5,6,7,8}
            string arrayLiteral = "{" + string.Join(",", numbers) + "}";

            // 3️⃣ Apply WRAPCOLS – convert array to columns (2 columns in this case)
            targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";

            // 4️⃣ Force calculation – evaluate excel formula c#
            try
            {
                workbook.Calculate();
            }
            catch (CellsException ex)
            {
                Console.Error.WriteLine($"Failed to evaluate formula: {ex.Message}");
                return;
            }

            // 5️⃣ Retrieve the 2‑column result
            object[,] result = targetCell.GetArrayValue() as object[,];
            if (result != null)
            {
                Console.WriteLine("WRAPCOLS result:");
                for (int r = 0; r < result.GetLength(0); r++)
                {
                    for (int c = 0; c < result.GetLength(1); c++)
                    {
                        Console.Write($"{result[r, c]}\t");
                    }
                    Console.WriteLine();
                }
            }

            // 6️⃣ Save the file for visual inspection (optional)
            workbook.Save("WrapColsDemo.xlsx");
            Console.WriteLine("\nWorkbook saved as WrapColsDemo.xlsx");
        }
    }
}
```

Εκτελέστε `dotnet run` και θα πρέπει να δείτε τον πίνακα εκτυπωμένο, ακολουθούμενο από μια επιβεβαίωση ότι το αρχείο `.xlsx` υπάρχει.

## Ανακεφαλαίωση & Επόμενα Βήματα

Καλύψαμε **πώς να χρησιμοποιήσετε το WRAPCOLS** για **convert array to columns**, παρουσιάσαμε την τεχνική **apply array formula excel** από C#, εξαναγκάσαμε έναν υπολογισμό για **evaluate excel formula c#**, και αποθηκεύσαμε το αποτέλεσμα για περαιτέρω χρήση.

Αν θέλετε να μάθετε περισσότερα:

- **Δυναμικοί αριθμοί στηλών:** αφήστε τον αριθμό στηλών να είναι μεταβλητή εισόδου χρήστη.
- **Στυλιζάρισμα του αποτελέσματος:** εφαρμόστε γραμματοσειρές, περιγράμματα ή μορφοποίηση υπό όρους μέσω Aspose.Cells μετά τον υπολογισμό.
- **Συνδυασμός με άλλες συναρτήσεις:** ενσωματώστε το WRAPCOLS μέσα σε `LET` ή `FILTER`

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Aspose.Cells .NET: Πώς να Δημιουργήσετε & Στυλιζάρετε Excel Workbooks Προγραμματιστικά](/cells/english/net/formatting/aspose-cells-net-create-style-excel-workbooks/)
- [Πώς να Δημιουργήσετε και να Αποθηκεύσετε ένα Excel Workbook ως ODS Χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Πώς να Δημιουργήσετε Named Ranges περιορισμένα στο Workbook σε Excel Χρησιμοποιώντας Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}