---
category: general
date: 2026-10-26
description: Ορίστε την περιοχή εκτύπωσης και εξάγετε ένα φύλλο Excel σε PNG με C#.
  Μάθετε τις επιλογές εξαγωγής εικόνας, πώς να εξάγετε PNG και πώς να λάβετε μια εκτυπώσιμη
  εικόνα από ένα βιβλίο εργασίας.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: el
lastmod: 2026-10-26
og_description: Ορίστε την περιοχή εκτύπωσης και εξάγετε ένα φύλλο Excel σε PNG σε
  C#. Αυτό το βήμα‑βήμα tutorial καλύπτει τις επιλογές εξαγωγής εικόνας και πώς να
  εξάγετε PNG από ένα βιβλίο εργασίας.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Ορισμός περιοχής εκτύπωσης και εξαγωγή φύλλου Excel σε PNG – Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Ορισμός περιοχής εκτύπωσης και εξαγωγή φύλλου Excel σε PNG σε C#
url: /el/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός περιοχής εκτύπωσης και εξαγωγή φύλλου Excel σε PNG με C#

Αν χρειάζεται να **ορίσετε περιοχή εκτύπωσης** πριν εξάγετε ένα φύλλο Excel σε PNG, αυτός ο οδηγός σας δείχνει πώς. Θα δείτε ένα πλήρες παράδειγμα C# που διαμορφώνει τις επιλογές εξαγωγής εικόνας, προσαρμόζει την περιοχή εκτύπωσης του φύλλου εργασίας και αποθηκεύει το αποτέλεσμα ως εικόνα.

Η εξαγωγή ενός φύλλου Excel σε PNG είναι συχνή απαίτηση όταν θέλετε να ενσωματώσετε μια λήψη του φύλλου εργασίας σε αναφορά, email ή ιστοσελίδα. Ο παρακάτω κώδικας λειτουργεί με οποιοδήποτε βιβλίο εργασίας που περιέχει έναν πίνακα Pivot, αλλά η τεχνική ισχύει και για κανονικές περιοχές δεδομένων. Δεν απαιτούνται εξωτερικά εργαλεία—μόνο η βιβλιοθήκη Aspose.Cells for .NET.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (το δείγμα στοχεύει στο .NET 6, αλλά οποιαδήποτε πρόσφατη έκδοση .NET λειτουργεί)
- Aspose.Cells for .NET (εγκατάσταση μέσω NuGet: `Install-Package Aspose.Cells`)
- Βασική εξοικείωση με C# και έννοιες του Excel όπως φύλλα εργασίας και περιοχές εκτύπωσης

## Βήμα 1: Διαμόρφωση επιλογών εξαγωγής εικόνας

Το πρώτο που κάνετε είναι να δημιουργήσετε μια παρουσία της κλάσης `ImageOrPrintOptions`. Αυτό το αντικείμενο λέει στο Aspose.Cells πώς να αποδώσει το φύλλο ως εικόνα.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Γιατί είναι σημαντικό:** `ImageOrPrintOptions` ελέγχει τη μορφή εξόδου, την ανάλυση και άλλες λεπτομέρειες απόδοσης. Η χρήση PNG εξασφαλίζει απώλεια‑από‑ποιότητας, κάτι που είναι ιδανικό για αναφορές που απαιτούν καθαρό κείμενο και γραφικά.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας και πρόσβαση στο επιθυμητό φύλλο εργασίας

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Γιατί είναι σημαντικό:** Πρέπει να εργαστείτε με ένα συγκεκριμένο αντικείμενο `Worksheet` επειδή η περιοχή εκτύπωσης είναι ρύθμιση επιπέδου φύλλου.

## Βήμα 3: Προσδιορισμός της περιοχής που θέλετε να εκτυπώσετε

Σε πολλές περιπτώσεις τα δεδομένα που σας ενδιαφέρουν βρίσκονται μέσα σε έναν πίνακα Pivot. Ο παρακάτω κώδικας εξάγει την περιοχή δεδομένων του πρώτου πίνακα Pivot στο φύλλο.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Αν το φύλλο εργασίας σας δεν περιέχει πίνακα Pivot, μπορείτε να αντικαταστήσετε το `pivotDataRange` με οποιοδήποτε `CellArea` δημιουργήσετε χειροκίνητα, π.χ.:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Βήμα 4: **Ορισμός περιοχής εκτύπωσης** ώστε να ταιριάζει με την επιλεγμένη περιοχή

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Γιατί είναι σημαντικό:** Η περιοχή εκτύπωσης λέει στο Excel (και στο Aspose.Cells) ποιες κελιά να συμπεριληφθούν κατά την απόδοση του φύλλου ως εικόνα. Με την ευθυγράμμιση της περιοχής εκτύπωσης με την περιοχή δεδομένων του Pivot, αποφεύγετε κενά περιθώρια και εξασφαλίζετε ότι το εξαγόμενο PNG περιέχει μόνο τα σχετικά δεδομένα.

## Βήμα 5: Εξαγωγή του φύλλου εργασίας σε εικόνα PNG

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Γιατί είναι σημαντικό:** `worksheet.ToImage` σέβεται την προηγουμένως ορισμένη περιοχή εκτύπωσης, έτσι το αρχείο PNG περιέχει ακριβώς τα κελιά που ορίσατε. Η ανάθεση της εικόνας σε σχήμα εικόνας (picture shape) σας επιτρέπει να την ενσωματώσετε ξανά στο βιβλίο εργασίας εάν χρειαστεί, ενώ η αποθήκευση στο δίσκο σας δίνει ένα αυτόνομο αρχείο.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα βήματα δημιουργείται ένα αυτόνομο πρόγραμμα που μπορείτε να εκτελέσετε αμέσως.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του προγράμματος δημιουργεί το `C:\Temp\WorksheetExport.png`. Το άνοιγμα του αρχείου εμφανίζει μια καθαρή εικόνα PNG που περιέχει μόνο τα κελιά που ορίστηκαν από την **ορισμένη περιοχή εκτύπωσης** (τα δεδομένα του πίνακα Pivot σε αυτό το παράδειγμα). Η εικόνα μπορεί να ενσωματωθεί σε έγγραφα Word, διαφάνειες PowerPoint ή ιστοσελίδες χωρίς πρόσθετα βήματα μετατροπής.

## Διαχείριση πολλαπλών φύλλων εργασίας ή πινάκων Pivot

- **Πολλαπλά φύλλα εργασίας:** Επανάληψη μέσω `wb.Worksheets` και επανάληψη των βημάτων 3‑5 για κάθε φύλλο που χρειάζεται να εξάγετε.
- **Πολλαπλοί πίνακες Pivot:** Επιλέξτε το κατάλληλο `PivotTables[index]` ή επαναλάβετε μέσω `worksheet.PivotTables` για να εξάγετε κάθε πίνακα ξεχωριστά.
- **Χωρίς πίνακα Pivot:** Δημιουργήστε ένα `CellArea` χειροκίνητα (δείτε το σχόλιο στο Βήμα 3) και αντιστοιχίστε το στο `PrintArea`.

## Πρακτικές συμβουλές (E‑E‑A‑T)

- **Συμβουλή επαγγελματία:** Ορίστε `HorizontalResolution` και `VerticalResolution` στα 300 DPI για PNG έτοιμα για εκτύπωση· χαμηλότερες τιμές μειώνουν το μέγεθος του αρχείου για χρήση στο web.
- **Προσοχή σε κενά σχήματα εικόνας:** Αν το φύλλο εργασίας δεν έχει σχήματα εικόνας, προσθέστε ένα πριν αντιστοιχίσετε την εικόνα:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Απόδοση:** Η επαναχρησιμοποίηση μιας μόνο παρουσίας `ImageOrPrintOptions` για πολλαπλά φύλλα εργασίας αποφεύγει περιττές κατανομές μνήμης.
- **Συμβατότητα:** Το Aspose.Cells 23.9+ υποστηρίζει πλήρως .NET 6 και νεότερες εκδόσεις· παλαιότερες εκδόσεις μπορεί να απαιτούν προσαρμογές στα ονόματα του API.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **ορίσετε περιοχή εκτύπωσης** και να εξάγετε ένα Excel

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to export Excel to PNG – full step‑by‑step guide](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [How to export excel range as image with C# and Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sheet to png – Export a Pivot Table as PNG in C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}