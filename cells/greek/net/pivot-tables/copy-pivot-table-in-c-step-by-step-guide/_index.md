---
category: general
date: 2026-03-18
description: Αντιγραφή πίνακα Pivot σε C# με το Aspose.Cells. Μάθετε πώς να αντιγράψετε
  περιοχή Excel, να διπλασιάσετε πίνακα Pivot Excel, να αντιγράψετε περιοχή σε νέο
  φύλλο και να αντιγράψετε πίνακα Pivot σε φύλλο σε λίγα λεπτά.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: el
og_description: Αντιγραφή πίνακα Pivot σε C# χρησιμοποιώντας το Aspose.Cells. Μάθετε
  πώς να διπλασιάζετε έναν πίνακα Pivot του Excel, να αντιγράφετε μια περιοχή του
  Excel σε νέα θέση και να μεταφέρετε τον πίνακα Pivot σε φύλλο με πλήρη παραδείγματα
  κώδικα.
og_title: Αντιγραφή πίνακα Pivot σε C# – Πλήρης Οδηγός Προγραμματισμού
tags:
- Aspose.Cells
- C#
- Excel automation
title: Αντιγραφή πίνακα Pivot σε C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αντιγραφή πίνακα Pivot σε C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε ποτέ χρειαστεί να **copy pivot table** από ένα τμήμα ενός βιβλίου εργασίας σε άλλο, αλλά δεν ήσασταν σίγουροι πώς να το κάνετε χωρίς να χάσετε τις υποκείμενες συνδέσεις δεδομένων; Δεν είστε μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν αυτοματοποιούν αναφορές Excel, ειδικά όταν το pivot βρίσκεται μέσα σε ένα μεγαλύτερο μπλοκ δεδομένων. Τα καλά νέα; Με το Aspose.Cells μπορείτε να αντιγράψετε τον πίνακα pivot **exactly as it appears**, και θα μάθετε επίσης πώς να **copy excel range**, **duplicate excel pivot**, και ακόμη **copy pivot to sheet** με λίγες μόνο γραμμές C#.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό σενάριο: τη μετακίνηση ενός pivot που καταλαμβάνει *A1:J20* σε μια νέα περιοχή *M1:V20* στο ίδιο φύλλο εργασίας. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα, θα κατανοήσετε γιατί κάθε βήμα είναι σημαντικό, και θα ξέρετε πώς να προσαρμόσετε τον κώδικα για άλλες περιοχές ή ακόμη και ξεχωριστά φύλλα εργασίας. Δεν χρειάζονται εξωτερικά έγγραφα — όλα είναι εδώ.

---

## Προαπαιτούμενα

- **Aspose.Cells for .NET** (έκδοση 23.9 ή νεότερη). Μπορείτε να το αποκτήσετε μέσω NuGet: `Install-Package Aspose.Cells`.
- Ένα βασικό περιβάλλον ανάπτυξης C# (Visual Studio 2022, Rider ή VS Code με την επέκταση C#).
- Ένα αρχείο Excel (`source.xlsx`) που περιέχει έναν πίνακα pivot εντός της περιοχής *A1:J20*.

Αυτό είναι όλο. Αν είστε άνετοι με τη δημιουργία μιας εφαρμογής κονσόλας, είστε έτοιμοι να ξεκινήσετε.

---

## Πώς να αντιγράψετε πίνακα pivot στο Aspose.Cells

Ο πυρήνας της λύσης είναι μια ενιαία κλήση στο `Worksheet.Cells.CopyRange`. Αυτή η μέθοδος όχι μόνο αντιγράφει τις ακατέργαστες τιμές κελιών, αλλά επίσης διατηρεί αυτόματα πίνακες pivot, γραφήματα και άλλα πλούσια αντικείμενα. Ας το αναλύσουμε.

### Βήμα 1: Φόρτωση του πηγαίου βιβλίου εργασίας

Πρώτα πρέπει να φορτώσουμε το βιβλίο εργασίας στη μνήμη.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Why this matters:** Η φόρτωση του βιβλίου εργασίας δημιουργεί μια αναπαράσταση στη μνήμη που το Aspose.Cells μπορεί να χειριστεί χωρίς να εκκινήσει το Excel. Είναι γρήγορη, ασφαλής για νήματα και λειτουργεί σε διακομιστές.

### Βήμα 2: Λήψη του πρώτου φύλλου εργασίας

Οι περισσότερες παραδείγματα χρησιμοποιούν το πρώτο φύλλο, αλλά μπορείτε να στοχεύσετε οποιοδήποτε δείκτη ή όνομα.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Tip:** Αν χρειάζεται να **copy pivot to sheet** αντί για το ίδιο φύλλο, απλώς αλλάξτε την αναφορά `worksheet` σε ένα άλλο αντικείμενο `Worksheet`.

### Βήμα 3: Ορισμός των πηγών και προορισμού περιοχών

Θα χρησιμοποιήσουμε δομές `CellArea` για να περιγράψουμε τα μπλοκ που μετακινούμε.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Explanation:** Οι δείκτες γραμμών και στηλών είναι μηδενικής βάσης. Στήλη 0 = **A**, στήλη 12 = **M**, κ.λπ. Προσαρμόστε αυτούς τους αριθμούς αν το pivot βρίσκεται σε άλλη θέση.

### Βήμα 4: Εκτέλεση της λειτουργίας αντιγραφής

Τώρα συμβαίνει η μαγεία. Ορίζοντας την τελευταία παράμετρο boolean σε `true` λέει στο Aspose.Cells να αντιγράψει όλα τα αντικείμενα — συμπεριλαμβανομένου του pivot.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Why `true`?** Η σημαία υποδηλώνει “copy all objects”. Αν τη θέσετε σε `false`, θα μετακινηθούν μόνο απλές τιμές κελιών και το pivot θα χαθεί.

### Βήμα 5: Αποθήκευση του βιβλίου εργασίας

Τέλος, γράψτε το τροποποιημένο βιβλίο εργασίας πίσω στο δίσκο.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Result:** Το `copy-pivot.xlsx` περιέχει τώρα το αρχικό pivot στο *A1:J20* **και** ένα πανομοιότυπο αντίγραφο στο *M1:V20*. Ανοίξτε το αρχείο στο Excel για να επαληθεύσετε ότι και τα δύο pivots λειτουργούν και διατηρούν τις συνδέσεις δεδομένων τους.

---

## Αντιγραφή περιοχής Excel σε νέα θέση – μια γρήγορη παραλλαγή

Μερικές φορές χρειάζεται μόνο να **copy excel range** χωρίς να ανησυχείτε για pivots. Η ίδια μέθοδος `CopyRange` κάνει τη δουλειά· απλώς ορίστε το τελευταίο όρισμα σε `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **When to use:** Αν μετακινείτε ακατέργαστα δεδομένα για ένα προσωρινό φύλλο υπολογισμών, η απενεργοποίηση της αντιγραφής αντικειμένων εξοικονομεί μνήμη και επιταχύνει τη λειτουργία.

---

## Δημιουργία αντιγράφου excel pivot σε πολλαπλά φύλλα

Τι γίνεται αν θέλετε να **duplicate excel pivot** σε διαφορετικό φύλλο εργασίας; Το μοτίβο παραμένει το ίδιο· απλώς αναφέρετε ένα άλλο `Worksheet` ως προορισμό.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Edge case:** Αν το πηγαίο pivot χρησιμοποιεί έναν πίνακα που βρίσκεται στο αρχικό φύλλο, το Aspose.Cells θα αντιγράψει επίσης τον υποκείμενο ορισμό του πίνακα, εξασφαλίζοντας ότι το νέο pivot λειτουργεί αμέσως.

---

## Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| **Pivot loses its cache** | Χρήση του `CopyRange` με `false` ή προσαρμοσμένη ρουτίνα αντιγραφής που αγνοεί τα αντικείμενα. | Πάντα περάστε `true` όταν χρειάζεστε το ίδιο το pivot. |
| **Target cells already contain data** | Αντικαθιστά σιωπηλά, ενδεχομένως καταστρέφοντας υπάρχουσες τύπους. | Καθαρίστε πρώτα την περιοχή προορισμού: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **Source range doesn’t include the whole pivot** | Οι πίνακες pivot εκτείνονται σε περισσότερες γραμμές/στήλες από ό,τι περιμένετε (π.χ., κρυφές γραμμές). | Χρησιμοποιήστε `worksheet.PivotTables[0].DataRange` για να λάβετε προγραμματιστικά τα ακριβή όρια. |
| **Copying between workbooks** | Το `CopyRange` λειτουργεί μόνο εντός του ίδιου βιβλίου εργασίας. | Χρησιμοποιήστε `sourceWorksheet.Cells.CopyRange` σε μια προσωρινή περιοχή, έπειτα `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## Αναμενόμενο αποτέλεσμα & επαλήθευση

Μετά την εκτέλεση του προγράμματος:

1. Ανοίξτε το `copy-pivot.xlsx`.
2. Θα δείτε δύο ταυτόσημους πίνακες pivot — ένας στο **A1:J20**, άλλος στο **M1:V20**.
3. Ανανέωση οποιουδήποτε pivot· και οι δύο πρέπει να αντανακλούν τα ίδια υποκείμενα δεδομένα.
4. Αν δημιουργήσατε αντίγραφο σε άλλο φύλλο, το νέο φύλλο θα περιέχει επίσης μια λειτουργική αντιγραφή.

Ένας γρήγορος τρόπος επαλήθευσης μέσω κώδικα:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Συμβουλή επαγγελματία: Αυτοματοποιήστε την ανίχνευση περιοχής

Η σκληρή κωδικοποίηση του `CellArea` λειτουργεί για στατικές αναφορές, αλλά ο κώδικας παραγωγής συχνά χρειάζεται να εντοπίζει το pivot δυναμικά.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Why bother?** Αυτό κάνει τη λύση σας ανθεκτική στις αλλαγές διάταξης — χωρίς άλλα σφάλματα “Ωχ, το pivot μετακινήθηκε στο B2”.

![παράδειγμα αντιγραφής πίνακα pivot](copy-pivot.png){alt="παράδειγμα αντιγραφής πίνακα pivot"}

*Το στιγμιότυπο (placeholder) δείχνει το αρχικό pivot στα αριστερά και το αντίγραφο στα δεξιά.*

---

## Σύνοψη

Μόλις καλύψαμε πώς να **copy pivot table** σε C# χρησιμοποιώντας το Aspose.Cells, εξετάσαμε τρόπους για **copy excel range**, **duplicate excel pivot**, και ακόμη **copy pivot to sheet** μεταξύ φύλλων εργασίας. Τα κύρια σημεία είναι:

- Χρησιμοποιήστε το `Worksheet.Cells.CopyRange` με τη σημαία `true` για να διατηρήσετε τα πλούσια αντικείμενα.
- Ορίστε τα αντικείμενα `CellArea` πηγής και προορισμού με δείκτες μηδενικής βάσης.
- Προσαρμόστε το φύλλο προορισμού εάν χρειάζεται να **copy pivot to sheet**.
- Προσέξτε περιπτώσεις όπως υπάρχοντα δεδομένα, κρυφές γραμμές και σενάρια μεταξύ βιβλίων εργασίας.

---

## Τι θα ακολουθήσει;

- **Dynamic pivot discovery**: Δημιουργήστε ένα βοηθητικό εργαλείο που σαρώνει ένα βιβλίο εργασίας για όλα τα pivots και τα αντιγράφει αυτόματα.
- **Export to PDF/HTML**: Μετά την αντιγραφή, ίσως θέλετε να αποδώσετε το φύλλο σε μορφή αναφοράς — το Aspose.Cells το διαχειρίζεται επίσης.
- **Performance tuning**: Για τεράστια βιβλία εργασίας, σκεφτείτε να απενεργοποιήσετε τον υπολογισμό πριν από την αντιγραφή και να τον ενεργοποιήσετε ξανά μετά.

Νιώστε ελεύθεροι να πειραματιστείτε: αλλάξτε τις συντεταγμένες προορισμού, αντιγράψτε σε ένα ολοκαίνουργιο βιβλίο εργασίας, ή ακόμη κάντε βρόχο σε πολλαπλά φύλλα εργασίας για να δημιουργήσετε μια ενοποιημένη αναφορά. Οι δυνατότητες είναι ατελείωτες, και με τη βάση που έχετε τώρα, θα μπορείτε να προσαρμόσετε τον κώδικα σε σχεδόν οποιαδήποτε εργασία αυτοματοποίησης Excel.

Καλό προγραμματισμό, και οι πίνακες pivot σας να παραμένουν πάντα τέλεια συγχρονισμένοι!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}