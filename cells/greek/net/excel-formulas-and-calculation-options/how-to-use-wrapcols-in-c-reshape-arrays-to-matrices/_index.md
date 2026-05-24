---
category: general
date: 2026-05-23
description: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# για να μετασχηματίσετε έναν
  μονοδιάστατο πίνακα σε δισδιάστατο. Μάθετε τη λειτουργία wrap columns, γράψτε τύπο
  σε κελί και μετατρέψτε εύκολα το 1D σε 2D.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- convert 1d to 2d
- write formula to cell
- wrap columns function
language: el
og_description: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# σας επιτρέπει να μετασχηματίσετε
  έναν μονοδιάστατο πίνακα σε δισδιάστατο με έναν μόνο τύπο. Ακολουθήστε αυτόν τον
  οδηγό για να γράψετε τύπο σε κελί και να κυριαρχήσετε στη λειτουργία περιτύλιξης
  στηλών.
og_title: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# – Αναδιαμορφώστε Πίνακες σε Μήτρες
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  headline: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  name: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  steps:
  - name: Why this matters
    text: You could try to roll your own matrix logic, but the **wrap columns function**
      already handles edge cases like uneven division and empty inputs. Adding the
      Aspose.Cells NuGet package gives us a clean API to interact with Excel formulas
      directly from C#.
  - name: The core of “how to use WRAPCOLS”
    text: 'The **WRAPCOLS** function takes two arguments: an array (or range) and
      the number of columns you want per row. In our case we’ll reshape the literal
      array `{1,2,3,4,5,6}` into **2 rows × 3 columns**.'
  - name: Expected output
    text: '``` 1 2 3 4 5 6 ```'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# – Ανασχηματισμός πινάκων σε μήτρες
url: /el/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-reshape-arrays-to-matrices/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# – Αναδιαμόρφωση Πινάκων σε Μήτρες

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το WRAPCOLS** όταν χρειάζεται να μετατρέψετε μια επίπεδη λίστα αριθμών σε έναν τακτοποιημένο πίνακα; Δεν είστε μόνοι—πολλοί προγραμματιστές συναντούν δυσκολίες όταν προσπαθούν να μετατρέψουν μια μονοδιάστατη λίστα σε δισδιάστατο πλέγμα χωρίς να γράψουν πολύ κώδικα βρόχων. Τα καλά νέα; Η συνάρτηση WRAPCOLs (μερικές φορές αποκαλούμενη συνάρτηση wrap columns) κάνει όλη τη δουλειά σε μία γραμμή, και μπορείτε να τη ρίξετε κατευθείαν σε ένα βιβλίο εργασίας Excel από C#.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από τη δημιουργία ενός workbook, μέχρι **write formula to cell**, μέχρι **reshape array to matrix**, και τέλος **convert 1d to 2d** χρησιμοποιώντας τον τύπο WRAPCOLS. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που λειτουργεί με οποιονδήποτε αριθμητικό πίνακα, και θα καταλάβετε γιατί η συνάρτηση wrap columns είναι συχνά μια πιο καθαρή εναλλακτική στην χειροκίνητη αναδιαμόρφωση πινάκων.

## Prerequisites

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+)  
* Τη βιβλιοθήκη **Aspose.Cells for .NET** (δωρεάν δοκιμή ή αδειοδοτημένη έκδοση) – είναι το στοιχείο που μας παρέχει τα αντικείμενα `Workbook`, `Worksheet` και `Cell` που χρησιμοποιούνται παρακάτω.  
* Βασική κατανόηση της σύνταξης C#—δεν απαιτείται προχωρημένη γνώση του Excel.

Τα έχετε; Τέλεια—ας βάλουμε τα χέρια στη δουλειά.

![Αποτέλεσμα 2x3 μήτρας μετά τη χρήση της συνάρτησης WRAPCOLS σε C# – πώς να χρησιμοποιήσετε το WRAPCOLS](https://example.com/images/wrapcols-result.png "Πώς να χρησιμοποιήσετε το WRAPCOLS – αποτέλεσμα 2x3 μήτρας")

## Step 1: Set Up the Project and Add Aspose.Cells

### Why this matters

Θα μπορούσατε να προσπαθήσετε να υλοποιήσετε τη δική σας λογική πινάκων, αλλά η **wrap columns function** ήδη διαχειρίζεται περιπτώσεις άκρων όπως άνιση διαίρεση και κενές εισόδους. Η προσθήκη του πακέτου NuGet Aspose.Cells μας δίνει ένα καθαρό API για αλληλεπίδραση με τύπους Excel απευθείας από C#.

```bash
dotnet add package Aspose.Cells
```

*Pro tip:* Αν χρησιμοποιείτε Visual Studio, κάντε δεξί‑κλικ στο project → **Manage NuGet Packages** → αναζητήστε **Aspose.Cells** και εγκαταστήστε την πιο πρόσφατη σταθερή έκδοση.

## Step 2: Create a New Workbook (or Load an Existing One)

Τώρα που η βιβλιοθήκη είναι στη θέση της, μπορούμε να δημιουργήσουμε ένα αντικείμενο workbook. Εδώ θα γίνει το βήμα **write formula to cell**.

```csharp
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 2: Initialize a fresh workbook
        Workbook workbook = new Workbook();          // creates an empty .xls/.xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0]; // grab the first sheet
```

Εδώ δημιουργήσαμε ένα ολοκαίνουργιο workbook· μπορείτε επίσης να φορτώσετε ένα υπάρχον αρχείο με `new Workbook("path/to/file.xlsx")` αν χρειάζεται να ενσωματώσετε τη μήτρα σε ένα προδιαμορφωμένο πρότυπο.

## Step 3: Insert the WRAPCOLS Formula into a Cell

### The core of “πώς να χρησιμοποιήσετε το WRAPCOLS”

Η συνάρτηση **WRAPCOLS** δέχεται δύο ορίσματα: έναν πίνακα (ή περιοχή) και τον αριθμό των στηλών που θέλετε ανά γραμμή. Στην περίπτωσή μας θα αναδιαμορφώσουμε τον κυριολεκτικό πίνακα `{1,2,3,4,5,6}` σε **2 γραμμές × 3 στήλες**.

```csharp
        // Step 3: Write the WRAPCOLS formula into cell A1
        // The formula =WRAPCOLS({1,2,3,4,5,6},3) tells Excel to wrap every 3 items into a new row.
        worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

Παρατηρήστε πώς ο τύπος αντικατοπτρίζει αυτό που θα πληκτρολογούσατε στο ίδιο το Excel. Τοποθετώντας τον στο `Cells[0,0]` (κελί **A1**) **γράφουμε τον τύπο σε ένα κελί** χωρίς επιπλέον υποδομές.

## Step 4: Force Calculation So the Formula Evaluates

Το Aspose.Cells δεν αξιολογεί τύπους αυτόματα εκτός αν του το ζητήσετε. Αυτό το βήμα διασφαλίζει ότι το workbook περιέχει πραγματικά τη μετασχηματισμένη μήτρα.

```csharp
        // Step 4: Recalculate the workbook so the WRAPCOLS formula runs
        workbook.CalculateFormula();
```

Αν παραλείψετε αυτή τη γραμμή, τα κελιά θα εμφανίζουν ακόμα το κείμενο του τύπου αντί για τις υπολογισμένες τιμές.

## Step 5: Read Back the Result (Optional, but Handy for Verification)

Μπορεί να θέλετε να επιβεβαιώσετε ότι η λειτουργία **reshape array to matrix** ολοκληρώθηκε επιτυχώς. Εδώ είναι ένας γρήγορος βρόχος που εκτυπώνει το αποτέλεσμα 2‑by‑3 στο console.

```csharp
        // Step 5: Output the matrix to the console for verification
        for (int row = 0; row < 2; row++)          // we expect 2 rows
        {
            for (int col = 0; col < 3; col++)      // and 3 columns per row
            {
                var value = worksheet.Cells[row, col].StringValue;
                Console.Write(value + "\t");
            }
            Console.WriteLine();
        }

        // Optional: Save the workbook to disk to see the Excel view
        workbook.Save("WrapColsResult.xlsx");
    }
}
```

### Expected output

```
1   2   3
4   5   6
```

Η κονσόλα δείχνει ακριβώς την ίδια διάταξη που θα δείτε στο Excel μετά την εκτέλεση του τύπου WRAPCOLS. Αυτή είναι η μετατροπή **convert 1d to 2d** σε δράση.

## Step 6: Handling Edge Cases – What If the Array Length Isn’t a Multiple of Columns?

Αν ο αρχικός πίνακας έχει, για παράδειγμα, 7 στοιχεία και ζητήσετε 3 στήλες, το WRAPCOLS θα δημιουργήσει την τελευταία γραμμή με τα υπόλοιπα στοιχεία και θα αφήσει τα υπόλοιπα κελιά κενά. Εδώ είναι μια γρήγορη τροποποίηση για να το δείτε:

```csharp
worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6,7},3)";
workbook.CalculateFormula();
```

Result:

```
1   2   3
4   5   6
7       
```

Η **wrap columns function** γεμίζει με χάρη την τελική γραμμή με κενά κελιά, οπότε δεν χρειάζεται επιπλέον κώδικας για να διαχειριστείτε μη ταιριαστά μεγέθη.

## Step 7: Using WRAPCOLS with Dynamic Data

Σε πραγματικά έργα σπάνια θα «σκληρά» κωδικοποιήσετε τον πίνακα. Αντίθετα, θα δημιουργήσετε μια αναπαράσταση συμβολοσειράς από μια συλλογή C#:

```csharp
int[] numbers = Enumerable.Range(1, 12).ToArray(); // 1..12
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
int columns = 4; // desired columns per row

worksheet.Cells[0, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
workbook.CalculateFormula();
```

Τώρα έχετε **converted 1d to 2d** για οποιοδήποτε μήκος, και εξακολουθείτε να λαμβάνετε το ίδιο καθαρό αποτέλεσμα μήτρας. Ο τύπος δημιουργείται κατά το χρόνο εκτέλεσης, αλλά η υποκείμενη **wrap columns function** παραμένει η ίδια.

## Common Pitfalls and Pro Tips

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Ξεχάσιμο `workbook.CalculateFormula()` | Το Aspose.Cells αφήνει τους τύπους αμετάφραστους | Πάντα να καλείτε τη μέθοδο μετά τον ορισμό οποιουδήποτε τύπου |
| Χρήση μη‑αριθμητικού κυριολεκτικού πίνακα | Η WRAPCOLS απαιτεί αριθμούς ή συμβολοσειρές που μπορούν να μετατραπούν | Βεβαιωθείτε ότι το κυριολεκτικό περιέχει μόνο αριθμούς (ή συμβολοσειρές σε εισαγωγικά) |
| Ακούσια αντικατάσταση υπάρχοντων δεδομένων | Τοποθέτηση του τύπου σε κελί που ήδη περιέχει δεδομένα | Επιλέξτε ένα καθαρό κελί (π.χ., A1) ή καθαρίστε την περιοχή πρώτα |
| Μη σωστή αναφορά στο index του φύλλου εργασίας | `Worksheets[0]` είναι το πρώτο φύλλο, αλλά μπορεί να έχετε προσθέσει άλλα | Επαληθεύστε `worksheet = workbook.Worksheets["SheetName"];` αν χρειάζεται |

## Why WRAPCOLS Beats Manual Loops

* **Αναγνωσιμότητα** – Μία γραμμή τύπου αντικαθιστά δεκάδες βρόχους `for`.  
* **Απόδοση** – Η εγγενής μηχανή του Excel είναι εξαιρετικά βελτιστοποιημένη για τύπους πίνακα.  
* **Διατηρησιμότητα** – Οι μελλοντικοί προγραμματιστές βλέπουν αμέσως την πρόθεση: “wrap these values into columns”.  
* **Φορητότητα** – Ο ίδιος τύπος λειτουργεί αν εξάγετε το workbook σε Google Sheets ή LibreOffice—χωρίς λογική ειδική για C#.

## Full Working Example (Copy‑Paste Ready)



## Related Tutorials

- [Πώς να χρησιμοποιήσετε το Aspose.Cells για .NET ώστε να εμφανίσετε περιοχές κελιών ως ετικέτες δεδομένων σε γραφήματα](/cells/english/net/charts-graphs/aspose-cells-net-chart-customization-cell-ranges-data-labels/)
- [Πώς να χρησιμοποιήσετε το Aspose.Cells για .NET για ομαδοποίηση γραμμών και στηλών στο Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [Πώς να χρησιμοποιήσετε τη λειτουργία IF του Excel](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}