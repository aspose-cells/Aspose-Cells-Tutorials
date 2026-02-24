---
category: general
date: 2026-01-14
description: Εξαγωγή πίνακα σε CSV με C# και μάθετε πώς να ορίσετε προσαρμοσμένη μορφή
  αριθμού, να γράψετε CSV σε αρχείο και να ενεργοποιήσετε αυτόματο υπολογισμό—όλα
  σε ένα σεμινάριο.
draft: false
keywords:
- export table to csv
- set custom number format
- write csv to file
- enable automatic calculation
- how to format numbers
language: el
og_description: Εξαγωγή πίνακα σε CSV με προσαρμοσμένες μορφές αριθμών, εγγραφή CSV
  σε αρχείο και ενεργοποίηση αυτόματου υπολογισμού χρησιμοποιώντας το Aspose.Cells
  σε C#.
og_title: Εξαγωγή Πίνακα σε CSV – Πλήρης Οδηγός C#
tags:
- Aspose.Cells
- C#
- CSV export
- Excel automation
title: Εξαγωγή Πίνακα σε CSV – Πλήρης Οδηγός C# με Προσαρμοσμένες Μορφές Αριθμών
url: /el/net/csv-file-handling/export-table-to-csv-complete-c-guide-with-custom-number-form/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Πίνακα σε CSV – Πλήρης Οδηγός C# με Προσαρμοσμένες Μορφές Αριθμών

Έχετε ποτέ χρειαστεί να **εξάγετε πίνακα σε CSV** αλλά δεν ήσασταν σίγουροι πώς να διατηρήσετε τους αριθμούς σας τακτοποιημένους; Δεν είστε μόνοι. Σε πολλές περιπτώσεις εξαγωγής δεδομένων θέλετε οι αριθμοί να μορφοποιούνται όμορφα, το CSV να γράφεται στο δίσκο και το βιβλίο εργασίας να παραμένει συγχρονισμένο με τυχόν τύπους. Αυτό το σεμινάριο σας δείχνει ακριβώς **πώς να εξάγετε πίνακα σε CSV**, πώς να **ορίσετε προσαρμοσμένη μορφή αριθμού**, πώς να **γράψετε CSV σε αρχείο**, και πώς να **ενεργοποιήσετε τον αυτόματο υπολογισμό** ώστε όλα να παραμένουν ενημερωμένα.

Θα περάσουμε από ένα πραγματικό παράδειγμα χρησιμοποιώντας το Aspose.Cells for .NET. Στο τέλος αυτού του οδηγού θα έχετε ένα ενιαίο, εκτελέσιμο πρόγραμμα C# που:

* Μορφοποιεί ένα κελί με προσαρμοσμένο αριθμητικό μοτίβο (το τμήμα «πώς να μορφοποιήσετε αριθμούς»).
* Εξάγει τον πρώτο πίνακα του φύλλου εργασίας σε συμβολοσειρά CSV με έναν διαχωριστή της επιλογής σας.
* Αποθηκεύει αυτή τη συμβολοσειρά CSV σε αρχείο στο δίσκο.
* Αναλύει μια ημερομηνία ιαπωνικής περιόδου και την γράφει πίσω στο φύλλο.
* Ενεργοποιεί τον αυτόματο υπολογισμό ώστε οι τύποι δυναμικού πίνακα να επαναϋπολογίζονται πάντα.

Δεν απαιτούνται εξωτερικές αναφορές—απλώς αντιγράψτε, επικολλήστε και εκτελέστε.

![Export table to CSV illustration](export-table-to-csv.png "Διάγραμμα εξαγωγής πίνακα σε CSV"){: alt="Διάγραμμα εξαγωγής πίνακα σε CSV που δείχνει το βιβλίο εργασίας, τον πίνακα και το αποτέλεσμα CSV"}

---

## Τι θα χρειαστείτε

* **Aspose.Cells for .NET** (πακέτο NuGet `Aspose.Cells`). Ο κώδικας λειτουργεί με την έκδοση 23.9 ή νεότερη.
* Ένα περιβάλλον ανάπτυξης .NET (Visual Studio, Rider ή `dotnet CLI`).
* Βασική εξοικείωση με τη σύνταξη C#—τίποτα περίπλοκο, μόνο τις συνήθεις δηλώσεις `using` και τη μέθοδο `Main`.

## Βήμα 1 – Ορισμός Προσαρμοσμένης Μορφής Αριθμού (Πώς να Μορφοποιήσετε Αριθμούς)

Πριν εξάγουμε οτιδήποτε, ας βεβαιωθούμε ότι οι αριθμοί εμφανίζονται όπως θέλουμε. Η ιδιότητα `Custom` ενός αντικειμένου `Style` σας επιτρέπει να ορίσετε ένα μοτίβο όπως `"0.####"` για να εμφανίζει έως και τέσσερα δεκαδικά ψηφία ενώ αφαιρεί τα μηδενικά στο τέλος.

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Put a raw double value into cell A1
        worksheet.Cells[0, 0].PutValue(123.456789);

        // 3️⃣ Define a custom number format – this is the “how to format numbers” piece
        Style numberStyle = workbook.CreateStyle();
        numberStyle.Custom = "0.####"; // up to 4 significant digits
        worksheet.Cells[0, 0].SetStyle(numberStyle);
```

**Γιατί είναι σημαντικό:**  
Όταν αργότερα εξάγετε τον πίνακα σε CSV, ο ακατέργαστος double `123.456789` θα εμφανιζόταν ως `123.456789`. Με την προσαρμοσμένη μορφή, το CSV θα περιέχει `123.4568` (στρογγυλοποιημένο σε τέσσερα δεκαδικά) – ακριβώς αυτό που αναμένουν τα περισσότερα εργαλεία αναφοράς.

## Βήμα 2 – Εξαγωγή Πίνακα σε CSV (Κύριος Στόχος)

Το Aspose.Cells αντιμετωπίζει μια περιοχή δεδομένων ως `Table`. Ακόμη και αν δεν έχετε δημιουργήσει ρητά έναν, το πρώτο φύλλο εργασίας περιέχει πάντα έναν προεπιλεγμένο πίνακα στο δείκτη 0. Η εξαγωγή αυτού του πίνακα γίνεται με μία μόνο γραμμή κώδικα μόλις έχετε ρυθμίσει το `ExportTableOptions`.

```csharp
        // 4️⃣ Grab the first table in the worksheet
        Table firstTable = worksheet.Tables[0];

        // 5️⃣ Configure export options – we want a CSV string, comma‑delimited
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            Delimiter = ","
        };

        // 6️⃣ Export to a CSV string
        string csvContent = firstTable.ExportToString(exportOptions);

        // Show what we got (optional debug output)
        Console.WriteLine("=== CSV CONTENT ===");
        Console.WriteLine(csvContent);
```

**Αναμενόμενη έξοδος CSV** (με βάση την προσαρμοσμένη μορφή από το Βήμα 1):

```
123.4568
```

Παρατηρήστε πώς ο αριθμός τηρεί το μοτίβο `"0.####"` που ορίσαμε νωρίτερα. Αυτή είναι η μαγεία του **export table to csv** σε συνδυασμό με ένα προσαρμοσμένο αριθμητικό στυλ.

## Βήμα 3 – Γράψιμο CSV σε Αρχείο (Διατήρηση Δεδομένων)

Τώρα που έχουμε μια συμβολοσειρά CSV, πρέπει να την αποθηκεύσουμε. Η μέθοδος `File.WriteAllText` κάνει τη δουλειά, και μπορούμε να τοποθετήσουμε το αρχείο όπου θέλουμε—απλώς αντικαταστήστε το `"YOUR_DIRECTORY"` με μια πραγματική διαδρομή.

```csharp
        // 7️⃣ Define where to save the CSV file
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "table.csv");

        // 8️⃣ Write the CSV string to disk – this is the “write csv to file” step
        File.WriteAllText(outputPath, csvContent);
        Console.WriteLine($"CSV file written to: {outputPath}");
```

**Συμβουλή:** Αν χρειάζεστε διαφορετικό διαχωριστικό (ερωτηματικό, tab, pipe), απλώς αλλάξτε το `Delimiter` στο `ExportTableOptions`. Το υπόλοιπο του κώδικα παραμένει το ίδιο, καθιστώντας την προσαρμογή εύκολη.

## Βήμα 4 – Ανάλυση Ημερομηνίας Ιαπωνικής Περιόδου (Επιπλέον Διασκέδαση)

Συχνά θα χρειαστεί να διαχειριστείτε ημερομηνίες ειδικές για τοπική ρύθμιση. Το Aspose.Cells περιλαμβάνει ένα `DateTimeParser` που καταλαβαίνει αλφαριθμητικά ιαπωνικής περιόδου όπως `"R02/04/01"` (Reiwa 2 = 2020). Ας τοποθετήσουμε αυτήν την ημερομηνία στην επόμενη γραμμή.

```csharp
        // 9️⃣ Set up a parser for Japanese‑era dates
        DateTimeParser eraParser = new DateTimeParser { Calendar = CalendarType.JapaneseEra };
        DateTime reiwaDate = eraParser.Parse("R02/04/01"); // 2020‑04‑01

        // 10️⃣ Write the parsed date into cell A2
        worksheet.Cells[1, 0].PutValue(reiwaDate);
```

Το κελί τώρα περιέχει μια πραγματική τιμή `DateTime`, την οποία το Excel (ή οποιοσδήποτε προβολέας) θα εμφανίσει σύμφωνα με τις περιφερειακές ρυθμίσεις του βιβλίου εργασίας.

## Βήμα 5 – Ενεργοποίηση Αυτόματου Υπολογισμού (Διατήρηση Τύπων Ενημερωμένων)

Αν το βιβλίο εργασίας σας περιέχει τύπους—ιδιαίτερα τύπους δυναμικού πίνακα—θα θέλετε να επαναϋπολογίζονται αυτόματα μετά την αλλαγή των δεδομένων. Η αλλαγή της λειτουργίας υπολογισμού γίνεται με μια μόνο αλλαγή ιδιότητας.

```csharp
        // 11️⃣ Turn on automatic calculation so formulas stay up‑to‑date
        workbook.Settings.CalcMode = CalculationMode.Automatic;

        // 12️⃣ Force a calculation pass (optional but ensures everything is up‑to‑date now)
        workbook.CalculateFormula();

        // Cleanup: save the workbook if you want to inspect it later
        string xlsPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "demo.xlsx");
        workbook.Save(xlsPath);
        Console.WriteLine($"Workbook saved to: {xlsPath}");
    }
}
```

**Γιατί να ενεργοποιήσετε τον αυτόματο υπολογισμό;**  
Όταν αργότερα ανοίξετε το `demo.xlsx` στο Excel, οποιοσδήποτε τύπος που αναφέρεται στον προσαρμοσμένο αριθμό ή στην ημερομηνία ιαπωνικής περιόδου θα αντικατοπτρίζει ήδη τις πιο πρόσφατες τιμές. Αυτό είναι το τμήμα “enable automatic calculation” του σεμιναρίου μας.

## Πλήρες Παράδειγμα Λειτουργίας (Όλα τα Βήματα Μαζί)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, έτοιμο για αντιγραφή‑και‑επικόλληση. Δεν λείπουν τμήματα· απλώς το εκτελέστε και παρακολουθήστε την έξοδο της κονσόλας και τα αρχεία που εμφανίζονται στην επιφάνεια εργασίας σας.

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Set a number with a custom format (how to format numbers)
        worksheet.Cells[0, 0].PutValue(123.456789);
        Style numberStyle = workbook.CreateStyle();
        numberStyle.Custom = "0.####";
        worksheet.Cells[0, 0].SetStyle(numberStyle);

        // Export the first table to CSV (export table to csv)
        Table firstTable = worksheet.Tables[0];
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            Delimiter = ","
        };
        string csvContent = firstTable.ExportToString(exportOptions);
        Console.WriteLine("=== CSV CONTENT ===");
        Console.WriteLine(csvContent);

        // Write CSV to file (write csv to file)
        string csvPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "table.csv");
        File.WriteAllText(csvPath, csvContent);
        Console.WriteLine($"CSV file written to: {csvPath}");

        // Parse a Japanese‑era date and write it to the sheet
        DateTimeParser eraParser = new DateTimeParser { Calendar = CalendarType.JapaneseEra };
        DateTime reiwaDate = eraParser.Parse("R02/04/01");
        worksheet.Cells[1, 0].PutValue(reiwaDate);

        // Enable automatic calculation (enable automatic calculation)
        workbook.Settings.CalcMode = CalculationMode.Automatic;
        workbook.CalculateFormula();

        // Save the workbook for inspection
        string xlsPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "demo.xlsx");
        workbook.Save(xlsPath);
        Console.WriteLine($"Workbook saved to: {xlsPath}");
    }
}
```

**Λίστα ελέγχου αποτελεσμάτων**

| ✅ | Τι θα πρέπει να δείτε |
|---|----------------------|
| Αρχείο CSV `table.csv` στην επιφάνεια εργασίας σας που περιέχει `123.4568` |
| Αρχείο Excel `demo.xlsx` στην επιφάνεια εργασίας σας με τον προσαρμοσμένο αριθμό στο A1 και την ημερομηνία ιαπωνικής περιόδου (2020‑04‑01) στο A2 |
| Έξοδος κονσόλας που επιβεβαιώνει κάθε βήμα |

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**Ε: Τι γίνεται αν ο πίνακάς μου έχει κεφαλίδες;**  
Α: Το `ExportTableOptions` σέβεται την ιδιότητα `ShowHeaders` του πίνακα. Ορίστε `firstTable.ShowHeaders = true;` πριν την εξαγωγή, και το CSV θα περιλαμβάνει αυτόματα τη σειρά κεφαλίδων.

**Ε: Μπορώ να εξάγω πολλούς πίνακες ταυτόχρονα;**  
Α: Απόλυτα. Επανάληψη μέσω `worksheet.Tables` και συνένωση των συμβολοσειρών CSV, ή αποθήκευση του καθενός σε ξεχωριστό αρχείο. Θυμηθείτε να προσαρμόσετε το `Delimiter` αν χρειάζεστε διαφορετικό διαχωριστικό ανά αρχείο.

**Ε: Οι αριθμοί μου χρειάζονται διαχωριστικό χιλιάδων (π.χ., `1,234.56`).**  
Α: Αλλάξτε την προσαρμοσμένη μορφή σε `"#,##0.##"` και το εξαγόμενο CSV θα περιέχει τα κόμματα. Λάβετε υπόψη ότι ορισμένα προγράμματα CSV θεωρούν τα κόμματα ως διαχωριστικά, οπότε μπορεί να μεταβείτε σε ερωτηματικό (`Delimiter = ";"`) για να αποφύγετε τη σύγχυση.

**Ε: Στοχεύω στο .NET 6—υπάρχουν προβλήματα συμβατότητας;**  
Α: Όχι. Το Aspose.Cells 23.9+ στοχεύει στο .NET Standard 2.0+, επομένως λειτουργεί άψογα με .NET 6, .NET 7, και ακόμη και .NET Framework 4.8.

## Σύνοψη

Έχουμε καλύψει πώς να **export table to csv** διατηρώντας μια **custom number format**, πώς να **write csv to file**, και πώς να **enable automatic calculation** ώστε το βιβλίο εργασίας σας να παραμένει συγχρονισμένο. Επιπλέον, προσθέσαμε μια γρήγορη επίδειξη ανάλυσης ιαπωνικής‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}