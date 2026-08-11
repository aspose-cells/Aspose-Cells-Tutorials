---
category: general
date: 2026-08-11
description: Πώς να εξάγετε το Excel σε PNG και να αποθηκεύσετε το εύρος του Excel
  ως εικόνα χρησιμοποιώντας το Aspose.Cells. Μάθετε πώς να αποθηκεύετε την εικόνα
  φύλλου Excel και να εξάγετε την εικόνα του πίνακα Pivot σε λίγα λεπτά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel to png
- save excel range as image
- save excel sheet picture
- export pivot table image
language: el
lastmod: 2026-08-11
og_description: Πώς να εξάγετε το Excel σε PNG γρήγορα. Αυτό το σεμινάριο σας δείχνει
  πώς να αποθηκεύσετε μια περιοχή του Excel ως εικόνα, να αποθηκεύσετε την εικόνα
  φύλλου Excel και να εξάγετε την εικόνα του πίνακα Pivot με το Aspose.Cells.
og_image_alt: Screenshot of C# code exporting an Excel worksheet to a PNG file
og_title: Πώς να εξάγετε το Excel σε PNG – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to export Excel to PNG and save Excel range as image using Aspose.Cells.
    Learn to save Excel sheet picture and export pivot table image in minutes.
  headline: How to export Excel to PNG – full step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Excel automation
- C#
- image export
title: Πώς να εξάγετε το Excel σε PNG – πλήρης οδηγός βήμα‑βήμα
url: /el/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε το Excel σε PNG – πλήρης οδηγός βήμα‑βήμα

Αν χρειάζεστε **πώς να εξάγετε το Excel σε PNG**, αυτός ο οδηγός σας καθοδηγεί μέσα από όλη τη διαδικασία χρησιμοποιώντας το Aspose.Cells για .NET. Είτε θέλετε να **αποθηκεύσετε ένα εύρος Excel ως εικόνα**, να ενσωματώσετε μια εικόνα φύλλου εργασίας σε μια αναφορά, ή να **εξάγετε εικόνα πίνακα Pivot** για έναν πίνακα ελέγχου, τα παρακάτω βήματα σας παρέχουν μια έτοιμη λύση.

Θα μάθετε πώς να φορτώσετε ένα βιβλίο εργασίας, να ανανεώσετε έναν πίνακα Pivot, να διαμορφώσετε τις επιλογές εικόνας και, τελικά, να γράψετε ένα αρχείο PNG που διατηρεί την μορφοποιημένη εμφάνιση των αρχικών δεδομένων. Δεν απαιτούνται εξωτερικά εργαλεία ή χειροκίνητες λήψεις οθόνης.

## Προαπαιτούμενα

* .NET 6.0 SDK ή νεότερο εγκατεστημένο  
* Visual Studio 2022 (ή οποιοδήποτε IDE C#)  
* Άδεια Aspose.Cells για .NET ή δωρεάν έκδοση αξιολόγησης – κατεβάστε από το [Aspose.Cells website](https://products.aspose.com/cells/net)  
* Ένα δείγμα αρχείου Excel (`PivotTable.xlsx`) που περιέχει τουλάχιστον έναν πίνακα Pivot  

Ο κώδικας λειτουργεί σε Windows, macOS και Linux επειδή το Aspose.Cells είναι ανεξάρτητο από την πλατφόρμα.

## Βήμα 1: Εγκατάσταση Aspose.Cells μέσω NuGet

Ανοίξτε το φάκελο του έργου σας σε ένα τερματικό και εκτελέστε:

```bash
dotnet add package Aspose.Cells
```

Αυτό προσθέτει την πιο πρόσφατη σταθερή έκδοση του **Aspose.Cells** στο `.csproj` σας. Η βιβλιοθήκη παρέχει τις κλάσεις `Workbook`, `Worksheet`, `ImageOrPrintOptions` και άλλες που θα χρησιμοποιήσουμε για να **αποθηκεύσουμε εικόνα φύλλου Excel**.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας που περιέχει τον πίνακα Pivot

```csharp
using Aspose.Cells;
using System;

// Load the Excel file – replace the path with your actual location
string sourcePath = @"YOUR_DIRECTORY\PivotTable.xlsx";
Workbook workbook = new Workbook(sourcePath);
```

*Γιατί είναι σημαντικό:*  
Η φόρτωση του βιβλίου εργασίας σας δίνει πρόσβαση σε όλα τα φύλλα εργασίας, τα κελιά και τα ενσωματωμένα αντικείμενα. Η κλάση `Workbook` αφαιρεί την πολυπλοκότητα του μορφότυπου αρχείου, ώστε να μπορείτε να δουλέψετε με `.xlsx`, `.xls` ή ακόμη και `.csv` χωρίς επιπλέον κώδικα ανάλυσης.

## Βήμα 3: Επιλογή του φύλλου εργασίας και ανανέωση του πίνακα Pivot

```csharp
// Get the first worksheet where the pivot table resides
Worksheet sheet = workbook.Worksheets[0];

// Refresh the pivot table so it reflects the latest source data
if (sheet.PivotTables.Count > 0)
{
    sheet.PivotTables[0].Refresh();
}
else
{
    Console.WriteLine("No pivot tables found on the selected worksheet.");
}
```

*Γιατί είναι σημαντικό:*  
Οι πίνακες Pivot αποθηκεύουν στην προσωρινή μνήμη τα δεδομένα προέλευσής τους. Η κλήση του `Refresh()` εξασφαλίζει ότι η οπτική αναπαράσταση ταιριάζει με τυχόν πρόσφατες αλλαγές, κάτι που είναι κρίσιμο όταν αργότερα **εξάγετε εικόνα πίνακα Pivot**.

## Βήμα 4: Διαμόρφωση επιλογών εξαγωγής εικόνας (μορφή PNG, διατήρηση στυλ)

```csharp
// Set up export options – PNG keeps lossless quality and supports transparency
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Png,
    // Preserve the pivot table’s style (fonts, colors, borders)
    CalculatePivotTableStyle = true,
    // Optional: set image resolution (DPI) for higher quality
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

*Γιατί είναι σημαντικό:*  
`CalculatePivotTableStyle = true` λέει στο Aspose.Cells να αποδώσει τον πίνακα Pivot ακριβώς όπως εμφανίζεται στο Excel, συμπεριλαμβανομένης της υπό συνθήκη μορφοποίησης. Η ρύθμιση του DPI μπορεί να είναι χρήσιμη για εκτύπωση ή οθόνες υψηλής ανάλυσης.

## Βήμα 5: Καταγραφή του χρησιμοποιημένου εύρους (συμπεριλαμβανομένου του πίνακα Pivot) ως εικόνα

```csharp
// Determine the range that contains data – MaxDisplayRange covers the whole used area
CellArea usedRange = sheet.Cells.MaxDisplayRange;

// Add a picture of the used range to the worksheet (position 0,0) and save it
Picture pic = sheet.Pictures.Add(0, 0, usedRange);
pic.Save(@"YOUR_DIRECTORY\PivotImage.png", imgOptions);
```

*Γιατί είναι σημαντικό:*  
`MaxDisplayRange` επεκτείνεται αυτόματα μέχρι το πιο απομακρυσμένο κελί που περιέχει δεδομένα, τύπους ή μορφοποίηση, εξασφαλίζοντας ότι ολόκληρος ο πίνακας Pivot και τα γύρω κελιά περιλαμβάνονται. Η μέθοδος `Pictures.Add` δημιουργεί μια εικόνα στη μνήμη που γράφουμε αμέσως στο δίσκο ως αρχείο PNG.

## Πλήρες εκτελέσιμο παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι ένα αυτόνομο πρόγραμμα κονσόλας που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε:

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPngExport
{
    class Program
    {
        static void Main()
        {
            // ---------- 1. Load workbook ----------
            string sourcePath = @"YOUR_DIRECTORY\PivotTable.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // ---------- 2. Get first worksheet ----------
            Worksheet sheet = workbook.Worksheets[0];

            // ---------- 3. Refresh pivot table ----------
            if (sheet.PivotTables.Count > 0)
            {
                sheet.PivotTables[0].Refresh();
            }
            else
            {
                Console.WriteLine("No pivot tables found on the selected worksheet.");
                return;
            }

            // ---------- 4. Set image export options ----------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Png,
                CalculatePivotTableStyle = true,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // ---------- 5. Export used range as PNG ----------
            CellArea usedRange = sheet.Cells.MaxDisplayRange;
            Picture pic = sheet.Pictures.Add(0, 0, usedRange);
            string outputPath = @"YOUR_DIRECTORY\PivotImage.png";
            pic.Save(outputPath, imgOptions);

            Console.WriteLine($"Pivot table image saved to: {outputPath}");
        }
    }
}
```

### Αναμενόμενη έξοδος

Όταν εκτελέσετε το πρόγραμμα, η κονσόλα εμφανίζει:

```
Pivot table image saved to: YOUR_DIRECTORY\PivotImage.png
```

Και το αρχείο `PivotImage.png` εμφανίζεται στον φάκελο προορισμού. Ανοίξτε το με οποιονδήποτε προβολέα εικόνων—θα δείτε την ακριβή οπτική αναπαράσταση του φύλλου εργασίας Excel, συμπεριλαμβανομένου του μορφοποιημένου πίνακα Pivot, των κεφαλίδων στηλών και τυχόν γύρω δεδομένων.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Σενάριο | Προσαρμογή |
|----------|------------|
| **Εξαγωγή μόνο ενός συγκεκριμένου εύρους κελιών** (π.χ., `A1:D20`) | Αντικαταστήστε το `sheet.Cells.MaxDisplayRange` με `new CellArea { StartRow = 0, StartColumn = 0, EndRow = 19, EndColumn = 3 }`. |
| **Πολλαπλά φύλλα εργασίας** | Κάντε βρόχο μέσω `workbook.Worksheets` και επαναλάβετε τα βήματα 3‑5 για κάθε φύλλο που θέλετε να εξάγετε. |
| **Διαφορετική μορφή εικόνας** (JPEG, BMP) | Αλλάξτε `SaveFormat = SaveFormat.Jpeg` (ή `Bmp`). Το PNG συνιστάται για απώλεια‑ποιότητας. |
| **Μεγάλα φύλλα εργασίας** που προκαλούν πίεση μνήμης | Χρησιμοποιήστε `sheet.Pictures.Add` με μικρότερο `CellArea` ή χωρίστε την εξαγωγή σε πολλές εικόνες. |
| **Δεν υπάρχει πίνακας Pivot** | Προστατέψτε με `if (sheet.PivotTables.Count == 0)` όπως φαίνεται· μπορείτε ακόμη να εξάγετε το κανονικό εύρος. |

## Συμβουλές επαγγελματιών

* **Καταχωρίστε την άδεια νωρίς** – Καταχωρίστε την άδεια Aspose.Cells πριν φορτώσετε το βιβλίο εργασίας για να αποφύγετε το υδατογράφημα αξιολόγησης.  
  ```csharp
  var license = new License();
  license.SetLicense(@"YOUR_DIRECTORY\Aspose.Total.NET.lic");
  ```
* **Ομαδική εξαγωγή** – Για pipelines αναφορών, τυλίξτε τη λογική εξαγωγής σε μια μέθοδο που επιστρέφει `byte[]`. Αυτό σας επιτρέπει να στέλνετε το PNG απευθείας σε ένα web API χωρίς να αγγίζετε το σύστημα αρχείων.  
* **Διαφανές φόντο** – Το PNG υποστηρίζει ήδη διαφάνεια. Αν θέλετε λευκό φόντο, ορίστε `imgOptions.Transparent = false;`.  

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να εξάγετε το Excel σε PNG** χρησιμοποιώντας το Aspose.Cells, καλύπτοντας ολόκληρη τη ροή εργασίας από τη φόρτωση του βιβλίου εργασίας μέχρι το **αποθήκευση εύρους Excel ως εικόνα**, το **αποθήκευση εικόνας φύλλου Excel** και το **εξαγωγή εικόνας πίνακα Pivot**. Ο παρεχόμενος κώδικας είναι πλήρης, εκτελέσιμος και προσαρμόσιμος σε πραγματικά σενάρια όπως η αυτοματοποιημένη αναφορά ή η δημιουργία πινάκων ελέγχου.

Έτοιμοι για το επόμενο βήμα; Εξερευνήστε πώς να **μετατρέψετε το PNG σε PDF** για εκτυπώσιμες αναφορές, ή ενσωματώστε την εικόνα σε μια υπηρεσία web που παρέχει ζωντανές οπτικοποιήσεις Excel. Καλή προγραμματιστική!

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να εξάγετε ένα φύλλο εργασίας Excel σε PNG χρησιμοποιώντας Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Εξαγωγή βιβλίου εργασίας Excel ως εικόνα χρησιμοποιώντας Aspose.Cells για Java: Οδηγός βήμα‑βήμα](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Πώς να εξάγετε κελιά Excel ως εικόνες χρησιμοποιώντας Aspose.Cells για Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}