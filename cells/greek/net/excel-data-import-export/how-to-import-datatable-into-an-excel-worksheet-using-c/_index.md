---
category: general
date: 2026-10-26
description: Μάθετε πώς να εισάγετε ένα DataTable σε ένα φύλλο εργασίας Excel με C#
  και Aspose.Cells, διατηρώντας τα στυλ και τις κεφαλίδες σε λίγες μόνο γραμμές κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: el
lastmod: 2026-10-26
og_description: πώς να εισάγετε datatable σε ένα φύλλο Excel χρησιμοποιώντας C# και
  Aspose.Cells. Ακολουθήστε αυτόν τον πλήρη οδηγό για να διατηρήσετε τα στυλ, τις
  κεφαλίδες και τη μορφοποίηση.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Πώς να εισάγετε DataTable σε ένα φύλλο εργασίας Excel – Οδηγός βήμα‑βήμα
  για C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Πώς να εισάγετε DataTable σε ένα φύλλο εργασίας Excel χρησιμοποιώντας C#
url: /el/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εισάγετε DataTable σε ένα φύλλο εργασίας Excel χρησιμοποιώντας C#

Αν χρειάζεστε **how to import datatable** σε ένα φύλλο εργασίας Excel, αυτός ο οδηγός δείχνει τα ακριβή βήματα σε C#. Είτε δημιουργείτε μια μηχανή αναφορών είτε εξάγετε δεδομένα πλέγματος, θα δείτε πώς να διατηρήσετε τις επικεφαλίδες των στηλών και τα στυλ των κελιών αμετάβλητα με το Aspose.Cells. Η λύση λειτουργεί με .NET 6+ και απαιτεί μόνο λίγες γραμμές κώδικα.

Η εισαγωγή ενός DataTable είναι μια κοινή εργασία όταν δουλεύετε με υπολογιστικά φύλλα, αλλά οι προγραμματιστές συχνά ξεχνούν να ενεργοποιήσουν τη μεταφορά στυλ ή να περάσουν σωστά τη σημαία των επικεφαλίδων. Σε αυτό το tutorial θα μάθετε πώς να διαμορφώσετε το **ImportTableOptions**, να ενεργοποιήσετε το **ImportDataTableStyle**, και να καλέσετε το `ImportDataTable` με ασφάλεια. Στο τέλος θα έχετε μια μέθοδο έτοιμη για εκτέλεση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C#.

## Προαπαιτούμενα

* .NET 6 SDK ή νεότερη έκδοση εγκατεστημένη.
* Αντίγραφο με άδεια του **Aspose.Cells for .NET** (η δωρεάν δοκιμή λειτουργεί για δοκιμές).
* Βασική εξοικείωση με το `DataTable` και τις έννοιες του Excel.
* Ένα IDE όπως το Visual Studio 2022 (οποιοσδήποτε επεξεργαστής που υποστηρίζει C# λειτουργεί).

Δεν απαιτούνται πρόσθετα πακέτα NuGet πέρα από το `Aspose.Cells`.

## Βήμα 1: Ανάκτηση των πηγαίων δεδομένων σε ένα DataTable

Το πρώτο πράγμα που κάνετε όταν απαντάτε **how to import datatable** είναι να έχετε τα δεδομένα έτοιμα. Στις περισσότερες πραγματικές περιπτώσεις το `DataTable` προέρχεται από ένα ερώτημα βάσης δεδομένων, έναν αναλυτή CSV ή μια συλλογή στη μνήμη. Ακολουθεί ένα ελάχιστο παράδειγμα που δημιουργεί έναν πίνακα με μερικές γραμμές:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Γιατί αυτό είναι σημαντικό*: Δημιουργώντας πρώτα το `DataTable`, ελέγχετε τη σειρά των στηλών, τους τύπους δεδομένων και τα ονόματα των επικεφαλίδων — όλα αυτά διατηρούνται όταν αργότερα εισάγετε τον πίνακα σε ένα φύλλο εργασίας Excel.

## Βήμα 2: Δημιουργία του `ImportTableOptions` και ενεργοποίηση της εισαγωγής στυλ

Όταν απαντάτε **how to import datatable**, η επόμενη απόφαση είναι αν θέλετε το οπτικό στυλ (γραμματοσειρές, χρώματα, περιγράμματα) που μπορεί ήδη να είναι ορισμένο στο πηγαίο `DataTable`. Το Aspose.Cells παρέχει την κλάση `ImportTableOptions` για λεπτομερή έλεγχο. Ορίζοντας `ImportDataTableStyle = true` αντιγράφει τις πληροφορίες στυλ στο φύλλο προορισμού.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Γιατί αυτό είναι σημαντικό*: Χωρίς την ενεργοποίηση του `ImportDataTableStyle`, τα εισαχθέντα κελιά θα χρησιμοποιούν το προεπιλεγμένο στυλ του φύλλου, χάνοντας τυχόν προσαρμοσμένη μορφοποίηση που μπορεί να έχετε εφαρμόσει στο `DataTable`. Αυτή η σημαία είναι απαραίτητη για μια επαγγελματική εξαγωγή.

## Βήμα 3: Εισαγωγή του DataTable στο φύλλο εργασίας, συμπεριλαμβανομένων των επικεφαλίδων

Τώρα έχετε όλα όσα χρειάζεστε για να απαντήσετε **how to import datatable** σε ένα αρχείο Excel. Δημιουργείτε ένα workbook, επιλέγετε ένα φύλλο εργασίας και καλείτε το `ImportDataTable`. Το δεύτερο όρισμα της μεθόδου (`true`) λέει στο Aspose.Cells να γράψει τις επικεφαλίδες των στηλών ως την πρώτη γραμμή.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

Η εκτέλεση του `ExportDataTableToExcel("Employees.xlsx")` δημιουργεί ένα αρχείο `Employees.xlsx` όπου η πρώτη γραμμή περιέχει **Id**, **Name** και **Department**, και κάθε κελί διατηρεί το στυλ που ορίστηκε στο αρχικό `DataTable`.

### Πλήρες εκτελέσιμο παράδειγμα

Ακολουθεί ένα πλήρες, αυτόνομο πρόγραμμα κονσόλας που δείχνει **how to import datatable** και αποθηκεύει το αποτέλεσμα στον τρέχοντα φάκελο. Αντιγράψτε‑και‑επικολλήστε το σε ένα νέο έργο κονσόλας και εκτελέστε το.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα**  
Όταν ανοίξετε το `Employees.xlsx`, θα δείτε:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Όλα τα κελιά διατηρούν το προεπιλεγμένο στυλ DataTable (γραμματοσειρά, στοίχιση). Εάν εφαρμόσατε προσαρμοσμένα στυλ στο `DataTable` πριν από την εισαγωγή, αυτά τα στυλ εμφανίζονται ακριβώς στο φύλλο εργασίας επειδή το `ImportDataTableStyle` είναι ορισμένο σε `true`.

## Συνηθισμένα προβλήματα και συμβουλές βέλτιστων πρακτικών

| Πρόβλημα | Γιατί συμβαίνει | Πώς να το αποφύγετε |
|----------|----------------|----------------------|
| **Headers missing** | Η παράδοση του `false` ως δεύτερο όρισμα στο `ImportDataTable` παραλείπει τα ονόματα των στηλών. | Χρησιμοποιείτε πάντα `true` όταν χρειάζεστε επικεφαλίδες, ή γράψτε τις χειροκίνητα πριν από την εισαγωγή. |
| **Style not transferred** | Ξεχάσατε να ενεργοποιήσετε το `ImportDataTableStyle`. | Ορίστε `ImportDataTableStyle = true` στο `ImportTableOptions`. |
| **Large tables cause performance lag** | Εισαγωγή εκατομμυρίων γραμμών χωρίς σελιδοποίηση. | Εισάγετε σε παρτίδες ή χρησιμοποιήστε το `ImportDataTable` με την υπερφόρτωση `startRow` για ροή δεδομένων. |
| **Incorrect worksheet reference** | Χρήση του `workbook.Worksheets[1]` όταν υπάρχει μόνο ένα φύλλο. | Χρησιμοποιήστε `workbook.Worksheets[0]` ή δημιουργήστε νέο φύλλο με `workbook.Worksheets.Add()`. |
| **License expiration** | Η δοκιμαστική έκδοση του Aspose.Cells εμφανίζει υδατογράφημα μετά από 30 ημέρες. | Εφαρμόστε έγκυρη άδεια με `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Συμβουλή**: Εάν χρειάζεται να εφαρμόσετε ένα προσαρμοσμένο θέμα μετά την εισαγωγή, καλέστε το `ws.Cells.ApplyStyle(style)` όπου το `style` είναι ένα αντικείμενο `Style` που διαμορφώνετε μία φορά και το επαναχρησιμοποιείτε σε όλες τις γραμμές.

## Επέκταση της λύσης

Τώρα που γνωρίζετε **how to import datatable**, μπορείτε να εξερευνήσετε σχετικές περιπτώσεις:

* **Importing multiple tables** – επαναλάβετε την εισαγωγή σε διαφορετικά φύλλα εργασίας.
* **Conditional formatting** – μετά την εισαγωγή, προσθέστε κανόνες με `ws.Cells.ApplyConditionalFormatting`.
* **Exporting to CSV** – χρησιμοποιήστε το `workbook.Save("file.csv", SaveFormat.Csv)` αν απαιτείται μορφή απλού κειμένου.
* **Reading back into a DataTable** – χρησιμοποιήστε το `ws.Cells.ExportDataTable` για να επαληθεύσετε την ακεραιότητα του κύκλου.

Όλες αυτές οι επεκτάσεις βασίζονται στο βασικό μοτίβο που παρουσιάστηκε παραπάνω: ανάκτηση δεδομένων, διαμόρφωση επιλογών εισαγωγής και κλήση μιας μόνο μεθόδου του Aspose.Cells.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή απάντηση στο **how to import datatable** σε ένα φύλλο εργασίας Excel χρησιμοποιώντας C#. Το tutorial κάλυψε την ανάκτηση των πηγαίων δεδομένων, τη διαμόρφωση του `ImportTableOptions` με `ImportDataTableStyle`, και την εκτέλεση της εισαγωγής με το `ImportDataTable`. Ακολουθώντας το παράδειγμα κώδικα, θα διατηρήσετε αυτόματα τις επικεφαλίδες και τα στυλ, και μπορείτε να προσαρμόσετε το μοτίβο για μεγαλύτερα σύνολα δεδομένων, πολλαπλά φύλλα ή πρόσθετες ανάγκες μορφοποίησης.

Έτοιμοι να αυτοματοποιήσετε τη ροή εργασίας αναφορών; Δοκιμάστε να αντικαταστήσετε το δείγμα `DataTable` με ένα πραγματικό ερώτημα βάσης δεδομένων, πειραματιστείτε με προσαρμοσμένα στυλ κελιών, και ενσωματώστε τη μέθοδο στο υπάρχον επίπεδο υπηρεσιών σας. Καλό προγραμματισμό!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να εισάγετε Arrays σε Excel χρησιμοποιώντας Aspose.Cells for .NET: Οδηγός βήμα‑βήμα](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [Πώς να εισάγετε δεδομένα XML σε Excel με Aspose.Cells for .NET: Οδηγός βήμα‑βήμα](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [Πώς να εισάγετε DataTables μορφοποιημένα σε HTML σε Excel χρησιμοποιώντας Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}