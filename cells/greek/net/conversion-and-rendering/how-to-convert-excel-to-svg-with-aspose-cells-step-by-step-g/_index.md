---
category: general
date: 2026-10-01
description: Μάθετε πώς να μετατρέψετε το Excel σε SVG και να αποθηκεύσετε το αρχείο
  Excel ως SVG χρησιμοποιώντας το Aspose.Cells. Ακολουθήστε αυτό το πλήρες σεμινάριο
  για να εξάγετε τα φύλλα εργασίας του Excel ως εικόνες SVG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to svg
- save excel file as svg
- how to export excel to svg
- export excel worksheet as svg
language: el
lastmod: 2026-10-01
og_description: Μετατροπή Excel σε SVG χρησιμοποιώντας το Aspose.Cells. Αυτό το σεμινάριο
  εξηγεί πώς να εξάγετε φύλλα εργασίας Excel ως εικόνες SVG, καλύπτοντας τη ρύθμιση,
  τον κώδικα και τις ειδικές περιπτώσεις.
og_image_alt: Diagram illustrating the convert excel to svg workflow
og_title: Μετατροπή Excel σε SVG με το Aspose.Cells – πλήρης οδηγός προγραμματισμού
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to convert Excel to SVG and save Excel file as SVG using
    Aspose.Cells. Follow this complete tutorial to export Excel worksheets as SVG
    images.
  headline: How to convert Excel to SVG with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert Excel to SVG and save Excel file as SVG using
    Aspose.Cells. Follow this complete tutorial to export Excel worksheets as SVG
    images.
  name: How to convert Excel to SVG with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Exporting multiple worksheets at once
    text: 'When a workbook contains several sheets, you can let Aspose.Cells generate
      a separate SVG for each sheet automatically:'
  - name: Controlling SVG dimensions
    text: 'SVG files are vector‑based, but you can still influence the viewport size:'
  - name: Handling formulas and calculated values
    text: 'By default, Aspose.Cells evaluates formulas before rendering. If you want
      to export raw formulas as text, set:'
  - name: Performance tips
    text: '- **Reuse `ImageOrPrintOptions`**: Create the options once and reuse them
      for multiple workbooks to avoid unnecessary allocations. - **Stream output**:
      If you are building a web API, write the SVG directly to a `MemoryStream` and
      return it as a file result instead of saving to disk.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- SVG export
title: Πώς να μετατρέψετε το Excel σε SVG με το Aspose.Cells – οδηγός βήμα‑προς‑βήμα
url: /el/net/conversion-and-rendering/how-to-convert-excel-to-svg-with-aspose-cells-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε το Excel σε SVG με το Aspose.Cells – βήμα‑βήμα οδηγός

Αν χρειάζεστε **convert Excel to SVG**, αυτός ο οδηγός σας δείχνει ακριβώς πώς να εξάγετε ένα φύλλο εργασίας Excel ως εικόνα SVG χρησιμοποιώντας το Aspose.Cells. Θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα που αποθηκεύει ένα αρχείο Excel ως SVG και θα μάθετε γιατί κάθε ρύθμιση είναι σημαντική.

Η εξαγωγή λογιστικών φύλλων ως διανυσματικά γραφικά (SVG) είναι χρήσιμη όταν θέλετε καθαρή απόδοση σε ιστοσελίδες, αναφορές ή τεκμηρίωση χωρίς απώλεια ποιότητας. Τα παρακάτω βήματα καλύπτουν τα πάντα, από την εγκατάσταση της βιβλιοθήκης μέχρι τη διαχείριση πολλαπλών φύλλων εργασίας και τις κοινές παγίδες.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7.2+)
- Ένα έγκυρο άδεια Aspose.Cells ή ένα δωρεάν κλειδί αξιολόγησης
- Ένα βιβλίο εργασίας Excel (`input.xlsx`) που θέλετε να μετατρέψετε
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή C# της επιλογής σας

Δεν απαιτούνται πρόσθετα πακέτα NuGet πέρα από `Aspose.Cells`.

## Βήμα 1: Εγκατάσταση Aspose.Cells

Η τυπική προσέγγιση είναι να προσθέσετε το πακέτο Aspose.Cells μέσω NuGet. Ανοίξτε ένα τερματικό στο φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.Cells --version 24.10
```

Αυτή η εντολή κατεβάζει την πιο πρόσφατη σταθερή έκδοση (24.10 τη στιγμή της συγγραφής) και ενημερώνει το αρχείο του έργου σας. Η χρήση της πιο πρόσφατης έκδοσης εξασφαλίζει συμβατότητα με τις νεότερες δυνατότητες του Excel και βελτιώσεις του SVG.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας Excel

Η φόρτωση του βιβλίου εργασίας είναι η πρώτη συγκεκριμένη ενέργεια στην **convert excel to svg** αλυσίδα. Η κλάση `Workbook` αντιπροσωπεύει ολόκληρο το αρχείο Excel και σας δίνει πρόσβαση στα φύλλα εργασίας, τους τύπους και τη μορφοποίηση.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the source workbook
var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Optional: verify that the workbook loaded correctly
Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");
```

**Γιατί αυτό είναι σημαντικό:**  
Αν το αρχείο δεν μπορεί να ανοιχθεί (π.χ. λανθασμένη διαδρομή ή μη υποστηριζόμενη μορφή), το Aspose.Cells ρίχνει μια περιγραφική εξαίρεση που μπορείτε να πιάσετε και να καταγράψετε. Η έγκαιρη επικύρωση του αριθμού των φύλλων εργασίας σας βοηθά να αποφασίσετε αν θα εξάγετε ένα μόνο φύλλο ή ολόκληρο το βιβλίο εργασίας.

## Βήμα 3: Διαμόρφωση επιλογών απόδοσης SVG

Για **save excel file as svg**, πρέπει να δημιουργήσετε μια παρουσία `ImageOrPrintOptions` και να ορίσετε το `SaveFormat` σε `SaveFormat.Svg`. Μπορείτε επίσης να ρυθμίσετε την ποιότητα εικόνας, την κλιμάκωση και αν θα ενσωματώσετε τις γραμματοσειρές.

```csharp
// Set up rendering options for SVG output
var imageOptions = new ImageOrPrintOptions
{
    // Export format must be SVG
    SaveFormat = SaveFormat.Svg,

    // Preserve the original aspect ratio
    OnePagePerSheet = true,

    // Optional: increase resolution for sharper vectors
    // (SVG is resolution‑independent, but this affects rasterized elements)
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Εξήγηση:**  
`OnePagePerSheet = true` αναγκάζει κάθε φύλλο εργασίας να αποδοθεί σε μία σελίδα SVG, κάτι που συνήθως θέλετε για ενσωμάτωση στο web. Η αλλαγή της ανάλυσης επηρεάζει το πώς αποδίδονται οι ενσωματωμένες ραστερ εικόνες (π.χ. εικόνες μέσα σε κελιά) μέσα στο SVG.

## Βήμα 4: Αποθήκευση του βιβλίου εργασίας ως εικόνα SVG

Τώρα μπορείτε να **export excel worksheet as svg** καλώντας το `Workbook.Save` με τη διαδρομή προορισμού και τις επιλογές που μόλις διαμορφώσατε.

```csharp
// Define the output path
string outputPath = @"YOUR_DIRECTORY\output.svg";

// Save the workbook (or a specific worksheet) as SVG
workbook.Save(outputPath, imageOptions);

Console.WriteLine($"Workbook exported to SVG at: {outputPath}");
```

Αν χρειάζεστε εξαγωγή μόνο ενός φύλλου αντί ολόκληρου του βιβλίου εργασίας, ανακτήστε το φύλλο και χρησιμοποιήστε το `SheetRender`:

```csharp
// Export only the first worksheet
var sheet = workbook.Worksheets[0];
var sheetRender = new SheetRender(sheet, imageOptions);
sheetRender.ToImage(0, outputPath); // 0 = first page
```

**Γιατί αυτό λειτουργεί:**  
`Workbook.Save` επαναλαμβάνει όλα τα φύλλα εργασίας όταν το `OnePagePerSheet` είναι true, δημιουργώντας ένα αρχείο SVG ανά φύλλο εάν η διαδρομή εξόδου περιέχει ένα σύμβολο κράτησης θέσης (π.χ. `output_{0}.svg`). Η χρήση του `SheetRender` σας δίνει ακριβή έλεγχο για το ποιο(α) φύλλο(α) εξάγετε.

## Βήμα 5: Επαλήθευση του αποτελέσματος SVG

Μετά την ολοκλήρωση της μετατροπής, ανοίξτε το παραγόμενο αρχείο `.svg` σε έναν περιηγητή ή έναν επεξεργαστή SVG (π.χ. Inkscape). Θα πρέπει να δείτε κείμενο, περιγράμματα κελιών και τυχόν ενσωματωμένες εικόνες ως διανυσματικά στοιχεία.

```bash
# On macOS or Linux you can open the file directly:
open YOUR_DIRECTORY/output.svg
```

Αν το SVG φαίνεται κενό ή λείπουν μορφοποιήσεις, ελέγξτε ξανά ότι:

1. Το βιβλίο εργασίας περιέχει πραγματικά δεδομένα στο επιλεγμένο φύλλο.  
2. Δεν υπάρχουν κρυφές γραμμές/στήλες που να κρύβουν το περιεχόμενο (χρησιμοποιήστε `sheet.IsVisible`).  
3. Οι γραμματοσειρές που χρησιμοποιούνται στο βιβλίο εργασίας είναι εγκατεστημένες στο μηχάνημα· διαφορετικά το Aspose.Cells τις αντικαθιστά, κάτι που μπορεί να επηρεάσει την εμφάνιση.

## Προχωρημένες παρατηρήσεις

### Εξαγωγή πολλαπλών φύλλων εργασίας ταυτόχρονα

Όταν ένα βιβλίο εργασίας περιέχει πολλά φύλλα, μπορείτε να αφήσετε το Aspose.Cells να δημιουργήσει αυτόματα ένα ξεχωριστό SVG για κάθε φύλλο:

```csharp
// Use a placeholder {0} for sheet index
string multiOutput = @"YOUR_DIRECTORY\output_{0}.svg";
workbook.Save(multiOutput, imageOptions);
```

Η βιβλιοθήκη αντικαθιστά το `{0}` με τον δείκτη του φύλλου (ξεκινώντας από 0). Αυτό είναι χρήσιμο για μαζική επεξεργασία μεγάλων αναφορών.

### Έλεγχος διαστάσεων SVG

Τα αρχεία SVG είναι διανυσματικά, αλλά μπορείτε ακόμη να επηρεάσετε το μέγεθος του viewport:

```csharp
imageOptions.PageWidth = 800;   // width in pixels (converted to SVG points)
imageOptions.PageHeight = 600;  // height in pixels
```

Ο καθορισμός ρητών διαστάσεων εξασφαλίζει συνεπή διάταξη όταν ενσωματώνετε το SVG σε HTML containers.

### Διαχείριση τύπων και υπολογισμένων τιμών

Από προεπιλογή, το Aspose.Cells αξιολογεί τους τύπους πριν την απόδοση. Αν θέλετε να εξάγετε ακατέργαστους τύπους ως κείμενο, ορίστε:

```csharp
imageOptions.ExportFormulasAsString = true;
```

Αυτή η επιλογή είναι χρήσιμη για τεκμηρίωση όπου χρειάζεται να εμφανίσετε τον πραγματικό τύπο του Excel αντί για το υπολογισμένο αποτέλεσμα.

### Συμβουλές απόδοσης

- **Επαναχρησιμοποίηση `ImageOrPrintOptions`**: Δημιουργήστε τις επιλογές μία φορά και επαναχρησιμοποιήστε τις για πολλαπλά βιβλία εργασίας ώστε να αποφύγετε περιττές κατανομές μνήμης.  
- **Ροή εξόδου**: Εάν δημιουργείτε ένα web API, γράψτε το SVG απευθείας σε ένα `MemoryStream` και επιστρέψτε το ως αποτέλεσμα αρχείου αντί να το αποθηκεύσετε στο δίσκο.

```csharp
using (var stream = new MemoryStream())
{
    workbook.Save(stream, imageOptions);
    // Reset position before reading
    stream.Position = 0;
    // Return stream to caller (e.g., ASP.NET Core FileResult)
}
```

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Συμπτωμα | Αιτία | Διόρθωση |
|----------|-------|----------|
| Κενό αρχείο SVG | Το πηγαίο βιβλίο εργασίας έχει κρυφές γραμμές/στήλες ή φύλλο μηδενικού μεγέθους | Αποκρύψτε τις γραμμές/στήλες ή ορίστε `sheet.IsVisible = true` |
| Λείπουν γραμματοσειρές | Η γραμματοσειρά δεν είναι εγκατεστημένη στον διακομιστή | Εγκαταστήστε τη απαιτούμενη γραμματοσειρά ή ενσωματώστε την χρησιμοποιώντας `imageOptions.EmbeddedFonts = true` |
| Πολλαπλά αρχεία SVG με απρόσμενα ονόματα | Η διαδρομή εξόδου δεν περιέχει το σύμβολο κράτησης θέσης `{0}` | Χρησιμοποιήστε `output_{0}.svg` για να δημιουργήσετε αρχεία ανά φύλλο |
| Αργή μετατροπή για μεγάλα βιβλία εργασίας | Απόδοση κάθε φύλλου ξεχωριστά χωρίς `OnePagePerSheet` | Ενεργοποιήστε το `OnePagePerSheet` ή επεξεργαστείτε τα φύλλα παράλληλα χρησιμοποιώντας `Task.Run` |

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει μια αυτόνομη εφαρμογή κονσόλας που δείχνει **how to export Excel to SVG** από την αρχή μέχρι το τέλος. Αντικαταστήστε το `YOUR_DIRECTORY` με έναν πραγματικό φάκελο στο μηχάνημά σας.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToSvgDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
            var workbook = new Workbook(workbookPath);
            Console.WriteLine($"Loaded {workbook.Worksheets.Count} worksheet(s).");

            // 2️⃣ Configure SVG options
            var svgOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Svg,
                OnePagePerSheet = true,
                HorizontalResolution = 300,
                VerticalResolution = 300,
                // Optional: set explicit dimensions
                // PageWidth = 800,
                // PageHeight = 600
            };

            // 3️⃣ Export each sheet as a separate SVG file
            string outputPattern = @"YOUR_DIRECTORY\output_{0}.svg";
            workbook.Save(outputPattern, svgOptions);
            Console.WriteLine("Export completed. SVG files created:");

            for (int i = 0; i < workbook.Worksheets.Count; i++)
            {
                Console.WriteLine($"\t{string.Format(outputPattern, i)}");
            }
        }
    }
}
```

**Αναμενόμενο αποτέλεσμα** (console):

```
Loaded 2 worksheet(s).
Export completed. SVG files created:
    YOUR_DIRECTORY\output_0.svg
    YOUR_DIRECTORY\output_1.svg
```

Ανοίξτε οποιοδήποτε από τα παραγόμενα αρχεία `.svg` σε έναν περιηγητή για να επαληθεύσετε ότι η μετατροπή ολοκληρώθηκε με επιτυχία.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **convert Excel to SVG** χρησιμοποιώντας το Aspose.Cells, από την εγκατάσταση της βιβλιοθήκης μέχρι τη διαχείριση πολλαπλών φύλλων εργασίας και τη λεπτομερή ρύθμιση των επιλογών απόδοσης. Ο οδηγός κάλυψε τη πλήρη ροή εργασίας για **save excel file as svg**, εξήγησε γιατί κάθε ρύθμιση είναι σημαντική και τόνισε ειδικές περιπτώσεις όπως κρυφές γραμμές, ενσωμάτωση γραμματοσειρών και ζητήματα απόδοσης.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

- **Πώς να εξάγετε Excel σε SVG** σε ένα web API (ροή του SVG απευθείας στον πελάτη)  
- Μετατροπή Excel σε άλλες μορφές διανυσματικών όπως PDF ή EMF  
- Χρήση Aspose.Slides για ενσωμάτωση του παραγόμενου SVG σε παρουσιάσεις PowerPoint  

Νιώστε ελεύθεροι να πειραματιστείτε με κλιμάκωση, προσαρμοσμένα στυλ ή συνδυασμό εξόδου SVG με HTML/CSS για διαδραστικές αναφορές. Καλή προγραμματιστική!

## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Μετατροπή Φύλλων Excel σε SVG χρησιμοποιώντας Aspose.Cells Java: Ένας Πλήρης Οδηγός](/cells/english/java/workbook-operations/convert-excel-to-svg-aspose-cells-java/)
- [Μετατροπή Excel σε SVG Χρησιμοποιώντας Aspose.Cells για .NET: Ένας Βήμα‑Βήμα Οδηγός](/cells/english/net/workbook-operations/convert-excel-to-svg-aspose-cells-net/)
- [Πώς να Μετατρέψετε Διαγράμματα Excel σε SVG Χρησιμοποιώντας Aspose.Cells σε Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}