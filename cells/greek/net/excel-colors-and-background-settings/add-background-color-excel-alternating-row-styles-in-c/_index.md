---
category: general
date: 2026-04-07
description: Προσθήκη χρώματος φόντου σε σειρές Excel χρησιμοποιώντας C#. Μάθετε πώς
  να εφαρμόζετε εναλλασσόμενα χρώματα σε σειρές, να ορίζετε στυλ στερεού φόντου και
  να εισάγετε datatable στο Excel σε μία ενιαία ροή εργασίας.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: el
og_description: Προσθέστε χρώμα φόντου στις σειρές του Excel με C#. Αυτός ο οδηγός
  δείχνει πώς να εφαρμόσετε εναλλασσόμενα χρώματα στις σειρές, να ορίσετε στερεό φόντο
  και να εισάγετε αποτελεσματικά έναν πίνακα δεδομένων στο Excel.
og_title: Προσθήκη χρώματος φόντου στο Excel – Εναλλασσόμενα στυλ γραμμών σε C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Προσθήκη χρώματος φόντου στο Excel – Εναλλασσόμενα στυλ γραμμών σε C#
url: /el/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη χρώματος φόντου excel – Εναλλασσόμενα Στυλ Γραμμών σε C#

Έχετε ποτέ χρειαστεί να **add background color excel** γραμμές αλλά δεν ήσασταν σίγουροι πώς να το κάνετε χωρίς χίλιες γραμμές πολύπλοκου κώδικα; Δεν είστε μόνοι—οι περισσότεροι προγραμματιστές συναντούν αυτό το εμπόδιο όταν προσπαθούν για πρώτη φορά να κάνουν τα φύλλα εργασίας τους να φαίνονται περισσότερο από μια ακατέργαστη συλλογή δεδομένων.  

Τα καλά νέα; Σε λίγα μόνο λεπτά μπορείτε να **apply alternating row colors**, να ορίσετε ένα **solid background**, και ακόμη να **import datatable to excel** χρησιμοποιώντας ένα καθαρό, επαναχρησιμοποιήσιμο μοτίβο σε C#.  

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία, από την ανάκτηση δεδομένων σε ένα `DataTable` μέχρι το στυλιζάρισμα κάθε γραμμής με ένα μοτίβο ελαφρώς κίτρινο‑λευκό λωρίδας. Δεν απαιτούνται εξωτερικές βιβλιοθήκες πέρα από ένα σταθερό πακέτο διαχείρισης Excel (όπως **ClosedXML** ή **GemBox.Spreadsheet**), και θα δείτε γιατί αυτή η προσέγγιση είναι τόσο αποδοτική όσο και εύκολη στη συντήρηση.

## Τι Θα Μάθετε

- Πώς να ανακτήσετε δεδομένα και να τα τροφοδοτήσετε σε ένα φύλλο εργασίας Excel.
- Πώς να **style excel rows** με εναλλασσόμενα χρώματα φόντου.
- Οι μηχανισμοί πίσω από το **set solid background** χρησιμοποιώντας το αντικείμενο `Style`.
- Πώς να **import datatable to excel** διατηρώντας τα στυλ των γραμμών.
- Συμβουλές για τη διαχείριση ειδικών περιπτώσεων όπως κενά tables ή προσαρμοσμένα σχήματα χρωμάτων.

> **Pro tip:** Αν χρησιμοποιείτε ήδη ένα αντικείμενο workbook (`wb`) από μια βιβλιοθήκη που υποστηρίζει δημιουργία στυλ, μπορείτε να επαναχρησιμοποιήσετε τις ίδιες παρουσίες `Style` σε πολλαπλά φύλλα εργασίας—εξοικονομώντας μνήμη και διατηρώντας τον κώδικά σας τακτικό.

---

## Βήμα 1: Ανάκτηση των Δεδομένων – Προετοιμασία του DataTable

Πριν μπορέσει να γίνει οποιοδήποτε στυλ, χρειαζόμαστε μια πηγή γραμμών. Στις περισσότερες πραγματικές περιπτώσεις αυτό προέρχεται από μια βάση δεδομένων, ένα API ή ένα αρχείο CSV. Για παράδειγμα, θα δημιουργήσουμε απλώς ένα απλό `DataTable` στη μνήμη.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Why this matters:** Η χρήση ενός `DataTable` σας παρέχει ένα πινάκο, container με γνώση σχήματος, το οποίο η βιβλιοθήκη Excel μπορεί να εισάγει άμεσα, εξαλείφοντας την ανάγκη για βρόχους κελιού‑με‑κελί.

---

## Βήμα 2: Δημιουργία Στυλ Γραμμών – **Apply alternating row colors**

Τώρα θα δημιουργήσουμε έναν πίνακα αντικειμένων `Style`—ένα ανά γραμμή—ώστε κάθε γραμμή να μπορεί να λάβει το δικό της φόντο. Το μοτίβο που θα χρησιμοποιήσουμε είναι ένα κλασικό ανοιχτό‑κίτρινο για τις ζυγές γραμμές και λευκό για τις μονές.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explanation:**  
- `wb.CreateStyle()` σας δίνει ένα καθαρό αντικείμενο στυλ που μπορείτε να τροποποιήσετε χωρίς να επηρεάσετε άλλα.  
- Ο τελεστής τριπλού `(i % 2 == 0)` αποφασίζει αν η γραμμή είναι ζυγή (ανοιχτό κίτρινο) ή μονή (λευκό).  
- Η ρύθμιση `Pattern = BackgroundType.Solid` είναι το κρίσιμο βήμα που **set solid background**· χωρίς αυτό το χρώμα θα αγνοηθεί.

---

## Βήμα 3: Λήψη του Στόχου Φύλλου Εργασίας

Οι περισσότερες βιβλιοθήκες εκθέτουν μια συλλογή φύλλων εργασίας. Θα δουλέψουμε με το πρώτο, αλλά μπορείτε να στοχεύσετε οποιοδήποτε δείκτη ή όνομα προτιμάτε.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Αν το workbook είναι ολοκαίνουργιο, η βιβλιοθήκη συνήθως δημιουργεί ένα προεπιλεγμένο φύλλο για εσάς. Διαφορετικά, μπορείτε να προσθέσετε ένα ρητά:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Βήμα 4: Εισαγωγή του DataTable με Στυλ Γραμμών – **Import datatable to excel**

Με τα στυλ έτοιμα, το τελευταίο βήμα είναι να εισάγετε το `DataTable` στο φύλλο εφαρμόζοντας το αντίστοιχο στυλ σε κάθε γραμμή.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**What’s happening under the hood?**  
- `true` λέει στη μέθοδο να γράψει τις επικεφαλίδες των στηλών ως την πρώτη γραμμή.  
- `0, 0` σηματοδοτεί την πάνω‑αριστερή γωνία (A1) ως σημείο εισαγωγής.  
- `rowStyles` ευθυγραμμίζει κάθε `Style` με την αντίστοιχη γραμμή δεδομένων, δίνοντάς μας τα εναλλασσόμενα χρώματα που προετοιμάσαμε νωρίτερα.

---

## Βήμα 5: Αποθήκευση του Workbook

Το τελευταίο κομμάτι του παζλ είναι η αποθήκευση του workbook σε αρχείο ώστε να το ανοίξετε στο Excel και να δείτε το αποτέλεσμα.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Ανοίξτε το αρχείο και θα πρέπει να δείτε ένα καλοσχεδιασμένο φύλλο:

- Γραμμή επικεφαλίδας με έντονη γραφή (προεπιλεγμένο στυλ βιβλιοθήκης).  
- Γραμμή 1, 3, 5… με καθαρό λευκό φόντο.  
- Γραμμή 2, 4, 6… με ήπιο ανοιχτό‑κίτρινο γέμισμα, κάνοντας την ανάγνωση εύκολη.

### Αναμενόμενη Στιγμιότυπο Εξόδου

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Rows 2, 4, 6, … appear with a light‑yellow background—exactly the **apply alternating row colors** effect we aimed for.

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Το κείμενο alt περιλαμβάνει τη βασική λέξη-κλειδί για SEO.)*

---

## Διαχείριση Ειδικών Περιπτώσεων & Παραλλαγών

### Κενό DataTable

Αν το `dataTable.Rows.Count` είναι μηδέν, ο πίνακας `rowStyles` θα είναι κενός και το `ImportDataTable` θα γράψει ακόμη τη γραμμή επικεφαλίδας (αν το `includeHeaders` είναι `true`). Δεν θα προκληθεί εξαίρεση, αλλά ίσως θέλετε να προστατέψετε την παραγωγή ενός σχεδόν κεντρικού αρχείου:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Προσαρμοσμένα Σχήματα Χρωμάτων

Θέλετε λωρίδα μπλε/γκρι αντί για κίτρινο/λευκό; Απλώς αντικαταστήστε τις τιμές `Color`:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Μπορείτε ελεύθερα να αντλήσετε τα χρώματα από ένα αρχείο ρυθμίσεων ώστε μη‑προγραμματιστές να μπορούν να τροποποιήσουν την παλέτα χωρίς να αγγίζουν τον κώδικα.

### Επαναχρησιμοποίηση Στυλ σε Πολλαπλά Φύλλα Εργασίας

Αν εξάγετε πολλούς πίνακες στο ίδιο workbook, μπορείτε να δημιουργήσετε τον πίνακα στυλ μία φορά και να τον επαναχρησιμοποιήσετε:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Απλώς προσέξτε ότι και οι δύο πίνακες έχουν τον ίδιο αριθμό γραμμών, ή δημιουργήστε έναν νέο πίνακα ανά φύλλο.

---

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε μια εφαρμογή κονσόλας.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το `Report.xlsx`, και θα δείτε το εναλλασσόμενο φόντο ακριβώς όπως περιγράφεται.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}