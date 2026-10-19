---
category: general
date: 2026-06-24
description: Δημιουργήστε νέο βιβλίο εργασίας σε C# και αντιγράψτε τον πίνακα Pivot
  διατηρώντας τα δεδομένα του. Μάθετε πώς να αντιγράψετε γραμμές, να εξάγετε το επιλεγμένο
  εύρος και να διατηρήσετε τον πίνακα Pivot αμετάβλητο.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: el
og_description: Δημιουργήστε νέο βιβλίο εργασίας σε C# και αντιγράψτε έναν πίνακα
  Pivot διατηρώντας τα δεδομένα του. Οδηγός βήμα‑βήμα που καλύπτει πώς να αντιγράψετε
  γραμμές και να εξάγετε το επιλεγμένο εύρος.
og_title: Δημιουργία νέου βιβλίου εργασίας σε C# – Αντιγραφή πίνακα Pivot
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Δημιουργία νέου βιβλίου εργασίας σε C# – Αντιγραφή Πίνακα Pivot
url: /el/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Νέου Βιβλίου Εργασίας σε C# – Αντιγραφή Πίνακα Pivot

Ποτέ χρειάστηκε να **δημιουργήσετε νέο βιβλίο εργασίας** σε C# μόνο για να μετακινήσετε ένα τμήμα δεδομένων που περιλαμβάνει πίνακα pivot; Δεν είστε οι μόνοι. Σε πολλές αλυσίδες αναφορών παίρνετε μερικές γραμμές, ίσως μερικές στήλες, και περιμένετε ο pivot να παραμείνει ακριβώς όπως ήταν — χωρίς σπασμένες αναφορές, χωρίς ελλιπείς υπολογισμούς.  

Τα καλά νέα; Με λίγες γραμμές κώδικα Aspose.Cells μπορείτε να **αντιγράψετε πίνακα pivot**, να τον διατηρήσετε αμετάβλητο και ακόμη να **εξάγετε επιλεγμένο εύρος** χωρίς να σπάσει τίποτα. Παρακάτω θα δείτε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει **πώς να αντιγράψετε γραμμές**, να διατηρήσετε τον pivot και να αποθηκεύσετε το αποτέλεσμα ως ένα ολοκαίνουργιο βιβλίο εργασίας.

## Τι Καλύπτει Αυτό το Tutorial

- Ρύθμιση ενός έργου C# με Aspose.Cells (η βιβλιοθήκη που τροφοδοτεί τον κώδικα).
- Φόρτωση του πηγαίου βιβλίου εργασίας που περιέχει τον αρχικό pivot.
- Χρήση των μεθόδων `CopyRows` και `CopyColumns` της βιβλιοθήκης για αντιγραφή του ακριβούς εύρους που χρειάζεστε.
- Αποθήκευση του αντιγραμμένου τμήματος σε σενάριο **δημιουργίας νέου βιβλίου εργασίας** ενώ ο pivot παραμένει λειτουργικός.
- Συμβουλές για ειδικές περιπτώσεις όπως πολλαπλοί πίνακες pivot, κρυμμένες γραμμές και μεγάλα σύνολα δεδομένων.

Στο τέλος αυτού του οδηγού θα μπορείτε να **εξάγετε επιλεγμένο εύρος** από οποιοδήποτε αρχείο Excel, να διατηρήσετε τη λογική του pivot ζωντανή και να αποθηκεύσετε το νέο αρχείο όπου θέλετε.

> **Προαπαιτούμενο**: Aspose.Cells for .NET (δωρεάν δοκιμή ή άδεια) εγκατεστημένο μέσω NuGet. Αν δεν το έχετε προσθέσει ακόμη, εκτελέστε `dotnet add package Aspose.Cells` στο φάκελο του έργου σας.

---

## Δημιουργία Νέου Βιβλίου Εργασίας και Αντιγραφή Πίνακα Pivot

Παρακάτω είναι η καρδιά της λύσης. Θα περάσουμε από κάθε γραμμή, θα εξηγήσουμε γιατί είναι σημαντική και στη συνέχεια θα δείξουμε το πλήρες πρόγραμμα.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Γιατί Λειτουργεί Αυτό

- **`CopyRows` / `CopyColumns`**: Αυτές οι μέθοδοι αντιγράφουν τα υποκείμενα δεδομένα κελιών *και* τα συναφή αντικείμενα (όπως την κρυφή μνήμη pivot). Γι’ αυτό ο pivot παραμένει λειτουργικός μετά τη μετακίνηση.
- **Ξεχωριστό προοριστικό βιβλίο εργασίας**: Δημιουργώντας μια νέα παρουσία `Workbook` **δημιουργούμε νέο βιβλίο εργασίας** χωρίς υπόλοιπο μορφοποίησης ή κρυφά φύλλα που θα μπορούσαν να παρεμβούν.
- **Δεικτοδότηση από το μηδέν**: Το Aspose.Cells χρησιμοποιεί δείκτες που ξεκινούν από το 0, έτσι το `0` αντιστοιχεί στο κελί **A1**. Προσαρμόστε τα `startRow`/`startColumn` αν ο pivot σας δεν βρίσκεται στην πάνω‑αριστερή γωνία.
- **Διατήρηση πίνακα pivot**: Η μνήμη του pivot βρίσκεται στο ίδιο εύρος, οπότε η αντιγραφή του εύρους αντιγράφει αυτόματα και τη μνήμη. Δεν χρειάζεται επιπλέον κώδικας.

---

## Πώς να Αντιγράψετε Γραμμές Χωρίς να Σπάσετε τον Pivot

Αν σας ενδιαφέρει μόνο το τμήμα αντιγραφής γραμμών, μπορείτε να το απομονώσετε:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Συμβουλή**: Όταν αντιγράφετε γραμμές που διασχίζουν έναν πίνακα pivot, αντιγράψτε πάντα *ολόκληρη* την περιοχή του pivot (γραμμές + στήλες). Μερικές αντιγραφές μπορεί να αφήσουν τον pivot με ελλιπή πεδία, προκαλώντας σφάλματα `#REF!`.

---

## Εξαγωγή Επιλεγμένου Εύρους – Σενάριο Πραγματικού Κόσμου

Φανταστείτε ότι έχετε ένα τεράστιο βιβλίο εργασίας πωλήσεων, αλλά ο πελάτης σας θέλει μόνο τη σύνοψη του πρώτου τριμήνου, η οποία βρίσκεται στις γραμμές 1‑20 και στήλες A‑D. Το παραπάνω απόσπασμα **εξάγει επιλεγμένο εύρος** για εσάς. Απλώς αλλάξτε τις μεταβλητές `totalRows` και `totalColumns` ώστε να ταιριάζουν με το αίτημα του πελάτη, και τελειώσατε.

### Διαχείριση Κρυμμένων Γραμμών ή Φίλτρων

Αν το πηγαίο φύλλο έχει κρυμμένες γραμμές (ίσως φιλτραρισμένες), ίσως θέλετε να αντιγράψετε μόνο τις *ορατές* γραμμές. Το Aspose.Cells προσφέρει υπερφορτώσεις της `CopyRows` που σέβονται την ορατότητα:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Ορίστε το τελευταίο boolean σε `true` για να αντιγράψετε μόνο τις ορατές γραμμές — ιδανικό για “εξαγωγή επιλεγμένου εύρους” όταν ο χρήστης έχει εφαρμόσει φίλτρα.

---

## Διατήρηση Πίνακα Pivot – Συνηθισμένα Πάγια & Πώς να τα Αποφύγετε

| Πάγιο | Γιατί Συμβαίνει | Διόρθωση |
|---------|----------------|-----|
| **Η μνήμη pivot δεν αντιγράφηκε** | Χρήση του απλού `Range.Copy` αντί των `Cells.CopyRows/CopyColumns`. | Χρησιμοποιήστε τις μεθόδους `Cells` όπως φαίνεται. |
| **Το προοριστικό φύλλο έχει υπάρχον pivot** | Αποθήκευση πάνω από βιβλίο εργασίας που ήδη περιέχει pivot με το ίδιο όνομα. | Ξεκινήστε με ένα φρέσκο `Workbook()` (όπως κάνουμε). |
| **Οι ονομασμένες περιοχές σπάζουν** | Ο πηγαίος pivot αναφέρεται σε ονομασμένη περιοχή που δεν υπάρχει στο νέο αρχείο. | Αντιγράψτε και την ονομασμένη περιοχή: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Η διαδρομή πηγής δεδομένων αλλάζει** | Ο pivot δείχνει σε εξωτερική πηγή δεδομένων που δεν είναι διαθέσιμη. | Χρησιμοποιήστε `PivotTable.RefreshData()` μετά την αντιγραφή αν χρειάζεται. |

---

## Πλήρες Παράδειγμα Από‑Από‑Τέλος (Έτοιμο για Εκτέλεση)

Παρακάτω είναι το πλήρες πρόγραμμα, συμπεριλαμβανομένων των `using` δηλώσεων και ενός σύντομου UI κονσόλας. Αντιγράψτε‑και‑επικολλήστε το σε ένα νέο έργο Console App και πατήστε **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Αναμενόμενη έξοδος** (στην κονσόλα):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Ανοίξτε το `copy-pivot.xlsx` και θα δείτε τον ίδιο πίνακα pivot που είχατε στο `source.xlsx`, πλήρως λειτουργικό και με αναφορά στο αντιγραμμένο εύρος δεδομένων.

---

## Συχνές Ερωτήσεις

**Ε: Λειτουργεί αυτό με πολλαπλούς πίνακες pivot στο ίδιο φύλλο;**  
Α: Ναι, εφόσον το αντιγραμμένο ορθογώνιο περιλαμβάνει κάθε pivot που χρειάζεστε. Αν θέλετε μόνο έναν, προσαρμόστε τα `rows`/`cols` ώστε να τον απομονώσετε.

**Ε: Τι γίνεται αν το πηγαίο βιβλίο εργασίας χρησιμοποιεί εξωτερικές συνδέσεις δεδομένων;**  
Α: Η μνήμη του pivot θα συνεχίσει να δείχνει στην αρχική σύνδεση. Καλέστε `pivotTable.RefreshData()` μετά τη φόρτωση του προορισμού αν θέλετε να επαναλάβετε το ερώτημα στην πηγή.

**Ε: Μπορώ να αντιγράψω τον pivot σε διαφορετικό φύλλο μέσα στο ίδιο βιβλίο εργασίας;**  
Α: Απόλυτα. Αντικαταστήστε το `destinationWorkbook` με `sourceWorkbook` και επιλέξτε έναν άλλο δείκτη φύλλου.

**Ε: Υπάρχει τρόπος να αντιγράψω μόνο τη μορφοποίηση;**  
Α: Χρησιμοποιήστε τις υπερφορτώσεις `CopyRows`/`CopyColumns` που δέχονται αντικείμενο `CopyOptions` — ορίστε `CopyOptions.CopyType = CopyType.ValuesOnly` ή `CopyType.All` ανάλογα με τις ανάγκες σας.

---

## Συμπέρασμα

Μόλις περάσαμε από ένα σενάριο **δημιουργίας νέου βιβλίου εργασίας** που **αντιγράφει πίνακα pivot**, **διατηρεί τον πίνακα pivot** και **εξάγει επιλεγμένο εύρος** — όλα σε καθαρό C#.

## Τι Πρέπει να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη, λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [Create a New Pivot Table Programmatically in .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [How to Manage Excel Pivot Table Compatibility with Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}