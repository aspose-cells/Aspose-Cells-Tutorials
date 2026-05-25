---
category: general
date: 2026-03-18
description: Πώς να εξάγετε δεδομένα Excel σε DataTable σε C# με κώδικα που διαχειρίζεται
  συγκεκριμένα κελιά, μετατρέπει το Excel σε DataTable και μορφοποιεί αριθμούς. Μάθετε
  πώς να εξάγετε συγκεκριμένα κελιά και περισσότερα.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: el
og_description: Πώς να εξάγετε δεδομένα Excel σε DataTable σε C#. Αυτό το σεμινάριο
  δείχνει πώς να εξάγετε συγκεκριμένα κελιά, να μετατρέψετε το Excel σε DataTable
  και να μορφοποιήσετε αριθμούς με ευκολία.
og_title: Πώς να εξάγετε το Excel σε DataTable με C# – Πλήρης Οδηγός
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Πώς να εξάγετε το Excel σε DataTable σε C# – Οδηγός βήμα‑βήμα
url: /el/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Excel σε DataTable σε C# – Οδηγός Βήμα‑βήμα

Έχετε αναρωτηθεί **πώς να εξάγετε δεδομένα Excel** σε ένα `DataTable` χωρίς να χάσετε τη μορφοποίηση; Δεν είστε οι μόνοι—οι προγραμματιστές χρειάζονται συνεχώς να τραβούν ένα τμήμα ενός υπολογιστικού φύλλου στη μνήμη για αναφορές, επικυρώσεις ή λειτουργίες μαζικής εισαγωγής. Τα καλά νέα; Με λίγες γραμμές C# μπορείτε να εξάγετε ένα ακριβές εύρος (π.χ. *A1:F11*), να αναγκάσετε κάθε κελί να αντιμετωπίζεται ως συμβολοσειρά και ακόμη να εφαρμόσετε προσαρμοσμένη μορφή αριθμού.

Σε αυτό το tutorial θα καλύψουμε όλα όσα χρειάζεστε: από τη φόρτωση του βιβλίου εργασίας, τη ρύθμιση **εξαγωγής συγκεκριμένων κελιών**, τη μετατροπή του εύρους σε `DataTable`, και τη διαχείριση ειδικών περιπτώσεων όπως κενές γραμμές ή αριθμοί εξαρτώμενοι από την τοπική ρύθμιση. Στο τέλος θα έχετε μια επαναχρησιμοποιήσιμη μέθοδο που λειτουργεί με σενάρια **excel to datatable c#** σε παραγωγικό κώδικα.

> **Προαπαιτούμενα** – Θα χρειαστείτε τη βιβλιοθήκη Aspose.Cells for .NET (ή οποιοδήποτε παρόμοιο API που προσφέρει `ExportDataTable`). Το παράδειγμα υποθέτει .NET 6+, αλλά οι έννοιες ισχύουν και για παλαιότερες εκδόσεις.

---

## Τι Θα Μάθετε

- Πώς να **μετατρέψετε Excel σε DataTable** χρησιμοποιώντας Aspose.Cells.  
- Εξαγωγή προσαρμοσμένου εύρους (`excel range to datatable`) ενώ όλα τα τιμές αντιμετωπίζονται ως συμβολοσειρές.  
- Εφαρμογή μορφής αριθμού με δύο δεκαδικά (`#,#00.00`) κατά την εξαγωγή.  
- Συνηθισμένα προβλήματα (κενές γραμμές, κρυμμένες στήλες) και πώς να τα αποφύγετε.  
- Ένα έτοιμο‑για‑αντιγραφή, πλήρως εκτελέσιμο δείγμα κώδικα.

---

## Προαπαιτούμενα και Ρύθμιση

Πριν βουτήξουμε στον κώδικα, βεβαιωθείτε ότι έχετε:

1. **Aspose.Cells for .NET** εγκατεστημένο μέσω NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Ένα αρχείο Excel (`input.xlsx`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε, π.χ. `YOUR_DIRECTORY/input.xlsx`.  
3. Ένα project που στοχεύει .NET 6 ή νεότερο (οι δηλώσεις `using` που φαίνονται παρακάτω λειτουργούν αμέσως).

> **Pro tip:** Αν χρησιμοποιείτε διαφορετική βιβλιοθήκη (π.χ. EPPlus ή ClosedXML), η έννοια παραμένει η ίδια—φορτώστε το βιβλίο εργασίας, επιλέξτε ένα εύρος, και καλέστε μια μέθοδο που επιστρέφει ένα `DataTable`.

---

## Βήμα 1: Φορτώστε το Workbook και Πάρτε το Πρώτο Worksheet

Το πρώτο που χρειάζεστε είναι ένα αντικείμενο `Workbook` που αντιπροσωπεύει το αρχείο Excel σας. Μόλις το έχετε, μπορείτε να προσπελάσετε οποιοδήποτε φύλλο με δείκτη ή όνομα.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Γιατί είναι σημαντικό:** Η φόρτωση του workbook νωρίς σας επιτρέπει να εξετάσετε τη δομή του (κρυφά φύλλα, προστασία) πριν αποφασίσετε ποια κελιά θα εξάγετε. Αν το αρχείο είναι μεγάλο, σκεφτείτε να χρησιμοποιήσετε `LoadOptions` για να ρέετε μόνο τα απαιτούμενα τμήματα.

---

## Βήμα 2: Ρυθμίστε τις Επιλογές Εξαγωγής – Αντιμετωπίστε Όλες τις Τιμές ως Συμβολοσειρές

Όταν εξάγετε δεδομένα για επεξεργασία (π.χ. μαζική εισαγωγή σε SQL), συχνά θέλετε μια **συνεπή αναπαράσταση συμβολοσειράς**. Αυτό αποτρέπει σφάλματα ασυμφωνίας τύπων αργότερα.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Επεξήγηση:**  
- `ExportAsString = true` λέει στο Aspose.Cells να αγνοήσει τον εγγενή τύπο του κελιού και να επιστρέψει το μορφοποιημένο κείμενο.  
- `NumberFormat = "#,##0.00"` εξασφαλίζει ότι αριθμοί όπως `1234.5` γίνονται `"1,234.50"`—χρήσιμο για οικονομικές αναφορές.

Αν χρειάζεστε τους αρχικούς τύπους δεδομένων, απλώς ορίστε `ExportAsString` σε `false` και διαχειριστείτε τη μετατροπή εσείς.

---

## Βήμα 3: Εξάγετε Συγκεκριμένο Εύρος (A1:F11) σε DataTable

Τώρα έρχεται η καρδιά του **export specific cells**. Η μέθοδος `ExportDataTable` δέχεται δείκτες γραμμής/στήλης έναρξης-τέλους (μηδενική βάση) και μια σημαία για την ένταξη των κεφαλίδων.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Τι παίρνετε:** Ένα `DataTable` με 11 γραμμές (συμπεριλαμβανομένης της κεφαλίδας) και 6 στήλες (`A`‑`F`). Όλες οι τιμές είναι συμβολοσειρές μορφοποιημένες σύμφωνα με το `exportOptions`.

---

## Βήμα 4: Επαληθεύστε το Αποτέλεσμα – Εκτύπωση στην Κονσόλα

Πάντα είναι καλή ιδέα να ελέγξετε το αποτέλεσμα πριν το περάσετε σε άλλο στοιχείο.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Θα πρέπει να δείτε κάτι σαν:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Παρατηρήστε πώς οι αριθμητικές στήλες εμφανίζουν δύο δεκαδικά ψηφία, ακριβώς όπως ορίσαμε.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή)

Παρακάτω είναι το πλήρες πρόγραμμα που ενώνει όλα τα παραπάνω. Τοποθετήστε το σε ένα νέο console project, προσαρμόστε τη διαδρομή του αρχείου, και τρέξτε—χωρίς επιπλέον ρυθμίσεις.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Κύρια σημεία από τον κώδικα:**

- Το αντικείμενο `ExportTableOptions` είναι επαναχρησιμοποιήσιμο· μπορείτε να το περάσετε σε πολλαπλές κλήσεις `ExportDataTable` αν χρειαστεί να εξάγετε πολλά εύρη.  
- Η αρίθμηση ξεκινά από **0**, έτσι το `A1` αντιστοιχεί σε `(0,0)`.  
- Ορίζοντας `includeColumnNames` σε `true` χρησιμοποιεί αυτόματα την πρώτη γραμμή ως κεφαλίδες στήλης—ιδανικό για επόμενες λειτουργίες `DataTable`.

---

## Διαχείριση Ειδικών Περιπτώσεων & Συχνές Ερωτήσεις

### Τι γίνεται αν το φύλλο έχει κρυμμένες γραμμές ή στήλες;

Το Aspose.Cells σέβεται την ορατότητα από προεπιλογή. Αν χρειάζεται να εξάγετε κρυφά δεδομένα, ορίστε `exportOptions.ExportHiddenRows = true` και `ExportHiddenColumns = true`.

### Το αρχείο Excel περιέχει τύπους—θα λάβω τις υπολογισμένες τιμές;

Ναι. Από προεπιλογή η `ExportDataTable` επιστρέφει την **εμφανιζόμενη τιμή** (το αποτέλεσμα του τύπου). Αν θέλετε το ακατέργαστο κείμενο του τύπου, ορίστε `exportOptions.ExportFormulas = true`.

### Πώς παραλείπω εντελώς κενές γραμμές;

Μετά την εξαγωγή, μπορείτε να καθαρίσετε το `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Μπορώ να εξάγω μη συνεχές εύρος (π.χ. A1:B5 και D1:E5);

Το Aspose.Cells δεν υποστηρίζει διασπασμένα εύρη σε μία κλήση. Αντ' αυτού, εξάγετε κάθε τμήμα ξεχωριστά και στη συνέχεια συγχωνεύστε τα `DataTable` χειροκίνητα.

---

## Συμβουλές Απόδοσης

- **Επαναχρησιμοποιήστε το `ExportTableOptions`** για πολλαπλές εξαγωγές· η δημιουργία νέας παρουσίας κάθε φορά προσθέτει ελάχιστο κόστος αλλά γεμίζει τον κώδικα.  
- **Ρέετε μεγάλα αρχεία** με `LoadOptions` για να αποφύγετε τη φόρτωση ολόκληρου του workbook στη μνήμη.  
- **Αποφύγετε το `DataTable`** αν χρειάζεστε μόνο γρήγορη εξαγωγή CSV—η `ExportDataTable` είναι βολική αλλά δεν είναι η πιο αποδοτική μνήμη για τεράστιες φύλλα.

---

## Συμπέρασμα

Διασχίσαμε **πώς να εξάγετε δεδομένα Excel** σε ένα `DataTable` ελέγχοντας τη μορφοποίηση, διαχειριζόμενοι συγκεκριμένα εύρη κελιών, και εξασφαλίζοντας ότι κάθε τιμή φθάνει ως συμβολοσειρά. Το πλήρες παράδειγμα δείχνει μια καθαρή, έτοιμη για παραγωγή προσέγγιση που μπορείτε να προσαρμόσετε για **convert excel to datatable**, **export specific cells**, ή οποιοδήποτε σενάριο **excel range to datatable** που συναντάτε.

Πειραματιστείτε: αλλάξτε το εύρος, εναλλάξτε το `ExportAsString`, ή στείλτε το `DataTable` κατευθείαν στο Entity Framework για μαζικές εισαγωγές. Οι δυνατότητες είναι απεριόριστες μόλις έχετε αυτή τη σταθερή βάση.

---

### Επόμενα Βήματα & Σχετικά Θέματα

- **Εισαγωγή DataTable πίσω στο Excel** – μάθετε την αντίστροφη λειτουργία με `ImportDataTable`.  
- **Μαζική εισαγωγή DataTable σε SQL Server** – χρησιμοποιήστε `SqlBulkCopy` για αστραπιαίες φορτώσεις.  
- **Δουλειά με EPPlus ή ClosedXML** – δείτε πώς φαίνεται η ίδια εργασία με εναλλακτικές βιβλιοθήκες.  
- **Μορφοποίηση κελιών κατά την εξαγωγή** – εξερευνήστε περαιτέρω το `ExportTableOptions` για μορφές ημερομηνίας, προσαρμοσμένες ρυθμίσεις πολιτισμού, και άλλα.

Έχετε ερωτήσεις ή διαφορετική περίπτωση χρήσης; Αφήστε ένα σχόλιο και ας συνεχίσουμε τη συζήτηση. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}