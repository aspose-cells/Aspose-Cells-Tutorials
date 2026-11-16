---
category: general
date: 2026-11-16
description: Μάθετε πώς να αποθηκεύετε το Excel ως PowerPoint και να μετατρέπετε το
  Excel σε PowerPoint προγραμματιστικά. Αυτός ο οδηγός βήμα‑βήμα καλύπτει επίσης την
  εξαγωγή του Excel σε PPTX και την αποθήκευση ενός βιβλίου εργασίας ως PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: el
lastmod: 2026-11-16
og_description: Αποθηκεύστε το Excel ως PowerPoint χρησιμοποιώντας το Aspose.Cells.
  Ακολουθήστε αυτόν τον οδηγό για να μετατρέψετε το Excel σε PowerPoint, να εξάγετε
  το Excel σε PPTX και να αποθηκεύσετε το βιβλίο εργασίας ως PPTX σε λίγα λεπτά.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Αποθήκευση Excel ως PowerPoint – Πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Πώς να αποθηκεύσετε το Excel ως PowerPoint με Aspose.Cells σε C#
url: /el/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αποθηκεύσετε το Excel ως PowerPoint με το Aspose.Cells σε C#

Αν χρειάζεστε να **αποθηκεύσετε το Excel ως PowerPoint** προγραμματιστικά, αυτό το tutorial σας παρέχει μια πλήρη, έτοιμη‑για‑εκτέλεση λύση. Είτε δημιουργείτε μια μηχανή αναφορών είτε έναν αυτοματοποιημένο γεννήτρια διαφανειών, τα παρακάτω βήματα σας επιτρέπουν να μετατρέψετε ένα φύλλο εργασίας Excel σε μια επεξεργάσιμη διαφάνεια PPTX με λίγες μόνο γραμμές κώδικα.

Θα μάθετε πώς να **μετατρέψετε το Excel σε PowerPoint**, να εξάγετε το φύλλο σε αρχείο PPTX και να διατηρήσετε τα πλαίσια κειμένου και τα σχήματα επεξεργάσιμα – όλα χωρίς να αφήσετε το περιβάλλον .NET.

## Προαπαιτούμενα

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7.2+)
* Ένα έγκυρο άδεια Aspose.Cells (η δωρεάν δοκιμή λειτουργεί για αξιολόγηση)
* Visual Studio 2022 (ή οποιοδήποτε IDE C#)
* Ένα βιβλίο εργασίας Excel που περιέχει τα δεδομένα και τα σχήματα που θέλετε να εξάγετε

## Βήμα 1: Εγκατάσταση Aspose.Cells

Προσθέστε το πακέτο NuGet Aspose.Cells στο έργο σας:

```bash
dotnet add package Aspose.Cells
```

> **Συμβουλή:** Χρησιμοποιήστε τη σημαία `-v` για να στοχεύσετε μια συγκεκριμένη έκδοση, π.χ., `Aspose.Cells.24.5`.

## Βήμα 2: Φόρτωση του βιβλίου εργασίας που θέλετε να εξάγετε

Η πρώτη ενέργεια στη ροή εργασίας **αποθήκευσης Excel ως PowerPoint** είναι η φόρτωση του πηγαίου βιβλίου εργασίας.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Γιατί είναι σημαντικό:* Η φόρτωση του βιβλίου εργασίας σας δίνει πρόσβαση στα φύλλα εργασίας, τη ρύθμιση σελίδας και τα αντικείμενα σχεδίασης που θα μετατραπούν σε επεξεργάσιμα σχήματα PowerPoint.

## Βήμα 3: Διαμόρφωση επιλογών εξαγωγής για επεξεργάσιμη διαφάνεια PPTX

Για να **μετατρέψετε το Excel σε PowerPoint** διατηρώντας την επεξεργασιμότητα, πρέπει να ορίσετε μερικές ιδιότητες στο `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Επεξήγηση:*  
* `SaveFormat = SaveFormat.Pptx` λέει στο Aspose.Cells να δημιουργήσει αρχείο PowerPoint.  
* `ExportEditableText` και `ExportEditableShapes` εξασφαλίζουν ότι η προκύπτουσα διαφάνεια συμπεριφέρεται όπως μια εγγενής διαφάνεια PowerPoint—μπορείτε να κάνετε κλικ σε ένα πλαίσιο κειμένου ή σχήμα και να το επεξεργαστείτε απευθείας στο PowerPoint.

## Βήμα 4: Ορισμός περιοχής εξαγωγής και προσαρμογή σε μία διαφάνεια

Όταν **εξάγετε το Excel σε PPTX**, συνήθως θέλετε μια συγκεκριμένη περιοχή να εμφανιστεί στη διαφάνεια. Ο ορισμός της περιοχής εκτύπωσης και των επιλογών προσαρμογής εγγυάται ένα καθαρό, μονό‑διαφάνειας αποτέλεσμα.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Γιατί είναι σημαντικό:* Η `PrintArea` περιορίζει την εξαγωγή στα κελιά A1 έως G30, ενώ οι `FitToPagesTall` και `FitToPagesWide` συμπιέζουν τα πάντα σε μία διαφάνεια, αποτρέποντας ανεπιθύμητες επιπλέον σελίδες.

## Βήμα 5: Αποθήκευση του φύλλου εργασίας ως επεξεργάσιμο αρχείο PPTX

Τώρα μπορείτε τελικά να **αποθηκεύσετε το βιβλίο εργασίας ως PPTX** και να ολοκληρώσετε τη διαδικασία **αποθήκευσης Excel ως PowerPoint**.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

Μετά την εκτέλεση του προγράμματος, ανοίξτε το `EditableShapes.pptx` στο Microsoft PowerPoint. Θα δείτε μια διαφάνεια που αντικατοπτρίζει την επιλεγμένη περιοχή του Excel, και όλα τα πλαίσια κειμένου και σχήματα είναι πλήρως επεξεργάσιμα.

### Αναμενόμενο αποτέλεσμα

* Ένα αρχείο με όνομα `EditableShapes.pptx` τοποθετημένο στο `C:\Output\`.
* Μία διαφάνεια PowerPoint που περιέχει την περιοχή A1:G30.
* Πλαίσια κειμένου, γραφήματα και σχήματα που μπορείτε να κάνετε διπλό‑κλικ και να επεξεργαστείτε απευθείας στο PowerPoint.

## Πλήρης κώδικας (έτοιμος για αντιγραφή)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Συχνές ερωτήσεις και αντιμετώπιση ειδικών περιπτώσεων

| Question | Answer |
|----------|--------|
| **Τι γίνεται αν έχω πολλά φύλλα εργασίας;** | Κάντε επανάληψη μέσω `workbook.Worksheets` και επαναλάβετε τα βήματα 3‑5 για κάθε φύλλο, αλλάζοντας το όνομα του αρχείου εξόδου (π.χ., `Sheet1.pptx`, `Sheet2.pptx`). |
| **Μπορώ να εξάγω ολόκληρο το βιβλίο εργασίας σε μία ενιαία παρουσίαση PowerPoint;** | Ναι. Ορίστε `ExportAllSheets = true` στο `ImageOrPrintOptions`. Κάθε φύλλο εργασίας γίνεται ξεχωριστή διαφάνεια. |
| **Τα σχήματά μου εμφανίζονται ως εικόνες, όχι ως επεξεργάσιμα αντικείμενα.** | Βεβαιωθείτε ότι `ExportEditableShapes = true` και ότι χρησιμοποιείτε Aspose.Cells 24.5+ (παλαιότερες εκδόσεις δεν διαθέτουν αυτή τη δυνατότητα). |
| **Το παραγόμενο PPTX είναι πολύ μεγάλο.** | Μειώστε την περιοχή εκτύπωσης ή χαμηλώστε την ανάλυση εικόνας μέσω `exportOptions.ImageResolution`. |
| **Χρειάζομαι άδεια για παραγωγική χρήση;** | Μια επί πληρωμή άδεια αφαιρεί το υδατογράφημα αξιολόγησης και ξεκλειδώνει πλήρη απόδοση. Η δωρεάν δοκιμή λειτουργεί για δοκιμές. |

## Συμβουλές για αξιόπιστο κώδικα παραγωγής

* **Επικυρώστε τις διαδρομές αρχείων** πριν καλέσετε `Workbook` ή `Save` για να αποφύγετε `FileNotFoundException`.  
* **Τυλίξτε την εξαγωγή σε μπλοκ try/catch** για να διαχειριστείτε σφάλματα αδειοδότησης (`Aspose.Cells.LicenseException`).  
* **Αποδεσμεύστε το βιβλίο εργασίας** (`workbook.Dispose()`) όταν τελειώσετε για να ελευθερώσετε μη διαχειριζόμενους πόρους.  
* **Χρησιμοποιήστε async I/O** (`FileStream` με `await`) εάν εξάγετε πολλά μεγάλα φύλλα σε μια υπηρεσία web.

## Επόμενα βήματα

Τώρα που ξέρετε πώς να **αποθηκεύσετε το Excel ως PowerPoint**, μπορείτε να εξερευνήσετε συναφή θέματα:

* **Εξαγωγή Excel σε PPTX με προσαρμοσμένες διατάξεις διαφανειών** – προσαρμόστε το `SlideSize` και προσθέστε μια κύρια διαφάνεια.  
* **Μετατροπή διαφάνειας Excel σε PDF** – χρησιμοποιήστε `SaveFormat.Pdf` για εκτυπώσιμη έκδοση.  
* **Ομαδική μετατροπή φακέλου βιβλίων εργασίας** – συνδυάστε τον βρόχο που φαίνεται παραπάνω με `Directory.GetFiles`.  

Πειραματιστείτε με διαφορετικές περιοχές εκτύπωσης, επιλογές κλιμάκωσης και θέματα PowerPoint για να προσαρμόσετε το αποτέλεσμα στην επωνυμία του οργανισμού σας.

---

*Καλό προγραμματισμό! Αν αυτός ο οδηγός σας βοήθησε να **μετατρέψετε το Excel σε PowerPoint**, μη διστάσετε να τον μοιραστείτε με συναδέλφους ή να ανοίξετε ένα ζήτημα στο αποθετήριο Aspose.Cells στο GitHub για περαιτέρω βοήθεια.*

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αποθηκεύσετε το Excel ως PowerPoint χρησιμοποιώντας C# και Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Πώς να αποθηκεύσετε PPTX από Excel – Πλήρης Οδηγός για Εξαγωγή Φύλλου Excel σε PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Μετατροπή Excel σε PowerPoint – Πλήρης Οδηγός Βήμα‑βήμα](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}