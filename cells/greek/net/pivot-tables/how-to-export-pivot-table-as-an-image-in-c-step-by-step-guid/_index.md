---
category: general
date: 2026-02-15
description: Πώς να εξάγετε έναν πίνακα Pivot ως εικόνα σε C# γρήγορα. Μάθετε πώς
  να εξάγετε τα δεδομένα του Pivot, να φορτώσετε ένα βιβλίο εργασίας Excel και να
  αποθηκεύσετε έναν πίνακα Pivot ως εικόνα.
draft: false
keywords:
- how to export pivot
- how to extract pivot
- load excel workbook c#
- export pivot table image
- pivot table to picture
language: el
og_description: Πώς να εξάγετε έναν πίνακα Pivot ως εικόνα σε C# εξηγείται σε λίγα
  λεπτά. Ακολουθήστε αυτό το σεμινάριο για να φορτώσετε ένα βιβλίο εργασίας Excel,
  να εξάγετε τον πίνακα Pivot και να αποθηκεύσετε τον πίνακα Pivot ως εικόνα.
og_title: Πώς να εξάγετε έναν Πίνακα Pivot ως εικόνα σε C# – Πλήρης οδηγός
tags:
- C#
- Excel
- Aspose.Cells
- Data Export
title: Πώς να εξάγετε έναν Πίνακα Pivot ως εικόνα σε C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Πίνακα Pivot ως Εικόνα σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε έναν πίνακα pivot ως εικόνα σε C#** χωρίς να χρησιμοποιείτε εργαλεία τρίτων για στιγμιότυπα οθόνης; Δεν είστε μόνοι—οι προγραμματιστές συχνά χρειάζονται μια καθαρή εικόνα ενός διαγράμματος pivot για να την ενσωματώσουν σε PDF, ιστοσελίδες ή αναφορές μέσω email. Τα καλά νέα; Με λίγες γραμμές κώδικα μπορείτε να εξάγετε το pivot απευθείας από ένα αρχείο Excel και να το γράψετε σε PNG.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: φόρτωση του workbook, εντοπισμός του πρώτου pivot και τελικά αποθήκευση του εύρους του pivot ως εικόνα. Στο τέλος θα είστε άνετοι με το **πώς να εξάγετε δεδομένα pivot** προγραμματιστικά, και θα δείτε πώς να **φορτώσετε Excel workbook C#** χρησιμοποιώντας τη δημοφιλή βιβλιοθήκη Aspose.Cells. Χωρίς περιττές πληροφορίες, μόνο μια πρακτική λύση έτοιμη για αντιγραφή‑επικόλληση.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+).  
- **Aspose.Cells for .NET** εγκατεστημένο μέσω NuGet (`Install-Package Aspose.Cells`).  
- Ένα δείγμα αρχείου Excel (`input.xlsx`) που περιέχει τουλάχιστον έναν πίνακα pivot.  
- Ένα IDE της επιλογής σας (Visual Studio, Rider ή VS Code).  

Αυτό είναι όλο—δεν απαιτείται πρόσθετο COM interop ή εγκατάσταση του Office.

---

## Βήμα 1 – Φόρτωση του Excel Workbook *(load excel workbook c#)*

Το πρώτο που χρειαζόμαστε είναι ένα αντικείμενο `Workbook` που αντιπροσωπεύει το αρχείο Excel στο δίσκο. Η Aspose.Cells αφαιρεί το επίπεδο COM, ώστε να μπορείτε να εργάζεστε σε διακομιστή χωρίς εγκατεστημένο Office.

```csharp
using Aspose.Cells;
using System;

// Path to the source workbook
string workbookPath = @"C:\Data\input.xlsx";

// Load the workbook into memory
Workbook workbook = new Workbook(workbookPath);
```

> **Γιατί είναι σημαντικό:** Η φόρτωση του workbook είναι η πύλη για κάθε άλλη λειτουργία. Αν το αρχείο δεν μπορεί να ανοιχθεί, κανένα από τα επόμενα βήματα—όπως η εξαγωγή του pivot—δεν θα εκτελεστεί.

**Συμβουλή:** Τυλίξτε τη φόρτωση σε ένα μπλοκ `try‑catch` για να διαχειρίζεστε κατεστραμμένα αρχεία με χάρη.  

```csharp
try
{
    Workbook workbook = new Workbook(workbookPath);
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to open workbook: {ex.Message}");
    return;
}
```

---

## Βήμα 2 – Εντοπισμός του Πρώτου Πίνακα Pivot *(how to extract pivot)*

Μόλις το workbook είναι στη μνήμη, πρέπει να εντοπίσουμε το pivot που θέλουμε να εξάγουμε. Στις πιο απλές περιπτώσεις, το πρώτο φύλλο περιέχει το pivot, αλλά μπορείτε να προσαρμόσετε το δείκτη όπως χρειάζεται.

```csharp
// Grab the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Ensure the worksheet actually has a pivot table
if (worksheet.PivotTables.Count == 0)
{
    Console.WriteLine("No pivot tables found on the first sheet.");
    return;
}

// Retrieve the first pivot table's range
CellArea pivotRange = worksheet.PivotTables[0].PivotTableRange;
```

> **Τι συμβαίνει εδώ;** Η `PivotTableRange` σας δίνει το ακριβές ορθογώνιο κελιών που καταλαμβάνει το pivot, συμπεριλαμβανομένων των κεφαλίδων και των γραμμών δεδομένων. Αυτή είναι η περιοχή που θα μετατρέψουμε σε εικόνα.

**Edge case:** Αν έχετε πολλά pivots και χρειάζεστε ένα συγκεκριμένο, επαναλάβετε μέσω του `worksheet.PivotTables` και ταιριάξτε με το όνομα:

```csharp
PivotTable targetPivot = null;
foreach (var pt in worksheet.PivotTables)
{
    if (pt.Name == "SalesSummary")
    {
        targetPivot = pt;
        break;
    }
}
if (targetPivot == null) { /* handle missing pivot */ }
CellArea pivotRange = targetPivot.PivotTableRange;
```

---

## Βήμα 3 – Εξαγωγή του Πίνακα Pivot σε Εικόνα *(how to export pivot)*

Τώρα έρχεται το αστέρι της παράστασης: η μετατροπή του `CellArea` σε αρχείο εικόνας. Η Aspose.Cells παρέχει τη βολική μέθοδο `ToImage` που γράφει απευθείας σε PNG, JPEG ή BMP.

```csharp
// Destination path for the exported image
string imagePath = @"C:\Data\Pivot.png";

// Export the pivot range as a PNG image
pivotRange.ToImage(imagePath);
Console.WriteLine($"Pivot exported successfully to {imagePath}");
```

> **Γιατί να χρησιμοποιήσετε PNG;** Το PNG διατηρεί καθαρό κείμενο και γραμμές πλέγματος χωρίς απώλεια συμπίεσης, καθιστώντας το ιδανικό για αναφορές. Αν χρειάζεστε μικρότερο αρχείο, αλλάξτε την επέκταση σε `.jpg` και η βιβλιοθήκη θα αναλάβει τη μετατροπή.

**Συνηθισμένη παγίδα:** Η παράλειψη ορισμού του σωστού DPI μπορεί να κάνει την εικόνα θολή όταν εκτυπώνεται. Μπορείτε να ελέγξετε την ανάλυση ως εξής:

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI for high‑quality output
};

pivotRange.ToImage(imagePath, imgOptions);
```

---

## Βήμα 4 – Επαλήθευση της Εξαγόμενης Εικόνας *(export pivot table image)*

Μετά την ολοκλήρωση της εξαγωγής, είναι καλή πρακτική να επιβεβαιώσετε ότι το αρχείο υπάρχει και φαίνεται όπως αναμένεται. Μια γρήγορη έλεγχος μπορεί να γίνει προγραμματιστικά ή χειροκίνητα.

```csharp
if (File.Exists(imagePath))
{
    Console.WriteLine("Image file verified.");
    // Optionally open the image using the default viewer
    System.Diagnostics.Process.Start(new ProcessStartInfo(imagePath) { UseShellExecute = true });
}
else
{
    Console.WriteLine("Export failed – image not found.");
}
```

Αν ανοίξετε το αρχείο και δείτε την ακριβή διάταξη του pivot, έχετε απαντήσει επιτυχώς στο **πώς να εξάγετε έναν πίνακα pivot ως εικόνα σε C#**.

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω υπάρχει μια αυτόνομη εφαρμογή κονσόλας που ενώνει όλα τα βήματα. Αντιγράψτε, επικολλήστε και τρέξτε—θα λειτουργήσει αμέσως εφόσον το πακέτο NuGet είναι εγκατεστημένο και οι διαδρομές αρχείων είναι έγκυρες.

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
using System.Diagnostics;
using System.IO;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string workbookPath = @"C:\Data\input.xlsx";
            Workbook workbook;
            try
            {
                workbook = new Workbook(workbookPath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Unable to load workbook: {ex.Message}");
                return;
            }

            // 2️⃣ Get the first worksheet and its first pivot table
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found.");
                return;
            }

            PivotTable pivot = sheet.PivotTables[0];
            CellArea range = pivot.PivotTableRange;

            // 3️⃣ Export the pivot range to PNG
            string imagePath = @"C:\Data\Pivot.png";
            try
            {
                // Optional: higher resolution for printing
                ImageOrPrintOptions opts = new ImageOrPrintOptions
                {
                    ImageFormat = ImageFormat.Png,
                    Resolution = 300
                };
                range.ToImage(imagePath, opts);
                Console.WriteLine($"Pivot exported to {imagePath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Export failed: {ex.Message}");
                return;
            }

            // 4️⃣ Verify and open the image
            if (File.Exists(imagePath))
            {
                Console.WriteLine("Verification succeeded – opening image.");
                Process.Start(new ProcessStartInfo(imagePath) { UseShellExecute = true });
            }
            else
            {
                Console.WriteLine("Verification failed – image missing.");
            }
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ένα αρχείο `Pivot.png` στο `C:\Data\` που φαίνεται ακριβώς όπως το pivot που βλέπετε μέσα στο `input.xlsx`. Μπορείτε τώρα να ενσωματώσετε αυτό το PNG σε PDF, διαφάνεια PowerPoint ή σε HTML σελίδα.

---

## Συχνές Ερωτήσεις

| Ερώτηση | Απάντηση |
|----------|--------|
| *Λειτουργεί αυτό με αρχεία .xls;* | Ναι. Η Aspose.Cells υποστηρίζει τόσο `.xlsx` όσο και παλαιότερα `.xls`. Απλώς δείξτε το `Workbook` στο αρχείο `.xls`. |
| *Τι γίνεται αν το pivot βρίσκεται σε κρυφό φύλλο;* | Το API εξακολουθεί να έχει πρόσβαση σε κρυφά φύλλα εργασίας· χρειάζεται μόνο να αναφέρετε τον σωστό δείκτη ή όνομα. |
| *Μπορώ να εξάγω πολλαπλά pivots ταυτόχρονα;* | Κάντε βρόχο μέσω του `worksheet.PivotTables` και καλέστε `ToImage` για κάθε `CellArea`. |
| *Υπάρχει τρόπος να ορίσω προσαρμοσμένο χρώμα φόντου;* | Χρησιμοποιήστε το `ImageOrPrintOptions` → ιδιότητα `BackgroundColor` πριν καλέσετε το `ToImage`. |
| *Χρειάζεται άδεια για το Aspose.Cells;* | Μια δωρεάν δοκιμή λειτουργεί αλλά προσθέτει υδατογράφημα. Για παραγωγική χρήση, μια εμπορική άδεια το αφαιρεί. |

---

## Τι Ακολουθεί; *(export pivot table image & pivot table to picture)*

Τώρα που έχετε κατακτήσει το **πώς να εξάγετε έναν πίνακα pivot ως εικόνα σε C#**, ίσως θέλετε:

- **Να επεξεργαστείτε μαζικά έναν φάκελο workbook** και να δημιουργήσετε PNG για κάθε pivot.  
- **Να συνδυάσετε τις εξαγόμενες εικόνες σε ένα ενιαίο PDF** χρησιμοποιώντας Aspose.PDF ή iTextSharp.  
- **Να ενημερώσετε τα δεδομένα του pivot προγραμματιστικά** πριν την εξαγωγή, ώστε η εικόνα να αντανακλά τους τελευταίους υπολογισμούς.  
- **Να εξερευνήσετε την εξαγωγή διαγραμμάτων** (`Chart.ToImage`) αν το pivot σας περιλαμβάνει συνδεδεμένο διάγραμμα.

Όλες αυτές οι επεκτάσεις βασίζονται στις ίδιες βασικές έννοιες που καλύφθηκαν εδώ, οπότε νιώστε ελεύθεροι να πειραματιστείτε.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για το **πώς να εξάγετε έναν πίνακα pivot ως εικόνα σε C#**: φόρτωση του workbook, εξαγωγή του εύρους του pivot και αποθήκευση του ως αρχείο εικόνας. Το πλήρες, εκτελέσιμο παράδειγμα παραπάνω δείχνει τα ακριβή βήματα, εξηγεί το «γιατί» πίσω από κάθε κλήση και επισημαίνει κοινές παγίδες.

Δοκιμάστε το με τα δικά σας αρχεία Excel, προσαρμόστε την ανάλυση ή κάντε βρόχο πάνω σε πολλαπλά pivots—υπάρχει άφθονος χώρος για προσαρμογές.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}