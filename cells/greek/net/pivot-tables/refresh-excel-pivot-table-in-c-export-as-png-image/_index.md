---
category: general
date: 2026-02-23
description: Ανανεώστε τον πίνακα Pivot του Excel σε C# και εξάγετε τον ως εικόνα
  PNG. Μάθετε πώς να φορτώνετε ένα βιβλίο εργασίας Excel σε C#, να ανανεώνετε τον
  πίνακα Pivot και να αποθηκεύετε το αποτέλεσμα.
draft: false
keywords:
- refresh excel pivot table
- load excel workbook c#
- export pivot as image
- export excel pivot image
language: el
og_description: Ανανεώστε τον πίνακα Pivot του Excel σε C# και εξάγετέ τον ως εικόνα
  PNG. Οδηγός βήμα‑προς‑βήμα με πλήρη κώδικα και πρακτικές συμβουλές.
og_title: Ανανέωση Πίνακα Pivot του Excel σε C# – Εξαγωγή ως εικόνα PNG
tags:
- C#
- Excel
- Aspose.Cells
- Data Automation
title: Ανανέωση Πίνακα Pivot του Excel σε C# – Εξαγωγή ως εικόνα PNG
url: /el/net/pivot-tables/refresh-excel-pivot-table-in-c-export-as-png-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ανανέωση Πίνακα Pivot του Excel σε C# – Εξαγωγή ως PNG Εικόνα

Έχετε ποτέ χρειαστεί να **ανανεώσετε έναν πίνακα pivot του Excel** από μια εφαρμογή C# και στη συνέχεια να τον μετατρέψετε σε εικόνα; Δεν είστε οι μόνοι που το σκέφτεστε. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα πώς να **ανανεώσετε έναν πίνακα pivot του Excel**, **φορτώσετε ένα Excel workbook με C#**, και τελικά **εξάγετε τον pivot ως εικόνα** — όλα σε ένα καθαρό, εκτελέσιμο απόσπασμα.

Στο τέλος θα έχετε ένα αρχείο PNG που μοιάζει ακριβώς με τον pivot που βλέπετε στο Excel, έτοιμο να ενσωματωθεί σε αναφορές, email ή dashboards. Χωρίς χειροκίνητη αντιγραφή‑επικόλληση, χωρίς περίπλοκο COM interop, απλώς απλό .NET κώδικα.

## Προαπαιτούμενα

- .NET 6+ (ή .NET Framework 4.7+)
- Aspose.Cells for .NET (δωρεάν δοκιμή ή έκδοση με άδεια) – μπορείτε να το αποκτήσετε από το NuGet με `Install-Package Aspose.Cells`.
- Ένα υπάρχον `input.xlsx` που περιέχει τουλάχιστον έναν πίνακα pivot.
- Ένας φάκελος όπου έχετε δικαίωμα εγγραφής για την έξοδο της εικόνας.

> **Pro tip:** Εάν χρησιμοποιείτε Visual Studio, ενεργοποιήστε τους **nullable reference types** (`<Nullable>enable</Nullable>`) για να εντοπίζετε νωρίς σφάλματα σχετιζόμενα με null.

---

## Βήμα 1: Φόρτωση Excel Workbook σε C#

Το πρώτο που χρειαζόμαστε είναι ένα αντικείμενο `Workbook` που δείχνει στο αρχείο προέλευσης. Σκεφτείτε το ως το άνοιγμα του αρχείου Excel προγραμματιστικά.

```csharp
using System;
using Aspose.Cells;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // The rest of the steps follow…
```

**Γιατί είναι σημαντικό:** Η φόρτωση του workbook μας δίνει πρόσβαση στα φύλλα εργασίας, τα κελιά και — κυρίως — στους πίνακες pivot που έχετε δημιουργήσει. Αν το αρχείο δεν βρεθεί, το Aspose ρίχνει ένα σαφές `FileNotFoundException`, το οποίο μπορείτε να πιάσετε για μια κομψή εναλλακτική.

---

## Βήμα 2: Διαμόρφωση Επιλογών Εξαγωγής Εικόνας (Export Pivot as Image)

Το Aspose.Cells σας επιτρέπει να ορίσετε πώς θα αποδοθεί ο pivot. Εδώ ζητάμε PNG επειδή είναι lossless και ευρέως υποστηριζόμενο.

```csharp
        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: set resolution for sharper output
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

**Γιατί PNG;** Σε αντίθεση με το JPEG, το PNG διατηρεί τις καθαρές γραμμές πλέγματος και τη σκίαση κειμένου που εξαρτώνται οι πίνακες pivot. Αν χρειάζεστε μικρότερο αρχείο, μπορείτε να μεταβείτε σε `ImageFormat.Jpeg` και να ρυθμίσετε την ποιότητα, αλλά θα χάσετε λίγη σαφήνεια.

---

## Βήμα 3: Ανανέωση του Πίνακα Pivot

Πριν καταγράψουμε το οπτικό, πρέπει να βεβαιωθούμε ότι ο pivot αντανακλά τα πιο πρόσφατα δεδομένα. Αυτό είναι ο πυρήνας του **refresh excel pivot table**.

```csharp
        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();
```

**Τι συμβαίνει στο παρασκήνιο;** Η `Refresh()` επαναϋπολογίζει τον pivot βάσει της περιοχής προέλευσης. Αν έχετε προσθέσει γραμμές στα δεδομένα προέλευσης μετά την αποθήκευση του workbook, αυτή η κλήση τις ενσωματώνει. Η παράλειψη αυτού του βήματος οδηγεί σε παλιά εικόνα που δεν ταιριάζει με τα τρέχοντα δεδομένα.

---

## Βήμα 4: Απόδοση του Πίνακα Pivot σε PNG (Export Excel Pivot Image)

Τώρα που όλα είναι ενημερωμένα, μπορούμε να αποδώσουμε τον pivot απευθείας σε αρχείο εικόνας.

```csharp
        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

**Αποτέλεσμα:** Ανοίξτε το `pivot.png` και θα δείτε ένα pixel‑perfect στιγμιότυπο του ανανεωμένου pivot. Αυτό το αρχείο μπορεί να προσαρτηθεί σε email, να ενσωματωθεί σε ιστοσελίδα ή να τροφοδοτηθεί σε μηχανή αναφορών.

### Αναμενόμενο Αποτέλεσμα

```
Pivot table exported successfully to: YOUR_DIRECTORY\pivot.png
```

Αν περιηγηθείτε στον φάκελο, το PNG θα εμφανίζει τις ίδιες γραμμές, στήλες και φίλτρα που βλέπετε στο Excel.

---

## Διαχείριση Συνηθισμένων Edge Cases

| Κατάσταση | Τι να κάνετε |
|-----------|--------------|
| **Πολλαπλοί πίνακες pivot** | Κάντε βρόχο μέσω `worksheet.PivotTables` και καλέστε `Refresh()` / `RenderToImage()` για κάθε έναν. |
| **Δυναμικά ονόματα φύλλων** | Χρησιμοποιήστε `wb.Worksheets[wb.Worksheets.IndexOf("SheetName")]` ή αναζητήστε με `worksheet.Name`. |
| **Μεγάλα σύνολα δεδομένων** | Αυξήστε το `imgOptions.OnePagePerSheet = false` και ορίστε `imgOptions.PageWidth`/`PageHeight` για να ελέγξετε την σελιδοποίηση. |
| **Λείπει η άδεια Aspose.Cells** | Η δωρεάν δοκιμή προσθέτει υδατογράφημα. Αποκτήστε άδεια και καλέστε `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` πριν φορτώσετε το workbook. |
| **Προβλήματα διαδρομής αρχείου** | Χρησιμοποιήστε `Path.Combine(Environment.CurrentDirectory, "input.xlsx")` για να αποφύγετε σκληρά κωδικοποιημένους διαχωριστές. |

---

## Συμβουλές & Καλές Πρακτικές

- **Κατάλληλη απελευθέρωση** – Τυλίξτε το `Workbook` σε μπλοκ `using` ή καλέστε `wb.Dispose()` όταν τελειώσετε για να ελευθερώσετε τους εγγενείς πόρους.
- **Cache αποδοθέντων εικόνων** – Αν χρειάζεστε την ίδια εικόνα pivot επανειλημμένα, αποθηκεύστε το PNG στο δίσκο και επαναχρησιμοποιήστε το αντί για επανασχεδίαση κάθε φορά.
- **Ασφάλεια νήματος** – Κάθε νήμα πρέπει να εργάζεται με τη δική του παρουσία `Workbook`; τα αντικείμενα Aspose.Cells δεν είναι thread‑safe.
- **Απόδοση** – Η απόδοση μεγάλων pivots μπορεί να είναι απαιτητική σε μνήμη. Ρυθμίστε το `imgOptions.ImageFormat` σε `Bmp` για ταχύτερη αλλά μεγαλύτερη αρχείο, ή μειώστε το DPI για πιο γρήγορη απόδοση.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.xlsx");
        if (!File.Exists(inputPath))
        {
            Console.Error.WriteLine($"File not found: {inputPath}");
            return;
        }

        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        if (worksheet.PivotTables.Count == 0)
        {
            Console.Error.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();

        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = Path.Combine(Environment.CurrentDirectory, "pivot.png");
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");

        // Clean up
        wb.Dispose();
    }
}
```

Εκτελέστε το πρόγραμμα, ανοίξτε το `pivot.png` και θα δείτε τον ανανεωμένο πίνακα pivot ακριβώς όπως εμφανίζεται στο Excel.

---

## Συχνές Ερωτήσεις

**Q: Λειτουργεί αυτό με αρχεία .xlsx που δημιουργήθηκαν από LibreOffice;**  
A: Ναι. Το Aspose.Cells διαβάζει τη μορφή Open XML ανεξάρτητα από την εφαρμογή προέλευσης, έτσι μπορείτε να **load excel workbook c#** από LibreOffice, εξαγωγή Google Sheets ή οποιαδήποτε άλλη πηγή.

**Q: Μπορώ να εξάγω πολλαπλά φύλλα εργασίας ταυτόχρονα;**  
A: Απόλυτα. Κάντε βρόχο μέσω `wb.Worksheets` και εφαρμόστε την ίδια λογική `RenderToImage` για κάθε φύλλο. Απλώς θυμηθείτε να δώσετε σε κάθε έξοδο ένα μοναδικό όνομα αρχείου.

**Q: Τι γίνεται αν ο pivot χρησιμοποιεί εξωτερική πηγή δεδομένων;**  
A: Το Aspose.Cells μπορεί να ανανεώσει εξωτερικές συνδέσεις αν είναι ενσωματωμένες στο αρχείο, αλλά θα πρέπει να παρέχετε το connection string και τα διαπιστευτήρια προγραμματιστικά. Δείτε την τεκμηρίωση του Aspose για `DataSourceOptions`.

---

## Συμπέρασμα

Τώρα έχετε μια ολοκληρωμένη λύση για **refresh excel pivot table** από C# και **export excel pivot image** ως PNG. Ο κώδικας δείχνει πώς να **load excel workbook c#**, να διαμορφώσετε τις ρυθμίσεις εικόνας, να εξασφαλίσετε ότι ο pivot αντανακλά τα πιο πρόσφατα δεδομένα, και τελικά να τον αποδώσετε σε αρχείο.

Στη συνέχεια, μπορείτε να εξερευνήσετε το **export pivot as image** σε άλλες μορφές (PDF, SVG) ή να αυτοματοποιήσετε τη διαδικασία για πολλαπλά workbooks σε batch job. Θέλετε να ενσωματώσετε το PNG σε αναφορά Word; Η ίδια κλάση `ImageOrPrintOptions` λειτουργεί με Aspose.Words.

Νιώστε ελεύθεροι να πειραματιστείτε, να σπάσετε πράγματα, και να θέσετε ερωτήσεις στα σχόλια — καλή προγραμματιστική!

![Στιγμιότυπο πίνακα pivot Excel](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}