---
category: general
date: 2026-10-10
description: Μετατρέψτε το Excel σε PNG γρήγορα χρησιμοποιώντας το Aspose.Cells σε
  C#. Μάθετε πώς να εξάγετε μια περιοχή Excel, να αποθηκεύσετε το Excel ως PNG και
  να μετατρέψετε ένα φύλλο εργασίας σε εικόνα σε λίγα λεπτά.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to png
- export excel range
- save excel as png
- how to export excel
- convert worksheet to image
language: el
lastmod: 2026-10-10
og_description: Μετατρέψτε το Excel σε PNG άμεσα με το Aspose.Cells. Αυτό το σεμινάριο
  δείχνει πώς να εξάγετε μια περιοχή Excel, να αποθηκεύσετε το Excel ως PNG και να
  μετατρέψετε το φύλλο εργασίας σε εικόνα.
og_image_alt: Screenshot of C# code that converts an Excel worksheet to a PNG image
og_title: Μετατροπή Excel σε PNG με C# – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: convert excel to png quickly using Aspose.Cells in C#. Learn to export
    excel range, save excel as png, and convert worksheet to image in minutes.
  headline: How to convert Excel to PNG with C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Image export
- Automation
title: Πώς να μετατρέψετε το Excel σε PNG με C# – οδηγός βήμα‑προς‑βήμα
url: /el/net/converting-excel-files-to-other-formats/how-to-convert-excel-to-png-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε το Excel σε PNG με C# – οδηγός βήμα‑βήμα

Αν χρειάζεστε να **μετατρέψετε το Excel σε PNG** προγραμματιστικά, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε χρησιμοποιώντας το Aspose.Cells for .NET. Είτε δημιουργείτε μια υπηρεσία αναφορών είτε έναν αυτοματοποιημένο πίνακα ελέγχου, θα μάθετε να εξάγετε μια περιοχή Excel, να αποθηκεύετε το αποτέλεσμα ως αρχείο PNG και να αντιμετωπίζετε κοινές περιπτώσεις άκρων.

Θα περάσετε από κάθε απαιτούμενο βήμα—από την προσθήκη του πακέτου NuGet μέχρι την απόδοση μιας συγκεκριμένης περιοχής φύλλου εργασίας—ώστε να ενσωματώσετε τη λύση σε οποιοδήποτε έργο C# χωρίς να χρειάζεται να ψάχνετε για πρόσθετους πόρους.

## Προαπαιτούμενα

* .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
* Visual Studio 2022 (ή οποιοδήποτε IDE που υποστηρίζει C#)
* Ένα έγκυρο άδεια Aspose.Cells for .NET (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση)
* Ένα αρχείο Excel με όνομα **Pivot.xlsx** τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε (το tutorial χρησιμοποιεί `YOUR_DIRECTORY` ως placeholder)

> **Συμβουλή επαγγελματία:** Εγκαταστήστε το πακέτο Aspose.Cells μέσω του NuGet Package Manager Console:  
> `Install-Package Aspose.Cells`

## Μετατροπή Excel σε PNG – πλήρης περιήγηση κώδικα

Το παρακάτω πλήρες πρόγραμμα φορτώνει ένα βιβλίο εργασίας, διαμορφώνει τις επιλογές εικόνας και αποδίδει μια ορισμένη περιοχή κελιών σε αρχείο PNG. Όλες οι απαιτούμενες οδηγίες `using` περιλαμβάνονται, ώστε να μπορείτε να αντιγράψετε τον κώδικα σε ένα νέο έργο κονσόλας και να το εκτελέσετε αμέσως.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the workbook (convert excel to png starts here)
            // -------------------------------------------------
            string workbookPath = @"YOUR_DIRECTORY\Pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -------------------------------------------------
            // Step 2: Configure image options (PNG format)
            // -------------------------------------------------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                // Export format – PNG ensures lossless quality
                ImageFormat = ImageFormat.Png,

                // Optional: set resolution (default is 96 DPI)
                // HorizontalResolution = 150,
                // VerticalResolution = 150
            };

            // -------------------------------------------------
            // Step 3: Define the range you want to export
            // -------------------------------------------------
            // Example range A1:H30 – you can change this to any valid Excel range
            string range = "A1:H30";

            // -------------------------------------------------
            // Step 4: Render the range to an image file
            // -------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\Pivot.png";
            workbook.Worksheets[0].RenderRangeToImage(range, outputPath, imgOptions);

            Console.WriteLine($"Excel range {range} has been exported to PNG at: {outputPath}");
        }
    }
}
```

### Πώς λειτουργεί ο κώδικας

* **Φόρτωση του βιβλίου εργασίας** – `Workbook` διαβάζει το αρχείο `.xlsx` στη μνήμη, παρέχοντάς σας πρόσβαση σε όλα τα φύλλα εργασίας.
* **ImageOrPrintOptions** – Αυτό το αντικείμενο λέει στο Aspose.Cells να παράγει PNG (`ImageFormat.Png`). Μπορείτε επίσης να προσαρμόσετε DPI, κλίμακα ή χρώμα φόντου αν χρειάζεται.
* **RenderRangeToImage** – Η μέθοδος `RenderRangeToImage` δέχεται τρία ορίσματα: την περιοχή κελιών (`"A1:H30"`), τη διαδρομή αρχείου προορισμού και τις επιλογές εικόνας. Αυτή είναι η βασική λειτουργία που **εξάγει την περιοχή excel** σε εικόνα PNG.
* **Αποτέλεσμα** – Μετά την εκτέλεση, θα βρείτε το `Pivot.png` στον καθορισμένο φάκελο, περιέχοντας μια ακριβή οπτική αναπαράσταση των επιλεγμένων κελιών.

## Εξαγωγή περιοχής excel σε PNG – προσαρμογή εξόδου

Αν χρειάζεστε να **εξάγετε περιοχή excel** διαφορετική από `A1:H30`, απλώς αλλάξτε τη μεταβλητή `range`. Η μέθοδος δέχεται οποιαδήποτε διεύθυνση σε στυλ Excel, συμπεριλαμβανομένων των ονομαστικών περιοχών:

```csharp
// Export a named range called "ReportArea"
string range = "ReportArea";
```

Μπορείτε επίσης να εξάγετε ολόκληρο το φύλλο εργασίας χρησιμοποιώντας `"A1:Z1000"` (ή μια μεγαλύτερη διεύθυνση) ή καλώντας το `RenderToImage` χωρίς παράμετρο περιοχής.

## Αποθήκευση excel ως png με πρόσθετες ρυθμίσεις

Μερικές φορές θέλετε το PNG να ταιριάζει με συγκεκριμένη ανάλυση για εκτύπωση ή χρήση στο web. Προσαρμόστε το `ImageOrPrintOptions` ως εξής:

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    HorizontalResolution = 300,   // 300 DPI for high‑quality print
    VerticalResolution = 300,
    Transparent = true           // Makes the background transparent
};
```

Αυτές οι ρυθμίσεις δείχνουν πώς να **αποθηκεύσετε excel ως png** με προσαρμοσμένο DPI και διαφάνεια, δίνοντάς σας πλήρη έλεγχο στην τελική ποιότητα της εικόνας.

## Πώς να εξάγετε excel – διαχείριση πολλαπλών φύλλων εργασίας

Το παράδειγμα στοχεύει στο πρώτο φύλλο εργασίας (`Worksheets[0]`). Για να **μετατρέψετε φύλλο εργασίας σε εικόνα** για διαφορετικό φύλλο, αναφερθείτε του με δείκτη ή όνομα:

```csharp
// By index (second sheet)
Worksheet sheet = workbook.Worksheets[1];

// By name
Worksheet sheet = workbook.Worksheets["DataSheet"];
sheet.RenderRangeToImage(range, outputPath, imgOptions);
```

Η επεξεργασία κάθε φύλλου σε βρόχο είναι απλή:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string sheetPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.png";
    workbook.Worksheets[i].RenderRangeToImage(range, sheetPath, imgOptions);
    Console.WriteLine($"Sheet {i + 1} exported to {sheetPath}");
}
```

## Περιπτώσεις άκρων και αντιμετώπιση προβλημάτων

| Κατάσταση | Συνιστώμενη προσέγγιση |
|-----------|----------------------|
| **Πολύ μεγάλη περιοχή** (π.χ., ολόκληρο το βιβλίο εργασίας) | Αυξήστε το `HorizontalResolution`/`VerticalResolution` σταδιακά για να αποφύγετε το `OutOfMemoryException`. Σκεφτείτε την εξαγωγή κάθε φύλλου ξεχωριστά. |
| **Συγχωνευμένα κελιά** | Το Aspose.Cells διατηρεί αυτόματα τα οπτικά στοιχεία των συγχωνευμένων κελιών, αλλά ελέγξτε το αποτέλεσμα εάν βασίζεστε σε ακριβές πλάτη στηλών. |
| **Τύποι που αναφέρονται σε εξωτερικά αρχεία** | Βεβαιωθείτε ότι αυτά τα αρχεία είναι προσβάσιμα πριν φορτώσετε το βιβλίο εργασίας· διαφορετικά η αποδοθείσα εικόνα μπορεί να εμφανίζει παλαιές τιμές. |
| **Λείπει άδεια** | Η δοκιμαστική έκδοση προσθέτει υδατογράφημα. Εφαρμόστε μια έγκυρη άδεια (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`) πριν την απόδοση για να παραχθεί ένα καθαρό PNG. |

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω είναι το αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε. Αντικαταστήστε το `YOUR_DIRECTORY` με μια πραγματική διαδρομή φακέλου στο μηχάνημά σας.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main()
        {
            // Load workbook
            var workbook = new Workbook(@"C:\Temp\Pivot.xlsx");

            // Set PNG options
            var options = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 150,
                VerticalResolution = 150
            };

            // Define range and output file
            string range = "A1:H30";
            string output = @"C:\Temp\Pivot.png";

            // Export the range as a PNG image
            workbook.Worksheets[0].RenderRangeToImage(range, output, options);

            Console.WriteLine($"Successfully converted Excel to PNG: {output}");
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα**

```
Successfully converted Excel to PNG: C:\Temp\Pivot.png
```

Ανοίξτε το `Pivot.png` με οποιονδήποτε προβολέα εικόνων—θα δείτε την ακριβή οπτική διάταξη των κελιών A1 μέχρι H30, συμπεριλαμβανομένων μορφοποίησης, χρωμάτων και περιγραμμάτων.

## Συμπέρασμα

Τώρα έχετε μια αξιόπιστη μέθοδο για **μετατροπή Excel σε PNG** χρησιμοποιώντας C#. Ο οδηγός κάλυψε πώς να **εξάγετε περιοχή excel**, **αποθηκεύσετε excel ως png**, και **μετατρέψετε φύλλο εργασίας σε εικόνα** με προσαρμόσιμες επιλογές και συμβουλές βέλτιστων πρακτικών.

* Ενσωματώστε τον κώδικα σε ένα web API για δημιουργία εικόνων κατ' απαίτηση.  
* Συνδυάστε την έξοδο PNG με δημιουργία PDF για αναφορές πολλαπλών μορφών.  
* Εξερευνήστε άλλες μορφές εικόνας (`ImageFormat.Jpeg`, `ImageFormat.Bmp`) προσαρμόζοντας την ιδιότητα `ImageFormat`.

Μη διστάσετε να πειραματιστείτε με διαφορετικές περιοχές, αναλύσεις και επιλογές φύλλων εργασίας για να ταιριάζουν στο συγκεκριμένο σενάριο αυτοματοποίησής σας.

---

## Τι Θα Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εξάγετε ένα Φύλλο Εργασίας Excel σε PNG Χρησιμοποιώντας Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Μετατροπή Excel σε PNG, TIFF και PDF σε Java χρησιμοποιώντας Aspose.Cells](/cells/english/java/workbook-operations/render-excel-as-png-tiff-pdf-aspose-cells-java/)
- [Κατακτώντας το Aspose.Cells Java: Μετατροπή Excel σε PNG με Προσαρμοσμένο Παροχέα Ροής](/cells/english/java/advanced-features/aspose-cells-java-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}