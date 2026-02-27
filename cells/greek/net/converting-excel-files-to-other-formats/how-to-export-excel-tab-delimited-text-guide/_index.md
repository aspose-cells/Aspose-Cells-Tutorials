---
category: general
date: 2026-02-26
description: πώς να εξάγετε το Excel σε αρχείο txt με διαχωριστικό ταμπ χρησιμοποιώντας
  C#. Μάθετε πώς να εξάγετε το Excel ως ταμπ, να μετατρέψετε το Excel σε txt και να
  εξάγετε το Excel με διαχωριστικό σε τρία εύκολα βήματα.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: el
og_description: πώς να εξάγετε το Excel σε αρχείο txt με διαχωριστικό tab χρησιμοποιώντας
  C#. Αυτό το σεμινάριο δείχνει πώς να εξάγετε το Excel ως tab, να μετατρέψετε το
  Excel σε txt και να εξάγετε το Excel με διαχωριστικό.
og_title: πώς να εξάγετε το Excel – Οδηγός για κείμενο διαχωρισμένο με καρτέλες
tags:
- csharp
- excel
- file-conversion
title: πώς να εξάγετε το Excel – Οδηγός για κείμενο διαχωρισμένο με καρτέλες
url: /el/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να εξάγετε excel – Πλήρης Εκμάθηση C#

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε δεδομένα excel** σε ένα αρχείο απλού κειμένου χωρίς να χάσετε τη μορφοποίηση; Ίσως χρειάζεστε ένα γρήγορο TSV (τιμές διαχωρισμένες με καρτέλα) για μια γραμμή δεδομένων, ή τροφοδοτείτε ένα παλιό σύστημα που διαβάζει μόνο `.txt`. Σε κάθε περίπτωση, δεν είστε μόνοι—οι προγραμματιστές συχνά αντιμετωπίζουν αυτό το εμπόδιο όταν μεταφέρουν δεδομένα έξω από τα φύλλα εργασίας.

Τα καλά νέα; Σε μόλις τρία απλά βήματα μπορείτε **να εξάγετε excel ως κείμενο διαχωρισμένο με καρτέλα**, **να μετατρέψετε excel σε txt**, και ακόμη να επιλέξετε προσαρμοσμένο διαχωριστικό αν αλλάξετε γνώμη αργότερα. Παρακάτω θα δείτε ένα πλήρως εκτελέσιμο παράδειγμα C#, γιατί κάθε γραμμή είναι σημαντική, και μερικές συμβουλές για να αποφύγετε τα συνηθισμένα προβλήματα.

> **Pro tip:** Αυτή η προσέγγιση λειτουργεί με τη δημοφιλή βιβλιοθήκη Aspose.Cells, αλλά οι έννοιες μεταφράζονται σε οποιοδήποτε .NET Excel API που προσφέρει μέθοδο τύπου `ExportTable`.

## Τι Θα Χρειαστείτε

- **.NET 6+** (ή .NET Framework 4.6+). Ο κώδικας μεταγλωττίζεται σε οποιοδήποτε πρόσφατο runtime.
- **Aspose.Cells for .NET** (δωρεάν δοκιμή ή αδειοδοτημένο). Εγκατάσταση μέσω NuGet: `dotnet add package Aspose.Cells`.
- Ένα αρχείο εργασίας εισόδου με όνομα `input.xlsx` τοποθετημένο σε φάκελο που ελέγχετε.
- Μια μικρή δόση περιέργειας—δεν απαιτούνται βαθιές γνώσεις του Excel.

Αν έχετε ήδη όλα αυτά, ας περάσουμε κατευθείαν στη λύση.

## Βήμα 1 – Φόρτωση του Workbook που Θέλετε να Εξάγετε

Πρώτα δημιουργούμε ένα αντικείμενο `Workbook` που δείχνει στο αρχείο προέλευσης. Αυτό το αντικείμενο αντιπροσωπεύει ολόκληρο το αρχείο Excel, συμπεριλαμβανομένων όλων των φύλλων, των ονομασμένων περιοχών και της μορφοποίησης.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Γιατί είναι σημαντικό:*  
Η φόρτωση του workbook σας δίνει πρόσβαση στη συλλογή φύλλων (`workbook.Worksheets`). Χωρίς αυτό το αντικείμενο δεν μπορείτε να προσπελάσετε κελιά, περιοχές ή ρυθμίσεις εξαγωγής.  

> **Σημείωση:** Αν το αρχείο σας βρίσκεται σε κοινόχρηστο δίκτυο, προσθέστε `\\` ή χρησιμοποιήστε διαδρομή UNC—η Aspose.Cells το διαχειρίζεται άψογα.

## Βήμα 2 – Διαμόρφωση Επιλογών Εξαγωγής (String Values & Tab Delimiter)

Τώρα λέμε στη βιβλιοθήκη πώς θέλουμε να γραφτούν τα δεδομένα. Ορίζοντας `ExportAsString = true` αναγκάζουμε κάθε κελί να αντιμετωπιστεί ως απλό κείμενο, εξαλείφοντας τις τοπικές μορφές αριθμών του Excel. Το `Delimiter = "\t"` είναι η καρδιά του **export excel as tab**.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Γιατί είναι σημαντικό:*  
Αν παραλείψετε το `ExportAsString`, ένα κελί που περιέχει `12345` μπορεί να μετατραπεί σε `12,345` σε ορισμένες τοπικές ρυθμίσεις, σπάζοντας τους επόμενους επεξεργαστές. Το διαχωριστικό μπορεί να αντικατασταθεί με κόμμα, κάθετο ή οποιονδήποτε χαρακτήρα αν αργότερα αποφασίσετε να **export excel with delimiter** διαφορετικό από καρτέλα.

## Βήμα 3 – Εξαγωγή Συγκεκριμένης Περιοχής σε Αρχείο Κειμένου

Τέλος, επιλέγουμε την περιοχή που μας ενδιαφέρει (`A1:D10` σε αυτό το παράδειγμα) και την γράφουμε στο `out.txt`. Η μέθοδος `ExportTable` κάνει όλη τη βαριά δουλειά: διαβάζει τα κελιά, εφαρμόζει τις επιλογές και αποθηκεύει το αποτέλεσμα στο δίσκο.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

Μετά την εκτέλεση, θα βρείτε το `out.txt` με περιεχόμενο που μοιάζει με:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

Κάθε στήλη διαχωρίζεται με **καρτέλα**, κάνοντάς το έτοιμο για `awk`, `PowerShell`, ή οποιοδήποτε εργαλείο συμβατό με CSV που σέβεται τις καρτέλες.

### Γρήγορη Επαλήθευση

Ανοίξτε το παραγόμενο αρχείο σε έναν επεξεργαστή απλού κειμένου (Notepad, VS Code) και ελέγξτε:

1. Οι στήλες ευθυγραμμίζονται όταν ενεργοποιήσετε την “Εμφάνιση κενών χαρακτήρων”.
2. Δεν εμφανίζονται επιπλέον εισαγωγικά ή κόμματα.
3. Όλα τα αριθμητικά κελιά εμφανίζονται ακριβώς όπως στο Excel (ευχαριστώ το `ExportAsString`).

Αν κάτι φαίνεται λανθασμένο, ελέγξτε ξανά ότι το αρχικό workbook δεν κρύβει γραμμές/στήλες και βεβαιωθείτε ότι αναφέρεστε στο σωστό δείκτη φύλλου.

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### Εξαγωγή Ολόκληρου Φύλλου

Αν θέλετε να **export excel range** που καλύπτει ολόκληρο το φύλλο, μπορείτε να χρησιμοποιήσετε `sheet.Cells.MaxDisplayRange`:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Χρήση Διαφορετικού Διαχωριστικού

Η αλλαγή από καρτέλα σε κάθετο (`|`) είναι τόσο απλή όσο η αλλαγή μιας γραμμής:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

Αυτό καλύπτει το σενάριο **export excel with delimiter** χωρίς να χρειάζεται να ξαναγράψετε κώδικα.

### Διαχείριση Μεγάλων Αρχείων (> 100 MB)

Για τεράστια workbooks, κάντε streaming την εξαγωγή για να αποφύγετε τη φόρτωση όλου του αρχείου στη μνήμη:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Μετατροπή Πολλαπλών Φύλλων σε Μία Περίοδο

Αν χρειάζεται να **convert excel to txt** για πολλά φύλλα, κάντε βρόχο πάνω τους:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

Κάθε φύλλο δημιουργεί το δικό του αρχείο TSV—χρήσιμο για batch jobs.

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι ολόκληρο το πρόγραμμα, έτοιμο για μεταγλώττιση. Απλώς αντικαταστήστε τις διαδρομές αρχείων με τις δικές σας.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ένα αρχείο με όνομα `out.txt` όπου κάθε στήλη διαχωρίζεται με χαρακτήρα καρτέλας, και κάθε τιμή κελιού εμφανίζεται ακριβώς όπως στο Excel.

## Συχνές Ερωτήσεις

- **Λειτουργεί με αρχεία .xls;**  
  Ναι. Η Aspose.Cells ανιχνεύει αυτόματα τη μορφή, οπότε μπορείτε να δείξετε το `Workbook` σε ένα παλιό `.xls` και ο ίδιος κώδικας ισχύει.

- **Τι γίνεται αν τα δεδομένα μου περιέχουν καρτέλες;**  
  Οι καρτέλες μέσα σε κελί θα διατηρηθούν, κάτι που μπορεί να σπάσει τους TSV αναλυτές. Σε αυτήν την περίπτωση, σκεφτείτε να αλλάξετε το διαχωριστικό σε κάθετο (`|`) ενημερώνοντας το `exportOptions.Delimiter`.

- **Μπορώ να εξάγω τύπους αντί για τιμές;**  
  Ορίστε `exportOptions.ExportAsString = false` και χρησιμοποιήστε την υπερφόρτωση `ExportTableOptions` που περιλαμβάνει `ExportFormula = true`. Η έξοδος θα περιέχει το ακατέργαστο κείμενο του τύπου.

- **Υπάρχει τρόπος να παραλείψω κρυμμένες γραμμές;**  
  Ναι. Ορίστε `exportOptions.ExportHiddenRows = false` (η προεπιλογή είναι `true`). Οι κρυμμένες γραμμές θα παραλειφθούν από το τελικό αρχείο κειμένου.

## Συμπέρασμα

Τώρα έχετε μια σταθερή, έτοιμη για παραγωγή συνταγή για **πώς να εξάγετε excel** δεδομένα ως αρχείο κειμένου διαχωρισμένο με καρτέλα, πώς να **export excel as tab**, και πώς να **convert excel to txt** με πλήρη έλεγχο των διαχωριστικών και της επιλογής περιοχής. Χρησιμοποιώντας τη μέθοδο `ExportTable` της Aspose.Cells αποφεύγετε χειροκίνητη κατασκευή CSV, διατηρείτε την ακεραιότητα των δεδομένων και κρατάτε τον κώδικά σας καθαρό.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε:

- Εξαγωγή απευθείας σε `MemoryStream` για web APIs.  
- Προσθήκη δυναμικής γραμμής κεφαλίδας βάσει του περιεχομένου της πρώτης γραμμής.  
- Ενσωμάτωση αυτής της ρουτίνας σε Azure Function που παρακολουθεί ένα bucket αποθήκευσης για νέες μεταφορτώσεις Excel.

Δοκιμάστε το, αλλάξτε το διαχωριστικό, και αφήστε τα δεδομένα να ρέουν όπου χρειάζεται. Καλή προγραμματιστική διασκέδαση!  

<img src="export-excel.png" alt="παράδειγμα εξαγωγής excel" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}