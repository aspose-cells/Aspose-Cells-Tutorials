---
category: general
date: 2026-09-15
description: Μάθετε πώς να αντιγράψετε έναν πίνακα Pivot, να αντιγράψετε φύλλο εργασίας
  με Pivot και να αποθηκεύσετε το βιβλίο εργασίας ως pptx χρησιμοποιώντας το Aspose.Cells
  σε C#. Πλήρης οδηγός βήμα‑βήμα.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: el
lastmod: 2026-09-15
og_description: Πώς να αντιγράψετε έναν πίνακα Pivot, να αντιγράψετε φύλλο εργασίας
  με Pivot και να αποθηκεύσετε το βιβλίο εργασίας ως pptx χρησιμοποιώντας το Aspose.Cells.
  Ακολουθήστε τα πλήρη, εκτελέσιμα παραδείγματα C#.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Πώς να αντιγράψετε έναν πίνακα Pivot και να εξάγετε φύλλα εργασίας – πλήρης
  οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Πώς να αντιγράψετε έναν συγκεντρωτικό πίνακα διατηρώντας τα φύλλα εργασίας
url: /el/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αντιγράψετε έναν πίνακα Pivot διατηρώντας τα φύλλα εργασίας

Αν χρειάζεστε **πώς να αντιγράψετε έναν πίνακα Pivot** από ένα βιβλίο εργασίας σε άλλο χωρίς να χάσετε την υποκείμενη κρυφή μνήμη Pivot, αυτός ο οδηγός παρέχει μια έτοιμη λύση. Θα δείτε επίσης πώς να **αντιγράψετε φύλλο εργασίας με Pivot** και πώς να **αποθηκεύσετε το βιβλίο εργασίας ως pptx** διατηρώντας τα επεξεργάσιμα πλαίσια κειμένου. Όλα τα παραδείγματα χρησιμοποιούν την πιο πρόσφατη έκδοση του Aspose.Cells για .NET, ώστε να μπορείτε να ενσωματώσετε τον κώδικα σε οποιοδήποτε έργο C# και να δείτε άμεσα τα αποτελέσματα.

Η προγραμματιστική εργασία με αρχεία Excel συχνά περιλαμβάνει τη μεταφορά δεδομένων μεταξύ βιβλίων εργασίας, την εξαγωγή σε παρουσιάσεις ή την εισαγωγή σύνθετων Smart Markers. Τα τρία αποσπάσματα κώδικα παρακάτω καλύπτουν αυτά τα κοινά σενάρια και εξηγούν γιατί κάθε βήμα είναι σημαντικό.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερη έκδοση εγκατεστημένη  
* Aspose.Cells για .NET (έκδοση 25.11 ή νεότερη) αναφορά στο έργο σας  
* Έναν φάκελο με όνομα `YOUR_DIRECTORY` όπου θα διαβαστούν και θα γραφτούν τα δείγμα αρχεία  

Δεν απαιτούνται επιπλέον πακέτα NuGet.

---

## Πώς να αντιγράψετε πίνακα Pivot με Aspose.Cells

Η αντιγραφή μιας περιοχής που περιέχει πίνακα Pivot διατηρώντας την κρυφή μνήμη Pivot είναι συχνή απαίτηση. Τα παρακάτω βήματα δείχνουν την ακριβή ακολουθία που χρειάζεστε.

### Βήμα 1 – Φορτώστε το πηγαίο βιβλίο εργασίας που περιέχει τον πίνακα Pivot

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Γιατί*: Το Aspose.Cells διαβάζει το βιβλίο εργασίας στη μνήμη, δίνοντάς σας πρόσβαση σε φύλλα εργασίας, κελιά και πίνακες Pivot.

### Βήμα 2 – Δημιουργήστε ένα κενό προορισμό βιβλίου εργασίας

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Γιατί*: Ξεκινώντας με ένα κενό βιβλίο εργασίας εξασφαλίζετε ότι δεν υπάρχουν κρυφά στυλ ή ονομαστικές περιοχές που να παρεμβαίνουν στη λειτουργία αντιγραφής.

### Βήμα 3 – Αντιγράψτε τις γραμμές που περιλαμβάνουν τον πίνακα Pivot

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Γιατί*: Η `CopyRows` αντιγράφει τις ακατέργαστες τιμές κελιών, τις μορφές και τις αναφορές στην κρυφή μνήμη Pivot. Η περιοχή πρέπει να περιλαμβάνει ολόκληρη την περιοχή του πίνακα Pivot.

### Βήμα 4 – Αντιγράψτε τις στήλες που περιέχουν τον πίνακα Pivot

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Γιατί*: Οι πίνακες Pivot εκτείνονται τόσο σε γραμμές όσο και σε στήλες· η αντιγραφή των στηλών εξασφαλίζει ότι διατηρείται η πλήρης διάταξη του πίνακα.

### Βήμα 5 – Μεταφέρετε το προετοιμασμένο φύλλο στον προορισμό βιβλίου εργασίας

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Γιατί*: Η μέθοδος `Copy` κλωνοποιεί το φύλλο εργασίας, συμπεριλαμβανομένης της κρυφής μνήμης Pivot, ώστε το προορισμένο βιβλίο εργασίας να εμφανίζει έναν ταυτόσιο πίνακα Pivot.

### Βήμα 6 – Αποθηκεύστε το αποτέλεσμα – ο πίνακας Pivot παραμένει αμετάβλητος

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Γιατί*: Η αποθήκευση του βιβλίου εργασίας γράφει όλες τις εσωτερικές δομές, εγγυώμενη ότι ο πίνακας μπορεί να ανανεωθεί αργότερα.

**Pro tip**: Μετά την αντιγραφή, μπορείτε να καλέσετε `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` για να ενημερώσετε τα δεδομένα εάν τα πηγαία δεδομένα έχουν αλλάξει.

---

## Αντιγραφή φύλλου εργασίας με Pivot – μια σύντομη εναλλακτική

Αν απλώς χρειάζεστε να αντιγράψετε ολόκληρο ένα φύλλο εργασίας που ήδη περιέχει πίνακα Pivot, μπορείτε να παραλείψετε τα βήματα αντιγραφής γραμμών/στηλών και να χρησιμοποιήσετε απευθείας τη μέθοδο `Copy` σε επίπεδο φύλλου.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Αυτή η προσέγγιση είναι χρήσιμη όταν το φύλλο εργασίας δεν περιέχει επιπλέον δεδομένα εκτός της περιοχής του Pivot. Η λειτουργία **copy worksheet with pivot** διατηρεί αυτόματα όλη τη μορφοποίηση, τις ονομαστικές περιοχές και τις κρυφές μνήμες Pivot.

---

## Αποθήκευση βιβλίου εργασίας ως PPTX με επεξεργάσιμα πλαίσια κειμένου

Η εξαγωγή ενός φύλλου Excel που περιέχει επεξεργάσιμο πλαίσιο κειμένου σε PowerPoint μπορεί να απαιτείται για dashboards αναφορών. Ο παρακάτω κώδικας δείχνει **save workbook as pptx** διατηρώντας το πλαίσιο κειμένου επεξεργάσιμο.

### Βήμα 1 – Φορτώστε το βιβλίο εργασίας που περιλαμβάνει το πλαίσιο κειμένου

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Βήμα 2 – Διαμορφώστε τις επιλογές αποθήκευσης PPTX

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Γιατί*: Η ρύθμιση `ExportEditableTextBox` λέει στο Aspose.Cells να μετατρέψει το πλαίσιο κειμένου του Excel σε σχήμα PowerPoint που παραμένει επεξεργάσιμο μετά την εξαγωγή.

### Βήμα 3 – Αποθηκεύστε το βιβλίο εργασίας ως PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Αναμενόμενο αποτέλεσμα**: Ανοίξτε το `Result.pptx` στο PowerPoint, επιλέξτε το πλαίσιο κειμένου και επεξεργαστείτε το περιεχόμενό του όπως οποιοδήποτε ενσωματωμένο σχήμα.

**Συχνή ερώτηση**: *Τι γίνεται αν χρειάζεται να κλειδώσω το πλαίσιο κειμένου;*  
Ορίστε `pptxOptions.ExportEditableTextBox = false`; το σχήμα θα μετατραπεί σε στατική εικόνα.

---

## Εξαγωγή Smart Marker που περιέχει πίνακα JSON ως τιμή ενός μόνο κελιού

Τα Smart Markers σας επιτρέπουν να γεμίζετε πρότυπα Excel με σύνθετες δομές δεδομένων. Παρακάτω υπάρχει ένα πλήρες παράδειγμα που δείχνει **how to copy pivot table**‑style διαχείριση δεδομένων ενώ εισάγει έναν πίνακα JSON σε ένα μόνο κελί.

### Βήμα 1 – Προετοιμάστε το SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Βήμα 2 – Εισάγετε ένα Smart Marker στο κελί A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Βήμα 3 – Ορίστε την πηγή δεδομένων με έναν πίνακα τύπου JSON

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Βήμα 4 – Επεξεργαστείτε το βιβλίο εργασίας

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Βήμα 5 – Αποθηκεύστε το παραγόμενο βιβλίο εργασίας

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Επαλήθευση αποτελέσματος**: Ανοίξτε το `JsonSingleCell.xlsx` και βεβαιωθείτε ότι το κελί A1 εμφανίζει `A,B,C`. Αυτό δείχνει πώς να αντιμετωπίζετε μια συλλογή ως τιμή ενός μόνο κελιού, ένα μοτίβο που συχνά απαιτείται όταν εξάγετε δεδομένα για downstream συστήματα.

---

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω υπάρχει ένα ενιαίο πρόγραμμα που συνδυάζει τα τρία σενάρια. Μπορείτε να αντιγράψετε τον κώδικα σε μια εφαρμογή console, να προσαρμόσετε τις διαδρομές αρχείων και να το εκτελέσετε για να δείτε όλα τα τρία αποτελέσματα.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Η εκτέλεση αυτού του προγράμματος παράγει:

* `CopyWithPivot.xlsx` – ένα τέλειο αντίγραφο του αρχικού πίνακα Pivot.  
* `Result.pptx` – μια διαφάνεια PowerPoint με επεξεργάσιμο πλαίσιο κειμένου.  
* `JsonSingleCell.xlsx` – ένα φύλλο όπου ο πίνακας JSON εμφανίζεται σε ένα μόνο κελί.

---

## Συμπέρασμα

Τώρα γνωρίζετε **πώς να αντιγράψετε έναν πίνακα Pivot** με ασφάλεια, πώς να **αντιγράψετε φύλλο εργασίας με Pivot** με μία κλήση, και πώς να **αποθηκεύσετε το βιβλίο εργασίας ως pptx** διατηρώντας επεξεργάσιμα πλαίσια κειμένου. Αυτά τα μοτίβα καλύπτουν τις πιο κοινές ροές εργασίας Excel‑to‑PowerPoint και Excel‑to‑JSON που θα συναντήσετε σε έργα επιχειρησιακού αυτοματισμού.

Στη συνέχεια, εξετάστε:

* Ανανέωση αντιγραμμένων πινάκων Pivot προγραμματιστικά (`PivotTable.Refresh()`)  
* Εξαγωγή σε άλλες μορφές όπως PDF ή HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Χρήση προχωρημένων επιλογών Smart Marker όπως προσαρμοσμένες συναρτήσεις ή μορφοποίηση υπό όρους  

Μη διστάσετε να πειραματιστείτε με διαφορετικές περιοχές, πολλαπλά φύλλα εργασίας ή μεγαλύτερες δομές JSON. Το API του Aspose.Cells σας δίνει λεπτομερή έλεγχο, ώστε να προσαρμόσετε αυτά τα παραδείγματα σε οποιοδήποτε πραγματικό σενάριο. Καλή κωδικοποίηση!

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στην υλοποίηση των δικών σας έργων.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}