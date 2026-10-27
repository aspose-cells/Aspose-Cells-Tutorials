---
category: general
date: 2026-07-26
description: Πώς να εξάγετε σχήματα από ένα φύλλο εργασίας του Excel στο PowerPoint
  σε λίγα μόνο βήματα – ένας γρήγορος οδηγός εξαγωγής Excel σε PPTX για προγραμματιστές.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: el
lastmod: 2026-07-26
og_description: Πώς να εξάγετε σχήματα από το Excel στο PowerPoint βήμα‑βήμα. Ακολουθήστε
  αυτό το σεμινάριο εξαγωγής Excel σε PPTX και δείτε τα φύλλα εργασίας σας να μετατρέπονται
  σε επεξεργάσιμες διαφάνειες.
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: Πώς να εξάγετε σχήματα από το Excel στο PowerPoint – Γρήγορα & Εύκολα
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: Πώς να εξάγετε σχήματα από το Excel στο PowerPoint – Πλήρης οδηγός
url: /el/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Σχήματα από το Excel στο PowerPoint – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε σχήματα** από ένα αρχείο Excel και να τα διατηρήσετε επεξεργάσιμα σε μια παρουσίαση PowerPoint; Δεν είστε ο μόνος. Είτε δημιουργείτε μια αλυσίδα αναφορών είτε χρειάζεστε απλώς έναν γρήγορο τρόπο να μετατρέψετε ένα υπολογιστικό φύλλο σε παρουσίαση, η δυνατότητα **convert worksheet to PowerPoint** χωρίς να χάσετε την επεξεργασιμότητα των σχημάτων μπορεί να σας εξοικονομήσει ώρες χειροκίνητης εργασίας.

Σε αυτό το **excel to powerpoint tutorial** θα περάσουμε από ένα πλήρως λειτουργικό παράδειγμα C# που φορτώνει ένα βιβλίο εργασίας, ρυθμίζει τις σωστές επιλογές εξαγωγής και γράφει ένα αρχείο PPTX όπου τα πλαίσια κειμένου και άλλα αντικείμενα σχεδίασης παραμένουν επεξεργάσιμα. Χωρίς ασαφείς αναφορές—μόνο ο κώδικας που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε σήμερα.

## Τι Θα Μάθετε

- Τα ακριβή βήματα για **export excel to pptx** διατηρώντας την επεξεργασιμότητα των σχημάτων.  
- Πώς η βιβλιοθήκη `Aspose.Cells` και το `PptxSaveOptions` ελέγχουν τη συμπεριφορά της εξαγωγής.  
- Συμβουλές για τη διαχείριση πολλαπλών φύλλων εργασίας, ελλιπών αρχείων και προσαρμοσμένων ρυθμίσεων σχήματος.  
- Ένα πλήρες, εκτελέσιμο πρόγραμμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.  

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+).  
- Ένα έγκυρο license για **Aspose.Cells for .NET** (η δωρεάν δοκιμή λειτουργεί για δοκιμές).  
- Ένα βιβλίο εργασίας Excel (π.χ., `ShapesDemo.xlsx`) που περιέχει τουλάχιστον ένα πλαίσιο κειμένου ή σχήμα.  
- Ένα περιβάλλον ανάπτυξης—Visual Studio, Rider ή VS Code αρκεί.  

Αν τα έχετε, ας βουτήξουμε.

## Βήμα 1: Φόρτωση του Workbook – Το Αρχικό Σημείο για Πώς να Εξάγετε Σχήματα  

Πρώτα πρέπει να ανοίξουμε το αρχείο Excel που περιέχει τα σχήματα που θέλουμε να διατηρήσουμε επεξεργάσιμα.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**Γιατί είναι σημαντικό:**  
Το αντικείμενο `Workbook` είναι η πύλη σε κάθε κελί, γράφημα και αντικείμενο σχεδίασης μέσα στο αρχείο. Με το να πάρουμε το πρώτο φύλλο εργασίας (`Worksheets[0]`) εξασφαλίζουμε ότι δουλεύουμε με ένα γνωστό φύλλο, αλλά μπορείτε να αντικαταστήσετε το δείκτη με ένα όνομα (`workbook.Worksheets["Sheet2"]`) αν χρειάζεστε συγκεκριμένο καρτέλα.

> **Pro tip:** Τυλίξτε την κλήση φόρτωσης σε ένα μπλοκ `try / catch` για να δώσετε ένα φιλικό σφάλμα αν η διαδρομή του αρχείου είναι λανθασμένη.

## Βήμα 2: Ρύθμιση Επιλογών Εξαγωγής PPTX – Ο Πυρήνας του Πώς να Εξάγετε Σχήματα  

Τώρα λέμε στο Aspose.Cells να διατηρήσει τα σχήματα επεξεργάσιμα στο παραγόμενο PPTX.

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**Γιατί αυτές οι σημαίες;**  
- `ExportEditableTextBoxes` μετατρέπει τα πλαίσια κειμένου του Excel σε placeholders κειμένου του PowerPoint που μπορείτε να κάνετε διπλό‑κλικ και να επεξεργαστείτε.  
- `ExportEditableShapes` κάνει το ίδιο για σχήματα όπως βέλη, ορθογώνια και SmartArt. Χωρίς αυτά, τα αντικείμενα γίνονται στατικές εικόνες, αντιστρέφοντας τον σκοπό μιας ροής εργασίας **convert worksheet to powerpoint**.  

Μπορείτε επίσης να τροποποιήσετε το `PptxSaveOptions` για να ελέγξετε το μέγεθος της διαφάνειας, το θέμα ή το αν θα ενσωματώσετε γραμματοσειρές—χρήσιμο όταν η παρουσίασή σας πρέπει να ταιριάζει με την εταιρική ταυτότητα.

## Βήμα 3: Αποθήκευση του Φύλλου Εργασίας ως PPTX – Το Τελικό Κομμάτι της Εξαγωγής Excel Workbook PowerPoint  

Με τις επιλογές ορισμένες, η αποθήκευση είναι απλή.

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**Τι συμβαίνει στο παρασκήνιο;**  
Το Aspose.Cells διατρέχει κάθε αντικείμενο σχεδίασης στο φύλλο, το αντιστοιχίζει στην αντίστοιχη κλάση σχήματος του PowerPoint και γράφει το XML που διαβάζει το PowerPoint. Επειδή ενεργοποιήσαμε τις επεξεργάσιμες σημαίες, το XML σηματοδοτεί κάθε σχήμα ως `Shape` αντί για `Picture`, έτσι το PowerPoint το αντιμετωπίζει ως ζωντανό αντικείμενο.

## Βήμα 4: Επιβεβαίωση της Εξαγωγής – Γρήγορη Ανατροφοδότηση για τον Χρήστη  

Ένα μικρό μήνυμα κονσόλας σας ενημερώνει ότι η διαδικασία ολοκληρώθηκε επιτυχώς.

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

Αν εκτελέσετε το πρόγραμμα και δείτε το μήνυμα, ανοίξτε το `ShapesEditable.pptx` στο PowerPoint. Κάντε κλικ σε οποιοδήποτε πλαίσιο κειμένου—θα πρέπει να μπορείτε να επεξεργαστείτε το κείμενο απευθείας, και σύροντας ένα σχήμα θα το μετακινεί όπως ένα εγγενές αντικείμενο PowerPoint.

## Βήμα 5: Διαχείριση Σχετικών Σε Σενάρια Πραγματικού Κόσμου  

Παρακάτω είναι κοινές παραλλαγές που μπορεί να συναντήσετε ενώ εργάζεστε σε ένα **excel to powerpoint tutorial**.

### Πολλαπλά Φύλλα Εργασίας

Αν χρειάζεστε να εξάγετε πολλά φύλλα σε ένα μόνο PPTX, επαναλάβετε μέσω `workbook.Worksheets` και καλέστε `worksheet.Save` με τις ίδιες `pptxOptions`. Το Aspose.Cells θα προσθέσει αυτόματα μια νέα διαφάνεια για κάθε φύλλο.

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### Προσαρμοσμένες Διατάξεις Διαφάνειας

Μπορείτε να καθορίσετε `pptxOptions.SlideSize` (π.χ., `SlideSizeType.Widescreen`) για να ταιριάζει με τις διαστάσεις της εταιρικής σας παρουσίασης.

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### Ελλιπή Αρχεία ή Δικαιώματα

Τυλίξτε ολόκληρη τη μέθοδο `Main` σε ένα μπλοκ `try`:

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

Αυτό καθιστά τη διαδικασία **export excel workbook powerpoint** ανθεκτική για παραγωγικές γραμμές εργασίας.

## Πλήρες Παράδειγμα Λειτουργίας

Ακολουθεί το πλήρες πρόγραμμα που μπορείτε να μεταγλωττίσετε αμέσως. Αποθηκεύστε το ως `ExportEditableShapes.cs`, προσαρμόστε τις διαδρομές αρχείων και εκτελέστε `dotnet run`.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

**Αναμενόμενη έξοδος** όταν εκτελέσετε το πρόγραμμα:

```
Exported worksheet with editable shapes.
```

Ανοίξτε το παραγόμενο `ShapesEditable.pptx` και θα δείτε κάθε σχήμα Excel ως πλήρως επεξεργάσιμο αντικείμενο PowerPoint—ακριβώς αυτό που ζητήσατε όταν ψάχνατε **how to export shapes**.

## Συχνές Ερωτήσεις

- **Λειτουργεί αυτό με παλαιότερες μορφές Excel (.xls);**  
  Ναι. Το `Workbook` μπορεί να ανοίξει αρχεία `.xls`, `.xlsx` και ακόμη CSV. Η εξαγωγή σχήματος λειτουργεί με τον ίδιο τρόπο.

- **Τι γίνεται αν χρειάζεται να διατηρήσω τα γραφήματα επεξεργάσιμα;**  
  Τα γραφήματα εξάγονται ήδη ως εγγενή γραφήματα PowerPoint· δεν χρειάζονται επιπλέον σημαίες.

- **Μπορώ να εξάγω σε PDF αντί για PPTX;**  
  Απόλυτα—απλώς αντικαταστήστε το `SaveFormat.Pptx` με `SaveFormat.Pdf` και παραλείψτε το `PptxSaveOptions`.

## Συμπέρασμα

Τώρα έχετε μια ισχυρή, ολοκληρωμένη λύση για **how to export shapes** από το Excel σε μια επεξεργάσιμη παρουσίαση PowerPoint. Χρησιμοποιώντας το `PptxSaveOptions` του `Aspose.Cells`, διατηρείτε κάθε πλαίσιο κειμένου και αντικείμενο σχεδίασης, μετατρέποντας ένα στατικό υπολογιστικό φύλλο σε μια δυναμική παρουσίαση με ελάχιστη προσπάθεια.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να προσθέσετε προσαρμοσμένα master slides, να εισάγετε εικόνες προγραμματιστικά ή να ενσωματώσετε αυτήν την εξαγωγή σε μια γραμμή CI/CD που δημιουργεί αυτόματα εβδομαδιαίες παρουσιάσεις πωλήσεων. Ο κόσμος του **export excel workbook powerpoint** είναι ανοιχτός—εξερευνήστε το!

--- 

*Αν βρήκατε αυτό το **excel to powerpoint tutorial** χρήσιμο, δώστε του ένα αστέρι στο GitHub ή μοιραστείτε το με έναν συνάδελφο που εξακολουθεί να αντιγράφει‑και‑επικολλά υπολογιστικά φύλλα σε διαφάνειες. Καλή προγραμματιστική!*

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Εξάγετε ένα Φύλλο Εργασίας Excel σε PNG Χρησιμοποιώντας Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Πώς να Εξάγετε Κελιά Excel ως Εικόνες Χρησιμοποιώντας Aspose.Cells για Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [Πώς να Εξάγετε Γραφήματα Excel ως SVG Χρησιμοποιώντας Aspose.Cells Java για Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}