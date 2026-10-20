---
category: general
date: 2026-10-20
description: Αντιγράψτε τον πίνακα Pivot σε νέο βιβλίο εργασίας χρησιμοποιώντας το
  Aspose.Cells και μάθετε πώς να εξάγετε ένα επεξεργάσιμο σχήμα στο PowerPoint σε
  έναν ενιαίο οδηγό.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: el
lastmod: 2026-10-20
og_description: Αντιγράψτε τον πίνακα Pivot σε νέο βιβλίο εργασίας χρησιμοποιώντας
  το Aspose.Cells και εξαγάγετε ένα επεξεργάσιμο σχήμα στο PowerPoint—βήμα‑βήμα κώδικας
  που μπορείτε να εκτελέσετε σήμερα.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Αντιγραφή πίνακα Pivot σε νέο βιβλίο εργασίας, εξαγωγή σχήματος σε PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Αντιγραφή πίνακα Pivot σε νέο βιβλίο εργασίας, εξαγωγή σχήματος στο PowerPoint
url: /el/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αντιγραφή πίνακα pivot σε νέο βιβλίο εργασίας, εξαγωγή σχήματος σε PowerPoint

Αν χρειάζεστε **copy pivot table to new workbook** διατηρώντας τη λειτουργικότητά του, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε με το Aspose.Cells. Θα δείτε επίσης τον πιο γρήγορο τρόπο για **export an editable shape to PowerPoint**, ώστε το πλαίσιο κειμένου να παραμένει επεξεργάσιμο μετά τη μετατροπή.

Πολλοί προγραμματιστές υποθέτουν ότι η αντιγραφή μιας περιοχής που περιέχει έναν πίνακα pivot θα χάσει τη λογική του pivot, ή ότι τα σχήματα γίνονται στατικές εικόνες όταν αποθηκευτούν ως PPTX. Αυτό το tutorial απορρίπτει αυτά τα μύθους και σας παρέχει μια αξιόπιστη, έτοιμη για παραγωγή λύση.

Στις παρακάτω ενότητες θα:

* Φορτώσετε ένα πηγαίο βιβλίο εργασίας και αντιγράψετε μια περιοχή που περιλαμβάνει πίνακα pivot.
* Δημιουργήσετε ένα προορισμό βιβλίου εργασίας που περιέχει τον ίδιο πίνακα pivot.
* Προσθέσετε ένα σχήμα πλαίσιο κειμένου, τροποποιήσετε το κείμενό του και αποθηκεύσετε το βιβλίο εργασίας ως παρουσίαση PowerPoint όπου το πλαίσιο κειμένου παραμένει επεξεργάσιμο.
* Κατανοήσετε γιατί απαιτείται κάθε κλήση API και πώς να αποφύγετε κοινά προβλήματα.

**Prerequisites**

* .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.7+).
* Aspose.Cells for .NET εγκατεστημένο (`Install-Package Aspose.Cells`).
* Βασικές γνώσεις C# και Visual Studio (ή οποιοδήποτε IDE προτιμάτε).

---

## Αντιγραφή πίνακα pivot σε νέο βιβλίο εργασίας

Αυτή η ενότητα βήμα‑βήμα δείχνει πώς να αντιγράψετε μια περιοχή που περιέχει πίνακα pivot και να διατηρήσετε τον ορισμό του pivot στο νέο αρχείο.

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Why?*  
`Workbook` είναι το σημείο εισόδου για οποιαδήποτε επεξεργασία Excel στο Aspose.Cells. Η επιλογή του σωστού φύλλου εξασφαλίζει ότι δουλεύουμε με την ακριβή θέση του πίνακα pivot.

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Why?*  
Ο πίνακας pivot βρίσκεται μέσα σε ένα συγκεκριμένο μπλοκ κελιών. Καθορίζοντας ένα `CellArea` που περιβάλλει πλήρως τον pivot, το Aspose.Cells γνωρίζει να αντιγράψει και την υποκείμενη cache του pivot.

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why?*  
Ένα νέο βιβλίο εργασίας εγγυάται ότι δεν υπάρχουν συγκρουόμενες ονομαστικές περιοχές ή υπάρχοντες pivots, κάνοντας την ενέργεια αντιγραφής καθαρή.

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Why?*  
`CopyRows` είναι μέρος του **Aspose.Cells copy rows** API. Αντιγράφει τόσο τις τιμές των κελιών όσο και την κρυφή cache του pivot, ώστε ο πίνακας pivot να παραμένει λειτουργικός μετά τη μεταφορά.

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
Ανοίξτε το `CopyWithPivot.xlsx` στο Excel. Ο πίνακας pivot εμφανίζεται ακριβώς όπως στο πηγαίο αρχείο και μπορείτε να τον ανανεώσετε ή να τον τροποποιήσετε κανονικά.

---

## Export editable shape to PowerPoint

Τώρα θα προσθέσουμε ένα σχήμα πλαίσιο κειμένου, θα αλλάξουμε το περιεχόμενό του και θα αποθηκεύσουμε το βιβλίο εργασίας ως αρχείο PPTX. Το σχήμα παραμένει πλήρως επεξεργάσιμο όταν ανοίξει στο PowerPoint.

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Why?*  
`AddTextBox` δημιουργεί ένα **editable textbox in PowerPoint**‑compatible σχήμα. Οι συντεταγμένες είναι σε points· προσαρμόστε τις ώστε να ταιριάζουν με τη διάταξή σας.

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Why?*  
Η άμεση πρόσβαση στο αντικείμενο `Shape` σας επιτρέπει να αλλάξετε ιδιότητες όπως `Text`, `Font` ή `Fill`. Αυτό το βήμα δείχνει πώς να ορίσετε προγραμματιστικά το αρχικό περιεχόμενο.

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
Ανοίξτε το `Presentation.pptx` στο Microsoft PowerPoint. Το πλαίσιο κειμένου εμφανίζεται στη πρώτη διαφάνεια και μπορείτε να κάνετε διπλό‑κλικ για να επεξεργαστείτε το κείμενο όπως σε οποιοδήποτε ενσωματωμένο σχήμα PowerPoint.

---

## Expected output

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | Ένα φύλλο εργασίας που περιέχει τον αρχικό πίνακα pivot, πλήρως λειτουργικό (η ανανέωση λειτουργεί). |
| `Presentation.pptx` | Μία διαφάνεια με επεξεργάσιμο πλαίσιο κειμένου που διαβάζει “Change me in PowerPoint”. |

---

## Common pitfalls and best‑practice tips

* **Pivot cache loss** – Εάν αντιγράψετε μόνο τις τιμές των κελιών (π.χ., χρησιμοποιώντας `CopyRows` με τη σημαία `PasteOptions` ορισμένη σε `PasteValues`), η cache του pivot παραλείπεται και ο πίνακας γίνεται στατικός. Χρησιμοποιείτε πάντα την προεπιλεγμένη υπερφόρτωση του `CopyRows` όπως φαίνεται.
* **Shape positioning** – Το `AddTextBox` χρησιμοποιεί μονάδες σημείου, όχι δείκτες κελιών του Excel. Δοκιμάστε τις συντεταγμένες σε ένα δείγμα αρχείου για να αποφύγετε τοποθέτηση εκτός διαφάνειας.
* **File format mismatch** – Η αποθήκευση ενός βιβλίου εργασίας ως PPTX με `SaveFormat.Pptx` μετατρέπει αυτόματα όλα τα υποστηριζόμενα σχήματα. Η προσπάθεια αποθήκευσης ως `Pdf` θα ραστεροποιήσει το σχήμα, καθιστώντας το μη επεξεργάσιμο.

---

## Conclusion

Τώρα ξέρετε πώς να **copy pivot table to new workbook** και πώς να **export an editable shape to PowerPoint** χρησιμοποιώντας το Aspose.Cells for .NET. Τα πλήρη, εκτελέσιμα παραδείγματα κώδικα καλύπτουν κάθε απαιτούμενη κλήση API, εξηγούν γιατί κάθε βήμα είναι σημαντικό και δείχνουν τα αναμενόμενα αποτελέσματα.

Στη συνέχεια, μπορείτε να εξερευνήσετε:

* **Working with charts** – αντιγραφή γραφημάτων μαζί με πίνακες pivot (`Aspose.Cells copy rows between worksheets`).

## Τι Θα Μάθετε Στη Σύντομη Μελλοντική Σας

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}