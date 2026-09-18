---
category: general
date: 2026-09-18
description: Δημιουργήστε PowerPoint από Excel με το Aspose.Cells – αντιγράψτε πίνακες
  Pivot, εξάγετε περιοχές και αποθηκεύστε ως PPTX σε λίγες γραμμές κώδικα C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: el
lastmod: 2026-09-18
og_description: Δημιουργήστε PowerPoint από το Excel γρήγορα. Μάθετε πώς να αντιγράψετε
  πίνακες Pivot, να εξάγετε περιοχές και να αποθηκεύσετε ένα βιβλίο εργασίας ως PPTX
  χρησιμοποιώντας το Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Δημιουργία PowerPoint από Excel με το Aspose.Cells – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Πώς να δημιουργήσετε PowerPoint από το Excel χρησιμοποιώντας το Aspose.Cells
url: /el/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε PowerPoint από το Excel χρησιμοποιώντας το Aspose.Cells

Αν χρειάζεστε να δημιουργήσετε PowerPoint από το Excel, αυτός ο οδηγός σας δείχνει μια σύντομη, ολοκληρωμένη λύση. Θα δείτε πώς να αντιγράψετε έναν πίνακα Pivot, να εξάγετε μια επιλεγμένη περιοχή και να αποθηκεύσετε το αποτέλεσμα ως αρχείο PPTX με λίγες μόνο γραμμές κώδικα C#.

Η δημιουργία ενός σετ διαφανειών απευθείας από δεδομένα υπολογιστικού φύλλου αφαιρεί το χειροκίνητο βήμα αντιγραφής‑επικόλλησης που επιβραδύνει τις ροές εργασίας αναφοράς. Ο οδηγός καλύπτει όλα όσα χρειάζεστε, από τη ρύθμιση του έργου μέχρι το τελικό αρχείο PPTX, και λειτουργεί με την πιο πρόσφατη έκδοση του Aspose.Cells για .NET.

## Προαπαιτούμενα

Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε:

* **Aspose.Cells for .NET** (έκδοση 23.12 ή νεότερη). Εγκαταστήστε το μέσω NuGet: `Install-Package Aspose.Cells`.
* Ένα περιβάλλον ανάπτυξης **.NET 6+** (Visual Studio 2022 ή VS Code λειτουργούν).
* Ένα βιβλίο εργασίας Excel (`Source.xlsx`) που περιέχει τα δεδομένα και τον πίνακα Pivot που θέλετε να επαναχρησιμοποιήσετε.
* Δικαιώματα εγγραφής στον φάκελο εξόδου.

Δεν απαιτούνται πρόσθετες βιβλιοθήκες τρίτων.

## Δημιουργία PowerPoint από Excel – βήμα‑βήμα

Η διαδικασία αποτελείται από τέσσερα λογικά βήματα που αντιστοιχούν άμεσα στο παράδειγμα κώδικα που θα δείτε αργότερα.

### Βήμα 1: Φόρτωση του πηγαίου βιβλίου εργασίας και ορισμός της περιοχής

Πρέπει να φορτώσετε το βιβλίο εργασίας που περιέχει τα πηγαία δεδομένα και τον πίνακα Pivot. Η επιλογή μιας ακριβούς περιοχής εξασφαλίζει ότι θα μεταφερθούν μόνο τα απαραίτητα κελιά, διατηρώντας τη διαφάνεια ελαφριά.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Γιατί είναι σημαντικό:**  
`CreateRange` δημιουργεί ένα αντικείμενο `Range` που μπορεί να αντιγραφεί ολόκληρο. Περιορίζοντας την περιοχή σε `A1:G20`, αποφεύγετε την ανάκτηση άσχετων κελιών, κάτι που διαφορετικά θα μπορούσε να αυξήσει το μέγεθος του αρχείου PowerPoint.

### Βήμα 2: Προετοιμασία του προορισμού βιβλίου εργασίας

Το Aspose.Cells αντιμετωπίζει μια διαφάνεια PowerPoint ως βιβλίο εργασίας όταν το αποθηκεύετε σε μορφή PPTX. Η δημιουργία ενός νέου βιβλίου εργασίας σας παρέχει έναν καθαρό καμβά για την αντιγραμμένη περιοχή.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Συμβουλή:** Αν χρειάζεστε πολλαπλές διαφάνειες, μπορείτε να προσθέσετε επιπλέον φύλλα εργασίας και αργότερα να αποθηκεύσετε το καθένα ως ξεχωριστό αρχείο PPTX.

### Βήμα 3: Αντιγραφή της περιοχής διατηρώντας τον πίνακα Pivot

Η μέθοδος `CopyRange` δέχεται ένα αντικείμενο `PasteOptions`. Ορίζοντας `CopyPivotTables = true` λέτε στο Aspose.Cells να διατηρήσει την δομή του πίνακα Pivot αμετάβλητη, όχι μόνο τις αποτυπωμένες τιμές.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Πώς λειτουργεί:**  
Όταν το `CopyPivotTables` είναι true, το φύλλο προορισμού λαμβάνει τόσο τα πηγαία δεδομένα όσο και την κρυφή μνήμη του Pivot. Αυτό σημαίνει ότι ο πίνακας Pivot παραμένει πλήρως λειτουργικός και μπορεί να ανανεωθεί αργότερα εάν αλλάξουν τα πηγαία δεδομένα.

### Βήμα 4: Αποθήκευση του βιβλίου εργασίας ως αρχείο PowerPoint

Τέλος, εξάγετε το βιβλίο εργασίας σε μορφή PPTX. Η σημαία `SaveFormat.Pptx` λέει στο Aspose.Cells να γράψει το φύλλο εργασίας ως διαφάνεια PowerPoint.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Αποτέλεσμα:**  
`CopyWithPivot.pptx` ανοίγει στο Microsoft PowerPoint (ή σε οποιονδήποτε συμβατό προβολέα) με μία μόνο διαφάνεια που εμφανίζει την αντιγραμμένη περιοχή, συμπεριλαμβανομένου ενός ζωντανού πίνακα Pivot που μπορεί να αλληλεπιδράσει μέσα στο PowerPoint.

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να επικολλήσετε σε ένα νέο έργο κονσόλας και να το εκτελέσετε αμέσως.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Αναμενόμενη έξοδος:**  
Η εκτέλεση του προγράμματος εκτυπώνει «PowerPoint file created successfully.» και δημιουργεί ένα αρχείο με όνομα `CopyWithPivot.pptx`. Το άνοιγμα του αρχείου στο PowerPoint εμφανίζει μία διαφάνεια όπου η αντιγραμμένη περιοχή Excel εμφανίζεται ακριβώς όπως ήταν στο πηγαίο φύλλο, με έναν ενεργό πίνακα Pivot που μπορεί να ανανεωθεί από το PowerPoint.

## Συχνές παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Τι να αλλάξετε |
|-----------|----------------|
| **Multiple pivot tables** | Ορίστε ξεχωριστά αντικείμενα `Range` για κάθε πίνακα και καλέστε `CopyRange` για το καθένα, ή αντιγράψτε ολόκληρο το φύλλο εάν μοιράζονται την ίδια πηγή δεδομένων. |
| **Large data sets** | Αυξήστε την περιοχή (π.χ., `"A1:Z5000"`). Σκεφτείτε την ενεργοποίηση του `PasteOptions.CompressData = true` για μείωση του μεγέθους του PPTX. |
| **Different slide layouts** | Μετά την αποθήκευση ως PPTX, ανοίξτε το αρχείο στο PowerPoint και εφαρμόστε προσαρμοσμένη διάταξη ή θέμα· τα δεδομένα παραμένουν επεξεργάσιμα. |
| **Saving to a stream** | Χρησιμοποιήστε `destinationWorkbook.Save(stream, SaveFormat.Pptx)` όταν χρειάζεται να επιστρέψετε το PPTX μέσω web API. |
| **Preserving cell formatting** | Ορίστε `PasteOptions.PasteType = PasteType.All` για να διατηρήσετε γραμματοσειρές, χρώματα και περιγράμματα. |

**Pro tip:** Πάντα βεβαιωθείτε ότι ο φάκελος προορισμού υπάρχει πριν καλέσετε το `Save`. Εάν λείπει ο φάκελος, το `Save` ρίχνει `DirectoryNotFoundException`.

## Συμπέρασμα

Τώρα γνωρίζετε πώς να δημιουργήσετε PowerPoint από το Excel, να αντιγράψετε έναν πίνακα Pivot και να εξάγετε το αποτέλεσμα ως αρχείο PPTX χρησιμοποιώντας το Aspose.Cells. Τα βήματα—φόρτωση του πηγαίου βιβλίου εργασίας, ορισμός περιοχής, αντιγραφή με `CopyPivotTables` και αποθήκευση ως PPTX—καλύπτουν ολόκληρη τη ροή εργασίας με αξιόπιστο, έτοιμο για παραγωγή τρόπο.

Στη συνέχεια, εξερευνήστε **πώς να εξάγετε το Excel σε PPTX** για πολλαπλά φύλλα εργασίας, ή μάθετε **πώς να αντιγράψετε περιοχές μεταξύ βιβλίων εργασίας** όταν χρειάζεται να συγχωνεύσετε δεδομένα από πολλές πηγές πριν δημιουργήσετε το σετ διαφανειών. Και τα δύο θέματα βασίζονται στην ίδια επιφάνεια API και μπορούν να συνδυαστούν για την αυτοματοποίηση σύνθετων αγωγών αναφοράς.

Καλή προγραμματιστική δουλειά και απολαύστε τη μετατροπή των υπολογιστικών φύλλων σας σε επαγγελματικές παρουσιάσεις!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω εκπαιδευτικές οδηγίες καλύπτουν στενά συναφή θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να αντιγράψετε πίνακα Pivot σε C# – Μετατροπή Excel σε PPTX, Αντιγραφή Περιοχής & Δημιουργία Πλαισίου Κειμένου](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Δημιουργία Νέου Βιβλίου Εργασίας – Πώς να αντιγράψετε ένα φύλλο εργασίας με πίνακα Pivot](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Πώς να δημιουργήσετε και να αποθηκεύσετε αρχεία Excel με Aspose.Cells για .NET: Πλήρης Οδηγός](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}