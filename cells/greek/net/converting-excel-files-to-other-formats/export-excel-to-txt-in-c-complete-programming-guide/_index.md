---
category: general
date: 2026-08-11
description: Εξαγωγή Excel σε txt σε C# με οδηγό βήμα‑βήμα. Μάθετε πώς να μετατρέψετε
  xlsx σε απλό κείμενο χρησιμοποιώντας το Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: el
lastmod: 2026-08-11
og_description: Εξαγωγή Excel σε txt σε C# γρήγορα. Αυτό το σεμινάριο δείχνει πώς
  να μετατρέψετε xlsx σε απλό κείμενο, να διαμορφώσετε μορφές και να διαχειριστείτε
  μεγάλα φύλλα εργασίας.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: Εξαγωγή Excel σε txt σε C# – βήμα‑βήμα οδηγός για προγραμματιστές
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: Εξαγωγή Excel σε txt σε C# – πλήρης οδηγός προγραμματισμού
url: /el/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή excel σε txt σε C# – πλήρης προγραμματιστικός οδηγός

Αν χρειάζεστε **εξαγωγή excel σε txt** μπορείτε να πετύχετε το αποτέλεσμα με λίγες γραμμές κώδικα C#. Αυτός ο οδηγός δείχνει πώς να μετατρέψετε ένα βιβλίο εργασίας `.xlsx` σε αρχείο απλού κειμένου διατηρώντας τη μορφή δεδομένων που ορίζετε.

Η εξαγωγή φύλλων εργασίας ως αρχεία κειμένου είναι συχνή απαίτηση όταν τα επόμενα συστήματα δέχονται μόνο διαχωρισμένα δεδομένα ή όταν πρέπει να ελέγξετε τις ακατέργαστες τιμές κελιών. Στις παρακάτω ενότητες θα μάθετε πώς να ρυθμίσετε μορφές ημερομηνίας και αριθμού, να διαχειριστείτε μεγάλα φύλλα και να αποφύγετε τυπικά προβλήματα.

## Προαπαιτούμενα για μετατροπή xlsx σε απλό κείμενο

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 (ή νεότερο) εγκατεστημένο – ο κώδικας στοχεύει στο .NET Standard 2.0, οπότε λειτουργεί και με .NET Framework 4.6+.
* Άδεια για **Aspose.Cells** (η δωρεάν αξιολόγηση λειτουργεί για δοκιμές).
* Ένα IDE όπως το Visual Studio 2022 ή το Visual Studio Code.
* Ένα αρχείο Excel με όνομα `input.xlsx` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από το πρόγραμμά σας.

Αυτά τα στοιχεία είναι οι μόνες εξωτερικές απαιτήσεις· το tutorial δεν εξαρτάται από πρόσθετα πακέτα NuGet.

## Πώς να εξάγετε excel σε txt χρησιμοποιώντας Aspose.Cells

Το Aspose.Cells παρέχει την κλάση `ExportTableOptions` που σας επιτρέπει να ελέγχετε πώς οι τιμές κελιών αποδίδονται ως συμβολοσειρές. Ορίζοντας το `ExportAsString` σε `true` εξαναγκάζετε κάθε κελί να γραφτεί ως κείμενο, κάτι που είναι απαραίτητο όταν θέλετε καθορισμένο αποτέλεσμα απλού κειμένου.

### Βήμα 1 – φόρτωση του βιβλίου εργασίας

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*Ο κατασκευαστής `Workbook` διαβάζει το αρχείο Excel στη μνήμη. Αν το αρχείο δεν υπάρχει, ρίχνεται εξαίρεση, οπότε ίσως θελήσετε να τυλίξετε αυτή την κλήση σε μπλοκ try‑catch για κώδικα παραγωγής.*

### Βήμα 2 – λήψη του πρώτου φύλλου εργασίας

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*Τα φύλλα εργασίας είναι μηδενικής βάσης, επομένως το index 0 αναφέρεται στην πρώτη καρτέλα. Μπορείτε να αντικαταστήσετε το index με όνομα φύλλου (`workbook.Worksheets["Sheet1"]`) όταν χρειάζεται να στοχεύσετε συγκεκριμένη καρτέλα.*

### Βήμα 3 – ορισμός επιλογών εξαγωγής για μετατροπή σε κείμενο

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*Το `ExportAsString` εγγυάται ότι κάθε κελί, ανεξαρτήτως αρχικού τύπου, γίνεται συμβολοσειρά στο αρχείο εξόδου. Οι ιδιότητες `DateTimeFormat` και `NumberFormat` σας επιτρέπουν να ελέγχετε πώς εμφανίζονται οι ημερομηνίες και οι αριθμοί, κάτι κρίσιμο όταν **μετατρέπετε xlsx σε απλό κείμενο** για συστήματα που αναμένουν συγκεκριμένο πρότυπο.*

### Βήμα 4 – εξαγωγή φύλλου εργασίας ως αρχείο κειμένου

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*Το `ExportDataTable` γράφει το περιεχόμενο του φύλλου εργασίας σε αρχείο απλού κειμένου χρησιμοποιώντας τις επιλογές που δώσατε. Ο προεπιλεγμένος διαχωριστής είναι το χαρακτήρα tab (`\t`). Αν χρειάζεστε διαφορετικό διαχωριστή, μπορείτε να χρησιμοποιήσετε την υπερφόρτωση που δέχεται ένα αντικείμενο `ExportTableOptions` και να ορίσετε `ExportTableOptions.Separator`. Το παραγόμενο αρχείο μπορεί να ανοιχθεί σε οποιονδήποτε επεξεργαστή κειμένου ή να εισαχθεί σε βάση δεδομένων.*

#### Αναμενόμενο αποτέλεσμα

Υποθέτουμε ότι το `input.xlsx` περιέχει:

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

Με τις παραπάνω επιλογές το αρχείο `Exported.txt` θα περιέχει:

```
2023-05-01	1,234.50	Sample text
```

Κάθε στήλη διαχωρίζεται με tab, οι ημερομηνίες ακολουθούν το `yyyy‑MM‑dd`, και οι αριθμοί χρησιμοποιούν κόμμα ως διαχωριστικό χιλιάδων και δύο δεκαδικά ψηφία.

## Συνηθισμένα προβλήματα όταν εξάγετε φύλλο εργασίας ως αρχείο κειμένου

| Πρόβλημα | Γιατί συμβαίνει | Πώς να το αποφύγετε |
|----------|------------------|----------------------|
| Μορφοποίηση αριθμών εξαρτημένη από τοπική ρύθμιση | Η προεπιλεγμένη μορφή σέβεται την πολιτισμική ρύθμιση του λειτουργικού συστήματος, που μπορεί να παράγει κόμματα ή τελείες ασυνεπώς. | Ορίστε ρητά το `NumberFormat` στο `ExportTableOptions`. |
| Κρυφές γραμμές ή στήλες εμφανίζονται στην έξοδο | Το Aspose.Cells εξάγει όλο το χρησιμοποιημένο εύρος, συμπεριλαμβανομένων των κρυφών γραμμών. | Ορίστε `ExportTableOptions.ExportHiddenRows = false` και `ExportHiddenColumns = false` αν θέλετε να τις παραλείψετε. |
| Μεγάλα φύλλα εργασίας προκαλούν πίεση μνήμης | Ολόκληρο το βιβλίο εργασίας φορτώνεται στη μνήμη πριν την εξαγωγή. | Χρησιμοποιήστε `Workbook.LoadOptions` με `LoadDataOnly = true` για μείωση χρήσης μνήμης, ή επεξεργαστείτε το αρχείο σε τμήματα. |
| Κελιά ημερομηνίας αποθηκευμένα ως κείμενο στο αρχικό αρχείο | Αν ένα κελί περιέχει ήδη μορφοποιημένη συμβολοσειρά, ο εξαγωγέας το θεωρεί κείμενο και αγνοεί το `DateTimeFormat`. | Βεβαιωθείτε ότι το αρχικό βιβλίο εργασίας αποθηκεύει τις ημερομηνίες ως πραγματικούς τύπους ημερομηνίας του Excel. |

Η αντιμετώπιση αυτών των ζητημάτων κάνει τη **διαδικασία εξαγωγής φύλλου εργασίας excel ως κείμενο** αξιόπιστη σε διαφορετικά περιβάλλοντα.

## Επέκταση της λύσης – προσαρμοσμένοι διαχωριστές και εξαγωγή με ροή

Αν χρειάζεστε αρχείο τιμών διαχωρισμένων με κόμμα (CSV) αντί για αρχείο διαχωρισμένο με tab, τροποποιήστε τις επιλογές:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

Για αρχεία μεγαλύτερα από 500 MB, η εξαγωγή με ροή αποτρέπει την εξάντληση της RAM:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

Η υπερφόρτωση που δέχεται ένα `Stream` γράφει τις γραμμές σταδιακά, ιδανική για batch jobs ή web services που επιστρέφουν το αρχείο κειμένου απευθείας σε πελάτη.

## Επαλήθευση του αποτελέσματος προγραμματιστικά

Μετά την ολοκλήρωση της εξαγωγής μπορείτε να διαβάσετε την πρώτη γραμμή ξανά στη μνήμη για να επιβεβαιώσετε τη μορφή:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

Η εκτέλεση αυτού του αποσπάσματος θα πρέπει να εκτυπώσει την ίδια γραμμή που φαίνεται στην ενότητα *Αναμενόμενο αποτέλεσμα*, δίνοντάς σας σιγουριά ότι η μετατροπή πέτυχε.

## Ανακεφαλαίωση του πλήρους κώδικα

Συνδυάζοντας όλα τα κομμάτια προκύπτει ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε σε μια εφαρμογή console:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Συγκροτήστε και τρέξτε το πρόγραμμα· το αρχείο `Exported.txt` θα εμφανιστεί στον ίδιο φάκελο με το πηγαίο βιβλίο εργασίας.

## Επόμενα βήματα και συναφή θέματα

* **Export worksheet as text file** – πειραματιστείτε με διαφορετικούς διαχωριστές, κωδικοποιήσεις (UTF‑8 vs. ASCII) και στυλ λήξης γραμμής για συμβατότητα μεταξύ πλατφορμών.
* **Bulk conversion** – κάντε βρόχο στα `workbook.Worksheets` για να δημιουργήσετε ξεχωριστό αρχείο κειμένου για κάθε καρτέλα.
* **Integration with databases** – διοχετεύστε το παραγόμενο κείμενο απευθείας σε λειτουργία bulk‑insert για SQL Server ή PostgreSQL.
* 

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα επεξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to Export Excel Files in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}