---
category: general
date: 2026-10-26
description: Μάθετε πώς να χρησιμοποιείτε το WRAPCOLS σε C# για να χωρίσετε ένα εύρος
  σε στήλες, να εφαρμόσετε το WRAPROWS για σειρές και να αποθηκεύσετε το βιβλίο εργασίας
  ως XLSX προγραμματιστικά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: el
lastmod: 2026-10-26
og_description: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# για να χωρίσετε τα δεδομένα
  σε στήλες, χρησιμοποιήστε το WRAPROWS για τις γραμμές και αποθηκεύστε το βιβλίο
  εργασίας ως XLSX. Ακολουθήστε τον πλήρη βήμα‑βήμα οδηγό.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# – διαχωρίστε περιοχές και αποθηκεύστε
  ως XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# και να αποθηκεύσετε το βιβλίο εργασίας
  ως XLSX
url: /el/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε το WRAPCOLS σε C# και να αποθηκεύσετε το βιβλίο εργασίας ως XLSX

Αν χρειάζεστε **how to use WRAPCOLS** για να αναδιοργανώσετε δεδομένα σε ένα αρχείο Excel, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, εκτελέσιμη λύση. Θα δείτε ένα **excel wrapcols example**, θα μάθετε πώς να **split range into rows** με WRAPROWS, και θα ολοκληρώσετε με **save workbook as XLSX**—όλα γίνονται **programmatically**.

Η εργασία με το Excel από C# συχνά σημαίνει δημιουργία βιβλίου εργασίας, εφαρμογή τύπων και αποθήκευση του αρχείου. Ο κώδικας παρακάτω χρησιμοποιεί τη βιβλιοθήκη Aspose.Cells, η οποία σας επιτρέπει να χειρίζεστε αρχεία Excel χωρίς να χρειάζεται εγκατεστημένο Microsoft Office. Στο τέλος αυτού του οδηγού θα μπορείτε να **create excel workbook programmatically**, να διαχωρίσετε δεδομένα οριζόντια και κάθετα, και να παράγετε ένα καθαρό αρχείο `.xlsx` έτοιμο για επεξεργασία downstream.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+)
* Αναφορά στο πακέτο NuGet **Aspose.Cells**  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Βασική εξοικείωση με C# και τύπους Excel

## Βήμα 1: Πώς να χρησιμοποιήσετε το WRAPCOLS για να χωρίσετε μια περιοχή σε στήλες

Η συνάρτηση **WRAPCOLS** λαμβάνει μια μονοδιάστατη περιοχή και διανέμει τις τιμές της σε έναν καθορισμένο αριθμό στηλών. Σε αυτό το παράδειγμα ξεκινούμε με τιμές στο `A1:A10` και ζητάμε από το WRAPCOLS να δημιουργήσει τρεις στήλες.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Αποτέλεσμα:** Τα κελιά `C1:E4` περιέχουν τώρα τα αρχικά δέκα στοιχεία διατεταγμένα σε τρεις στήλες (η τελευταία στήλη περιέχει τα υπόλοιπα στοιχεία).

![Στιγμιότυπο οθόνης που δείχνει πώς να χρησιμοποιήσετε το WRAPCOLS για να χωρίσετε μια περιοχή σε στήλες στο Excel](image-url.png)

## Βήμα 2: Χωρίστε την περιοχή σε γραμμές με WRAPROWS

Ενώ η **WRAPCOLS** λειτουργεί οριζόντια, η **WRAPROWS** κάνει το αντίστροφο: διανέμει μια περιοχή σε έναν καθορισμένο αριθμό γραμμών. Εδώ παίρνουμε τιμές από το `B1:B10` και τις τοποθετούμε σε δύο γραμμές ξεκινώντας από το `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Αποτέλεσμα:** Ο τύπος γεμίζει τα κελιά `F1:K2` με τις δέκα τιμές που διανέμονται σε δύο γραμμές.

## Βήμα 3: Save workbook as XLSX

Μετά την εφαρμογή των τύπων, το τελευταίο βήμα είναι η αποθήκευση του αρχείου. Η λειτουργία **save workbook as xlsx** γράφει το βιβλίο εργασίας στη μνήμη στο δίσκο σε μορφή OpenXML.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Πώς φαίνεται το αποθηκευμένο αρχείο

Όταν ανοίξετε το `wrapcols_wraprows_output.xlsx` στο Excel, θα δείτε:

| C | D | E |
|---|---|---|
| Στοιχείο 1 | Στοιχείο 4 | Στοιχείο 7 |
| Στοιχείο 2 | Στοιχείο 5 | Στοιχείο 8 |
| Στοιχείο 3 | Στοιχείο 6 | Στοιχείο 9 |
|  |  | Στοιχείο 10 |

και

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Τιμή 1 | Τιμή 3 | Τιμή 5 | Τιμή 7 | Τιμή 9 | |
| Τιμή 2 | Τιμή 4 | Τιμή 6 | Τιμή 8 | Τιμή 10 | |

Οι τύποι παραμένουν στα κελιά, ώστε τυχόν μεταγενέστερες αλλαγές στις πηγές περιοχών να αντικατοπτρίζονται αυτόματα.

## Βήμα 4: Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

### Αλλαγή του αριθμού των στηλών ή των γραμμών

* **More columns:** Αυξήστε το δεύτερο όρισμα της `WRAPCOLS`.  
  Παράδειγμα: `=WRAPCOLS(A1:A10,5)` δημιουργεί πέντε στήλες, αφήνοντας κενά κελιά όπου τα δεδομένα λήγουν.
* **Dynamic column count:** Χρησιμοποιήστε μια αναφορά κελιού αντί για σταθερό αριθμό.  
  `=WRAPCOLS(A1:A10, G1)` όπου το `G1` περιέχει τον επιθυμητό αριθμό στηλών.

### Διαχείριση κενών ή μη‑αριθμητικών κελιών

Η WRAPCOLS και η WRAPROWS αγνοούν τα κενά κελιά εξ ορισμού, αλλά διατηρούν τη σειρά των μη‑κενών τιμών. Εάν χρειάζεται να διατηρήσετε τα κενά, τυλίξτε την πηγή περιοχής με τις συναρτήσεις `IFERROR` ή `TEXT` πριν εφαρμόσετε τη WRAPCOLS.

### Αποθήκευση σε άλλες μορφές

Ενώ αυτός ο οδηγός εστιάζει στο **save workbook as xlsx**, το Aspose.Cells υποστηρίζει πολλές μορφές (`.xls`, `.csv`, `.pdf`, κ.λπ.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Συμβουλές και παγίδες

* **Pro tip:** Ορίστε `Workbook.Settings.CalcEngineEnabled = true` εάν σκοπεύετε να αξιολογήσετε τους τύπους αμέσως μετά την αποθήκευση.
* **Watch out for:** Μεγάλες περιοχές πηγής μπορούν να δημιουργήσουν πολύ μεγάλες περιοχές spill, κάτι που μπορεί να επηρεάσει την απόδοση. Περιορίστε το μέγεθος της περιοχής ή χωρίστε τη λειτουργία σε πολλαπλά φύλλα εργασίας.
* **Thread safety:** Τα αντικείμενα Aspose.Cells **δεν** είναι thread‑safe. Δημιουργήστε ένα ξεχωριστό στιγμιότυπο `Workbook` ανά νήμα εάν επεξεργάζεστε αρχεία παράλληλα.

## Συμπέρασμα

Τώρα γνωρίζετε **how to use WRAPCOLS** για να χωρίσετε μια κάθετη περιοχή σε πολλαπλές στήλες, πώς να **split range into rows** με WRAPROWS, και πώς να **save workbook as XLSX** μετά την εκτέλεση αυτών των μετασχηματισμών. Ακολουθώντας τα παραπάνω βήματα μπορείτε να **create excel workbook programmatically**, να εφαρμόσετε ισχυρούς τύπους spill, και να δημιουργήσετε έτοιμα προς κοινή χρήση αρχεία Excel χωρίς χειροκίνητη παρέμβαση.

### Τι θα ακολουθήσει;

* Εξερευνήστε το **conditional formatting** για να επισημάνετε τα δεδομένα spill.
* Συνδυάστε το **WRAPCOLS** με το **SORT** ή το **FILTER** για δυναμικούς πίνακες ελέγχου.
* Χρησιμοποιήστε το **charting API** του Aspose.Cells για να οπτικοποιήσετε τα αναδιατεταγμένα δεδομένα απευθείας από τον κώδικα.

Καλό κώδικα και απολαύστε την αυτοματοποίηση των ροών εργασίας σας στο Excel!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [πώς να χρησιμοποιήσετε wrapcols σε C# – Πλήρης Οδηγός με Excel WRAPROWS & Επαναϋπολογισμό Τύπων](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Πώς να χρησιμοποιήσετε WRAPCOLS σε C# – Μετασχηματισμός Πίνακα σε Μήτρα στο Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [Πώς να χρησιμοποιήσετε WRAPCOLS – Πλήρης Οδηγός για Αυτοματοποίηση Excel με C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}