---
category: general
date: 2026-02-21
description: Μάθετε πώς να μορφοποιείτε στήλες όταν εισάγετε ένα DataTable στο Excel
  χρησιμοποιώντας C#. Περιλαμβάνει συμβουλές για το χρώμα της δεύτερης στήλης στο
  Excel και την εισαγωγή DataTable στο Excel με C#.
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: el
og_description: Πώς να μορφοποιήσετε στήλες κατά την εισαγωγή ενός DataTable στο Excel
  χρησιμοποιώντας C#. Βήμα‑βήμα κώδικας, χρωματισμός της δεύτερης στήλης στο Excel
  και βέλτιστες πρακτικές.
og_title: Πώς να μορφοποιήσετε στήλες στο Excel με C# – Πλήρης οδηγός
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Πώς να μορφοποιήσετε στήλες στο Excel με C# – Εισαγωγή DataTable
url: /el/net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μορφοποιήσετε στήλες σε Excel με C# – Εισαγωγή DataTable

Έχετε αναρωτηθεί **πώς να μορφοποιήσετε στήλες** σε ένα φύλλο εργασίας Excel ενώ αντλείτε δεδομένα απευθείας από ένα `DataTable`; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν δυσκολία όταν χρειάζονται μια γρήγορη πινελιά χρώματος — ίσως κόκκινο για την πρώτη στήλη, μπλε για τη δεύτερη — χωρίς να πρέπει να παίζουν χειροκίνητα με κάθε κελί μετά την εισαγωγή.  

Τα καλά νέα; Η λύση είναι μερικές γραμμές κώδικα C# και θα έχετε ένα πλήρως μορφοποιημένο φύλλο τη στιγμή που τα δεδομένα θα φορτωθούν. Σε αυτό το tutorial θα καλύψουμε επίσης **import datatable to excel**, θα σας δείξουμε **color second column excel**, και θα εξηγήσουμε γιατί η προσέγγιση λειτουργεί τόσο για .NET Framework όσο και για έργα .NET 6+.

---

## Τι θα μάθετε

- Ανάκτηση ενός γεμάτου `DataTable` (ή δημιουργία ενός εν κινήσει).  
- Ορισμός αντικειμένων `Style` ανά στήλη για ορισμό χρωμάτων προσκηνίου.  
- Δημιουργία βιβλίου εργασίας, λήψη του πρώτου φύλλου και εισαγωγή του πίνακα με τις εφαρμοσμένες μορφές.  
- Διαχείριση περιπτώσεων όπως κενά tables, προσαρμοσμένες αρχικές γραμμές και δυναμικός αριθμός στηλών.  

Στο τέλος, θα μπορείτε να δημιουργείτε ένα μορφοποιημένο αρχείο Excel σε οποιοδήποτε pipeline αναφοράς — χωρίς ανάγκη μετα-επεξεργασίας.

> **Prerequisite:** Βασική εξοικείωση με C# και μια βιβλιοθήκη spreadsheet που υποστηρίζει `ImportDataTable` (π.χ., Aspose.Cells, GemBox.Spreadsheet, ή EPPlus με βοηθητικό). Ο κώδικας παρακάτω χρησιμοποιεί **Aspose.Cells** επειδή η υπερφόρτωση `ImportDataTable` δέχεται άμεσα ένα `Style[]`.

---

## Βήμα 1: Ρύθμιση του έργου και προσθήκη της βιβλιοθήκης Excel

Πριν μπορέσουμε να μορφοποιήσουμε οτιδήποτε, χρειαζόμαστε ένα έργο που να αναφέρει μια βιβλιοθήκη διαχείρισης Excel.

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*Pro tip:* Αν χρησιμοποιείτε .NET 6, προσθέστε το πακέτο μέσω `dotnet add package Aspose.Cells`. Η βιβλιοθήκη λειτουργεί σε Windows, Linux και macOS, οπότε είστε έτοιμοι για το μέλλον.

---

## Βήμα 2: Ανάκτηση ή δημιουργία του πηγαίου DataTable

Ο πυρήνας του tutorial εστιάζει στη μορφοποίηση, αλλά χρειάζεστε πάντοτε ένα `DataTable`. Παρακάτω υπάρχει ένας γρήγορος βοηθός που δημιουργεί δείγμα δεδομένων· αντικαταστήστε τον με τη δική σας κλήση `GetTable()` στην παραγωγή.

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **Why this matters:** Η χρήση ενός `DataTable` κρατά την πηγή δεδομένων ανεξάρτητη — είτε προέρχεται από SQL, CSV ή μια συλλογή στη μνήμη, η λογική εισαγωγής παραμένει η ίδια. Αυτό είναι το θεμέλιο του **how to import datatable** αποδοτικά.

---

## Βήμα 3: Ορισμός στυλ στηλών (Η καρδιά του “How to Style Columns”)

Τώρα λέμε στο φύλλο πώς πρέπει να φαίνεται κάθε στήλη. Η κλάση `Style` σας επιτρέπει να ορίσετε γραμματοσειρές, χρώματα, περιγράμματα κ.λπ. Σε αυτό το παράδειγμα αλλάζουμε μόνο το χρώμα προσκηνίου.

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*What if you have more columns?* Απλώς αυξήστε το μέγεθος του πίνακα και συμπληρώστε τα στυλ που σας ενδιαφέρουν. Οι στήλες χωρίς στυλ κληρονομούν αυτόματα το προεπιλεγμένο στυλ του φύλλου.

---

## Βήμα 4: Δημιουργία του Workbook και εισαγωγή του DataTable με στυλ

Με τα δεδομένα και τα στυλ έτοιμα, ήρθε η ώρα να τα ενώσουμε.

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**What just happened?**  
- Η `ImportDataTable` αντιγράφει γραμμές, στήλες και *προαιρετικά* τη γραμμή κεφαλίδας.  
- Με τη μεταβλητή `columnStyles`, κάθε στήλη λαμβάνει το `Style` που ορίσαμε νωρίτερα.  
- Η κλήση είναι μια μόνο γραμμή, που σημαίνει ότι το **import datatable excel c#** είναι τόσο απλό όσο αυτό.

---

## Βήμα 5: Επαλήθευση του αποτελέσματος – Αναμενόμενο αποτέλεσμα

Ανοίξτε το `StyledDataTable.xlsx` στο Excel (ή LibreOffice). Θα πρέπει να δείτε:

| **ID** (κόκκινο) | **Όνομα** (μπλε) | **Σκορ** (προεπιλογή) |
|------------------|------------------|-----------------------|
| 1                | Alice            | 92.5                  |
| 2                | Bob              | 85.3                  |
| …                | …                | …                     |

- Το κείμενο της πρώτης στήλης εμφανίζεται **κόκκινο**, ικανοποιώντας την απαίτηση “how to style columns”.  
- Το κείμενο της δεύτερης στήλης είναι **μπλε**, καλύπτοντας επίσης το ερώτημα **color second column excel**.  

Αν το αρχείο ανοίξει χωρίς σφάλματα, έχετε κατακτήσει με επιτυχία το **how to import datatable** ενώ μορφοποιείτε στήλες.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το DataTable είναι κενό;
Η `ImportDataTable` θα δημιουργήσει ακόμα τη γραμμή κεφαλίδας (αν περάσατε `true`). Δεν προστίθενται γραμμές δεδομένων, αλλά τα στυλ εφαρμόζονται ακόμα στα κελιά της κεφαλίδας.

### Χρειάζεται να ξεκινήσετε την εισαγωγή από διαφορετικό κελί;
Αλλάξτε τις παραμέτρους `rowIndex` και `columnIndex` στην `ImportDataTable`. Για παράδειγμα, για να ξεκινήσετε από το `B2` χρησιμοποιήστε `1, 1` αντί για `0, 0`.

### Θέλετε να μορφοποιήσετε γραμμές αντί για στήλες;
Μπορείτε να κάνετε βρόχο μέσω `worksheet.Cells.Rows` μετά την εισαγωγή και να αναθέσετε ένα `Style` ανά γραμμή. Ωστόσο, η μορφοποίηση σε επίπεδο στήλης είναι πολύ πιο αποδοτική επειδή η βιβλιοθήκη εφαρμόζει το στυλ μία φορά ανά στήλη.

### Χρησιμοποιείτε EPPlus ή ClosedXML;
Αυτές οι βιβλιοθήκες δεν εκθέτουν άμεση υπερφόρτωση `ImportDataTable` με πίνακα στυλ. Η εναλλακτική λύση είναι να εισάγετε πρώτα τον πίνακα, μετά να διασχίσετε την περιοχή στηλών και να ορίσετε `Style.Font.Color.SetColor(...)`. Η λογική παραμένει η ίδια, μόνο με μερικές επιπλέον γραμμές.

---

## Pro Tips για Κώδικα Έτοιμο για Παραγωγή

- **Reuse Styles:** Η δημιουργία νέου `Style` για κάθε στήλη μπορεί να είναι σπατάλη. Αποθηκεύστε επαναχρησιμοποιήσιμα στυλ σε λεξικό με κλειδί το χρώμα ή το βάρος γραμματοσειράς.  
- **Avoid Hard‑Coded Column Counts:** Ανιχνεύστε `dataTable.Columns.Count` και δημιουργήστε δυναμικά τον πίνακα `columnStyles`.  
- **Thread Safety:** Αν δημιουργείτε πολλά workbooks παράλληλα, δημιουργήστε ξεχωριστό `Workbook` ανά νήμα· τα αντικείμενα Aspose.Cells δεν είναι thread‑safe.  
- **Performance:** Για πίνακες μεγαλύτερους από 10 k γραμμές, σκεφτείτε να απενεργοποιήσετε το `AutoFitColumns` (σαρώνει κάθε κελί) και ορίστε το πλάτος των στηλών χειροκίνητα.

---

## Πλήρες Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το παραγόμενο `StyledDataTable.xlsx` και θα δείτε αμέσως τις χρωματισμένες στήλες. Αυτή είναι η συνολική ροή **import datatable excel c#** σε μια φάση.

---

## Συμπέρασμα

Συζητήσαμε πώς να **μορφοποιήσετε στήλες** όταν **εισάγετε datatable to excel** χρησιμοποιώντας C#. Ορίζοντας έναν πίνακα `Style[]` και περνώντας τον στην `ImportDataTable`, μπορείτε να χρωματίσετε την πρώτη στήλη κόκκινη, τη δεύτερη μπλε, και να αφήσετε τις υπόλοιπες όπως είναι — όλα με μία μόνο γραμμή κώδικα.  

Η προσέγγιση κλιμακώνεται: προσθέστε περισσότερα αντικείμενα `Style` για επιπλέον στήλες, προσαρμόστε τις αρχικές γραμμές ή αντικαταστήστε το Aspose.Cells με άλλη βιβλιοθήκη με παρόμοιο API. Τώρα μπορείτε να δημιουργείτε επαγγελματικές αναφορές Excel χωρίς να αγγίζετε το αρχείο χειροκίνητα.

**Επόμενα βήματα** που μπορείτε να εξερευνήσετε:

- Χρήση **conditional formatting** για δυναμική επισήμανση τιμών (σχετίζεται με το “color second column excel”).  
- Εξαγωγή πολλαπλών φύλλων εργασίας από ένα σύνολο `DataTable` (ιδανικό για μηνιαίες dashboards).  
- Συνδυάστε αυτό με **CSV → DataTable** μετατροπή για να χτίσετε μια ολοκληρωμένη αλυσίδα.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}