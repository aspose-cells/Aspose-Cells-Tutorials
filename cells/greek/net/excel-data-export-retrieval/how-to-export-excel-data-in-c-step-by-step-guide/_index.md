---
category: general
date: 2026-03-21
description: Πώς να εξάγετε δεδομένα Excel με ονόματα στηλών, να διατηρήσετε τη μορφή
  αριθμών και να διαβάσετε συγκεκριμένες γραμμές χρησιμοποιώντας το Aspose.Cells σε
  C#. Μάθετε πώς να διαβάζετε φύλλο εργασίας Excel και να εξάγετε συγκεκριμένες γραμμές
  αποδοτικά.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: el
og_description: Πώς να εξάγετε δεδομένα Excel με ονόματα στηλών, να διατηρήσετε τη
  μορφή αριθμών και να διαβάσετε συγκεκριμένες γραμμές χρησιμοποιώντας το Aspose.Cells.
  Ένα πλήρες, εκτελέσιμο παράδειγμα για προγραμματιστές C#.
og_title: Πώς να εξάγετε δεδομένα Excel σε C# – Πλήρης οδηγός προγραμματισμού
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Πώς να εξάγετε δεδομένα Excel σε C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Δεδομένα Excel σε C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε excel** δεδομένα χωρίς να χάσετε την αρχική μορφοποίηση; Ίσως έχετε δοκιμάσει μια γρήγορη αντιγραφή‑επικόλληση και να καταλήξατε με ημερομηνίες που φαίνονται σαν “44728” ή χωρίς κεφαλίδες στηλών. Αυτό είναι εκνευριστικό, σωστά; Σε αυτό το tutorial θα δείτε έναν καθαρό, από‑αρχή‑μέχρι‑τέλος τρόπο για να διαβάσετε ένα φύλλο εργασίας Excel, να διατηρήσετε τη μορφή αριθμών, να εξάγετε με ονόματα στηλών, και ακόμη να επιλέξετε μόνο τις γραμμές που χρειάζεστε.

Θα χρησιμοποιήσουμε τη βιβλιοθήκη Aspose.Cells επειδή παρέχει λεπτομερή έλεγχο των επιλογών εξαγωγής. Στο τέλος αυτού του οδηγού θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορεί να ενσωματωθεί σε οποιοδήποτε έργο .NET, και θα καταλάβετε γιατί κάθε επιλογή είναι σημαντική. Δεν απαιτούνται εξωτερικά έγγραφα—όλα όσα χρειάζεστε είναι εδώ.

---

## Τι Θα Μάθετε

- **Διαβάστε το φύλλο εργασίας Excel** στη μνήμη με Aspose.Cells.
- **Εξάγετε συγκεκριμένες γραμμές** (π.χ., γραμμές 0‑49) διατηρώντας τα ονόματα στηλών.
- **Διατηρήστε τη μορφή αριθμών** ώστε το νόμισμα, οι ημερομηνίες και τα ποσοστά να παραμένουν αμετάβλητα.
- Πώς να **εξάγετε με ονόματα στηλών** και να συμπεριλάβετε σχόλια κελιών αν τα χρειάζεστε.
- Ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα C# συν συμβουλές για κοινές παγίδες.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+).
- Aspose.Cells για .NET εγκατεστημένο μέσω NuGet (`Install-Package Aspose.Cells`).
- Ένα αρχείο Excel (`input.xlsx`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.

> **Συμβουλή Pro:** Αν βρίσκεστε σε CI pipeline, σκεφτείτε να κατεβάζετε το πακέτο NuGet από ιδιωτικό feed για να αποφύγετε εκπλήξεις αδειοδότησης.

## Βήμα 1 – Εγκατάσταση Aspose.Cells και Προσθήκη Namespaces

Πρώτα, βεβαιωθείτε ότι το πακέτο Aspose.Cells βρίσκεται στο έργο σας. Ανοίξτε το Package Manager Console και εκτελέστε:

```powershell
Install-Package Aspose.Cells
```

Στη συνέχεια προσθέστε τις απαιτούμενες οδηγίες `using` στην κορυφή του αρχείου C#:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Αυτές οι εισαγωγές σας δίνουν πρόσβαση στα `Workbook`, `Worksheet`, `ExportTableOptions` και `DataTable`—τα βασικά στοιχεία για **reading an Excel worksheet** και εξαγωγή δεδομένων.

## Βήμα 2 – Φόρτωση του Workbook (Ανάγνωση του Αρχείου Excel)

Τώρα διαβάζουμε πραγματικά **το φύλλο εργασίας Excel**. Ο κατασκευαστής `Workbook` δέχεται τη διαδρομή του αρχείου, και το Aspose.Cells θα διαχειριστεί τόσο μορφές `.xlsx` όσο και παλαιότερες `.xls`.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του workbook μία φορά και η επαναχρήση του ίδιου αντικειμένου `Worksheet` είναι πολύ πιο αποδοτική από το άνοιγμα του αρχείου επανειλημμένα, ειδικά για μεγάλα φύλλα.

## Βήμα 3 – Διαμόρφωση Επιλογών Εξαγωγής (Διατήρηση Μορφής Αριθμών & Ονομάτων Στηλών)

Εδώ λέμε στο Aspose.Cells *πώς* να εξάγει. Η κλάση `ExportTableOptions` μας επιτρέπει να ρυθμίσουμε λεπτομερώς την έξοδο. Θα ενεργοποιήσουμε τρία flags:

1. `ExportAsString = true` – αναγκάζει κάθε κελί να γίνει συμβολοσειρά, εξασφαλίζοντας ότι οι αριθμοί διατηρούν την οπτική τους αναπαράσταση.
2. `IncludeCellComments = true` – αντιγράφει τυχόν σχόλια που είναι συνδεδεμένα στα κελιά (χρήσιμο για τεκμηρίωση).
3. `PreserveNumberFormat = true` – διατηρεί την αρχική μορφή αριθμού (σύμβολα νομίσματος, μοτίβα ημερομηνίας κλπ).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Ακραία περίπτωση:** Αν ορίσετε `ExportAsString` σε `false` αλλά θέλετε να κρατήσετε τις μορφές αριθμών, μπορεί να καταλήξετε με ακατέργαστες αριθμητικές τιμές (π.χ., 44728 για ημερομηνία). Η ενεργοποίηση και των δύο flags αποτρέπει αυτή την έκπληξη.

## Βήμα 4 – Λήψη του Πρώτου Worksheet (Ανάγνωση Excel Worksheet)

Τα περισσότερα απλά αρχεία έχουν τα δεδομένα που χρειάζεστε στο πρώτο φύλλο, οπότε θα το πάρουμε με βάση το δείκτη. Αν χρειάζεστε διαφορετικό φύλλο, απλώς αντικαταστήστε το `0` με τον κατάλληλο μηδενικό δείκτη ή χρησιμοποιήστε `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Γιατί είναι χρήσιμο:** Η άμεση πρόσβαση στο αντικείμενο worksheet σας δίνει πλήρη έλεγχο στη συλλογή `Cells`, κάτι που είναι ουσιώδες για **export specific rows** αργότερα.

## Βήμα 5 – Εξαγωγή Περιοχής Κελιών (Εξαγωγή Συγκεκριμένων Γραμμών)

Τώρα η καρδιά του tutorial: εξαγωγή γραμμών 0‑49 και στηλών 0‑4 (δηλαδή τις πρώτες 50 γραμμές και τις πρώτες πέντε στήλες) σε ένα `DataTable`. Θα ζητήσουμε επίσης από το Aspose.Cells να συμπεριλάβει τα ονόματα στηλών ως την πρώτη γραμμή του `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Τι Κάνει Αυτό

- **`startRow: 0`** – αρχίζει στην κορυφή του φύλλου.
- **`totalRows: 50`** – παίρνει τις πρώτες 50 γραμμές (δηλαδή **export specific rows**).
- **`totalColumns: 5`** – περιορίζει την εξαγωγή στις πρώτες πέντε στήλες.
- **`includeColumnNames: true`** – εξασφαλίζει ότι οι κεφαλίδες στήλης του `DataTable` ταιριάζουν με τη γραμμή κεφαλίδας του Excel, ικανοποιώντας την απαίτηση **export with column names**.
- **`exportOptions`** – εφαρμόζει τις ρυθμίσεις από το Βήμα 3, ώστε οι αριθμητικές τιμές σας να παραμένουν όπως “$1,234.56” αντί για “1234.56”.

## Βήμα 6 – Επαλήθευση της Εξαγωγής (Πώς Φαίνεται το Αποτέλεσμα)

Ας εκτυπώσουμε τις πρώτες λίγες γραμμές στην κονσόλα ώστε να δείτε ότι η μορφοποίηση διατήρησε.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Αναμενόμενη έξοδος (παράδειγμα):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Παρατηρήστε πώς οι ημερομηνίες εμφανίζονται σε μορφή `MM/dd/yyyy` και το νόμισμα διατηρεί το σύμβολο `$`—ευχαριστώντας τη **preserve number format**.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| Οι ημερομηνίες μετατρέπονται σε μεγάλα νούμερα | `ExportAsString` άφησε `false` | Κρατήστε `ExportAsString = true` ή μετατρέψτε τα κελιά χειροκίνητα |
| Λείπουν οι κεφαλίδες στηλών | `includeColumnNames` ορίστηκε σε `false` | Ορίστε το σε `true` όταν χρειάζεστε **export with column names** |
| Τα σχόλια εξαφανίζονται | `IncludeCellComments` δεν ενεργοποιήθηκε | Ενεργοποιήστε `IncludeCellComments` στο `ExportTableOptions` |
| Εξάγετε το λάθος φύλλο | Χρήση `Worksheets[0]` σε αρχείο πολλαπλών φύλλων | Καθορίστε το όνομα του φύλλου: `workbook.Worksheets["Data"]` |
| Εξαίρεση εκτός εύρους | `totalRows` υπερβαίνει τις πραγματικές γραμμές | Χρησιμοποιήστε `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

## Μπόνους: Εξαγωγή Ολόκληρου Φύλλου Διατηρώντας τις Μορφές

Αν αργότερα αποφασίσετε ότι χρειάζεστε ολόκληρο το φύλλο, απλώς αντικαταστήστε τα `totalRows` και `totalColumns` με τις μέγιστες διαστάσεις του φύλλου:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Τώρα έχετε μια ρουτίνα **read excel worksheet** που λειτουργεί για οποιοδήποτε μέγεθος, ενώ εξακολουθεί να **preserving number format** και **exporting with column names**.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να ενσωματώσετε σε μια εφαρμογή console. Περιλαμβάνει όλα τα βήματα, τις εισαγωγές και μια απλή εκτύπωση επαλήθευσης.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Αποθηκεύστε το ως `Program.cs`, τρέξτε `dotnet run`, και θα δείτε την μορφοποιημένη προεπισκόπηση στο τερματικό σας.

## Συμπέρασμα

Μόλις περάσαμε από **how to export excel** δεδομένα χρησιμοποιώντας το Aspose.Cells, καλύπτοντας όλα από τη φόρτωση του workbook μέχρι τη διατήρηση της μορφής αριθμών, την εξαγωγή με ονόματα στηλών, και τον περιορισμό της εξαγωγής σε συγκεκριμένες γραμμές. Ο κώδικας είναι αυτόνομος, πλήρως εκτελέσιμος, και περιλαμβάνει πρακτικά μέτρα ασφαλείας για τις πιο συνηθισμένες ακραίες περιπτώσεις.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να εξάγετε απευθείας σε CSV διατηρώντας τη μορφοποίηση αριθμών, ή σπρώξτε το `DataTable` σε ένα Entity Framework Core context για μαζικές εισαγωγές στη βάση δεδομένων. Και τα δύο σενάρια βασίζονται στα ίδια θεμέλια που καλύψαμε εδώ.

Αν βρήκατε αυτόν τον οδηγό χρήσιμο

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}