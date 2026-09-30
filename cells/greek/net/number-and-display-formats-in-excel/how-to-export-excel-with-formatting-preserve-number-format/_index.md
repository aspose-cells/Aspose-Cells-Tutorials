---
category: general
date: 2026-03-22
description: Πώς να εξάγετε το Excel με μορφοποίηση και να διατηρήσετε τη μορφή αριθμών.
  Μάθετε να μετατρέπετε το εύρος του Excel, να λαμβάνετε το αποτέλεσμα του τύπου και
  να εξάγετε το Excel με μορφοποίηση χρησιμοποιώντας το Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: el
og_description: Πώς να εξάγετε το Excel με μορφοποίηση και να διατηρήσετε τη μορφή
  αριθμών. Οδηγός βήμα‑βήμα για τη μετατροπή περιοχής Excel, την απόκτηση του αποτελέσματος
  του τύπου και την εξαγωγή του Excel με μορφοποίηση σε C#.
og_title: Πώς να εξάγετε το Excel με μορφοποίηση – Διατηρήστε τη μορφή αριθμών
tags:
- C#
- Aspose.Cells
- Excel automation
title: Πώς να εξάγετε το Excel με μορφοποίηση – Διατηρήστε τη μορφή αριθμών
url: /el/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε το Excel με Μορφοποίηση – Διατήρηση Μορφής Αριθμού

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε δεδομένα Excel** διατηρώντας την εμφάνιση κάθε κελιού ακριβώς όπως τη βλέπετε στο βιβλίο εργασίας; Ίσως χρειάζεται να στείλετε μια αναφορά σε πελάτη, να τροφοδοτήσετε έναν έλεγχο πλέγματος, ή απλώς να αποθηκεύσετε τις τιμές σε μια βάση δεδομένων. Το πρόβλημα συνήθως είναι η απώλεια μορφοποίησης αριθμών ή οι τύποι που μετατρέπονται σε ακατέργαστες συμβολοσειρές.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα ένα πλήρες, έτοιμο προς εκτέλεση παράδειγμα C# που **διατηρεί τη μορφή αριθμού**, **μετατρέπει μια περιοχή Excel** σε `DataTable`, **παίρνει το αποτέλεσμα του τύπου**, και τελικά **εξάγει το Excel με μορφοποίηση** χρησιμοποιώντας το Aspose.Cells. Στο τέλος θα έχετε μια μοναδική μέθοδο που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο και να καλέσετε με μια αναφορά φύλλου εργασίας.

> **Γρήγορη προεπισκόπηση:** ο κώδικας δημιουργεί ένα βιβλίο εργασίας, γράφει μια τιμή και έναν τύπο, λέει στο Aspose.Cells να εξάγει τα κελιά ως μορφοποιημένες συμβολοσειρές, και εκτυπώνει `123.456 | 246.912` – ακριβώς ό,τι θα περιμένατε να δείτε στο Excel.

---

## Τι Θα Χρειαστείτε

- **Aspose.Cells for .NET** (η δωρεάν δοκιμαστική έκδοση λειτουργεί καλά για μάθηση)
- .NET 6.0 ή νεότερο (το API είναι το ίδιο στο .NET Framework)
- Ένα βασικό περιβάλλον ανάπτυξης C# (Visual Studio, VS Code, Rider… όπως προτιμάτε)

Δεν απαιτούνται επιπλέον πακέτα NuGet εκτός από το Aspose.Cells. Αν δεν το έχετε εγκαταστήσει ακόμη, εκτελέστε:

```bash
dotnet add package Aspose.Cells
```

---

## Βήμα 1 – Δημιουργία Βιβλίου Εργασίας και Εγγραφή Τιμών (συμπεριλαμβανομένου τύπου)

Αρχικά δημιουργούμε ένα νέο βιβλίο εργασίας και τοποθετούμε μια αριθμητική τιμή στο **A1**. Στη συνέχεια προσθέτουμε έναν απλό τύπο στο **B1** που πολλαπλασιάζει το πρώτο κελί με το δύο. Αυτό θέτει το σκηνικό για την επίδειξη του **get formula result** αργότερα.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Γιατί είναι σημαντικό:**  
- `PutValue` αποθηκεύει τον ακατέργαστο αριθμό, ενώ `PutFormula` αποθηκεύει τον υπολογισμό.  
- Το Aspose.Cells διατηρεί τον τύπο **ζωντανό**, έτσι όταν αργότερα ζητήσουμε την τιμή του κελιού θα πάρουμε πραγματικά `246.912`, όχι τη συμβολοσειρά `"=A1*2"`.

---

## Βήμα 2 – Εντολή στο Aspose.Cells να Εξάγει Τιμές ως Μορφοποιημένες Συμβολοσειρές

Αν απλώς καλέσετε το `ExportDataTable` με τις προεπιλεγμένες ρυθμίσεις, τα αριθμητικά κελιά θα επιστραφούν ως οι υποκείμενες τιμές `double`. Αυτό αφαιρεί τυχόν διαχωριστικά χιλιάδων, σύμβολα νομίσματος ή προσαρμοσμένα δεκαδικά που έχετε ορίσει. Η κλάση `ExportTableOptions` μας επιτρέπει να **διατηρήσουμε τη μορφή αριθμού** και να **εξάγουμε ως συμβολοσειρά**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Κύριο σημείο:** `ExportNumberFormat = true` είναι η σημαία που κάνει τη **διατήρηση μορφής αριθμού** λειτουργική. Χωρίς αυτήν θα δείτε `"123.456"` και `"246.912"` ως ακατέργαστους αριθμούς, κάτι που μπορεί να φαίνεται εντάξει στον κώδικα αλλά όχι όταν επικολλάτε τα δεδομένα σε UI που αναμένει την ίδια μορφοποίηση όπως το Excel.

---

## Βήμα 3 – Εκτύπωση των Εξαγόμενων Δεδομένων (Επαλήθευση)

Τώρα που έχουμε ένα `DataTable` γεμάτο μορφοποιημένες συμβολοσειρές, ας εκτυπώσουμε το περιεχόμενό του στην κονσόλα. Αυτό επίσης δείχνει ότι καταφέραμε να **get formula result** χωρίς να αξιολογήσουμε τον τύπο εμείς.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Running the program prints:

```
123.456 | 246.912
```

Παρατηρήστε πώς η δεύτερη στήλη εμφανίζει το **αποτέλεσμα του τύπου**, όχι το κείμενο του τύπου. Αυτό είναι ακριβώς ό,τι χρειάζεστε όταν **εξάγετε Excel με μορφοποίηση** για επεξεργασία σε επόμενα στάδια.

---

## Βήμα 4 – Μετατροπή Μεγαλύτερων Περιοχών Excel (Προαιρετικό)

Το παραπάνω παράδειγμα διαχειρίζεται ένα μικρό τμήμα `A1:B1`, αλλά σε πραγματικές συνθήκες συχνά χρειάζεται η εξαγωγή ολόκληρων πινάκων. Η ίδια μέθοδος λειτουργεί για οποιοδήποτε ορθογώνιο μπλοκ – απλώς προσαρμόστε τις παραμέτρους `firstRow`, `firstColumn`, `totalRows` και `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Συμβουλή:** Αν το φύλλο σας έχει ήδη μια γραμμή κεφαλίδας, ορίστε `includeColumnNames` σε `true`. Το Aspose.Cells θα χρησιμοποιήσει την πρώτη γραμμή της περιοχής ως ονόματα στηλών, κάτι που είναι χρήσιμο όταν αργότερα συνδέσετε το `DataTable` με ένα UI grid.

---

## Βήμα 5 – Συνηθισμένα Πιθανά Σφάλματα & Πώς να τα Αποφύγετε

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Οι αριθμοί χάνουν κόμματα ή σύμβολα νομίσματος** | `ExportAsString` είναι `false` ή λείπει το `ExportNumberFormat` | Ορίστε και τα δύο `ExportAsString = true` **και** `ExportNumberFormat = true`. |
| **Τα κελιά τύπου επιστρέφουν το κείμενο του τύπου** | Δεν κάλεσατε το `CalculateFormula` πριν την εξαγωγή (απαιτείται μόνο αν το βιβλίο εργασίας δεν είναι σε auto‑calculate) | Ενεργοποιήστε το auto‑calculate (`workbook.CalculateFormula()`) ή βασιστείτε στο `ExportAsString` που αναγκάζει την αξιολόγηση. |
| **Οι κεφαλίδες εμφανίζονται ως γραμμές δεδομένων** | `includeColumnNames` είναι `false` ενώ η περιοχή σας περιλαμβάνει γραμμή κεφαλίδας | Ορίστε `includeColumnNames = true` για να θεωρήσετε την πρώτη γραμμή ως ονόματα στηλών. |
| **Οι μεγάλες περιοχές προκαλούν πίεση μνήμης** | Η εξαγωγή ολόκληρου του φύλλου ταυτόχρονα φορτώνει όλα στη μνήμη | Εξάγετε σε τμήματα (π.χ., 500 γραμμές τη φορά) και συγχωνεύστε τα `DataTable` αν χρειαστεί. |

---

## Βήμα 6 – Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, από τις δηλώσεις `using` μέχρι τη `Main`. Επικολλήστε το σε μια εφαρμογή console και πατήστε **F5** – θα δείτε αμέσως την μορφοποιημένη έξοδο.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Αναμενόμενη έξοδος**

```
123.456 | 246.912

Press any key to exit...
```

Αυτή είναι ολόκληρη η ροή εργασίας **πώς να εξάγετε excel**, με τη μορφοποίηση αμετάβλητη, τα αποτελέσματα των τύπων αξιολογημένα, και ένα καθαρό `DataTable` έτοιμο για οποιονδήποτε καταναλωτή .NET.

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεται να γνωρίζετε σχετικά με το **πώς να εξάγετε δεδομένα Excel** ενώ **διατηρείτε τη μορφή αριθμού**, **μετατρέπετε μια περιοχή Excel** σε `DataTable`, και **παίρνετε τα αποτελέσματα των τύπων** χωρίς πρόσθετη ανάλυση. Το κλειδί είναι η διαμόρφωση `ExportTableOptions` – μόλις ορίσετε `ExportAsString` και `ExportNumberFormat` σε `true`, το Aspose.Cells κάνει τη σκληρή δουλειά για εσάς.

Από εδώ μπορείτε:

- Συνδέστε το `DataTable` σε ένα WPF `DataGrid` ή σε μια προβολή ASP.NET MVC.
- Γράψτε τον πίνακα σε αρχείο CSV διατηρώντας την ακριβή οπτική αναπαράσταση.
- Επεκτείνετε την προσέγγιση σε πολλαπλά φύλλα ή δυναμικές περιοχές.

Μη διστάσετε να πειραματιστείτε με διαφορετικές μορφές (νόμισμα, ποσοστά) και μεγαλύτερα τμήματα δεδομένων. Αν αντιμετωπίσετε οποιοδήποτε πρόβλημα, επιστρέψτε στον πίνακα **συνηθισμένων παγίδων** – καλύπτει τα πιο συχνά εμπόδια όταν **εξάγετε excel με μορφοποίηση**.

Καλή προγραμματιστική δουλειά, και εύχομαι τα εξαγόμενα φύλλα σας να είναι πάντα τόσο καλοσχεδιασμένα όσο τα πρωτότυπα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}