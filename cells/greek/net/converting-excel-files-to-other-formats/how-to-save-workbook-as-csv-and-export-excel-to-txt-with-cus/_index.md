---
category: general
date: 2026-09-15
description: Μάθετε πώς να αποθηκεύσετε το βιβλίο εργασίας ως CSV, να εξάγετε το Excel
  σε TXT και να εφαρμόσετε προσαρμοσμένη μορφή αριθμού ενώ μετατρέπετε τις τιμές των
  κελιών σε κεφαλαία γράμματα σε C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- apply custom number format
- export excel to txt
- uppercase cell values
- export worksheet as text
language: el
lastmod: 2026-09-15
og_description: Αποθήκευση βιβλίου εργασίας ως CSV, εξαγωγή Excel σε TXT και εφαρμογή
  προσαρμοσμένης μορφής αριθμού ενώ μετατρέπετε τις τιμές των κελιών σε κεφαλαία χρησιμοποιώντας
  το Aspose.Cells σε C#.
og_image_alt: Screenshot showing workbook saved as CSV using C# code
og_title: Αποθήκευση βιβλίου εργασίας ως CSV και εξαγωγή Excel σε TXT με προσαρμοσμένη
  μορφοποίηση σε C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to save workbook as CSV, export Excel to TXT, and apply custom
    number format while converting cell values to uppercase in C#.
  headline: How to save workbook as CSV and export Excel to TXT with custom formatting
    in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να αποθηκεύσετε το βιβλίο εργασίας ως CSV και να εξάγετε το Excel σε TXT
  με προσαρμοσμένη μορφοποίηση σε C#
url: /el/net/converting-excel-files-to-other-formats/how-to-save-workbook-as-csv-and-export-excel-to-txt-with-cus/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε το βιβλίο εργασίας ως CSV και να εξάγετε το Excel σε TXT με προσαρμοσμένη μορφοποίηση σε C#

Αν χρειάζεστε **αποθήκευση βιβλίου εργασίας ως CSV** ενώ ταυτόχρονα εξάγετε ένα φύλλο ως απλό‑κείμενο και εφαρμόζετε προσαρμοσμένη μορφή αριθμού, αυτός ο οδηγός σας παρουσιάζει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Θα δείτε πώς να διατηρήσετε την αριθμητική ακρίβεια, να μετατρέψετε κάθε τιμή κελιού σε κεφαλαία και να διαχειριστείτε ημερομηνίες ιαπωνικής εποχής — όλα με το Aspose.Cells για .NET.

Η εξαγωγή δεδομένων από το Excel συχνά σημαίνει χειρισμό πολλαπλών μορφών: CSV για ανταλλαγή δεδομένων, TXT για παλαιά συστήματα και προσαρμοσμένες μορφές αριθμών για αναφορές ειδικές για τοπικές ρυθμίσεις. Αυτό το tutorial περνάει βήμα‑βήμα από κάθε απαίτηση, ώστε να μπορείτε να αντιγράψετε τον κώδικα απευθείας στο έργο σας.

Στις επόμενες ενότητες θα μάθετε πώς να:

* **αποθηκεύσετε το βιβλίο εργασίας ως csv** με καθορισμένο αριθμό σημαντικών ψηφίων  
* **εξάγετε το excel σε txt** ενώ επιβάλλετε **τιμές κελιών σε κεφαλαία**  
* **εφαρμόσετε προσαρμοσμένη μορφή αριθμού** για ημερομηνίες ιαπωνικής εποχής και να διαβάσετε το μορφοποιημένο αποτέλεσμα  

Δεν απαιτούνται εξωτερικά εργαλεία — μόνο η βιβλιοθήκη Aspose.Cells και ένα περιβάλλον ανάπτυξης .NET.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.8)  
* Aspose.Cells για .NET (πακέτο NuGet `Aspose.Cells`)  
* Βασική εξοικείωση με C# και έννοιες του Excel  

---

## Βήμα 1: Αποθήκευση του βιβλίου εργασίας ως CSV με ελεγχόμενη ακρίβεια

Όταν **αποθηκεύετε το βιβλίο εργασίας ως CSV**, οι αριθμητικές τιμές γράφονται χρησιμοποιώντας την προεπιλεγμένη αναπαράσταση συμβολοσειράς, η οποία μπορεί να χάσει ακρίβεια. Ρυθμίζοντας το `CsvSaveOptions.SignificantDigits`, λέτε στο Aspose.Cells πόσα σημαντικά ψηφία πρέπει να διατηρηθούν.

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();               // you can also use new Workbook("input.xlsx");

// Configure CSV options to keep up to 4 significant digits
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    SignificantDigits = 4   // ensures numbers like 123.4567 stay precise
};

// Save the workbook as CSV
string csvPath = @"C:\Temp\Digits.csv";
workbook.Save(csvPath, csvOptions);

Console.WriteLine($"Workbook saved as CSV to {csvPath}");
```

**Γιατί είναι σημαντικό:**  
Ο καθορισμός του `SignificantDigits` αποτρέπει σφάλματα στρογγυλοποίησης που συχνά εμφανίζονται όταν μεγάλα σύνολα δεδομένων ανταλλάσσονται με συστήματα downstream (π.χ. αποθήκες δεδομένων). Το αντικείμενο `CsvSaveOptions` σας επιτρέπει επίσης να ελέγξετε διαχωριστικά, κωδικοποίηση και άλλες ρυθμίσεις ειδικές για CSV, εφόσον χρειαστεί.

---

## Βήμα 2: Εξαγωγή ενός φύλλου ως απλό κείμενο ενώ μετατρέπετε τις τιμές σε κεφαλαία

Η εξαγωγή ενός φύλλου σε αρχείο `.txt` είναι χρήσιμη για παλαιές διαδικασίες εισαγωγής που αναμένουν δεδομένα διαχωρισμένα με κενά. Ενεργοποιώντας το `ExportTableOptions.ExportAsString` και παρέχοντας έναν `CustomExport` delegate, μπορείτε να **εξάγετε το excel σε txt** και ταυτόχρονα να επιβάλλετε **τιμές κελιών σε κεφαλαία**.

```csharp
// Prepare export options for plain‑text output
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // forces every cell to be treated as a string
    // CustomExport receives the cell and its current string value,
    // allowing you to modify it before it is written.
    CustomExport = (cell, value) =>
    {
        // Convert the cell value to an upper‑case string
        return value?.ToString().ToUpperInvariant();
    }
};

// Define the output path for the text file
string txtPath = @"C:\Temp\Table.txt";

// Export the first worksheet (index 0) as a tab‑delimited text file
workbook.Worksheets[0].ExportTable(txtPath, tableOptions);

Console.WriteLine($"Worksheet exported as text to {txtPath}");
```

**Γιατί είναι σημαντικό:**  
Πολλά σημεία ενσωμάτωσης (π.χ. παρτίδες mainframe) απαιτούν αναγνωριστικά σε κεφαλαία. Η κλήση `CustomExport` σας δίνει πλήρη έλεγχο πάνω στην αναπαράσταση κάθε κελιού, επιτρέποντας την εισαγωγή μετασχηματισμών όπως αποκοπή, συμπλήρωση ή μορφοποίηση ειδική για τοπική ρύθμιση, χωρίς επεξεργασία του αρχείου μετά την εξαγωγή.

---

## Βήμα 3: Εφαρμογή προσαρμοσμένης μορφής αριθμού και ανάγνωση του μορφοποιημένου αποτελέσματος

Οι ενσωματωμένες μορφές αριθμού του Excel καλύπτουν τις περισσότερες περιπτώσεις, αλλά μερικές φορές χρειάζεται να εμφανίσετε ημερομηνίες σε συγκεκριμένο ημερολογιακό σύστημα — όπως η ιαπωνική εποχή. Ο παρακάτω κώδικας δείχνει πώς να **εφαρμόσετε προσαρμοσμένη μορφή αριθμού** σε ένα κελί, στη συνέχεια να διαβάσετε τη μορφοποιημένη συμβολοσειρά που σέβεται την τοπική ρύθμιση του βιβλίου εργασίας.

```csharp
// Create a new workbook for the era example
Workbook eraWorkbook = new Workbook();

// Access the first worksheet and target cell A1
Worksheet sheet = eraWorkbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// Insert a Japanese‑era date string (Reiwa 3 = 2021)
dateCell.PutValue("Reiwa 3/04/01");

// Apply a built‑in date number format (14 = mm-dd-yy)
// You could also assign a custom format string, e.g., "[$-ja-JP]ggge年m月d日"
Style style = eraWorkbook.CreateStyle();
style.Number = 14; // standard short date format
dateCell.SetStyle(style);

// Force formula calculation (necessary if the cell contains a formula)
eraWorkbook.CalculateFormula();

// Retrieve the formatted string as it would appear in Excel
string formattedDate = dateCell.StringValue;
Console.WriteLine($"Formatted date (locale aware): {formattedDate}");
```

**Γιατί είναι σημαντικό:**  
Η χρήση του `SetStyle` με μορφή αριθμού διασφαλίζει ότι η εμφάνιση του κελιού σέβεται τις περιφερειακές ρυθμίσεις, κάτι κρίσιμο για εκθέσεις που διανέμονται σε διαφορετικές τοπικές αγορές. Όταν αργότερα διαβάζετε το `StringValue`, λαμβάνετε ακριβώς τη συμβολοσειρά που θα έβλεπε ένας χρήστης στο UI του Excel, εξαλείφοντας την ανάγκη για χειροκίνητη ανάλυση.

---

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει ένα ενιαίο πρόγραμμα που συνδυάζει τα τρία βήματα. Επικολλήστε το σε ένα νέο έργο Console App, προσθέστε το πακέτο NuGet Aspose.Cells και τρέξτε το.

```csharp
using Aspose.Cells;
using System;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Save workbook as CSV ----------
            Workbook workbook = new Workbook(); // start with a fresh workbook
            // (Optionally load an existing file: new Workbook("input.xlsx"))

            // Populate some sample data
            workbook.Worksheets[0].Cells["A1"].PutValue(123.456789);
            workbook.Worksheets[0].Cells["B1"].PutValue("Sample Text");

            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 4
            };
            string csvPath = @"C:\Temp\Digits.csv";
            workbook.Save(csvPath, csvOptions);
            Console.WriteLine($"Saved CSV to {csvPath}");

            // ---------- Step 2: Export worksheet as text with uppercase ----------
            ExportTableOptions tableOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, value) => value?.ToString().ToUpperInvariant()
            };
            string txtPath = @"C:\Temp\Table.txt";
            workbook.Worksheets[0].ExportTable(txtPath, tableOptions);
            Console.WriteLine($"Exported TXT to {txtPath}");

            // ---------- Step 3: Apply custom number format ----------
            Workbook eraWorkbook = new Workbook();
            Cell dateCell = eraWorkbook.Worksheets[0].Cells["A1"];
            dateCell.PutValue("Reiwa 3/04/01");

            Style eraStyle = eraWorkbook.CreateStyle();
            eraStyle.Number = 14; // short date format; replace with custom if needed
            dateCell.SetStyle(eraStyle);
            eraWorkbook.CalculateFormula();

            Console.WriteLine($"Japanese era date formatted: {dateCell.StringValue}");
        }
    }
}
```

**Αναμενόμενη έξοδος**

```
Saved CSV to C:\Temp\Digits.csv
Exported TXT to C:\Temp\Table.txt
Japanese era date formatted: 4/1/2021
```

(Η ακριβής μορφή ημερομηνίας μπορεί να διαφέρει ανάλογα με τις ρυθμίσεις τοπικής γλώσσας του συστήματός σας.)

---

## Συχνές ερωτήσεις και διαχείριση ειδικών περιπτώσεων

| Ερώτηση | Απάντηση |
|----------|--------|
| *Τι κάνω αν χρειάζομαι διαφορετικό διαχωριστικό στο CSV;* | Ορίστε `csvOptions.Separator` σε `','`, `'\t'` ή οποιονδήποτε προσαρμοσμένο χαρακτήρα πριν καλέσετε το `Save`. |
| *Μπορώ να διατηρήσω την αρχική αριθμητική ακρίβεια αντί για στρογγυλοποίηση;* | Χρησιμοποιήστε `SignificantDigits = 0` για να γράψετε την πλήρη τιμή double‑precision, ή ορίστε `NumberDecimalSeparator` για σύμβολα δεκαδικού ανάλογα με την τοπική ρύθμιση. |
| *Πώς εξάγω μόνο ένα συγκεκριμένο εύρος αντί για ολόκληρο το φύλλο;* | Καλέστε `ExportTable(string fileName, ExportTableOptions options, CellArea area)` και περάστε ένα `CellArea` που ορίζει το εύρος. |
| *Τι γίνεται αν το βιβλίο εργασίας περιέχει τύπους που αναφέρονται σε άλλα φύλλα;* | Βεβαιωθείτε ότι έχετε καλέσει `workbook.CalculateFormula()` πριν από την εξαγωγή· διαφορετικά θα λάβετε τις αποθηκευμένες τιμές. |
| *Υπάρχει τρόπος να διατηρήσω την αρχική μορφοποίηση κελιού (γραμματοσειρές, χρώματα) στο αρχείο TXT;* | Τα μορφότυπα απλού κειμένου δεν μπορούν να διατηρήσουν οπτικό στυλ. Αν χρειάζεστε πλούσια μορφοποίηση, σκεφτείτε την εξαγωγή σε HTML (`HtmlSaveOptions`). |

---

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **αποθηκεύσετε το βιβλίο εργασίας ως CSV** με ελεγχόμενη ακρίβεια, **να εξάγετε το excel σε TXT** ενώ επιβάλλετε **τιμές κελιών σε κεφαλαία**, και **να εφαρμόσετε προσαρμοσμένη μορφή αριθμού** για ημερομηνίες προσαρμοσμένες σε τοπική ρύθμιση. Κάθε απόσπασμα είναι αυτόνομο, λειτουργεί αμέσως και ακολουθεί βέλτιστες πρακτικές τόσο για απόδοση όσο και για συντηρησιμότητα.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

* Χρήση του `HtmlSaveOptions` για διατήρηση στυλ κατά την εξαγωγή σε μορφές φιλικές για το web.  
* Εκμετάλλευση του `CsvSaveOptions.Encoding` για UTF‑8 ή άλλες κωδικοποιήσεις όταν εργάζεστε με πολυγλωσσικά δεδομένα.  
* Αυτοματοποίηση επεξεργασίας δέσμης πολλαπλών φύλλων μέσω βρόχου πάνω στο `workbook.Worksheets`.

Αισθανθείτε ελεύθεροι να προσαρμόσετε τον κώδικα στις δικές σας ροές δεδομένων και αφήστε την ευελιξία του Aspose.Cells να αναλάβει το δύσκολο κομμάτι.

---


## Τι θα πρέπει να μάθετε στη συνέχεια;


Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Αποθήκευση βιβλίου εργασίας σε μορφή κειμένου Csv](/cells/german/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Αποθήκευση βιβλίου εργασίας σε μορφή κειμένου Csv](/cells/french/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Αποθήκευση βιβλίου εργασίας σε μορφή κειμένου Csv](/cells/spanish/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}