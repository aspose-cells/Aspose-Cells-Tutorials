---
category: general
date: 2026-06-17
description: Μετατρέψτε το φύλλο εργασίας σε DataTable σε C# γρήγορα. Μάθετε πώς να
  διαβάζετε αρχείο Excel σε DataTable C# και να εξάγετε Excel σε DataTable C# με πραγματικό
  κώδικα.
draft: false
keywords:
- convert worksheet to datatable
- read excel file into datatable c#
- load excel workbook c#
- export excel to datatable c#
language: el
og_description: Μετατρέψτε το φύλλο εργασίας σε DataTable σε C# γρήγορα. Αυτό το σεμινάριο
  δείχνει πώς να διαβάσετε αρχείο Excel σε DataTable C# και να εξάγετε το Excel σε
  DataTable C# με πλήρες παράδειγμα.
og_title: Μετατροπή φύλλου εργασίας σε DataTable σε C# – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Convert worksheet to DataTable in C# quickly. Learn how to read Excel
    file into DataTable C# and export Excel to DataTable C# with real code.
  headline: Convert Worksheet to DataTable in C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Μετατροπή φύλλου εργασίας σε DataTable σε C# – Πλήρης οδηγός προγραμματισμού
url: /el/net/excel-data-import-export/convert-worksheet-to-datatable-in-c-complete-programming-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή Φύλλου Εργασίας σε DataTable σε C# – Πλήρης Οδηγός Προγραμματισμού

Κάποτε χρειάστηκε να **convert worksheet to DataTable** αλλά δεν ήξερες ποιο API να καλέσεις; Δεν είσαι μόνος σου—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν αυτοματοποιούν αναφορές ή τροφοδοτούν δεδομένα Excel σε βάση δεδομένων. Τα καλά νέα; Με λίγες γραμμές C# μπορείς να διαβάσεις ένα αρχείο Excel σε ένα `DataTable` και να είσαι έτοιμος να εκτελέσεις ερωτήματα LINQ, μαζικές εισαγωγές ή ό,τι ακολουθεί.

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα τη φόρτωση ενός βιβλίου εργασίας Excel, την ανάκτηση του πρώτου φύλλου και το **export excel to DataTable C#**—χωρίς μαγεία, μόνο καθαρός κώδικας. Στο τέλος θα έχεις μια επαναχρησιμοποιήσιμη μέθοδο που μετατρέπει οποιοδήποτε φύλλο εργασίας σε πλήρως τυποποιημένο `DataTable`. (Και ναι, θα καλύψουμε επίσης το σενάριο “read Excel file into DataTable C#” για όσους προτιμούν μια γραμμή κώδικα.)

## Προαπαιτούμενα – Τι Θα Χρειαστείς

Πριν ξεκινήσουμε, βεβαιώσου ότι έχεις:

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί και σε .NET Framework 4.6+)
- Αναφορά στο **Aspose.Cells** (ή οποιαδήποτε άλλη βιβλιοθήκη που προσφέρει `ExportDataTable`; το παράδειγμα χρησιμοποιεί Aspose επειδή είναι απλό)
- Ένα αρχείο Excel (`.xlsx`) που θέλεις να επεξεργαστείς
- Ένα βασικό IDE C# (Visual Studio, Rider ή VS Code)

Αυτό είναι όλο—δεν χρειάζονται επιπλέον πακέτα NuGet εκτός από τη βιβλιοθήκη Excel. Έτοιμος; Πάμε.

## Βήμα 1: Φόρτωση Βιβλίου Εργασίας Excel C# – Φέρνουμε το Αρχείο στη Μνήμη

Πρώτο πράγμα: πρέπει να **load excel workbook c#**. Σκέψου το βιβλίο εργασίας ως το δοχείο που κρατά όλα τα φύλλα, τα στυλ και τα μεταδεδομένα. Το άνοιγμα του σωστά εξασφαλίζει ότι δεν κλειδώνουμε το αρχείο ή δεν διαρρέουμε πόρους.

```csharp
using Aspose.Cells;
using System.Data;

// Path to your input file – change as needed
string excelPath = @"C:\Data\input.xlsx";

// Load the workbook; the constructor reads the file into memory
Workbook workbook = new Workbook(excelPath);
```

> **Γιατί είναι σημαντικό:** Η κλάση `Workbook` αφαιρεί την ανάγκη να αναλύεις το χαμηλού επιπέδου format XML. Επίσης απελευθερώνει το υποκείμενο stream όταν το αντικείμενο βγει εκτός εμβέλειας, αποτρέποντας σφάλματα “αρχείο σε χρήση”.

### Συμβουλή
Αν δουλεύεις με τεράστια λογιστικά φύλλα, σκέψου τη χρήση `LoadOptions` για **memory‑optimized loading**:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook workbook = new Workbook(excelPath, options);
```

## Βήμα 2: Πρόσβαση στο Επιθυμητό Φύλλο – Συνήθως το Πρώτο

Τα περισσότερα γρήγορα σενάρια παίρνουν το πρώτο φύλλο, αλλά μπορείς να επιλέξεις οποιοδήποτε με όνομα ή δείκτη. Εδώ είναι η κλασική προσέγγιση “πρώτο φύλλο εργασίας”, η οποία καλύπτει το **convert worksheet to DataTable** για απλά αρχεία.

```csharp
// Grab the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Optional: verify the sheet isn’t empty
if (sheet.Cells.MaxDataRow < 0 || sheet.Cells.MaxDataColumn < 0)
{
    throw new InvalidOperationException("The worksheet appears to be empty.");
}
```

> **Edge case:** Αν το βιβλίο εργασίας σου περιέχει κρυφά φύλλα ή χρειάζεσαι συγκεκριμένη καρτέλα, αντικατέστησε το `0` με `workbook.Worksheets["MySheet"]`.

## Βήμα 3: Διαμόρφωση Επιλογών Εξαγωγής – Export As String για Προβλέψιμους Τύπους

Κατά τη μετατροπή σε `DataTable`, συχνά θέλουμε κάθε κελί ως συμβολοσειρά ώστε να αποφύγουμε προβλήματα μετατροπής τύπων αργότερα. Αυτό ακριβώς κάνει η σημαία **export excel to datatable c#**.

```csharp
// Set up options so every cell is treated as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true   // forces string output for all cells
};
```

Γιατί να εξαναγκάσουμε τις συμβολοσειρές; Επειδή τα κελιά Excel μπορούν να περιέχουν ημερομηνίες, αριθμούς ή τύπους. Εξάγοντας τα πάντα ως κείμενο αποφεύγουμε ασυμφωνίες τύπων στη στήλη όταν αργότερα εισάγουμε τα δεδομένα σε πίνακα SQL.

## Βήμα 4: Εκτέλεση της Εξαγωγής – Ο Πυρήνας της Λογικής Convert Worksheet to DataTable

Τώρα συμβαίνει η “μαγεία”. Καλούμε `ExportDataTable` στο αντικείμενο `Worksheet`, περνώντας τη γραμμή/στήλη εκκίνησης, τον συνολικό αριθμό γραμμών/στηλών, μια σημαία για την ένταξη των επικεφαλίδων στηλών και τις επιλογές μας.

```csharp
// Determine the used range
int totalRows = sheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int totalCols = sheet.Cells.MaxDataColumn + 1;   // +1 for the same reason

// Export the used range to a DataTable
DataTable dataTable = sheet.ExportDataTable(
    0,                 // start row (0‑based)
    0,                 // start column (0‑based)
    totalRows,
    totalCols,
    true,              // include column names as first row
    exportOptions);
```

### Τι παίρνεις
`dataTable` τώρα αντικατοπτρίζει το φύλλο εργασίας:

| Column1 | Column2 | Column3 |
|---------|---------|---------|
| Row1‑A  | Row1‑B  | Row1‑C  |
| Row2‑A  | Row2‑B  | Row2‑C  |
| …       | …       | …       |

Όλες οι τιμές είναι συμβολοσειρές, κάνοντας την επεξεργασία πιο προβλέψιμη.

## Βήμα 5: Επαλήθευση Αποτελέσματος – Γρήγορος Έλεγχος (read excel file into datatable c#)

Ένας γρήγορος τρόπος να επιβεβαιώσεις ότι η μετατροπή πέτυχε είναι να εκτυπώσεις τις πρώτες λίγες γραμμές στην κονσόλα. Αυτό δείχνει επίσης το πρότυπο **read excel file into datatable c#** σε πράξη.

```csharp
Console.WriteLine("First 5 rows of the imported DataTable:");
for (int i = 0; i < Math.Min(5, dataTable.Rows.Count); i++)
{
    var row = dataTable.Rows[i];
    Console.WriteLine(string.Join(" | ", row.ItemArray));
}
```

Αν δεις τις αναμενόμενες τιμές χωρισμένες με pipe, ολοκλήρωσες επιτυχώς το **convert worksheet to DataTable**.

## Βήμα 6: Συσκευασία – Μια Επαναχρησιμοποιήσιμη Μέθοδος Βοηθού

Τα περισσότερα έργα θα χρειαστούν αυτή τη μετατροπή σε πολλά σημεία, οπότε ας τοποθετήσουμε τα πάντα σε μια στατική μέθοδο. Έτσι η κλήση **read excel file into datatable c#** γίνεται με μία γραμμή.

```csharp
public static DataTable WorksheetToDataTable(string filePath, int sheetIndex = 0, bool exportAsString = true)
{
    // Load the workbook
    Workbook wb = new Workbook(filePath);

    // Grab the requested sheet
    Worksheet ws = wb.Worksheets[sheetIndex];

    // Prepare export options
    ExportTableOptions opts = new ExportTableOptions
    {
        ExportAsString = exportAsString
    };

    // Determine used range
    int rows = ws.Cells.MaxDataRow + 1;
    int cols = ws.Cells.MaxDataColumn + 1;

    // Export and return
    return ws.ExportDataTable(0, 0, rows, cols, true, opts);
}
```

Παράδειγμα χρήσης:

```csharp
DataTable myTable = WorksheetToDataTable(@"C:\Data\input.xlsx");
```

Αυτή είναι η πλήρης ιστορία—χωρίς επιπλέον βρόχους, χωρίς COM interop, μόνο καθαρά, τυποποιημένα δεδομένα.

## Συνηθισμένα Πιθανά Προβλήματα & Πώς να τα Αποφύγεις

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Το αρχείο κλειδωμένο από άλλη διεργασία** | Το άνοιγμα του βιβλίου χωρίς `LoadOptions` μπορεί να κρατήσει ανοιχτό το handle του αρχείου. | Χρησιμοποίησε `LoadOptions` με `MemorySetting.MemoryPreference` ή τυλίξτε το `Workbook` σε `using`. |
| **Απουσία επικεφαλίδων στηλών** | Αν η πρώτη γραμμή περιέχει δεδομένα αντί για επικεφαλίδες, το `ExportDataTable` θα τις θεωρήσει δεδομένα. | Πέρασε `false` στην παράμετρο `includeColumnNames` και πρόσθεσε τα ονόματα στηλών χειροκίνητα. |
| **Μικτοί τύποι δεδομένων προκαλούν εξαιρέσεις** | Όταν `ExportAsString` είναι `false`, τα αριθμητικά κελιά γίνονται `double`, οι ημερομηνίες `DateTime`. | Κράτησε `ExportAsString = true` εκτός αν χρειάζεσαι ισχυρή τυποποίηση, τότε διαχειρίσου τις μετατροπές εσύ. |
| **Πολύ μεγάλα φύλλα προκαλούν OutOfMemory** | Η εξαγωγή εκατομμυρίων γραμμών ταυτόχρονα μπορεί να γεμίσει τη μνήμη. | Εξάγαγε σε τμήματα: κάνε βρόχο πάνω σε μπλοκ γραμμών και συνέθεσε τα `DataTable`. |

## Bonus: Εξαγωγή Πολλαπλών Φύλλων Ταυτόχρονα

Αν χρειάζεται να **export excel to datatable c#** για κάθε φύλλο, απλώς επανάλαβε πάνω στο `workbook.Worksheets`:

```csharp
var tables = new Dictionary<string, DataTable>();
foreach (Worksheet ws in workbook.Worksheets)
{
    tables[ws.Name] = ws.ExportDataTable(
        0, 0,
        ws.Cells.MaxDataRow + 1,
        ws.Cells.MaxDataColumn + 1,
        true,
        exportOptions);
}
```

Τώρα το `tables` περιέχει ένα `DataTable` ανά φύλλο, κλειδωμένο με το όνομα του φύλλου—χρήσιμο για μαζικές εισαγωγές.

## Συμπέρασμα

Σε πήγαμε από ένα κενό αρχείο Excel σε ένα πλήρως γεμάτο `DataTable` με μια σύντομη, **convert worksheet to DataTable** ροή εργασίας. Τα βήματα κάλυψαν τη φόρτωση του βιβλίου, την επιλογή του φύλλου, τη διαμόρφωση των επιλογών εξαγωγής και, τέλος, την ανάκτηση των δεδομένων σε `DataTable`. Με τη βοηθητική μέθοδο μπορείς τώρα να **read excel file into datatable c#** οπουδήποτε στον κώδικά σου, και έχεις επίσης ένα πρότυπο για **export excel to datatable c#** σε πολλαπλά φύλλα.

Τι έπεται; Δοκίμασε να τροφοδοτήσεις το `DataTable` σε `BulkInsert` του Entity Framework, να δημιουργήσεις αναφορές CSV ή να εφαρμόσεις φίλτρα LINQ για εξαγωγή πληροφοριών. Οι δυνατότητες είναι ατελείωτες μόλις τα δεδομένα Excel ζήσουν στη μνήμη ως σωστός πίνακας.

Έχεις ερωτήσεις ή ένα δύσκολο αρχείο Excel που δεν μπορείς να σπάσεις; Άφησε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Μάθεις Στη Σειρά Επόμενη;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές του παρόντος οδηγού. Κάθε πόρος περιλαμβάνει πλήρη κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσεις επιπλέον δυνατότητες API και να εξερευνήσεις εναλλακτικές προσεγγίσεις στα δικά σου έργα.

- [Πώς να Εισάγετε DataTable σε Excel Χρησιμοποιώντας Aspose.Cells για .NET (Βήμα‑Βήμα Οδηγός)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Εξαγωγή Δεδομένων Excel σε DataTable Χρησιμοποιώντας Aspose.Cells για .NET: Πλήρης Οδηγός](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Εξαγωγή HTML Strings από Excel σε DataTable χρησιμοποιώντας Aspose.Cells για .NET: Βήμα‑Βήμα Οδηγός](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}