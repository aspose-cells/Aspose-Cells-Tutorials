---
category: general
date: 2026-03-21
description: Δημιουργία εικόνας από το Excel σε C# χρησιμοποιώντας το Aspose.Cells.
  Μάθετε πώς να μετατρέπετε το Excel σε εικόνα, να εξάγετε pivot και να αποθηκεύετε
  την εικόνα ως PNG με ένα πλήρες, εκτελέσιμο παράδειγμα.
draft: false
keywords:
- create image from excel
- convert excel to image
- how to export pivot
- how to save image
- export excel to png
language: el
og_description: Δημιουργήστε εικόνα από το Excel σε C# γρήγορα. Αυτός ο οδηγός δείχνει
  πώς να μετατρέψετε το Excel σε εικόνα, να εξάγετε το pivot και να αποθηκεύσετε την
  εικόνα ως PNG με καθαρό κώδικα.
og_title: Δημιουργία εικόνας από το Excel – Εξαγωγή Pivot σε PNG με C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Δημιουργία εικόνας από το Excel – Εξαγωγή Pivot σε PNG σε C#
url: /el/net/conversion-and-rendering/create-image-from-excel-export-pivot-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία εικόνας από Excel – Εξαγωγή Pivot σε PNG με C#

Έχετε ποτέ χρειαστεί να **create image from Excel** αλλά δεν ήξερτε ποιο API να χρησιμοποιήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν προσπαθούν να μετατρέψουν έναν ζωντανό πίνακα pivot σε ένα διαμοιραζόμενο PNG.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη προς εκτέλεση λύση που **converts Excel to image**, δείχνει **how to export pivot**, και εξηγεί **how to save image** ως αρχείο PNG. Στο τέλος θα έχετε μια μοναδική μέθοδο που εκτελεί όλη τη δουλειά, καθώς και συμβουλές για edge cases που μπορεί να συναντήσετε.

## Τι Θα Χρειαστείτε

- **Aspose.Cells for .NET** (το πακέτο NuGet `Aspose.Cells`). Είναι εμπορική βιβλιοθήκη αλλά προσφέρει δωρεάν λειτουργία αξιολόγησης—ιδανική για δοκιμές.  
- .NET 6+ (ή .NET Framework 4.6+).  
- Ένα απλό αρχείο Excel (`Pivot.xlsx`) που περιέχει τουλάχιστον έναν πίνακα pivot.  
- Οποιοδήποτε IDE προτιμάτε—Visual Studio, Rider, ή ακόμη και VS Code λειτουργεί.

Αυτό είναι όλο. Χωρίς επιπλέον DLLs, χωρίς COM interop, και χωρίς μπερδεμένα κόλπα αυτοματισμού Excel.  

Τώρα, ας βουτήξουμε στον κώδικα.

## Βήμα 1: Φόρτωση του Workbook – Create Image from Excel

Το πρώτο που κάνουμε είναι να ανοίξουμε το αρχείο Excel που περιέχει τον πίνακα pivot. Αυτό το βήμα είναι κρίσιμο επειδή ο renderer λειτουργεί πάνω σε ένα αντικείμενο `Workbook` στη μνήμη.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

public class ExcelImageExporter
{
    /// <summary>
    /// Loads the workbook and prepares it for rendering.
    /// </summary>
    /// <param name="excelPath">Full path to the source .xlsx file.</param>
    /// <returns>The worksheet that contains the pivot.</returns>
    private static Worksheet LoadPivotWorksheet(string excelPath)
    {
        // Step 1: Load the workbook that contains the pivot table
        Workbook workbook = new Workbook(excelPath);

        // Assume the first sheet holds the pivot; adjust index if needed
        Worksheet pivotWorksheet = workbook.Worksheets[0];
        return pivotWorksheet;
    }
}
```

*Γιατί είναι σημαντικό:* Η φόρτωση του workbook μας δίνει πρόσβαση στο **pivot** και σε οποιαδήποτε μορφοποίηση που θα διατηρηθεί όταν αργότερα **convert Excel to image**. Αν το παραλείψετε, ο renderer δεν θα έχει τίποτα για να δουλέψει.

## Βήμα 2: Διαμόρφωση Επιλογών Εξαγωγής – Convert Excel to Image

Στη συνέχεια, λέμε στο Aspose πώς θέλουμε να φαίνεται η τελική εικόνα. Η κλάση `ImageOrPrintOptions` μας επιτρέπει να επιλέξουμε PNG, να ορίσουμε DPI, και ακόμη να ελέγξουμε το χρώμα φόντου.

```csharp
private static ImageOrPrintOptions GetImageOptions()
{
    // Step 3: Configure image export options – we want a PNG image
    ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
    {
        ImageFormat = ImageFormat.Png,      // Export Excel to PNG
        HorizontalResolution = 300,         // High‑resolution output
        VerticalResolution = 300,
        OnePagePerSheet = true               // Render the whole sheet as one page
    };
    return imageOptions;
}
```

*Γιατί είναι σημαντικό:* Ορίζοντας υψηλό DPI εξασφαλίζουμε ότι η **export Excel to PNG** φαίνεται καθαρή, ακόμα και όταν ο pivot περιέχει πολλές γραμμές. Μπορείτε να μειώσετε το DPI αν το μέγεθος του αρχείου είναι πρόβλημα.

## Βήμα 3: Απόδοση του Worksheet – How to Export Pivot

Τώρα έρχεται η καρδιά της διαδικασίας: η μετατροπή του worksheet (με το pivot) σε εικόνα. Η κλάση `WorksheetRender` κάνει το σκληρό έργο.

```csharp
private static void RenderWorksheetToImage(Worksheet sheet, string outputPath)
{
    // Step 4: Create a renderer for the worksheet using the options
    WorksheetRender renderer = new WorksheetRender(sheet, GetImageOptions());

    // Step 5: Render the first page (index 0) to an image file
    renderer.ToImage(0, outputPath);
}
```

*Γιατί είναι σημαντικό:* Εδώ είναι που **how to export pivot** σε οπτική μορφή. Ο renderer σέβεται όλη τη μορφοποίηση του pivot, τα slicers και τα conditional styles, έτσι το PNG φαίνεται ακριβώς όπως το βλέπετε στο Excel.

## Βήμα 4: Συνδυασμός Όλων – How to Save Image

Τέλος, εκθέτουμε μια μοναδική δημόσια μέθοδο που ενώνει όλα τα κομμάτια. Αυτή είναι η μέθοδος που θα καλέσετε από την εφαρμογή, την υπηρεσία ή το εργαλείο console σας.

```csharp
/// <summary>
/// Converts an Excel file containing a pivot table into a PNG image.
/// </summary>
/// <param name="excelFile">Path to the source .xlsx file.</param>
/// <param name="imageFile">Desired path for the output PNG.</param>
public static void ExportPivotToPng(string excelFile, string imageFile)
{
    Worksheet pivotWorksheet = LoadPivotWorksheet(excelFile);
    RenderWorksheetToImage(pivotWorksheet, imageFile);
}
```

### Πλήρες Παράδειγμα Λειτουργίας

Δημιουργήστε ένα νέο project console, προσθέστε το πακέτο NuGet `Aspose.Cells`, και στη συνέχεια τοποθετήστε το παρακάτω `Program.cs`:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to your environment
            string excelPath = @"C:\Temp\Pivot.xlsx";
            string pngPath   = @"C:\Temp\PivotImage.png";

            try
            {
                ExcelImageExporter.ExportPivotToPng(excelPath, pngPath);
                Console.WriteLine($"✅ Image saved successfully: {pngPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed: {ex.Message}");
            }
        }
    }

    // ----- Helper class from earlier steps -----
    public class ExcelImageExporter
    {
        private static Worksheet LoadPivotWorksheet(string excelPath)
        {
            Workbook workbook = new Workbook(excelPath);
            Worksheet pivotWorksheet = workbook.Worksheets[0];
            return pivotWorksheet;
        }

        private static ImageOrPrintOptions GetImageOptions()
        {
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300,
                OnePagePerSheet = true
            };
            return imageOptions;
        }

        private static void RenderWorksheetToImage(Worksheet sheet, string outputPath)
        {
            WorksheetRender renderer = new WorksheetRender(sheet, GetImageOptions());
            renderer.ToImage(0, outputPath);
        }

        public static void ExportPivotToPng(string excelFile, string imageFile)
        {
            Worksheet pivotWorksheet = LoadPivotWorksheet(excelFile);
            RenderWorksheetToImage(pivotWorksheet, imageFile);
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση του προγράμματος, το `PivotImage.png` θα εμφανιστεί στο φάκελο που καθορίσατε, εμφανίζοντας ένα pixel‑perfect στιγμιότυπο του πίνακα pivot.

![Create image from Excel example](https://example.com/placeholder.png "Create image from Excel example")

*Alt text:* παράδειγμα δημιουργίας εικόνας από excel που δείχνει τον εξαγόμενο πίνακα pivot ως PNG.

## Συχνές Ερωτήσεις & Edge Cases

### Τι γίνεται αν το workbook μου έχει πολλαπλά worksheets;

Ο βοηθός αυτή τη στιγμή παίρνει το `Worksheets[0]`. Για να στοχεύσετε ένα συγκεκριμένο φύλλο, περάστε το όνομα του φύλλου:

```csharp
Worksheet pivotWorksheet = workbook.Worksheets["SalesPivot"];
```

### Το PNG είναι θολό—πώς το διορθώνω;

Αυξήστε το `HorizontalResolution` και το `VerticalResolution` στο `GetImageOptions`. Τιμές 300–600 DPI συνήθως παράγουν καθαρά αποτελέσματα. Θυμηθείτε, υψηλότερο DPI σημαίνει μεγαλύτερο μέγεθος αρχείου.

### Ο pivot μου εκτείνεται σε περισσότερες από μία σελίδες—μπορώ να εξάγω όλες τις σελίδες;

Ναι. Κάντε βρόχο πάνω από το `renderer.PageCount` και καλέστε `ToImage(pageIndex, ...)` για κάθε σελίδα, ή ορίστε `OnePagePerSheet = false` για να λάβετε ξεχωριστές εικόνες ανά σελίδα.

### Χρειάζομαι μόνο ένα τμήμα του φύλλου (π.χ., μια συγκεκριμένη περιοχή);

Χρησιμοποιήστε το `ImageOrPrintOptions` για να ορίσετε το `PrintArea`:

```csharp
imageOptions.PrintArea = "A1:D20";
```

Με αυτόν τον τρόπο **convert Excel to image** μόνο για την περιοχή που σας ενδιαφέρει.

### Λειτουργεί αυτό με αρχεία .xls (Excel 97‑2003);

Απολύτως. Το Aspose.Cells αφαιρεί την εξάρτηση από τη μορφή αρχείου, έτσι μπορείτε να δώσετε `.xls`, `.xlsx`, `.xlsm`, ή ακόμη και `.ods` και να **export excel to png**.

## Pro Tips & Gotchas

- **License matters**: Στην κατάσταση αξιολόγησης το Aspose προσθέτει υδατογράφημα. Αναπτύξτε μια κατάλληλη άδεια για παραγωγή.  
- **Memory usage**: Η απόδοση μεγάλων workbooks μπορεί να καταναλώνει πολύ μνήμη. Αποδεσμεύστε το αντικείμενο `Workbook` άμεσα ή τυλίξτε το σε block `using`.  
- **Thread safety**: Το `Workbook` δεν είναι thread‑safe. Δημιουργήστε μια νέα παρουσία ανά αίτημα αν βρίσκεστε σε web service.  
- **Image format flexibility**: Αν χρειάζεστε JPEG ή BMP, απλώς αλλάξτε το `ImageFormat` στο `GetImageOptions`.  

## Συμπέρασμα

Τώρα έχετε μια ισχυρή, end‑to‑end συνταγή για **create image from Excel**, συγκεκριμένα για **export pivot** δεδομένα ως PNG υψηλής ποιότητας. Το παραπάνω snippet δείχνει τον πλήρη, εκτελέσιμο κώδικα, εξηγεί **how to save image**, και καλύπτει παραλλαγές όπως πολλαπλά φύλλα ή προσαρμοσμένες περιοχές εκτύπωσης.  

Επόμενα βήματα; Δοκιμάστε να συνδέσετε αυτόν τον εξαγωγέα με μια υπηρεσία email για να στέλνετε το PNG αυτόματα, ή πειραματιστείτε με το `ImageOrPrintOptions` για να δημιουργήσετε PDFs αντί για PNGs. Το ίδιο pattern λειτουργεί για εργασίες **convert excel to image** σε πολλές μορφές.  

Έχετε περισσότερες ερωτήσεις; Αφήστε ένα σχόλιο, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}