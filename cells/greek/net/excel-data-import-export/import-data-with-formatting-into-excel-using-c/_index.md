---
category: general
date: 2026-03-01
description: Εισαγωγή δεδομένων με μορφοποίηση στο Excel χρησιμοποιώντας C#. Μάθετε
  πώς να εισάγετε DataTable στο Excel και να προσθέτετε χρώμα φόντου στα κελιά σε
  λίγα μόνο βήματα.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: el
og_description: Εισαγωγή δεδομένων με μορφοποίηση στο Excel χρησιμοποιώντας C#. Οδηγός
  βήμα‑προς‑βήμα που δείχνει πώς να εισάγετε ένα DataTable και να προσθέσετε χρώμα
  φόντου στα κελιά.
og_title: Εισαγωγή δεδομένων με μορφοποίηση στο Excel – Οδηγός C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: Εισαγωγή δεδομένων με μορφοποίηση στο Excel χρησιμοποιώντας C#
url: /el/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εισαγωγή Δεδομένων με Μορφοποίηση στο Excel χρησιμοποιώντας C#

## Τι Θα Μάθετε

- Πώς να ανακτήσετε δεδομένα σε ένα `DataTable`.
- Πώς να ορίσετε έναν πίνακα αντικειμένων `Style` που μεταφέρουν χρώματα φόντου.
- Πώς να καλέσετε το `ImportDataTable` με αυτά τα στυλ ώστε η εισαγωγή να διατηρεί τη μορφοποίηση.
- Ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε σε μια εφαρμογή κονσόλας και να δείτε το αποτέλεσμα άμεσα.
- Συμβουλές, παγίδες και παραλλαγές για πραγματικά έργα.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+).
- Η βιβλιοθήκη **GemBox.Spreadsheet** (η δωρεάν έκδοση είναι επαρκής για τη demo).
- Βασική εξοικείωση με C# και τις έννοιες του Excel.

Αν αναρωτιέστε *γιατί GemBox;* επειδή προσφέρει μια μεθόδους `ImportDataTable` σε μία γραμμή που δέχεται πίνακες στυλ — ακριβώς αυτό που χρειαζόμαστε για **εισαγωγή δεδομένων με μορφοποίηση** χωρίς να γράψουμε βρόχο.

---

## Βήμα 1: Ρύθμιση του Έργου και Προσθήκη του GemBox.Spreadsheet

Για να ξεκινήσετε, δημιουργήστε μια νέα εφαρμογή κονσόλας:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Συμβουλή επαγγελματία:** Η δωρεάν έκδοση περιορίζει τα φύλλα εργασίας σε 150 k κελιά, κάτι που είναι άφθονο για demos. Αν φτάσετε το όριο, αναβαθμίστε ή μεταβείτε σε EPPlus, αλλά το API θα φαίνεται ελαφρώς διαφορετικό.

## Βήμα 2: Ανάκτηση των Πηγαίων Δεδομένων ως `DataTable`

Το πρώτο πράγμα που χρειάζεστε είναι ένα `DataTable` που μιμείται τα δεδομένα που συνήθως αντλείτε από μια βάση δεδομένων. Εδώ είναι ένας μικρός βοηθός που δημιουργεί ένα στη μνήμη:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Γιατί είναι σημαντικό:** Διαχωρίζοντας την ανάκτηση δεδομένων σε μια δική του μέθοδο, μπορείτε να αντικαταστήσετε οποιαδήποτε πηγή — SQL, CSV, web service — χωρίς να επηρεάσετε τη λογική εισαγωγής. Αυτό διατηρεί τον κώδικα καθαρό και κάνει το tutorial **how to import datatable into excel** επαναχρησιμοποιήσιμο.

## Βήμα 3: Ορισμός των Στυλ που Θέλετε να Εφαρμόσετε

Τώρα έρχεται το διασκεδαστικό μέρος: θα δημιουργήσουμε έναν πίνακα αντικειμένων `Style`, καθένα με διαφορετικό `ForegroundColor`. Το GemBox σας επιτρέπει να ορίσετε `BackgroundPatternColor` (το γέμισμα του κελιού) και `ForegroundColor` (το χρώμα του κειμένου). Για αυτή τη demo θα χρωματίσουμε τις πρώτες δύο στήλες διαφορετικά.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Επεξήγηση:**  
- `Style` αντικείμενα είναι ελαφριά containers· δεν χρειάζεται να δημιουργήσετε ένα νέο για κάθε κελί.  
- Συμφωνώντας τη σειρά του πίνακα με τη σειρά των στηλών, το GemBox εφαρμόζει αυτόματα το αντίστοιχο στυλ κατά την εισαγωγή.  
- Αυτό είναι το κλειδί για **εισαγωγή δεδομένων με μορφοποίηση** — η μορφοποίηση μεταφέρεται μαζί με τα δεδομένα, όχι μετά.

## Βήμα 4: Εισαγωγή του `DataTable` στο Φύλλο Εργασίας με Στυλ

Με τα δεδομένα και τα στυλ έτοιμα, μπορούμε τώρα να δημιουργήσουμε ένα βιβλίο εργασίας, να επιλέξουμε το πρώτο φύλλο εργασίας και να καλέσουμε το `ImportDataTable`. Η υπογραφή της μεθόδου είναι ως εξής:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Αυτή είναι η χρήση του:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Τι συμβαίνει στο παρασκήνιο;**  
- `true` λέει στο GemBox να γράψει τα ονόματα των στηλών ως την πρώτη σειρά.  
- `0, 0` τοποθετεί την εισαγωγή στο κελί A1.  
- `importStyles` συνδέει κάθε στήλη με τα χρώματα που ορίσαμε νωρίτερα.  

Όταν ανοίξετε το *Report.xlsx*, θα δείτε τη στήλη **ID** με ανοιχτό μπλε χρώμα, τη στήλη **Name** με ανοιχτό πράσινο χρώμα, και τη στήλη **Score** αμετάβλητη. Αυτό είναι **εισαγωγή δεδομένων με μορφοποίηση** με μία κλήση.

## Βήμα 5: Επαλήθευση του Αποτελέσματος (Αναμενόμενο Αποτέλεσμα)

Ανοίξτε το παραγόμενο `Report.xlsx`. Θα πρέπει να δείτε κάτι όπως αυτό:

| ID (light blue) | Name (light green) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- Τα κελιά της στήλης **ID** έχουν φόντο ανοιχτό‑μπλε.  
- Τα κελιά της στήλης **Name** έχουν φόντο ανοιχτό‑πράσινο.  
- Η στήλη **Score** παραμένει με το προεπιλεγμένο λευκό φόντο.

Αυτό το οπτικό cue κάνει την αναφορά άμεσα αναγνώσιμη — μια μικρή πινελιά που μπορεί να βελτιώσει δραματικά την εμπειρία του χρήστη.

![Excel sheet showing import data with formatting – ID column light blue, Name column light green](excel-screenshot.png "παράδειγμα εισαγωγής δεδομένων με μορφοποίηση")

*Το κείμενο alt της εικόνας περιλαμβάνει τη βασική λέξη-κλειδί για SEO.*

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Μπορώ να εφαρμόσω κάτι παραπάνω από χρώματα φόντου;

Απολύτως. Το `Style` σας επιτρέπει να ορίσετε γραμματοσειρές, περιθώρια, μορφές αριθμών και ακόμη και conditional formatting. Για παράδειγμα, για να κάνετε τα σκορ πάνω από 90 έντονα και κόκκινα:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Τι γίνεται αν το DataTable μου έχει περισσότερες στήλες από τα στυλ;

Το GemBox θα εφαρμόσει στυλ μόνο στις στήλες που έχουν αντίστοιχο στοιχείο στον πίνακα. Οι επιπλέον στήλες θα χρησιμοποιήσουν το προεπιλεγμένο στυλ — δεν θα προκληθεί σφάλμα.

### Λειτουργεί αυτό με μεγάλα σύνολα δεδομένων;

Ναι, αλλά προσέξτε το όριο κελιών της δωρεάν έκδοσης (150 k κελιά). Για τεράστιες αναφορές, σκεφτείτε την επί πληρωμή άδεια ή τη ροή των δεδομένων γραμμή‑με‑γραμμή με `worksheet.Cells[row, col].Value = …` — αν και θα χάσετε την ευκολία της μίας γραμμής.

### Πώς μπορώ να εισάγω δεδομένα με μορφοποίηση από ένα υπάρχον πρότυπο Excel;

Μπορείτε πρώτα να φορτώσετε ένα βιβλίο εργασίας προτύπου:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Αυτό σας επιτρέπει να διατηρήσετε τα λογότυπα κεφαλίδας, τα υποσέλιδα και τυχόν προϋπάρχοντα στυλ, ενώ εξακολουθείτε να **εισάγετε δεδομένα με μορφοποίηση** για το δυναμικό τμήμα.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Εκτελέστε το πρόγραμμα (`dotnet run`) και ανοίξτε το παραγόμενο *Report.xlsx* για να δείτε τα χρώματα να εφαρμόζονται άμεσα.

---

## Συμπέρασμα

Τώρα έχετε μια σταθερή, τελική

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}