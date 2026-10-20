---
category: general
date: 2026-03-22
description: Προσαρμοσμένη μορφή αριθμού στο Excel – σεμινάριο που δείχνει πώς να
  εισάγετε datatable στο Excel, να ορίσετε χρώμα φόντου στήλης, να μορφοποιήσετε τη
  στήλη ως νόμισμα και να αποθηκεύσετε το βιβλίο εργασίας ως xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: el
og_description: Προσαρμοσμένο μάθημα Excel για μορφοποίηση αριθμών που σας καθοδηγεί
  στη εισαγωγή ενός DataTable, στον ορισμό χρώματος φόντου στήλης, στη μορφοποίηση
  στήλης ως νόμισμα και στην αποθήκευση του βιβλίου εργασίας ως xlsx.
og_title: Προσαρμοσμένη μορφή αριθμού στο Excel με C# – Οδηγός βήμα‑προς‑βήμα
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Προσαρμοσμένη μορφή αριθμού στο Excel με C# – Πλήρης οδηγός
url: /el/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσαρμοσμένη Μορφή Αριθμών Excel – Full‑Stack C# Tutorial

Έχετε αναρωτηθεί ποτέ πώς να εφαρμόσετε ένα **custom number format excel** στυλ απευθείας από C#; Ίσως έχετε προσπαθήσει να αποβάλετε ένα DataTable σε ένα υπολογιστικό φύλλο μόνο για να δείτε απλούς αριθμούς, χωρίς χρώματα και χωρίς μορφοποίηση νομίσματος. Αυτό είναι ένα κοινό πρόβλημα—ιδιαίτερα όταν χρειάζεστε μια επαγγελματική αναφορά για τα ενδιαφερόμενα μέρη.

Σε αυτόν τον οδηγό θα λύσουμε αυτό το πρόβλημα μαζί: θα μάθετε πώς να **import datatable to excel**, **set column background color**, **format column as currency**, και τέλος **save workbook as xlsx** με μια προσαρμοσμένη μορφή αριθμού που κάνει τα νούμερά σας να ξεχωρίζουν. Καμία ασαφής αναφορά, μόνο μια πλήρης, εκτελέσιμη λύση που μπορείτε να αντιγράψετε‑επικολλήσετε στο έργο σας.

---

## Τι Θα Δημιουργήσετε

Στο τέλος αυτού του tutorial θα έχετε μια αυτόνομη εφαρμογή C# console που:

1. Ανακτά ένα `DataTable` (μπορείτε να αντικαταστήσετε το stub με το δικό σας ερώτημα).  
2. Δημιουργεί ένα νέο Excel workbook χρησιμοποιώντας το Aspose.Cells (ή οποιαδήποτε συμβατή βιβλιοθήκη).  
3. Εφαρμόζει μια μπλε, έντονη γραμματοσειρά στην πρώτη στήλη, ένα ανοιχτό‑κίτρινο φόντο στη δεύτερη, και μια μορφή νομίσματος (`$#,##0.00`) στην τρίτη.  
4. Αποθηκεύει το αρχείο ως `DataTableWithStyleArray.xlsx` σε έναν φάκελο της επιλογής σας.

Θα δείτε ακριβώς πώς κάθε γραμμή συμβάλλει στο τελικό αρχείο Excel, και θα συζητήσουμε γιατί αυτές οι επιλογές έχουν σημασία για τη συντηρησιμότητα και την απόδοση.

---

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).  
- Aspose.Cells για .NET (δωρεάν δοκιμή ή έκδοση με άδεια). Εγκατάσταση μέσω NuGet:

```bash
dotnet add package Aspose.Cells
```

- Βασική εξοικείωση με `DataTable` και εφαρμογές C# console.

---

## Βήμα 1: Ανάκτηση των Πηγαίων Δεδομένων ως DataTable

Πρώτα, χρειαζόμαστε κάποια δεδομένα για εξαγωγή. Σε ένα πραγματικό σενάριο πιθανότατα θα καλέσετε ένα repository ή θα εκτελέσετε ένα ερώτημα SQL. Για παραδείγματα θα δημιουργήσουμε έναν απλό πίνακα στη μνήμη.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Γιατί είναι σημαντικό:** Η χρήση ενός `DataTable` σας παρέχει μια πινάκωση, σχήμα‑συνειδητή πηγή που αντιστοιχεί καθαρά σε σειρές και στήλες του Excel. Σας επιτρέπει επίσης να επαναχρησιμοποιήσετε την ίδια λογική εξαγωγής για οποιοδήποτε σύνολο δεδομένων χωρίς να ξαναγράψετε κώδικα.

---

## Βήμα 2: Δημιουργία Νέου Workbook και Λήψη του Πρώτου Worksheet

Τώρα δημιουργούμε ένα Excel workbook. Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο· το `Worksheets[0]` είναι το προεπιλεγμένο φύλλο όπου θα τοποθετήσουμε τα δεδομένα μας.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Συμβουλή:** Αν χρειάζεστε πολλαπλά φύλλα, απλώς καλέστε `workbook.Worksheets.Add("SheetName")` και επαναλάβετε τα βήματα στυλ για το καθένα.

---

## Βήμα 3: Ορισμός Στυλ Στηλών – Γραμματοσειρά, Φόντο και Μορφή Αριθμού

Το στυλ στο Aspose.Cells γίνεται μέσω αντικειμένων `Style`. Θα δημιουργήσουμε έναν πίνακα όπου κάθε στοιχείο αντιστοιχεί σε μια στήλη του DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Γιατί ένας πίνακας στυλ;** Η μεταβίβαση ενός πίνακα στο `ImportDataTable` σας επιτρέπει να εφαρμόσετε διαφορετικό στυλ σε κάθε στήλη με μία κλήση, κάτι που είναι τόσο σύντομο όσο και αποδοτικό. Επίσης εγγυάται ότι η μορφοποίηση παραμένει συγχρονισμένη με τη σειρά των δεδομένων.

---

## Βήμα 4: Εισαγωγή του DataTable Κατά την Εφαρμογή των Στυλ

Αυτή είναι η καρδιά της λειτουργίας: τροφοδοτούμε το `DataTable` στο worksheet, λέμε στο Aspose να συμπεριλάβει τη γραμμή κεφαλίδας, και παραδίδουμε τον πίνακα `columnStyles`.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **Τι συμβαίνει στο παρασκήνιο;** Το Aspose διασχίζει κάθε στήλη, γράφει την κεφαλίδα, μετά γράφει κάθε τιμή γραμμής. Κατά τη διάρκεια εφαρμόζει το αντίστοιχο `Style` από τον πίνακα, έτσι καταλήγετε με μια μπλε κεφαλίδα για το “Product”, μια κίτρινη σκίαση για το “Quantity”, και μια ωραία μορφοποιημένη στήλη “Revenue”.

---

## Βήμα 5: Αποθήκευση του Workbook ως Αρχείο XLSX

Τέλος, αποθηκεύουμε το workbook στο δίσκο. Η μέθοδος `Save` επιλέγει αυτόματα τη μορφή XLSX βάσει της επέκτασης του αρχείου.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Συμβουλή:** Αν χρειάζεστε να μεταφέρετε το αρχείο (π.χ., για web API), χρησιμοποιήστε `workbook.Save(stream, SaveFormat.Xlsx)` αντί για διαδρομή αρχείου.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να επικολλήσετε σε ένα νέο έργο console. Συγκεντρώνεται και εκτελείται ακριβώς όπως είναι, παράγοντας ένα μορφοποιημένο αρχείο Excel.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Όταν ανοίξετε το `DataTableWithStyleArray.xlsx` θα δείτε:

| **Product** (μπλε, έντονο) | **Quantity** (ανοιχτό‑κίτρινο) | **Revenue** (νόμισμα) |
|----------------------------|--------------------------------|------------------------|
| Widget A                   | 120                            | $3,450.75              |
| Widget B                   | 85                             | $2,190.00              |
| Widget C                   | 60                             | $1,580.40              |

Η **custom number format excel** που καθορίσατε (`$#,##0.00`) εξασφαλίζει ότι κάθε κελί εσόδων εμφανίζει το σύμβολο δολαρίου, το διαχωριστικό χιλιάδων και δύο δεκαδικά ψηφία—ακριβώς αυτό που αναμένουν οι οικονομικές ομάδες.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Μπορώ να το χρησιμοποιήσω με διαφορετική βιβλιοθήκη Excel;

Απόλυτα. Η έννοια—δημιουργία στυλ ανά στήλη και εφαρμογή του κατά την εισαγωγή—μεταφράζεται σε EPPlus, ClosedXML ή NPOI. Οι κλήσεις API διαφέρουν, αλλά το μοτίβο παραμένει το ίδιο.

### Τι γίνεται αν το DataTable μου έχει περισσότερες στήλες από τα στυλ;

Το Aspose θα εφαρμόσει το προεπιλεγμένο στυλ σε οποιαδήποτε στήλη δεν έχει αντίστοιχο στοιχείο στον πίνακα `columnStyles`. Για να αποφύγετε εκπλήξεις, είτε ορίστε το μέγεθος του πίνακα σε `dataTable.Columns.Count` είτε δημιουργήστε στυλ δυναμικά σε έναν βρόχο.

### Πώς ορίζω προσαρμοσμένη μορφή αριθμού για ημερομηνίες;

Απλώς ορίστε `style.Custom = "dd‑mm‑yyyy"` (ή οποιοδήποτε έγκυρο Excel format string). Η ίδια προσέγγιση με πίνακα λειτουργεί για ημερομηνίες, ποσοστά ή επιστημονική σημειογραφία.

### Υπάρχει τρόπος αυτόματης προσαρμογής του πλάτους των στηλών μετά την εισαγωγή;

Ναι—καλέστε `worksheet.AutoFitColumns();` μετά την εισαγωγή. Εκτελεί έναν γρήγορο υπολογισμό πλάτους βάσει του περιεχομένου των κελιών.

### Τι γίνεται με μεγάλα σύνολα δεδομένων (100k+ γραμμές);

Το `ImportDataTable` είναι βελτιστοποιημένο για μαζικές λειτουργίες, αλλά μπορεί να φτάσετε τα όρια μνήμης. Σε αυτήν την περίπτωση, σκεφτείτε τη ροή των γραμμών χειροκίνητα με `Cells[i, j].PutValue(...)` και την επαναχρησιμοποίηση ενός μόνο αντικειμένου `Style` για μείωση του φόρτου.

---

## Επαγγελματικές Συμβουλές & Συνηθισμένα Πάγια

- **Αποφύγετε την σκληρή κωδικοποίηση διαδρομών** σε κώδικα παραγωγής· χρησιμοποιήστε `Environment.GetFolderPath` ή ρυθμίσεις παραμετροποίησης.  
- **Αποδεσμεύστε το workbook** αν βρίσκεστε σε υπηρεσία μακράς διάρκειας—τυλίξτε το σε μπλοκ `using` για να ελευθερώσετε τους εγγενείς πόρους.  
- **Προσέξτε τους διαχωριστές ανάλογα με τον πολιτισμό**. Η προσαρμοσμένη μορφή `$#,##0.00` επιβάλλει τελεία ως διαχωριστικό δεκαδικών ανεξάρτητα από την τοπική ρύθμιση του OS, κάτι που συνήθως θέλετε για οικονομικές αναφορές.  
- **Θυμηθείτε να αναφέρετε το System.Drawing** (ή `System.Drawing.Common` σε .NET Core) για τις δομές χρώματος που χρησιμοποιούνται στο στυλ.  
- **Δοκιμάστε το αποτέλεσμα σε διαφορετικές εκδόσεις του Excel**· οι παλαιότερες εκδόσεις μπορεί να ερμηνεύσουν κάποιες προσαρμοσμένες μορφές ελαφρώς διαφορετικά.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για να **custom number format excel** αρχεία από C#: την ανάκτηση δεδομένων από ένα `DataTable`, **import datatable to excel**, την εφαρμογή **set column background color**, τη χρήση **format column as currency**, και τέλος **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}