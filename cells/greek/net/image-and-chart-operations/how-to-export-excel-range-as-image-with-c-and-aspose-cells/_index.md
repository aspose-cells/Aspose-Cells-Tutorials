---
category: general
date: 2026-09-24
description: Εξαγωγή περιοχής Excel ως εικόνα σε C# χρησιμοποιώντας το Aspose.Cells
  – βήμα‑βήμα οδηγός για αποθήκευση περιοχής φύλλου εργασίας ως PNG ή JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: el
lastmod: 2026-09-24
og_description: Εξαγωγή περιοχής Excel ως εικόνα σε C# με το Aspose.Cells. Μάθετε
  πώς να μετατρέπετε οποιαδήποτε περιοχή φύλλου εργασίας, συμπεριλαμβανομένων των
  πινάκων Pivot, σε PNG ή JPEG σε λίγα λεπτά.
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: Εξαγωγή περιοχής Excel ως εικόνα με C# – πλήρης οδηγός Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: Πώς να εξάγετε μια περιοχή του Excel ως εικόνα με C# και Aspose.Cells
url: /el/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εξάγετε περιοχή Excel ως εικόνα με C# και Aspose.Cells

Αν χρειάζεστε **να εξάγετε περιοχή Excel ως εικόνα** σε μια εφαρμογή .NET, αυτός ο οδηγός σας δείχνει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Είτε δημοσιεύετε έναν πίνακα ελέγχου, ενσωματώνετε έναν πίνακα Pivot σε μια ιστοσελίδα, είτε δημιουργείτε μια μικρογραφία αναφοράς, μπορείτε να μετατρέψετε οποιαδήποτε περιοχή φύλλου εργασίας σε PNG (ή JPEG) με λίγες μόνο γραμμές κώδικα C#.

Σε αυτό το tutorial θα μάθετε πώς να:

* Φορτώσετε ένα υπάρχον βιβλίο εργασίας (`Workbook` class)  
* Ορίσετε την ακριβή περιοχή κελιών που θέλετε να καταγράψετε (`PrintArea`)  
* Διαμορφώσετε τις επιλογές εξαγωγής εικόνας (`ImageOrPrintOptions`)  
* Αποθηκεύσετε την προκύπτουσα εικόνα στο δίσκο  

Όλες οι προαπαιτούμενες συνθήκες, περιπτώσεις άκρων και κοινά λάθη καλύπτονται ώστε να μπορείτε να προσαρμόσετε τον κώδικα στα δικά σας έργα χωρίς εκπλήξεις.

## Προαπαιτούμενα

| Απαίτηση | Αιτιολογία |
|-------------|------------|
| **Aspose.Cells for .NET** (latest version) | Παρέχει τα API `Workbook`, `Worksheet` και `ImageOrPrintOptions` που χρησιμοποιούνται στο παράδειγμα. |
| **.NET 6.0 or later** | Το παράδειγμα στοχεύει στο .NET 6, αλλά οποιαδήποτε έκδοση .NET Core/Framework που υποστηρίζει το Aspose.Cells λειτουργεί. |
| **A valid Excel file** (e.g., `input.xlsx`) | Το βιβλίο εργασίας που θέλετε να μετατρέψετε. |
| **Write permission to the output folder** | Απαιτείται για την επιτυχία του `Save`. |

Μπορείτε να εγκαταστήσετε το Aspose.Cells μέσω NuGet:

```bash
dotnet add package Aspose.Cells
```

## Εξαγωγή περιοχής Excel ως εικόνα – επισκόπηση της διαδικασίας

Η λειτουργία αποτελείται από τρία λογικά στάδια:

1. **Load** το βιβλίο εργασίας από το δίσκο.  
2. **Define** την περιοχή κελιών που θα μετατραπεί σε εικόνα (η *print area*).  
3. **Export** την περιοχή χρησιμοποιώντας `ImageOrPrintOptions` και γράψτε το αρχείο.

Κάθε στάδιο αναλύεται παρακάτω σε ένα αφιερωμένο βήμα με πλήρη κώδικα και εξήγηση.

## Step 1: Load the workbook

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**Why this matters:**  
`Workbook` είναι το σημείο εισόδου για όλες τις λειτουργίες Excel. Η φόρτωση του αρχείου μία φορά διατηρεί τη χρήση μνήμης χαμηλή και σας επιτρέπει να έχετε πρόσβαση σε οποιοδήποτε φύλλο αργότερα.

## Step 2: Access the target worksheet

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**Tip:** Αν χρειάζεστε ένα συγκεκριμένο φύλλο με όνομα, αντικαταστήστε το δείκτη με `workbook.Worksheets["SheetName"]`. Αυτό αποτρέπει σφάλματα όταν η διάταξη του βιβλίου εργασίας αλλάζει.

## Step 3: Define the range you want to export

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**Why set `PrintArea`?**  
Το Aspose.Cells αποδίδει την *print area* κατά τη δημιουργία της εικόνας. Περιορίζοντάς την στην ακριβή περιοχή, αποφεύγετε περιττό κενό και βελτιώνετε την απόδοση.

### Alternative: Export the entire sheet

Αν θέλετε ολόκληρο το φύλλο εργασίας, απλώς παραλείψτε την ανάθεση του `PrintArea`. Το Aspose.Cells θα χρησιμοποιήσει την χρησιμοποιημένη περιοχή του φύλλου εξ ορισμού.

## Step 4: Configure image export options

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**Explanation of key properties:**

* `ImageFormat` – Καθορίζει τον τύπο αρχείου (`Png`, `Jpeg`, `Bmp`, κ.λπ.). Το PNG είναι ιδανικό για γραφήματα και κείμενο επειδή διατηρεί τις καθαρές άκρες.  
* `HorizontalResolution` / `VerticalResolution` – Ελέγχουν την πυκνότητα εικονοστοιχείων. Για μικρογραφίες ιστού 96 DPI αρκούν· για γραφικά έτοιμα για εκτύπωση συνιστάται 300 DPI.  
* `PageOrientation` – Βοηθά όταν η επιλεγμένη περιοχή είναι πιο πλατιά από ψηλή.

## Step 5: Export the range to an image file

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**What happens under the hood:**  
Όταν ορίζεται το `PrintArea`, το Aspose.Cells δημιουργεί μια προσωρινή εικόνα που αντιπροσωπεύει εκείνη την περιοχή. Το αντικείμενο `Pictures[0]` αποθηκεύεται στη συνέχεια χρησιμοποιώντας τις επιλογές που δώσατε.

### Handling worksheets without pictures

Αν το φύλλο εργασίας δεν περιέχει ήδη εικόνα (π.χ., ένα ολοκαίνουργιο αρχείο), μπορείτε να δημιουργήσετε μία επί τόπου:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## Full, runnable example

Συνδυάζοντας τα πάντα, εδώ είναι μια αυτόνομη εφαρμογή κονσόλας που μπορείτε να αντιγράψετε, επικολλήσετε και να εκτελέσετε:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**Expected output:**  
Ένα αρχείο με όνομα `range.png` εμφανίζεται στο `YOUR_DIRECTORY`. Το άνοιγμα του δείχνει τα ακριβή κελιά από **A1 έως G20** αποδομένα ως καθαρή εικόνα PNG.

## Common variations and edge‑case handling

| Σενάριο | Προσαρμογή |
|----------|------------|
| **Export to JPEG** | Αλλάξτε `ImageFormat = ImageFormat.Jpeg` και προαιρετικά ορίστε `Quality = 90` (εύρος 0‑100). |
| **Multiple ranges** | Καλέστε `sheet.Pictures.Add` για κάθε περιοχή και αποθηκεύστε κάθε εικόνα με διαφορετικό όνομα αρχείου. |
| **Large worksheets** | Αυξήστε `HorizontalResolution`/`VerticalResolution` μόνο για την απαιτούμενη περιοχή ώστε να αποφύγετε αιχμές μνήμης. |
| **No picture generated** | Επαληθεύστε ότι το `PrintArea` είναι σωστά μορφοποιημένο (`"A1:G20"`). Μία μη έγκυρη διεύθυνση οδηγεί σε κενή συλλογή `Pictures`. |
| **Saving to a stream** | Χρησιμοποιήστε `pic.Save(Stream, imgOptions)` όταν χρειάζεστε την εικόνα στη μνήμη (π.χ., για απόκριση ASP.NET). |

## Pro tips for reliable image export

* **Validate the print area** – Χρησιμοποιήστε την ανάλυση `CellArea` (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) για να δημιουργήσετε προγραμματιστικά περιοχές και να αποφύγετε τυπογραφικά λάθη.  
* **Dispose of resources** – Τυλίξτε το `Workbook` σε ένα `using` block αν επεξεργάζεστε πολλά αρχεία ώστε να ελευθερώνονται άμεσα οι εγγενείς πόροι.  
* **Batch processing** – Όταν εξάγετε δεκάδες περιοχές, επαναχρησιμοποιήστε ένα μόνο αντικείμενο `ImageOrPrintOptions` για να μειώσετε το κόστος δημιουργίας αντικειμένων.  
* **Thread safety** – Τα αντικείμενα Aspose.Cells **δεν** είναι thread‑safe. Δημιουργήστε ξεχωριστό `Workbook` ανά νήμα ή συγχρονίστε την πρόσβαση.

## Conclusion

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή μέθοδο για **να εξάγετε περιοχή Excel ως εικόνα** χρησιμοποιώντας C# και Aspose.Cells. Τα βήματα—φόρτωση του βιβλίου εργασίας, ορισμός της περιοχής εκτύπωσης, διαμόρφωση του `ImageOrPrintOptions` και αποθήκευση της εικόνας—καλύπτουν τόσο το “πώς” όσο και το “γιατί”, εξασφαλίζοντας ότι μπορείτε να προσαρμόσετε τον κώδικα σε pivot tables, γραφήματα ή οποιοδήποτε προσαρμοσμένο μπλοκ κελιών.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* **Export excel range as image** σε άλλες μορφές (SVG, BMP) – μια επιπλέον δευτερεύουσα λέξη-κλειδί για δοκιμή.  
* **Embedding the PNG in a PDF** χρησιμοποιώντας Aspose.PDF για ολοκληρωμένη δημιουργία αναφορών.  
* **Automating batch exports** σε πολλαπλά βιβλία εργασίας με έναν απλό βρόχο κονσόλας.

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές αναλύσεις, προσανατολισμούς και καταλόγους εξόδου. Καλό κώδικα!

## What Should You Learn Next?

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}