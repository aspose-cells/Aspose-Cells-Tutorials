---
category: general
date: 2026-08-14
description: Εξαγωγή Excel σε PowerPoint χρησιμοποιώντας το Aspose.Cells και μάθετε
  πώς να υπολογίζετε τύπους Excel στον κώδικα. Παράδειγμα C# βήμα‑προς‑βήμα με πλήρες
  πηγαίο κώδικα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: el
lastmod: 2026-08-14
og_description: Εξαγωγή Excel σε PowerPoint με το Aspose.Cells και υπολογισμός τύπων
  Excel στον κώδικα. Ακολουθήστε αυτόν τον πλήρη οδηγό για να δημιουργήσετε επεξεργάσιμα
  αρχεία PPTX από βιβλία εργασίας.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Εξαγωγή Excel σε PowerPoint με το Aspose.Cells – πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Εξαγωγή Excel σε PowerPoint με το Aspose.Cells – πλήρης οδηγός προγραμματισμού
url: /el/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Excel σε PowerPoint με Aspose.Cells – πλήρης προγραμματιστικός οδηγός

Αν χρειάζεστε **εξαγωγή Excel σε PowerPoint** προγραμματιστικά, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.Cells για .NET. Θα μάθετε επίσης πώς να **υπολογίζετε τύπους Excel σε κώδικα**, να αντιγράφετε πίνακες Pivot χωρίς να χάνετε τις ορισμούς τους και να χρησιμοποιείτε τη νέα λειτουργία Office‑365 EXPAND για δυναμικούς πίνακες.

Στις παρακάτω ενότητες θα περάσουμε από ένα πραγματικό παράδειγμα C#, θα εξηγήσουμε γιατί κάθε γραμμή είναι σημαντική και θα καλύψουμε κοινά προβλήματα ώστε να προσαρμόσετε τη λύση στα δικά σας έργα.

## Τι καλύπτει αυτό το tutorial

* Φόρτωση υπάρχοντος βιβλίου εργασίας (`input.xlsx`)  
* Αντιγραφή περιοχής που περιέχει πίνακα Pivot διατηρώντας τον ορισμό του  
* Εξαγωγή του βιβλίου εργασίας σε αρχείο PowerPoint (`.pptx`) με επεξεργάσιμα πλαίσια κειμένου και σχήματα  
* Εξαγωγή περιοχής κελιών ως συμβολοσειρές χρησιμοποιώντας προσαρμοσμένη λογική  
* Υπολογισμός τύπων Excel σε κώδικα, συμπεριλαμβανομένης της λειτουργίας Office‑365 EXPAND  
* Αποθήκευση του τελικού βιβλίου εργασίας με όλες τις αλλαγές που εφαρμόστηκαν  

**Προαπαιτούμενα**  
* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7.2+)  
* Aspose.Cells για .NET v25.11 ή νεότερο (η επιλογή `CopyPivotTable` εισήχθη στην έκδοση v25.11)  
* Βασική κατανόηση της C# και των εννοιών του Excel όπως περιοχές, πίνακες Pivot και τύποι  

> **Συμβουλή επαγγελματία:** Εγκαταστήστε το Aspose.Cells μέσω NuGet (`Install-Package Aspose.Cells`) για να διατηρείτε το έργο σας ενημερωμένο με τις τελευταίες δυνατότητες.

## Εξαγωγή Excel σε PowerPoint με Aspose.Cells

Η πρώτη σημαντική εργασία είναι η μετατροπή του βιβλίου εργασίας σε παρουσίαση PowerPoint διατηρώντας όλα τα οπτικά στοιχεία επεξεργάσιμα. Αυτό είναι απαραίτητο όταν θέλετε να δημιουργείτε αυτόματα διαφάνειες από οικονομικές αναφορές ή πίνακες ελέγχου.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Γιατί λειτουργεί αυτό

* **`Workbook`** φορτώνει ολόκληρο το αρχείο Excel στη μνήμη, δίνοντάς σας πλήρη πρόσβαση στο API.  
* **`CopyRange`** με `CopyPivotTable = true` εξασφαλίζει ότι η πηγή δεδομένων, η κρυφή μνήμη και η διάταξη του πίνακα Pivot αντιγράφονται ακριβώς—κάτι που οι παλαιότερες εκδόσεις του Aspose.Cells δεν μπορούσαν να κάνουν.  
* Η προσθήκη ενός νέου φύλλου εργασίας (`Copy`) σας επιτρέπει να διατηρήσετε το αρχικό φύλλο ανέγγιχτο, κάτι χρήσιμο για ιχνηλασιμότητα.

## Εξαγωγή του βιβλίου εργασίας σε PowerPoint με επεξεργάσιμα αντικείμενα

Τώρα **μετατρέπουμε το βιβλίο εργασίας** σε αρχείο PowerPoint. Ενεργοποιώντας το `ExportEditableObjects`, κάθε γράφημα, σχήμα ή πλαίσιο κειμένου γίνεται εγγενές αντικείμενο PowerPoint που οι χρήστες **μπορούν να επεξεργαστούν** απευθείας μετά την εξαγωγή.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Εξήγηση

* **`WorkbookDesigner`** είναι ένας υψηλού επιπέδου βοηθός που προετοιμάζει το βιβλίο εργασίας για εξαγωγή, διαχειριζόμενος Smart Markers, ονομασμένες περιοχές και προσαρμογές διάταξης.  
* Ορίζοντας `ExportEditableObjects = true` λέτε στο Aspose.Cells να μεταφράσει τα σχέδια του Excel σε σχήματα PowerPoint αντί να τα μετατρέπει σε εικόνες. Αυτό παράγει μια **πλήρως επεξεργάσιμη** παρουσίαση.  

> **Ακραία περίπτωση:** Εάν το βιβλίο εργασίας σας περιέχει σύνθετα γραφήματα που προέρχονται από εξωτερικές συνδέσεις δεδομένων, βεβαιωθείτε ότι αυτές οι συνδέσεις έχουν επιλυθεί πριν καλέσετε το **`ExportToPptx`**, διαφορετικά το γράφημα μπορεί να εμφανιστεί κενό.

## Εξαγωγή περιοχής ως συμβολοσειρές χρησιμοποιώντας προσαρμοσμένη λογική

Μερικές φορές χρειάζεστε ακατέργαστες τιμές κειμένου για επεξεργασία σε επόμενο στάδιο (π.χ. τροφοδοσία ενός αναλυτή CSV). Η κλάση `ExportTableOptions` σας επιτρέπει να ελέγξετε πώς μετατρέπεται κάθε κελί.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Γιατί μπορεί να το χρησιμοποιήσετε

* **Ομοιόμορφος τύπος δεδομένων:** Η εξαγωγή ως συμβολοσειρές αποτρέπει σφάλματα ασυμφωνίας τύπων όταν ο καταναλωτής αναμένει κείμενο.  
* **Προσαρμοσμένη μορφοποίηση:** Αντικαταστήστε το `value.ToString()` με οποιονδήποτε προσαρμοσμένο μορφοποιητή (π.χ. `value.ToString("yyyy-MM-dd")` για ημερομηνίες).  

## Υπολογισμός τύπων Excel σε κώδικα

Μια συχνή απαίτηση είναι η **υπολογισμός τύπων Excel σε κώδικα** χωρίς το άνοιγμα του Excel. Το Aspose.Cells παρέχει ενσωματωμένο μηχανισμό υπολογισμού που λειτουργεί εκτός σύνδεσης και υποστηρίζει τις τελευταίες λειτουργίες του Office‑365, συμπεριλαμβανομένης της `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Πώς λειτουργεί η μηχανή υπολογισμού

* Η ιδιότητα `Formula` αποθηκεύει την έκφραση ακριβώς όπως θα την πληκτρολογούσατε στο Excel.  
* Η μέθοδος `CalculateFormula()` ενεργοποιεί μια πλήρη επανυπολογισμό του βιβλίου εργασίας, λαμβάνοντας υπόψη τις εξαρτήσεις μεταξύ των κελιών.  
* Η λειτουργία `EXPAND` (διαθέσιμη στο Excel 365) επιστρέφει μια περιοχή διασποράς βασισμένη στο κελί προέλευσης (`B1`) και στις καθορισμένες γραμμές (`5`) και στήλες (`3`).  

> **Συμβουλή:** Εάν χρειάζεται να υπολογίσετε μόνο ένα υποσύνολο του βιβλίου εργασίας, χρησιμοποιήστε το `Worksheet.CalculateFormula()` για να περιορίσετε το εύρος και να βελτιώσετε την απόδοση.

## Αποθήκευση του βιβλίου εργασίας με όλες τις αλλαγές

Τέλος, γράψτε το τροποποιημένο βιβλίο εργασίας πίσω στο δίσκο. Μπορείτε να αποθηκεύσετε σε οποιαδήποτε από τις υποστηριζόμενες μορφές (`.xlsx`, `.xls`, `.csv`, κ.λπ.) αλλάζοντας την επέκταση του αρχείου.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Τι πρέπει να ελέγξετε

* Ανοίξτε το `result.xlsx` στο Excel για να επιβεβαιώσετε ότι ο πίνακας Pivot έχει αντιγραφεί, ότι το αποτέλεσμα του τύπου `EXPAND` είναι σωστό και ότι οι προσαρμοσμένες συμβολοσειρές έχουν εξαχθεί.  
* Ανοίξτε το `output.pptx` στο PowerPoint· θα πρέπει να δείτε μια διαφάνεια που αντικατοπτρίζει τη διάταξη του Excel και όλα τα γραφήματα/πλαίσια κειμένου να είναι επεξεργάσιμα.

## Συχνές ερωτήσεις και αντιμετώπιση προβλημάτων

| Ερώτηση | Απάντηση |
|----------|--------|
| **Χρειάζομαι άδεια για να χρησιμοποιήσω το Aspose.Cells;** | Ναι. Η δοκιμαστική έκδοση λειτουργεί για αξιολόγηση, αλλά μια πλήρης άδεια αφαιρεί τα υδατογραφήματα αξιολόγησης και ξεκλειδώνει τη δυνατότητα `CopyPivotTable`. |
| **Τι γίνεται αν το εξαγόμενο PPTX εμφανίζει κενά σχήματα;** | Ελέγξτε ότι τα αντικείμενα σχεδίασης του βιβλίου εργασίας δεν είναι κρυμμένα (`Visible = true`) και ότι τυχόν εξωτερικοί σύνδεσμοι εικόνων έχουν ενσωματωθεί πριν από την εξαγωγή. |
| **Μπορώ να εξάγω πολλαπλά φύλλα εργασίας σε ξεχωριστές διαφάνειες PPTX;** | Χρησιμοποιήστε το `WorkbookDesigner.ExportToPptx` σε βρόχο, ορίζοντας διαφορετικό `ExportOptions` για κάθε φύλλο, ή συνδυάστε τα σε μία παρουσίαση προσθέτοντας διαφάνειες χειροκίνητα μέσω του Aspose.Slides. |
| **Η μέθοδος `CalculateFormula` είναι thread‑safe;** | Όχι. Εκτελέστε τους υπολογισμούς σε ένα μόνο νήμα ή κλωνοποιήστε το βιβλίο εργασίας ανά νήμα για να αποφύγετε συνθήκες αγώνα. |

## Συμπέρασμα

Τώρα έχετε μια **πλήρη, ολοκληρωμένη λύση για εξαγωγή Excel σε PowerPoint** χρησιμοποιώντας το Aspose.Cells, και καταλαβαίνετε πώς να **υπολογίζετε τύπους Excel σε κώδικα**—συμπεριλαμβανομένης της σύγχρονης λειτουργίας `EXPAND`. Το tutorial κάλυψε τη φόρτωση βιβλίου εργασίας, την αντιγραφή πινάκων Pivot, την εξαγωγή σε επεξεργάσιμο PowerPoint, την προσαρμοσμένη εξαγωγή συμβολοσειρών, τον υπολογισμό τύπων και την τελική αποθήκευση.

Από εδώ μπορείτε:

* Να επεκτείνετε την εξαγωγή ώστε να περιλαμβάνει πολλαπλές διαφάνειες ανά φύλλο εργασίας (η δευτερεύουσα λέξη‑κλειδί *calculate Excel formulas in code* μπορεί να επαναχρησιμοποιηθεί κατά τη δημιουργία δεδομένων γραφημάτων).  
* Να ενσωματώσετε το Aspose.Slides για προσθήκη κινήσεων ή διατάξεων κύριας διαφάνειας.  
* Να αντικαταστήσετε το απλό delegate `CustomExport` με μορφοποίηση προσαρμοσμένης τοπικής ρύθμισης για διεθνή έργα.  

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές περιοχές, να εξερευνήσετε άλλες λειτουργίες του Office‑365 (π.χ. `FILTER`, `SORT`) και να συνδυάσετε αυτή τη ροή εργασίας με αυτοματοποιημένη αποστολή email για πλήρως αυτόματες pipelines αναφορών.

---


## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίησή σας.

- [Automate Excel Data Export Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}