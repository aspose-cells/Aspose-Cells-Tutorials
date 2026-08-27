---
category: general
date: 2026-02-14
description: πώς να εξάγετε έναν πίνακα Pivot από ένα βιβλίο εργασίας Excel σε PNG
  χρησιμοποιώντας το Aspose.Cells. Μάθετε πώς να φορτώνετε ένα βιβλίο εργασίας Excel,
  να αποδίδετε τον πίνακα Pivot σε εικόνα και να αποθηκεύετε την εικόνα του Pivot
  χωρίς κόπο.
draft: false
keywords:
- how to export pivot
- export excel pivot
- load excel workbook
- pivot table to png
- save pivot image
language: el
og_description: πώς να εξάγετε ένα pivot από το Excel σε PNG σε C#. Αυτός ο οδηγός
  σας δείχνει πώς να φορτώσετε ένα βιβλίο εργασίας Excel, να αποδώσετε έναν πίνακα
  pivot σε PNG και να αποθηκεύσετε την εικόνα του pivot.
og_title: πώς να εξάγετε το pivot σε PNG σε C# – Πλήρης οδηγός
tags:
- Aspose.Cells
- C#
- Excel automation
title: πώς να εξάγετε το pivot σε png στο C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/rendering-and-export/how-to-export-pivot-to-png-in-c-step-by-step-guide/
---

εξαγωγής pivot". The title attribute also same; we can translate. But the instruction says preserve URLs and file paths, but alt text is not a URL. So we can translate alt text and title.

But maybe better to translate alt text and title.

Proceed.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να εξάγετε pivot σε PNG σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε pivot** από ένα φύλλο Excel ως καθαρό αρχείο PNG; Δεν είστε μόνοι—οι προγραμματιστές συχνά χρειάζονται μια γρήγορη οπτική αναπαράσταση ενός πίνακα pivot για αναφορές, dashboards ή συνημμένα email. Τα καλά νέα; Με το Aspose.Cells μπορείτε να φορτώσετε το βιβλίο εργασίας Excel, να πάρετε τον πρώτο πίνακα pivot, να τον μετατρέψετε σε εικόνα και **να αποθηκεύσετε την εικόνα του pivot** με λίγες μόνο γραμμές κώδικα C#.

Σε αυτόν τον οδηγό θα περάσουμε από όλα όσα χρειάζεστε: από τα βασικά του **load excel workbook**, μέχρι τη μετατροπή ενός **pivot table to png**, και τέλος την αποθήκευση του αρχείου στο δίσκο. Στο τέλος θα έχετε ένα αυτόνομο, εκτελέσιμο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

---

## Τι Θα Χρειαστείτε

- **.NET 6 ή νεότερο** (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+)
- **Aspose.Cells for .NET** πακέτο NuGet (έκδοση 23.12 τη στιγμή της συγγραφής)
- Ένα αρχείο Excel (`input.xlsx`) που περιέχει τουλάχιστον έναν πίνακα pivot
- Περιβάλλον Visual Studio ή VS Code που γνωρίζετε καλά

Καμία επιπλέον βιβλιοθήκη, χωρίς COM interop και χωρίς εγκατάσταση του Excel—το Aspose.Cells διαχειρίζεται τα πάντα στη μνήμη.

---

## Βήμα 1 – Φόρτωση του Excel Workbook

Το πρώτο βήμα είναι να φέρετε το βιβλίο εργασίας στη μνήμη. Εδώ η λέξη-κλειδί **load excel workbook** δείχνει την αξία της.

```csharp
using System.Drawing;
using Aspose.Cells;

class PivotExport
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        // Adjust the path to where your input.xlsx lives
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Grab the first worksheet (you can also select by name)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Γιατί είναι σημαντικό:**  
> Η φόρτωση του βιβλίου εργασίας μία φορά διατηρεί τη λειτουργία γρήγορη και αποτρέπει το κλείδωμα του αρχικού αρχείου. Το Aspose.Cells διαβάζει το αρχείο σε ένα διαχειριζόμενο stream, ώστε να μπορείτε ακόμη να φορτώσετε από byte array ή από τοδική τοποθεσία δικτύου αργότερα.

---

## Βήμα 2 – Απόδοση του Pivot Table σε Εικόνα

Τώρα που το βιβλίο εργασίας είναι στη μνήμη, μπορούμε να προσπελάσουμε τους πίνακες pivot. Το API παρέχει τη βολική μέθοδο `ToImage()` που επιστρέφει ένα `System.Drawing.Image`.

```csharp
        // Step 2: Find the first pivot table on the worksheet
        if (worksheet.PivotTables.Count == 0)
        {
            System.Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        // Export the first pivot table as an image
        Image pivotImage = worksheet.PivotTables[0].ToImage();

        // Optional: tweak image quality or size here
        // pivotImage.SetResolution(300, 300);
```

> **Συμβουλή επαγγελματία:** Αν το βιβλίο εργασίας σας περιέχει πολλαπλούς πίνακες pivot, απλώς κάντε βρόχο πάνω από `worksheet.PivotTables` και εξάγετε καθέναν. Η κλήση `ToImage()` σέβεται την τρέχουσα προβολή (φίλτρα, slicers κ.λπ.), ώστε να λαμβάνετε ακριβώς ό,τι βλέπει ο χρήστης.

---

## Βήμα 3 – Αποθήκευση του Δημιουργημένου Αρχείου PNG

Τέλος, αποθηκεύουμε το bitmap στο δίσκο. Η υπερφόρτωση `Save` επιλέγει αυτόματα τη μορφή βάσει της επέκτασης του αρχείου.

```csharp
        // Step 3: Save the image as PNG
        var outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivotImage.Save(outputPath, System.Drawing.Imaging.ImageFormat.Png);

        System.Console.WriteLine($"Pivot table exported successfully to {outputPath}");
    }
}
```

Η εκτέλεση του προγράμματος παράγει ένα `pivot.png` που μοιάζει ακριβώς με τον πίνακα pivot μέσα στο Excel. Ανοίξτε το με οποιονδήποτε προβολέα εικόνων και θα δείτε γραμμές, στήλες και σύνολα αποδομένα pixel‑perfect.

---

## Διαχείριση Συνηθισμένων Περιπτώσεων

### Πολλαπλά Φύλλα ή Πίνακες Pivot

Αν το βιβλίο εργασίας αποθηκεύει το pivot σε διαφορετικό φύλλο, αλλάξτε το index του φύλλου ή χρησιμοποιήστε το όνομα του φύλλου:

```csharp
Worksheet ws = workbook.Worksheets["SalesData"];
```

Στη συνέχεια κάντε βρόχο:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Image img = pt.ToImage();
    img.Save($"pivot_{pt.Name}.png", ImageFormat.Png);
}
```

### Μεγάλοι Πίνακες Pivot

Για πολύ μεγάλους πίνακες pivot το προεπιλεγμένο μέγεθος εικόνας μπορεί να είναι τεράστιο. Μπορείτε να ελέγξετε το μέγεθος απόδοσης ρυθμίζοντας το zoom factor του φύλλου πριν καλέσετε `ToImage()`:

```csharp
worksheet.PageSetup.Zoom = 75; // renders at 75 % of original size
```

### Διαχείριση Μνήμης

`System.Drawing.Image` υλοποιεί το `IDisposable`. Σε κώδικα παραγωγής τυλίξτε την εικόνα σε μπλοκ `using` ώστε να απελευθερώνονται άμεσα οι εγγενείς πόροι:

```csharp
using (Image pivotImage = worksheet.PivotTables[0].ToImage())
{
    pivotImage.Save(outputPath, ImageFormat.Png);
}
```

---

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το ολοκληρωμένο, έτοιμο‑για‑εκτέλεση πρόγραμμα. Επικολλήστε το σε ένα νέο console project, προσαρμόστε τις διαδρομές αρχείων και πατήστε **F5**.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook (load excel workbook)
            // -----------------------------------------------------------------
            string inputFile = @"YOUR_DIRECTORY\input.xlsx";
            Workbook wb = new Workbook(inputFile);
            Worksheet ws = wb.Worksheets[0]; // first worksheet

            // -----------------------------------------------------------------
            // 2️⃣ Ensure a pivot table exists and export it (how to export pivot)
            // -----------------------------------------------------------------
            if (ws.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found. Exiting.");
                return;
            }

            // Export the first pivot table as a PNG image (pivot table to png)
            using (Image img = ws.PivotTables[0].ToImage())
            {
                // -----------------------------------------------------------------
                // 3️⃣ Save the pivot image to disk (save pivot image)
                // -----------------------------------------------------------------
                string outputFile = @"YOUR_DIRECTORY\pivot.png";
                img.Save(outputFile, ImageFormat.Png);
                Console.WriteLine($"Pivot exported successfully → {outputFile}");
            }
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:**  
```
Pivot exported successfully → YOUR_DIRECTORY\pivot.png
```

Και το αρχείο `pivot.png` θα περιέχει μια οπτική αναπαράσταση του αρχικού πίνακα pivot.

---

## Συχνές Ερωτήσεις

- **Λειτουργεί αυτό με αρχεία .xlsx που περιέχουν γραφήματα;**  
  Ναι. Η μέθοδος `ToImage()` ενδιαφέρεται μόνο για τη διάταξη του pivot table· τα γραφήματα δεν επηρεάζονται.

- **Μπορώ να εξάγω σε JPEG ή BMP αντί για PNG;**  
  Απόλυτα—απλώς αλλάξτε το όρισμα `ImageFormat` στη μέθοδο `Save`. Το PNG είναι lossless, γι' αυτό το προτείνουμε για καθαρά δεδομένα.

- **Τι γίνεται αν το βιβλίο εργασίας είναι προστατευμένο με κωδικό;**  
  Φορτώστε το με την υπερφόρτωση κωδικού:  
  `Workbook wb = new Workbook(inputFile, new LoadOptions { Password = "mySecret" });`

---

## Συμπεράσματα

Μόλις καλύψαμε **πώς να εξάγετε pivot** από ένα αρχείο Excel σε εικόνα PNG χρησιμοποιώντας το Aspose.Cells. Τα βήματα—**load excel workbook**, εντοπισμός του **pivot table to png**, και **save pivot image**—είναι απλά, αλλά αρκετά ισχυρά για πραγματικές ροές αναφοράς.

Επόμενα βήματα που μπορείτε να εξερευνήσετε:

- Αυτοματοποίηση της εξαγωγής για όλους τους πίνακες pivot σε έναν φάκελο (export excel pivot in bulk)  
- Ενσωμάτωση του PNG σε PDF ή HTML email (combine with iTextSharp or Razor)  
- Προσθήκη υδατογραφήματος ή προσαρμοσμένου στυλ στην εξαγόμενη εικόνα  

Δοκιμάστε τα και αφήστε τις εικόνες να μιλήσουν στο επόμενο dashboard σας.

---

![παράδειγμα εξόδου εξαγωγής pivot](assets/pivot-export-example.png "παράδειγμα εξόδου εξαγωγής pivot")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}