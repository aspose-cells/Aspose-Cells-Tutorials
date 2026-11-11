---
category: general
date: 2026-10-01
description: εναλλασσόμενα χρώματα στηλών στο Excel με χρήση C# – μάθετε πώς να δημιουργήσετε
  αρχείο Excel από DataTable, να ορίσετε το χρώμα φόντου κελιού σε C# και να εισάγετε
  DataTable στο Excel με στυλιζαρισμένες στήλες.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: el
lastmod: 2026-10-01
og_description: Τα εναλλασσόμενα χρώματα στηλών στο Excel έγιναν εύκολα. Ακολουθήστε
  αυτόν τον οδηγό για να δημιουργήσετε ένα αρχείο Excel από ένα DataTable, να ορίσετε
  το χρώμα φόντου των κελιών σε C# και να εισάγετε το DataTable στο Excel με μορφοποιημένες
  στήλες.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: Προσθήκη εναλλασσόμενων χρωμάτων στηλών στο Excel με C# – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Πώς να προσθέσετε εναλλασσόμενα χρώματα στηλών στο Excel χρησιμοποιώντας C#
url: /el/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να προσθέσετε εναλλασσόμενα χρώματα στηλών στο Excel χρησιμοποιώντας C#

Αν χρειάζεστε **alternating column colors excel** σε μια αναφορά που δημιουργείται από την εφαρμογή σας, αυτός ο οδηγός σας παρουσιάζει μια πλήρη λύση. Θα δείτε πώς να δημιουργήσετε ένα αρχείο Excel από ένα `DataTable`, να ορίσετε το χρώμα φόντου κελιού με στυλ C#, και να εισάγετε το `DataTable` στο Excel εφαρμόζοντας διαφορετικό στυλ σε κάθε στήλη.

Το tutorial καλύπτει όλα όσα χρειάζεστε: τα απαιτούμενα πακέτα NuGet, ένα πλήρες, εκτελέσιμο παράδειγμα κώδικα, και εξηγήσεις για το γιατί κάθε βήμα είναι σημαντικό. Στο τέλος θα έχετε ένα μορφοποιημένο βιβλίο εργασίας που μπορεί να ανοιχθεί απευθείας στο Microsoft Excel.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 (ή νεότερο) SDK εγκατεστημένο  
* Visual Studio 2022 (ή οποιοδήποτε IDE συμβατό με C#)  
* Τη βιβλιοθήκη **Aspose.Cells for .NET** – εγκαταστήστε την με  

```bash
dotnet add package Aspose.Cells
```

Το Aspose.Cells παρέχει τις κλάσεις `Workbook`, `Worksheet`, `Style` και `BackgroundType` που χρησιμοποιούνται στο παράδειγμα.

## Βήμα 1: Ανάκτηση των πηγαίων δεδομένων ως `DataTable`

Το πρώτο καθήκον είναι η λήψη των δεδομένων που θέλετε να εξάγετε. Σε πραγματικά έργα μπορεί να γεμίσετε το `DataTable` από ένα ερώτημα βάσης δεδομένων, κλήση API ή οποιαδήποτε συλλογή στη μνήμη.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Γιατί είναι σημαντικό:**  
Ένα `DataTable` είναι ένας καθολικός δοχείο που αντιστοιχεί άμεσα σε ένα φύλλο εργασίας Excel. Χρησιμοποιώντας `DataTable` μπορείτε να **create excel file from datatable c#** χωρίς να γράψετε προσαρμοσμένους βρόχους για κάθε στήλη.

## Βήμα 2: Δημιουργία νέου βιβλίου εργασίας και λήψη του πρώτου φύλλου

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Εξήγηση:**  
`Workbook` είναι το αντικείμενο ρίζας· `Worksheets[0]` σας δίνει το προεπιλεγμένο φύλλο όπου θα τοποθετηθούν τα δεδομένα.

## Βήμα 3: Προετοιμασία διαφορετικού στυλ για κάθε στήλη (εναλλασσόμενα χρώματα φόντου)

Για να επιτύχουμε **alternating column colors excel**, δημιουργούμε ένα `Style` για κάθε στήλη και του αναθέτουμε ένα ανοιχτό χρώμα φόντου που εναλλάσσεται μεταξύ δύο αποχρώσεων.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Γιατί χρησιμοποιούμε βρόχο:**  
Ο βρόχος εγγυάται ότι το **set cell background color c#** εφαρμόζεται ομοιόμορφα, ακόμη και αν ο αριθμός των στηλών αλλάξει κατά την εκτέλεση. Αυτό κάνει τη λύση ανθεκτική για δυναμικές αναφορές.

## Βήμα 4: Εισαγωγή του `DataTable` στο φύλλο εργασίας, εφαρμόζοντας τα στυλ στηλών

Το Aspose.Cells μπορεί να εισάγει ένα `DataTable` απευθείας, και μπορούμε να περάσουμε τον πίνακα στυλ για να χρωματίσουμε κάθε στήλη.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Τι συμβαίνει στο παρασκήνιο:**  
`ImportDataTable` γράφει τη γραμμή κεφαλίδας, στη συνέχεια κάθε γραμμή δεδομένων. Επειδή παρείχαμε `columnStyles`, κάθε κελί σε μια δεδομένη στήλη λαμβάνει το αντίστοιχο στυλ, δίνοντάς μας τα επιθυμητά εναλλασσόμενα χρώματα.

## Βήμα 5: Αποθήκευση του μορφοποιημένου βιβλίου εργασίας σε αρχείο

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Όταν ανοίξετε το *StyledTable.xlsx* στο Excel, θα δείτε κάθε στήλη να χρωματίζεται εναλλακτικά, κάνοντας τον πίνακα πιο ευανάγνωστο.

## Πλήρες, εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα κομμάτια, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, να επικολλήσετε και να εκτελέσετε.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Αναμενόμενο αποτέλεσμα

* Ένα αρχείο με όνομα **StyledTable.xlsx** στο `C:\Temp\`.
* Το φύλλο εργασίας εμφανίζει τρεις στήλες (`Id`, `Name`, `Score`) με εναλλασσόμενα χρώματα φόντου: στήλες 1 και 3 σε *LightYellow*, στήλη 2 σε *LightCyan*.
* Όλες οι γραμμές από το `DataTable` εμφανίζονται κάτω από τη γραμμή κεφαλίδας.

## Συχνές ερωτήσεις και ειδικές περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| *Μπορώ να χρησιμοποιήσω άλλα χρώματα;* | Ναι. Αντικαταστήστε το `System.Drawing.Color.LightYellow` και `LightCyan` με οποιαδήποτε τιμή `System.Drawing.Color`. |
| *Τι γίνεται αν το DataTable έχει πολλές στήλες;* | Ο βρόχος δημιουργεί αυτόματα ένα στυλ για κάθε στήλη, οπότε το μοτίβο κλιμακώνεται χωρίς αλλαγές κώδικα. |
| *Πρέπει να απελευθερώσω το βιβλίο εργασίας;* | Το Aspose.Cells υλοποιεί `IDisposable`. Αν τυλίξετε το `Workbook` σε ένα μπλοκ `using`, οι πόροι απελευθερώνονται άμεσα. |
| *Πώς να εφαρμόσω τα ίδια εναλλασσόμενα χρώματα σε γραμμές αντί για στήλες;* | Δημιουργήστε ένα `Style[]` για τις γραμμές και καλέστε `worksheet.Cells.ImportDataTable(..., rowStyles)` – το Aspose.Cells παρέχει υπερφορτώσεις και για τις δύο περιπτώσεις. |
| *Μπορώ να γράψω το αρχείο απευθείας σε ροή (π.χ., για web API);* | Ναι. Χρησιμοποιήστε `workbook.Save(stream, SaveFormat.Xlsx);` αντί για διαδρομή αρχείου. |

## Συμβουλές από το πεδίο

* **Συμβουλή επαγγελματία:** Κρατήστε στα cache τα αντικείμενα στυλ αν δημιουργείτε πολλά φύλλα εργασίας σε μία εκτέλεση – η δημιουργία στυλ είναι σχετικά φθηνή, αλλά η επαναχρησιμοποίησή τους μειώνει την κατανάλωση μνήμης.  
* **Προσοχή:** Όταν χρησιμοποιείτε `System.Drawing.Color` σε πλατφόρμες εκτός των Windows, προσθέστε το πακέτο NuGet `System.Drawing.Common` και βεβαιωθείτε ότι το runtime υποστηρίζει GDI+.

## Συμπέρασμα

Τώρα ξέρετε πώς να **alternating column colors excel** δημιουργώντας ένα αρχείο Excel από ένα `DataTable` σε C#, ορίζοντας χρώματα φόντου κελιού με Aspose.Cells, και **import datatable to excel** με έναν στυλιζαρισμένο πίνακα στηλών. Αυτή η προσέγγιση είναι γρήγορη, συντηρήσιμη και λειτουργεί με οποιοδήποτε μέγεθος συνόλου δεδομένων.

### Επόμενα βήματα

* Εξερευνήστε το **set cell background color c#** για μορφοποίηση υπό όρους (π.χ., επισήμανση χαμηλών σκορ).  
* Συνδυάστε αυτήν την τεχνική με το **create excel file from datatable c#** για δημιουργία αναφορών πολλαπλών φύλλων.  
* Ρίξτε μια ματιά στο API γραφημάτων του Aspose.Cells για να προσθέσετε οπτικές περιλήψεις στο ίδιο βιβλίο εργασίας.

Αισθανθείτε ελεύθεροι να προσαρμόσετε τα χρώματα, τη μορφή αρχείου ή την πηγή δεδομένων ώστε να ταιριάζουν στις ανάγκες του έργου σας. Καλό coding!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίησή σας.

- [Set Column Background in Excel with C# – Complete Guide](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Add background color excel – Alternating Row Styles in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Create Workbook C# – Import DataTable to Excel with Styles](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}