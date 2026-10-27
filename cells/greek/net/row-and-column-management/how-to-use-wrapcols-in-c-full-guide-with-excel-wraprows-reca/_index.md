---
category: general
date: 2026-06-27
description: πώς να χρησιμοποιήσετε wrapcols και wrap rows excel σε C#. Μάθετε να
  δημιουργείτε βιβλίο εργασίας Excel με C# και να επαναϋπολογίζετε τους τύπους του
  Excel με ένα βήμα‑βήμα παράδειγμα.
draft: false
keywords:
- how to use wrapcols
- wrap rows excel
- wrap columns excel
- recalculate excel formulas
- create excel workbook c#
language: el
og_description: πώς να χρησιμοποιήσετε wrapcols και wrap rows στο Excel χρησιμοποιώντας
  C#. Αυτός ο οδηγός δείχνει πώς να δημιουργήσετε ένα βιβλίο εργασίας Excel με C#
  και να επαναϋπολογίσετε τους τύπους του Excel σε λίγα λεπτά.
og_title: πώς να χρησιμοποιήσετε το wrapcols σε C# – Πλήρης οδηγός περιτύλιξης Excel
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  headline: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate
    Formulas
  type: TechArticle
- description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  name: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas
  steps:
  - name: Expected Result
    text: '| A | B | C | |---|---|---| | 1 | A | 2 | | 2 | B | 3 | | 3 | C | 4 | |
      4 | D | 5 | | 5 | E | 6 | | 6 | F | 7 | | 7 | G | 8 | | 8 | H | 9 | | 9 | I
      | |'
  - name: What if the source range is empty?
    text: Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting
      in a blank cell. It’s safe to call the functions even when you’re not sure about
      data presence.
  - name: Can I wrap more than one range at a time?
    text: Yes—just place additional formulas in other cells. Each formula works independently,
      so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.
  - name: How does this differ from a simple copy‑paste transpose?
    text: '`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20
      items and ask for 3 columns, the function creates the necessary number of rows
      (7 in this case) without you calculating the dimensions manually.'
  - name: Does the library support dynamic array formulas (Excel 365)?
    text: Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS`
      and `WRAPROWS`. The calculation engine will spill the results just like native
      Excel.
  - name: What about performance on large datasets?
    text: For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`)
      or disabling automatic calculation while you insert formulas, then re‑enable
      it before saving.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: πώς να χρησιμοποιήσετε το wrapcols σε C# – Πλήρης Οδηγός με Excel WRAPROWS
  & Επαναϋπολογισμό Τύπων
url: /el/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να χρησιμοποιήσετε wrapcols σε C# – Πλήρης Οδηγός με Excel WRAPROWS & Επαναϋπολογισμό Τύπων

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το wrapcols** όταν χρειάζεται να μετασχηματίσετε μια μακριά λίστα σε ένα τακτικό πλέγμα; Ίσως έχετε δοκιμάσει το χειροκίνητο κόπ‑παστ, αλλά είναι αργό, επιρρεπές σε σφάλματα και, ειλικρινά, ενοχλητικό. Τα καλά νέα; Το `WRAPCOLS` του Excel (και ο αδελφός του `WRAPROWS`) μπορεί να κάνει τη βαριά δουλειά για εσάς—*και* μπορείτε να τα ελέγξετε από κώδικα C#.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τη δημιουργία ενός Excel workbook σε C#, την εφαρμογή των `WRAPCOLS` και `WRAPROWS`, και τέλος **τον επαναϋπολογισμό των τύπων του Excel** ώστε τα τυλιγμένα δεδομένα να εμφανίζονται αμέσως. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

## Τι Θα Μάθετε

- Πώς να **create excel workbook c#** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells (χωρίς ανάγκη COM interop).  
- Η ακριβής σύνταξη της συνάρτησης `WRAPCOLS` και πώς διαφέρει από την `WRAPROWS`.  
- Γιατί πρέπει να **recalculate excel formulas** μετά την εισαγωγή των συναρτήσεων, και πώς να το κάνετε αποδοτικά.  
- Ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε και να δείτε το αποτέλεσμα σε αρχείο `.xlsx`.  

**Prerequisites** – Χρειάζεστε .NET 6+ (ή .NET Framework 4.7+), Visual Studio 2022 ή οποιοδήποτε IDE προτιμάτε, και το πακέτο NuGet Aspose.Cells for .NET. Αν είστε νέοι στο Aspose.Cells, μην ανησυχείτε· τα βήματα είναι απλά και πλήρως εξηγημένα.

---

## Step 1: Set Up the Project and Install Aspose.Cells

Για να ξεκινήσετε, δημιουργήστε ένα νέο console project:

```bash
dotnet new console -n WrapDemo
cd WrapDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Αν χρησιμοποιείτε Visual Studio, κάντε δεξί‑κλικ στο project → *Manage NuGet Packages* → ψάξτε για **Aspose.Cells** και εγκαταστήστε το.

Η βιβλιοθήκη μας παρέχει τις κλάσεις `Workbook`, `Worksheet` και `Cell` που θα χρειαστούμε για το υπόλοιπο tutorial.

## Step 2: Create an Excel Workbook and Populate Sample Data

Τώρα θα δημιουργήσουμε ένα workbook, θα πάρουμε το πρώτο worksheet, και θα γεμίσουμε τις στήλες **A** και **B** με δείγμα αριθμών. Αυτά τα δεδομένα θα τυλιχθούν αργότερα σε στήλες και γραμμές.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2‑1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2‑2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate A2:A10 with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate B2:B10 with letters A‑I (just for variety)
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // The rest of the steps follow…
```

> **Why this matters:** Η ύπαρξη καθορισμένων δεδομένων σας επιτρέπει να επαληθεύσετε ότι τα `WRAPCOLS` και `WRAPROWS` κάνουν ακριβώς αυτό που περιμένετε.

## Step 3: Apply the `WRAPCOLS` Function – **how to use wrapcols**

Η `WRAPCOLs` παίρνει μια μονοδιάστατη περιοχή και τη διανέμει σε έναν καθορισμένο αριθμό στηλών, προσθέτοντας αυτόματα νέες γραμμές όπως χρειάζεται. Εδώ είναι ο ακριβής τύπος που θα εισάγουμε στο κελί **A1**:

```csharp
        // Step 3: Insert WRAPCOLS formula – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";
```

> **Explanation:** Το δεύτερο όρισμα (`3`) λέει στο Excel να δημιουργήσει τρεις στήλες ανά γραμμή. Έτσι οι πρώτες τρεις τιμές (1, 2, 3) καταλήγουν στο A1:C1, οι επόμενες τρεις (4, 5, 6) στο A2:C2, και οι υπόλοιπες τιμές γεμίζουν την επόμενη γραμμή.

## Step 4: Apply the `WRAPROWS` Function – wrap rows excel

Η `WRAPROWS` κάνει το αντίστροφο: παίρνει μια κάθετη περιοχή και τη διατάσσει σε έναν καθορισμένο αριθμό γραμμών ανά στήλη. Θα τοποθετήσουμε αυτόν τον τύπο στο **B1**:

```csharp
        // Step 4: Insert WRAPROWS formula – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";
```

> **Explanation:** Με `2` γραμμές ανά στήλη, οι τιμές “A, B” πηγαίνουν στο B1:B2, “C, D” στο C1:C2, κλπ. Η συνάρτηση επεκτείνει αυτόματα το φύλλο οριζόντια.

## Step 5: Recalculate All Formulas – **recalculate excel formulas**

Όταν ορίζετε έναν τύπο προγραμματιστικά, το Excel δεν θα υπολογίσει το αποτέλεσμα μέχρι να ανοίξει το workbook ή μέχρι να του πείτε ρητά να το αξιολογήσει. Εδώ έρχεται το **recalculate excel formulas**:

```csharp
        // Step 5: Force calculation so the wrapped data appears immediately
        workbook.CalculateFormula();
```

> **Why you need this:** Χωρίς την κλήση `CalculateFormula()`, τα κελιά θα εμφανίζουν το ακατέργαστο κείμενο `=WRAPCOLS(...)` όταν ανοίξετε το αρχείο, κάτι που αναιρεί τον σκοπό του tutorial.

## Step 6: Save the Workbook and Verify the Output

Τέλος, γράψτε το workbook στο δίσκο. Μπορείτε να ανοίξετε το παραγόμενο αρχείο στο Excel για να δείτε τη τυλιγμένη διάταξη.

```csharp
        // Step 6: Save the workbook (adjust the path as needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see wrapcols and wraprows in action.");
    }
}
```

### Expected Result

| A | B | C |
|---|---|---|
| 1 | A | 2 |
| 2 | B | 3 |
| 3 | C | 4 |
| 4 | D | 5 |
| 5 | E | 6 |
| 6 | F | 7 |
| 7 | G | 8 |
| 8 | H | 9 |
| 9 | I |   |

- **Columns A‑C** είναι γεμάτες από την κλήση `WRAPCOLS` (τρεις στήλες ανά γραμμή).  
- **Rows B‑I** είναι γεμάτες από την κλήση `WRAPROWS` (δύο γραμμές ανά στήλη).  

Ανοίξτε το `output.xlsx` και θα δείτε ακριβώς τη διάταξη που φαίνεται παραπάνω. Αν οι αριθμοί δεν ταιριάζουν, ελέγξτε ξανά τις συμβολοσειρές τύπων και βεβαιωθείτε ότι κλήθηκε το `CalculateFormula()`.

---

## Common Questions & Edge Cases

### What if the source range is empty?
Και οι δύο `WRAPCOLS` και `WRAPROWS` θα επιστρέψουν απλώς έναν κενό πίνακα, με αποτέλεσμα ένα κενό κελί. Είναι ασφαλές να καλέσετε τις συναρτήσεις ακόμη και όταν δεν είστε σίγουροι για την παρουσία δεδομένων.

### Can I wrap more than one range at a time?
Ναι—απλώς τοποθετήστε επιπλέον τύπους σε άλλα κελιά. Κάθε τύπος λειτουργεί ανεξάρτητα, οπότε μπορείτε να έχετε `WRAPCOLS` στο D1, `WRAPROWS` στο E1 κλπ.

### How does this differ from a simple copy‑paste transpose?
Το `WRAPCOLS`/`WRAPROWS` διαχειρίζεται την *σελιδοποίηση* αυτόματα. Αν έχετε 20 στοιχεία και ζητήσετε 3 στήλες, η συνάρτηση δημιουργεί τις απαραίτητες γραμμές (7 σε αυτήν την περίπτωση) χωρίς να χρειάζεται να υπολογίσετε χειροκίνητα τις διαστάσεις.

### Does the library support dynamic array formulas (Excel 365)?
Το Aspose.Cells υποστηρίζει πλήρως τις δυναμικές συναρτήσεις πίνακα, συμπεριλαμβανομένων των `WRAPCOLS` και `WRAPROWS`. Η μηχανή υπολογισμού θα «χύνεται» τα αποτελέσματα όπως το κάνει το φυσικό Excel.

### What about performance on large datasets?
Για εκατομμύρια γραμμές, σκεφτείτε να κάνετε batch τον υπολογισμό (`workbook.CalculateFormula(FormulaCalculationOptions)`) ή να απενεργοποιήσετε τον αυτόματο υπολογισμό ενώ εισάγετε τύπους, και να τον ενεργοποιήσετε ξανά πριν την αποθήκευση.

---

## Full Source Code (Ready to Run)

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate column A (A2:A10) with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate column B (B2:B10) with letters A‑I
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // Apply WRAPCOLS – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";

        // Apply WRAPROWS – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";

        // Recalculate all formulas so the wrapped data appears
        workbook.CalculateFormula();

        // Save the workbook (adjust the folder if needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the wrapped results.");
    }
}
```

---

## Conclusion

Τώρα ξέρετε **πώς να χρησιμοποιήσετε wrapcols** (και το αντίστοιχο `WRAPROWS`) από C# για να μετασχηματίσετε δεδομένα σε ένα φύλλο Excel, και κατανοείτε γιατί το **recalculate excel formulas** είναι απαραίτητο βήμα. Αυτό το μοτίβο—*create excel workbook c# → insert WRAP functions → recalculate*—είναι μια σταθερή βάση για οποιοδήποτε έργο αναφοράς ή παρουσίασης δεδομένων που απαιτεί δυναμικές διατάξεις στηλών ή γραμμών.

Τι θα κάνετε στη συνέχεια; Δοκιμάστε να πειραματιστείτε με:

- Διαφορετικούς αριθμούς στηλών/γραμμών (`WRAPCOLS(..., 5)` ή `WRAPROWS(..., 4)`).  
- Συνδυασμό `WRAPCOLS` με άλλες δυναμικές συναρτήσεις όπως `FILTER` ή `SORT`.  
- Εξαγωγή του workbook σε PDF με `workbook.Save("report.pdf", SaveFormat.Pdf)`.

Νιώστε ελεύθεροι να τροποποιήσετε το δείγμα, να προσθέσετε μορφοποίηση ή να το ενσωματώσετε σε μια μεγαλύτερη αλυσίδα αυτοματισμού. Αν συναντήσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω—καλή προγραμματιστική!

![Διάγραμμα που δείχνει πώς τα wrapcols και wraprows μετασχηματίζουν μια μονή στήλη σε πλέγμα – παράδειγμα χρήσης wrapcols](wrapcols-wraprows-diagram.png "παράδειγμα χρήσης wrapcols")

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας projects.

- [How to Use Aspose.Cells for .NET to Group Rows and Columns in Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [How to Hide Rows and Columns in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/range-management/aspose-cells-net-hide-rows-columns-excel/)
- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}