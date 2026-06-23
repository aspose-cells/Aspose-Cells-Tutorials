---
category: general
date: 2026-03-22
description: Αποθήκευση βιβλίου εργασίας ως CSV σε C# γρήγορα. Μάθετε πώς να εξάγετε
  το Excel σε CSV, να ορίσετε την ακρίβεια και να μετατρέψετε xlsx σε CSV με το Aspose.Cells
  σε λίγες μόνο γραμμές.
draft: false
keywords:
- save workbook as csv
- export excel to csv
- how to export csv
- how to set precision
- convert xlsx to csv
language: el
og_description: Αποθηκεύστε το βιβλίο εργασίας ως CSV σε C# γρήγορα. Αυτός ο οδηγός
  δείχνει πώς να εξάγετε το Excel σε CSV, να ορίσετε την ακρίβεια και να μετατρέψετε
  xlsx σε CSV χρησιμοποιώντας το Aspose.Cells.
og_title: Αποθήκευση βιβλίου εργασίας ως CSV σε C# – Εξαγωγή Excel σε CSV
tags:
- C#
- Aspose.Cells
- Excel
- CSV
title: Αποθήκευση βιβλίου εργασίας ως CSV σε C# – Εξαγωγή Excel σε CSV
url: /el/net/csv-file-handling/save-workbook-as-csv-in-c-export-excel-to-csv/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση βιβλίου εργασίας ως CSV σε C# – Εξαγωγή Excel σε CSV

Έχετε ποτέ χρειαστεί να **save workbook as CSV** αλλά δεν ήσασταν σίγουροι πώς να διατηρήσετε τους αριθμούς τακτικούς; Δεν είστε μόνοι. Σε πολλές περιπτώσεις data‑pipeline πρέπει να **export Excel to CSV** διατηρώντας έναν συγκεκριμένο αριθμό σημαντικών ψηφίων, και η βιβλιοθήκη Aspose.Cells το κάνει παιχνιδάκι.

Σε αυτό το tutorial θα δείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που **saves a workbook as CSV**, δείχνει *how to set precision* και εξηγεί ακόμη *how to convert xlsx to CSV* για πραγματικά έργα. Χωρίς ασαφείς αναφορές—μόνο κώδικας που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε σήμερα.

## Τι θα μάθετε

- Τα ακριβή βήματα για **save workbook as CSV** με προσαρμοσμένη ρύθμιση ακρίβειας.  
- Πώς να **export Excel to CSV** χρησιμοποιώντας `CsvSaveOptions` και γιατί η ιδιότητα `SignificantDigits` είναι σημαντική.  
- Παραλλαγές για διαφορετικές ανάγκες ακρίβειας και κοινά προβλήματα όταν εργάζεστε με μεγάλα νούμερα.  
- Μια γρήγορη ματιά στη μετατροπή ενός αρχείου `.xlsx` σε `.csv` χωρίς απώλεια ακεραιότητας δεδομένων.  

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.6+).  
- Το πακέτο NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`).  
- Βασική κατανόηση του C# και του file I/O.  

Αν τα έχετε, ας βουτήξουμε.

![save workbook as csv example](image.png "save workbook as csv example")

## Αποθήκευση βιβλίου εργασίας ως CSV – Οδηγός βήμα‑βήμα

Παρακάτω είναι το πλήρες πρόγραμμα. Κάθε γραμμή είναι σχολιασμένη ώστε να βλέπετε *γιατί* υπάρχει κάθε τμήμα, όχι μόνο *τι* κάνει.

```csharp
// ------------------------------------------------------------
// 1️⃣ Load the workbook from an existing .xlsx file
// ------------------------------------------------------------
using Aspose.Cells;          // Aspose.Cells provides Workbook, Worksheet, CsvSaveOptions, etc.
using System;               // For basic .NET types
using System.IO;            // For path handling (optional but handy)

class Program
{
    static void Main()
    {
        // Adjust these paths to match your environment
        string sourcePath = @"YOUR_DIRECTORY\Numbers.xlsx";
        string targetPath = @"YOUR_DIRECTORY\Numbers_4sd.csv";

        // Load the Excel file into a Workbook object.
        // This step automatically parses all worksheets, styles, and formulas.
        Workbook workbook = new Workbook(sourcePath);

        // ------------------------------------------------------------
        // 2️⃣ (Optional) Grab the first worksheet if you need to manipulate it
        // ------------------------------------------------------------
        Worksheet firstSheet = workbook.Worksheets[0];

        // Example: you could change a cell value here before exporting.
        // firstSheet.Cells["A1"].PutValue("Header"); // Uncomment if needed

        // ------------------------------------------------------------
        // 3️⃣ Configure CSV save options – here we set 4 significant digits
        // ------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions
        {
            // SignificantDigits tells Aspose.Cells how many meaningful digits
            // to keep for floating‑point numbers. Values beyond this are rounded.
            SignificantDigits = 4,

            // Optional: you can also control delimiter, encoding, etc.
            // Delimiter = ',',   // default is comma
            // Encoding = Encoding.UTF8
        };

        // ------------------------------------------------------------
        // 4️⃣ Save the workbook as CSV using the configured options
        // ------------------------------------------------------------
        workbook.Save(targetPath, csvOptions);

        Console.WriteLine($"✅ Workbook successfully saved as CSV at: {targetPath}");
    }
}
```

### Γιατί να χρησιμοποιήσετε `CsvSaveOptions.SignificantDigits`?

Όταν **how to set precision** για εξαγωγή CSV, στην πραγματικότητα αποφασίζετε πόσα ψηφία ενός αριθμού κινητής υποδιαστολής θα διατηρηθούν μετά τη μετατροπή. Το Excel αποθηκεύει αριθμούς με ακρίβεια έως 15 ψηφία, αλλά τα περισσότερα downstream συστήματα (βάσεις δεδομένων, pipelines analytics) χρειάζονται μόνο λίγα. Ορίζοντας `SignificantDigits = 4`, η βιβλιοθήκη στρογγυλοποιεί το `123.456789` σε `123.5`, διατηρώντας το αρχείο συμπαγές και ευανάγνωστο.

> **Pro tip:** Αν χρειάζεστε *ακριβείς* τιμές (π.χ., για οικονομικά δεδομένα), ορίστε `SignificantDigits` σε υψηλότερο αριθμό ή παραλείψτε το εντελώς. Η προεπιλογή είναι 15, που αντικατοπτρίζει την εσωτερική ακρίβεια του Excel.

## Export Excel to CSV – Συνηθισμένες Παραλλαγές

### Αλλαγή του διαχωριστικού

Ορισμένα συστήματα αναμένουν άνω τελεία (`;`) αντί για κόμμα. Μπορείτε να το προσαρμόσετε ως εξής:

```csharp
csvOptions.Delimiter = ';';
```

### Εξαγωγή συγκεκριμένου φύλλου εργασίας

Αν θέλετε να εξάγετε μόνο το δεύτερο φύλλο, αντικαταστήστε το προαιρετικό μπλοκ με:

```csharp
Worksheet sheetToExport = workbook.Worksheets[1];
workbook.Worksheets.Clear();               // Remove all sheets
workbook.Worksheets.AddCopy(sheetToExport); // Add only the chosen sheet
```

Στη συνέχεια καλέστε `workbook.Save` όπως πριν. Αυτή η τεχνική είναι χρήσιμη όταν **convert xlsx to csv** αλλά σας ενδιαφέρει μόνο μια συγκεκριμένη καρτέλα.

### Διαχείριση μεγάλων συνόλων δεδομένων

Όταν διαχειρίζεστε εκατομμύρια γραμμές, σκεφτείτε τη ροή του CSV αντί να φορτώνετε ολόκληρο το βιβλίο εργασίας στη μνήμη. Η Aspose.Cells προσφέρει την ιδιότητα `CsvSaveOptions` `ExportDataOnly` που παραλείπει τις πληροφορίες στυλ, μειώνοντας το φορτίο μνήμης:

```csharp
csvOptions.ExportDataOnly = true;
```

## Πώς να εξάγετε CSV – Επαλήθευση του αποτελέσματος

Μετά την εκτέλεση του προγράμματος, ανοίξτε το `Numbers_4sd.csv` σε έναν επεξεργαστή απλού κειμένου. Θα πρέπει να δείτε κάτι όπως:

```
ID,Value,Description
1,123.5,Sample A
2,0.9876,Sample B
3,45.67,Sample C
```

Παρατηρήστε πώς οι αριθμοί περιορίζονται σε τέσσερα σημαντικά ψηφία, ακριβώς όπως ζητήσαμε. Αν ανοίξετε το αρχείο στο Excel, οι τιμές θα εμφανιστούν ταυτόσες επειδή το Excel σέβεται το στρογγυλοποίηση που εφαρμόστηκε κατά την εξαγωγή.

## Περιπτώσεις Άκρων & Επίλυση Προβλημάτων

| Κατάσταση | Τι να ελέγξετε | Διόρθωση |
|-----------|---------------|----------|
| **Αρχείο δεν βρέθηκε** | Επαληθεύστε ότι το `sourcePath` δείχνει σε ένα πραγματικό αρχείο `.xlsx`. | Χρησιμοποιήστε `Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Numbers.xlsx")`. |
| **Λανθασμένη στρογγυλοποίηση** | Βεβαιωθείτε ότι το `SignificantDigits` έχει οριστεί πριν καλέσετε το `Save`. | Μετακινήστε την ανάθεση του `CsvSaveOptions` νωρίτερα ή ελέγξτε ξανά την τιμή. |
| **Ειδικοί χαρακτήρες εμφανίζονται ως �** | Η κωδικοποίηση CSV προεπιλέγεται ως UTF‑8 χωρίς BOM. | Ορίστε `csvOptions.Encoding = System.Text.Encoding.UTF8` ή `Encoding.Unicode`. |
| **Επιπλέον κενές στήλες** | Ορισμένα φύλλα εργασίας έχουν περιττή μορφοποίηση πέρα από την χρησιμοποιούμενη περιοχή. | Καλέστε `worksheet.Cells.MaxDisplayRange` για να περικόψετε τις αχρησιμοποίητες στήλες πριν την εξαγωγή. |

## Πώς να ορίσετε την ακρίβεια δυναμικά

Μερικές φορές η απαιτούμενη ακρίβεια δεν είναι γνωστή κατά τη μεταγλώττιση. Μπορείτε να την διαβάσετε από αρχείο ρυθμίσεων ή από όρισμα γραμμής εντολών:

```csharp
int precision = int.Parse(args.Length > 0 ? args[0] : "4");
csvOptions.SignificantDigits = precision;
```

Τώρα μπορείτε να εκτελέσετε:

```
dotnet run -- 6
```

και να λάβετε ένα CSV με έξι σημαντικά ψηφία. Αυτή η μικρή τροποποίηση κάνει τη λύση ευέλικτη για **how to export csv** σε διαφορετικά περιβάλλοντα.

## Συνοπτικό Παράδειγμα Πλήρους Λειτουργίας

Συνδυάζοντας όλα, το πλήρες πρόγραμμα (συμπεριλαμβανομένων των προαιρετικών ρυθμίσεων) φαίνεται ως εξής:

```csharp
using Aspose.Cells;
using System;
using System.IO;
using System.Text;

class CsvExporter
{
    static void Main(string[] args)
    {
        // -----------------------------------------------------------------
        // Configuration – change these paths as needed
        // -----------------------------------------------------------------
        string source = @"YOUR_DIRECTORY\Numbers.xlsx";
        string dest   = @"YOUR_DIRECTORY\Numbers_4sd.csv";

        // -----------------------------------------------------------------
        // Load workbook
        // -----------------------------------------------------------------
        Workbook wb = new Workbook(source);

        // -----------------------------------------------------------------
        // Optional: work with a specific worksheet
        // -----------------------------------------------------------------
        Worksheet ws = wb.Worksheets[0]; // first sheet
        // ws.Cells["B2"].PutValue(42);   // example modification

        // -----------------------------------------------------------------
        // Prepare CSV options – precision can be passed via args
        // -----------------------------------------------------------------
        int precision = args.Length > 0 ? int.Parse(args[0]) : 4;

        CsvSaveOptions opts = new CsvSaveOptions
        {
            SignificantDigits = precision,
            Delimiter = ',',               // change if you need ';'
            Encoding = Encoding.UTF8,
            ExportDataOnly = true          // speeds up large exports
        };

        // -----------------------------------------------------------------
        // Save as CSV
        // -----------------------------------------------------------------
        wb.Save(dest, opts);

        Console.WriteLine($"✅ Saved workbook as CSV ({precision} digits) to {dest}");
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το παραγόμενο CSV, και θα δείτε την ακρίβεια που ζητήσατε, επιβεβαιώνοντας ότι έχετε αποθηκεύσει επιτυχώς **saved workbook as CSV**.

## Συμπέρασμα

Τώρα έχετε μια σταθερή, έτοιμη για παραγωγή συνταγή για **saving a workbook as CSV** σε C#. Ο οδηγός κάλυψε *how to export Excel to CSV*, έδειξε *how to set precision* μέσω `CsvSaveOptions.SignificantDigits`, και παρουσίασε διάφορες παραλλαγές για σενάρια **convert xlsx to csv**. Με το πλήρες απόσπασμα κώδικα, μπορείτε να το ενσωματώσετε σε οποιοδήποτε έργο .NET και να αρχίσετε άμεσα την εξαγωγή δεδομένων.

**What’s next?**  

- Δοκιμάστε διαφορετικούς διαχωριστές (`;`, `\t`) για εξαγωγές TSV.  
- Συνδυάστε αυτή την προσέγγιση με έναν file‑watcher για να αυτοματοποιήσετε τη δημιουργία CSV όποτε ένα αρχείο Excel αλλάζει.  
- Εξερευνήστε το `CsvLoadOptions` της Aspose.Cells αν χρειαστεί ποτέ να διαβάσετε CSV πίσω σε ένα βιβλίο εργασίας.

Νιώστε ελεύθεροι να προσαρμόσετε την ακρίβεια, να προσθέσετε προσαρμοσμένες κεφαλίδες ή να συνδέσετε τον εξαγωγέα

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}