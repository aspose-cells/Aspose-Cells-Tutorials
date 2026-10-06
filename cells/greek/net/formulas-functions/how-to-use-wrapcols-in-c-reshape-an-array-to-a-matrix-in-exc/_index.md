---
category: general
date: 2026-06-17
description: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# για να μετασχηματίσετε έναν
  πίνακα σε μήτρα, να γράψετε τύπο πίνακα σε ένα κελί και να φορτώσετε υπάρχοντα αρχεία
  Excel με το Aspose.Cells.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- write array formula
- write formula to cell
- load existing excel
language: el
og_description: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# για να μετασχηματίσετε γρήγορα
  έναν πίνακα σε μήτρα, να γράψετε έναν τύπο πίνακα σε ένα κελί και να εργαστείτε
  με υπάρχοντα αρχεία Excel.
og_title: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# – Αναδιαμόρφωση ενός πίνακα σε
  μήτρα
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  headline: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  name: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  steps:
  - name: 'Optional: Write a Dynamic Array Reference'
    text: 'If you prefer to reference a range instead of a hard‑coded list, you can
      use:'
  - name: 1. What if I need a different number of rows?
    text: '`WRAPCOLS` only takes the column count; the row count is inferred. To force
      a specific row count, you can combine it with `WRAPROWS` or pad the source array
      with empty strings.'
  - name: 2. Does WRAPCOLS work with text values?
    text: 'Absolutely. Replace the numbers with quoted strings:'
  - name: 3. Can I apply formatting to the generated matrix?
    text: 'After calculation, you can style the range programmatically:'
  - name: 4. How do I handle very large arrays?
    text: Aspose.Cells can process tens of thousands of elements, but keep an eye
      on memory. If you hit limits, consider writing the data in chunks or using `Workbook.Settings.MemorySetting
      = MemorySetting.MemoryPreference;`.
  type: HowTo
tags:
- excel
- csharp
- aspose.cells
title: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# – Αναδιαμορφώστε έναν πίνακα σε μήτρα
  στο Excel
url: /el/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το WRAPCOLS σε C# – Μετασχηματισμός Πίνακα σε Μήτρα στο Excel

Έχετε αναρωτηθεί **πώς να χρησιμοποιήσετε το WRAPCOLS** για να μετατρέψετε μια επίπεδη λίστα αριθμών σε έναν τακτοποιημένο πίνακα μέσα στο Excel; Δεν είστε μόνοι. Είτε δημιουργείτε ένα εργαλείο αναφορών είτε απλώς παίζετε με δεδομένα, η μετατροπή ενός πίνακα σε μήτρα μπορεί να σας εξοικονομήσει πολύ χρόνο αντιγραφής‑επικόλλησης.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει πώς να **γράψετε έναν τύπο πίνακα σε ένα κελί**, να υπολογίσετε το αποτέλεσμα και ακόμη **να φορτώσετε ένα υπάρχον βιβλίο εργασίας Excel** αν χρειάζεται. Στο τέλος θα έχετε ένα σταθερό, έτοιμο‑για‑αντιγραφή‑επικόλληση snippet που λειτουργεί με την πιο πρόσφατη έκδοση του Aspose.Cells για .NET.

## Τι Θα Μάθετε

- Τον σκοπό της συνάρτησης `WRAPCOLS` και πότε είναι χρήσιμη.  
- Πώς να **μετασχηματίσετε έναν πίνακα σε μήτρα** χρησιμοποιώντας έναν μόνο τύπο.  
- Κώδικας βήμα‑βήμα για **να γράψετε έναν τύπο σε ένα κελί** και να εξαναγκάσετε τον υπολογισμό.  
- Προαιρετικές τεχνικές για **φόρτωση ενός υπάρχοντος αρχείου Excel** πριν την εφαρμογή του τύπου.  
- Συνηθισμένα λάθη και συμβουλές για επέκταση της προσέγγισης σε μεγαλύτερα σύνολα δεδομένων.

Καμία εξωτερική τεκμηρίωση δεν απαιτείται—όλα όσα χρειάζεστε είναι εδώ.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- Aspose.Cells για .NET εγκατεστημένο (`dotnet add package Aspose.Cells`).  
- Βασική κατανόηση της σύνταξης C#· αν μπορείτε να δημιουργήσετε μια εφαρμογή console, είστε έτοιμοι.

> **Pro tip:** Αν χρησιμοποιείτε το Visual Studio, ενεργοποιήστε τους *nullable reference types* (`<Nullable>enable</Nullable>`) για να εντοπίζετε πιθανά σφάλματα null νωρίς.

## Βήμα 1: Ρύθμιση του Έργου και Εισαγωγή Namespaces

Πρώτα, δημιουργήστε ένα νέο project console (ή προσθέστε τον κώδικα σε ένα υπάρχον). Στη συνέχεια προσθέστε τις απαραίτητες οδηγίες `using` ώστε ο μεταγλωττιστής να ξέρει πού βρίσκονται τα `Workbook` και `Worksheet`.

```csharp
using System;
using Aspose.Cells;   // Main library for Excel manipulation

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill in the logic in the next steps
        }
    }
}
```

> **Γιατί είναι σημαντικό:** Η εισαγωγή του `Aspose.Cells` σας δίνει πρόσβαση στη υψηλής απόδοσης μηχανή Excel που αξιολογεί το `WRAPCOLS` χωρίς να χρειάζεται το Excel εγκατεστημένο στο μηχάνημα.

## Βήμα 2: Δημιουργία ή Φόρτωση ενός Workbook

Μπορείτε να ξεκινήσετε από το μηδέν ή να ανοίξετε ένα υπάρχον αρχείο. Το παρακάτω απόσπασμα δείχνει και τις δύο επιλογές· απλώς σχολιάστε αυτή που δεν χρειάζεστε.

```csharp
// Option A – Create a brand‑new workbook
Workbook workbook = new Workbook();   // starts with a single empty worksheet

// Option B – Load an existing Excel file (useful when you have templates)
// string inputPath = @"C:\Data\input.xlsx";
// Workbook workbook = new Workbook(inputPath);
```

> **Edge case:** Αν το αρχείο που φορτώνετε είναι προστατευμένο με κωδικό, περάστε τον κωδικό ως δεύτερο όρισμα: `new Workbook(path, "password")`.

## Βήμα 3: Λήψη του Στόχου Worksheet

Στις περισσότερες περιπτώσεις το πρώτο φύλλο (`Worksheets[0]`) είναι αυτό που θέλετε, αλλά μπορείτε επίσης να αναφερθείτε σε φύλλο με το όνομά του.

```csharp
Worksheet sheet = workbook.Worksheets[0];               // by index
// Worksheet sheet = workbook.Worksheets["DataSheet"]; // by name (if it exists)
```

## Βήμα 4: Γράψτε τον Τύπο WRAPCOLS σε ένα Κελί

Αυτή είναι η καρδιά του tutorial. Το `WRAPCOLS` παίρνει έναν πίνακα και έναν αριθμό στηλών, και στη συνέχεια «χύνεται» τις τιμές κατά γραμμές. Θα τοποθετήσουμε τον τύπο στο **A1** ώστε η μήτρα να ξεκινά στην πάνω‑αριστερή γωνία.

```csharp
// Write the WRAPCOLS formula that turns {1,2,3,4,5,6} into 2 rows × 3 columns
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

> **Τι συμβαίνει;**  
> - Η σύνταξη με αγκύλες `{1,2,3,4,5,6}` δημιουργεί μια ενσωματωμένη σταθερά πίνακα.  
> - Το δεύτερο όρισμα (`3`) λέει στο Excel να δημιουργήσει τρεις στήλες, τυλίγοντας αυτόματα τα υπόλοιπα στοιχεία σε νέες γραμμές.  
> - Επειδή χρησιμοποιούμε Aspose.Cells, ο τύπος αποθηκεύεται ακριβώς όπως θα τον πληκτρολογούσατε στο Excel, και η μηχανή τον αξιολογεί κατ’ ανάγκη.

### Προαιρετικό: Γράψτε μια Αναφορά Δυναμικού Πίνακα

Αν προτιμάτε να αναφέρετε μια περιοχή αντί για μια στατική λίστα, μπορείτε να χρησιμοποιήσετε:

```csharp
// Assume B1:B6 already contains numbers you want to reshape
sheet.Cells["A1"].Formula = "=WRAPCOLS(B1:B6,3)";
```

Με αυτόν τον τρόπο η μήτρα ενημερώνεται αυτόματα όποτε αλλάζει η πηγή.

## Βήμα 5: Εξαναγκάστε τον Υπολογισμό και Αποθηκεύστε το Αποτέλεσμα

Το Aspose.Cells δεν υπολογίζει τύπους μέχρι να το ζητήσετε. Καλώντας το `Calculate()` υλοποιείται το αποτέλεσμα, μετατρέποντας την έξοδο του τύπου σε πραγματικές τιμές κελιών.

```csharp
// Force calculation so the WRAPCOLS output appears in the sheet
workbook.Calculate();

// Save the workbook – adjust the path as needed
string outputPath = @"C:\Data\output.xlsx";
workbook.Save(outputPath);
```

Όταν ανοίξετε το `output.xlsx` στο Excel, θα δείτε:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Αυτό είναι το **αποτέλεσμα μετασχηματισμού πίνακα σε μήτρα** που θέλατε.

## Πλήρες Παράδειγμα Εργασίας

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι ένα έτοιμο‑για‑εκτέλεση πρόγραμμα:

```csharp
using System;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook (or load an existing one)
            Workbook workbook = new Workbook(); // new Workbook(@"C:\Data\input.xlsx");

            // 2️⃣ Get the first worksheet
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ Write the WRAPCOLS formula – reshape {1..6} into 2×3
            sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

            // 4️⃣ Force calculation so the matrix is materialized
            workbook.Calculate();

            // 5️⃣ Save the result
            string outputPath = @"C:\Data\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το `output.xlsx`, και θα δείτε τη μήτρα ακριβώς όπως φαίνεται παραπάνω.

## Συχνές Ερωτήσεις & Παγίδες

### 1. Τι γίνεται αν χρειάζομαι διαφορετικό αριθμό γραμμών;

Το `WRAPCOLS` δέχεται μόνο τον αριθμό στηλών· ο αριθμός γραμμών υπολογίζεται αυτόματα. Για να επιβάλετε συγκεκριμένο αριθμό γραμμών, μπορείτε να το συνδυάσετε με το `WRAPROWS` ή να συμπληρώσετε τον αρχικό πίνακα με κενές συμβολοσειρές.

```csharp
// Example: Force 3 rows, 2 columns (will add blanks if needed)
sheet.Cells["A1"].Formula = "=WRAPROWS({1,2,3,4,5,6},3)";
```

### 2. Λειτουργεί το WRAPCOLS με τιμές κειμένου;

Απολύτως. Αντικαταστήστε τους αριθμούς με συμβολοσειρές σε εισαγωγικά:

```csharp
sheet.Cells["A1"].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",\"Apr\",\"May\",\"Jun\"},3)";
```

### 3. Μπορώ να εφαρμόσω μορφοποίηση στη δημιουργημένη μήτρα;

Μετά τον υπολογισμό, μπορείτε να μορφοποιήσετε την περιοχή προγραμματιστικά:

```csharp
Range matrix = sheet.Cells.CreateRange("A1:C2");
Style style = workbook.CreateStyle();
style.Font.Color = System.Drawing.Color.Blue;
style.Font.IsBold = true;
matrix.ApplyStyle(style, new StyleFlag() { Font = true });
```

### 4. Πώς να διαχειριστώ πολύ μεγάλους πίνακες;

Το Aspose.Cells μπορεί να επεξεργαστεί δεκάδες χιλιάδες στοιχεία, αλλά προσέξτε τη μνήμη. Αν φτάσετε τα όρια, σκεφτείτε να γράψετε τα δεδομένα σε τμήματα ή να χρησιμοποιήσετε `Workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;`.

## Pro Tips για Κώδικα Παραγωγής

- **Cache τη αναφορά του worksheet** αν γράφετε πολλούς τύπους σε βρόχο· μειώνει το κόστος αναζήτησης.  
- **Απενεργοποιήστε τον αυτόματο υπολογισμό** (`workbook.Settings.CalculateFormulaOnOpen = false;`) όταν σκοπεύετε να γράψετε δεκάδες τύπους, και καλέστε το `Calculate()` μία φορά στο τέλος.  
- **Τυλίξτε το I/O αρχείων σε try/catch** για να εντοπίζετε γρήγορα σφάλματα δικαιωμάτων:

```csharp
try
{
    workbook.Save(outputPath);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

- **Επικυρώστε την είσοδο** πριν δημιουργήσετε το string του τύπου—ιδιαίτερα αν συνενώσετε τιμές που προέρχονται από χρήστη—για να αποφύγετε κατεστραμμένους τύπους.

## Οπτική Σύνοψη

![Πώς να χρησιμοποιήσετε το WRAPCOLS για τη δημιουργία μήτρας στο Excel](wrapcols-output.png "Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# για να μετασχηματίσετε έναν πίνακα σε μήτρα")

*Το στιγμιότυπο δείχνει τη μήτρα 2 × 3 που παράγεται από τον τύπο WRAPCOLS.*

## Συμπέρασμα

Καλύψαμε **πώς να χρησιμοποιήσετε το WRAPCOLS** σε C# από την αρχή μέχρι το τέλος: δημιουργία ή φόρτωση βιβλίου εργασίας, εγγραφή τύπου πίνακα σε κελί, εξαναγκασμός υπολογισμού και αποθήκευση του αποτελέσματος. Τώρα ξέρετε πώς να **μετασχηματίσετε έναν πίνακα σε μήτρα**, **να γράψετε τύπο πίνακα**, και **να φορτώσετε υπάρχοντα αρχεία Excel**—όλα με λίγες γραμμές καθαρού, συντηρήσιμου κώδικα.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές του παρόντος οδηγού. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to Load Excel Files Efficiently Using Aspose.Cells in .NET](/cells/english/net/workbook-operations/efficient-excel-load-aspose-cells-net/)
- [How to Load and Modify Excel Files Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}