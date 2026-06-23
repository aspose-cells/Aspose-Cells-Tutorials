---
category: general
date: 2026-03-30
description: Πώς να αντιγράψετε φύλλο εργασίας σε C# χρησιμοποιώντας το Aspose.Cells
  – βήμα‑βήμα οδηγός που καλύπτει την αντιγραφή περιοχής κελιών, την αντιγραφή στηλών
  μεταξύ φύλλων, την αντιγραφή του πίνακα Pivot του φύλλου εργασίας και την προσθήκη
  κώδικα για νέο φύλλο εργασίας.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: el
og_description: Μάθετε πώς να αντιγράψετε φύλλο εργασίας σε C# με το Aspose.Cells.
  Αυτός ο οδηγός δείχνει πώς να αντιγράψετε περιοχή κελιών, να διατηρήσετε πίνακες
  Pivot, να αντιγράψετε στήλες μεταξύ φύλλων και να προσθέσετε κώδικα για νέο φύλλο
  εργασίας.
og_title: Πώς να αντιγράψετε φύλλο εργασίας σε C# – Πλήρες σεμινάριο Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Πώς να αντιγράψετε φύλλο εργασίας σε C# με το Aspose.Cells – Πλήρης οδηγός
url: /el/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Αντιγράψετε Φύλλο Εργασίας σε C# με Aspose.Cells – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να αντιγράψετε φύλλο εργασίας** σε C# χωρίς να χάσετε ούτε έναν πίνακα pivot ή τύπο; Δεν είστε μόνοι—πολλοί προγραμματιστές συναντούν πρόβλημα όταν πρέπει να διπλασιάσουν ένα φύλλο διατηρώντας όλα τα στοιχεία ανέπαφα. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα μια πρακτική, ολοκληρωμένη λύση που όχι μόνο αντιγράφει τα δεδομένα αλλά επίσης διατηρεί το **copy worksheet pivot table**, διαχειρίζεται το **copy cell range**, και δείχνει τον **add new worksheet code** που χρειάζεστε.

Θα καλύψουμε τα πάντα, από τη φόρτωση του πηγαίου workbook μέχρι την αποθήκευση του αρχείου προορισμού, ώστε να μπορείτε να **copy columns between sheets**, να διατηρήσετε αντικείμενα και να κρατήσετε τον κώδικά σας καθαρό. Χωρίς ασαφείς αναφορές, μόνο ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

## Τι Καλύπτει Αυτός ο Οδηγός

- Φόρτωση υπάρχοντος αρχείου Excel με Aspose.Cells  
- Χρήση **add new worksheet code** για δημιουργία φύλλου προορισμού  
- Ορισμός ενός **copy cell range** που περιλαμβάνει πίνακα pivot  
- Ρύθμιση **CopyOptions** για διατήρηση διαγραμμάτων, τύπων και πινάκων pivot ανέπαφων  
- Εκτέλεση **copy columns between sheets** με ακρίβεια ανά γραμμή  
- Αποθήκευση του αποτελέσματος και επαλήθευση ότι το φύλλο εργασίας αντιγράφηκε σωστά  

Στο τέλος αυτού του οδηγού θα μπορείτε να απαντήσετε με σιγουριά στην ερώτηση “how to copy worksheet”, είτε αυτοματοποιείτε αναφορές είτε δημιουργείτε UI που βασίζεται σε υπολογιστικά φύλλα.

---

## Πώς να Αντιγράψετε Φύλλο Εργασίας – Επισκόπηση

Πριν βουτήξουμε στον κώδικα, ας περιγράψουμε τη γενική ροή. Σκεφτείτε το ως μια συνταγή:

1. **Load** το πηγαίο workbook (`Source.xlsx`).  
2. **Add** ένα νέο φύλλο για να κρατήσει το αντίγραφο (`add new worksheet code`).  
3. **Define** την περιοχή που θέλετε να αντιγράψετε (`copy cell range`).  
4. **Configure** τις επιλογές αντιγραφής ώστε ο πίνακας pivot να παραμείνει (`copy worksheet pivot table`).  
5. **Copy** γραμμές και στήλες (`copy columns between sheets`).  
6. **Save** το νέο workbook (`Destination.xlsx`).  

Αυτό είναι—έξι βήματα, χωρίς μαγεία. Κάθε βήμα εξηγείται παρακάτω με αποσπάσματα κώδικα και τη λογική που τα υποστηρίζει.

---

## Βήμα 1 – Φόρτωση του Πηγαίου Workbook

Πρώτα απ’ όλα: χρειάζεστε μια παρουσία `Workbook` που να δείχνει στο αρχείο που θέλετε να αντιγράψετε. Αυτό το βήμα είναι απαραίτητο επειδή το Aspose.Cells λειτουργεί άμεσα με το σύστημα αρχείων, όχι με το UI του Office.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Why this matters:* Η φόρτωση του αρχείου δημιουργεί μια αναπαράσταση στη μνήμη για κάθε φύλλο, κελί και αντικείμενο. Χωρίς αυτό, δεν υπάρχει τίποτα για αντιγραφή, και οποιαδήποτε προσπάθεια `add new worksheet code` αργότερα θα αποτύχει επειδή τα δεδομένα πηγής δεν υπάρχουν.

## Βήμα 2 – Προσθήκη Νέου Φύλλου Εργασίας (add new worksheet code)

Τώρα χρειαζόμαστε ένα μέρος για να επικολλήσουμε τα αντιγραμμένα δεδομένα. Εδώ ξεχωρίζει ο **add new worksheet code**. Μπορείτε να ονομάσετε το φύλλο όπως θέλετε· εδώ το ονομάζουμε `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Pro tip:* Αν σκοπεύετε να αντιγράψετε πολλά φύλλα, καλέστε `Worksheets.Add` μέσα σε βρόχο και δώστε σε κάθε φύλλο ένα μοναδικό όνομα. Έτσι αποφεύγετε συγκρούσεις ονομάτων και κρατάτε το workbook σας τακτοποιημένο.

## Βήμα 3 – Ορισμός του Copy Cell Range

Ένα **copy cell range** λέει στο Aspose.Cells ακριβώς ποιες γραμμές και στήλες να διπλασιαστούν. Σε πολλές πραγματικές περιπτώσεις η περιοχή περιλαμβάνει πίνακα pivot, οπότε πρέπει να είμαστε ακριβείς.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Why we need this:* Αναφέροντας ρητά την περιοχή, αποφεύγετε την αντιγραφή ολόκληρου του φύλλου (που μπορεί να είναι σπατάλη) και εξασφαλίζετε ότι ο πίνακας pivot βρίσκεται μέσα στην αντιγραμμένη περιοχή. Αυτό είναι το κεντρικό στοιχείο του **how to copy worksheet** όταν χρειάζεστε μόνο μέρος του φύλλου.

## Βήμα 4 – Ρύθμιση Copy Options (preserve copy worksheet pivot table)

Το Aspose.Cells προσφέρει ένα αντικείμενο `CopyOptions` που ελέγχει τι θα επικολληθεί. Για να διατηρήσετε τον πίνακα pivot, τα διαγράμματα και τους τύπους, ορίζουμε `PasteType.All` και ενεργοποιούμε `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Explanation:* Το `PasteType.All` είναι η πιο περιεκτική επιλογή, ενώ το `PasteSpecial` λέει στη μηχανή να χειριστεί σωστά πολύπλοκα αντικείμενα—όπως πίνακες pivot. Η παράλειψη αυτού του βήματος είναι κοινό λάθος· το αντιγραμμένο φύλλο θα χάσει τις διαδραστικές του λειτουργίες.

## Βήμα 5 – Αντιγραφή Γραμμών και Στηλών (copy columns between sheets)

Τώρα έρχεται η βαριά δουλειά: η πραγματική μετακίνηση των δεδομένων. Θα χρησιμοποιήσουμε `CopyRows` και `CopyColumns` για να χειριστούμε το **copy columns between sheets**. Η εκτέλεση και των δύο εξασφαλίζει ότι τα συγχωνευμένα κελιά και τα πλάτη των στηλών διατηρούνται.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*What’s happening:* Το `CopyRows` μεταφέρει τα δεδομένα γραμμή‑με‑γραμμή, ενώ το `CopyColumns` κάνει το ίδιο στήλη‑με‑στήλη. Η εκτέλεση και των δύο εγγυάται ότι ολόκληρο το ορθογώνιο μπλοκ αντιγράφεται, κάτι που είναι κρίσιμο όταν πρέπει να **copy columns between sheets** που έχουν διαφορετικά πλάτη στηλών ή κρυφές στήλες.

## Βήμα 6 – Αποθήκευση του Workbook

Τέλος, γράψτε τις αλλαγές πίσω στο δίσκο. Αυτό το βήμα ολοκληρώνει τη διαδικασία **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Verification tip:* Ανοίξτε το `Destination.xlsx` και ελέγξτε ότι το φύλλο `"Copy"` φαίνεται ταυτόσημο με το αρχικό, οι πίνακες pivot λειτουργούν και τα πλάτη των στηλών ταιριάζουν. Αν κάτι φαίνεται λανθασμένο, επανεξετάστε τις ρυθμίσεις του `CopyOptions`.

## Περιπτώσεις Άκρων & Συνηθισμένες Παραλλαγές

### Αντιγραφή Πολλαπλών Φύλλων Εργασίας

Αν χρειάζεται να διπλασιάσετε αρκετά φύλλα, τυλίξτε τη λογική σε έναν βρόχο `foreach`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Διατήρηση Τύπων μεταξύ Διαφορετικών Workbook

Όταν τα πηγαία και προορισμένα workbooks έχουν διαφορετικές ονομαστικές περιοχές, ορίστε το `copyOptions` σε `PasteType.Formulas` επιπλέον του `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Μεγάλες Περιοχές και Απόδοση

Για τεράστιες βάσεις δεδομένων (εκατοντάδες χιλιάδες γραμμές), σκεφτείτε να χρησιμοποιήσετε μόνο `CopyRows` και να παραλείψετε το `CopyColumns` αν τα πλάτη των στηλών δεν είναι κρίσιμα. Αυτό μπορεί να εξοικονομήσει μερικά δευτερόλεπτα.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενσωματώνει όλα όσα συζητήσαμε. Επικολλήστε το σε μια εφαρμογή console, προσαρμόστε τις διαδρομές αρχείων και πατήστε **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Expected result:** Το άνοιγμα του `Destination.xlsx` δείχνει ένα φύλλο με όνομα **Copy** που αντικατοπτρίζει το πρώτο φύλλο του `Source.xlsx`—συμπεριλαμβανομένων τυχόν πινάκων pivot, μορφοποίησης και πλάτους στηλών. Το αρχικό αρχείο παραμένει αμετάβλητο.

## Συχνές Ερωτήσεις

**Q: Λειτουργεί αυτό με αρχεία .xlsx που δημιουργήθηκαν από το Excel 2019;**  
A: Απόλυτα. Το Aspose.Cells υποστηρίζει όλες τις σύγχρονες μορφές Excel, οπότε ο ίδιος κώδικας λειτουργεί για `.xlsx`, `.xlsm` και ακόμη και παλαιότερα αρχεία `.xls`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}