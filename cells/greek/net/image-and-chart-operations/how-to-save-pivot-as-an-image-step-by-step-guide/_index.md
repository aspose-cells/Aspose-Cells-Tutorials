---
category: general
date: 2026-03-01
description: Πώς να αποθηκεύσετε το pivot γρήγορα και αξιόπιστα. Μάθετε πώς να εξάγετε
  το pivot, να εξάγετε την εικόνα του pivot και να μετατρέψετε την περιοχή σε εικόνα
  με λίγες μόνο γραμμές κώδικα C#.
draft: false
keywords:
- how to save pivot
- how to export pivot
- export pivot image
- convert range to image
language: el
og_description: Πώς να αποθηκεύσετε το pivot σε C# σε δευτερόλεπτα. Ακολουθήστε αυτόν
  τον οδηγό για εξαγωγή του pivot, εξαγωγή εικόνας pivot και μετατροπή περιοχής σε
  εικόνα με καθαρό κώδικα.
og_title: Πώς να αποθηκεύσετε το Pivot ως εικόνα – Γρήγορος οδηγός C#
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Πώς να αποθηκεύσετε το Pivot ως εικόνα – Οδηγός βήμα‑βήμα
url: /el/net/image-and-chart-operations/how-to-save-pivot-as-an-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Αποθηκεύσετε ένα Pivot ως Εικόνα – Πλήρες Tutorial C#

Έχετε αναρωτηθεί ποτέ **πώς να αποθηκεύσετε pivot** απευθείας από ένα φύλλο Excel χωρίς να ανοίξετε το αρχείο χειροκίνητα; Δεν είστε μόνοι. Σε πολλές αλυσίδες αναφοράς ο πίνακας pivot είναι το τελικό οπτικό, και το επόμενο βήμα — η ενσωμάτωσή του σε PDF, η αποστολή του μέσω email ή η τοποθέτησή του σε έναν πίνακα ελέγχου — απαιτεί μια στατική εικόνα. Τα καλά νέα; Με λίγες κλήσεις API μπορείτε **πώς να αποθηκεύσετε pivot** χωρίς καμία αλληλεπίδραση UI.

Σε αυτό το tutorial θα περάσουμε από τον ακριβή κώδικα που χρειάζεστε για **πώς να εξάγετε pivot**, να μετατρέψετε αυτήν την εξαγωγή σε **εξαγωγή εικόνας pivot**, και ακόμη **μετατροπή περιοχής σε εικόνα** για οποιαδήποτε προσαρμοσμένη περιοχή θέλετε. Στο τέλος θα έχετε μια επαναχρησιμοποιήσιμη μέθοδο που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

> **Σύντομη σημείωση:** Τα παραδείγματα χρησιμοποιούν τη δημοφιλή βιβλιοθήκη Aspose.Cells for .NET, αλλά οι έννοιες μεταφράζονται σε οποιαδήποτε βιβλιοθήκη που εκθέτει `PivotTable`, `Range` και λειτουργία εξαγωγής εικόνας.

## Προαπαιτούμενα – Τι Χρειάζεστε Πριν Ξεκινήσετε

- **.NET 6+** (ή .NET Framework 4.7.2+) εγκατεστημένο στον υπολογιστή σας.  
- **Aspose.Cells for .NET** (δωρεάν δοκιμή ή έκδοση με άδεια). Μπορείτε να το προσθέσετε μέσω NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```
- Βασική κατανόηση των εννοιών C# και Excel. Δεν απαιτούνται βαθιές εσωτερικές γνώσεις.  
- Ένα υπάρχον αρχείο Excel (`sample.xlsx`) που περιέχει τουλάχιστον έναν πίνακα pivot.

Αν κάτι από αυτά σας φαίνεται άγνωστο, κάντε παύση και εγκαταστήστε το πακέτο πρώτα — δεν έχει νόημα να προχωρήσετε πιο βαθιά μέχρι να είναι έτοιμη η βιβλιοθήκη.

## Πώς να Αποθηκεύσετε Pivot ως Εικόνα – Η Κεντρική Μέθοδος

Παρακάτω υπάρχει ένα **πλήρες, εκτελέσιμο** απόσπασμα που δείχνει τη συνολική ροή. Περιλαμβάνει εισαγωγές, διαχείριση σφαλμάτων και σχόλια ώστε να μπορείτε να το αντιγράψετε‑επικολλήσετε απευθείας σε μια εφαρμογή κονσόλας.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // Needed for Image handling
using System.Drawing;        // System.Drawing.Image

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the workbook that holds the pivot table
            string workbookPath = @"C:\Temp\sample.xlsx";

            // Destination folder for the exported image
            string outputFolder = @"C:\Temp\Images";

            try
            {
                // Ensure output directory exists
                System.IO.Directory.CreateDirectory(outputFolder);

                // Call the helper that does the actual work
                SavePivotAsImage(workbookPath, outputFolder, "pivot.png");
                Console.WriteLine("Pivot saved successfully!");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }

        /// <summary>
        /// Saves the first pivot table in the given workbook as an image file.
        /// This method shows exactly **how to export pivot** and **convert range to image**.
        /// </summary>
        /// <param name="workbookPath">Full path to the source .xlsx file.</param>
        /// <param name="outputFolder">Folder where the image will be written.</param>
        /// <param name="fileName">Desired image file name (e.g., pivot.png).</param>
        public static void SavePivotAsImage(string workbookPath, string outputFolder, string fileName)
        {
            // Load the workbook
            Workbook wb = new Workbook(workbookPath);

            // --------------------------------------------------------------
            // Step 1: Get the first pivot table from the first worksheet
            // --------------------------------------------------------------
            Worksheet ws = wb.Worksheets[0];
            if (ws.PivotTables.Count == 0)
                throw new InvalidOperationException("No pivot tables found in the worksheet.");

            // This is the object we will eventually export.
            PivotTable pivot = ws.PivotTables[0];

            // --------------------------------------------------------------
            // Step 2: Create a range that covers the entire pivot table
            // --------------------------------------------------------------
            // The CreateRange method returns a Range object that precisely
            // matches the pivot's visual bounds.
            Range pivotRange = pivot.CreateRange();

            // --------------------------------------------------------------
            // Step 3: Convert the range to an image (the **export pivot image** step)
            // --------------------------------------------------------------
            // ToImage returns a System.Drawing.Image instance.
            Image pivotImg = pivotRange.ToImage();

            // --------------------------------------------------------------
            // Step 4: Save the image to a file
            // --------------------------------------------------------------
            string fullPath = System.IO.Path.Combine(outputFolder, fileName);
            pivotImg.Save(fullPath, System.Drawing.Imaging.ImageFormat.Png);
        }
    }
}
```

### Γιατί Λειτουργεί Αυτό

- **Πρόσβαση στο Pivot:** `ws.PivotTables[0]` παίρνει τον πρώτο πίνακα pivot, ο οποίος είναι συχνά αυτός που θέλετε να εξάγετε. Αν έχετε πολλαπλά pivots, απλώς αλλάξτε το δείκτη ή κάντε επανάληψη στη συλλογή.  
- **Δημιουργία της Περιοχής:** `pivot.CreateRange()` σας δίνει ένα αντικείμενο `Range` που ταιριάζει ακριβώς με τα κελιά που εμφανίζονται στην οθόνη. Αυτό είναι το κρίσιμο βήμα που σας επιτρέπει να **μετατρέψετε περιοχή σε εικόνα** χωρίς να υπολογίζετε χειροκίνητα τις διευθύνσεις.  
- **Μετατροπή της Περιοχής σε Εικόνα:** `pivotRange.ToImage()` εσωτερικά rasterizes τα κελιά, διατηρώντας τη μορφοποίηση, τα χρώματα και τα περιγράμματα — ακριβώς ό,τι βλέπετε στο Excel.  
- **Αποθήκευση του PNG:** Η τελική κλήση `Save` γράφει ένα φορητό αρχείο PNG, κάνοντας το **export pivot image** έτοιμο για οποιαδήποτε επόμενη διαδικασία (PDF, email, web).

## Πώς να Εξάγετε Pivot – Παραλλαγές που Μπορεί να Χρειαστείτε

### Εξαγωγή Πολλαπλών Pivots από το Ίδιο Φύλλο

Αν το βιβλίο εργασίας σας περιέχει αρκετά pivots, μπορείτε να τα επαναλάβετε:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Range r = pt.CreateRange();
    Image img = r.ToImage();
    string name = $"pivot_{pt.Index}.png";
    img.Save(System.IO.Path.Combine(outputFolder, name), ImageFormat.Png);
}
```

### Εξαγωγή σε Άλλες Μορφές (JPEG, BMP, GIF)

Η μέθοδος `Image.Save` δέχεται οποιοδήποτε `ImageFormat`. Απλώς αντικαταστήστε το `ImageFormat.Png` με `ImageFormat.Jpeg` ή `ImageFormat.Bmp`:

```csharp
pivotImg.Save(fullPath, System.Drawing.Imaging.ImageFormat.Jpeg);
```

### Προσαρμογή Ανάλυσης Εικόνας

Μερικές φορές χρειάζεστε ένα screenshot υψηλότερης ανάλυσης για εκτύπωση. Χρησιμοποιήστε την υπερφόρτωση που δέχεται `ImageOrPrintOptions`:

```csharp
ImageOrPrintOptions opts = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300   // DPI
};
Image highRes = pivotRange.ToImage(opts);
highRes.Save(fullPath, ImageFormat.Png);
```

## Μετατροπή Περιοχής σε Εικόνα – Πέρα από τα Pivots

Η μέθοδος `ToImage` δεν περιορίζεται στα pivots. Θέλετε να καταγράψετε ένα γράφημα, έναν πίνακα δεδομένων ή ένα προσαρμοσμένο μπλοκ κελιών; Απλώς περάστε οποιοδήποτε `Range`:

```csharp
// Capture cells B2:E20 as an image
Range customRange = ws.Cells.CreateRange("B2", "E20");
Image rangeImg = customRange.ToImage();
rangeImg.Save(@"C:\Temp\custom_range.png", ImageFormat.Png);
```

Αυτή είναι η ουσία του **convert range to image** — το ίδιο API που χρησιμοποιήσατε για το pivot λειτουργεί για οποιοδήποτε ορθογώνιο μπλοκ.

## Συνηθισμένα Πιθανά Σφάλματα & Επαγγελματικές Συμβουλές

- **Ανανέωση Pivot:** Εάν τα δεδομένα πηγής σας αλλάξουν, καλέστε `pivot.RefreshData()` πριν δημιουργήσετε την περιοχή. Η παράλειψη αυτού του βήματος μπορεί να σας δώσει μια παλιά εικόνα.  
- **Κρυφές Γραμμές/Στήλες:** Από προεπιλογή, οι κρυφές γραμμές/στήλες αγνοούνται. Εάν χρειάζεστε να είναι ορατές, ορίστε `pivot.ShowHiddenData = true` πριν το `CreateRange()`.  
- **Διαχείριση Μνήμης:** Το `Image` υλοποιεί το `IDisposable`. Σε κώδικα παραγωγής τυλίξτε την εικόνα σε ένα μπλοκ `using` ή καλέστε `Dispose()` μετά την αποθήκευση για να αποφύγετε διαρροές μνήμης.  
- **Ασφάλεια Νήματος:** Τα αντικείμενα Aspose.Cells δεν είναι thread‑safe. Εάν εξάγετε pivots από πολλαπλά νήματα, δημιουργήστε ένα ξεχωριστό αντικείμενο `Workbook` ανά νήμα.

## Πλήρες Παράδειγμα Εργασίας – Λύση σε Ένα Αρχείο

Για όσους αγαπούν το copy‑paste, εδώ είναι ολόκληρο το πρόγραμμα συμπυκνωμένο σε ένα μόνο αρχείο. Τοποθετήστε το σε ένα νέο έργο κονσόλας, ενημερώστε τις διαδρομές και τρέξτε το.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            string src = @"C:\Temp\sample.xlsx";
            string outDir = @"C:\Temp\Images";

            Directory.CreateDirectory(outDir);
            SaveFirstPivotAsPng(src, outDir, "pivot.png");
        }

        static void SaveFirstPivotAsPng(string workbookPath, string folder, string fileName)
        {
            Workbook wb = new Workbook(workbookPath);
            Worksheet ws = wb.Worksheets[0];

            if (ws.PivotTables.Count == 0)
                throw new Exception("Worksheet contains no pivots.");

            PivotTable pt = ws.PivotTables[0];
            Range r = pt.CreateRange();

            using (Image img = r.ToImage())
            {
                string full = Path.Combine(folder, fileName);
                img.Save(full, ImageFormat.Png);
            }
        }
    }
}
```

Η εκτέλεση αυτού εκτυπώνει “Pivot saved successfully!” και αφήνει ένα `pivot.png` ακριβώς εκεί που το υποδείξατε.

## Συμπέρασμα

Καλύψαμε **πώς να αποθηκεύσετε pivot** σε C# από την αρχή μέχρι το τέλος, σας δείξαμε **πώς να εξάγετε pivot** για πολλαπλά σενάρια, παρουσιάσαμε μια **export pivot image** με διαφορετικές μορφές, και εξηγήσαμε τη βασική μηχανική του **convert range to image**. Με αυτά τα αποσπάσματα μπορείτε να αυτοματοποιήσετε τη δημιουργία αναφορών, να ενσωματώσετε εικόνες σε PDF, ή απλώς να αρχειοθετήσετε τα dashboards αναλύσεων χωρίς ποτέ να ανοίξετε το Excel χειροκίνητα.

Επόμενα βήματα; Δοκιμάστε να ενσωματώσετε το παραγόμενο PNG σε PDF χρησιμοποιώντας Aspose.PDF, ή να το στείλετε σε Azure Blob για χρήση στο web. Μπορείτε επίσης να εξερευνήσετε την εξαγωγή γραφημάτων με τον ίδιο τρόπο — απλώς αντικαταστήστε το `PivotTable` με ένα αντικείμενο `Chart` και καλέστε `ToImage()`.

Έχετε ερωτήσεις σχετικά με ειδικές περιπτώσεις, άδειες ή απόδοση; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

![πώς να αποθηκεύσετε pivot](/images/pivot-save-example.png "πώς να αποθηκεύσετε pivot")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}