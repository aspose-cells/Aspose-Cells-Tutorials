---
category: general
date: 2026-11-16
description: Μάθετε πώς να επεκτείνετε έναν πίνακα στο Excel χρησιμοποιώντας το Aspose.Cells,
  τις δυναμικές συναρτήσεις πίνακα και έναν λήμμα reducer, και στη συνέχεια να γράψετε
  το αρχείο Excel από C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: el
lastmod: 2026-11-16
og_description: Πώς να επεκτείνετε έναν πίνακα στο Excel χρησιμοποιώντας το Aspose.Cells,
  τις δυναμικές συναρτήσεις πίνακα και μια συνάρτηση μειωτή λάμδα. Ακολουθήστε το
  πλήρες παράδειγμα C# για να γράψετε το αρχείο Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Πώς να επεκτείνετε έναν πίνακα στο Excel με το Aspose.Cells – βήμα‑βήμα
  οδηγός
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να επεκτείνετε έναν πίνακα στο Excel με το Aspose.Cells
url: /el/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να επεκτείνετε έναν πίνακα στο Excel με το Aspose.Cells

Αν χρειάζεστε **πώς να επεκτείνετε έναν πίνακα** σε ένα φύλλο εργασίας Excel από C#, αυτό το tutorial δείχνει τα ακριβή βήματα. Θα δημιουργήσετε ένα βιβλίο εργασίας Excel, θα χρησιμοποιήσετε δυναμικές συναρτήσεις πίνακα όπως `EXPAND` και `REDUCE`, θα εφαρμόσετε έναν **lambda** συσσωρευτή και τελικά θα **γράψετε το αρχείο Excel** στον δίσκο. Η προσέγγιση λειτουργεί με Aspose.Cells 23.10 ή νεότερη έκδοση και δεν απαιτεί καμία χειροκίνητη εγκατάσταση του Excel.

Στο τέλος αυτού του οδηγού θα έχετε ένα πλήρως λειτουργικό `ExpandReduceDemo.xlsx` που δείχνει τη δύναμη των δυναμικών τύπων πίνακα σε προγραμματιστικό περιβάλλον.

## Τι θα χρειαστείτε

- .NET 6.0 (ή οποιαδήποτε έκδοση .NET υποστηρίζεται από το Aspose.Cells)
- Πακέτο Aspose.Cells for .NET (`dotnet add package Aspose.Cells`)
- Έναν επεξεργαστή κώδικα ή IDE (Visual Studio, VS Code, Rider, κ.λπ.)

Δεν απαιτείται πρόσθετο COM interop ή εγκατάσταση του Office, επειδή το Aspose.Cells διαχειρίζεται το φορμά αρχείου εσωτερικά.

## Βήμα 1: Δημιουργία βιβλίου εργασίας Excel

Το πρώτο καθήκον είναι να **δημιουργήσετε ένα βιβλίο εργασίας excel** στη μνήμη. Το Aspose.Cells παρέχει την κλάση `Workbook`, η οποία αντιπροσωπεύει ένα ολόκληρο αρχείο XLSX.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Γιατί είναι σημαντικό:** Η δημιουργία ενός `Workbook` σας δίνει έναν καθαρό καμβά. Το προεπιλεγμένο φύλλο εργασίας είναι ήδη έτοιμο, οπότε δεν χρειάζεται να προσθέσετε κάποιο χειροκίνητα εκτός αν θέλετε πολλαπλά φύλλα.

## Βήμα 2: Εισαγωγή μιας κάθετης σταθεράς πίνακα

Η μηχανή δυναμικών πινάκων του Excel μπορεί να δουλέψει με κυριολεκτικές σταθερές πίνακα. Θα τοποθετήσουμε τον κάθετο πίνακα `{1;2;3;4;5}` στο κελί **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Συμβουλή:** Το ερωτηματικό (`;`) διαχωρίζει γραμμές στη σταθερά, ενώ το κόμμα (`,`) θα διαχωρούσε στήλες. Αυτό αντικατοπτρίζει τη σύνταξη του Excel.

## Βήμα 3: Επέκταση του πίνακα σε μήτρα

Τώρα απαντάμε στην κεντρική ερώτηση – **πώς να επεκτείνετε έναν πίνακα** – χρησιμοποιώντας τη συνάρτηση `EXPAND`. Ο τύπος επεκτείνει τον μονοστήλο πίνακα σε μια μήτρα 5 γραμμών × 2 στηλών, ξεκινώντας από το **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Γιατί EXPAND;** `EXPAND(source, rows, cols)` αναγκάζει την πηγή να καταλάβει το καθορισμένο μέγεθος, προσθέτοντας κενά αν χρειαστεί. Είναι ο πιο ευανάγνωστος τρόπος για να δημιουργήσετε μια μεγαλύτερη μήτρα από έναν απλό πίνακα.

## Βήμα 4: Συρρίκνωση της μήτρας με έναν λανβάδα (lambda) συσσωρευτή

Η συνάρτηση `REDUCE` επαναλαμβάνει μια περιοχή και συγκεντρώνει τιμές χρησιμοποιώντας μια **lambda** έκφραση. Εδώ αθροίζουμε κάθε τιμή στήλης σε μια μοναδική στήλη, τοποθετώντας το αποτέλεσμα στο **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Πώς να χρησιμοποιήσετε lambda:** Η `LAMBDA(acc, val, acc+val)` λαμβάνει τον τρέχοντα συσσωρευτή (`acc`) και την επόμενη τιμή κελιού (`val`). Επιστρέφει τον νέο συσσωρευτή, εκτελώντας ουσιαστικά ένα τρέχον άθροισμα. Αυτό δείχνει **πώς να χρησιμοποιήσετε lambda** σε τύπους Excel από κώδικα.

## Βήμα 5: Υπολογισμός τύπων ώστε να εμφανιστούν τα αποτελέσματα

Το Aspose.Cells δεν αξιολογεί αυτόματα τους τύπους όταν τους ορίζετε. Η κλήση `CalculateFormula` αναγκάζει τη μηχανή να υπολογίσει κάθε τύπο στο βιβλίο εργασίας.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Σημείωση:** Αν ανοίξετε το παραγόμενο αρχείο στο Excel, οι τιμές θα είναι ήδη ορατές επειδή έχουν προ‑υπολογιστεί.

## Βήμα 6: Γράψιμο του αρχείου Excel στον δίσκο

Τέλος, **γράψτε το αρχείο excel** χρησιμοποιώντας τη μέθοδο `Save`. Επιλέξτε έναν φάκελο για τον οποίο έχετε δικαίωμα εγγραφής.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Αναμενόμενο αποτέλεσμα

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- Η **στήλη B** και η **C** περιέχουν τη μήτρα 5 × 2 που παράγεται από το `EXPAND`.
- Το **κελί D1** δείχνει `15`, το άθροισμα όλων των αριθμών, υπολογισμένο από τον τύπο `REDUCE` + **lambda**.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

- **Μπορώ να επεκτείνω σε περισσότερες στήλες από ό,τι παρέχει η πηγή;**  
  Ναι. Το `EXPAND` συμπληρώνει τις ελλιπείς στήλες με κενά κελιά. Το ίδιο ισχύει και για τις γραμμές.

- **Τι γίνεται αν η πηγή είναι οριζόντια (`{1,2,3,4,5}`);**  
  Το `EXPAND` θα θεωρήσει την πηγή ως μία γραμμή· μπορείτε ακόμη να ορίσετε γραμμές και στήλες για να την επανασχηματίσετε.

- **Λειτουργεί το `REDUCE` με μη‑αριθμητικά δεδομένα;**  
  Η lambda πρέπει να επιστρέφει μια τιμή συμβατή με τον τύπο του συσσωρευτή. Για συγχώνευση κειμένου μπορείτε να χρησιμοποιήσετε `LAMBDA(acc, val, acc & val)`.

- **Πρέπει να καλώ `CalculateFormula` για κάθε αλλαγή;**  
  Μόνο όταν χρειάζεστε τις υπολογισμένες τιμές πριν από την αποθήκευση. Το Excel θα επαναϋπολογίσει κατά το άνοιγμα αν το παραλείψετε.

## Pro tips

- **Απόδοση:** Για μεγάλα βιβλία εργασίας, καλέστε `workbook.CalculateFormula` μία φορά μετά τον ορισμό όλων των τύπων, αντί για κάθε κελί.
- **Ασφάλεια έκδοσης:** Τα `EXPAND` και `REDUCE` είναι διαθέσιμα στο Excel 365 και νεότερα. Το Aspose.Cells τα υλοποιεί ανεξάρτητα από την έκδοση-στόχο του Excel, επειδή η μηχανή υπολογισμού είναι ενσωματωμένη.
- **Ανίχνευση σφαλμάτων τύπων:** Χρησιμοποιήστε `sheet.Cells["B1"].Formula` για να διαβάσετε την ακριβή συμβολοσειρά που ορίσατε· αυτό βοηθά όταν δημιουργείτε τύπους δυναμικά.

## Συμπέρασμα

Τώρα ξέρετε **πώς να επεκτείνετε έναν πίνακα** στο Excel χρησιμοποιώντας το Aspose.Cells, να αξιοποιήσετε **δυναμικές συναρτήσεις πίνακα**, να εφαρμόσετε μια **lambda** με το `REDUCE`, και να **γράψετε το αρχείο excel** από C#. Αυτό το ολοκληρωμένο παράδειγμα μπορεί να προσαρμοστεί σε πιο σύνθετες μετασχηματισμούς δεδομένων, όπως μετατόπιση μήτρας, αθροίσματα συσσωρευτικών τιμών ή προσαρμοσμένες συγκεντρώσεις.

---

*Επόμενα βήματα:*  
- Εξερευνήστε άλλες δυναμικές συναρτήσεις όπως `FILTER`, `SORT` και `UNIQUE`.  
- Συνδυάστε πολλαπλές εκφράσεις `LAMBDA` για να δημιουργήσετε επαναχρησιμοποιήσιμες συναρτήσεις χρήστη.  
- Ενσωματώστε τη δημιουργία βιβλίου εργασίας σε ASP.NET Core APIs για δημιουργία αναφορών «on‑the‑fly».

## Τι πρέπει να μάθετε στη συνέχεια;


Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση στα δικά σας έργα.

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}