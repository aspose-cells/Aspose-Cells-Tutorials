---
category: general
date: 2026-02-15
description: Δημιουργήστε βιβλίο εργασίας C# και εξάγετε ένα DataTable στο Excel με
  μορφοποίηση γραμμών, ορίστε το φόντο της γραμμής και αυτοματοποιήστε εργασίες Excel
  σε λίγα λεπτά.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: el
og_description: Δημιουργήστε γρήγορα ένα βιβλίο εργασίας C#, εφαρμόστε στυλ γραμμών
  και αυτοματοποιήστε την εξαγωγή σε Excel με πλήρη παραδείγματα κώδικα και συμβουλές
  βέλτιστων πρακτικών.
og_title: Δημιουργία βιβλίου εργασίας C# – Εξαγωγή DataTable σε Excel με μορφοποίηση
tags:
- C#
- Excel
- DataExport
title: Δημιουργία βιβλίου εργασίας C# – Εξαγωγή DataTable σε Excel με μορφοποίηση
url: /el/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

code block content or shortcodes.

Now produce final content with same ordering.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Workbook C# – Εξαγωγή DataTable σε Excel με Μορφοποίηση

Έχετε ποτέ χρειαστεί να **create workbook C#** και να αποβάλετε ένα `DataTable` σε Excel με προσαρμοσμένο στυλ; Δεν είστε μόνοι. Σε πολλές επιχειρηματικές εφαρμογές η απαίτηση είναι να παραχθεί ένα καλά μορφοποιημένο φύλλο εργασίας που ένας μη‑τεχνικός χρήστης μπορεί να ανοίξει και να καταλάβει αμέσως.  

Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη προς εκτέλεση λύση που σας δείχνει **how to create workbook C#**, εφαρμόζει **excel export formatting**, ορίζει ένα **row background**, και αξιοποιεί **excel automation c#** για να παράγει ένα επαγγελματικό αρχείο. Χωρίς ασαφείς συντομεύσεις “δείτε την τεκμηρίωση” — μόνο ο πλήρης κώδικας, εξηγήσεις για το γιατί κάθε γραμμή είναι σημαντική, και συμβουλές που θα χρησιμοποιήσετε πραγματικά αύριο.

---

## Προαπαιτούμενα

- .NET 6 (ή .NET Framework 4.6+).  
- Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με C#.  
- Το πακέτο NuGet **Aspose.Cells for .NET** (ή οποιαδήποτε βιβλιοθήκη που εκθέτει `Workbook`, `Worksheet`, `Style`).  
- Βασική εξοικείωση με `DataTable`.  

Αν δεν έχετε ακόμη το Aspose.Cells, εκτελέστε:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Η δωρεάν δοκιμή λειτουργεί για τις περισσότερες περιπτώσεις ανάπτυξης· απλώς θυμηθείτε να αντικαταστήσετε το κλειδί άδειας πριν τη διανομή.

---

![Παράδειγμα δημιουργίας workbook C# που δείχνει μορφοποιημένες σειρές σε Excel]( "Παράδειγμα δημιουργίας workbook C# με χρώματα φόντου γραμμών")

---

## Βήμα 1: Αρχικοποίηση του Workbook και του Worksheet (Create Workbook C#)

Το πρώτο που πρέπει να κάνετε είναι να δημιουργήσετε ένα αντικείμενο `Workbook`. Σκεφτείτε το ως το άνοιγμα ενός ολοκαίνουργιου αρχείου Excel στη μνήμη.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Γιατί;**  
`Workbook` περιέχει ολόκληρο το έγγραφο Excel, ενώ `Worksheet` αντιπροσωπεύει μια μόνο καρτέλα. Ξεκινώντας με ένα καθαρό workbook εξασφαλίζετε ότι ελέγχετε κάθε πτυχή της εξόδου — χωρίς κρυφά προεπιλεγμένα στυλ να εμφανίζονται.

---

## Βήμα 2: Δημιουργία Δείγματος DataTable (Export DataTable Excel)

Σε ένα πραγματικό έργο θα αντλούσατε δεδομένα από μια βάση, αλλά για παράδειγμα θα δημιουργήσουμε ένα μικρό `DataTable` επί τόπου.

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Γιατί είναι σημαντικό:**  
Η εξαγωγή ενός `DataTable` είναι ο πιο συνηθισμένος τρόπος μεταφοράς πινάκων δεδομένων από μια εφαρμογή σε Excel. Η παραπάνω μέθοδος είναι πλήρως αυτόνομη, ώστε να μπορείτε να την αντιγράψετε‑επικολλήσετε σε οποιοδήποτε έργο και θα λειτουργήσει.

---

## Βήμα 3: Δημιουργία Στυλ ανά Σειρά (Excel Export Formatting)

Για να δώσουμε σε κάθε σειρά το δικό της χρώμα φόντου, δημιουργούμε ένα αντικείμενο `Style` για κάθε σειρά του `DataTable`. Εδώ η **excel export formatting** λάμπει.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Γιατί στυλ ανά σειρά;**  
Αν χρειάζεται να επισημάνετε συγκεκριμένες εγγραφές (π.χ., ληξιπρόθεσμοι λογαριασμοί) μπορείτε να αντικαταστήσετε τον απλό κύκλο χρωμάτων με λογική υπό όρους — απλώς ορίστε το `style.ForegroundColor` βάσει των δεδομένων της σειράς.

---

## Βήμα 4: Εισαγωγή του DataTable με Στυλ Σειρών (Set Row Background)

Τώρα φέρνουμε όλα μαζί: τα δεδομένα, το workbook και τα στυλ.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**Τι θα δείτε:**  
Ανοίγοντας το `EmployeesReport.xlsx` θα δείτε μια γραμμή κεφαλίδας με προεπιλεγμένο στυλ, ακολουθούμενη από τέσσερις γραμμές δεδομένων, καθεμία βαμμένη με ένα ανοιχτόχρωμο φόντο. Το αποτέλεσμα μοιάζει με χειροποίητη αναφορά, όχι με μια βαρετή εξαγωγή.

---

## Βήμα 5: Προχωρημένες Συμβουλές Excel Automation C# (Excel Automation C#)

| Συμβουλή | Απόσπασμα Κώδικα | Πότε να Χρησιμοποιηθεί |
|-----|--------------|-------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | Μετά την εισαγωγή δεδομένων για να αποφευχθεί η περικοπή κειμένου. |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | Όταν ο πίνακας μπορεί να κυλήσει πέρα από την οθόνη. |
| **Conditional Formatting** | <details><summary>Show</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Επισημαίνει μισθούς πάνω από ένα όριο. |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Όταν χρειάζεστε αναφορές μόνο για ανάγνωση. |

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**Τι γίνεται αν το DataTable έχει χιλιάδες γραμμές;**  
Το Aspose.Cells μεταδίδει τα δεδομένα αποδοτικά, αλλά ίσως θέλετε να απενεργοποιήσετε τη δημιουργία στυλ για κάθε σειρά ώστε να εξοικονομήσετε μνήμη. Αντ' αυτού, εφαρμόστε ένα ενιαίο στυλ σε μια περιοχή:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Μπορώ να εξάγω σε .csv αντί για .xlsx;**  
Βεβαίως — απλώς αλλάξτε τη μορφή αποθήκευσης:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

Το στυλ θα χαθεί (CSV δεν υποστηρίζει στυλ), αλλά η εξαγωγή δεδομένων παραμένει η ίδια.

**Λειτουργεί αυτό σε .NET Core;**  
Ναι. Το Aspose.Cells υποστηρίζει .NET Standard 2.0 και νεότερες εκδόσεις, έτσι ο ίδιος κώδικας εκτελείται σε .NET 6, .NET 7 ή .NET Framework.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}