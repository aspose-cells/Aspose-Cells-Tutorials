---
category: general
date: 2026-05-04
description: Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή ενός βιβλίου εργασίας
  Excel σε PDF χρησιμοποιώντας C#. Μάθετε πώς να αποθηκεύετε το βιβλίο εργασίας ως
  PDF με ενσωματωμένες τυπικές γραμματοσειρές και να αποφεύγετε προβλήματα έλλειψης
  γραμματοσειρών.
draft: false
keywords:
- how to embed fonts
- save workbook as pdf
- convert excel to pdf
- export spreadsheet to pdf
- how to save pdf
language: el
og_description: Πώς να ενσωματώσετε γραμματοσειρές κατά τη μετατροπή ενός βιβλίου
  εργασίας Excel σε PDF χρησιμοποιώντας C#. Αυτός ο οδηγός παρουσιάζει τον πλήρη κώδικα,
  εξηγεί γιατί η ενσωμάτωση είναι σημαντική και καλύπτει κοινά προβλήματα.
og_title: Πώς να ενσωματώσετε γραμματοσειρές σε PDF – Αποθήκευση βιβλίου εργασίας
  ως PDF σε C#
tags:
- C#
- Aspose.Cells
- PDF generation
title: Πώς να ενσωματώσετε γραμματοσειρές σε PDF – Αποθήκευση βιβλίου εργασίας ως
  PDF σε C#
url: /el/net/conversion-to-pdf/how-to-embed-fonts-in-pdf-save-workbook-as-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ενσωματώσετε Γραμματοσειρές σε PDF – Αποθήκευση Φύλλου Εργασίας ως PDF σε C#

Έχετε αναρωτηθεί ποτέ **πώς να ενσωματώσετε γραμματοσειρές** όταν εξάγετε ένα φύλλο Excel σε PDF; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν την ενοχλητική προειδοποίηση “missing font” μετά την αποθήκευση ενός φύλλου εργασίας ως PDF, μόνο για να διαπιστώσουν ότι το τελικό αρχείο φαίνεται λανθασμένο σε άλλο υπολογιστή.  

Το καλό νέο είναι ότι η λύση είναι αρκετά απλή με το Aspose.Cells for .NET. Σε αυτό το tutorial θα περάσουμε βήμα-βήμα τις ακριβείς ενέργειες για **αποθήκευση φύλλου εργασίας ως PDF** με ενσωματωμένες τυπικές γραμματοσειρές, και θα αγγίξουμε επίσης **convert excel to pdf**, **export spreadsheet to pdf**, καθώς και την ερώτηση **how to save pdf** με τις σωστές επιλογές. Στο τέλος θα έχετε ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο C#.

## Προαπαιτούμενα

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε:

* .NET 6 ή νεότερο (ο κώδικας λειτουργεί επίσης σε .NET Framework 4.7+)  
* Ένα έγκυρο license του Aspose.Cells for .NET (η δωρεάν δοκιμή λειτουργεί, αλλά ένα license αφαιρεί τα υδατογραφήματα αξιολόγησης)  
* Visual Studio 2022 ή οποιοδήποτε IDE προτιμάτε  
* Βασική κατανόηση της σύνταξης C# – αν μπορείτε να γράψετε “Hello World”, είστε έτοιμοι  

Αν κάποιο από αυτά σας είναι άγνωστο, κάντε ένα διάλειμμα και φροντίστε να το αποκτήσετε· το υπόλοιπο του οδηγού υποθέτει ότι είναι ήδη στη θέση τους.

## Βήμα 1: Προσθήκη του Πακέτου NuGet Aspose.Cells

Πρώτα, χρειάζεστε τη βιβλιοθήκη που επικοινωνεί με τα αρχεία Excel. Ανοίξτε το NuGet console του έργου σας και εκτελέστε:

```powershell
Install-Package Aspose.Cells
```

Αυτή η εντολή προσθέτει όλα όσα χρειάζεστε, συμπεριλαμβανομένων των κλάσεων `Workbook` και `PdfSaveOptions` που θα χρησιμοποιήσουμε αργότερα.  

*Συμβουλή:* Αν χρησιμοποιείτε pipeline CI/CD, κλειδώστε την έκδοση του πακέτου (π.χ., `Aspose.Cells -Version 24.9`) για να αποφύγετε απρόσμενες αλλαγές που σπάζουν τον κώδικα.

## Βήμα 2: Δημιουργία ή Φόρτωση Φύλλου Εργασίας

Τώρα είτε δημιουργούμε ένα ολοκαίνουργιο φύλλο εργασίας είτε φορτώνουμε ένα υπάρχον `.xlsx`. Για επίδειξη, ας δημιουργήσουμε ένα απλό φύλλο με μερικές γραμμές δεδομένων.

```csharp
using Aspose.Cells;

namespace PdfExportDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Create a fresh workbook (or replace with Workbook("input.xlsx"))
            Workbook workbook = new Workbook();

            // Populate the first worksheet with sample data
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Quantity");
            sheet.Cells["A2"].PutValue("Apples");
            sheet.Cells["B2"].PutValue(120);
            sheet.Cells["A3"].PutValue("Oranges");
            sheet.Cells["B3"].PutValue(85);
```

Μόλις δημιουργήσαμε μια μικρή λίστα αποθεμάτων. Αν έχετε ήδη αρχείο Excel, αντικαταστήστε την κλήση `new Workbook()` με `new Workbook("path/to/file.xlsx")` και παραλείψτε το μπλοκ εισαγωγής δεδομένων.

## Βήμα 3: Διαμόρφωση Επιλογών Αποθήκευσης PDF για Ενσωμάτωση Τυπικών Γραμματοσειρών

Εδώ συμβαίνει η μαγεία. Από προεπιλογή το Aspose.Cells μπορεί να αναφέρει συστημικές γραμματοσειρές αντί να τις ενσωματώνει, κάτι που οδηγεί στο πρόβλημα “font not found” σε άλλους υπολογιστές. Ορίζοντας το `EmbedStandardFonts` σε `true` αναγκάζει τον δημιουργό PDF να ενσωματώσει τις πιο κοινές γραμματοσειρές (Arial, Times New Roman κ.λπ.).

```csharp
            // Step 3: Set PDF options – embed standard fonts for portability
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                // Ensures that fonts like Arial, Times New Roman are embedded
                EmbedStandardFonts = true,

                // Optional: keep the original layout (no scaling)
                OnePagePerSheet = false
            };
```

**Γιατί να ενσωματώσετε γραμματοσειρές;** Σκεφτείτε ότι στέλνετε το PDF σε έναν συνεργάτη που έχει μόνο Helvetica. Χωρίς ενσωμάτωση, ο προβολέας του θα χρησιμοποιήσει υποκατάστατο, παραμορφώνοντας πίνακες και σπάζοντας το σχεδιασμό. Η ενσωμάτωση εγγυάται ότι το PDF θα φαίνεται ακριβώς το ίδιο παντού.

## Βήμα 4: Αποθήκευση του Φύλλου Εργασίας ως Αρχείο PDF

Τέλος, καλούμε τη μέθοδο `Save` και υποδεικνύουμε το φάκελο προορισμού. Η μέθοδος δέχεται τη διαδρομή του αρχείου και τις επιλογές που μόλις διαμορφώσαμε.

```csharp
            // Step 4: Save the workbook as a PDF with embedded fonts
            string outputPath = @"C:\Temp\InventoryReport.pdf";
            workbook.Save(outputPath, pdfOptions);

            // Let the user know we’re done
            Console.WriteLine($"PDF saved successfully to {outputPath}");
        }
    }
}
```

Τρέξτε το πρόγραμμα και θα βρείτε το `InventoryReport.pdf` στο `C:\Temp`. Ανοίξτε το σε οποιονδήποτε υπολογιστή — οι γραμματοσειρές παραμένουν, οι πίνακες ευθυγραμμίζονται, και η διάταξη ταιριάζει με το αρχικό φύλλο Excel.

> **Αναμενόμενο αποτέλεσμα:** Το PDF περιέχει τον πίνακα δύο στηλών ακριβώς όπως εμφανίζεται στο Excel, με την Arial (ή την προεπιλεγμένη συστημική γραμματοσειρά) ενσωματωμένη. Δεν εμφανίζονται προειδοποιήσεις “missing‑font” στο Adobe Reader ή σε οποιονδήποτε άλλο προβολέα.

## Βήμα 5: Επαλήθευση Ενσωμάτωσης Γραμματοσειρών (Προαιρετικό αλλά Χρήσιμο)

Αν θέλετε να ελέγξετε ξανά ότι οι γραμματοσειρές είναι πράγματι ενσωματωμένες, ανοίξτε το PDF στο Adobe Acrobat και μεταβείτε σε **File → Properties → Fonts**. Θα πρέπει να δείτε καταχωρήσεις όπως “ArialMT (Embedded Subset)”.

Εναλλακτικά, ένα δωρεάν εργαλείο όπως το **PDF‑Info** (`pdfinfo` σε Linux) μπορεί να εμφανίσει τις ενσωματωμένες γραμματοσειρές από τη γραμμή εντολών:

```bash
pdfinfo -meta InventoryReport.pdf | grep Font
```

Η εμφάνιση του “Embedded” δίπλα σε κάθε γραμματοσειρά που εμφανίζεται επιβεβαιώνει ότι έχετε κάνει τη σωστή δουλειά.

## Συνηθισμένες Περιπτώσεις & Πώς να τις Διαχειριστείτε

| Κατάσταση | Τι πρέπει να κάνετε |
|-----------|---------------------|
| **Προσαρμοσμένη εταιρική γραμματοσειρά** (π.χ., `MyCompanySans`) | Ορίστε `PdfSaveOptions.CustomFonts = new string[] { @"C:\Fonts\MyCompanySans.ttf" };` και διατηρήστε `EmbedStandardFonts = true`. |
| **Μεγάλο φύλλο εργασίας (πολλές καρτέλες)** | Ενεργοποιήστε `PdfSaveOptions.OnePagePerSheet = true` για να αποφύγετε τεράστιες σελίδες δύσκολες στην ανάγνωση. |
| **Μη εφαρμοσμένο license** | Η δοκιμαστική έκδοση προσθέτει υδατογράφημα. Καταχωρίστε το license με `License license = new License(); license.SetLicense("Aspose.Cells.lic");` πριν δημιουργήσετε το φύλλο εργασίας. |
| **Ανησυχίες για απόδοση** | Επαναχρησιμοποιήστε μια ενιαία παρουσία `PdfSaveOptions` για πολλαπλές αποθηκεύσεις και εξετάστε `PdfSaveOptions.Compression = PdfCompressionLevel.Maximum;` για να μειώσετε το μέγεθος του αρχείου. |

Αυτές οι προσαρμογές κρατούν τη **convert excel to pdf** διαδικασία σας αξιόπιστη, ανεξάρτητα από τα δεδομένα προέλευσης.

## Συχνές Ερωτήσεις

**Ε: Το `EmbedStandardFonts` ενσωματώνει επίσης μη‑τυπικές γραμματοσειρές;**  
Α: Όχι. Εγγυάται μόνο τις βασικές 14 γραμματοσειρές PDF. Για προσαρμοσμένες γραμματοσειρές πρέπει να τις παρέχετε μέσω της συλλογής `CustomFonts` όπως φαίνεται παραπάνω.

**Ε: Θα αυξηθεί δραματικά το μέγεθος του PDF;**  
Α: Η ενσωμάτωση μερικών τυπικών γραμματοσειρών προσθέτει μόνο λίγα kilobytes. Αν ενσωματώσετε πολλές μεγάλες προσαρμοσμένες γραμματοσειρές, περιμένετε μια μέτρια αύξηση — ακόμα πολύ μικρότερη από το ενσωμάτωμα πλήρων εικόνων.

**Ε: Μπορώ να ενσωματώσω γραμματοσειρές χρησιμοποιώντας άλλες βιβλιοθήκες (π.χ., iTextSharp);**  
Α: Φυσικά, αλλά το API διαφέρει. Αυτός ο οδηγός εστιάζει στο Aspose.Cells επειδή διαχειρίζεται τη μετατροπή Excel‑to‑PDF σε ένα βήμα, απλοποιώντας τη **export spreadsheet to pdf** ροή εργασίας.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το πλήρες πρόγραμμα, έτοιμο για μεταγλώττιση. Περιλαμβάνει όλες τις απαραίτητες δηλώσεις `using`, το τμήμα άδειας (σχολιασμένο) και εκτενείς σχολιασμούς.

```csharp
using System;
using Aspose.Cells;

namespace PdfExportDemo
{
    class Program
    {
        static void Main()
        {
            // Uncomment and set the path if you have a license file
            // License lic = new License();
            // lic.SetLicense(@"C:\Path\To\Aspose.Cells.lic");

            // -------------------------------------------------
            // Step 1: Create or load a workbook
            // -------------------------------------------------
            Workbook workbook = new Workbook(); // Replace with new Workbook("input.xlsx") to load an existing file

            // -------------------------------------------------
            // Step 2: Populate sample data (optional)
            // -------------------------------------------------
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Quantity");
            sheet.Cells["A2"].PutValue("Apples");
            sheet.Cells["B2"].PutValue(120);
            sheet.Cells["A3"].PutValue("Oranges");
            sheet.Cells["B3"].PutValue(85);

            // -------------------------------------------------
            // Step 3: Configure PDF save options – embed fonts
            // -------------------------------------------------
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                EmbedStandardFonts = true, // <-- This is the key to how to embed fonts
                OnePagePerSheet = false,
                // Uncomment and set custom fonts if needed
                // CustomFonts = new string[] { @"C:\Fonts\MyCompanySans.ttf" }
            };

            // -------------------------------------------------
            // Step 4: Save the workbook as a PDF file
            // -------------------------------------------------
            string outputPath = @"C:\Temp\InventoryReport.pdf";
            workbook.Save(outputPath, pdfOptions);

            Console.WriteLine($"PDF saved successfully to {outputPath}");
        }
    }
}
```

Αποθηκεύστε το ως `Program.cs`, δημιουργήστε το έργο και τρέξτε το. Το PDF θα εμφανιστεί ακριβώς στο `outputPath` που ορίσατε, με τις γραμματοσειρές σφιχτά ενσωματωμένες.

## Συμπέρασμα

Καλύψαμε **πώς να ενσωματώσετε γραμματοσειρές** όταν **αποθηκεύετε φύλλο εργασίας ως pdf** χρησιμοποιώντας το Aspose.Cells, περάσαμε κάθε γραμμή κώδικα και εξηγήσαμε γιατί η ενσωμάτωση είναι σημαντική για μια αξιόπιστη **convert excel to pdf** ροή εργασίας. Τώρα ξέρετε πώς να **export spreadsheet to pdf**, να επαληθεύσετε την ενσωμάτωση και να αντιμετωπίσετε τυπικές περιπτώσεις όπως προσαρμοσμένες γραμματοσειρές ή μεγάλα φύλλα εργασίας.  

Στο επόμενο βήμα, μπορείτε να εξερευνήσετε την προσθήκη κεφαλίδων/υποσέλιδων, την προστασία του PDF με κωδικό πρόσβασης, ή την επεξεργασία πολλαπλών φύλλων εργασίας σε μια ενιαία εκτέλεση. Κάθε

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}