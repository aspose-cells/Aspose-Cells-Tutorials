---
category: general
date: 2026-03-21
description: Εξαγωγή πίνακα δεδομένων Excel σε DataTable με κεφαλίδες, περιορισμός
  των δεκαδικών ψηφίων και εξαγωγή των πρώτων 100 γραμμών χρησιμοποιώντας το Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: el
og_description: Μάθετε πώς να εξάγετε έναν πίνακα δεδομένων Excel σε DataTable, να
  διατηρήσετε τις κεφαλίδες, να περιορίσετε τα δεκαδικά ψηφία και να πάρετε τις πρώτες
  100 γραμμές σε C#.
og_title: Εξαγωγή Πίνακα Δεδομένων Excel σε C# – Οδηγός Βήμα‑προς‑Βήμα
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Εξαγωγή Πίνακα Δεδομένων Excel σε C# – Πλήρης Οδηγός
url: /el/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Πίνακα Δεδομένων Excel – Πλήρης Οδηγός C#

Χρειάζεστε **εξαγωγή πίνακα δεδομένων excel** από ένα βιβλίο εργασίας σε ένα .NET `DataTable`; Βρίσκεστε στο σωστό σημείο — αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε, να διατηρήσετε τις επικεφαλίδες των στηλών, να περιορίσετε τα δεκαδικά ψηφία και να λάβετε μόνο τις πρώτες 100 γραμμές.  

Αν έχετε ποτέ κοίταξει ένα υπολογιστικό φύλλο και σκεφτείτε, «Πώς θα το βάλω στην εφαρμογή μου χωρίς να χάσω τη μορφοποίηση;», δεν είστε μόνοι. Στα επόμενα λεπτά θα μετατρέψουμε αυτό το «τι θα γίνει αν» σε μια συγκεκριμένη, αντιγραφή‑και‑επικόλληση λύση που λειτουργεί με το Aspose.Cells, μια δημοφιλής βιβλιοθήκη για χειρισμό Excel.

## Τι Θα Μάθετε

- Πώς να **εξάγετε excel σε datatable** χρησιμοποιώντας τη μέθοδο `ExportDataTable`.  
- Πώς να διατηρήσετε τα αρχικά ονόματα στηλών (`export excel with headers`).  
- Πώς να **περιορίσετε τα δεκαδικά ψηφία excel** ρυθμίζοντας το `ExportTableOptions`.  
- Πώς να ανακτήσετε με ασφάλεια μόνο τις πρώτες 100 γραμμές (`export first 100 rows`).  

Χωρίς εξωτερικά σενάρια, χωρίς μαγικές συμβολοσειρές — μόνο απλό C# που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|-----------------------|
| .NET 6 ή νεότερο (ή .NET Framework 4.7+) | Το Aspose.Cells υποστηρίζει και τα δύο, αλλά τα πιο πρόσφατα runtime παρέχουν async‑ready APIs. |
| Πακέτο NuGet Aspose.Cells για .NET | Παρέχει `Workbook`, `ExportTableOptions` και το βοηθητικό `ExportDataTable`. |
| Ένα δείγμα αρχείου Excel (π.χ. `Numbers.xlsx`) | Η πηγή των δεδομένων που θα εξάγετε. |
| Βασικές γνώσεις C# | Θα ακολουθήσετε τα αποσπάσματα κώδικα, αλλά δεν απαιτείται τίποτα περίπλοκο. |

Αν κάτι από αυτά σας φαίνεται άγνωστο, κατεβάστε το πακέτο NuGet με `dotnet add package Aspose.Cells` και δημιουργήστε ένα μικρό αρχείο Excel με μερικούς αριθμούς — τα δεδομένα δοκιμής σας.

![παράδειγμα εξαγωγής πίνακα δεδομένων excel](excel-data-table.png "Στιγμιότυπο οθόνης ενός φύλλου Excel που θα εξαχθεί σε DataTable")

## Βήμα 1: Φόρτωση του Workbook (export excel data table)

Το πρώτο πράγμα που χρειάζεστε είναι μια παρουσία `Workbook` που δείχνει στο αρχείο Excel σας. Σκεφτείτε το σαν το άνοιγμα ενός βιβλίου πριν διαβάσετε τα κεφάλαιά του.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του workbook σας δίνει πρόσβαση στα φύλλα εργασίας, τα κελιά και τα στυλ του. Αν η διαδρομή του αρχείου είναι λανθασμένη, το Aspose θα ρίξει `FileNotFoundException`, γι’ αυτό ελέγξτε ξανά τη θέση.

## Βήμα 2: Διαμόρφωση Επιλογών Εξαγωγής – limit decimal places excel

Από προεπιλογή το Aspose εξάγει κάθε αριθμητική τιμή με πλήρη ακρίβεια. Συχνά χρειάζεστε μόνο λίγα σημαντικά ψηφία, ειδικά όταν τα δεδομένα πηγαίνουν σε UI grid ή σε API που απαιτεί στρογγυλοποιημένους αριθμούς.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Συμβουλή:** Αν χρειάζεστε διαφορετική στρατηγική στρογγυλοποίησης (π.χ. πάντα προς τα πάνω), μπορείτε να επεξεργαστείτε το `DataTable` μετά την εξαγωγή. Η ρύθμιση `SignificantDigits` είναι ο πιο γρήγορος τρόπος να **περιορίσετε τα δεκαδικά ψηφία excel** χωρίς επιπλέον βρόχους.

## Βήμα 3: Εξαγωγή του Επιθυμητού Περιοχής (export first 100 rows)

Τώρα λέμε στο Aspose ποιο μπλοκ κελιών θέλουμε να μεταφέρουμε σε ένα `DataTable`. Σε αυτόν τον οδηγό εξάγουμε τις πρώτες 100 γραμμές και τις πρώτες 10 στήλες, αλλά μπορείτε να προσαρμόσετε τους αριθμούς ώστε να ταιριάζουν στο σενάριό σας.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Ακραία περίπτωση:** Αν το φύλλο περιέχει λιγότερες από 100 γραμμές, το Aspose θα εξάγει απλώς ό,τι υπάρχει χωρίς να ρίξει σφάλμα. Ωστόσο, ίσως θελήσετε να προστατέψετε τον κώδικα σας από απροσδόκητα μικρές περιοχές:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Βήμα 4: Επαλήθευση του Αποτελέσματος – Γρήγορη Εκτύπωση στην Κονσόλα

Το να βλέπετε τα δεδομένα στον debugger είναι ωραίο, αλλά η εκτύπωση μερικών γραμμών στην κονσόλα επιβεβαιώνει ότι η **εξαγωγή excel σε datatable** λειτούργησε και ότι τα δεκαδικά ψηφία έχουν περικοπεί.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Αναμενόμενη Έξοδος

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Παρατηρήστε πώς οι αριθμητικές στήλες τώρα εμφανίζουν μόνο τέσσερα σημαντικά ψηφία, σύμφωνα με τη ρύθμιση `SignificantDigits = 4` που εφαρμόσαμε νωρίτερα.

## Βήμα 5: Συνολική Ενσωμάτωση – Πλήρες, Εκτελέσιμο Παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια εφαρμογή console. Περιλαμβάνει διαχείριση σφαλμάτων, την προαιρετική προστασία αριθμού γραμμών και τη βοηθητική μέθοδο εκτύπωσης.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Τρέξτε το πρόγραμμα και θα δείτε τις πρώτες 100 γραμμές του φύλλου σας, ωραία στρογγυλοποιημένες, με τα ονόματα των στηλών αμετάβλητα.

## Συχνές Ερωτήσεις & Πιθανά Προβλήματα

| Ερώτηση | Απάντηση |
|----------|----------|
| **Τι γίνεται αν το φύλλο μου έχει συγχωνευμένα κελιά;** | Το `ExportDataTable` επίπεδωση (flatten) των συγχωνευμένων κελιών παίρνοντας την τιμή του πάνω‑αριστερού κελιού. Αν χρειάζεστε προσαρμοσμένη διαχείριση, αποσυγχωνεύστε πρώτα ή διαβάστε τα ακατέργαστα αντικείμενα `Cell`. |
| **Μπορώ να εξάγω σε `DataSet` αντί για `DataTable`;** | Ναι — χρησιμοποιήστε `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}