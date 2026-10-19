---
category: general
date: 2026-07-13
description: Διαμορφώστε τη στήλη ημερομηνίας στο Excel κατά την εξαγωγή ενός DataTable
  από C#. Μάθετε πώς να εξάγετε DataTable σε Excel με C# και να εισάγετε DataTable
  στο Excel με στυλ σε λίγα λεπτά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: el
lastmod: 2026-07-13
og_description: Διαμορφώστε τη στήλη ημερομηνίας στο Excel χωρίς κόπο. Αυτός ο οδηγός
  σας δείχνει πώς να εξάγετε datatable σε Excel με C# και να εισάγετε datatable στο
  Excel με προσαρμοσμένα στυλ.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Μορφοποίηση Στήλης Ημερομηνίας στο Excel – Βήμα‑προς‑βήμα Μάθημα Εξαγωγής
  C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Μορφοποίηση στήλης ημερομηνίας στο Excel – Πλήρης οδηγός C# για εξαγωγή DataTable
url: /el/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Διαμόρφωση Στήλης Ημερομηνίας Excel – Πλήρης Οδηγός C# για Εξαγωγή DataTable

Κάποτε χρειάστηκε να **διαμορφώσετε στήλη ημερομηνίας Excel** όταν εξάγετε δεδομένα από μια βάση, αλλά τα κελιά έδειχναν ακατέργαστες χρονικές σήμανση; Δεν είστε μόνοι. Σε πολλές επιχειρηματικές εφαρμογές η προεπιλεγμένη εξαγωγή ρίχνει μια τιμή `DateTime` όπως `2024‑03‑15 00:00:00` και κανείς δεν θέλει αυτό το ακατάστατο.

Το καλό νέο είναι ότι μπορείτε να ελέγξετε ακριβώς την εμφάνιση κάθε στήλης απευθείας από το C#. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια ολοκληρωμένη λύση που **excel export datatable c#**, εφαρμόζει στυλ ημερομηνίας στην πρώτη στήλη, στυλ νομίσματος στη δεύτερη, και τελικά **import datatable to excel** χωρίς κανένα κόπο μορφοποίησης.

Στο τέλος θα έχετε μια επαναχρησιμοποιήσιμη μέθοδο που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET, είτε χρησιμοποιείτε .NET 6, .NET Framework 4.8, είτε μια νεότερη έκδοση.

---

## Τι Θα Χρειαστείτε

- **Aspose.Cells for .NET** (ή οποιαδήποτε βιβλιοθήκη που προσφέρει `CreateStyle` και `ImportDataTable`). Τα αποσπάσματα κώδικα χρησιμοποιούν Aspose επειδή το API του είναι καθαρό και ευρέως υιοθετημένο.
- Ένα **DataTable** που έχετε ήδη γεμίσει από SQL, CSV ή οποιαδήποτε άλλη πηγή.
- Visual Studio (ή το αγαπημένο σας IDE).  
- .NET runtime 5.0+ (το παράδειγμα στοχεύει .NET 6, αλλά παλαιότερα frameworks λειτουργούν το ίδιο).

Αν δεν έχετε ακόμη Aspose.Cells, κατεβάστε μια δωρεάν δοκιμή από την επίσημη ιστοσελίδα — δεν απαιτείται πιστωτική κάρτα.

---

## Βήμα 1: Ανάκτηση των Πηγών Δεδομένων ως DataTable

Πρώτα απ’ όλα, χρειάζεστε ένα `DataTable`. Σε πραγματικές συνθήκες αυτό συνήθως προέρχεται από `SqlDataAdapter.Fill`, αλλά για λόγους σαφήνειας θα δημιουργήσουμε έναν απλό πίνακα:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Συμβουλή:** Όταν αντλείτε δεδομένα απευθείας από μια stored procedure, βεβαιωθείτε ότι οι τύποι των στηλών ταιριάζουν με τις επιθυμητές μορφές του Excel. Μια στήλη `datetime` θα είναι αργότερα ο στόχος για το στυλ **format date column excel**.

---

## Βήμα 2: Δημιουργία Excel Workbook και Ορισμός Στυλ Στηλών

Τώρα δημιουργούμε ένα νέο workbook. Το κόλπο για **format date column excel** βρίσκεται στη δημιουργία ενός αντικειμένου `Style`, ορίζοντας την ιδιότητα `Number` στο ενσωματωμένο φορμάτ ημερομηνίας του Excel (κώδικας 14), και αναθέτοντας αυτό το στυλ στο αντίστοιχο index στήλης.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Γιατί `Number = 14`; Το Excel αποθηκεύει τις ημερομηνίες ως σειριακούς αριθμούς· το φορμάτ 14 λέει στο πρόγραμμα να εμφανίζει αυτούς τους αριθμούς χρησιμοποιώντας το σύντομο μοτίβο ημερομηνίας της τοπικής ρύθμισης. Αν χρειάζεστε προσαρμοσμένο μοτίβο (π.χ. `dd‑MMM‑yyyy`), μπορείτε να θέσετε `columnStyles[0].Custom = "dd-MMM-yyyy"` αντί αυτού.

---

## Βήμα 3: Εισαγωγή του DataTable στο Worksheet με Στυλ

Με το array στυλ έτοιμο, η κλήση εισαγωγής είναι μια μόνο γραμμή. Αυτό είναι η καρδιά του **excel export datatable c#** και επίσης το σημείο όπου **import datatable to excel** διατηρεί τη μορφοποίηση.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

Η υπερφόρτωση `ImportDataTable` που χρησιμοποιούμε δέχεται το array στυλ, εφαρμόζοντας κάθε στυλ στη σχετική στήλη καθώς γράφονται τα δεδομένα. Δεν απαιτείται βρόχος επεξεργασίας μετά· η στήλη ημερομηνίας είναι ήδη ωραία μορφοποιημένη.

---

## Βήμα 4: Αποθήκευση του Workbook (ή Άμεση Ροή στον Browser)

Ανάλογα με το σενάριο, μπορείτε να αποθηκεύσετε στο δίσκο, σε memory stream, ή να επιστρέψετε το αρχείο ως HTTP response. Εδώ είναι τρία κοινά μοτίβα:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Προσοχή:** Αν χρησιμοποιείτε `FileResult` σε ASP.NET Core, βεβαιωθείτε ότι ορίζετε `Response.Headers["Cache-Control"] = "no-cache"` όταν το αρχείο δημιουργείται “on the fly”. Αυτό αποτρέπει τον browser από το να σερβίρει παλιά έκδοση.

---

## Βήμα 5: Επαλήθευση Αποτελέσματος – Πώς Δείχνει το Φύλλο Excel

Αφού τρέξετε τον κώδικα, ανοίξτε το `ExportedReport.xlsx`. Θα πρέπει να δείτε:

| ΗμερομηνίαΠαραγγελίας (μορφοποιημένη) | ΣυνολικόΠοσό (νόμισμα) | Πελάτης |
|--------------------------------------|------------------------|----------|
| 03/13/2024                           | $1,245.67              | Acme Corp|
| 03/14/2024                           | $980.00                | Beta Ltd |
| 03/15/2024                           | $1,500.25              | Gamma Inc|

Παρατηρήστε πώς το **format date column excel** εμφανίζει μια καθαρή σύντομη ημερομηνία, ενώ η στήλη νομίσματος ευθυγραμμίζεται αυτόματα με τις τοπικές ρυθμίσεις. Δεν χρειάζεται χειροκίνητη μορφοποίηση κελιού‑κατά‑κελί.

![format date column excel example](/images/format-date-column-excel.png)

*Image alt text: format date column excel – ένα στιγμιότυπο του φύλλου Excel με σωστά μορφοποιημένη στήλη ημερομηνίας.*

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν το DataTable μου έχει περισσότερες από τρεις στήλες;

Απλώς επεκτείνετε το array `columnStyles`. Για κάθε στήλη που δεν μορφοποιείτε ρητά, αφήστε την τιμή `null`; το Excel θα εφαρμόσει το προεπιλεγμένο General format.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Πώς να εφαρμόσω προσαρμοσμένο φορμάτ ημερομηνίας (π.χ. “dd‑MMM‑yyyy”);

Αντικαταστήστε τον ενσωματωμένο αριθμό με μια προσαρμοσμένη συμβολοσειρά:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Μπορώ να χρησιμοποιήσω αυτήν την προσέγγιση με EPPlus ή ClosedXML;

Ναι, η ιδέα είναι η ίδια: δημιουργήστε ένα αντικείμενο στυλ, αναθέστε το σε στήλη, και στη συνέχεια φορτώστε το `DataTable`. Το API διαφέρει, αλλά το μοτίβο **excel export datatable c#** παραμένει το ίδιο.

### Τι γίνεται με μεγάλα σύνολα δεδομένων (100k+ γραμμές);

Το `ImportDataTable` είναι βελτιστοποιημένο για μαζικές εγγραφές, αλλά μπορεί να αντιμετωπίσετε περιορισμούς μνήμης. Σε αυτήν την περίπτωση, σκεφτείτε να κάνετε streaming των γραμμών με `Cells.ImportDataTable` σε τμήματα, ή να χρησιμοποιήσετε `Worksheet.Cells["A1"].PutValue` σε βρόχο ενώ επαναχρησιμοποιείτε τα αντικείμενα στυλ.

---

## Πλήρες Παράδειγμα (Όλα τα Βήματα σε Μία Μέθοδο)

Παρακάτω υπάρχει μια αυτόνομη μέθοδος που μπορείτε να αντιγράψετε‑επικολλήσετε σε οποιαδήποτε console εφαρμογή ή controller ASP.NET. Δείχνει τη συνολική ροή—from ανάκτηση δεδομένων μέχρι εξαγωγή Excel με στυλ.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το `StyledExport.xlsx`, και θα δείτε το **format date column excel** εφαρμοσμένο τέλεια.

---

## Ανακεφαλαίωση & Επόμενα Βήματα

Μόλις καλύψαμε πώς να **format date column excel** όταν κάνετε **excel export datatable c#**, και πώς να **import datatable to excel** με στυλ ανά στήλη σε μία κλήση. Τα κύρια σημεία:

1. Δημιουργήστε ένα `Style` για κάθε στήλη που θέλετε να μορφοποιήσετε.  
2. Χρησιμοποιήστε `Number = 14` για ημερομηνίες, `Number = 2` για νόμισμα, ή οποιοδήποτε προσαρμοσμένο φορμάτ χρειάζεστε.  
3. Περνάτε το array στυλ στο `ImportDataTable` — η βιβλιοθήκη κάνει το σκληρό κομμάτι.

Τι θα εξερευνήσετε στη συνέχεια;

- **Conditional formatting** για να επισημαίνετε ληγόμενες ημερομηνίες.  
- **


## Τι Θα Μάθεις Στη Σύντομη Επόμενη Στιγμή;


Τα παρακάτω tutorials καλύπτουν στενά σχετικούς τομείς που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετα χαρακτηριστικά του API και να εξερευνήσετε εναλλακτικές υλοποιήσεις στα δικά σας έργα.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Export Excel Data to DataTable Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}