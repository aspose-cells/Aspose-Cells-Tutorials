---
category: general
date: 2026-07-03
description: Εφαρμόστε εναλλασσόμενα χρώματα στις γραμμές κατά την εισαγωγή πίνακα
  δεδομένων στο Excel χρησιμοποιώντας C#. Μάθετε πώς να εξάγετε πίνακα δεδομένων C#
  σε Excel, να αποθηκεύσετε το στυλιζαρισμένο φύλλο Excel και να διατηρήσετε τη μορφοποίηση
  του βιβλίου εργασίας.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: el
og_description: Εφαρμόστε εναλλασσόμενα χρώματα γραμμών στο Excel χρησιμοποιώντας
  C#. Αυτό το σεμινάριο δείχνει πώς να εισάγετε datatable στο Excel, να εξάγετε datatable
  C# στο Excel και να αποθηκεύσετε το βιβλίο εργασίας με μορφοποίηση.
og_title: Εφαρμόστε εναλλασσόμενα χρώματα γραμμών στο Excel με C# – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: Εφαρμογή εναλλασσόμενων χρωμάτων γραμμών στο Excel με C# – Πλήρης οδηγός
url: /el/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εφαρμογή Εναλλασσόμενων Χρωμάτων Γραμμών στο Excel με C# – Πλήρης Οδηγός

Κάποτε χρειάστηκε να **εφαρμόσετε εναλλασσόμενα χρώματα γραμμών** όταν εξάγετε ένα C# `DataTable` σε Excel; Δεν είστε ο μόνος—οι προγραμματιστές ρωτούν συνεχώς πώς να κάνουν αυτά τα φύλλα εργασίας να φαίνονται επαγγελματικά χωρίς να παρεμβαίνουν χειροκίνητα στο Excel μετά. Τα καλά νέα; Μπορείτε να το κάνετε προγραμματιστικά με λίγες μόνο γραμμές κώδικα.

Σε αυτό το tutorial θα περάσουμε από **import datatable to excel**, θα σας δείξουμε πώς να **export c# datatable to excel** με έναν μορφοποιημένο πίνακα, και τελικά **save styled table excel** διατηρώντας τη μορφοποίηση. Στο τέλος θα μπορείτε να **save workbook with formatting** που φαίνεται έτοιμο για παρουσίαση σε πελάτη.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (το δείγμα χρησιμοποιεί .NET 6, αλλά οποιαδήποτε πρόσφατη έκδοση λειτουργεί)
- Aspose.Cells for .NET (δωρεάν δοκιμή ή αδειοδοτημένη έκδοση) – αυτή η βιβλιοθήκη κάνει το styling παιχνιδάκι
- Μια πηγή `DataTable` (μπορεί να προέρχεται από βάση δεδομένων, CSV ή συλλογή στη μνήμη)

> **Συμβουλή:** Αν δεν έχετε ήδη το Aspose.Cells, μπορείτε να το αποκτήσετε από το NuGet με `dotnet add package Aspose.Cells`.

## Βήμα 1: Ρύθμιση του Έργου και Φόρτωση των Δεδομένων σας

Πρώτα, δημιουργήστε μια εφαρμογή console (ή οποιοδήποτε έργο C#) και προσθέστε τις απαραίτητες δηλώσεις `using`. Στη συνέχεια φορτώστε τα δεδομένα σε ένα `DataTable`. Για παράδειγμα, θα δημιουργήσουμε έναν απλό πίνακα επί τόπου.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Γιατί είναι σημαντικό:** Έχοντας ένα `DataTable` έτοιμο, μπορείτε να **import datatable to excel** με μία κλήση, εξαλείφοντας την ανάγκη για χειροκίνητη εισαγωγή κελιού‑με‑κελί.

## Βήμα 2: Δημιουργία ενός Workbook και Ορισμός των Στυλ Εναλλασσόμενων Γραμμών

Τώρα θα δημιουργήσουμε ένα νέο `Workbook`. Το κόλπο για **εφαρμόσετε εναλλασσόμενα χρώματα γραμμών** βρίσκεται στο `ImportTableOptions.StyleArray`. Θα χρησιμοποιήσουμε τα πρώτα δύο ενσωματωμένα στυλ (συνήθως λευκό και ανοιχτό γκρι), αλλά μπορείτε να τα προσαρμόσετε αργότερα.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Εξήγηση:** Το `ImportTableOptions` λέει στο Aspose.Cells πώς να αντιμετωπίσει κάθε γραμμή κατά την εισαγωγή. Παρέχοντας ένα `StyleArray` με δύο στοιχεία, η βιβλιοθήκη βαφά αυτόματα κάθε περιττή γραμμή με το πρώτο στυλ και κάθε ζυγή με το δεύτερο—ακριβώς αυτό που χρειάζεστε για **εφαρμόσετε εναλλασσόμενα χρώματα γραμμών**.

## Βήμα 3: Φόρτωση του DataTable στο Worksheet (Συμπεριλαμβανομένων των Κεφαλίδων)

Με το workbook και τα στυλ έτοιμα, τώρα **import datatable to excel**. Η μέθοδος `ImportDataTable` κάνει το βαρύ έργο: γράφει τις κεφαλίδες των στηλών, σέβεται το style array και τοποθετεί τα δεδομένα ξεκινώντας από το κελί A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Γιατί συμπεριλαμβάνουμε `true` ως δεύτερο όρισμα:** Λέει στη μέθοδο να γράψει τα ονόματα των στηλών ως πρώτη γραμμή, κάτι απαραίτητο για μια επαγγελματική αναφορά.

## Βήμα 4: Λεπτομερής Ρύθμιση του Πίνακα (Προαιρετικό αλλά Χρήσιμο)

Αν θέλετε ο πίνακας να προσαρμόζει αυτόματα τις στήλες ή να προσθέσετε μια γραμμή φίλτρου, μερικές επιπλέον γραμμές τον κάνουν να λάμπει.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

Αυτές οι μικρές βελτιώσεις δεν επηρεάζουν τα εναλλασσόμενα χρώματα, αλλά βελτιώνουν τη συνολική εμπειρία χρήστη του αρχείου **save styled table excel**.

## Βήμα 5: Αποθήκευση του Workbook Διατηρώντας Όλη τη Μορφοποίηση

Τέλος, γράφουμε το αρχείο στο δίσκο. Η μέθοδος `Save` διατηρεί κάθε στυλ που ορίσαμε, εξασφαλίζοντας ότι οι εναλλασσόμενες γραμμές παραμένουν αμετάβλητες.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Όταν ανοίξετε το `StyledEmployees.xlsx`, θα δείτε έναν καθαρό πίνακα όπου οι γραμμές εναλλάσσονται μεταξύ λευκού και ανοιχτό‑γκρι—ακριβώς το οπτικό cue που πολλοί χρήστες βασίζονται για ευανάγνωστη παρουσίαση.

### Αναμενόμενη Έξοδος

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- Γραμμή 1, 3 … → λευκό φόντο  
- Γραμμή 2, 4 … → ανοιχτό‑γκρι φόντο  

Αυτή είναι η πλήρης διαδικασία **save workbook with formatting**.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το DataTable μου έχει χιλιάδες γραμμές;

Η μέθοδος `ImportDataTable` μεταδίδει τα δεδομένα αποδοτικά, αλλά μπορεί να αντιμετωπίσετε όρια μνήμης σε πολύ μεγάλους πίνακες. Σε τέτοιες περιπτώσεις, σκεφτείτε να χωρίσετε την εξαγωγή σε πολλαπλά worksheets ή να χρησιμοποιήσετε την υπερφόρτωση `ImportDataTable` που επιτρέπει τον καθορισμό αρχικής γραμμής και στήλης.

### Μπορώ να χρησιμοποιήσω προσαρμοσμένα χρώματα αντί των ενσωματωμένων;

Απολύτως. Απλώς αντικαταστήστε τις αναθέσεις `ForegroundColor` στα `styleWhite` και `styleGray` με οποιοδήποτε `System.Drawing.Color` προτιμάτε—σκεφτείτε παστέλ μπλε ή χρώματα εταιρικής ταυτότητας.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### Πώς μπορώ να εξασφαλίσω ότι το εναλλασσόμενο στυλ λειτουργεί όταν ο χρήστης προσθέτει γραμμές αργότερα;

Αν οι χρήστες επεξεργαστούν το αρχείο χειροκίνητα, ο αρχικός πίνακας στυλ δεν θα επεκταθεί αυτόματα. Μια γρήγορη λύση είναι να μετατρέψετε την περιοχή σε Excel Table (`ListObject`) μετά την εισαγωγή· το Excel τότε επαναλαμβάνει το μοτίβο για νέες γραμμές.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

Τώρα κάθε νέα γραμμή κληρονομεί τα εναλλασσόμενα χρώματα.

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα σε Ένα Σημείο)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το παραγόμενο αρχείο και θα δείτε αμέσως τα εναλλασσόμενα χρώματα εφαρμοσμένα—χωρίς καμία χειροκίνητη μορφοποίηση.

## Συμπέρασμα

Δείξαμε πώς να **εφαρμόσετε εναλλασσόμενα χρώματα γραμμών** όταν **import datatable to excel** χρησιμοποιώντας C#. Η διαδικασία καλύπτει όλα όσα χρειάζεστε για **export c# datatable to excel**, **save styled table excel**, και **save workbook with formatting** που φαίνεται επαγγελματικό αμέσως.

Τι θα κάνετε μετά; Δοκιμάστε να ανταλλάξετε τα δύο στυλ για ένα προσαρμοσμένο θέμα, ή μετατρέψτε την περιοχή σε Excel Table ώστε οι χρήστες να μπορούν να ταξινομούν και να φιλτράρουν διατηρώντας το χρωματικό μοτίβο. Μπορείτε επίσης να εξερευνήσετε conditional formatting μέσω `ConditionalFormattingCollection` για πιο δυναμικά οπτικά σήματα.

Got a twist

## Τι Πρέπει Να Μάθετε Στη Σειρά;

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εισάγετε DataTable στο Excel Χρησιμοποιώντας Aspose.Cells για .NET (Βήμα‑Βήμα Οδηγός)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Εφαρμογή Χρωμάτων & Φόντων στο Excel χρησιμοποιώντας Aspose.Cells για .NET](/cells/english/net/formatting/colors-and-background/)
- [Αυτοματοποιήστε τα Χρώματα Θέματος του Excel Χρησιμοποιώντας Aspose.Cells .NET για Αποδοτική Μορφοποίηση](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}