---
category: general
date: 2026-01-14
description: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα χρησιμοποιώντας το Aspose.Cells
  και επίσης να μάθετε πώς να μετατρέπετε το Excel σε PPTX, να αντιγράφετε περιοχή
  σε άλλο βιβλίο εργασίας και να κάνετε το πλαίσιο κειμένου επεξεργάσιμο σε PPTX σε
  ένα ενιαίο σεμινάριο.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: el
og_description: Πώς να αντιγράψετε έναν πίνακα Pivot και στη συνέχεια να μετατρέψετε
  το Excel σε PPTX, να αντιγράψετε μια περιοχή σε άλλο βιβλίο εργασίας και να κάνετε
  το πλαίσιο κειμένου επεξεργάσιμο σε PPTX—όλα με το Aspose.Cells.
og_title: Πώς να αντιγράψετε έναν Πίνακα Pivot σε C# – Πλήρης οδηγός Excel σε PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Πώς να αντιγράψετε έναν Πίνακα Pivot σε C# – Μετατροπή Excel σε PPTX, Αντιγραφή
  περιοχής & Επεξεργάσιμο πεδίο κειμένου
url: /el/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Αντιγράψετε Πίνακα Pivot σε C# – Πλήρης Οδηγός Excel σε PPTX

Το πώς να αντιγράψετε έναν πίνακα pivot από ένα βιβλίο εργασίας σε άλλο είναι συχνή ερώτηση όταν αυτοματοποιείτε αναφορές που βασίζονται στο Excel. Σε αυτό το tutorial θα περάσουμε από τρία πραγματικά σενάρια χρησιμοποιώντας **Aspose.Cells for .NET**: αντιγραφή περιοχής πίνακα pivot, εξαγωγή φύλλου εργασίας σε αρχείο PPTX με επεξεργάσιμο πλαίσιο κειμένου, και γέμισμα ενός μοναδικού κελιού με έναν πίνακα JSON μέσω Smart Markers.  

Θα δείτε επίσης πώς να **μετατρέψετε Excel σε PPTX**, **αντιγράψετε περιοχή σε άλλο βιβλίο εργασίας**, και **κάνετε το πλαίσιο κειμένου επεξεργάσιμο σε PPTX** χωρίς να διασπαστεί η μορφοποίηση. Στο τέλος θα έχετε μια έτοιμη προς εκτέλεση βάση κώδικα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

> **Συμβουλή:** Όλα τα παραδείγματα στοχεύουν στο Aspose.Cells 23.12, αλλά οι ίδιες έννοιες ισχύουν και για παλαιότερες εκδόσεις με μικρές αλλαγές στο API.

![Διάγραμμα που δείχνει πώς αντιγράφεται ένας πίνακας pivot, εξάγεται ένα φύλλο εργασίας σε PPTX και εισάγεται ένας πίνακας JSON – ροή εργασίας αντιγραφής πίνακα pivot](how-to-copy-pivot-table-diagram.png)

---

## Τι Θα Χρειαστεί

- Visual Studio 2022 (ή οποιοδήποτε IDE C#)
- .NET 6.0 ή νεότερο runtime
- Πακέτο NuGet Aspose.Cells for .NET  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Δύο δείγμα αρχεία Excel (`source.xlsx`, `chartWithTextbox.xlsx`) τοποθετημένα σε φάκελο που ελέγχετε (αντικαταστήστε το `YOUR_DIRECTORY` με την πραγματική διαδρομή σας).

Δεν απαιτούνται πρόσθετες βιβλιοθήκες· η ίδια συναρμολόγηση `Aspose.Cells` διαχειρίζεται Excel, PPTX και Smart Markers.

## Πώς να Αντιγράψετε Πίνακα Pivot και να Διατηρήσετε τα Δεδομένα του

Όταν αντιγράφετε μια περιοχή που περιέχει πίνακα pivot, η προεπιλεγμένη συμπεριφορά είναι να επικολλήσετε μόνο τις **τιμές**. Για να διατηρήσετε αμετάβλητο τον ορισμό του pivot πρέπει να ενεργοποιήσετε τη σημαία `CopyPivotTable`.

### Βήμα‑βήμα

1. **Φορτώστε το πηγαίο βιβλίο εργασίας** που περιέχει τον πίνακα pivot.  
2. **Δημιουργήστε ένα κενό βιβλίο προορισμού** – αυτό θα λάβει την αντιγραμμένη περιοχή.  
3. **Χρησιμοποιήστε `CopyRange` με `CopyPivotTable = true`** ώστε ο ορισμός του pivot να μεταφερθεί μαζί με τα δεδομένα.  
4. **Αποθηκεύστε το αρχείο προορισμού** όπου χρειάζεται.

#### Πλήρες Παράδειγμα Κώδικα

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Γιατί λειτουργεί:**  
`CopyOptions.CopyPivotTable` λέει στο Aspose.Cells να κλωνοποιήσει το υποκείμενο αντικείμενο `PivotTable` αντί μόνο των αποδομένων τιμών του. Το βιβλίο εργασίας προορισμού περιέχει τώρα έναν πλήρως λειτουργικό pivot που μπορείτε να ανανεώσετε ή να τροποποιήσετε προγραμματιστικά.

**Περίπτωση άκρης:** Εάν το πηγαίο βιβλίο εργασίας χρησιμοποιεί εξωτερικές πηγές δεδομένων, ίσως χρειαστεί να ενσωματώσετε τα δεδομένα ή να προσαρμόσετε τις αλυσίδες σύνδεσης μετά την αντιγραφή· διαφορετικά ο pivot θα εμφανίσει “#REF!”.

## Μετατροπή Excel σε PPTX και Δημιουργία Επεξεργάσιμου Πλαισίου Κειμένου

Η εξαγωγή ενός φύλλου εργασίας σε PowerPoint είναι χρήσιμη για τη δημιουργία παρουσιάσεων απευθείας από δεδομένα. Από προεπιλογή το εξαγόμενο πλαίσιο κειμένου γίνεται στατικό σχήμα, αλλά η ρύθμιση `IsTextBoxEditable` αλλάζει αυτή τη συμπεριφορά.

### Βήμα‑βήμα

1. **Ανοίξτε το βιβλίο εργασίας** που περιέχει το γράφημα και το πλαίσιο κειμένου που θέλετε να εξάγετε.  
2. **Διαμορφώστε το `ImageOrPrintOptions`** με `SaveFormat = SaveFormat.Pptx`.  
3. **Ορίστε μια περιοχή εκτύπωσης** που περιλαμβάνει το πλαίσιο κειμένου.  
4. **Ενεργοποιήστε το `IsTextBoxEditable`** ώστε το κείμενο να μπορεί να επεξεργαστεί μετά το άνοιγμα του PPTX.  
5. **Αποθηκεύστε το αρχείο PPTX**.

#### Πλήρες Παράδειγμα Κώδικα

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Αποτέλεσμα:** Ανοίξτε το `result.pptx` στο PowerPoint – το πλαίσιο κειμένου που τοποθετήσατε στο Excel θα είναι τώρα ένα κανονικό πλαίσιο κειμένου που μπορείτε να πληκτρολογήσετε. Δεν χρειάζεται να το δημιουργήσετε ξανά χειροκίνητα.

**Κοινό λάθος:** Εάν το φύλλο εργασίας περιέχει συγχωνευμένα κελιά που διασχίζουν την περιοχή εκτύπωσης, η διαφάνεια μπορεί να μετατοπιστεί. Προσαρμόστε την περιοχή εκτύπωσης ή αποσυγχωνεύστε τα κελιά πριν την εξαγωγή.

## Αντιγραφή Περιοχής σε Άλλο Βιβλίο Εργασίας με Smart Markers (JSON → Μονό Κελί)

Μερικές φορές χρειάζεται να ενσωματώσετε έναν πίνακα JSON σε ένα μόνο κελί του Excel, για παράδειγμα όταν μεταβιβάζετε δεδομένα σε downstream συστήματα που αναμένουν μια συμβολοσειρά JSON. Τα Smart Markers του Aspose.Cells μπορούν να σειριοποιήσουν έναν πίνακα ως ένα μόνο κελί όταν ορίσετε `ArrayAsSingle = true`.

### Βήμα‑βήμα

1. **Φορτώστε ένα βιβλίο εργασίας προτύπου** που περιέχει έναν placeholder Smart Marker (π.χ., `&=Items.Name`).  
2. **Προετοιμάστε το αντικείμενο δεδομένων** – έναν ανώνυμο τύπο με έναν πίνακα `Items`.  
3. **Δημιουργήστε έναν `SmartMarkerProcessor`** και εφαρμόστε τα δεδομένα με `ArrayAsSingle`.  
4. **Αποθηκεύστε το γεμάτο βιβλίο εργασίας**.

#### Πλήρες Παράδειγμα Κώδικα

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Εξήγηση:**  
Όταν το `ArrayAsSingle` είναι true, το Aspose.Cells συνενώνει κάθε στοιχείο του `Items.Name` σε μια συμβολοσειρά τύπου JSON (`["A","B"]`) και την γράφει στο κελί που περιείχε το smart marker. Αυτό αποτρέπει τη δημιουργία ξεχωριστής σειράς για κάθε στοιχείο του πίνακα.

**Πότε να το χρησιμοποιήσετε:** Ιδανικό για εξαγωγή πινάκων ρυθμίσεων, φορτίων API, ή οποιοδήποτε σενάριο όπου ο καταναλωτής αναμένει μια συμπαγή συμβολοσειρά JSON αντί για μια πινάκωση διάταξη.

## Πρόσθετες Συμβουλές & Διαχείριση Περιπτώσεων Άκρων

| Scenario | What to Watch For | Suggested Fix |
|----------|-------------------|---------------|
| **Μεγάλοι Πίνακες Pivot** | Η χρήση μνήμης αυξάνεται απότομα κατά την αντιγραφή τεράστιων cache pivot. | Χρησιμοποιήστε `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` πριν τη φόρτωση. |
| **Εξαγωγή σε PPTX με Εικόνες** | Οι εικόνες μπορεί να rasterize με χαμηλό DPI. | Ορίστε `pptxOptions.ImageResolution = 300` για πιο καθαρές διαφάνειες. |
| **Μορφοποίηση JSON Smart Marker** | Ειδικοί χαρακτήρες (`"` , `\`) διασπούν το JSON. | Διαφύγετε τα χειροκίνητα ή χρησιμοποιήστε `JsonSerializer` για προ-σειριοποίηση πριν την τροφοδοσία των Smart Markers. |
| **Αντιγραφή Περιοχής μεταξύ Διαφορετικών Εκδόσεων Excel** | Τα παλαιότερα αρχεία `.xls` μπορεί να χάσουν τη μορφοποίηση. | Αποθηκεύστε τον προορισμό ως `.xlsx` για να διατηρήσετε τις σύγχρονες δυνατότητες. |

## Ανακεφαλαίωση – Πώς να Αντιγράψετε Πίνακα Pivot και Πολλά Άλλα

Ξεκινήσαμε απαντώντας στο **πώς να αντιγράψετε πίνακα pivot** διατηρώντας τη λειτουργικότητά του, στη συνέχεια σας δείξαμε πώς να **μετατρέψετε Excel σε PPTX**, **κάνετε το πλαίσιο κειμένου επεξεργάσιμο σε PPTX**, και τέλος πώς να **αντιγράψετε περιοχή σε άλλο βιβλίο εργασίας** χρησιμοποιώντας Smart Markers για την ενσωμάτωση ενός πίνακα JSON ως ένα μόνο κελί.

Τα τρία αποσπάσματα είναι αυτόνομα· μπορείτε να τα επικολλήσετε σε μια νέα εφαρμογή console, να προσαρμόσετε τις διαδρομές αρχείων και να τα εκτελέσετε σήμερα.

## Τι Ακολουθεί;

- **Εξερευνήστε άλλες μορφές εξαγωγής** – το Aspose.Cells υποστηρίζει επίσης PDF, XPS και HTML.  
- **Ανανεώστε πίνακες pivot προγραμματιστικά** χρησιμοποιώντας `PivotTable.RefreshData()` μετά την αντιγραφή.  
- **Συνδυάστε Smart Markers με γραφήματα** για τη δημιουργία δυναμικών ταμπλό που ενημερώνονται αυτόματα.  

Αν ενδιαφέρεστε για **αποθήκευση βιβλίου εργασίας ως PPTX** με προσαρμοσμένες διατάξεις διαφάνειας, δείτε την τεκμηρίωση του Aspose.Cells για το `SlideOptions`.

Νιώστε ελεύθεροι να πειραματιστείτε—αλλάξτε την περιοχή εκτύπωσης, δοκιμάστε διαφορετικές `CopyOptions`, ή δώστε ένα πιο σύνθετο φορτίο JSON. Το API είναι αρκετά ευέλικτο για τις περισσότερες γραμμές αναφοράς.

### Συχνές Ερωτήσεις

**Ε: Αντιγράφει το `CopyPivotTable` επίσης τα slicers;**  
Α: Όχι άμεσα. Τα slicers είναι ξεχωριστά αντικείμενα· μετά την αντιγραφή θα χρειαστεί να τα δημιουργήσετε ξανά ή να τα αντιγράψετε μέσω της συλλογής `Worksheet.Shapes`.

**Ε: Μπορώ να εξάγω πολλά φύλλα εργασίας σε ένα ενιαίο PPTX deck;**  
Α: Ναι. Επαναλάβετε για κάθε φύλλο εργασίας, καλέστε `Save` με τις ίδιες `ImageOrPrintOptions` και ορίστε `pptxOptions.StartSlideNumber` για να συνεχίσετε την αρίθμηση.

**Ε: Τι γίνεται αν ο πίνακας JSON περιέχει ένθετα αντικείμενα;**  
Α: Ορίστε `ArrayAsSingle = false` και χρησιμοποιήστε ένα προσαρμοσμένο πρότυπο που επαναλαμβάνεται πάνω σε

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}