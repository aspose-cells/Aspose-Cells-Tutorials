---
category: general
date: 2026-06-27
description: Εξαγωγή πίνακα σε CSV με προσαρμοσμένες επιλογές εξαγωγής CSV σε C#.
  Μάθετε πώς το TableExportOptions και ένας διαχειριστής εξαγωγής κελιών σας επιτρέπουν
  να προσαρμόσετε την έξοδο CSV για οποιοδήποτε βιβλίο εργασίας.
draft: false
keywords:
- export table to csv
- custom CSV export
- TableExportOptions
- cell export handler
- C# workbook to CSV
language: el
og_description: Εξαγωγή πίνακα σε CSV με προσαρμοσμένες επιλογές εξαγωγής CSV σε C#.
  Αυτός ο οδηγός σας καθοδηγεί μέσω των TableExportOptions, των χειριστών εξαγωγής
  κελιών και πλήρων παραδειγμάτων κώδικα.
og_title: Εξαγωγή πίνακα σε CSV σε C# – Πλήρης Οδηγός Προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export table to CSV with custom CSV export options in C#. Learn how
    TableExportOptions and a cell export handler let you tailor CSV output for any
    workbook.
  headline: Export table to CSV in C# – Complete Programming Guide
  type: TechArticle
- description: Export table to CSV with custom CSV export options in C#. Learn how
    TableExportOptions and a cell export handler let you tailor CSV output for any
    workbook.
  name: Export table to CSV in C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code works on .NET Framework 4.6+ as well). -
      A reference to the **GemBox.Spreadsheet** NuGet package (or any library exposing
      `TableExportOptions`). - Basic familiarity with C# and CSV concepts.'
  - name: Why `ExportAsString = true`?
    text: When you set `ExportAsString` to `true`, the library treats every cell as
      text before handing it to your handler. This guarantees that numeric cells don’t
      get auto‑formatted (e.g., scientific notation) before you have a chance to prepend
      the `$`. If you leave this flag `false`, the handler might rec
  - name: Understanding the **cell export handler**
    text: The lambda receives a `cell` object that carries metadata such as `Column`,
      `Row`, and `Value`. By checking `cell.Column == 1` we target the *Price* column
      only. The `double.TryParse` guard ensures we only format legitimate numbers—avoiding
      exceptions on empty or text cells.
  - name: Null or Empty Cells
    text: If your source data contains blanks, the handler will receive `null`. The
      guard clause `if (cell == null) return string.Empty;` prevents a `NullReferenceException`.
      You can also return a placeholder like `"N/A"` if that fits your business rules.
  - name: Large Workbooks
    text: 'When dealing with thousands of rows, consider streaming the CSV to avoid
      high memory consumption:'
  - name: Different Delimiters
    text: 'If you need a semicolon (`;`) instead of a comma, adjust the `SaveOptions`:'
  type: HowTo
tags:
- CSV
- C#
- Spreadsheet
title: Εξαγωγή πίνακα σε CSV σε C# – Πλήρης Οδηγός Προγραμματισμού
url: /el/net/csv-file-handling/export-table-to-csv-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή πίνακα σε CSV με C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε ποτέ χρειαστεί να **εξάγετε πίνακα σε CSV** αλλά η προεπιλεγμένη έξοδος δεν ήταν ικανοποιητική; Ίσως θέλατε να προσθέσετε ένα σύμβολο νομίσματος, να αλλάξετε τους διαχωριστές ή να παραλείψετε ορισμένες στήλες. Σε αυτό το σεμινάριο θα σας δείξουμε ακριβώς πώς να **εξάγετε πίνακα σε CSV** χρησιμοποιώντας την ισχυρή κλάση `TableExportOptions` και έναν προσαρμοσμένο *cell export handler* — χωρίς εξωτερικά σενάρια.

Θα περάσουμε από ένα πραγματικό σενάριο: παίρνουμε ένα βιβλίο εργασίας σε στυλ λογιστικού φύλλου, τροποποιούμε τη δεύτερη στήλη ώστε κάθε τιμή να εμφανίζεται ως ποσό σε δολάρια, και στη συνέχεια αποθηκεύουμε το αποτέλεσμα ως αρχείο CSV. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο μοτίβο για οποιαδήποτε **προσαρμοσμένη εξαγωγή CSV** που μπορεί να χρειαστείτε στα έργα σας C#.

## Τι Θα Μάθετε

- Πώς να ρυθμίσετε τη μετατροπή **C# workbook to CSV** με τη βιβλιοθήκη GemBox.Spreadsheet (ή οποιοδήποτε συμβατό API).  
- Γιατί το `TableExportOptions.ExportAsString` είναι σημαντικό όταν χρειάζεστε έξοδο με βάση κείμενο.  
- Πώς να γράψετε έναν **cell export handler** που τροποποιεί τις τιμές των κελιών σε πραγματικό χρόνο.  
- Συμβουλές για τη διαχείριση ειδικών περιπτώσεων όπως κενά κελιά, διαφορετικοί τύποι δεδομένων και μεγάλα σύνολα δεδομένων.  

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+).  
- Μια αναφορά στο πακέτο NuGet **GemBox.Spreadsheet** (ή οποιαδήποτε βιβλιοθήκη που εκθέτει το `TableExportOptions`).  
- Βασική εξοικείωση με C# και τις έννοιες του CSV.  

Αν τα έχετε, ας ξεκινήσουμε.

---

## Βήμα 1: Εγκατάσταση και Αναφορά στη Βιβλιοθήκη Spreadsheet

Πρώτα, προσθέστε το πακέτο GemBox.Spreadsheet στο έργο σας. Ανοίξτε ένα τερματικό στο φάκελο της λύσης και εκτελέστε:

```bash
dotnet add package GemBox.Spreadsheet --version 131.0
```

> **Συμβουλή:** Το GemBox προσφέρει μια δωρεάν λειτουργία για έως 150 γραμμές — ιδανική για πειραματισμό πριν αγοράσετε άδεια.

Αφού επαναφερθεί το πακέτο, συμπεριλάβετε το namespace στην κορυφή του αρχείου `.cs` σας:

```csharp
using GemBox.Spreadsheet;
```

> **Γιατί είναι σημαντικό:** Ο τύπος `TableExportOptions` βρίσκεται σε αυτό το namespace· χωρίς αυτό ο μεταγλωττιστής θα εμφανίσει σφάλμα.

---

## Βήμα 2: Δημιουργία Δείγματος Βιβλίου Εργασίας με Δεδομένα

Ας δημιουργήσουμε ένα μικρό βιβλίο εργασίας που μιμείται μια τυπική αναφορά πωλήσεων. Αυτό θα μας δώσει κάτι συγκεκριμένο για εξαγωγή.

```csharp
// Initialize the library (free mode)
SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

// Create a new workbook and a worksheet
var wb = new ExcelFile();
var ws = wb.Worksheets.Add("Sales");

// Populate header row
ws.Cells[0, 0].Value = "Product";
ws.Cells[0, 1].Value = "Price";

// Add a few data rows
ws.Cells[1, 0].Value = "Laptop";
ws.Cells[1, 1].Value = 999.99;

ws.Cells[2, 0].Value = "Mouse";
ws.Cells[2, 1].Value = 25.5;

ws.Cells[3, 0].Value = "Keyboard";
ws.Cells[3, 1].Value = 45.0;
```

Η εκτέλεση αυτού του αποσπάσματος μόνη της θα σας δώσει ένα κανονικό αρχείο Excel. Ο στόχος μας, ωστόσο, είναι να **εξάγετε πίνακα σε CSV** με μια τροποποίηση: η στήλη τιμής πρέπει να προεξέχει με `$`.

## Βήμα 3: Διαμόρφωση του `TableExportOptions` για Προσαρμοσμένη Εξαγωγή CSV

Εδώ συμβαίνει η μαγεία. Το `TableExportOptions` σας επιτρέπει να ελέγχετε πώς αποδίδεται κάθε κελί, αν οι αριθμοί παραμένουν αριθμητικοί ή μετατρέπονται σε συμβολοσειρές, και ακόμη και ποιον διαχωριστή να χρησιμοποιήσετε.

```csharp
// Step 3.1: Create export options for the table
var tableExportOptions = new TableExportOptions();

// Step 3.2: Export each cell's value as a string – essential for custom formatting
tableExportOptions.ExportAsString = true;

// Step 3.3: Define a custom handler to modify cell output
//         We prepend a dollar sign only for the second column (index 1)
tableExportOptions.CellExportHandler = (cell) =>
{
    // Guard against null cells – they become empty strings
    if (cell == null) return string.Empty;

    // If we are in the Price column, format as currency
    if (cell.Column == 1 && double.TryParse(cell.Value?.ToString(), out var price))
        return "$" + price.ToString("0.00");

    // Default: return the cell's string representation
    return cell.StringValue;
};
```

### Γιατί `ExportAsString = true`;

Όταν ορίζετε το `ExportAsString` σε `true`, η βιβλιοθήκη αντιμετωπίζει κάθε κελί ως κείμενο πριν το περάσει στον χειριστή σας. Αυτό εγγυάται ότι τα αριθμητικά κελιά δεν μορφοποιούνται αυτόματα (π.χ., επιστημονική σημειογραφία) πριν έχετε την ευκαιρία να προσθέσετε το `$`. Αν αφήσετε αυτή τη σημαία `false`, ο χειριστής μπορεί να λάβει μια αριθμητική τιμή που δεν μπορείτε εύκολα να μετατρέψετε σε μορφοποιημένη συμβολοσειρά.

### Κατανόηση του **cell export handler**

Η λήψη (lambda) λαμβάνει ένα αντικείμενο `cell` που μεταφέρει μεταδεδομένα όπως `Column`, `Row` και `Value`. Ελέγχοντας `cell.Column == 1` στοχεύουμε μόνο στη στήλη *Price*. Η προστασία `double.TryParse` εξασφαλίζει ότι μορφοποιούμε μόνο έγκυρους αριθμούς — αποφεύγοντας εξαιρέσεις σε κενά ή κελιά κειμένου.

## Βήμα 4: Αποθήκευση του Βιβλίου Εργασίας ως CSV Χρησιμοποιώντας τις Προσαρμοσμένες Επιλογές

Τώρα τελικά **εξάγουμε πίνακα σε CSV** με την προσαρμοσμένη λογική μας ενσωματωμένη.

```csharp
// Define the output path – change this to your desired folder
string outputPath = Path.Combine(Environment.CurrentDirectory, "customSalesReport.csv");

// Save the worksheet as CSV using the options we configured
ws.Save(outputPath, SaveOptions.CsvDefault, tableExportOptions);

// Inform the user
Console.WriteLine($"CSV file created at: {outputPath}");
```

> **Αναμενόμενη έξοδος (`customSalesReport.csv`):**  
> ```
> Product,Price  
> Laptop,$999.99  
> Mouse,$25.50  
> Keyboard,$45.00  
> ```

Παρατηρήστε πώς κάθε τιμή τώρα έχει ένα προεξαίρετο `$` — ακριβώς αυτό που καθοδήγησε ο **cell export handler** μας.

## Βήμα 5: Διαχείριση Ειδικών Περιπτώσεων και Συνηθισμένων Παγίδων

### Κενά ή Κενά Κελιά

Αν τα δεδομένα προέλευσης περιέχουν κενά, ο χειριστής θα λάβει `null`. Η προφυλακτική εντολή `if (cell == null) return string.Empty;` αποτρέπει ένα `NullReferenceException`. Μπορείτε επίσης να επιστρέψετε έναν δείκτη όπως `"N/A"` αν ταιριάζει στους επιχειρηματικούς σας κανόνες.

### Μεγάλα Βιβλία Εργασίας

Όταν εργάζεστε με χιλιάδες γραμμές, σκεφτείτε τη ροή (streaming) του CSV για να αποφύγετε την υψηλή κατανάλωση μνήμης:

```csharp
using (var stream = new FileStream(outputPath, FileMode.Create, FileAccess.Write))
{
    ws.Save(stream, SaveOptions.CsvDefault, tableExportOptions);
}
```

### Διαφορετικοί Διαχωριστές

Αν χρειάζεστε άνω τελεία (`;`) αντί για κόμμα, προσαρμόστε το `SaveOptions`:

```csharp
var csvOptions = SaveOptions.CsvDefault;
csvOptions.Separator = ';';
ws.Save(outputPath, csvOptions, tableExportOptions);
```

Αυτή είναι μια γρήγορη επίδειξη του πόσο ευέλικτη μπορεί να είναι η **προσαρμοσμένη εξαγωγή CSV**.

## Βήμα 6: Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι ολόκληρο το πρόγραμμα ενωμένο. Επικολλήστε το σε ένα νέο έργο κονσόλας και τρέξτε το — δεν απαιτούνται επιπλέον αρχεία.

```csharp
using System;
using System.IO;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize GemBox (free mode)
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 2️⃣ Build a sample workbook
        var wb = new ExcelFile();
        var ws = wb.Worksheets.Add("Sales");

        ws.Cells[0, 0].Value = "Product";
        ws.Cells[0, 1].Value = "Price";

        ws.Cells[1, 0].Value = "Laptop";
        ws.Cells[1, 1].Value = 999.99;

        ws.Cells[2, 0].Value = "Mouse";
        ws.Cells[2, 1].Value = 25.5;

        ws.Cells[3, 0].Value = "Keyboard";
        ws.Cells[3, 1].Value = 45.0;

        // 3️⃣ Configure export options (custom CSV export)
        var tableExportOptions = new TableExportOptions
        {
            ExportAsString = true,
            CellExportHandler = (cell) =>
            {
                if (cell == null) return string.Empty;
                if (cell.Column == 1 && double.TryParse(cell.Value?.ToString(), out var price))
                    return "$" + price.ToString("0.00");
                return cell.StringValue;
            }
        };

        // 4️⃣ Save as CSV
        string outputPath = Path.Combine(Environment.CurrentDirectory, "customSalesReport.csv");
        ws.Save(outputPath, SaveOptions.CsvDefault, tableExportOptions);

        Console.WriteLine($"✅ CSV created at: {outputPath}");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το `customSalesReport.csv` σε οποιονδήποτε επεξεργαστή κειμένου, και θα δείτε την ωραία μορφοποιημένη έξοδο.

## Συμπέρασμα

Τώρα έχετε ένα σταθερό, επαναχρησιμοποιήσιμο μοτίβο για **εξαγωγή πίνακα σε CSV** με C#. Χρησιμοποιώντας το `TableExportOptions` και έναν **cell export handler**, μπορείτε να ενσωματώσετε οποιαδήποτε προσαρμοσμένη λογική — σύμβολα νομισμάτων, μορφές ημερομηνίας, υπό όρους απόκρυψη, ό,τι θέλετε. Αυτή η προσέγγιση λειτουργεί για μικρές αναφορές και κλιμακώνεται σε τεράστιες εξαγωγές δεδομένων όταν συνδυάζεται με streaming.

Τι θα ακολουθήσει; Δοκιμάστε να αντικαταστήσετε το `$` με άλλα πρόθεματα, να εξάγετε ημερομηνίες σε μορφή ISO, ή ακόμη και να δημιουργήσετε πολλαπλά αρχεία CSV από διαφορετικά φύλλα εργασίας στο ίδιο βιβλίο. Οι ίδιες αρχές **προσαρμοσμένης εξαγωγής CSV** ισχύουν.

Έχετε ερωτήσεις σχετικά με ειδικές περιπτώσεις όπως πολυγλωσσικά δεδομένα ή ειδικούς χαρακτήρες; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω σεμινάρια καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Load CSV & Export to JSON Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/spanish/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}