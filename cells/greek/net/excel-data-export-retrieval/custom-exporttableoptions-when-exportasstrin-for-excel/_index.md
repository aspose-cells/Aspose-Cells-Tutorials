---
category: general
date: 2026-10-26
description: Προσαρμοσμένες επιλογές ExportTableOptions όταν το ExportAsStrin σας
  επιτρέπει να εξάγετε δεδομένα Excel ως συμβολοσειρές σε C#. Ακολουθήστε τον οδηγό
  βήμα‑βήμα για να διαμορφώσετε και να εκτελέσετε την εξαγωγή.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: el
lastmod: 2026-10-26
og_description: Προσαρμοσμένες ExportTableOptions όταν το ExportAsStrin ενεργοποιεί
  εξαγωγή Excel μόνο με συμβολοσειρές. Μάθετε τα ακριβή βήματα για τη διαμόρφωση και
  την εκτέλεση της εξαγωγής σε C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Προσαρμοσμένες ExportTableOptions όταν ExportAsString – εξαγωγή Excel ως
  συμβολοσειρά σε C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Προσαρμοσμένες επιλογές ExportTableOptions όταν ExportAsStrin για Excel
url: /el/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – εξαγωγή Excel ως string σε C#

Αν χρειάζεστε **Custom ExportTableOptions when ExportAsStrin** για να λαμβάνετε κάθε τιμή κελιού ως απλό string, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Είτε χτίζετε μια διαδικασία εισαγωγής δεδομένων είτε χρειάζεστε ένα καθαρό dump έτοιμο για CSV, θα δείτε γιατί η ρύθμιση των επιλογών με αυτόν τον τρόπο αποφεύγει εκπλήξεις μετατροπής τύπων.

Σε αυτό το tutorial θα μάθετε **πώς να εξάγετε excel ως string** χρησιμοποιώντας τη βιβλιοθήκη Aspose.Cells, θα δείτε τον πλήρη, εκτελέσιμο κώδικα, και θα κατανοήσετε τη λογική πίσω από κάθε ρύθμιση. Δεν απαιτείται εξωτερική τεκμηρίωση – όλα όσα χρειάζεστε είναι εδώ.

## Prerequisites

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 SDK ή νεότερο εγκατεστημένο  
* Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει .NET)  
* Πακέτο Aspose.Cells for .NET (εγκατάσταση μέσω NuGet: `Install-Package Aspose.Cells`)  
* Ένα Excel workbook (`sample.xlsx`) τοποθετημένο στο ριζικό φάκελο του έργου  

Αυτά είναι τα μόνα εξαρτήματα· ο κώδικας εκτελείται σε Windows, Linux ή macOS χωρίς πρόσθετες βιβλιοθήκες.

## Step 1: Load the workbook you want to export

Το πρώτο βήμα όταν χρησιμοποιείτε **Custom ExportTableOptions when ExportAsStrin** είναι να αποκτήσετε ένα αντικείμενο `Worksheet` από ένα φορτωμένο workbook. Αυτό το αντικείμενο σας δίνει πρόσβαση σε γραμμές, στήλες και το API εξαγωγής.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Γιατί είναι σημαντικό:*  
`Workbook` διαβάζει το αρχείο μία φορά και διατηρεί όλες τις πληροφορίες μορφοποίησης στη μνήμη. Επιλέγοντας ένα συγκεκριμένο `Worksheet`, περιορίζετε το πεδίο εξαγωγής και αποφεύγετε την επεξεργασία κρυφών φύλλων.

## Step 2: Configure ExportTableOptions with ExportAsString = true

Ο πυρήνας του **Custom ExportTableOptions when ExportAsStrin** είναι το αντικείμενο `ExportTableOptions`. Ορίζοντας `ExportAsString` εξαναγκάζει τον εξαγωγέα να αντιμετωπίζει κάθε κελί ως string, ανεξάρτητα από τον αρχικό του τύπο δεδομένων (ημερομηνία, αριθμός, boolean κ.λπ.). Η ενεργοποίηση του `PreserveFormatting` διατηρεί το οπτικό στυλ (π.χ. σύμβολα νομισμάτων) στο παραγόμενο string.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Γιατί είναι σημαντικό:*  
Όταν καλέσετε αργότερα το `ExportDataTable`, η βιβλιοθήκη κανονικά προσπαθεί να προβλέψει τον τύπο .NET κάθε στήλης. Με `ExportAsString = true`, αυτό το βήμα παραλείπεται, αποτρέποντας ανεπιθύμητες μετατροπές `DateTime` ή `double` που μπορούν να σπάσουν τους επόμενους επεξεργαστές CSV.

## Step 3: Export a range to a DataTable using the custom options

Τώρα μπορείτε να εξάγετε ένα ορθογώνιο εύρος (γραμμές 0‑9, στήλες 0‑4) από το worksheet. Η μέθοδος επιστρέφει ένα `DataTable` όπου κάθε πεδίο είναι `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Γιατί είναι σημαντικό:*  
`ExportDataTable` είναι ο πιο βολικός τρόπος για να μεταφέρετε δεδομένα Excel σε μια σχεσιακή δομή που πολλές .NET APIs ήδη κατανοούν (π.χ. Entity Framework, Dapper). Με τη χρήση του **Custom ExportTableOptions when ExportAsStrin**, εξασφαλίζετε ότι κάθε `DataColumn.DataType` θα είναι `typeof(string)`.

## Step 4: Verify the result – all values are strings

Είναι καλή πρακτική να επιβεβαιώσετε ότι η εξαγωγή λειτουργεί όπως αναμένεται. Ο παρακάτω βρόχος εκτυπώνει κάθε κελί και τον τύπο του κατά το χρόνο εκτέλεσης.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Αναμενόμενη έξοδος**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Κάθε κελί εμφανίζει `String` ως τύπο του, επιβεβαιώνοντας ότι το **Custom ExportTableOptions when ExportAsStrin** λειτούργησε σωστά.

## Step 5: Optional – write the DataTable to CSV

Αν ο τελικός σας στόχος είναι ένα αρχείο απλού κειμένου, μπορείτε εύκολα να σειριοποιήσετε το `DataTable` σε CSV:



## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Export Custom Properties Excel Pdf Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}